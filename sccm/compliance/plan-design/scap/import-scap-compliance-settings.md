---
title: Importar la configuración de cumplimiento de SCAP
titleSuffix: Configuraton Manager
description: Importar la configuración de cumplimiento de SCAP como líneas base de configuración y exportar los resultados
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 1f6b1fa0dd0775083eff9925a65509083b3f47d3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336619"
---
# <a name="import-the-compliance-settings-compliant-cab-files-into-system-center-configuration-manager"></a>Importar los archivos .cab compatibles con Configuración de cumplimiento en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

> [!Tip]  
> Esta característica se introdujo por primera vez en la versión preliminar técnica 1803 como una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). Esta versión preliminar de las extensiones SCAP puede instalarse en cualquier versión admitida de Rama actual de Configuration Manager y LTSB 1606. El archivo de instalación se encuentra en cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi a partir de 1803 Technical Preview. 

El siguiente paso del proceso es usar la consola de Configuration Manager para importar los archivos .cab conformes a Configuración de cumplimiento a Configuration Manager. Al importar los archivos .cab que creó anteriormente en este proceso, se crean uno o más elementos de configuración y líneas base de configuración en la base de datos de Configuration Manager. Más adelante en el proceso puede asignar cada una de las líneas base de configuración a una recopilación de equipos en Configuration Manager.

## <a name="to-import-the-compliance-settings-compliant-cab-files-into-configuration-manager"></a>Para importar archivos .cab conformes a Configuración de cumplimiento a Configuration Manager

1. Abra la **consola de Configuration Manager**.
2. En la  **consola de Configuration Manager, en el panel de navegación, vaya a \*\* Activos y compatibilidad**> **Configuración de cumplimiento** > **Líneas base de configuración**.

3. En el panel Acciones, haga clic en **Importar datos de configuración** para iniciar el Asistente para importar datos de configuración.

1. Siga los pasos del **Asistente para importar datos de configuración** usando la información de la tabla de abajo y acepte los valores predeterminados a menos que se especifique lo contrario.



Proceso del Asistente para importar datos de configuración

| Nombre de página del Asistente | Acción del usuario |
| --- | --- |
| **Elegir archivo** |1. Haga clic en **Agregar**. </br>Aparece el cuadro de diálogo Abrir.|
||2. En el cuadro de diálogo **Abrir**, vaya a la carpeta **&lt;salida del archivo cab de cumplimiento\_ &gt;**. Haga clic en el archivo **&lt;cumplimiento\_cab&gt;**.cab, donde la **carpeta\_salida** de _cumplimiento cab es la carpeta que se especifica después del modificador -output cuando se ejecuta la herramienta Sces.ScapToDcm.exe. **archivo\_cumplimiento** es el nombre de un archivo .cab que creó en un paso anterior de este proceso. Después, haga clic en **Abrir**. </br> Aparece el cuadro de diálogo Consola de Configuration Manager: advertencia de seguridad.|
||3. En el cuadro de diálogo **Consola de Configuration Manager: advertencia de seguridad**, haga clic en **Ejecutar**. En la página Elegir archivos, se muestran los datos de configuración en la lista de líneas base para importar.|
||3. Haga clic en **Siguiente**.|
| **Resumen** |5. Haga clic en **Siguiente**. |
| **Finalizando el Asistente para importar datos de configuración** |6. Haga clic en **Cerrar**. |

La nueva línea base de configuración se muestra en el panel de información de la consola de Configuration Manager.

>[!IMPORTANT]
> Deberá repetir este proceso para cada archivo .cab que crease anteriormente en el proceso. Hay un archivo .cab para cada perfil seleccionado en el archivo XML de XCCDF/DataStream que descargó del sitio web de NVD, que puede procesar si ejecuta la herramienta Microsoft.Sces.ScapToDcm.exe.

La línea base de configuración importada es de solo lectura, tiene el estado &#39;Habilitado&#39; y el estado implementado inicial en &#39;No&#39;.  La propiedad &#39;fecha de modificación&#39; indica el momento en que se importó la línea de base.  El nombre de la línea base de configuración procede de la sección de nombre para mostrar del XML de XCCDF/DataStream. El nombre se construye usando esta convención:

ABC[XYZ], donde ABC es el identificador de la prueba comparativa de XCCDF y XYZ es el identificador de perfil de XCCDF (si se ha seleccionado un perfil).



