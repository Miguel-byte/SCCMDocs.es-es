---
title: Crear una secuencia de tareas para capturar un sistema operativo
titleSuffix: Configuration Manager
description: "Una secuencia de tareas de captura y compilación crea un equipo de referencia que puede incluir controladores concretos y actualizaciones de software junto con el sistema operativo."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
caps.latest.revision: "19"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 48530c177a03b66dbc126025ca61e0078bc89d9f
ms.sourcegitcommit: 5ec9f8c312688bf7f4de4d6007b121d743b80c4d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2017
---
# <a name="create-a-task-sequence-to-capture-an-operating-system-in-system-center-configuration-manager"></a>Crear una secuencia de tareas para capturar un sistema operativo en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Cuando use una secuencia de tareas para implementar un sistema operativo en un equipo en System Center Configuration Manager, el equipo instala la imagen de sistema operativo que especifique en la secuencia de tareas. Para personalizar la imagen de sistema operativo de modo que incluya ciertos controladores, aplicaciones, actualizaciones de software, etc., utilice una secuencia de tareas de generación y captura para generar un equipo de referencia y, a continuación, capturar la imagen del sistema operativo de ese equipo de referencia. Si ya tiene un equipo de referencia disponible para capturar, puede crear una secuencia de tareas personalizada para capturar el sistema operativo. Utilice las siguientes secciones para capturar un sistema operativo personalizado.  

##  <a name="BKMK_BuildCaptureTS"></a> Utilizar una secuencia de tareas para generar y capturar un equipo de referencia  
 La secuencia de tareas de compilación y captura particiona y aplica formato al equipo de referencia, instala el sistema operativo, así como el cliente de Configuration Manager, las aplicaciones y las actualizaciones de software y, luego, captura el sistema operativo del equipo de referencia. Los paquetes asociados a la secuencia de tareas, como las aplicaciones, deben estar disponibles en los puntos de distribución antes de crear la secuencia de tareas de generación y captura.  

###  <a name="BKMK_CreatePackages"></a> Prepararse para la implementación de sistemas operativos  
 Hay muchos escenarios para implementar un sistema operativo en los equipos de su entorno. En la mayoría de los casos, creará una secuencia de tareas y seleccionará **Instalar un paquete de imágenes existente** en el Asistente para crear secuencias de tareas a fin de instalar el sistema operativo, migrar la configuración de usuario, aplicar las actualizaciones de software e instalar las aplicaciones. Antes de crear una secuencia de tareas para instalar un sistema operativo, debe contar con lo siguiente:  

-   **Requerido**  

    -   La [imagen de arranque](../get-started/manage-boot-images.md) debe estar disponible en la consola de Configuration Manager.  

    -   Debe haber una [imagen de sistema operativo](../get-started/manage-operating-system-images.md) disponible en la consola de Configuration Manager.  

