---
title: Crear medios independientes
titleSuffix: Configuration Manager
description: "Use medios independientes para implementar el sistema operativo en un equipo sin necesidad de una conexión a un sitio de Configuration Manager o a la red."
ms.custom: na
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
caps.latest.revision: "21"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: ef9ee10c94cea3e9d8437a8d8b3df8427d0cc524
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/12/2017
---
# <a name="create-stand-alone-media-with-system-center-configuration-manager"></a>Crear medios independientes con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los medios independientes de Configuration Manager contienen toda la información necesaria para implementar el sistema operativo en un equipo sin necesidad de una conexión a un sitio de Configuration Manager o a la red. Use medios independientes con los siguientes escenarios de implementación de sistema operativo:  

-   [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Actualizar Windows a la versión más reciente](upgrade-windows-to-the-latest-version.md)  

Los medios independientes incluyen la secuencia de tareas que automatiza los pasos de instalación del sistema operativo y todo otro contenido requerido, incluida la imagen de arranque, la imagen de sistema operativo y los controladores de dispositivos. Dado que todos lo necesario para implementar el sistema operativo se guarda en los medios independiente, el espacio en disco que estos necesitan es significativamente mayor que el espacio en disco necesario para otros tipos de medios. Cuando cree un medio independiente en un sitio de administración central, el cliente recuperará su código de sitio asignado de Active Directory. Los medios independientes que creó en los sitios secundarios asignarán automáticamente al cliente el código de sitio para dicho sitio.  

##  <a name="BKMK_CreateStandAloneMedia"></a> Crear medios independientes  
Antes de crear medios independientes con el Asistente para crear medio de secuencia de tareas, asegúrese de que se cumplen las condiciones siguientes:  

### <a name="create-a-task-sequence-to-deploy-an-operating-system"></a>Crear una secuencia de tareas para implementar un sistema operativo
Como parte de los medios independientes, debe especificar la secuencia de tareas para implementar un sistema operativo. Para obtener los pasos para crear una nueva secuencia de tareas, consulte [Create a task sequence to install an operating system in System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md) (Crear una secuencia de tareas para instalar un sistema operativo en System Center Configuration Manager).

No se admiten las siguientes acciones para medios independientes:
- El paso Aplicar controladores automáticamente en la secuencia de tareas. No se admite la aplicación automática de controladores de dispositivos desde el catálogo de controladores, pero puede elegir el paso Aplicar paquete de controladores para que haya un conjunto especificado de controladores disponible para el Programa de instalación de Windows.
- Paso de la secuencia de tareas Descargar contenido de paquete. La información del punto de administración no está disponible en medios independientes, por lo tanto, se producirá un error en el paso al intentar enumerar las ubicaciones de contenido.
- Instalación de actualizaciones de software.
- Instalación de software antes de implementar un sistema operativo.
- Secuencias de tareas para implementaciones que no son de sistema operativo.
- Asociación de usuarios con el equipo de destino para admitir la afinidad de dispositivo de usuario.
- El paquete dinámico se instala a través de la tarea Instalar paquete.
- La aplicación dinámica se instala a través de la tarea Instalar aplicación.

> [!NOTE]    
> Si la secuencia de tareas para implementar un sistema operativo incluye el paso [Instalar paquete](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) y usted crea los medios independientes en un sitio de administración central, podría producirse un error. El sitio de administración central no tiene las directivas de configuración de cliente necesarias para habilitar el agente de distribución de software durante la ejecución de la secuencia de tareas. Es probable que aparezca el siguiente error en el archivo CreateTsMedia.log:    
>     
> "WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)" (Error en el método WMI SMS_TaskSequencePackage.GetClientConfigPolicies (0x80041001))    
> 
> En medios independientes que incluyen un paso **Instalar paquete**, debe crear el medio independiente en un sitio primario que tenga el agente de distribución de software habilitado o agregar un paso [Ejecutar línea de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine) después del paso [Instalar Windows y Configuration Manager](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) y antes del primer paso **Instalar paquete** de la secuencia de tareas. El paso **Ejecutar línea de comandos** ejecuta un comando de WMIC para habilitar el agente de distribución de software antes de que se ejecuta el primer paso Instalar paquete. Puede utilizar lo siguiente en su paso de secuencia de tareas **Ejecutar línea de comandos** :    
>    
> *WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE*


