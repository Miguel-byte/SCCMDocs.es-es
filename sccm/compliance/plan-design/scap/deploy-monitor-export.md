---
title: Implementar y supervisar el cumplimiento de SCAP
titleSuffix: Configuration Manager
description: Importe la configuración de cumplimiento de SCAP como líneas base de configuración, supervise el cumplimiento y exporte los resultados.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7b59b7414ad2095d053b1121ba936281559aa5e2
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386006"
---
# <a name="deploy-and-monitor-scap-compliance-in-configuration-manager"></a>Implementar y supervisar el cumplimiento de SCAP en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Cuando haya [convertido e importado](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import) los archivos de flujo de datos SCAP, vea los pasos siguientes:  

- [Implementar](#bkmk_deploy) las líneas base de configuración en recopilaciones para evaluar el cumplimiento de SCAP de los dispositivos  

- [Supervisar](#bkmk_monitor) los datos de cumplimiento devueltos desde los clientes de destino  

- [Exportar](#bkmk_export) los resultados de cumplimiento al formato SCAP  



## <a name="bkmk_deploy"></a> Implementar líneas base de configuración de SCAP

Cree primero las recopilaciones de dispositivos de los equipos cuyo cumplimiento de SCAP quiere evaluar. Para más información, vea [Create collections](/sccm/core/clients/manage/collections/create-collections) (Crear recopilaciones).  

Ahora está listo para implementar las líneas base de configuración que importó a estas recopilaciones de dispositivos. Para más información, vea [Cómo implementar líneas base de configuración](/sccm/compliance/deploy-use/deploy-configuration-baselines).  

> [!Tip]  
> Repita este proceso para cada línea base de configuración que quiera implementar en cada recopilación de dispositivos. Como mínimo, implemente cada línea base de configuración en al menos una recopilación de dispositivos.



## <a name="bkmk_monitor"></a> Supervisar los datos de cumplimiento de SCAP 

Para poder exportar los datos de cumplimiento de nuevo al formato SCAP, tiene que comprobar que se han recopilado los datos en el sitio. Después de asignar una línea base de configuración a una recopilación de dispositivos, el cliente de Configuration Manager de cada equipo de la recopilación reúne automáticamente la información de cumplimiento. La información de cumplimiento se almacena en la base de datos de Configuration Manager.

Vea el estado de la implementación de la línea base de configuración en Configuration Manager para asegurarse de que los clientes de Configuration Manager hayan recopilado los datos adecuados. Es importante comprobar que se han recopilado los datos de cumplimiento adecuados en Configuration Manager porque puede ayudarle a validar los archivos de resultados de XCCDF/DataStream que creará posteriormente en este proceso.

Para más información, vea [Supervisar la configuración de cumplimiento](/sccm/compliance/deploy-use/monitor-compliance-settings).


### <a name="validate-the-xccdfdatastream-results"></a>Validar los resultados de XCCDF/DataStream

1. En la consola de Configuration Manager, vaya el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y seleccione el **panel de SCAP**.  

2. Seleccione la línea base de configuración, la asignación, el archivo SCAP, el flujo de datos, la prueba comparativa y el perfil (si corresponde).  

3. Haga clic en **Mostrar informe**
 ![informe SCAP de ejemplo](./media/scap-report.png)



## <a name="bkmk_export"></a> Exportar resultados de cumplimiento al formato SCAP

El siguiente paso del proceso consiste en exportar los datos de cumplimiento al formato SCAP, que es un archivo de informe ARF en formato XML/lenguaje natural. SCAP Extensions Export Wizard (Asistente para exportar extensiones SCAP) y la herramienta de línea de comandos Microsoft.Sces.DcmToScap.exe exportan un archivo de resultados XCCDF/DataStreamARF independiente para cada línea base de configuración. Estos archivos corresponden a cada archivo de entrada XCCDF/DataStream que la herramienta Microsoft.Sces.ScapToDcm.exe usa para crear cada línea base de configuración.


### <a name="manually-export-with-the-console-wizard"></a>Exportar manualmente con el asistente para la consola

> [!Note]  
> En esta sección se describe el proceso manual para exportar los resultados de cumplimiento con la consola de Configuration Manager. Para automatizar este proceso, vea la sección [Exportar automáticamente con la herramienta de línea de comandos](#bkmk_auto-export) siguiente.  


1. Inicie **Export SCAP Report Wizard** (Asistente para exportar informes de SCAP) haciendo clic con el botón derecho en el nodo del **panel de SCAP**.  
![Iniciar el Asistente para exportar informes de SCAP desde el panel de SCAP](./media/import-from-scap-dashboard.png)

2. Seleccione la línea base de configuración, la asignación y el tipo de contenido de SCAP.  
![Seleccionar línea base](./media/select-ci-baseline.png)

3. Elija la ubicación del archivo de flujo de datos de SCAP, el archivo XCCDF/CPE o los archivos de contenido y variables de OVAL.  
![Elegir flujo de datos](./media/export-scap-report-datastream.png)

4. Especifique el nombre de la organización y elija la ubicación de la carpeta para exportar el informe SCAP.  
 ![Elegir flujo de datos](./media/specify-org-export.png)
   > [!Tip]  
   > Esta página del asistente muestra la línea de comandos que puede utilizar con la herramienta **DcmToScap.exe** para automatizar el mismo proceso.  

5. Confirme la configuración.  
 ![Elegir flujo de datos](./media/confirm-export.png)

6. Elija **Siguiente** para exportar el informe. Complete el asistente.  
 ![Complete the export](./media/complete-report-export.png) (Completar la exportación)


### <a name="bkmk_auto-export"></a> Exportar automáticamente con la herramienta de línea de comandos

Abra el símbolo del sistema y vaya a la carpeta **AdminConsole\Bin** de Configuration Manager. Utilice uno de los ejemplos de línea de comandos siguientes:  

> [!NOTE]  
> La cuenta debe tener permisos de lectura para el proveedor de Configuration Manager. También necesita permisos de escritura en la carpeta especificada en el parámetro `–out` de la línea de comandos.

**Para contenido de SCAP 1.0/1.1 (como contenido de USGCB y DISA):**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –xccdf <xccdf.xml> -cpe <cpe.xml>  -select <xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

  > [!NOTE]  
  > Si hay varias pruebas comparativas o perfiles en el contenido, utilice el parámetro `–select` para especificar la prueba comparativa o el perfil que se ha evaluado en los clientes.  

**Para contenido de SCAP 1.2 (como el contenido de USGCB más reciente):**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID -select <datastream/xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > Si hay varios flujos de datos, pruebas comparativas o perfiles en el contenido, utilice el parámetro `–select` para especificar el flujo de datos, la prueba comparativa o el perfil que se ha evaluado en los clientes.  

**Para un archivo OVAL único con variables externas:**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > La herramienta Microsoft.Sces.DcmToScap.exe solo generará informes de resultados de definición de OVAL para cada máquina de destino. No generará el informe de ARF.  


#### <a name="how-to-get-the-baselineciid-and-assignmentid"></a>Cómo obtener BaselineCIID y AssignmentID

En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y seleccione **Líneas base de configuración**. `BaselineCIID` es el identificador (ID) de la línea base de configuración.  
![Obtener el identificador de CI y el identificador de asignación](./media/get-to-baselines.png)

Seleccione la línea base de configuración que prefiera y haga clic en la pestaña **Implementaciones**. `AssignmentID` es el identificador (ID) de la implementación de línea base de configuración para una recopilación de dispositivos. Si el identificador de asignación no se muestra, haga clic con el botón derecho en el encabezado de columna y seleccione **Id. de asignación**.  
![Obtener el identificador de CI y el identificador de asignación](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>Parámetros de la línea de comandos de Microsoft.Sces.DcmToScap.exe

| Parámetro | Uso | Requerido |
| --- | --- | --- |
| `-baseline [Baseline CI ID]` | Especificar la línea base de configuración | Sí |
| `-assignment [Assignment ID]` | Especificar la implementación de la línea base de configuración | Sí |
| `-organization [organization name]` | Especificar el nombre de la organización, el cual aparecerá en el informe. Para especificar un nombre de organización de varias líneas se puede usar `;` como separador. | No |
| `-type [thin/full/fullnosc]` | Especifique el tipo de resultado OVAL: resultado fino, resultado completo o resultado completo sin la característica del sistema. | No (si no se especifica, el valor predeterminado es completo) |
| `-scap [scap data stream file]` | Especificar el archivo de flujo de datos SCAP. | Sí (para el flujo de datos de SCAP 1.2, es mutuamente excluyente con -xccdf y -oval/-variable) |
| `-xccdf [xccdf file]` | Especificar el archivo XCCDF. | Sí (para XCCDF de SCAP 1.0/1.1, es mutuamente excluyente con -scap y -oval/-variable) |
| `-cpe [cpe file]` | Especificar el archivo CPE. | Sí (para XCCDF de SCAP 1.0/1.1, es mutuamente excluyente con -scap y -oval/-variable) |
| `-oval [oval file]` | Especificar el archivo OVAL. | Sí (para archivos OVAL independientes, es mutuamente excluyente con –xccdf y -scap) |
| `-variable [oval external variable file]` | Especificar el archivo de variables externas OVAL. | No (opcional para archivos OVAL independientes cuando hay un archivo de variable de OVAL externo, es mutuamente excluyente con -xccdf y -scap) |
| `-select [xccdf benchmark/profile]` | Seleccionar la prueba comparativa o el perfil de XCCDF desde el flujo de datos SCAP o el archivo XCCDF. | Sí (se debe realizar una selección para generar un informe que pueda coincidir con la línea base de DCM correspondiente en la base de datos de Configuration Manager |
| `-out [output directory]` | Especificar dónde se debe generar el archivo cab de Configuración de cumplimiento. | No (si no se especifica, la herramienta solo mostrará el contenido sin conversión) |
| `-log [log file]` | Especificar el archivo de registro. | No (si no se especifica, el registro se escribe en el archivo Microsoft.Sces.DcmToScap.log) |
| `-help` o `-?` | Mostrar el uso de la herramienta. | No |

 > [!TIP]  
 > Puede especificar el parámetro `-?`, `–h` o `–help` para mostrar la sintaxis de la herramienta Microsoft.Sces.DcmToScap.exe y una lista de los parámetros.

De forma predeterminada, la herramienta Microsoft.Sces.DcmToScap.exe accede a la base de datos de Configuration Manager con sus credenciales. La herramienta Microsoft.Sces.DcmToScap.exe requiere un mínimo de acceso de lectura a la base de datos de Configuration Manager.

Tras ejecutar la herramienta, compruebe que existen los siguientes archivos: 
- El informe **ARF**: `_ARF_xxxx.xml_` y/o el informe **en lenguaje natural**: `xxx.txt`
- El informe **Cyberscope**: `LASR_xxx.xml`
- El informe **ConsumedOval**: `xx-oval-<machineName>.xml`
- El informe de **resultados de la prueba comparativa XCCDF**: `xccdf_xxx.xml` 



## <a name="next-step"></a>Paso siguiente
> [!div class="nextstepaction"]
> [Solución de problemas](/sccm/compliance/plan-design/scap/troubleshooting-scap)
