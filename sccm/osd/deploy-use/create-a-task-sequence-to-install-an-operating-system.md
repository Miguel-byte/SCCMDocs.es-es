---
title: Crear una secuencia de tareas para instalar un sistema operativo
titleSuffix: Configuration Manager
description: Use secuencias de tareas de System Center Configuration Manager para instalar automáticamente una imagen de sistema operativo y otro contenido en un equipo de destino.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 604cf10c660cd1f26513a6a34b370d380635504b
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421083"
---
# <a name="create-a-task-sequence-to-install-an-operating-system-in-system-center-configuration-manager"></a>Crear una secuencia de tareas para instalar un sistema operativo en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use secuencias de tareas de System Center Configuration Manager para instalar automáticamente una imagen de sistema operativo en un equipo de destino. Cree una secuencia de tareas que haga referencia a la imagen de arranque que se usa para iniciar el equipo de destino, la imagen de sistema operativo que quiere instalar en el equipo de destino y cualquier otro contenido adicional (por ejemplo, otras aplicaciones o actualizaciones de software) que quiera instalar. A continuación, implemente la secuencia de tareas en la recopilación que contiene el equipo de destino.  

##  <a name="BKMK_InstallOS"></a> Crear una secuencia de tareas para instalar un sistema operativo  
 Hay muchos escenarios para implementar un sistema operativo en los equipos de su entorno. En la mayoría de los casos, creará una secuencia de tareas y seleccionará **Instalar un paquete de imágenes existente** en el Asistente para crear secuencias de tareas a fin de instalar el sistema operativo, migrar la configuración de usuario, aplicar las actualizaciones de software e instalar las aplicaciones. Antes de crear una secuencia de tareas para instalar un sistema operativo, debe contar con lo siguiente:   

-   **Requerido**  

    -   La [imagen de arranque](../get-started/manage-boot-images.md) debe estar disponible en la consola de Configuration Manager.  

    -   Debe haber una [imagen de sistema operativo](../get-started/manage-operating-system-images.md) disponible en la consola de Configuration Manager.  

-   **Necesario (si se usa)**  

    -   Las [actualizaciones de software](../../sum/get-started/synchronize-software-updates.md) deben estar sincronizadas en la consola de Configuration Manager.  

    -   Las [aplicaciones](../../apps/deploy-use/create-applications.md) deben agregarse a la consola de Configuration Manager.  

#### <a name="to-create-a-task-sequence-that-installs-an-operating-system"></a>Para crear una secuencia de tareas que instale un sistema operativo  

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2. En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear secuencia de tareas** para iniciar el Asistente para crear secuencia de tareas.  

4. En la página **Crear nueva secuencia de tareas** , haga clic en **Instalar un paquete de imágenes existente**y, a continuación, haga clic en **Siguiente**.  

5. En la página **Información de secuencia de tareas** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

   -   **Nombre de la secuencia de tareas**: especifique un nombre que identifique la secuencia de tareas.  

   -   **Descripción**: especifique una descripción de la tarea que se realiza mediante la secuencia de tareas.  

   -   **Imagen de arranque**: especifique la imagen de arranque que instala el sistema operativo en el equipo de destino. La imagen de arranque contiene una versión de Windows PE que se utiliza para instalar el sistema operativo, así como los controladores de dispositivo adicionales que son necesarios. Para más información, vea [Manage boot images (Administrar imágenes de arranque)](../get-started/manage-boot-images.md).  

       > [!IMPORTANT]  
       >  La arquitectura de la imagen de arranque debe ser compatible con la arquitectura de hardware del equipo de destino.  