> [!IMPORTANT]    
> Cuando se usa el paso **Instalar Windows y Configuration Manager** en la secuencia de tareas del sistema operativo, no seleccione la opción **Usar paquete de cliente de preproducción cuando esté disponible** para medios independientes. Si se selecciona esta opción y el paquete de cliente de preproducción está disponible, se utilizará en los medios independientes. Y esto no se admite. Para obtener más información sobre esta configuración, consulte [Instalar Windows y Configuration Manager](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).


### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo el contenido asociado con la secuencia de tareas
Debe distribuir todo el contenido requerido por la secuencia de tareas a un punto de distribución como mínimo. Esto incluye la imagen de arranque, la imagen de sistema operativo y otros archivos asociados. El asistente recopila la información desde el punto de distribución al crear los medios independientes. Debe tener derechos de acceso de **lectura** para la biblioteca de contenido de dicho punto de distribución.  Para obtener más información, consulte [Distribute content referenced by a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) (Distribuir contenido al que hace referencia una secuencia de tareas).

### <a name="prepare-the-removable-usb-drive"></a>Preparar la unidad USB extraíble
*Para una unidad USB extraíble:*

Si va a usar una unidad USB extraíble, dicha unidad debe estar conectada al equipo donde se ejecuta el asistente y debe ser detectada por Windows como un dispositivo de eliminación. El asistente escribe directamente en la unidad extraíble cuando crea los medios. Los medios independientes utilizan un sistema de archivos FAT32. No se pueden crear medios independientes en una unidad flash USB cuyo contenido incluye un archivo de más de 4 GB de tamaño.

### <a name="create-an-output-folder"></a>Crear una carpeta de salida
*Para un conjunto de CD o DVD:*

Antes de ejecutar el Asistente para crear medio de secuencia de tareas para crear medios para un conjunto de CD o DVD, debe crear una carpeta para los archivos de salida creados por el asistente. El medio creado para un conjunto de CD o DVD se escribe como archivo .iso directamente en esa carpeta.


 Use el procedimiento siguiente para crear medios independientes para una unidad USB extraíble o un conjunto de CD o DVD.  

## <a name="to-create-stand-alone-media"></a>Para crear medios independientes  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear medio de secuencia de tareas** para iniciar el Asistente para crear medio de secuencia de tareas.  

4.  En la página **Seleccionar tipo de medio** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    -   Seleccione **Medio independiente**.  

    -   Opcionalmente, si desea permitir que el sistema operativo se implemente sin intervención del usuario, seleccione **Permitir la implementación desatendida de sistema operativo**. Cuando se selecciona esta opción, no se pide al usuario información de configuración de red ni secuencias de tareas opcionales. No obstante, se seguirá solicitando una contraseña al usuario si el medio está configurado para la protección con contraseña.  

