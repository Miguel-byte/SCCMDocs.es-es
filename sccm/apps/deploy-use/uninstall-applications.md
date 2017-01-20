---
title: Desinstalar aplicaciones | System Center Configuration Manager
description: "Desinstalar una aplicación mediante System Center Configuration Manager"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
caps.latest.revision: 4
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9f654d899a1e3e1603eccb3943ffc4d4c178e143


---
# <a name="uninstall-applications-with-system-center-configuration-manager"></a>Desinstalar aplicaciones con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


## <a name="introduction"></a>Introducción  
  
-   Especifique la línea de comandos para desinstalar el contenido del tipo de implementación en la página **Contenido** del **Asistente para crear tipos de implementación**.  

-   Implemente la aplicación mediante la acción de implementación **Desinstalar**.  

> [!IMPORTANT]  
>  Algunos tipos de aplicaciones no admiten la desinstalación.  

 La lista siguiente proporciona más información acerca del comportamiento de desinstalación de la aplicación:  

-   Cuando se desinstala una aplicación de Configuration Manager, las aplicaciones dependientes no se desinstalan de forma automática.  

-   Si implementa una aplicación que usa la acción **Desinstalar** en un usuario, y la aplicación se instaló para todos los usuarios del equipo, entonces, la desinstalación podría presentar un error si la cuenta de usuario no tiene permisos para desinstalar la aplicación.  

-   Si quita un usuario o un dispositivo de una recopilación que tiene implementada una aplicación, la aplicación no se quitará automáticamente del dispositivo.  

-   Una implementación con el propósito de implementación **Desinstalar** no comprueba las reglas de requisitos. Si la aplicación está instalada en el equipo donde se ejecuta la implementación, se desinstalará.  

> [!IMPORTANT]  
>  Debe eliminar todas las implementaciones existentes o implementaciones simuladas de una aplicación en una recopilación para poder implementar la aplicación con la acción de implementación **Desinstalar**.  
  
 Para obtener más información sobre cómo crear un tipo de implementación, consulte [Crear aplicaciones](../../apps/deploy-use/create-applications.md).  
  
 Para obtener más información sobre cómo implementar una aplicación, consulte [Implementar aplicaciones](../../apps/deploy-use/deploy-applications.md).  
  
## <a name="uninstall-an-application"></a>Desinstalar una aplicación  

1.  Configure el tipo de implementación de la aplicación con la línea de comandos de desinstalación mediante alguno de los métodos siguientes:  

    -   En la página **General** del **Asistente para crear implementación**, seleccione **Identificar automáticamente la información sobre este tipo de implementación a partir de los archivos de instalación**. Si la información está disponible en los archivos de instalación, la línea de comandos de desinstalación se agrega automáticamente a las propiedades del tipo de implementación.  

    -   En la página **Contenido** del **Asistente para crear tipos de implementación**, en el campo **Programa de desinstalación** , especifique la línea de comandos para desinstalar la aplicación.  

        > [!NOTE]  
        >  La página **Contenido** se muestra solo si selecciona la opción **Especificar manualmente la información del tipo de implementación** en la página **General** del **Asistente para crear tipos de implementación**.  

    -   En la pestaña **Programas** del cuadro de diálogo **Propiedades** de *<nombre de tipo de implementación\>*, especifique la línea de comandos para desinstalar la aplicación en el campo **Desinstalar programa**.  

2.  Implemente la aplicación y seleccione la acción de implementación **Desinstalar** en la página **Configuración de implementación** del **Asistente para implementar software**.  

    > [!NOTE]  
    >  Al seleccionar la acción de implementación **Desinstalar**, el propósito de la implementación se configura automáticamente como **Requerido**.  



<!--HONumber=Nov16_HO1-->