6. En la página **Instalar Windows** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

   -   **Paquete de imagen**: especifique el paquete que contiene la imagen de sistema operativo que desea instalar. Para obtener más información, consulte [Administrar imágenes de sistema operativo](../get-started/manage-operating-system-images.md).  

   -   **Imagen**: si el paquete de imágenes de sistema operativo contiene varias imágenes, especifique el índice de la imagen de sistema operativo que desea instalar.  

   -   **Particionar y formatear el equipo de destino antes de instalar el sistema operativo**: especifique si desea que la secuencia de tareas particione y formatee el equipo de destino antes de instalar el sistema operativo.  

   -   **Clave de producto**: especifique la clave de producto para el sistema operativo Windows que desea instalar. Puede especificar claves de licencia por volumen codificadas y claves de producto estándar. Si utiliza una clave de producto no codificada, cada grupo de 5 caracteres debe estar separado por un guión (-). Por ejemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

   -   **Modo de licencia de servidor**: especifique que la licencia de servidor es **Por puesto**, **Por servidor**, o bien que no se especifica ninguna licencia. Si la licencia de servidor es **Por servidor**, especifique también el número máximo de conexiones de servidor.  

   -   Especifique cómo administrar la cuenta de administrador que se utiliza cuando se implementa la imagen de sistema operativo.  

       -   **Deshabilitar cuenta de administrador local**: especifique si la cuenta de administrador local se deshabilita cuando se implementa la imagen de sistema operativo.  

       -   **Usar siempre la misma contraseña de administrador**: especifique si se utiliza la misma contraseña para la cuenta de administrador local en todos los equipos donde se implementa la imagen de sistema operativo.  

7. En la página **Configurar red** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

   -   **Unirse a un grupo de trabajo**: especifique si desea agregar el equipo de destino a un grupo de trabajo.  

   -   **Unirse a un dominio**: especifique si desea agregar el equipo de destino a un dominio. En **Dominio**, especifique el nombre del dominio.  

       > [!IMPORTANT]  
       >  Puede examinar para localizar los dominios del bosque local, pero debe especificar el nombre de dominio para un bosque remoto.  

        También puede especificar una unidad organizativa (OU). Es una configuración opcional que especifica el nombre distintivo LDAP X.500 de la unidad organizativa en la que se va a crear la cuenta de equipo si aún no existe.  

   -   **Cuenta**: especifique el nombre de usuario y la contraseña de la cuenta que tenga permisos para unirse al dominio especificado. Por ejemplo: *dominio\usuario* o *%variable%*.  

       > [!IMPORTANT]  
       >  Debe especificar las credenciales de dominio apropiadas si planea migrar la configuración del dominio o la configuración del grupo de trabajo.  

8. En la página **Instalar Configuration Manager**, especifique el paquete de cliente de Configuration Manager que quiere instalar en el equipo de destino y, después, haga clic en **Siguiente**.  

9. En la página **Migración de estado** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    -   **Capturar configuración de usuario**: especifique si la secuencia de tareas captura el estado de usuario. Para más información sobre cómo capturar y restaurar el estado de usuario, vea [Manage user state (Administrar el estado de usuario)](../get-started/manage-user-state.md).  

    -   **Capturar configuración de red**: especifique si la secuencia de tareas captura la configuración de red del equipo de destino. Puede capturar la pertenencia del dominio o del grupo de trabajo además de la configuración del adaptador de red.  

    -   **Capturar configuración de Microsoft Windows**:  especifique si la secuencia de tareas captura la configuración de Windows del equipo antes de que se instale la imagen de sistema operativo. Puede capturar el nombre de equipo, el nombre de usuario registrado y de organización, y la configuración de zona horaria.  

10. En la página **Incluir actualizaciones** , especifique si desea instalar las actualizaciones de software necesarias, todas las actualizaciones de software o ninguna y, a continuación, haga clic en **Siguiente**. Si especifica que se instalen las actualizaciones de software, Configuration Manager instala solo las que se destinan a las colecciones a las que pertenece el equipo de destino.  

11. En la página **Instalar aplicaciones** , especifique las aplicaciones que desee instalar en el equipo de destino y, a continuación, haga clic en **Siguiente**. Si especifica varias aplicaciones, también puede especificar que la secuencia de tareas continúe si se produce un error en la instalación de una aplicación específica.  

