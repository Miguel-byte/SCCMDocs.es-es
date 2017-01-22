---
title: "Usar medios de arranque para implementar Windows a través de la red | Microsoft Docs"
description: Use implementaciones de medios de arranque en System Center Configuration Manager para implementar el sistema operativo al iniciar el equipo de destino.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: beb730efbe4d9bae7c4c97f4e587c8919bd79049


---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Use medios de arranque para implementar Windows a través de la red con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Las implementaciones de medios de arranque en System Center Configuration Manager le permiten implementar el sistema operativo al iniciar el equipo de destino. Cuando se inicia el equipo de destino, recupera la secuencia de tareas, la imagen de sistema operativo y cualquier otro tipo de contenido necesario de la red. Debido a que el contenido no se incluye en los medios, puede actualizar el contenido sin tener que volver a crear los medios.  

 Puede implementar sistemas operativos a través de la red mediante multidifusión en los siguientes escenarios de implementación de sistema operativo:  

-   [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Reemplazar un equipo existente y transferir la configuración](replace-an-existing-computer-and-transfer-settings.md)  

 Complete los pasos de uno de los escenarios de implementación de sistema operativo y luego use las secciones siguientes para usar medios de arranque para implementar el sistema operativo.  

## <a name="configure-deployment-settings"></a>Configurar la implementación  
 Cuando use un medio de arranque para iniciar el proceso de implementación del sistema operativo, debe configurar la implementación para que el sistema operativo esté disponible para los medios. Puede configurar esto en la página **Configuración de implementación** del Asistente para implementar Software o en la pestaña **Configuración de implementación** en las propiedades de la implementación.  Para la opción de configuración **Estar disponible para** , configure uno de los siguientes:  

-   **Clientes de Configuration Manager, medios y PXE**  

-   **Solo medios y PXE**  

-   **Sólo medios y PXE (ocultos)**  

## <a name="create-the-bootable-media"></a>Crear medios de arranque  
 Puede especificar si el medio de arranque es una unidad flash USB o un conjunto de CD/DVD. El equipo que iniciará el medio debe admitir la opción que elija como unidad de arranque. Para obtener más información, consulte [Crear medios de arranque](create-bootable-media.md).  

##  <a name="a-namebkmkdeploya-install-the-operating-system-from--bootable-media"></a><a name="BKMK_Deploy"></a> Instalar el sistema operativo desde un medio de arranque  
 Inserte el medio de arranque en una unidad de arranque en el equipo y luego vuelva a encenderlo para instalar el sistema operativo.  



<!--HONumber=Dec16_HO3-->


