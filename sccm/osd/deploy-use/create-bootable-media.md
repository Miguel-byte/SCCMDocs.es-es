---
title: Crear medios de arranque en Configuration Manager | Microsoft Docs
description: "Los medios de arranque de Configuration Manager facilitan instalar una nueva versión de Windows o reemplazar un equipo y transferir la configuración."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
caps.latest.revision: 11
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 89158debdf4c345a325feeb608db2215a88ed81b
ms.openlocfilehash: 9032698fa12bf453041ea06bf330d3b4687c2a97
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017


---
# <a name="create-bootable-media-with-system-center-configuration-manager"></a>Crear medios de arranque con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los medios de arranque de Configuration Manager contienen la imagen de arranque, comandos de preinicio y archivos asociados opcionales y archivos de Configuration Manager. Use los medios preconfigurados para los siguientes escenarios de implementación de sistema operativo:  

-   [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Reemplazar un equipo existente y transferir la configuración](replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_CreateBootableMedia"></a> Crear medios de arranque  
 Si se arranca en el medio de arranque, el equipo de destino se inicia, se conecta a la red y recupera la secuencia de tareas específica, la imagen de sistema operativo y cualquier otro tipo de contenido necesario de la red. Dado que la secuencia de tareas no está en el medio, puede cambiar la secuencia de tareas o el contenido sin tener que volver a crear el medio. Los paquetes en el medio de arranque no se cifran. Debe adoptar las medidas de seguridad adecuadas, como agregar una contraseña a los medios, para asegurarse de que el contenido del paquete está protegido contra usuarios no autorizados.  

 Antes de crear medios de arranque con el Asistente para crear medio de secuencia de tareas, asegúrese de que se cumplen las condiciones siguientes:  

|Tarea|Descripción|  
|----------|-----------------|  
|Imagen de arranque|Tenga en cuenta los siguientes datos sobre la imagen de arranque que usará en la secuencia de tareas para implementar el sistema operativo:<br /><br /> - La arquitectura de la imagen de arranque debe ser adecuada para la arquitectura del equipo de destino. Por ejemplo, un equipo de destino x64 puede arrancar y ejecutar una imagen de arranque x86 o x64. Sin embargo, un equipo de destino x86 solo puede arrancar y ejecutar una imagen de arranque x86.<br />- Asegúrese de que la imagen de arranque contiene los controladores de almacenamiento y de red necesarios para aprovisionar el equipo de destino.|  
|Crear una secuencia de tareas para implementar un sistema operativo|Como parte de los medios de arranque, debe especificar la secuencia de tareas para implementar un sistema operativo. Para obtener los pasos para crear una nueva secuencia de tareas, consulte [Create a task sequence to install an operating system](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md) (Crear una secuencia de tareas para instalar un sistema operativo).|  
|Distribuir todo el contenido asociado con la secuencia de tareas|Debe distribuir todo el contenido requerido por la secuencia de tareas a un punto de distribución como mínimo. Esto incluye la imagen de arranque y otros archivos de preinicio de asociados. El asistente recopila la información del punto de distribución al crear los medios de arranque. Debe tener derechos de acceso de **lectura** para la biblioteca de contenido de dicho punto de distribución.  Para obtener más información, consulte [About the content library](../../core/plan-design/hierarchy/the-content-library.md) (Acerca de la biblioteca de contenido).|  
|Preparar la unidad USB extraíble|Para una unidad USB extraíble:<br /><br /> Si va a usar una unidad USB extraíble, dicha unidad debe estar conectada al equipo donde se ejecuta el asistente y debe ser detectada por Windows como un dispositivo de eliminación. El asistente escribe directamente en la unidad extraíble cuando crea los medios. Los medios independientes utilizan un sistema de archivos FAT32. No se pueden crear medios independientes en una unidad flash USB cuyo contenido incluye un archivo de más de 4 GB de tamaño.|  
|Crear una carpeta de salida|Para un conjunto de CD o DVD:<br /><br /> Antes de ejecutar el Asistente para crear medio de secuencia de tareas para crear medios para un conjunto de CD o DVD, debe crear una carpeta para los archivos de salida creados por el asistente. El medio creado para un conjunto de CD o DVD se escribe como archivo .iso directamente en esa carpeta.|  

 Utilice el procedimiento siguiente para crear medios de arranque.  

### <a name="to-create-bootable-media"></a>Para crear medios de arranque  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear medio de secuencia de tareas** para iniciar el Asistente para crear medio de secuencia de tareas.  

4.  En la página **Seleccionar tipo de medio** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    -   Seleccione **Medio de arranque**.  

    -   Opcionalmente, si desea permitir solo que el sistema operativo se implemente sin requerir intervención del usuario, seleccione **Permitir la implementación desatendida de sistema operativo**.  

        > [!IMPORTANT]  
        >  Cuando se selecciona esta opción, no se solicita al usuario que brinde información de configuración de red ni que realice secuencias de tareas opcionales. No obstante, se seguirá solicitando una contraseña al usuario si el medio está configurado para la protección con contraseña.  

5.  En la página **Administración de medio** , especifique una de las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    -   Seleccione **Medio dinámico** si desea permitir que un punto de administración redirija el medio a otro punto de administración, según la ubicación del cliente en los límites del sitio.  

    -   Seleccione **Medio basado en sitio** si desea que el medio solo se ponga en contacto con el punto de administración especificado.  

6.  En la página **Tipo de medios** , especifique si se trata de una unidad flash o un conjunto de CD o DVD y luego haga clic para configurar los siguientes elementos:  

    > [!IMPORTANT]  
    >  Los medios independientes utilizan un sistema de archivos FAT32. No se pueden crear medios independientes en una unidad flash USB cuyo contenido incluye un archivo de más de 4 GB de tamaño.  

    -   Si selecciona **Unidad flash USB**, especifique la unidad en la que quiere almacenar el contenido.  

    -   Si selecciona **Conjunto de CD/DVD**, especifique la capacidad del medio y el nombre y la ruta de acceso de los archivos de salida. El asistente escribe los archivos de salida en esta ubicación. Por ejemplo: **\\\nombre de servidor\carpeta\archivo de salida.iso**  

         Si la capacidad de los medios es demasiado pequeña para almacenar todo el contenido, se crean varios archivos y debe almacenar el contenido en varios CD o DVD. Si se requieren varios medios, Configuration Manager agrega un número de secuencia al nombre de cada archivo de salida que crea. Además, si implementa una aplicación junto con el sistema operativo y la aplicación no cabe en un solo medio, Configuration Manager almacena la aplicación en varios medios. Cuando se ejecuta el medio independiente, Configuration Manager pide al usuario el siguiente medio en el que se almacena la aplicación.  

        > [!IMPORTANT]  
        >  Si selecciona una imagen .iso existente, el Asistente para crear medio de secuencia de tareas elimina la imagen de la unidad o el recurso compartido cuando pasa a la siguiente página del asistente. Se elimina la imagen existente incluso si, a continuación, se cancela al asistente.  

     Haga clic en **Siguiente**.  

7.  En la página **Seguridad** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    -   Active la casilla **Habilitar compatibilidad de equipos desconocida** para permitir que el medio implemente un sistema operativo en un equipo que no esté administrado por Configuration Manager. No hay ningún registro de estos equipos en la base de datos de Configuration Manager.  

         Los equipos desconocidos incluyen los siguientes:  

        -   Un equipo que no tiene instalado el cliente de Configuration Manager  

        -   Un equipo que no se importa en Configuration Manager  

        -   Un equipo que no ha detectado Configuration Manager  

    -   Active la casilla **Proteger medio con contraseña** y escriba una contraseña segura para ayudar a proteger el medio frente a un acceso no autorizado. Al especificar una contraseña, el usuario debe proporcionar dicha contraseña para poder utilizar el medio de arranque.  

        > [!IMPORTANT]  
        >  Por seguridad, se recomienda siempre asignar una contraseña para ayudar a proteger los medios de arranque.  

    -   Para comunicaciones HTTP, seleccione **Crear certificado autofirmado de medio**y, a continuación, especifique las fechas de inicio y de expiración del certificado.  

    -   Para comunicaciones HTTPS, seleccione **Importar certificado PKI**y, a continuación, especifique el certificado que desea importar y su contraseña.  

         Para obtener más información sobre este certificado de cliente que se usa para imágenes de arranque, consulte [PKI certificate requirements](../../core/plan-design/network/pki-certificate-requirements.md) (Requisitos de certificado PKI).  

    -   **Afinidad entre usuario y dispositivo**: para admitir la administración centrada en el usuario en Configuration Manager, especifique cómo quiere que el medio asocie los usuarios con el equipo de destino. Para obtener más información sobre cómo es compatible la implementación de sistema operativo con la afinidad entre usuario y dispositivo, consulte [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md) (Asociar usuarios con un equipo de destino).  

        -   Especifique **Permitir afinidad de dispositivo de usuario con autoaprobación** si desea que el medio asocie automáticamente los usuarios al equipo de destino. Esta funcionalidad se basa en las acciones de la secuencia de tareas que implementa el sistema operativo. En este escenario, la secuencia de tareas crea una relación entre los usuarios especificados y el equipo de destino cuando se implementa el sistema operativo en el equipo de destino.  

        -   Especifique **Permitir afinidad de dispositivo de usuario pendiente de la aprobación del administrador** si desea que el medio asocie los usuarios al equipo de destino después de conceder la aprobación. Esta funcionalidad se basa en el ámbito de la secuencia de tareas que implementa el sistema operativo.  En este escenario, la secuencia de tareas crea una relación entre los usuarios especificados y el equipo de destino, pero espera la aprobación del usuario administrativo antes de implementar el sistema operativo.  

        -   Especifique **No permitir afinidad de dispositivo de usuario** si no desea que el medio asocie usuarios al equipo de destino. En este escenario, la secuencia de tareas no asocia usuarios al equipo de destino cuando se implementa el sistema operativo.  

8.  En la página **Imagen de arranque** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    > [!IMPORTANT]  
    >  La arquitectura de la imagen de arranque que se distribuye debe ser adecuada para la arquitectura del equipo de destino. Por ejemplo, un equipo de destino x64 puede arrancar y ejecutar una imagen de arranque x86 o x64. Sin embargo, un equipo de destino x86 solo puede arrancar y ejecutar una imagen de arranque x86.  

    -   En el cuadro **Imagen de arranque** , especifique la imagen de arranque para iniciar el equipo de destino.  

    -   En el cuadro **Punto de distribución** , especifique el punto de distribución donde reside la imagen de arranque. El asistente recupera la imagen de arranque desde el punto de distribución y la escribe en el medio.  

        > [!NOTE]  
        >  Debe tener derechos de acceso de **lectura** en la biblioteca de contenido del punto de distribución.  

    -   Si crea medios de arranque basados en sitio en la página **Administración de medio** del asistente, especifique un punto de administración de un sitio primario en el cuadro **Punto de administración** .  

    -   Si crea medios de arranque dinámicos en la página **Administración de medio** del asistente, especifique los puntos de administración del sitio primario que se usarán y un orden de prioridad para las comunicaciones iniciales en **Puntos de administración asociados**.  

9. En la página **Personalización** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    -   Especifique las variables que la secuencia de tareas utiliza para implementar el sistema operativo.  

    -   Especifique los comandos de preinicio que desee ejecutar antes de que se ejecute la secuencia de tareas. Los comandos de preinicio son un script o un ejecutable que puede interactuar con el usuario en Windows PE antes de que se ejecute la secuencia de tareas para instalar el sistema operativo. Para obtener más información, consulte [Prestart commands for task sequence media](../understand/prestart-commands-for-task-sequence-media.md) (Comandos de preinicio para medios de secuencia de tareas).  

        > [!TIP]  
        >  Durante la creación de medios de secuencia de tareas, la secuencia de tareas escribe el identificador de paquete y el comando de preinicio, incluidos los valores de las variables de secuencia de tareas, en el archivo de registro CreateTSMedia.log en el equipo que ejecuta la consola de Configuration Manager. Puede revisar este archivo de registro para comprobar el valor de las variables de secuencia de tareas.  

         Si lo desea, active la casilla **Incluir archivos para el comando de preinicio** para incluir los archivos que el comando de preinicio necesita.  

10. Complete el asistente.  

## <a name="create-bootable-media-on-a-usb-drive-from-a-network-share"></a>Crear medios de arranque en una unidad USB desde un recurso compartido de red
La información de esta sección le ayuda a crear medios de arranque en una unidad flash USB, cuando la unidad flash no está conectada al equipo que ejecuta la consola de Configuration Manager. Para crear el medio de arranque en la unidad USB, puede crear medios de arranque de secuencia de tareas, montar la imagen ISO y transferir los archivos desde la imagen ISO a la unidad USB.

1. [Crear el medio de arranque de secuencia de tareas](#to-create-task-boobable-media). En la página **Tipo de medio**, seleccione **Conjunto de CD/DVD**. El asistente escribe los archivos de salida en la ubicación que especifique. Por ejemplo: **\\\nombre de servidor\carpeta\archivo de salida.iso**.  
2. Prepare la unidad USB extraíble. Debe ser una unidad de con formato, vacía y de arranque.
3. Monte la imagen ISO desde la ubicación del recurso compartido y transfiera los archivos desde la imagen ISO a la unidad USB.

## <a name="next-steps"></a>Pasos siguientes  
[Usar medios de arranque para implementar Windows a través de la red](use-bootable-media-to-deploy-windows-over-the-network.md)  

