---
title: Crear medios independientes
titleSuffix: Configuration Manager
description: Use un medio independiente para implementar el sistema operativo en un equipo sin conexión de red.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35dd110c2566dab945bb0701e113becb3412d65c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="create-stand-alone-media-with-system-center-configuration-manager"></a>Crear medios independientes con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los medios independientes de Configuration Manager contienen todo lo necesario para implementar el sistema operativo (SO) en un equipo que no esté conectado a la red. Use medios independientes en los siguientes escenarios de implementación de sistema operativo:  

-   [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Actualizar Windows a la versión más reciente](upgrade-windows-to-the-latest-version.md)  

Los medios independientes incluyen la secuencia de tareas que automatiza los pasos para instalar el sistema operativo, además de otros contenidos necesarios como la imagen de arranque, la imagen del sistema operativo y los controladores de dispositivos. Dado que los medios independientes contienen todo lo necesario para implementar el sistema operativo, requieren más espacio en disco que otros tipos de medios. Al crear un medio independiente en un sitio de administración central, el cliente recupera su código de sitio asignado de Active Directory. Los medios independientes que se crean en los sitios secundarios asignan automáticamente al cliente el código de sitio para dicho sitio.  

##  <a name="BKMK_CreateStandAloneMedia"></a> Crear medios independientes  
Antes de crear medios independientes con el Asistente para crear medio de secuencia de tareas, asegúrese de que se cumplen las condiciones siguientes:  

### <a name="create-a-task-sequence-to-deploy-an-operating-system"></a>Crear una secuencia de tareas para implementar un sistema operativo
Como parte de los medios independientes, debe especificar la secuencia de tareas para implementar un sistema operativo. Para obtener los pasos para crear una nueva secuencia de tareas, consulte [Create a task sequence to install an operating system in System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md) (Crear una secuencia de tareas para instalar un sistema operativo en System Center Configuration Manager).

No se admiten las siguientes acciones para medios independientes:
- El paso **Aplicar controladores automáticamente** en la secuencia de tareas. Los medios independientes no admiten la aplicación automática de controladores de dispositivos desde el catálogo de controladores. Use el paso **Aplicar paquete de controladores** para que un conjunto especificado de controladores esté disponible en el programa de instalación de Windows.
- El paso **Descargar contenido de paquete** de la secuencia de tareas. La información del punto de administración no está disponible en los medios independientes, por lo que se producirá un error en el paso al intentar enumerar las ubicaciones de contenido.
- Instalación de actualizaciones de software.
- Instalación de software antes de implementar un sistema operativo.
- Secuencias de tareas para implementaciones que no son de sistema operativo.
- Asociación de usuarios con el equipo de destino para admitir la afinidad de dispositivo de usuario.
- El paquete dinámico se instala a través de la tarea **Instalar paquetes**.
- La aplicación dinámica se instala a través de la tarea **Instalar aplicación**.

> [!NOTE]    
> Podría producirse un error si la secuencia de tareas incluye el paso [Instalar paquete](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) y usted crea los medios independientes en un sitio de administración central. El sitio de administración central no tiene las directivas de configuración de cliente necesarias. Estas directivas sirven para habilitar al agente de distribución de software durante la ejecución de la secuencia de tareas. Es probable que aparezca el siguiente error en el archivo CreateTsMedia.log:    
>     
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`    
> 
> Para los medios independientes que incluyan un paso **Instalar paquete**, cree los medios independientes en un sitio primario que tenga habilitado el agente de distribución de software. 
>
> O bien, agregue un paso [Ejecutar línea de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine) después del paso [Instalar Windows y Configuration Manager](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) y antes del primer paso **Instalar paquete** de la secuencia de tareas. El paso **Ejecutar línea de comandos** ejecuta el siguiente comando de WMIC para habilitar el agente de distribución de software antes del primer paso Instalar paquete:    
>    
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`


