---
title: "Visualización de datos de diagnóstico | Microsoft Docs"
description: "Vea datos de diagnóstico y de uso para confirmar que la jerarquía de System Center Configuration Manager no contiene información confidencial."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 5b5d6b6c176de8acbc1161f6820aa1cc3e9fca49


---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Visualización de datos de diagnóstico y uso para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede ver datos de diagnóstico y de uso de la jerarquía de System Center Configuration Manager para confirmar que no se incluye información confidencial o de identificación. Los datos de telemetría se resumen y se almacenan en la tabla **TEL_TelemetryResults** de la base de datos del sitio y se les aplica formato para que sean eficientes y útiles en programación. Aunque las opciones siguientes proporcionan una visión de los datos exactos que se envían a Microsoft, no se pretenden usar para otros propósitos, como el análisis de datos.  

El siguiente comando SQL puede usarse para ver el contenido de esta tabla y muestra los datos exactos que se envían (también puede exportar estos datos a un archivo de texto):  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  Antes de instalar la versión 1602, la tabla que almacena los datos de telemetría es **TelemetryResults**.  

Cuando el punto de conexión de servicio está en modo sin conexión, puede usar la herramienta de conexión de servicio para exportar los datos de diagnóstico y uso actuales a un archivo de valores separados por comas (CSV). Ejecute la herramienta de conexión de servicio en el punto de conexión de servicio con el parámetro **-Export**.  

##  <a name="a-namebkmkhashesa-one-way-hashes"></a><a name="bkmk_hashes"></a> Valores hash unidireccionales  
Algunos de los datos consisten en cadenas de caracteres alfanuméricos aleatorios. Configuration Manager usa valores hash unidireccionales con el algoritmo SHA-256 para garantizar que no se recopilan datos potencialmente confidenciales, pero los deja en un estado en el que todavía se pueden usar para la comparación y la correlación. Por ejemplo, en lugar de recopilar los nombres de tablas en la base de datos del sitio, se captura un hash unidireccional para cada nombre de tabla. Esto garantiza que no están visibles los nombres de tabla personalizados que ha creado usted o complementos de terceros del producto. A continuación, podemos realizar el mismo hash unidireccional de los nombres de la tabla SQL que se distribuyen de forma predeterminada en el producto y compararlos para determinar la desviación de su esquema de base de datos con el valor predeterminado del producto. A continuación, se usa para mejorar las actualizaciones que requieren cambios en el esquema SQL.  

Cuando se consultan los datos sin procesar, aparecerá un valor de hash común en cada fila de datos. Este es el identificador de la jerarquía. Este valor de hash se utiliza para garantizar que los datos se correlacionan con la misma jerarquía sin identificar el cliente o el origen.  

#### <a name="to-see-how-the-one-way-hash-works"></a>Para ver cómo funciona el algoritmo hash unidireccional  

1.  Obtenga el identificador de la jerarquía mediante la ejecución de la instrucción SQL siguiente en SQL Management Studio en la base de datos de Configuration Manager: **select [dbo].[fnGetHierarchyID](\)**  

2.  Luego, use el siguiente script de Windows PowerShell para llevar a cabo el hash unidireccional del GUID obtenido de la base de datos. A continuación, puede compararlo con el identificador de la jerarquía de los datos sin procesar para ver cómo se ocultan estos datos.  

    ```  
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
         #many of the values we hash are Guids  
         $bytesToHash = $guid.ToByteArray()  
    } else {  
         #otherwise hash as string (unicode)  
         $ue = New-Object System.Text.UnicodeEncoding  
         $bytesToHash = $ue.GetBytes($value)   
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)   
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()    
    # Hash the input   
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)              
    # Base64 encode the result for transport   
    $result = [Convert]::ToBase64String($hashedBytes)    
    return $result   
    ```  



<!--HONumber=Dec16_HO3-->


