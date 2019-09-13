---
title: Instalación y configuración de extensiones SCAP
titleSuffix: Configuration Manager
description: Instale y configure las extensiones de Security Content Automation Protocol (SCAP) para Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c36f2380a93d6da27651f1aa3a4894e25b3bce39
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70890709"
---
# <a name="install-and-configure-the-scap-extensions-for-configuration-manager"></a>Instalar y configurar extensiones SCAP para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Después de [preparar la infraestructura](/sccm/compliance/plan-design/scap/about-scap#bkmk_prepare), ya tiene todo listo para instalar y configurar las extensiones SCAP para Configuration Manager en el equipo en el que quiera ejecutar este proceso.



## <a name="bkmk_install"></a> Instalar las extensiones de SCAP

El archivo de instalación se encuentra en la siguiente ruta de acceso en el directorio de instalación en el servidor de sitio de Configuration Manager:  
`cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi`

1. Copie **ConfigMgrExtensionsforSCAP.msi** en el equipo con la consola de Configuration Manager en la que quiera ejecutar este proceso.  

2. En el Explorador de Windows, vaya a la carpeta donde copió **ConfigMgrExtensionsforSCAP.msi**. Haga doble clic en el archivo para abrirlo e iniciar las extensiones SCAP para el Asistente para instalación de Configuration Manager.  

3. Revise el contrato de licencia. Haga clic en **Acepto los términos del Contrato de licencia** y después en **Instalar**.  

4. Una vez completada la instalación, haga clic en **Finalizar** para cerrar el Asistente para instalación.  

El Asistente para instalación instala las extensiones SCAP en la carpeta de instalación de la consola de Configuration Manager. De forma predeterminada la carpeta de instalación de la consola es `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole`.  



## <a name="bkmk_scap-data-stream-files"></a> Descargar e instalar los archivos de flujo de datos SCAP