> [!IMPORTANT]    
> Con medios independientes, no seleccione la opción **Usar paquete de cliente de preproducción cuando esté disponible** en la secuencia de tareas **Instalar Windows y Configuration Manager**. Un medio independiente no admite el uso de esta opción. Para obtener más información sobre esta configuración, consulte [Instalar Windows y Configuration Manager](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).


### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo el contenido asociado con la secuencia de tareas
Distribuya todo el contenido requerido por la secuencia de tareas a un punto de distribución como mínimo. Este contenido incluye la imagen de arranque, la imagen de sistema operativo y otros archivos asociados. El asistente recopila la información desde el punto de distribución al crear los medios independientes. Debe tener derechos de acceso de **lectura** para la biblioteca de contenido de dicho punto de distribución. Para obtener más información, consulte [Distribuir contenido al que hace referencia una secuencia de tareas](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS).

### <a name="prepare-the-removable-usb-drive"></a>Preparar la unidad USB extraíble
*Para una unidad USB extraíble:*

Si utiliza una unidad USB extraíble, conecte la unidad USB al equipo donde se ejecuta el asistente. Windows debe identificar la unidad USB como un dispositivo extraíble. El asistente escribe directamente en la unidad extraíble cuando crea los medios. Los medios independientes utilizan un sistema de archivos FAT32. No se pueden crear medios independientes en una unidad flash USB cuyo contenido incluye un archivo de más de 4 GB de tamaño.

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

    -   Opcionalmente, si desea permitir que el sistema operativo se implemente sin intervención del usuario, seleccione **Permitir la implementación desatendida de sistema operativo**. Cuando se selecciona esta opción, no se solicita al usuario que brinde información de configuración de red ni que realice secuencias de tareas opcionales. Se seguirá solicitando una contraseña al usuario si el medio está configurado para la protección con contraseña.  

5.  En la página **Tipo de medios**, especifique si el medio es una unidad USB extraíble o un conjunto de CD/DVD:  

    > [!IMPORTANT]  
    >  De manera predeterminada, los medios independientes utilizan un sistema de archivos FAT32. No se pueden crear medios independientes en una unidad USB extraíble cuyo contenido incluya un archivo de más de 4 GB de tamaño.  

    -   Si selecciona **Unidad USB extraíble**, especifique la unidad en la que quiere almacenar el contenido.  

        - **Formatear la unidad USB extraíble (FAT32) y hacerla de arranque**: de forma predeterminada, deje que Configuration Manager prepare la unidad USB. Muchos de los nuevos dispositivos UEFI requieren una partición FAT32 de arranque. Sin embargo, este formato también limita el tamaño de los archivos y la capacidad total de la unidad. Si ya ha formateado y configurado la unidad extraíble, deshabilite esta opción. 

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
7.  En la página **CD/DVD independiente** , especifique la secuencia de tareas que implementa el sistema operativo y, a continuación, haga clic en **Siguiente**. Para agregar contenido a los medios independientes para las dependencias de la aplicación, elija **Detectar dependencias de aplicación asociadas y agregarlas a este medio**.
    > [!TIP]
    > Si no ve las dependencias de aplicación esperadas, anule la selección y luego vuelva a seleccionar la configuración **Detectar dependencias de aplicación asociadas y agregarlas a este medio** para actualizar la lista.

    El asistente le permite seleccionar las secuencias de tareas asociadas con una imagen de arranque.  