5.  En la página **Tipo de medios** , especifique si se trata de una unidad flash o un conjunto de CD o DVD y luego haga clic para configurar los siguientes elementos:  

    > [!IMPORTANT]  
    >  Los medios independientes utilizan un sistema de archivos FAT32. No se pueden crear medios independientes en una unidad flash USB cuyo contenido incluye un archivo de más de 4 GB de tamaño.  

    -   Si selecciona **Unidad flash USB**, especifique la unidad en la que quiere almacenar el contenido.  

    -   Si selecciona **Conjunto de CD/DVD**, especifique la capacidad del medio y el nombre y la ruta de acceso de los archivos de salida. El asistente escribe los archivos de salida en esta ubicación. Por ejemplo: **\\\nombre de servidor\carpeta\archivo de salida.iso**  

         Si la capacidad de los medios es demasiado pequeña para almacenar todo el contenido, se crean varios archivos y debe almacenar el contenido en varios CD o DVD. Si se requieren varios medios, Configuration Manager agrega un número de secuencia al nombre de cada archivo de salida que crea. Además, si implementa una aplicación junto con el sistema operativo y la aplicación no cabe en un solo medio, Configuration Manager almacena la aplicación en varios medios. Cuando se ejecuta el medio independiente, Configuration Manager pide al usuario el siguiente medio en el que se almacena la aplicación.   

         > [!IMPORTANT]  
         >  Si selecciona una imagen .iso existente, el Asistente para crear medio de secuencia de tareas elimina la imagen de la unidad o el recurso compartido cuando pasa a la siguiente página del asistente. Se elimina la imagen existente incluso si, a continuación, se cancela al asistente.  

     Haga clic en **Siguiente**.  

6.  En la página **Seguridad**, elija una de las siguientes opciones de configuración y después haga clic en **Siguiente**:
    - **Proteger medio con contraseña**: escriba una contraseña segura para ayudar a proteger el medio. Si se especifica una contraseña, será necesaria para utilizar el medio.  

        > [!IMPORTANT]  
        >  En un medio independiente, se cifran únicamente los pasos de la secuencia de tareas y sus variables. El contenido restante del medio no se cifra: no incluya información confidencial en los scripts de secuencia de tareas. Almacene e implemente la información confidencial mediante el uso de variables de secuencia de tareas.  

    - **Seleccionar el intervalo de tiempo de validez de este medio independiente** (a partir de la versión 1702): establezca las fechas de inicio y expiración opcionales en el medio. Estas opciones están deshabilitadas de forma predeterminada. Las fechas se comparan con la hora del sistema del equipo antes de que se ejecuten los medios independientes. Cuando la hora del sistema es anterior a la hora de inicio o posterior a la hora de expiración, los medios independientes no se inician. Estas opciones también están disponibles mediante el cmdlet de PowerShell New-CMStandaloneMedia.
7.  En la página **CD/DVD independiente** , especifique la secuencia de tareas que implementa el sistema operativo y, a continuación, haga clic en **Siguiente**. Elija **Detectar dependencias de aplicación asociadas y agregarlas a este medio** para agregar contenido a los medios independientes para las dependencias de la aplicación.
    > [!TIP]
    > Si no ve las dependencias de aplicación esperadas, anule la selección y luego vuelva a seleccionar la configuración **Detectar dependencias de aplicación asociadas y agregarlas a este medio** para actualizar la lista.

    El asistente le permite seleccionar las secuencias de tareas asociadas con una imagen de arranque.  

8. En la página **Seleccionar aplicación** (disponible a partir de la versión 1702), especifique el contenido de la aplicación que desea incluir como parte del archivo multimedia y después haga clic en **Siguiente**.
9. En la página **Seleccionar paquete** (disponible a partir de la versión 1702), especifique el contenido del paquete que desea incluir como parte del archivo multimedia y después haga clic en **Siguiente**.
10. En la página **Seleccionar el paquete de controladores** (disponible a partir de la versión 1702), especifique el contenido del paquete de controladores que desea incluir como parte del archivo multimedia y después haga clic en **Siguiente**.
11.  En la página **Puntos de distribución** , especifique uno o varios puntos de distribución que tengan el contenido que la secuencia de tareas necesita y luego haga clic en **Siguiente**.  

     Configuration Manager solo muestra los puntos de distribución que tienen el contenido. Debe distribuir todo el contenido asociado con la secuencia de tareas (imagen de arranque, imagen de sistema operativo, etc.) al menos a un punto de distribución para poder continuar. Después de distribuir el contenido, puede reiniciar el asistente o quitar los puntos de distribución ya seleccionados en esta página. Además, vaya a la página anterior y después regrese a la página **Puntos de distribución** para actualizar la lista de puntos de distribución. Para obtener más información sobre la distribución de contenido, consulte [Distribute content referenced by a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) (Distribuir contenido al que hace referencia una secuencia de tareas). Para obtener más información sobre los puntos de distribución y la administración de contenido, consulte [Manage content and content infrastructure for System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager).  

    > [!NOTE]  
    >  Debe tener derechos de acceso de **lectura** para la biblioteca de contenido en los puntos de distribución.  