Antes de poder ejecutar extensiones SCAP, debe descargar los archivos de flujo de datos SCAP desde la [página de descarga](https://csrc.nist.gov/Projects/United-States-Government-Configuration-Baseline) de la Base de datos nacional de vulnerabilidad (NVD). Después, cópielos en la carpeta donde instaló las extensiones SCAP.

Dependiendo de su entorno, es posible que no necesite todos los archivos de flujo de datos SCAP que se muestran en la página de descarga.

### <a name="install-the-scap-data-streams"></a>Instalar los flujos de datos SCAP

1. Visite el [sitio web de NVD](https://nvd.nist.gov/) para identificar los flujos de datos SCAP que requiere su organización.
Los flujos de datos SCAP publicados por el NIST se organizan en varios paquetes, que también se denominan _listas de comprobación_.  

2. Descargue los flujos de datos SCAP desde el [sitio web de NVD](https://nvd.nist.gov/home.cfm). Están almacenados en archivos comprimidos con una extensión de nombre de archivo .zip o marcados como archivos XML DataStream.  

    > [!IMPORTANT]  
    > Hay muchos archivos de flujo de datos SCAP con la extensión .xml que puede descargar desde el NVD. En cambio, solo los archivos .xml que incluyen contenido XCCDF (SCAP 1.0 y 1.1)/DataStream (SCAP 1.2) son adecuados para usarlos con las extensiones SCAP.  

3. Extraiga los archivos .zip de flujo de datos SCAP/archivo DataStream XML que descargó en la misma carpeta donde instaló SCAP Extensions.  



## <a name="bkmk_convert-and-import"></a> Convertir e importar manualmente los archivos de flujo de datos SCAP 

Después de obtener los flujos de datos SCAP, ya puede importar y convertir los flujos de datos en líneas base de configuración. Los flujos de datos SCAP publicados por el NIST se organizan en varios paquetes. Siga las instrucciones del NIST para comprobar qué paquetes debe usar en su entorno. Por ejemplo, hay un paquete diferente para cada versión de Windows, otro paquete específico de versión para la configuración del firewall y un paquete para Internet Explorer. Use los procedimientos siguientes para realizar esta tarea.  

> [!Note]  
> Esta sección describe el proceso manual para convertir e importar los archivos de flujo de datos con la consola de Configuration Manager. Para automatizar este proceso, consulte la siguiente sección para [Convertir e importar automáticamente los archivos de flujo de datos SCAP](#bkmk_auto-convert-and-import).  

1. Haga clic en el asistente **Importar contenido de SCAP**desde la cinta de la línea base de configuración.

     ![Botón Importar contenido SCAP en la cinta de opciones de consola](./media/import-scap-content.png)

2. Seleccione la opción de contenido de SCAP.

      ![Seleccionar la página de opciones de contenido SCAP del asistente para importar](./media/import-new-scap-content.png)

3. Seleccione el archivo de flujo de datos SCAP, XCCDF y el archivo de diccionario de CPE o el archivo de contenido de OVAL.

     ![Seleccionar el archivo de flujo de datos SCAP](./media/select-datastream-file.png)

4. Si se trata de SCAP 1.2 seleccione el flujo de datos. Después, seleccione la prueba comparativa y el perfil de SCAP 1.x. Haga clic en **Siguiente** para convertir el contenido. 

      ![Seleccione la prueba comparativa y el perfil de SCAP 1.2.](./media/select-benchmark-and-profile.png)

      > [!Tip]  
      > Esta página del asistente muestra la línea de comandos que puede utilizar con la herramienta **ScapToDcm.exe** para automatizar el proceso mismo.  

5. Confirme los datos de configuración que se van a importar.

      ![Captura de pantalla de confirmación de la configuración](./media/confirm-configuration.png)

6. Haga clic en **Siguiente** para importar los datos de configuración.

      ![Completar la importación](./media/complete-import.png)



## <a name="bkmk_auto-convert-and-import"></a> Convertir e importar automáticamente los archivos de flujo de datos SCAP 

### <a name="import-with-the-command-line-tool"></a>Importar con la herramienta de línea de comandos

Después de obtener los flujos de datos SCAP, puede usar la herramienta **Microsoft.Sces.ScapToDcm.exe** para convertir los flujos de datos SCAP en archivos .cab compatibles con Configuración de cumplimiento. Después, importe los archivos .cab en Configuration Manager. La herramienta Microsoft.Sces.ScapToDcm.exe convierte los flujos de datos SCAP en elementos de configuración y líneas base de configuración que puede usar en Configuration Manager. La herramienta Microsoft.Sces.ScapToDcm.exe convierte los flujos de datos SCAP en manifiestos XML. Después, empaqueta los manifiestos XML en un archivo .cab que se puede importar a Configuration Manager.

> [!Tip]  
> El paso 4 del proceso manual en la sección anterior muestra la página del asistente que muestra la línea de comandos que puede utilizar con la herramienta **ScapToDcm.exe** para automatizar el proceso mismo.  


#### <a name="use-microsoftscesscaptodcmexe-to-convert-scap-data-streams-into-cab-files"></a>Usar Microsoft.Sces.ScapToDcm.exe para convertir los flujos de datos SCAP en archivos .cab

En el símbolo del sistema, vaya a la carpeta **AdminConsole\Bin** y ejecute el archivo **Microsoft.Sces.ScapToDcm.exe**. Esta herramienta genera un archivo .cab conforme a la configuración de cumplimiento y lo importa en el sitio de Configuration Manager.

   > [!NOTE]  
   > La cuenta debe tener permisos de lectura o escritura para la carpeta de salida.

**Uso para el contenido de SCAP 1.0/1.1 (archivo XML de XCCDF, como el contenido de USGCB y DISA):**  

`Microsoft.Sces.ScapToDcm.exe –xccdf <xccdf.xml> -cpe <cpe.xml> -out <outputFolder> [-select benchmark/profile] [-log LogFileName]`  

   > [!NOTE]  
   > Si no especifica la prueba comparativa o el perfil mediante el parámetro `–select`, la herramienta genera un archivo .cab de DCM para cada prueba comparativa en el archivo de contenido.  

**Uso para contenido de SCAP 1.2 (archivo XML de DataStream, como el contenido más reciente USGCB):**  

`Microsoft.Sces.ScapToDcm.exe –scap <scapdatastreamfile.xml> -out <outputFolder> [-select datastream/benchmark/profile] [-log LogFileName]`  

   > [!NOTE]  
   > Si no especifica el flujo de datos, la prueba comparativa o el perfil mediante el parámetro `–select`, la herramienta genera un archivo .cab de DCM para cada prueba comparativa en el archivo de contenido.

**Usar para un archivo OVAL único con variables externas:**  

`Microsoft.Sces.ScapToDcm.exe –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputFolder> [-log LogFileName]`  

   > [!NOTE]  
   > Si hay varios valores para una variable en el archivo de variables externas, la herramienta Microsoft.Sces.ScapToDcm.exe tratará los valores como una matriz de esta variable.  



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Parámetros de la línea de comandos de Microsoft.Sces.ScapToDcm.exe

| Parámetro | Uso | Requerido |
| --- | --- | --- |
| `-scap [scap data stream file]` | Especificar el archivo de flujo de datos SCAP. | Sí (para el flujo de datos de SCAP 1.2, es mutuamente excluyente con -xccdf y -oval/-variable) |
| `-xccdf [xccdf file]` | Especificar el archivo XCCDF. | Sí (para XCCDF de SCAP 1.0/1.1, es mutuamente excluyente con -scap y -oval/-variable) |
| `-cpe [cpe file]` | Especificar el archivo CPE. | Sí (para XCCDF de SCAP 1.0/1.1, es mutuamente excluyente con -scap y -oval/-variable) |
| `-oval [oval file]` | Especificar el archivo OVAL. | Sí (para archivos OVAL independientes, es mutuamente excluyente con –xccdf y -scap) |
| `-variable [oval external variable file]` | Especificar el archivo de variables externas OVAL. | No (opcional para archivos OVAL independientes cuando hay un archivo de variable de OVAL externo, es mutuamente excluyente con -xccdf y -scap) |
| `-select [xccdf benchmark/profile]` | Seleccionar la prueba comparativa o el perfil de XCCDF desde el flujo de datos SCAP o el archivo XCCDF. | No (Este parámetro no es necesario pero se recomienda. Si no se especifica, la herramienta generará un archivo .cab para todos los perfiles en todos los DataStream o pruebas de rendimiento incrustados) |
| `-out [output directory]` | Especificar dónde se debe generar el archivo cab de DCM. | No (Si no se especifica, la herramienta solo mostrará el contenido sin conversión) |
| `-log [log file]` | Especificar el archivo de registro. | No (Si no se especifica, el registro se escribe en el archivo Microsoft.Sces.ScapToDcm.log) |
| `-help` o `-?` | Mostrar el uso de la herramienta. | No |


#### <a name="microsoftscesscaptodcmexe-examples"></a>Ejemplos de Microsoft.Sces.ScapToDcm.exe

**Contenido de SCAP 1.2:**  

`Microsoft.Sces.ScapToDcm.exe –scap scap_gov.nist_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID`  

**Contenido de SCAP 1.0/1.1:**  

`Microsoft.Sces.ScapToDcm.exe–xccdf scap_gov.nist_Test-WinXP_xccdf.xml –cpe scap_gov.nist_Test-WinXP_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID`  

**Contenido de SCAP OVAL:**  

`Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder`  


#### <a name="sample-output-from-microsoftscesscaptodcmexe"></a>Ejemplo de salida de Microsoft.Sces.ScapToDcm.exe

``` Output
  Compliance Settings compliant cab file created:

  Validate the schema of SCAP data stream file C:\24SCAP\BVT_Test_Data_Stream.xml

  Successfully validate the schema of SCAP data stream file C:\24SCAP\BVT_Test_Data_Stream.xml

  Process XCCDF Benchmark xccdf_tst.bvt_benchmark_Windows-F

  Process XCCDF Profile: xccdf_tst.bvt_profile_version_1.0.0.0-BVT Profile #1

  Process OVAL: scap_tst.bvt_comp_Windows-F-oval.xml

  Successfully finished process OVAL: scap_tst.bvt_comp_Windows-F-oval.xml

  Process OVAL: scap_tst.bvt_comp_Windows-F-cpe-oval.xml

  Successfully finished process OVAL: scap_tst.bvt_comp_Windows-F-cpe-oval.xml
   Process SCAP data stream: scap_tst.bvt_datastream_Windows-F.zip
    SCAP Data Stream: [scap_tst.bvt_datastream_Windows-F.zip]

  Version:        [1.2]

  Timestamp:      [2/24/2012]

  Use-case:       [CONFIGURATION]

  CPE Dictionary:  [scap_tst.bvt_comp_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml]
  Product name:    [National Institute of Standards and Technology]

  Product version: []

  Schema version:  [5.3]

  Timestamp:       [2/24/2012]

  XCCDF Benchmark: [xccdf_tst.bvt_benchmark_Windows-F]

  Version:       [v1.0.0.0]
   Update:        [http://usgcb.nist.gov]

  Timestamp:     [2/24/2012]

  Status:        [accepted]

  Status date:   [2/24/2012]

  Title:         [Ohh New BVT for SCAP 1.2]

 Description:   [My description]

  XCCDF Profile: [xccdf_tst.bvt_profile_version_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Product name:    [scaptool]

   Product version: []

   Schema version:  [5.4]

   Timestamp:       [2/24/2012]

  Start SCAP to DCM conversion...

  Processing SCAP data stream: scap_tst.bvt_datastream_Windows-F.zip

  Processing CPE dictionary: scap_tst.bvt_comp_Windows-F-cpe-dictionary.xml

  …

  Generating CI baseline cab file: C:\28\bbt\xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab

  Successfully generated CI baseline cab file: C:\28\bbt\xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab

  Successfully converted XCCDF profile: xccdf_tst.bvt_profile_version_1.0.0.0 into DCM baseline xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab
```


### <a name="import-the-cab-file"></a>Importar el archivo .cab

El siguiente paso del proceso es usar la consola de Configuration Manager para importar los archivos .cab conformes a Configuración de cumplimiento a Configuration Manager. Al importar los archivos .cab que creó anteriormente en este proceso, se crean uno o más elementos de configuración y líneas base de configuración en la base de datos de Configuration Manager. Más adelante en el proceso puede implementar líneas de base de configuración en recopilaciones de dispositivos. Para obtener más información, vea [Import configuration data (Importar datos de configuración)](/sccm/compliance/deploy-use/import-configuration-data).

La ubicación del archivo .cab que creó anteriormente es la carpeta especificada por el parámetro `–output` de la herramienta Microsoft.Sces.ScapToDcm.exe.

> [!IMPORTANT]  
> Repita este proceso para cada archivo .cab que crease anteriormente en el proceso. Hay un archivo .cab para cada perfil seleccionado en el archivo XCCDF/DataStreamXML que descargó desde el sitio web NVD. Puede procesar estos archivos ejecutando la herramienta Microsoft.Sces.ScapToDcm.exe.  

La línea base de configuración es de solo lectura, su estado es *Habilitado* y su estado implementado *No*. La propiedad **Fecha de modificación** muestra la fecha y hora en que se importó la línea base. El nombre de la línea base de configuración procede de la sección de nombre para mostrar del XML de XCCDF/DataStream. El nombre se construye usando la convención `ABC[XYZ]`, donde **ABC** es el identificador de la prueba comparativa de XCCDF y **XYZ** es el identificador de perfil de XCCDF (si se ha seleccionado un perfil).



## <a name="next-step"></a>Paso siguiente
> [!div class="nextstepaction"]
> [Implementar y supervisar el cumplimiento de SCAP y exportar los resultados de cumplimiento](/sccm/compliance/plan-design/scap/deploy-monitor-export)
