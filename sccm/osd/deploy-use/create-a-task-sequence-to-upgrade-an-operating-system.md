---
title: Creación de una secuencia de tareas de actualización de SO
titleSuffix: Configuration Manager
description: Use una secuencia de tareas para actualizar automáticamente de Windows 7 o una versión posterior a Windows 10
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c7932609d9a52968a3c610fd9c5a00326cced8d5
ms.sourcegitcommit: 9c02c00c4061ab17beb3bc1cc895b533f3b55bc4
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2019
ms.locfileid: "66501719"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>Crear una secuencia de tareas para actualizar un SO en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use secuencias de tareas en Configuration Manager para actualizar automáticamente un SO en un equipo de destino. Esta actualización puede ser desde Windows 7 o una versión posterior a Windows 10, o desde Windows Server 2012 o posterior a Windows Server 2016. Cree una secuencia de tareas que haga referencia al paquete de actualización de sistema operativo y cualquier otro contenido para instalar, como aplicaciones o actualizaciones de software. La secuencia de tareas para actualizar un SO es parte del escenario de [Actualizar Windows a la versión más reciente](upgrade-windows-to-the-latest-version.md).  



## <a name="prerequisites"></a>Requisitos previos

Antes de crear la secuencia de tareas, se deben aplicar los requisitos siguientes:    

#### <a name="required"></a>Requerido  

- El [paquete de actualización del SO](/sccm/osd/get-started/manage-operating-system-upgrade-packages) debe estar disponible en la consola de Configuration Manager.  

- Al actualizar a Windows Server 2016, seleccione la opción **Omitir cualquier mensaje de compatibilidad descartable** en el paso de secuencia de tareas Actualizar sistema operativo. En caso contrario, se produce un error en la actualización.  

#### <a name="required-if-used"></a>Necesario (si se usa)  

-   Las [actualizaciones de software](/sccm/sum/get-started/synchronize-software-updates) deben estar sincronizadas en la consola de Configuration Manager.  

-   Las [aplicaciones](/sccm/apps/deploy-use/create-applications) deben agregarse a la consola de Configuration Manager.  



##  <a name="BKMK_UpgradeOS"></a> Crear una secuencia de tareas para actualizar un sistema operativo  

Para actualizar el sistema operativo en los clientes, puede crear una secuencia de tareas y seleccionar **Actualizar un sistema operativo desde el paquete de actualización** en el Asistente para crear secuencia de tareas. El asistente agrega los pasos de secuencia de tareas para actualizar el sistema operativo, aplica actualizaciones de software e instala aplicaciones. 

#### <a name="to-create-a-task-sequence-that-upgrades-an-os"></a>Crear una secuencia de tareas que actualice un sistema operativo  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y después haga clic en **Secuencias de tareas**.  

2.  En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Crear secuencia de tareas**.  

3.  En la página **Crear nueva secuencia de tareas** del Asistente para creación de secuencia de tareas, seleccione **Actualizar un sistema operativo desde un paquete de actualización** y luego haga clic en **Siguiente**.  

4.  En la página **Información de secuencia de tareas**, especifique la siguiente configuración y después haga clic en **Siguiente**:  

    -   **Nombre de secuencia de tareas**: especifique un nombre que identifique la secuencia de tareas.  

    -   **Descripción**: si quiere, especifique una descripción.  