12. En la página **Personalización** , especifique la siguiente información y, a continuación, haga clic en **Siguiente**.  

    -   Especifique las variables que la secuencia de tareas utiliza para implementar el sistema operativo.  

    -   Especifique los comandos de preinicio que desea ejecutar antes de la secuencia de tareas. Los comandos de preinicio son un script o un ejecutable que puede interactuar con el usuario en Windows PE antes de que se ejecute la secuencia de tareas para instalar el sistema operativo. Para obtener más información sobre los comandos de preinicio para los medios, consulte [Prestart commands for task sequence media in System Center Configuration Manager](../understand/prestart-commands-for-task-sequence-media.md) (Comandos de preinicio para medios de secuencia de tareas en System Center Configuration Manager).  

         Si lo desea, active la casilla **Incluir archivos para el comando de preinicio** para incluir los archivos que el comando de preinicio necesita.  

        > [!TIP]  
        >  Durante la creación de medios de secuencia de tareas, la secuencia de tareas escribe el identificador de paquete y el comando de preinicio, incluidos los valores de las variables de secuencia de tareas, en el archivo de registro CreateTSMedia.log en el equipo que ejecuta la consola de Configuration Manager. Puede revisar este archivo de registro para comprobar el valor de las variables de secuencia de tareas.  

13. Complete el asistente.  

 Los archivos de medios independientes (.iso) se crean en la carpeta de destino. Si seleccionó **CD/DVD independiente**, ahora puede copiar los archivos de salida a un conjunto de CD o DVD.  

##  <a name="BKMK_StandAloneMediaTSExample"></a> Ejemplo de secuencia de tareas de medios independientes  
 Utilice la tabla siguiente como guía al crear una secuencia de tareas para implementar un sistema operativo mediante medios independientes. La tabla le ayudará a decidir la secuencia general de los pasos de la secuencia de tareas y cómo organizar y estructurar los pasos de la secuencia de tareas en grupos lógicos. La secuencia de tareas que cree puede variar de este ejemplo y puede contener más o menos pasos de secuencia de tareas y grupos.  

> [!NOTE]  
>  Siempre debe utilizar al Asistente para medios de secuencia de tareas para crear medios independientes.  