8. En la página **Seleccionar aplicación** (disponible a partir de la versión 1702), especifique el contenido de la aplicación que desea incluir como parte del archivo multimedia y después haga clic en **Siguiente**.
9. En la página **Seleccionar paquete** (disponible a partir de la versión 1702), especifique el contenido del paquete que desea incluir como parte del archivo multimedia y después haga clic en **Siguiente**.
10. En la página **Seleccionar el paquete de controladores** (disponible a partir de la versión 1702), especifique el contenido del paquete de controladores que desea incluir como parte del archivo multimedia y después haga clic en **Siguiente**.
11.  En la página **Puntos de distribución**, especifique los puntos que tengan el contenido necesario y luego haga clic en **Siguiente**.  

     Configuration Manager solo muestra los puntos de distribución que incluyen el contenido. Antes de continuar, distribuya todo el contenido asociado a la secuencia de tareas en al menos un punto de distribución. Después de distribuir el contenido, actualice la lista de puntos de distribución. Quite los puntos de distribución ya haya seleccionado en esta página, vaya a la página anterior y después regrese a la página **Puntos de distribución**. O bien, reinicie al asistente. Para obtener más información, consulte [Distribuir contenido al que hace referencia una secuencia de tareas](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) y [Administración del contenido y de la infraestructura de contenido](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    > [!NOTE]  
    >  Debe tener derechos de acceso de **lectura** para la biblioteca de contenido en los puntos de distribución.  

12. En la página **Personalización** , especifique la siguiente información y, a continuación, haga clic en **Siguiente**.  

    -   Especifique las variables que la secuencia de tareas utiliza para implementar el sistema operativo.  

    -   Especifique los comandos de preinicio que desea ejecutar antes de la secuencia de tareas. Los comandos de preinicio son un script o un archivo ejecutable que se ejecuta en Windows PE antes de que se inicie la secuencia de tareas. Para obtener más información, consulte [Prestart commands for task sequence media](../understand/prestart-commands-for-task-sequence-media.md) (Comandos de preinicio para medios de secuencia de tareas).  

         Si lo desea, active la casilla **Incluir archivos para el comando de preinicio** para incluir los archivos que el comando de preinicio necesita.  

        > [!TIP]  
        >  Durante la creación de medios de secuencia de tareas, Configuration Manager escribe el identificador de paquete y la línea de comandos de preinicio en el archivo **CreateTSMedia.log** en el equipo que ejecuta la consola de Configuration Manager. Esta salida incluye el valor de las variables de secuencia de tareas. Revise este archivo de registro para comprobar el valor de las variables de secuencia de tareas.  

13. Complete el asistente.  

 Los archivos de medios independientes (.iso) se crean en la carpeta de destino. Si seleccionó **CD/DVD independiente**, ahora puede copiar los archivos de salida a un conjunto de CD o DVD.  

##  <a name="BKMK_StandAloneMediaTSExample"></a> Ejemplo de secuencia de tareas de medios independientes  
 Utilice la tabla siguiente como guía al crear una secuencia de tareas para implementar un sistema operativo mediante medios independientes. La tabla le ayuda a decidir la secuencia general de los pasos de secuencia de tareas. También ayuda a organizar y estructurar los pasos de secuencia de tareas en grupos lógicos. La secuencia de tareas que cree puede variar de este ejemplo y puede contener más o menos pasos de secuencia de tareas y grupos.  

> [!NOTE]  
>  Siempre debe utilizar al Asistente para medios de secuencia de tareas para crear medios independientes.  

|Grupo de secuencias de tareas o paso a paso|Descripción|  
|---------------------------------|-----------------|  
|Capturar archivos y configuraciones - **(nuevo grupo de secuencia de tareas)**|Crear un grupo de secuencia de tareas. Un grupo de secuencia de tareas mantiene los pasos de la secuencia de tareas similares para una mejor organización y control de errores.|  
|Capturar configuración de Windows|Utilice este paso de secuencia de tareas para capturar la configuración de Windows en el equipo de destino antes de restablecer la imagen inicial. Capture el nombre de equipo, la información de los usuarios y la organización, y la configuración de zona horaria.|  
|Capturar configuración de red|Utilice este paso de la secuencia de tareas para capturar a la configuración de red desde el equipo que recibe la secuencia de tareas. Puede capturar a la pertenencia de grupo de trabajo o dominio del equipo y el adaptador de red, información de configuración.|  
|Capturar archivos de usuario y configuraciones: **(nuevo subgrupo de secuencia de tareas)**|Crear un grupo de secuencia de tareas dentro de un grupo de secuencia de tareas. Este subgrupo contiene los pasos para capturar los datos de estado de usuario desde el equipo de destino antes de restablecer la imagen inicial. De forma similar al grupo inicial que agregó, este subgrupo mantiene pasos de secuencia de tareas parecidos para una mejor organización y control de errores.|  
|Ubicación de establecer el estado Local|Utilice este paso de la secuencia de tareas para especificar una ubicación local mediante la variable de secuencia de tareas de ruta protegida. El estado del usuario se almacena en un directorio protegido en el disco duro.|  
|Capturar estado de usuario|Use este paso de la secuencia de tareas para capturar los archivos de usuario y la configuración que desee migrar al nuevo sistema operativo.|  
|Instalar el sistema operativo: **(nuevo grupo de secuencia de tareas)**|Cree otro subgrupo de secuencia de tareas. Este subgrupo contiene los pasos necesarios para instalar el sistema operativo.|  
|Reiniciar en Windows PE o disco duro|Utilice este paso de la secuencia de tareas para especificar las opciones de reinicio del equipo que recibe esta secuencia de tareas. Este paso muestra un mensaje al usuario indicándole que el equipo se está reiniciando para continuar con la instalación.<br /><br /> Este paso usa solo lectura **_SMSTSInWinPE** variable de secuencia de tareas. Si el valor asociado es igual a **false**, el paso de la secuencia de tareas continúa.|  
|Aplicar sistema operativo|Utilice este paso de la secuencia de tareas para instalar la imagen de sistema operativo en el equipo de destino. Este paso elimina todos los archivos del volumen, salvo los archivos de control específicos de Configuration Manager. A continuación, aplica todas las imágenes de volumen incluidas en el archivo WIM al volumen de disco secuencial correspondiente. También puede especificar un **sysprep** archivo de respuesta para configurar qué partición de disco que se utilizará para la instalación.|  
|Aplicar configuraciones de Windows|Utilice este paso de secuencia de tareas para definir la información de configuración de valores de Windows para el equipo de destino. Esta configuración incluye información de usuarios e información organizativa, información de clave de producto o licencia, zona horaria y la contraseña de administrador local.|  
|Aplicar configuración de red|Utilice este paso de la secuencia de tareas para especificar la información de configuración de red o grupo de trabajo del equipo de destino. También puede especificar si el equipo utiliza un servidor DHCP o puede asignar estáticamente la información de dirección IP.|  
|Aplicar paquete de controladores|Utilice este paso de la secuencia de tareas para hacer que todos los controladores de dispositivo en un paquete de controladores disponibles para su uso por el programa de instalación de Windows. Todos los controladores de dispositivo necesarios deben estar contenidos en el medio independiente.|  
|La instalación de sistema operativo: **(nuevo grupo de secuencia de tareas)**|Cree otro subgrupo de secuencia de tareas. Este subgrupo contiene los pasos necesarios para instalar el cliente de Configuration Manager.|  
|Instalar Windows y Configuration Manager|Use este paso de secuencia de tareas para instalar el software cliente de Configuration Manager. Configuration Manager instala y registra el GUID del cliente de Configuration Manager. Puede asignar los parámetros de instalación necesarios en la ventana **Propiedades de instalación** .|  
|Restaurar archivos de usuario y la configuración - **(nuevo grupo de secuencia de tareas)**|Cree otro subgrupo de secuencia de tareas. Este subgrupo contiene los pasos necesarios para restaurar el estado del usuario.|  
|Restaurar estado de usuario|Utilice este paso de secuencia de tareas para iniciar la herramienta de migración de estado de usuario (USMT). USMT restaura en el equipo de destino el estado de usuario y la configuración que se ha capturado previamente con el paso Capturar estado de usuario.|  