## <a name="assign-configuration-baselines-to-the-computer-collections"></a>Asignar líneas base de configuración para colecciones de equipos

Después de crear las colecciones de equipos adecuadas para los equipos donde quiere evaluar el cumplimiento de SCAP, ya puede asignar las líneas base de configuración que importó para asociarlas con las colecciones de equipos. Esta sección proporciona información para asignar una línea base de configuración a una recopilación de equipos mediante la consola de Configuration Manager.

Para asignar una línea base de configuración a una colección de equipos:

1. Abra la **consola de** **Configuration Manager**.

2. En la **consola de Configuration Manager, en el panel de navegación, vaya a **Activos y compatibilidad** > **Configuración de cumplimiento** >** Líneas de base de configuración**.
3. En el panel de navegación, haga clic en &lt;**Línea de base de\_configuración>, donde &lt;_línea de base de\_configuración&gt;_ es el nombre de la línea base de configuración que quiere asignar a una colección de equipos.

    La lista de elementos de configuración de la línea base de configuración se muestra en el panel de información de Configuration Manager.

4. En el panel Acciones, haga clic en **Implementar**.

5. Siga los pasos del cuadro de diálogo **Implementar** **línea de base de** **configuración** usando la información de la tabla de abajo y aceptando los valores predeterminados a menos que se especifique lo contrario.

### <a name="deploy-configuration-baseline-dialog-process"></a>Proceso del cuadro de diálogo Implementar línea base de configuración

| Nombre de página del Asistente | Acción del usuario |
| --- | --- |
| **Elegir recopilación** | 1. Haga clic en **Examinar**.|
||2. En el cuadro de diálogo **Elegir recopilación**, seleccione **Recopilaciones de dispositivos**. Después, haga clic en **&lt;colección\_equipos&gt;**, donde &lt;_colección\_equipos&gt;_ es el nombre de la colección de equipos que creó en un paso anterior de este proceso. Haga clic en **Aceptar**.|
| **Establecer programación** |3. Seleccione la programación adecuada para su organización.|
 
>[!IMPORTANT]
> Repita este proceso para cada recopilación de equipos que desee asignar a cada línea base de configuración. Asigne cada línea base de configuración a una recopilación de equipos como mínimo.

## <a name="verify-that-the-compliance-data-has-been-collected"></a>Comprobar que se han recopilado los datos de cumplimiento

Antes de exportar los datos de cumplimiento nuevamente al formato SCAP, deberá verificar que se han recopilado los datos. Después de asignar una línea base de configuración a una recopilación de equipos, el cliente de Configuration Manager en cada equipo de la recopilación recoge automáticamente la información de cumplimiento. La información de cumplimiento se almacena en la base de datos de Configuration Manager.

Puede ver el estado de la implementación de la línea base de configuración en Configuration Manager para verificar la recopilación de los datos por parte de los clientes de Configuration Manager. Es importante comprobar que se han recopilado los datos de cumplimiento adecuados en Configuration Manager porque puede ayudarle a validar los archivos de resultados de XCCDF/DataStream que creará posteriormente en este proceso.



### <a name="verify-that-the-compliance-data-has-been-collected"></a>Comprobación de la recopilación de los datos de cumplimiento

1. Abra la consola de Configuration Manager.
2. En la consola de Configuration Manager, en el panel de navegación, vaya a **Supervisión** > **Implementaciones**.
3. Haga clic en **Tipo de característica** para ordenar el tipo de implementación y buscar elementos que sean **Línea de base** en la lista.
4. Haga clic con el botón derecho en &lt;línea de base de\_configuración&gt; en la lista que acaba de implementar en la colección y haga clic en **Ver estado**.
5. Vaya al nodo &lt;línea de base de\_configuración&gt; para ver el estado de cumplimiento. Si hay una máquina con el estado desconocido, significa que la recopilación de datos de cumplimiento aún no se ha completado para esa máquina.

### <a name="validate-the-xccdfdatastream-results"></a>Validar los resultados de XCCDF/DataStream

1. Abra la consola de Configuration Manager.
2. En la consola de Configuration Manager, en el panel de navegación, vaya al panel **Configuración de cumplimiento** > **SCAP**.
3. Seleccione la línea base de configuración, la asignación, el archivo SCAP, el flujo de datos, la prueba comparativa y el perfil (si corresponde).
4. Haga clic en **Mostrar informe**
 ![SCAP report](./media/scap-report.png) (Informe de SCAP).



