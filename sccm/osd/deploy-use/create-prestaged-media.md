---
title: Crear medios preconfigurados
titleSuffix: Configuration Manager
description: "Cree medios preconfigurados en System Center Configuration Manager para simplificar la implementación de Windows en varios escenarios."
ms.custom: na
ms.date: 04/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
caps.latest.revision: "12"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: a26fc3daf17aefe24a46ece561fc2ceaf5284ffb
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/12/2017
---
# <a name="create-prestaged-media-with-system-center-configuration-manager"></a>Crear medios preconfigurados con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los medios preconfigurados de System Center Configuration Manager son un archivo Windows Imaging Format (WIM) que puede ser instalado en un equipo sin sistema operativo por el fabricante o en un centro de configuración empresarial no relacionado con el entorno de Configuration Manager.  
Los medios preconfigurados contienen la imagen de arranque que se utiliza para iniciar el equipo de destino y la imagen de sistema operativo que se aplica al equipo de destino. También puede especificar las aplicaciones, los paquetes y los paquetes de controladores que quiere incluir como parte de los medios preconfigurados. La secuencia de tareas que implementa el sistema operativo no se incluye en el medio. Los medios preconfigurados se aplican a la unidad de disco duro de un nuevo equipo antes de enviar el equipo al usuario final. Use los medios preconfigurados para los siguientes escenarios de implementación de sistema operativo:  

