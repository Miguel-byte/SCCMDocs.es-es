---
title: Instalar y configurar extensiones de Security Content Automation Protocol (SCAP)
titleSuffix: System Center Configuration Manager
description: Instalar y configurar extensiones de Security Content Automation Protocol (SCAP)
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 03fc9fa9f82aeae8ab22d6b4c3fa7858e93401cc
ms.sourcegitcommit: 27da4be015f1496b7b89ebddb517a2685f1ecf74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="install-and-configure-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Instalar y configurar extensiones SCAP para Microsoft System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

> [!Tip]  
> Esta característica se introdujo por primera vez en la versión preliminar técnica 1803 como una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). Esta versión preliminar de las extensiones SCAP puede instalarse en cualquier versión admitida de Rama actual de Configuration Manager y LTSB 1606. El archivo de instalación se encuentra en cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi a partir de 1803 Technical Preview.   

Después de preparar la infraestructura de requisitos previos, ya está listo para instalar y configurar las extensiones SCAP para Microsoft System Center Configuration Manager en el equipo en el que quiera ejecutar este proceso.

## <a name="install-scap-extensions-configuration-manager"></a>Instalación de SCAP Extensions Configuration Manager

1. Ejecute ConfigMgr\_Extensions\_for\_SCAP.msi para instalar la herramienta.
2. En el Explorador de Windows, vaya a la carpeta donde descargó el archivo **ConfigMgr\_Extensions\_for\_SCAP.msi** y, después, haga doble clic en el archivo **ConfigMgr\_Extensions\_for\_SCAP.msi**. Se inicia SCAP Extensions for Microsoft System Center Configuration Manager Installation Wizard (Asistente para la instalación de extensiones SCAP para Microsoft System Center Configuration Manager).

Siga los pasos de **SCAP Extensions for Microsoft System Center Configuration Manager Installation Wizard** (Asistente para la instalación de extensiones SCAP para Microsoft System Center Configuration Manager) usando la información de esta tabla y acepte los valores predeterminados del asistente, a menos que necesite especificar otros valores.

**Tabla 1.0** Proceso de SCAP Extensions for Microsoft System Center Configuration Manager Installation Wizard (Asistente para la instalación de extensiones SCAP para Microsoft System Center Configuration Manager)

| Nombre de página del Asistente | Acción del usuario |
| --- | --- |
| Welcome and End-User License Agreement (Bienvenida y contrato de licencia para el usuario final) |1. Revise el contrato de licencia.|
| Welcome and End-User License Agreement (Bienvenida y contrato de licencia para el usuario final)|2. Haga clic en **Acepto los términos del Contrato de licencia**.|
| Welcome and End-User License Agreement (Bienvenida y contrato de licencia para el usuario final)|3. Haga clic en **Instalar**.|
| Complete el Asistente para la instalación de SCAP Extensions para Microsoft System Center Configuration Manager. |4. Haga clic en **Finalizar**.|
 



SCAP Extensions for Microsoft System Center Configuration Manager (Asistente para la instalación de extensiones SCAP para Microsoft System Center Configuration Manager) instala las extensiones de forma predeterminada en la carpeta de instalación de la consola de Configuration Manager.



## <a name="download-and-install-the-scap-data-stream-files"></a>Descargar e instalar los archivos de flujo de datos de SCAP

