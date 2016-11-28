---
title: "Administración de paquetes de actualización de sistema operativo | Configuration Manager"
description: "Aprenda a administrar paquetes de actualización de sistema operativo en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
caps.latest.revision: 12
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 226e283b5d9a04d2a9e0f3ce6894a82a3683d972


---
# <a name="manage-operating-system-upgrade-packages-with-system-center-configuration-manager"></a>Administrar paquetes de actualización de sistema operativo con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Un paquete de actualización de System Center Configuration Manager contiene los archivos de origen de instalación de Windows que se usan para actualizar un sistema operativo existente en un equipo. Use las siguientes secciones para administrar los paquetes de actualización del sistema operativo en Configuration Manager.

##  <a name="a-namebkmkaddosupgradepkgsa-add-operating-system-upgrade-packages-to-configuration-manager"></a><a name="BKMK_AddOSUpgradePkgs"></a> Incorporación de paquetes de actualización de sistema operativo a Configuration Manager  
 Para poder usar un paquete de actualización de sistema operativo, es necesario agregarlo a un sitio de Configuration Manager. Use el procedimiento siguiente para agregar un paquete de actualización de sistema operativo a un sitio.  

#### <a name="to-add-an-operating-system-upgrade-package"></a>Para agregar un paquete de actualización de sistema operativo  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y haga clic en **Paquetes de actualización de sistema operativo**.  

3.  En la pestaña **Inicio** , del grupo **Crear** , haga clic en **Agregar paquete de actualización de sistema operativo** para iniciar el Asistente para agregar paquete de actualización de sistema operativo.  

4.  En la página **Origen de datos** , especifique la ruta de acceso de red a los archivos de origen de instalación del paquete de actualización de sistema operativo. Por ejemplo, especifique la ruta UNC **\\\\servidor\rutaDeAcceso** donde se encuentran los archivos de origen de instalación.  

    > [!NOTE]  
    >  Los archivos de origen de instalación contienen Setup.exe y otros archivos y carpetas para instalar el sistema operativo.  

    > [!IMPORTANT]  
    >  Limite el acceso a los archivos de origen de instalación para evitar la manipulación no deseada.  

5.  En la página **General** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**. Esta información es útil para propósitos de identificación cuando se agregan varios instaladores de sistema operativo.  

    -   **Nombre**: especifique el nombre del instalador de sistema operativo.  

    -   **Versión**: especifique la versión del instalador de sistema operativo.  

    -   **Comentario**: especifique una breve descripción del instalador de sistema operativo.  

6.  Complete el asistente.  

 Ahora puede distribuir el instalador de sistema operativo a los puntos de distribución a los que tienen acceso las secuencias de tareas de implementación.  

##  <a name="a-namebkmkdistributebootimagesa-distribute-operating-system-images-to-a-distribution-point"></a><a name="BKMK_DistributeBootImages"></a> Distribución de imágenes de sistema operativo a un punto de distribución  
 Las imágenes de sistema operativo se distribuyen a los puntos de distribución de la misma forma que se distribuye otro tipo de contenido. En la mayoría de los casos, debe distribuir la imagen de sistema operativo a un punto de distribución, como mínimo, antes de implementar el sistema operativo. Para conocer los pasos de distribución de una imagen de sistema operativo, vea [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content) (Distribuir contenido).  

##  <a name="a-namebkmkosupgradepkgapplyupdatesa-apply-software-updates-to-an-operating-system-upgrade-package"></a><a name="BKMK_OSUpgradePkgApplyUpdates"></a> Aplicación de actualizaciones de software a un paquete de actualización del sistema operativo  
 A partir de Configuration Manager versión 1602, puede aplicar actualizaciones de software nuevas a la imagen de sistema operativo en el paquete de actualización del sistema operativo. Por supuesto, antes de aplicar las actualizaciones de software a un paquete de actualización debe contar con la infraestructura de actualizaciones de software y haber sincronizado correctamente dichas actualizaciones. Para obtener más información, consulte [Deploy software updates](../../sum/deploy-use/deploy-software-updates.md) (Implementación de actualizaciones de software).  

 Puede aplicar las actualizaciones de software que sean aplicables a un paquete de actualización según una programación especificada. En función de la programación que especifique, Configuration Manager aplica las actualizaciones de software que seleccione al paquete de actualización del sistema operativo y, opcionalmente, distribuye el paquete actualizado de actualizaciones a los puntos de distribución. La información sobre el paquete de actualización del sistema operativo se almacena en la base de datos del sitio, incluidas las actualizaciones de software que se aplicaron en el momento de la importación. Las actualizaciones de software que se hayan aplicado al paquete de actualización desde que se agregó inicialmente también se almacenan en la base de datos del sitio. Cuando inicia el asistente para aplicar actualizaciones de software al paquete de actualización del sistema operativo, el asistente recupera una lista de actualizaciones de software aplicables aún no aplicadas al paquete de actualización para seleccionar la deseada. Configuration Manager copia las actualizaciones de software de la biblioteca de contenido que se encuentra en el servidor de sitio y las aplica al paquete de actualización del sistema operativo.  

 Utilice el siguiente procedimiento para aplicar las actualizaciones de software a un paquete de actualización del sistema operativo.  

#### <a name="to-apply-software-updates-to-an-operating-system-upgrade-package"></a>Para aplicar las actualizaciones de software a un paquete de actualización del sistema operativo  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y haga clic en **Paquetes de actualización de sistema operativo**.  

3.  Seleccione el paquete de actualización del sistema operativo al que desea aplicar actualizaciones de software.  

4.  En la pestaña **Inicio** , en el grupo **Paquetes de actualización del sistema operativo** , haga clic en **Programar actualizaciones** para iniciar el asistente.  

5.  En la página **Elija las actualizaciones** , seleccione las actualizaciones de software que desea aplicar a la imagen de sistema operativo y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Establecer programación** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

    1.  **Programación**: especifique la programación para el momento en el que deben aplicarse las actualizaciones de software a la imagen de sistema operativo.  

    2.  **Continuar después de un error**: seleccione esta opción para continuar con la aplicación de las actualizaciones de software a la imagen incluso cuando se produzca un error.  

    3.  **Distribuir la imagen a los puntos de distribución**: seleccione esta opción para actualizar la imagen de sistema operativo en los puntos de distribución después de que se apliquen las actualizaciones de software.  

7.  En la página **Resumen** , compruebe la información y, a continuación, haga clic en **Siguiente**.  

8.  En la página **Finalización** , compruebe que las actualizaciones de software se aplicaron correctamente a la imagen de sistema operativo.  



<!--HONumber=Nov16_HO1-->