5.  En la página **Actualizar el sistema operativo de Windows**, especifique la siguiente configuración y luego haga clic en **Siguiente**:  

    -   **Paquete de actualización**: especifique el paquete de actualización que contiene los archivos de origen de actualización del sistema operativo. Compruebe que ha seleccionado el paquete de actualización correcto examinando la información del panel **Propiedades**. Para más información, vea [Administrar paquetes de actualización de sistema operativo](/sccm/osd/get-started/manage-operating-system-upgrade-packages).  

    -   **Índice de edición**: si hay varios índices de edición del sistema operativo disponibles en el paquete, seleccione el índice de la edición deseada. De forma predeterminada, el asistente selecciona el primer índice.  

    -   **Clave de producto**: especifique la clave de producto para el sistema operativo que quiere instalar. Puede especificar claves de licencia por volumen codificadas o claves de producto estándar. Si usa una clave de producto estándar, separe cada grupo de cinco caracteres por un guion (-). Por ejemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Si se trata de una actualización de una edición de licencia por volumen, la clave de producto puede no ser necesaria.  

        > [!Note]  
        > Esta clave de producto puede ser una clave de activación múltiple (CAM) o una clave de licencias por volumen genérica (CLVG). Las CLVG también se conocen como claves de configuración de cliente del servicio de administración de claves (SAC). Para obtener más información, consulte [Plan para la activación por volumen](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Para obtener una lista de claves de configuración de cliente KMS, consulte el [Apéndice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) de la Guía de activación de Windows Server. 

    -   **Omitir cualquier mensaje de compatibilidad descartable**: seleccione esta configuración si actualiza a Windows Server 2016. Si no selecciona esta configuración, la secuencia de tareas no se completará, ya que el programa de instalación de Windows espera a que el usuario haga clic en **Confirmar** en un cuadro de diálogo de compatibilidad de aplicaciones de Windows.   

7.  En la página **Incluir actualizaciones**, especifique si se van a instalar las actualizaciones de software necesarias, todas o ninguna. A continuación, haga clic en **Siguiente**. Si especifica que se instalen las actualizaciones, Configuration Manager instala solo las destinadas a las colecciones a las que pertenece el equipo de destino.  

8.  En la página **Instalar aplicaciones** , especifique las aplicaciones que desee instalar en el equipo de destino y, a continuación, haga clic en **Siguiente**. Si selecciona más de una aplicación, especifique también si la secuencia de tareas debe continuar si se produce un error en la instalación de una aplicación específica.  

9. Complete el asistente.  


> [!Important]  
> Cuando se ejecuta la secuencia de tareas en un dispositivo, el cliente de Configuration Manager crea varios scripts para controlar el comportamiento de la secuencia de tareas en distintos escenarios. Cuando se completa la secuencia de tareas, el cliente no quita estos scripts hasta que se reinicia el equipo. Estos archivos de script no contienen información confidencial.  


A partir de la versión 1802, la plantilla de secuencia de tareas predeterminada para la actualización en contexto de Windows 10 incluye grupos adicionales con las acciones recomendadas que se van a agregar antes y después del proceso de actualización. Estas acciones son comunes entre muchos clientes que están actualizando correctamente los dispositivos a Windows 10. Para obtener más información, vea los pasos de secuencia de tareas recomendados [para preparar la actualización](#recommended-task-sequence-steps-to-prepare-for-upgrade) y [para el procesamiento posterior](#recommended-task-sequence-steps-for-post-processing).

A partir de la versión 1806, esta plantilla de secuencia de tareas también incluye un grupo con las acciones recomendadas que se deben agregar en caso de error del proceso de actualización. Estas acciones facilitan la solución de problemas. Para obtener más información, consulte [Pasos de la secuencia de tareas recomendados para errores](#recommended-task-sequence-steps-on-failure).<!--1358500-->  



## <a name="configure-pre-cache-content"></a>Configuración del contenido de la caché previa
<!--1021244-->
La característica de caché previa para las implementaciones disponibles de secuencias de tareas permite que los clientes descarguen el contenido del paquete de actualización del sistema operativo relevante antes de que un usuario instale la secuencia de tareas.  

> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Por ejemplo, solo quiere una secuencia de tareas de actualización en contexto para todos los usuarios y tiene muchas arquitecturas y lenguajes. En versiones anteriores, el contenido se comienza a descargar cuando el usuario instala una implementación de secuencia de tareas disponible desde el Centro de software. Este retraso agrega tiempo adicional antes de que la instalación esté lista para iniciarse. Se descarga todo el contenido al que se hace referencia en la secuencia de tareas. Este contenido incluye el paquete de actualización de sistema operativo para todos los lenguajes y arquitecturas. Si cada paquete de actualización tiene aproximadamente 3 GB de tamaño, el contenido total es muy grande.

El contenido de caché previa proporciona la opción al cliente de descargar solo el paquete de actualización del sistema operativo aplicable y otro contenido al que se haga referencia, tan pronto como reciba la implementación. Cuando el usuario hace clic en **Instalar** en el Centro de software, el contenido está listo. La instalación se inicia rápidamente porque el contenido está en el disco duro local.

> [!NOTE]  
> Actualmente este comportamiento solo se aplica al paquete de actualización del sistema operativo. Ese paquete es el único contenido en el que se especifica la arquitectura o el idioma correspondiente. Por ejemplo, si la secuencia de tareas también hace referencia a varios paquetes de controladores, el cliente actualmente los descarga todos. El motor de secuencia de tareas evalúa las condiciones en los pasos cuando se ejecuta la secuencia de tareas, no con antelación. El cliente usa las etiquetas de las propiedades del paquete para determinar qué contenido se almacena en la caché previa.


### <a name="to-configure-the-pre-cache-feature"></a>Para configurar la característica de caché previa

1. Cree paquetes de actualización del sistema operativo para idiomas y arquitecturas específicas. Especifique la arquitectura y el idioma en la pestaña **Origen de datos** del paquete. Para el idioma, use la conversión decimal. Por ejemplo, **1033** es el valor decimal para inglés y **0x0409** es el hexadecimal equivalente.  

    El cliente evalúa los valores de idioma y arquitectura para determinar qué paquete de actualización del sistema operativo se descarga durante el almacenamiento en la caché previa.  

2. Cree una secuencia de tareas con pasos condicionales para los diferentes idiomas y arquitecturas. Por ejemplo, en el siguiente paso se usa la versión en inglés:  

    ![Editor de secuencia de tareas en el que se muestran varios pasos de actualización del sistema operativo para ENU, DEU y JPN](../media/precacheproperties2.png)

    ![Pestaña Opciones del editor de secuencia de tareas, en la que se muestra la consulta WQL de WMI para la Configuración regional y OSArchitecture](../media/precacheoptions2.png)  

3. Implemente la secuencia de tareas. Para la característica de caché previa, configure las opciones siguientes:  

    - En la pestaña **General**, seleccione **Descargar contenido previamente para esta secuencia de tareas**.  

    - En la pestaña **Configuración de implementación**, configure la secuencia de tareas como **Disponible**.  

    - En la pestaña **Programación**, elija la hora seleccionada actualmente para la opción **Programar cuándo estará disponible esta implementación**. El cliente inicia el almacenamiento del contenido en la caché previa a la hora de disponibilidad de la implementación. Cuando un cliente de destino recibe esta directiva, la hora disponible se encuentra en el pasado, por lo que la descarga en la caché previa se inicia inmediatamente. Si el cliente recibe esta directiva pero la hora disponible está en el futuro, el cliente no inicia el almacenamiento del contenido en la caché previa hasta la hora disponible.  

    - En la pestaña **Puntos de distribución**, configure los valores **Opciones de implementación**. Si el contenido no se ha almacenado previamente en la caché antes de que un usuario inicie la instalación, el cliente usa esta configuración.  
  

### <a name="user-experience"></a>Experiencia del usuario

- Cuando el cliente recibe la directiva de implementación, inicia el almacenamiento del contenido en la caché previa después de la hora disponible de la implementación. Este contenido incluye todos los paquetes a los que se hace referencia, pero solo el paquete de actualización del sistema operativo que coincide con los atributos de idioma y arquitectura del paquete.  

- Cuando el cliente pone la implementación a disposición de los usuarios, se muestra una notificación para informarles sobre la nueva implementación. Ahora la secuencia de tareas es visible en el Centro de software. El usuario puede ir al Centro de software y hacer clic en **Instalar** para iniciar la instalación.  

- Si el cliente no ha almacenado previamente en la caché el contenido cuando el usuario instala la secuencia de tareas, el cliente usa la configuración que se especifique en la pestaña **Opción de implementación** de la implementación.  



## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Pasos de secuencia de tareas recomendados para preparación para actualización

A partir de la versión 1802, la plantilla de secuencia de tareas predeterminada para la actualización en contexto de Windows 10 incluye grupos adicionales con las acciones recomendadas que se van a agregar antes del proceso de actualización. Estas acciones del grupo **Preparación para actualización** son comunes entre muchos clientes que están actualizando correctamente los dispositivos a Windows 10. Para los sitios en versiones anteriores a la 1802, agregue manualmente estas acciones a la secuencia de tareas en el grupo **Preparación para actualización**.  

- **Comprobaciones de batería**: agregue pasos a este grupo para comprobar si el equipo está usando la batería o un cable de alimentación. Esta acción requiere un script o utilidad personalizado a fin de realizar la comprobación. Por ejemplo: mediante WbemTest, conéctese al espacio de nombres `root\cimv2`. Después, ejecute la siguiente consulta: `Select Batterystatus From Win32_Battery where batterystatus != 2`. Si devuelve algún resultado, el dispositivo se está ejecutando con batería. En caso contrario, el dispositivo está conectado a la red por cable.  

- **Comprobaciones de conexión por cable o red**: agregue pasos a este grupo para comprobar si el equipo está conectado a una red y no está usando una conexión inalámbrica. Esta acción requiere un script o utilidad personalizado a fin de realizar la comprobación.  Por ejemplo: mediante WbemTest, conéctese al espacio de nombres `root\cimv2`. Después, ejecute la siguiente consulta: `Select * From Win32_NetworkAdapter Where NetConnectionStatus = 2 and PhysicalAdapter = 'True' and NetConnectionID = 'Wi-Fi'`. Si se devuelve algún resultado, el dispositivo esta funcionando con una conexión Wi-Fi. En caso contrario, el dispositivo está conectado a la red por cable.

- **Quitar aplicaciones no compatibles**: agregue pasos a este grupo para quitar todas las aplicaciones que no sean compatibles con esta versión de Windows 10. El método para desinstalar una aplicación es diferente en cada situación.  

    - Si la aplicación usa Windows Installer, copie la línea de comandos de **Desinstalar programa** desde la pestaña **Programas** en las propiedades del tipo de implementación de Windows Installer de la aplicación. Luego, agregue un paso para **Ejecutar línea de comandos** a este grupo con la línea de comandos de desinstalar programa. Por ejemplo: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br>  

- **Quitar controladores no compatibles**: agregue pasos a este grupo para quitar todos los controladores que no sean compatibles con esta versión de Windows 10.  

- **Quitar/suspender seguridad de terceros**: agregue pasos a este grupo para quitar o suspender programas de seguridad de terceros, como antivirus.  

   - Si utiliza un programa de cifrado de disco de otro fabricante, indique su controlador de cifrado al programa de instalación de Windows con la [opción de línea de comandos](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#23) `/ReflectDrivers`. Agregue un paso para [establecer la variable de secuencia de tareas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) a la secuencia de tareas en este grupo. Establezca la variable de secuencia de tareas en **OSDSetupAdditionalUpgradeOptions**. Establezca el valor en `/ReflectDrivers` con la ruta de acceso al controlador. Esta [variable de secuencia de tareas](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions) anexa la línea de comandos del programa de instalación de Windows utilizada por la secuencia de tareas. Para obtener las instrucciones adicionales sobre este proceso, póngase en contacto con su proveedor de software.  


### <a name="download-package-content-task-sequence-step"></a>Paso de la secuencia de tareas Descargar contenido de paquete  

Use el paso [Descargar contenido de paquete](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent) antes del paso **Actualizar sistema operativo** en los siguientes escenarios:  

-   Use una única secuencia de tareas de actualización para las plataformas x86 y x64. Incluya dos pasos **Descargar contenido de paquete** en el grupo **Preparación para actualización**. Establezca condiciones en cada paso para detectar la arquitectura del cliente. Esta condición hace que el paso solo descargue el paquete de actualización de sistema operativo adecuado. Configure todos los pasos **Descargar contenido de paquete** para que usen la misma variable, y use la variable para la ruta de los medios en el paso **Actualizar sistema operativo** .  

-   Para descargar dinámicamente un paquete de controladores aplicables, use dos pasos **Descargar contenido de paquete** con condiciones para detectar el tipo de hardware adecuado para cada paquete de controlador. Configure los pasos **Descargar contenido de paquete** para que usen la misma variable. Después, use esa variable para el valor **Contenido preconfigurado** de la sección de controladores del paso **Actualizar sistema operativo**.  

    > [!NOTE]  
    > Configuration Manager agrega un sufijo numérico al nombre de variable. Por ejemplo, si especifica `%mycontent%` como variable personalizada, el cliente almacena todo el contenido al que se hace referencia en esta ubicación. Cuando se hace referencia a la variable en un paso posterior, como **Actualizar sistema operativo**, se usa con un sufijo numérico. En este ejemplo, `%mycontent01%` o `%mycontent02%`, donde el número se corresponde al orden en el que el paso **Descargar contenido de paquete** muestra este contenido específico.  



## <a name="recommended-task-sequence-steps-for-post-processing"></a>Pasos de la secuencia de tareas recomendados para posprocesamiento   

Después de crear la secuencia de tareas, agregue pasos adicionales al grupo **Posprocesamiento** de la secuencia de tareas.  

> [!NOTE]  
>  Esta secuencia de tareas no es lineal. Hay condiciones en los pasos que pueden afectar a los resultados de la secuencia de tareas. Este comportamiento depende de si actualiza correctamente el equipo cliente, o bien de si tiene que revertir el equipo cliente al sistema operativo original.  

A partir de la versión 1802, la plantilla de secuencia de tareas predeterminada para la actualización en contexto de Windows 10 incluye grupos adicionales con las acciones recomendadas que se van a agregar después del proceso de actualización. Estas acciones del grupo **Posprocesamiento** son comunes entre muchos clientes que están actualizando correctamente los dispositivos a Windows 10. Para los sitios en versiones anteriores a la 1802, agregue manualmente estas acciones a la secuencia de tareas en el grupo **Posprocesamiento**.  

- **Aplicar controladores basados en el programa de instalación**: agregue pasos a este grupo para instalar controladores basados en el programa de instalación (.exe) a partir de paquetes.  

- **Instalar/habilitar seguridad de terceros**: agregue pasos a este grupo para instalar o habilitar programas de seguridad de terceros, como antivirus.  

- **Establecer aplicaciones y asociaciones de Windows predeterminadas**: agregue pasos a este grupo para establecer las asociaciones de aplicaciones y archivos predeterminadas de Windows. En primer lugar, prepare un equipo de referencia con las asociaciones de aplicaciones deseadas. A continuación, ejecute la siguiente línea de comandos para exportar: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Agregue el archivo XML a un paquete. Luego, ejecute el paso [Ejecutar línea de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) en este grupo. Especifique el paquete que contiene el archivo XML y, a continuación, especifique la siguiente línea de comandos: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Para obtener más información, consulte [Export or import default application associations](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations) (Exportación o importación de asociaciones de aplicaciones predeterminadas).  

- **Aplicar valores personalizados**: agregue pasos a este grupo para aplicar las personalizaciones del menú Inicio, como la organización de los grupos de programas. Para obtener más información, consulte [Customize the Start screen](/windows-hardware/manufacture/desktop/customize-the-start-screen) (Personalización de la pantalla Inicio).  



## <a name="optional-task-sequence-steps-for-rollback"></a>Pasos de secuencia de tareas opcionales para la reversión  

Cuando se produce algún problema con el proceso de actualización después de reiniciar el equipo, el programa de instalación de Windows revierte el sistema al SO anterior. La secuencia de tareas continúa después con cualquier paso en el grupo **Reversión**. Después de crear la secuencia de tareas, agregue pasos opcionales en este grupo según sea necesario. Por ejemplo, revierta los cambios realizados en el sistema en el grupo Preparación para actualización, como desinstalar el software incompatible.



## <a name="recommended-task-sequence-steps-on-failure"></a>Pasos de la secuencia de tareas recomendados para errores
<!--1358500-->

A partir de la versión 1806, la plantilla de secuencia de tareas predeterminada para la actualización en contexto de Windows 10 incluye un grupo para **Ejecutar acciones en caso de error**. Este grupo incluye las acciones recomendadas para agregar en caso de que se produzca un error en el proceso de actualización. Estas acciones facilitan la solución de problemas.

- **Recopilar registros**: para recopilar registros del cliente, agregue pasos en este grupo.  

    - Una práctica común consiste en copiar los archivos de registro en un recurso compartido de red. Para establecer esta conexión, use el paso [Conectar a carpeta de red](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder).  

    - Para llevar a cabo la operación de copia, utilice una utilidad o script personalizado con el paso [Ejecutar línea de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) o [Ejecutar script de PowerShell Script](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript).  

    - Los archivos para recopilar podrían incluir los siguientes registros:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

    - Para más información sobre setupact.log y otros registros de instalación de Windows, vea [Windows Setup Log files](https://docs.microsoft.com/windows/deployment/upgrade/log-files) (Archivos de registro de instalación de Windows).  

    - Para obtener más información sobre registros de cliente de Configuration Manager, vea [Registros de cliente de Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs).  

    - Para obtener más información sobre **_SMSTSLogPath** y otras variables útiles, vea [Task sequence variables](/sccm/osd/understand/task-sequence-variables) (Variables de secuencia de tareas).  

- **Ejecutar herramientas de diagnóstico**: para ejecutar herramientas de diagnóstico adicionales, agregue pasos en este grupo. Automatice estas herramientas para recopilar información adicional del sistema justo después del error.  

    - Una de estas herramientas es Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). Es una herramienta de diagnóstico independiente para obtener detalles sobre el motivo de que una actualización de Windows 10 se haya realizado incorrectamente.  

        - En Configuration Manager, [cree un paquete](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program) para la herramienta.  

        - Agregue un paso [Ejecutar línea de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) a este grupo de la secuencia de tareas. Use la opción **Paquete** para hacer referencia a la herramienta. La siguiente cadena es una **línea de comandos** de ejemplo:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`  



## <a name="additional-recommendations"></a>Otras recomendaciones

- Consulte la documentación de Windows para [solucionar los errores de actualización de Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). En este artículo también se incluye información detallada sobre el proceso de actualización.  

- En el paso predeterminado **Comprobar preparación**, habilite **Garantizar espacio libre mínimo en disco (MB)** . Establezca el valor en al menos **16384** (16 GB) para un paquete de actualización de sistema operativo de 32 bits, o **20480** (20 GB) para 64 bits.  

- Use la [variable de secuencia de tareas](/sccm/osd/understand/task-sequence-variables#SMSTSDownloadRetryCount) **SMSTSDownloadRetryCount** para intentar descargar de nuevo la directiva. En este momento, el cliente lo reintenta de manera predeterminada dos veces; esta variable está configurada en dos (2). Si los clientes no utilizan una conexión de red intranet por cable, una mayor cantidad de reintentos ayudará al cliente a obtener la directiva. El uso de esta variable no tiene ningún efecto secundario, además del retraso que implica la imposibilidad de descargar la directiva.<!--501016--> Aumente también la variable **SMSTSDownloadRetryDelay** desde el valor predeterminado de 15 segundos.  

- Realice una evaluación de compatibilidad en línea:  

   - Agregue un segundo paso para **actualizar el sistema operativo** al principio del grupo **Preparar para la actualización**. Póngale el nombre *Evaluación de actualización*. Especifique el mismo paquete de actualización y, a continuación, habilite la opción **Realizar examen de compatibilidad del programa de instalación de Windows sin iniciar la actualización**. Habilite **Continuar después de un error** en la pestaña Opciones.  

   - Inmediatamente después de este paso de *Evaluación de actualización*, agregue otro paso **Ejecutar línea de comandos**. Especifique la siguiente línea de comandos:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>En la pestaña **Opciones** , agregue la siguiente condición: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Este código de retorno es el equivalente decimal de MOSETUP_E_COMPAT_SCANONLY (0xC1900210), que es un examen de compatibilidad en el que no se detecta ningún problema. Si el paso *Evaluación de actualización* se realiza correctamente y devuelve este código, la secuencia de tareas omite este paso. En caso contrario, si el paso de la evaluación devuelve cualquier otro código de retorno, este paso produce un error en la secuencia de tareas con el código de retorno del examen de compatibilidad del programa de instalación de Windows. Para obtener más información sobre **_SMSTSOSUpgradeActionReturnCode**, vea [Task sequence variables](/sccm/osd/understand/task-sequence-variables#SMSTSOSUpgradeActionReturnCode) (Variables de secuencia de tareas).  

   - Para obtener más información, consulte [Actualizar el sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).  

- Si desea cambiar el dispositivo de BIOS a UEFI durante esta secuencia de tareas, consulte [Conversión de BIOS a UEFI durante una actualización local](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).  

- Si usa el cifrado de disco BitLocker, en ese caso, de forma predeterminada el programa de instalación de Windows la suspende automáticamente durante la actualización. A partir de Windows 10, versión 1803, el programa de instalación de Windows incluye el parámetro de línea de comandos `/BitLocker` para controlar este comportamiento. Si los requisitos de seguridad exigen mantener el cifrado de disco activo en todo momento, utilice la [variable de secuencia de tareas](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions) **OSDSetupAdditionalUpgradeOptions** en el grupo **Preparar para actualización** para incluir `/BitLocker TryKeepActive`. Para más información, consulte [Opciones de la línea de comandos del programa de instalación de Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#33).<!--SCCMDocs issue #494-->  

- Algunos clientes quitan las aplicaciones predeterminadas aprovisionadas en Windows 10. Por ejemplo, la aplicación Bing El Tiempo o la Microsoft Solitaire Collection. En algunas situaciones, estas aplicaciones vuelven después de actualizar Windows 10. Para obtener más información, vea [How to keep apps removed from Windows 10 (Cómo mantener las aplicaciones eliminadas en Windows 10)](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update). Agregue un paso **Ejecutar línea de comandos** a la secuencia de tareas en el grupo **Preparar para actualización**. Especifique una línea de comandos similar al ejemplo siguiente:</br> `cmd /c reg delete "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f` <!--SCCMDocs issue #526-->  