Para poder ejecutar las extensiones SCAP para convertir archivos de flujo de datos SCAP y, después, importarlos a la característica Configuración de cumplimiento, debe descargar los archivos de flujo de datos SCAP de la [página de descarga](http://nvd.nist.gov/fdcc/download_fdcc.cfm) de National Vulnerability Database (NVD). Después, cópielos en la carpeta donde instaló las extensiones SCAP.

Dependiendo de su entorno, es posible que no necesite todos los archivos de flujo de datos SCAP que se muestran en la página de descarga.

Para instalar los flujos de datos SCAP

1. Visite el [sitio web de NVD](http://nvd.nist.gov/) para identificar los flujos de datos SCAP que requiere su organización.
Los flujos de datos SCAP publicados por el NIST se organizan en varios paquetes, que también se denominan _listas de comprobación_.

2. Descargue los flujos de datos SCAP desde el [sitio web de NVD](http://nvd.nist.gov/home.cfm). Están almacenados en archivos comprimidos con una extensión de nombre de archivo .zip o marcados como archivos XML DataStream.

    >[!IMPORTANT] 
    >Hay muchos archivos de flujo de datos SCAP con la extensión .xml que puede descargar desde el NVD. Pero solo los archivos .xml que incluyen contenido XCCDF (SCAP 1.0 y 1.1)/DataStream (SCAP 1.2) son adecuados para usarlos con las extensiones SCAP.

3. Extraiga los archivos .zip de flujo de datos SCAP/archivo DataStream XML que descargó en la misma carpeta donde instaló SCAP Extensions.

## <a name="convert-and-import-the-scap-data-stream-files-using-the-import-scap-content-wizard"></a>Convertir e importar archivos de flujo de datos SCAP mediante Import SCAP Content Wizard (Asistente para importar contenido de SCAP)

Después de obtener los flujos de datos SCAP, ya puede importar y convertir los flujos de datos en líneas base de configuración. Los flujos de datos SCAP publicados por el NIST se organizan en varios paquetes. Siga las instrucciones del NIST para comprobar qué paquetes debe usar en su entorno. Por ejemplo, hay un paquete diferente para cada versión de Windows, otro paquete específico de versión para la configuración del firewall y un paquete para Internet Explorer 8.0. Use los procedimientos siguientes para realizar esta tarea.

### <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>Para importar los flujos de datos SCAP a Configuration Manager

1. Inicie Import SCAP Content Wizard (Asistente para importar contenido de SCAP) desde la cinta de la línea base de configuración.

     ![Iniciar Import SCAP Content Wizard (Asistente para importar contenido de SCAP) desde la cinta de línea de base de CI](./media/import-scap-content.png)

2. Seleccione el tipo de contenido.

      ![Seleccionar tipo de contenido](./media/import-new-scap-content.png)

3. Seleccione el archivo de flujo de datos SCAP, XCCDF y el archivo de diccionario de CPE o el archivo de contenido de OVAL.

     ![Seleccionar el archivo de flujo de datos SCAP](./media/select-datastream-file.png)

4. Si se trata de SCAP 1.2, selecciona el flujo de datos. Después, seleccione la prueba comparativa y el perfil de SCAP 1.x.  Seleccione **Siguiente** para convertir el contenido. Verá una barra de progreso.

      ![Seleccione la prueba comparativa y el perfil de SCAP 1.2.](./media/select-benchmark-and-profile.png)

5. Confirme los datos de configuración que se van a importar.

      ![Captura de pantalla de confirmación de la configuración](./media/confirm-configuration.png)

6. Haga clic en **Siguiente** para importar los datos de configuración.

      ![Completar la importación](./media/complete-import.png)

## <a name="alternate-method-convert-and-import-the-scap-data-stream-files-using-the-cmd-line-tool"></a>(Método alternativo) Convertir e importar archivos de flujo de datos SCAP con la herramienta de línea de comandos

Después de obtener los flujos de datos SCAP, puede usar la herramienta Microsoft.Sces.ScapToDcm.exe para convertir los flujos de datos SCAP en archivos .cab compatibles con Configuración de cumplimiento. Después, importe los archivos .cab en Configuration Manager. La herramienta Microsoft.Sces.ScapToDcm.exe convierte los flujos de datos SCAP en elementos de configuración y líneas base de configuración a las que se pueden acceder mediante la característica Configuración de cumplimiento en Configuration Manager. La herramienta Microsoft.Sces.ScapToDcm.exe convierte los flujos de datos SCAP en manifiestos XML. Después, empaqueta los manifiestos XML en un archivo .cab que se puede importar a Configuration Manager.

Los flujos de datos SCAP publicados por el NIST se organizan en varios paquetes. Siga las instrucciones del NIST para comprobar qué paquetes debe usar en su entorno. Por ejemplo, hay un paquete diferente para cada versión de Windows, otro paquete específico de versión para la configuración del firewall y un paquete para Internet Explorer 8.0. Use los procedimientos siguientes para realizar esta tarea.





## <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>Para importar los flujos de datos SCAP a Configuration Manager

1. Convierta los flujos de datos SCAP en un archivo .cab conforme a Configuración de cumplimiento.
2. Importe el archivo .cab a Configuration Manager.

### <a name="convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files"></a>Convertir flujos de datos SCAP en archivos .cab compatibles con Configuración de cumplimiento

Para poder analizar y evaluar el cumplimiento de sus sistemas, debe convertir los flujos de datos SCAP en formato XML en manifiestos XML conforme a los elementos y líneas base de configuración de Configuración de cumplimiento . La herramienta Microsoft.Sces.ScapToDcm.exe convierte los flujos de datos SCAP en manifiestos XML. Después, empaqueta los manifiestos XML en un archivo .cab que se puede importar posteriormente en Configuration Manager.

#### <a name="to-convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files-using-the-microsoftscesscaptodcmexe-tool"></a>**Para convertir los flujos de datos SCAP en archivos .cab compatibles con Configuración de cumplimiento mediante la herramienta Microsoft.Sces.ScapToDcm.exe**

En el símbolo del sistema, vaya a la carpeta AdminConsole\Bin, ejecute Microsoft.Sces.ScapToDcm.exe para generar un archivo cab compatible con Configuración de cumplimiento e impórtelo en el sitio de Configuration Manager.

   >[!NOTE] 
   > La cuenta debe tener permisos de lectura/escritura para la carpeta de salida.

**Para el contenido de SCAP 1.0/1.1 (archivo XML de XCCDF, como el contenido de USGCB y DISA):**

 Microsoft.Sces.ScapToDcm.exe –xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt; -out &lt;carpetaDeSalida&gt; [-select benchmark/profile] [-log LogFileName]

   >[!NOTE] 
   >Si no especifica la prueba comparativa/perfil mediante el parámetro -select, la herramienta generará un archivo cab de DCM para cada prueba comparativa en el archivo de contenido.

**Para contenido de SCAP 1.2 (archivo XML de DataStream, como el contenido más reciente USGCB):**

Microsoft.Sces.ScapToDcm.exe –scap &lt;scapdatastreamfile.xml&gt; -out &lt;carpetaDeSalida&gt; [-select datastream/benchmark/profile] [-log LogFileName]

   >[!NOTE] 
   > Si no especifica el flujo de datos/prueba comparativa/perfil mediante el parámetro –select, la herramienta generará un archivo cab de DCM para cada prueba comparativa en el archivo de contenido.

**Para un archivo OVAL único con variables externas:**

Microsoft.Sces.ScapToDcm.exe –oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;] -out &lt;carpetaDeSalida&gt; [-log LogFileName]

   >[!NOTE] 
   > Si hay varios valores para una variable en el archivo de variables externas, la herramienta Microsoft.Sces.ScapToDcm.exe tratará los valores como una matriz de esta variable.



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Microsoft.Sces.ScapToDcm.exe. Parámetros de la línea de comandos

| **Parámetro** | **Uso** | **Requerido** |
| --- | --- | --- |
| -scap [archivo de flujo de datos scap] | Especificar el archivo de flujo de datos SCAP. | Sí (para el flujo de datos de SCAP 1.2, es mutuamente excluyente con -xccdf y -oval/-variable) |
| -xccdf [archivo xccdf] | Especificar el archivo XCCDF. | Sí (para XCCDF de SCAP 1.0/1.1, es mutuamente excluyente con -scap y -oval/-variable) |
| -cpe [archivo cpe] | Especificar el archivo CPE. | Sí (para XCCDF de SCAP 1.0/1.1, es mutuamente excluyente con -scap y -oval/-variable) |
| oval [archivo oval] | Especificar el archivo OVAL. | Sí (para archivos OVAL independientes, es mutuamente excluyente con –xccdf y -scap) |
| -variable [archivo de variables externas oval] | Especificar el archivo de variables externas OVAL. | No (opcional para archivos OVAL independientes cuando hay un archivo de variables externas OVAL, es mutuamente excluyente con -xccdf y -scap) |
| -select [prueba comparativa/perfil de xccdf] | Seleccionar la prueba comparativa o el perfil de XCCDF desde el flujo de datos SCAP o el archivo XCCDF. | No (se recomienda especificar este modificador. Si no se especifica, la herramienta generará un archivo cab para todos los perfiles en todos los DataStream o pruebas de rendimiento incrustados) |
| -out [directorio de salida] | Especificar dónde se debe generar el archivo cab de DCM. | No (si no se especifica, la herramienta solo mostrará el contenido sin conversión) |
| -log [archivo de registro] | Especificar el archivo de registro. | No (si no se especifica, el registro se escribe en el archivo Microsoft.Sces.ScapToDcm.log) |
| -help / -? | Mostrar el uso de la herramienta. | No |





#### <a name="the-following-command-lines-are-samples-for-the-microsoftscesscaptodcmexe-tool"></a>Las líneas de comandos de abajo son ejemplos de la herramienta Microsoft.Sces.ScapToDcm.exe:

**SCAP1.2 Content:**

  Microsoft.Sces.ScapToDcm.exe –scap scap\_gov.nist\_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID

**SCAP1.0/1.1 Content:**

   Microsoft.Sces.ScapToDcm.exe–xccdf scap\_gov.nist\_Test-WinXP\_xccdf.xml –cpe scap\_gov.nist\_Test-WinXP\_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID

**SCAP OVAL Content:**

  Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder

**Aquí se muestra un ejemplo de los resultados obtenidos con la herramienta Microsoft.Sces.ScapToDcm.exe:**

  Compliance Settings compliant cab file created:

  Validate the schema of SCAP data stream file C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Successfully validate the schema of SCAP data stream file C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Process XCCDF Benchmark xccdf\_tst.bvt\_benchmark\_Windows-F

  Process XCCDF Profile: xccdf\_tst.bvt\_profile\_version\_1.0.0.0-BVT Profile #1

  Process OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Successfully finished process OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Process OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml

  Successfully finished process OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml Process SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip SCAP Data Stream: [scap\_tst.bvt\_datastream\_Windows-F.zip]

  Version:        [1.2]

  Timestamp:      [2/24/2012]

  Use-case:       [CONFIGURATION]

  CPE Dictionary:  [scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml] Product name:    [National Institute of Standards and Technology]

  Product version: []

  Schema version:  [5.3]

  Timestamp:       [2/24/2012]

  XCCDF Benchmark: [xccdf\_tst.bvt\_benchmark\_Windows-F]

  Version:       [v1.0.0.0] Update:        [http://usgcb.nist.gov]

  Timestamp:     [2/24/2012]

  Status:        [accepted]

  Status date:   [2/24/2012]

  Title:         [Ohh New BVT for SCAP 1.2]

 Description:   [My description]

  XCCDF Profile: [xccdf\_tst.bvt\_profile\_version\_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Product name:    [scaptool]

   Product version: []

   Schema version:  [5.4]

   Timestamp:       [2/24/2012]

  Start SCAP to DCM conversion...

  Processing SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip

  Processing CPE dictionary: scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml

  …

  Generating CI baseline cab file: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Successfully generated CI baseline cab file: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Successfully converted XCCDF profile: xccdf\_tst.bvt\_profile\_version\_1.0.0.0 into DCM baseline xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

## <a name="next-step"></a>Paso siguiente
> [!div class="nextstepaction"]
> [Importar la configuración de cumplimiento de SCAP y exportar los resultados de cumplimiento](/sccm/compliance/plan-design/scap/import-scap-compliance-settings)