## <a name="export-compliance-results-to-scap-format"></a>Exportar resultados de cumplimiento al formato de SCAP

La siguiente tarea del proceso consiste en exportar los datos de cumplimiento de Configuración de cumplimiento al formato de SCAP, que es un archivo de ARFreport en formato XML/lenguaje natural. SCAP Extensions Export Wizard (Asistente para exportar extensiones SCAP) y la herramienta Microsoft.Sces.DcmToScap.exe exportan un archivo de resultados de XCCDF/DataStreamARF independiente para cada línea base de configuración de Configuración de cumplimiento. Estos archivos corresponden a cada archivo de entrada XCCDF/DataStream que la herramienta Microsoft.Sces.ScapToDcm.exe usa para crear cada línea base de configuración de Configuración de cumplimiento.

### <a name="export-the-compliance-settings-compliance-data-using-the-export-scap-report-wizard"></a>Exportar los datos de cumplimiento de Configuración de cumplimiento mediante Export SCAP Report Wizard (Asistente para exportar informes de SCAP)

1. Inicie Export SCAP Report Wizard (Asistente para exportar informes de SCAP) desde el menú contextual del panel de SCAP.
![Importar desde el panel de SCAP](./media/import-from-scap-dashboard.png)

2. Seleccionar la línea base de configuración y la asignación en ![Seleccionar línea de base](./media/select-ci-baseline.png)

3. Elija la ubicación del archivo de flujo de datos de SCAP, el archivo XCCDF/CPE o los archivos de contenido y variables de OVAL.
![Choose datastream](./media/export-scap-report-datastream.png) (Elegir flujo de datos)

4. Especifique el nombre de la organización y elija la ubicación de la carpeta para exportar el informe SCAP.
 ![Choose datastream](./media/specify-org-export.png) (Elegir flujo de datos)

5. Confirme la configuración.
 ![Choose datastream](./media/confirm-export.png) (Elegir flujo de datos)

6. Elija **Siguiente para exportar el informe.  Verá una barra de progreso y luego una página de finalización.
 ![Complete the export](./media/complete-report-export.png) (Completar la exportación)



### <a name="alternate-method-export-the-compliance-settings-compliance-data-using-the-microsoftscesdcmtoscapexe-tool"></a>(Método alternativo) Exportar los datos de cumplimiento de Configuración de cumplimiento mediante la herramienta Microsoft.Sces.DcmToScap.exe

1. En el símbolo del sistema, vaya al tipo de carpeta AdminConsole\Bin, escriba los parámetros de línea de comandos que se muestran en la tabla de abajo y presione **ENTRAR:

    >[!NOTE] 
    >Su cuenta debe tener permisos de lectura para el proveedor de Configuration Manager y también permisos de escritura para la carpeta de salida especificada en el parámetro -out de la línea de comandos.

**Para contenido de SCAP 1.0/1.1 (como contenido de USGCB y DISA):**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt;  -select &lt;prueba comparativa o perfil de  xccdf&gt; -out &lt;carpeta de resultados de salida&gt;  [-log logFileName]

  >[!NOTE] 
    >Debe usar el parámetro -select para especificar la prueba comparativa o el perfil que se ha evaluado en los clientes si hay varias pruebas comparativas o perfiles en el contenido.

**Para contenido de SCAP 1.2 (como el contenido de USGCB más reciente):**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID  -select &lt;flujo de datos/prueba comparativa de xccdf/perfil&gt; -out &lt;carpeta de resultados de salida&gt;  [-log logFileName]

   >[!NOTE] 
   >Debe usar el parámetro -select para especificar el flujo de datos/prueba comparativa/perfil que se ha evaluado en los clientes si hay varios flujos de datos/pruebas comparativas/perfiles en el contenido.

**Para un archivo OVAL único con variables externas:**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;]  -out &lt;carpeta de resultados de salida&gt;  [-log logFileName]

   >[!NOTE] 
    >La herramienta Microsoft.Sces.DcmToScap.exe solo generará informes de resultados de definición de OVAL para cada máquina de destino. No generará un informe de ARF.

#### <a name="how-to-get-baseline-ci-id-and-assignment-id"></a>Cómo obtener el identificador de CI de línea de base y el identificador de asignación