-   **Necesario (si se usa)**  

    -   Los [paquetes de controladores](../get-started/manage-drivers.md) que contienen los controladores de Windows necesarios para admitir el hardware del equipo de referencia deben estar disponibles en la consola de Configuration Manager. Para más información sobre los pasos de la secuencia de tareas para administrar controladores, vea [Use task sequences to install device drivers (Usar secuencias de tareas para instalar controladores de dispositivos)](../get-started/manage-drivers.md#BKMK_TSDrivers).  

    -   Las [actualizaciones de software](../../sum/get-started/synchronize-software-updates.md) deben estar sincronizadas en la consola de Configuration Manager.  

    -   Las [aplicaciones](../../apps/deploy-use/create-applications.md) deben agregarse a la consola de Configuration Manager.  

###  <a name="BKMK_CreateBuildCaptureTS"></a> Crear una secuencia de tareas de generación y captura  
 Utilice el siguiente procedimiento para usar una secuencia de tareas para generar un equipo de referencia y capturar el sistema operativo.  

#### <a name="to-create-a-task-sequence-that-builds-and-captures-an-operating-system-image"></a>Para crear una secuencia de tareas que cree y capture una imagen de sistema operativo  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear secuencia de tareas** para iniciar el Asistente para crear secuencia de tareas.  

4.  En la página **Crear una nueva secuencia de tareas** , seleccione **Generar y capturar una imagen de sistema operativo de referencia**.  

5.  En la página **Información de secuencia de tareas** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

    -   **Nombre de secuencia de tareas**: especifique un nombre que identifique la secuencia de tareas.  

    -   **Descripción**: escriba una descripción de la tarea realizada por la secuencia de tareas, como una descripción del sistema operativo que se crea mediante la secuencia de tareas.  

    -   **Imagen de arranque**: especifique la imagen de arranque que instala la imagen de sistema operativo.  

        > [!IMPORTANT]  
        >  La arquitectura de la imagen de arranque debe ser compatible con la arquitectura de hardware del equipo de destino.  

6.  En la página **Instalar Windows** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

    -   **Paquete de imagen**: especifique el paquete de imagen de sistema operativo, que contiene los archivos necesarios para instalar el sistema operativo.  

    -   **Índice de imagen**: especifique el sistema operativo que va a instalar. Si la imagen de sistema operativo contiene varias versiones, seleccione la versión que desee instalar.  

    -   **Clave de producto**: especifique la clave de producto para el sistema operativo Windows que quiere instalar. Puede especificar claves de licencia por volumen codificadas y claves de producto estándar. Si utiliza una clave de producto no codificada, cada grupo de 5 caracteres debe estar separado por un guión (-). Por ejemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Modo de licencia de servidor**: especifique que la licencia de servidor sea **Por puesto**, **Por servidor**o que no se especifica ninguna licencia. Si la licencia de servidor es **Por servidor**, especifique también el número máximo de conexiones de servidor.  

    -   Especifique cómo administrar la cuenta de administrador que se utiliza cuando se implementa el sistema operativo.  

        -   **Generar la contraseña de administrador local aleatoriamente y deshabilitar la cuenta en todas las plataformas admitidas**: especifique si quiere que Configuration Manager cree una contraseña aleatoria para la cuenta de administrador local y deshabilite la cuenta cuando se implemente el sistema operativo.  

        -   **Habilitar la cuenta y especificar la contraseña de administrador local**: especifique si se utilizará la misma contraseña para la cuenta de administrador local en todos los equipos donde se implemente el sistema operativo.  

7.  En la página **Configurar red** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

    -   **Unirse a un grupo de trabajo**: especifique si desea agregar el equipo de destino a un grupo de trabajo cuando se implemente el sistema operativo.  

    -   **Unirse a un dominio**: especifique si desea agregar el equipo de destino a un dominio cuando se implemente el sistema operativo. En **Dominio**, especifique el nombre del dominio.  

        > [!IMPORTANT]  
        >  Puede examinar para localizar los dominios del bosque local, pero debe especificar el nombre de dominio para un bosque remoto.  

         También puede especificar una unidad organizativa (OU). Es una configuración opcional que especifica el nombre distintivo LDAP X.500 de la unidad organizativa en la que se va a crear la cuenta de equipo si aún no existe.  

    -   **Cuenta**: especifique el nombre de usuario y la contraseña de la cuenta que tenga permisos para unirse al dominio especificado. Por ejemplo: *dominio\usuario* o *%variable%*.  

        > [!IMPORTANT]  
        >  Debe especificar las credenciales de dominio apropiadas si planea migrar la configuración del dominio o la configuración del grupo de trabajo.  

8.  En la página **Instalar Configuration Manager**, especifique el paquete de cliente de Configuration Manager que contiene los archivos de origen para instalar el cliente de Configuration Manager, agregue las propiedades adicionales necesarias para instalar el cliente y, luego, haga clic en **Siguiente**.  

     Para más información sobre las propiedades que se pueden usar para instalar un cliente, vea [Acerca de las propiedades de instalación de cliente](../../core/clients/deploy/about-client-installation-properties.md).  

9. En la página **Incluir actualizaciones** , especifique si desea instalar las actualizaciones de software necesarias, todas las actualizaciones de software o ninguna y, a continuación, haga clic en **Siguiente**. Si especifica que se instalen las actualizaciones de software, Configuration Manager instala solo las que se destinan a las colecciones a las que pertenece el equipo de destino.  

10. En la página **Instalar aplicaciones** , especifique las aplicaciones que desee instalar en el equipo de destino y, a continuación, haga clic en **Siguiente**. Si especifica varias aplicaciones, también puede especificar que la secuencia de tareas continúe si se produce un error en la instalación de una aplicación específica.  

11. En la página **Preparación del sistema** , especifique los valores siguientes y, a continuación, haga clic en **Siguiente**.  

    -   **Paquete**: especifique el paquete de Configuration Manager que contiene la versión adecuada de Sysprep para capturar la configuración del equipo de referencia.  

         Si la versión del sistema operativo que está ejecutando es Windows Vista o posterior, Sysprep se instala automáticamente en el equipo y no es necesario especificar un paquete.  

12. En la página **Propiedades de imagen** , especifique los valores siguientes para la imagen de sistema operativo y, a continuación, haga clic en **Siguiente**.  

    -   **Creado por**: especifique el nombre del usuario que creó la imagen de sistema operativo.  

    -   **Versión**: especifique un número de versión definido por el usuario que se asocie a la imagen de sistema operativo.  

    -   **Descripción**: especifique una descripción definida por el usuario de la imagen de sistema operativo.  

13. En la página **Capturar imagen** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    -   **Ruta de acceso**: especifique una carpeta de red compartida donde se guardará el archivo .WIM. Este archivo contiene la imagen de sistema operativo basada en la configuración que especifique en este asistente. Si especifica una carpeta que contenga un archivo .WIM, el archivo existente se sobrescribirá.  

    -   **Cuenta**: especifique la cuenta de Windows que tenga permisos para el recurso compartido de red donde se almacena la imagen.  

14. Complete el asistente.  

15. Para agregar pasos adicionales a la secuencia de tareas, seleccione la secuencia de tareas que creó, y haga clic en **Editar**. Para más información sobre cómo editar una secuencia de tareas, vea [Edit a task sequence (Editar una secuencia de tareas)](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

 Implemente la secuencia de tareas en un equipo de referencia según una de las maneras siguientes:  

-   Si el equipo de referencia es un cliente de Configuration Manager, puede implementar la secuencia de tareas de compilación y captura en la colección que contiene el equipo de referencia. Para más información sobre cómo implementar la imagen de sistema operativo, vea [Crear una secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).  

    > [!NOTE]  
    >  Si la secuencia de tareas tiene un paso de partición de disco, no seleccione la opción **Programa de descarga** cuando implemente la secuencia de tareas.  

-   Si el equipo de referencia no es un cliente de Configuration Manager o si quiere ejecutar manualmente la secuencia de tareas en el equipo de referencia, ejecute el **Asistente para crear medio de secuencia de tareas** para crear un medio de arranque. Para más información sobre cómo crear un medio de arranque, vea [Create bootable media (Crear medios de arranque)](create-bootable-media.md).  

##  <a name="BKMK_CaptureExistingRefComputer"></a> Capturar una imagen de sistema operativo a partir de un equipo de referencia existente  
 Si ya tiene un equipo de referencia listo para capturar, puede crear una secuencia de tareas que capture el sistema operativo a partir del equipo de referencia. Utilizará el paso de la secuencia de tareas **Capturar imagen de sistema operativo** para capturar una o más imágenes en un equipo de referencia y almacenarlas en un archivo de imagen (.wim) en el recurso compartido de red especificado. El equipo de referencia se inicia en Windows PE mediante una imagen de arranque, cada unidad de disco duro del equipo de referencia se captura como una imagen independiente en el archivo .wim. Si el equipo de referencia tiene varias unidades, el archivo .wim resultante contendrá una imagen independiente para cada volumen. Solo se capturan los volúmenes formateados como NTFS o FAT32. Se omiten los volúmenes con otros formatos y los volúmenes USB.  

 Siga el procedimiento a continuación para capturar una imagen de sistema operativo a partir de un equipo de referencia existente.  

#### <a name="to-capture-an-operating-system-from-an-existing-reference-computer"></a>Para capturar una imagen de sistema operativo a partir de un equipo de referencia existente  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear secuencia de tareas** para iniciar el Asistente para crear secuencia de tareas.  

4.  En la página **Crear una nueva secuencia de tareas** , seleccione **Crear una nueva secuencia de tareas personalizada**.  

5.  En la página **Información de secuencia de tareas** , especifique un nombre para la secuencia de tareas y una descripción de la secuencia de tareas.  

6.  Especifique una imagen de arranque para la secuencia de tareas. Esta imagen de arranque se utiliza para iniciar el equipo de referencia con Windows PE.  Para más información, vea [Manage boot images (Administrar imágenes de arranque)](../get-started/manage-boot-images.md).  

7.  Complete el asistente.  

8.  En **Secuencias de tareas**, seleccione la secuencia de tareas personalizada y, a continuación, en la pestaña **Inicio** , en el grupo **Secuencia de tareas** , haga clic en **Editar** para abrir el editor de secuencia de tareas.  

9. Use este paso solo si el cliente de Configuration Manager está instalado en el equipo de referencia.  

     Haga clic en **Agregar**, en **Imágenes** y finalmente en [Preparar el cliente de Configuration Manager para la captura](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture). Este paso de secuencia de tareas toma el cliente de Configuration Manager instalado en el equipo de referencia y lo prepara para la captura como parte del proceso de creación de imágenes.  

    > [!Note]  
    >  La secuencia de tareas no es compatible con la desinstalación del cliente de Configuration Manager.

10. Haga clic en **Agregar**, en **Imágenes** y finalmente en [Preparar Windows para la captura](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture). Esta acción de secuencia de tareas ejecuta Sysprep y, a continuación, reinicia el equipo en la imagen de arranque de Windows PE especificada para la secuencia de tareas. Para que esta acción se complete correctamente, el equipo de referencia no debe estar unido a un dominio.  

11. Haga clic en **Agregar**, en **Imágenes** y finalmente en [Capturar imagen de sistema operativo](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  Este paso de la secuencia de tareas únicamente se ejecutará desde Windows PE para capturar las unidades de disco duras del equipo de referencia. Configure las siguientes opciones para el paso de la secuencia de tareas.  

    -   **Nombre** y **Descripción**: si lo desea, puede cambiar el nombre de paso de la secuencia de tareas y escribir una descripción.  

    -   **Destino**: especifique una carpeta de red compartida donde se guardará el archivo .WIM. Este archivo contiene la imagen de sistema operativo basada en la configuración que especifique en este asistente. Si especifica una carpeta que contenga un archivo .WIM, el archivo existente se sobrescribirá.  

    -   **Descripción**, **Versión**y **Creado por**: a elección, proporcione detalles acerca de la imagen que capturará.  

    -   **Cuenta de captura de imagen del sistema operativo**: especifique la cuenta de Windows que tenga permisos para el recurso compartido de red que especificó. Haga clic en **Establecer** para especificar el nombre de esa cuenta de Windows.  

     Haga clic en **Aceptar** para cerrar el editor de secuencia de tareas.  

 Implemente la secuencia de tareas en un equipo de referencia según una de las maneras siguientes:  

-   Si el equipo de referencia es un cliente de Configuration Manager, puede implementar la secuencia de tareas en la colección que contiene el equipo de referencia. Para más información sobre cómo implementar la imagen de sistema operativo, vea [Crear una secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).  

-   Si el equipo de referencia no es un cliente de Configuration Manager o si quiere ejecutar manualmente la secuencia de tareas en el equipo de referencia, ejecute el **Asistente para crear medio de secuencia de tareas** para crear un medio de arranque. Para más información sobre cómo crear un medio de arranque, vea [Create bootable media (Crear medios de arranque)](create-bootable-media.md).  

##  <a name="BKMK_BuildandCaptureTSExample"></a> Ejemplo de secuencia de tareas para generar y capturar una imagen de sistema operativo  
 Utilice la tabla siguiente como guía para crear una secuencia de tareas que genere y capture una imagen de sistema operativo. La tabla le ayudará a decidir la secuencia general de los pasos de la secuencia de tareas y cómo organizar y estructurar los pasos de la secuencia de tareas en grupos lógicos. La secuencia de tareas que cree puede ser diferente a la de este ejemplo y puede contener más o menos pasos y grupos de secuencias de tareas.  

> [!IMPORTANT]  
>  Siempre use el Asistente para crear secuencia de tareas para crear este tipo de secuencia de tareas.  

 Cuando utilice **Nueva secuencia de tareas** para crear esta nueva secuencia de tareas, algunos de los nombres de los pasos de la secuencia de tareas son diferentes de lo serían si agregase manualmente estos pasos de secuencia de tareas a una secuencia de tareas existente. En la tabla siguiente, se muestran las diferencias de nomenclaturas:  

|Nombre del paso de la secuencia de tareas del Asistente para nueva secuencia de tareas|Nombre del paso equivalente en el Editor de secuencia de tareas|  
|------------------------------------------------------|-----------------------------------------------|  
|Reiniciar en Windows PE|Reiniciar en Windows PE o disco duro|  
|Disco de partición 0|Formatear y crear particiones en el disco|  
|Aplicar controladores del dispositivo|Aplicar controladores automáticamente|  
|Instalar actualizaciones|Instalar actualizaciones de software|  
|Unirse a grupo de trabajo|Unirse a dominio o grupo de trabajo|  
|Preparar el cliente de Configuration Manager|Prepare ConfigMgr Client for Capture|  
|Preparar el sistema operativo|Prepare Windows for Capture|  
|Capturar el equipo de referencia|Capturar imagen de sistema operativo|  

|Grupo/paso de secuencia de tareas|Referencia|  
|-------------------------------|---------------|  
|Generar el equipo de referencia **(nuevo grupo de secuencia de tareas)**|Crear un grupo de secuencia de tareas. Un grupo de secuencia de tareas mantiene pasos similares de secuencia de tareas para una mejor organización y un control de errores.<br /><br /> Este grupo contiene las acciones necesarias para generar un equipo de referencia.|  
|Reiniciar en Windows PE|Utilice este paso de secuencia de tareas para especificar las opciones de reinicio del equipo de destino. Este paso mostrará un mensaje al usuario para indicar que el equipo se reiniciará de modo que pueda continuar la instalación.<br /><br /> Este paso usa la variable de secuencia de tareas **_SMSTSInWinPE** de solo lectura. Si el valor asociado es igual a **false** , continuará con el paso de secuencia de tareas.|  
|Disco de partición 0|Utilice este paso de secuencia de tareas para especificar las acciones necesarias para formatear el disco duro del equipo de destino. El número de disco predeterminado es **0**.<br /><br /> Este paso usa la variable de secuencia de tareas **_SMSTSClientCache** de solo lectura. Este paso se ejecutará si la memoria caché del cliente de Configuration Manager no existe.|  
|Aplicar sistema operativo|Utilice este paso de secuencia de tareas para instalar una imagen de sistema operativo especificada en el equipo de destino. Este paso aplica todas las imágenes de volumen contenidas en el archivo WIM al volumen de disco secuencial correspondiente en el equipo de destino después de eliminar primero todos los archivos en ese volumen (con la excepción de los archivos de control específicos de Configuration Manager).|  
|Aplicar configuraciones de Windows|Utilice este paso de secuencia de tareas para definir la información de configuración de valores de Windows para el equipo de destino.|  
|Aplicar configuración de red|Utilice este paso de secuencia de tareas para especificar la información de configuración de red o grupo de trabajo del equipo de destino.|  
|Aplicar controladores del dispositivo|Utilice este paso de secuencia de tareas para comparar e instalar controladores como parte de la implementación del sistema operativo. Para permitir que el Programa de instalación de Windows busque todas las categorías de controladores existentes, seleccione **Considerar controladores de todas las categorías** o, para limitar las categorías de controlador en las que busca el Programa de instalación de Windows, seleccione **Limitar la coincidencia de controladores a los controladores de las categorías seleccionadas**.<br /><br /> Este paso usa la variable de secuencia de tareas **_SMSTSMediaType** de solo lectura. Si el valor asociado no es igual a **FullMedia** , se ejecutará este paso de secuencia de tareas.|  
|Instalar Windows y Configuration Manager|Use este paso de secuencia de tareas para instalar el software cliente de Configuration Manager. Configuration Manager instala y registra el GUID del cliente de Configuration Manager. Puede asignar los parámetros de instalación necesarios en la ventana **Propiedades de instalación** .|  
|Instalar actualizaciones|Utilice este paso de secuencia de tareas para especificar cómo se instalan las actualizaciones de software en el equipo de destino. No se evalúa si hay actualizaciones de software aplicables al equipo de destino hasta que se ejecuta este paso de secuencia de tareas. En ese momento, se evalúa si existen actualizaciones de software para el equipo de destino similares a las de cualquier otro cliente administrado de Configuration Manager.<br /><br /> Este paso usa la variable de secuencia de tareas **_SMSTSMediaType** de solo lectura. Si el valor asociado no es igual a **FullMedia** , se ejecutará este paso de secuencia de tareas.|  
|Capturar el equipo de referencia **(nuevo grupo de secuencia de tareas)**|Crear otro grupo de secuencia de tareas. Este grupo contiene los pasos necesarios para preparar y capturar un equipo de referencia.|  
|Unirse a grupo de trabajo|Utilice este paso de secuencia de tareas para especificar la información necesaria para que el equipo de destino se una a un grupo de trabajo.|  
|Prepare ConfigMgr Client for Capture|Use este paso para tomar el cliente de Configuration Manager instalado en el equipo de referencia y prepararlo para la captura como parte del proceso de creación de imágenes|  
|Preparar el sistema operativo|Utilice este paso de secuencia de tareas para especificar las opciones de Sysprep que se usarán al capturar la configuración de Windows del equipo de referencia. Este paso de secuencia de tareas ejecuta Sysprep y, a continuación, reinicia el equipo en la imagen de arranque de Windows PE especificada para la secuencia de tareas.|  
|Capturar imagen de sistema operativo|Utilice este paso de secuencia de tareas para especificar un recurso compartido de red existente específico y un archivo .wim que se usará al guardar la imagen. Esta ubicación se utiliza como ubicación de origen del paquete cuando se agrega un paquete de imágenes de sistema operativo mediante el **Asistente para agregar el paquete de imágenes de sistema operativo**.|  

 Después de haber capturado una imagen de un equipo de referencia, no capture otra imagen del sistema operativo del equipo de referencia porque las entradas del Registro se crean durante la configuración inicial. Cree un nuevo equipo de referencia cada vez que capture una imagen del sistema operativo. Si planea usar el mismo equipo de referencia para crear futuras imágenes de sistema operativo, primero debe desinstalar el cliente de Configuration Manager y luego volverlo a instalar.  

## <a name="next-steps"></a>Pasos siguientes  
[Métodos para implementar sistemas operativos de empresa](methods-to-deploy-enterprise-operating-systems.md)