|Grupo de secuencias de tareas o paso a paso|Descripción|  
|---------------------------------|-----------------|  
|Capturar archivos y configuraciones - **(nuevo grupo de secuencia de tareas)**|Crear un grupo de secuencia de tareas. Un grupo de secuencia de tareas mantiene los pasos de la secuencia de tareas similares para una mejor organización y control de errores.|  
|Capturar configuración de Windows|Utilice este paso de la secuencia de tareas para identificar la configuración de Microsoft Windows que se captura desde el sistema operativo existente en el equipo de destino antes de restaurar. Puede capturar el nombre de equipo, usuario e información de la organización y la configuración de zona horaria.|  
|Capturar configuración de red|Utilice este paso de la secuencia de tareas para capturar a la configuración de red desde el equipo que recibe la secuencia de tareas. Puede capturar a la pertenencia de grupo de trabajo o dominio del equipo y el adaptador de red, información de configuración.|  
|Capturar archivos de usuario y configuraciones - **(nueva tarea subelemento grupo Sequence)**|Crear un grupo de secuencia de tareas dentro de un grupo de secuencia de tareas. Este grupo secundario contiene los pasos necesarios para capturar los datos de estado de usuario desde el sistema operativo existente en el equipo de destino antes de restaurar. Similar al grupo inicial de agregado, esta mantiene subgrupos similar pasos juntos para errores y mejor organización controlan.|  
|Ubicación de establecer el estado Local|Utilice este paso de la secuencia de tareas para especificar una ubicación local mediante la variable de secuencia de tareas de ruta protegida. El estado del usuario se almacena en un directorio protegido en el disco duro.|  
|Capturar estado de usuario|Use este paso de la secuencia de tareas para capturar los archivos de usuario y la configuración que desee migrar al nuevo sistema operativo.|  
|Instalar el sistema operativo: **(nuevo grupo de secuencia de tareas)**|Cree otro grupo de subsistema de secuencia de tareas. Este grupo secundario contiene los pasos necesarios para instalar el sistema operativo.|  
|Reiniciar Windows PE o disco duro|Utilice este paso de la secuencia de tareas para especificar las opciones de reinicio del equipo que recibe esta secuencia de tareas. Este paso mostrará un mensaje al usuario indicando que se reiniciará el equipo para que pueda continuar la instalación.<br /><br /> Este paso usa solo lectura **_SMSTSInWinPE** variable de secuencia de tareas. Si el valor asociado es igual a **false** continuará con el paso de la secuencia de tareas.|  
|Aplicar sistema operativo|Utilice este paso de la secuencia de tareas para instalar la imagen de sistema operativo en el equipo de destino. En este paso se eliminan todos los archivos de dicho volumen (con la excepción de los archivos de control específicos de Configuration Manager) y, luego, se aplican todas las imágenes de volumen del archivo WIM al volumen de disco secuencial correspondiente. También puede especificar un **sysprep** archivo de respuesta para configurar qué partición de disco que se utilizará para la instalación.|  
|Aplicar configuraciones de Windows|Utilice este paso de la secuencia de tareas para configurar la información de configuración de la configuración de Windows para el equipo de destino. Puede aplicar la configuración de windows es usuarios e información organizativa, información de clave de producto o licencia, zona horaria y la contraseña de administrador local.|  
|Aplicar configuración de red|Utilice este paso de la secuencia de tareas para especificar la información de configuración de red o grupo de trabajo del equipo de destino. También puede especificar si el equipo utiliza un servidor DHCP o puede asignar estáticamente la información de dirección IP.|  
|Aplicar paquete de controladores|Utilice este paso de la secuencia de tareas para hacer que todos los controladores de dispositivo en un paquete de controladores disponibles para su uso por el programa de instalación de Windows. Todos los controladores de dispositivo necesarios deben estar contenidos en el medio independiente.|  
|La instalación de sistema operativo: **(nuevo grupo de secuencia de tareas)**|Cree otro grupo de subsistema de secuencia de tareas. Este subgrupo contiene los pasos necesarios para instalar el cliente de Configuration Manager.|  
|Instalar Windows y Configuration Manager|Use este paso de secuencia de tareas para instalar el software cliente de Configuration Manager. Configuration Manager instala y registra el GUID del cliente de Configuration Manager. Puede asignar los parámetros de instalación necesarios en la ventana **Propiedades de instalación** .|  
|Restaurar archivos de usuario y la configuración - **(nuevo grupo de secuencia de tareas)**|Cree otro grupo de subsistema de secuencia de tareas. Este grupo secundario contiene los pasos necesarios para restaurar el estado del usuario.|  
|Restaurar estado de usuario|Use este paso de secuencia de tareas para iniciar la herramienta de migración de estado de usuario (USMT) con el fin de restaurar la configuración y el estado de usuario que se capturaron con la acción Capturar estado de usuario en el equipo de destino.|  