En la consola de administración, vaya a **Activos y compatibilidad** > **Configuración de cumplimiento** > **Líneas base de configuración**. El identificador de CI es el identificador de CI de línea base de configuración.

![Obtener el identificador de CI y el identificador de asignación](./media/get-to-baselines.png)

Seleccione la línea base de configuración que quiera, haga clic en la pestaña Implementaciones, si el identificador de asignación no está en pantalla, haga clic con el botón derecho en el encabezado de columna y haga clic en Identificador de asignación para habilitarlo.
![Obtener el identificador de CI y el identificador de asignación](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>Parámetros de la línea de comandos de Microsoft.Sces.DcmToScap.exe

| **Parámetro** | **Uso** | **Requerido** |
| --- | --- | --- |
| -baseline [identificador de CI de línea de base] | Especificar la línea base de configuración | Sí |
| -assignment [identificador de asignación] | Especificar la implementación de la línea base de configuración | Sí |
| -organization [nombre organización] | Especificar el nombre de la organización, el cual aparecerá en el informe. Se puede separar con &#39;;&#39; para especificar un nombre de organización de varias líneas. | No |
| -type [fino/completo/completosincs] | Especifique el tipo de resultado OVAL: resultado fino, resultado completo o resultado completo sin la característica del sistema. | No (si no se especifica, el valor predeterminado es completo) |
| -scap [archivo de flujo de datos scap] | Especificar el archivo de flujo de datos SCAP. | Sí (para el flujo de datos de SCAP 1.2, es mutuamente excluyente con -xccdf y -oval/-variable) |
| -xccdf [archivo xccdf] | Especificar el archivo XCCDF. | Sí (para XCCDF de SCAP 1.0/1.1, es mutuamente excluyente con -scap y -oval/-variable) |
| -cpe [archivo cpe] | Especificar el archivo CPE. | Sí (para XCCDF de SCAP 1.0/1.1, es mutuamente excluyente con -scap y -oval/-variable) |
| oval [archivo oval] | Especificar el archivo OVAL. | Sí (para archivos OVAL independientes, es mutuamente excluyente con -xccdf y -scap) |
| -variable [archivo de variables externas oval] | Especificar el archivo de variables externas OVAL. | No (opcional para archivos OVAL independientes cuando hay un archivo de variable de OVAL externo, es mutuamente excluyente con -xccdf y -scap) |
| -select [prueba comparativa/perfil de xccdf] | Seleccionar la prueba comparativa o el perfil de XCCDF desde el flujo de datos SCAP o el archivo XCCDF. | Sí (se debe realizar una selección para generar un informe para hacer coincidir la línea de base de DCM correspondiente en la base de datos de Configuration Manager. |
| -out [directorio de salida] | Especificar dónde se debe generar el archivo cab de Configuración de cumplimiento. | No (si no se especifica, la herramienta solo mostrará el contenido sin conversión) |
| -log [archivo de registro] | Especificar el archivo de registro. | No (si no se especifica, el registro se escribe en el archivo Microsoft.Sces.DcmToScap.log) |
| -help / -? | Mostrar el uso de la herramienta. | No |



 >[!TIP] 
 >Puede especificar los parámetros -?, El parámetro –h o –help para mostrar la sintaxis de la herramienta Microsoft.Sces.DcmToScap.exe y una lista de los parámetros.

De forma predeterminada, la herramienta Microsoft.Sces.DcmToScap.exe accede a la base de datos de Configuration Manager con sus credenciales. La herramienta Microsoft.Sces.DcmToScap.exe requiere un mínimo de acceso de lectura a la base de datos de Configuration Manager.

Tras comprobar que existen los archivos del informe **ARF** (_ARF\_xxxx.xml_), el informe en **lenguaje natural** (xxx.txt), el informe de **Cyberscope** (LASR\_xxx.xml), el informe **ConsumedOval** (xx-oval-&lt;nombreDeMáquina&gt;.xml), el informe de **resultado de prueba comparativa de XCCDF** (xccdf\_xxx.xml), vaya a la línea de comandos, escriba exit y presione **ENTRAR** para salir del símbolo del sistema.

## <a name="next-step"></a>Paso siguiente
> [!div class="nextstepaction"]
> [Solución de problemas](/sccm/compliance/plan-design/scap/troubleshooting-scap)
