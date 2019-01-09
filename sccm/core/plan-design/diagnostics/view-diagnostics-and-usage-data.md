---
title: Visualización de datos de diagnóstico
titleSuffix: Configuration Manager
description: Vea datos de diagnóstico y de uso para confirmar que la jerarquía de System Center Configuration Manager no contiene información confidencial.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cce48cad13eaa37221e0ee9dca3b1923bb902bc4
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416238"
---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Visualización de datos de diagnóstico y uso para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede ver datos de diagnóstico y de uso de la jerarquía de System Center Configuration Manager para confirmar que no se incluye información confidencial o de identificación. Los datos de telemetría se resumen y se almacenan en la tabla **TEL_TelemetryResults** de la base de datos del sitio y se les aplica formato para que sean eficientes y útiles en programación. Aunque las opciones siguientes proporcionan una visión de los datos exactos que se envían a Microsoft, no se pretenden usar para otros propósitos, como el análisis de datos.  

Use el siguiente comando de SQL para ver el contenido de esta tabla y mostrar los datos exactos que se envían. (También puede exportar estos datos en un archivo de texto):  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  Antes de instalar la versión 1602, la tabla que almacena los datos de telemetría es **TelemetryResults**.  

Cuando el punto de conexión de servicio está en modo sin conexión, puede usar la herramienta de conexión de servicio para exportar los datos de diagnóstico y uso actuales a un archivo de valores separados por comas (CSV). Ejecute la herramienta de conexión de servicio en el punto de conexión de servicio con el parámetro **-Export**.  

##  <a name="bkmk_hashes"></a> Valores hash unidireccionales  
Algunos datos consisten en cadenas de caracteres alfanuméricos aleatorios. Configuration Manager usa el algoritmo SHA-256, que usa hashes unidireccionales, para garantizar que no recopilamos datos potencialmente confidenciales. El algoritmo deja los datos en un estado en el que todavía puedan usarse con fines de comparación y correlación. Por ejemplo, en lugar de recopilar los nombres de tablas en la base de datos del sitio, se captura un hash unidireccional para cada nombre de tabla. Esto garantiza que cualquier nombre de tabla personalizado que ha creado o complementos de productos de terceros no estén visibles. A continuación, podemos realizar el mismo hash unidireccional de los nombres de la tabla SQL que se distribuyen de manera predeterminada en el producto y comparar los resultados de las dos consultas para determinar la desviación de su esquema de base de datos con el valor predeterminado del producto. A continuación, se usa para mejorar las actualizaciones que requieren cambios en el esquema SQL.  

Cuando se consultan los datos sin procesar, aparecerá un valor de hash común en cada fila de datos. Este es el identificador de la jerarquía. Este valor de hash se usa para garantizar que los datos se correlacionan con la misma jerarquía sin identificar el cliente o el origen.  

#### <a name="to-see-how-the-one-way-hash-works"></a>Para ver cómo funciona el algoritmo hash unidireccional  

1.  Obtenga el identificador de la jerarquía mediante la ejecución de la instrucción SQL siguiente en SQL Management Studio en la base de datos de Configuration Manager: **select [dbo].[fnGetHierarchyID]\(\)**.  

2.  Use el siguiente script de Windows PowerShell para llevar a cabo el hash unidireccional del GUID que se ha obtenido de la base de datos. A continuación, puede compararlo con el identificador de la jerarquía de los datos sin procesar para ver cómo se ocultan estos datos.  

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
