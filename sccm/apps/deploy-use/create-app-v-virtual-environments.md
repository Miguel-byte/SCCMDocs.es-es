---
title: Crear entornos virtuales de App-V | System Center Configuration Manager
description: "Cree entornos virtuales con Microsoft Application Virtualization para que las aplicaciones puedan compartir datos entre sí."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 625ea93d855089f6dbbdcc8368032e61b8a1ba0b


---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>Crear entornos virtuales de App-V en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los entornos virtuales de Microsoft Application Virtualization (App-V) en System Center Configuration Manager permiten a las aplicaciones virtuales implementadas compartir el mismo sistema de archivos y el Registro en equipos cliente de Windows. Esto significa que, a diferencia de las aplicaciones virtuales estándar, estas aplicaciones pueden compartir datos entre sí. Los entornos virtuales se crean o modifican en equipos cliente cuando se instala la aplicación o cuando los clientes vuelven a evaluar sus aplicaciones instaladas. Puede ordenar las aplicaciones para que cuando varias aplicaciones intenten modificar un valor del Registro o del sistema de archivos, la aplicación con el orden más alto tenga prioridad.  

> [!IMPORTANT]  
>  No se base en entornos virtuales de App-V para proporcionar protección de seguridad (por ejemplo, contra malware).  

 Use el procedimiento siguiente para crear entornos virtuales de App-V en Configuration Manager.  

## <a name="create-an-app-v-virtual-environment"></a>Crear un entorno virtual de App-V  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Entornos virtuales de App-V**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear entorno virtual**.  

4.  En el cuadro de diálogo **Crear entorno virtual** , especifique la siguiente información:  

    -   **Nombre** : especifique un nombre único para el entorno virtual con un máximo de 128 caracteres.  

    -   **Descripción** : si lo desea, especifique una descripción para el entorno virtual.  

5.  Haga clic en **Agregar** para agregar un nuevo tipo de implementación para el entorno virtual. Debe agregar al menos un tipo de implementación.  

6.  En el cuadro de diálogo **Agregar aplicaciones** , especifique un **Nombre de grupo** de hasta 128 caracteres que usará para referirse al grupo de aplicaciones que agrega al entorno virtual.  

7.  Haga clic en **Agregar**, seleccione los tipos de implementación y las aplicaciones de App-V 5 que desea agregar al grupo y, a continuación, haga clic en **Aceptar**.  

8.  En el cuadro de diálogo **Agregar aplicaciones** , haga clic en **Aumentar orden** o **Disminuir orden** para especificar la aplicación que tendrá prioridad si varias aplicaciones intentan modificar la configuración del Registro o del sistema de archivos en el mismo entorno virtual.  

9. Haga clic en **Aceptar** para volver al cuadro de diálogo **Crear entorno virtual** .  

10. Cuando haya terminado de agregar grupos, haga clic en **Aceptar** para crear el entorno virtual. El nuevo entorno virtual se muestra en el nodo **Entornos virtuales de App-V** de la consola de Configuration Manager. Puede supervisar el estado de los entornos virtuales mediante el informe **Estado del entorno virtual de App-V**.  

    > [!NOTE]  
    >  El entorno virtual se agregará o modificará en equipos cliente cuando la aplicación se instale o cuando el cliente vuelva a evaluar las aplicaciones instaladas.  



<!--HONumber=Nov16_HO1-->