12. Complete el asistente.  

    Ahora puede implementar la secuencia de tareas en una recopilación de equipos.  Para obtener más información, vea [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

##  <a name="BKMK_InstallExistingOSImageTSExample"></a> Ejemplo de secuencia de tareas para instalar la imagen de sistema operativo existente  
 Use la tabla siguiente como guía para crear una secuencia de tareas que implemente un sistema operativo mediante una imagen de sistema operativo existente. La tabla le ayudará a decidir la secuencia general de los pasos de la secuencia de tareas y cómo organizar y estructurar los pasos de la secuencia de tareas en grupos lógicos. La secuencia de tareas que cree puede variar desde este ejemplo y puede contener más o menos pasos de secuencia de tareas y grupos.  

> [!IMPORTANT]  
>  Siempre debe utilizar al Asistente para crear la secuencia de tareas para crear esta secuencia de tareas.  

 Cuando se utiliza el Asistente para crear la secuencia de tareas para crear esta secuencia de tareas nueva algunos de los nombres de paso de secuencia de tareas son diferentes a lo que de lo sería si agrega manualmente estos pasos de la secuencia de tareas a una secuencia de tareas existente. En la tabla siguiente muestra las diferencias de nomenclatura:  

|Crear nombre de paso de secuencia de tareas del Asistente de secuencia de tareas|Nombre del paso de Editor de secuencia de tareas equivalente|  
|---------------------------------------------------------|-----------------------------------------------|  
|Almacenamiento de información de estado de usuario de solicitud|Solicitar almacén de estado|  
|Capturar archivos de usuario y configuración|Capturar estado de usuario|  
|Almacenamiento de información de estado de usuario de la versión|Liberar almacén de estado|  
|Reiniciar en Windows PE|Reiniciar en Windows PE o disco duro|  
|Disco de partición 0|Formatear y crear particiones en el disco|  
|Restaurar archivos de usuario y configuración|Restaurar estado de usuario|  

|Grupo o paso de secuencia de tareas|Descripción|  
|---------------------------------|-----------------|  
|Capturar archivos y configuraciones - **(nuevo grupo de secuencia de tareas)**|Crear un grupo de secuencia de tareas. Un grupo de secuencia de tareas mantiene pasos similares de secuencia de tareas para una mejor organización y un control de errores.<br /><br /> Este grupo contiene los pasos necesarios para capturar archivos y configuraciones del sistema operativo de un equipo de referencia.|  
|Capturar configuración de Windows|Utilice este paso de la secuencia de tareas para identificar la configuración de Microsoft Windows para capturar desde el equipo de referencia. Puede capturar el nombre de equipo, usuario e información de la organización y la configuración de zona horaria.|  
|Capturar configuración de red|Utilice este paso de la secuencia de tareas para capturar a la configuración de red del equipo de referencia. Puede capturar a la pertenencia de grupo de trabajo o dominio del equipo de referencia y el adaptador de red, información de configuración.|  
|Capturar archivos de usuario y configuraciones - **(nueva tarea subelemento grupo Sequence)**|Crear un grupo de secuencia de tareas dentro de un grupo de secuencia de tareas. Este grupo secundario contiene los pasos necesarios para capturar los datos de estado de usuario. Similar al grupo inicial que ha agregado, este subgrupo mantiene juntos los pasos similares de la secuencia de tareas para mejorar la organización y el control de errores.|  
|Almacenamiento de información de estado de usuario de solicitud|Utilice este paso de la secuencia de tareas para solicitar acceso a un punto de migración de estado donde se almacenan los datos de estado de usuario. Puede configurar este paso de la secuencia de tareas para capturar o restaurar la información de estado de usuario.|  
|Capturar archivos de usuario y configuración|Use este paso de la secuencia de tareas para usar la herramienta de migración de estado de usuario (USMT) para capturar el estado de usuario y la configuración del equipo de referencia que recibirá la secuencia de tareas asociada a este paso de la tarea. Puede capturar las opciones estándar o configurar las opciones que se deben capturar.|  
|Liberar almacenamiento de estado de usuario|Utilice este paso de la secuencia de tareas para notificar el estado del punto de migración que la acción de captura o la restauración está completa.|  
|Instalar el sistema operativo: **(nuevo grupo de secuencia de tareas)**|Cree otro grupo de subsistema de secuencia de tareas. Este grupo secundario contiene los pasos necesarios para instalar y configurar el entorno Windows PE.|  
|Reiniciar en Windows PE|Utilice este paso de la secuencia de tareas para especificar las opciones de reinicio del equipo de destino que recibe esta secuencia de tareas. Este paso mostrará un mensaje al usuario indicando que se reiniciará el equipo para que pueda continuar la instalación.<br /><br /> Este paso usa la variable de secuencia de tareas **_SMSTSInWinPE** de solo lectura. Si el valor asociado es igual a **false** sigue el paso de la secuencia de tareas.|  
|Disco de partición 0|Este paso especifica las acciones necesarias para formatear el disco duro del equipo de destino. El número de disco predeterminado es **0**.<br /><br /> Este paso usa la variable de secuencia de tareas **_SMSTSClientCache** de solo lectura. Este paso se ejecutará si la memoria caché del cliente de Configuration Manager no existe.|  
|Aplicar sistema operativo|Utilice este paso de la secuencia de tareas para instalar la imagen de sistema operativo en el equipo de destino. Este paso aplica todas las imágenes de volumen contenidas en el archivo WIM al volumen de disco secuencial correspondiente en el equipo de destino después de eliminar primero todos los archivos en ese volumen (con la excepción de los archivos de control específicos de Configuration Manager). Puede especificar un **sysprep** archivo de respuesta y también configurar qué partición de disco se utiliza para la instalación.|  
|Aplicar configuraciones de Windows|Utilice este paso de la secuencia de tareas para configurar la información de configuración de la configuración de Windows para el equipo de destino. Puede aplicar la configuración de windows es usuarios e información organizativa, información de clave de producto o licencia, zona horaria y la contraseña de administrador local.|  
|Aplicar configuración de red|Utilice este paso de la secuencia de tareas para especificar la información de configuración de red o grupo de trabajo del equipo de destino. También puede especificar si el equipo utiliza un servidor DHCP o puede asignar estáticamente la información de dirección IP.|  
|Aplicar controladores del dispositivo|Utilice este paso de la secuencia de tareas para instalar a controladores como parte de la implementación de sistema operativo. Para permitir que el Programa de instalación de Windows busque todas las categorías de controladores existentes, seleccione **Considerar controladores de todas las categorías** o, para limitar las categorías de controlador en las que busca el Programa de instalación de Windows, seleccione **Limitar la coincidencia de controladores a los controladores de las categorías seleccionadas**.<br /><br /> Este paso usa solo lectura **_SMSTSMediaType** variable de secuencia de tareas. Este paso de la secuencia de tareas se ejecuta sólo si el valor de la variable no es **FullMedia**.|  
|Aplicar paquete de controladores|Utilice este paso de la secuencia de tareas para hacer que todos los controladores de dispositivo en un paquete de controladores disponibles para su uso por el programa de instalación de Windows.|  
|La instalación de sistema operativo: **(nuevo grupo de secuencia de tareas)**|Cree otro grupo de subsistema de secuencia de tareas. Este grupo secundario contiene los pasos necesitados para configurar el sistema operativo instalado.|  
|Instalar Windows y Configuration Manager|Use este paso de secuencia de tareas para instalar el software cliente de Configuration Manager. Configuration Manager instala y registra el GUID del cliente de Configuration Manager. Puede asignar los parámetros de instalación necesarios en la ventana **Propiedades de instalación** .|  
|Instalar actualizaciones|Utilice este paso de secuencia de tareas para especificar cómo se instalan las actualizaciones de software en el equipo de destino. No se evalúa si hay actualizaciones de software aplicables al equipo de destino hasta que se ejecuta este paso de secuencia de tareas. En ese momento, se evalúa si existen actualizaciones de software para el equipo de destino similares a las de cualquier otro cliente administrado de Configuration Manager.<br /><br /> Este paso usa la variable de secuencia de tareas **_SMSTSMediaType** de solo lectura. Este paso de secuencia de tareas se ejecuta solo si el valor de la variable no es igual a **FullMedia**.|  
|Restaurar archivos de usuario y configuración: **(nuevo subgrupo de secuencia de tareas)**|Cree otro grupo de subsistema de secuencia de tareas. Este grupo secundario contiene los pasos necesarios para restaurar los archivos de usuario y la configuración.|  
|Solicitar almacenamiento de estado de usuario|Utilice este paso de la secuencia de tareas para solicitar acceso a un punto de migración de estado donde se almacenan los datos de estado de usuario.|  
|Restaurar archivos de usuario y configuración|Utilice este paso de la secuencia de tareas para iniciar la herramienta de migración de estado de usuario (USMT) para restaurar el estado de usuario y la configuración en un equipo de destino.|  
|Almacenamiento de información de estado de usuario de la versión|Use este paso de secuencia de tareas para notificar al punto de migración de estado que los datos de estado de usuario ya no son necesarios.|  