-   [Crear una imagen para un OEM en fábrica o en un almacén local](../../osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

-   [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Implementar Windows to Go](deploy-windows-to-go.md)  

 Cuando el equipo se inicia por primera vez después de la aplicación del medio preconfigurado, el equipo arranca en Windows PE y se conecta a un punto de administración para encontrar la secuencia de tareas que completa el proceso de implementación de sistema operativo. Puede especificar las aplicaciones, los paquetes y los paquetes de controladores que quiere incluir como parte de los medios preconfigurados. Al implementar una secuencia de tareas que usa un medio preconfigurado, el asistente comprueba en primer lugar la presencia de contenido válido en la memoria caché local de la secuencia de tareas y, si el contenido no se encuentra o se ha revisado, el asistente lo descarga del punto de distribución.  

##  <a name="BKMK_CreatePrestagedMedia"></a> Creación de medios preconfigurados  
 Antes de crear medios preconfigurados con el Asistente para crear medio de secuencia de tareas, asegúrese de que se cumplen las condiciones siguientes:  

|Tarea|Descripción|  
|----------|-----------------|  
|Imagen de arranque|Tenga en cuenta los siguientes datos sobre la imagen de arranque que usará en la secuencia de tareas para implementar el sistema operativo:<br /><br /> - La arquitectura de la imagen de arranque debe ser adecuada para la arquitectura del equipo de destino. Por ejemplo, un equipo de destino x64 puede arrancar y ejecutar una imagen de arranque x86 o x64. Sin embargo, un equipo de destino x86 solo puede arrancar y ejecutar una imagen de arranque x86.<br />- Asegúrese de que la imagen de arranque contiene los controladores de almacenamiento y de red necesarios para aprovisionar el equipo de destino.|  
|Crear una secuencia de tareas para implementar un sistema operativo|Como parte de los medios preconfigurados, debe especificar la secuencia de tareas para implementar un sistema operativo.<br /><br /> - Para conocer los pasos necesarios para crear una nueva secuencia de tareas, consulte [Create a task sequence to install an operating system](../../osd/deploy-use/create-a-task-sequence-to-install-an-operating-system.md) (Crear una secuencia de tareas para instalar un sistema operativo).<br />- Para obtener más información sobre las secuencias de tareas, consulte [Manage task sequences to automate tasks](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md) (Administrar secuencias de tareas para automatizar tareas).|  
|Distribuir todo el contenido asociado con la secuencia de tareas|Debe distribuir todo el contenido requerido por la secuencia de tareas a un punto de distribución como mínimo. Esto incluye la imagen de arranque, la imagen de sistema operativo y otros archivos asociados. El asistente recopila la información desde el punto de distribución al crear los medios independientes. Debe tener derechos de acceso de **lectura** para la biblioteca de contenido de dicho punto de distribución.  Para obtener más información, consulte [About the content library](../../core/plan-design/hierarchy/the-content-library.md) (Acerca de la biblioteca de contenido).|  
|Unidad de disco duro del equipo de destino|El disco duro del equipo de destino debe estar formateado antes de que se realice una copia intermedia del medio preconfigurado en dicha unidad. Si el disco duro no está formateado cuando se aplique el medio, la secuencia de tareas que implementa el sistema operativo producirá un error al intentar iniciar el equipo de destino.|  

> [!NOTE]  
>  El Asistente para crear medio de secuencia de tareas establece la siguiente condición de variable de secuencia de tareas en el medio: **_SMSTSMediaType = OEMMedia**. Puede usar esta condición en la secuencia de tareas.  

 Utilice el procedimiento siguiente para crear medios preconfigurados.  

#### <a name="to-create-prestaged-media"></a>Para crear medios preconfigurados  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear medio de secuencia de tareas** para iniciar el Asistente para crear medio de secuencia de tareas.  

4.  En la página **Seleccionar tipo de medio** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    -   Seleccione **Medio preconfigurado**.  

    -   Opcionalmente, si desea permitir que el sistema operativo se implemente sin intervención del usuario, seleccione **Permitir la implementación desatendida de sistema operativo**. Cuando se selecciona esta opción, no se pide al usuario información de configuración de red ni secuencias de tareas opcionales. No obstante, se seguirá solicitando una contraseña al usuario si el medio está configurado para la protección con contraseña.  

5.  En la página **Administración de medio** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    -   Seleccione **Medio dinámico** si desea permitir que un punto de administración redirija el medio a otro punto de administración, según la ubicación del cliente en los límites del sitio.  

    -   Seleccione **Medio basado en sitio** si desea que el medio solo se ponga en contacto con el punto de administración especificado.  

6.  En la página **Propiedades de medio**  , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    -   **Creado por**: especifique el autor de lo medio.  

    -   **Versión**: especifique el número de versión del medio.  

    -   **Comentario**: escriba una descripción única del uso del medio.  

    -   **Archivo multimedia**: especifique el nombre y la ruta de acceso de los archivos de salida. El asistente escribe los archivos de salida en esta ubicación. Por ejemplo: **\\\nombre de servidor\carpeta\archivo de salida.iso**  

7.  En la página **Seguridad** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    -   Active la casilla **Habilitar compatibilidad de equipos desconocida** para permitir que el medio implemente un sistema operativo en un equipo que no esté administrado por Configuration Manager. No hay ningún registro de estos equipos en la base de datos de Configuration Manager.  Para obtener más información, consulte [Prepare for unknown computer deployments](../get-started/prepare-for-unknown-computer-deployments.md) (Preparación para implementaciones en equipos desconocidos).  

    -   Active la casilla **Proteger medio con contraseña** y escriba una contraseña segura para ayudar a proteger el medio frente a un acceso no autorizado. Cuando se especifica una contraseña, el usuario debe proporcionar esa contraseña para utilizar el medio preconfigurado.  

        > [!IMPORTANT]  
        >  Por motivos de seguridad, asigne siempre una contraseña para ayudar a proteger el medio preconfigurado.  

    -   Para comunicaciones HTTP, seleccione **Crear certificado autofirmado de medio**y, a continuación, especifique las fechas de inicio y de expiración del certificado.  

    -   Para comunicaciones HTTPS, seleccione **Importar certificado PKI**y, a continuación, especifique el certificado que desea importar y su contraseña.  

         Para obtener más información sobre este certificado de cliente que se usa para imágenes de arranque, consulte [PKI certificate requirements](../../core/plan-design/network/pki-certificate-requirements.md) (Requisitos de certificado PKI).  

    -   **Afinidad entre usuario y dispositivo**: para admitir la administración centrada en el usuario en Configuration Manager, especifique cómo quiere que el medio asocie los usuarios con el equipo de destino. Para obtener más información sobre cómo es compatible la implementación de sistema operativo con la afinidad entre usuario y dispositivo, consulte [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md) (Asociar usuarios con un equipo de destino).  

        -   Especifique **Permitir afinidad de dispositivo de usuario con autoaprobación** si desea que el medio asocie automáticamente los usuarios al equipo de destino. Esta funcionalidad se basa en las acciones de la secuencia de tareas que implementa el sistema operativo. En este escenario, la secuencia de tareas crea una relación entre los usuarios especificados y el equipo de destino cuando se implementa el sistema operativo en el equipo de destino.  

        -   Especifique **Permitir afinidad de dispositivo de usuario pendiente de la aprobación del administrador** si desea que el medio asocie los usuarios al equipo de destino después de conceder la aprobación. Esta funcionalidad se basa en el ámbito de la secuencia de tareas que implementa el sistema operativo. En este escenario, la secuencia de tareas crea una relación entre los usuarios especificados y el equipo de destino, pero espera la aprobación del usuario administrativo antes de implementar el sistema operativo.  

        -   Especifique **No permitir afinidad de dispositivo de usuario** si no desea que el medio asocie usuarios al equipo de destino. En este escenario, la secuencia de tareas no asocia usuarios al equipo de destino cuando se implementa el sistema operativo.  

8.  En la página **Secuencia de tareas** , especifique la secuencia de tareas que se ejecutará en el equipo de destino. El contenido al que hace referencia la secuencia de tareas se muestra en **Esta secuencia de tareas hace referencia al siguiente contenido**. Compruebe el contenido y, después, haga clic en **Siguiente**.  

9. En la página **Imagen de arranque** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    > [!IMPORTANT]  
    >  La arquitectura de la imagen de arranque que se distribuye debe ser adecuada para la arquitectura del equipo de destino. Por ejemplo, un equipo de destino x64 puede arrancar y ejecutar una imagen de arranque x86 o x64. Sin embargo, un equipo de destino x86 solo puede arrancar y ejecutar una imagen de arranque x86.  

    -   En el cuadro **Imagen de arranque** , especifique la imagen de arranque para iniciar el equipo de destino. Para más información, vea [Manage boot images (Administrar imágenes de arranque)](../get-started/manage-boot-images.md).  

    -   En el cuadro **Punto de distribución** , especifique el punto de distribución donde reside la imagen de arranque. El asistente recupera la imagen de arranque desde el punto de distribución y la escribe en el medio.  

        > [!NOTE]  
        >  Debe tener derechos de acceso de **lectura** para la biblioteca de contenido en el punto de distribución. Para obtener más información, consulte [About the content library](../../core/plan-design/hierarchy/the-content-library.md) (Acerca de la biblioteca de contenido).  

    -   Si seleccionó **Medio basado en sitio** en la página **Administración de medio** de este asistente, en el cuadro **Punto de administración** , especifique un punto de administración de un sitio primario.  

    -   Si seleccionó **Medio dinámico** en la página **Administración de medio** de este asistente, en el cuadro **Puntos de administración asociados** , especifique los puntos de administración del sitio primario que se usarán y un orden de prioridad para las comunicaciones iniciales.  

10. En la página **Imágenes** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    -   En el cuadro **Paquete de imágenes** , especifique la imagen de sistema operativo. Para obtener más información, consulte [Manage operating system images](../get-started/manage-operating-system-images.md) (Administrar imágenes de sistema operativo).  

    -   Si el paquete contiene varias imágenes de sistema operativo, en el cuadro **Índice de imágenes** , especifique la imagen que desee implementar.  

    -   En el cuadro **Punto de distribución** , especifique el punto de distribución donde reside el paquete de imágenes de sistema operativo. El asistente recupera la imagen de sistema operativo desde el punto de distribución y la escribe en el medio.  

11. En la página **Personalización** , especifique la siguiente información y, a continuación, haga clic en **Siguiente**.  

    -   Especifique las variables que la secuencia de tareas utiliza para implementar el sistema operativo.  

    -   Especifique los comandos de preinicio que desee ejecutar antes de que se ejecute la secuencia de tareas. Los comandos de preinicio son un script o un ejecutable que puede interactuar con el usuario en Windows PE antes de que se ejecute la secuencia de tareas para instalar el sistema operativo. Para obtener más información sobre los comandos de preinicio para los medios, consulte [Prestart commands for task sequence media](../understand/prestart-commands-for-task-sequence-media.md) (Comandos de preinicio para medios de secuencia de tareas).  

        > [!TIP]  
        >  Durante la creación de medios de secuencia de tareas, la secuencia de tareas escribe el identificador de paquete y el comando de preinicio, incluidos los valores de las variables de secuencia de tareas, en el archivo de registro CreateTSMedia.log en el equipo que ejecuta la consola de Configuration Manager. Puede revisar este archivo de registro para comprobar el valor de las variables de secuencia de tareas.  

12. Complete el asistente.  

## <a name="next-steps"></a>Pasos siguientes
[Escenarios para implementar sistemas operativos de empresa](scenarios-to-deploy-enterprise-operating-systems.md)
