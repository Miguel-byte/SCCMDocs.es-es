---
title: "Usar el Centro de software para implementar Windows a través de la red | Configuration Manager"
description: "Puede implementar un sistema operativo en el Centro de software para actualizar un equipo existente con una nueva versión de Windows o para actualizar Windows a la versión más reciente."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 189fdac38760b75eb3795348f6af4ef7e83c3f20


---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Use Centro de software para implementar Windows a través de la red con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

La secuencia de tareas para instalar un sistema operativo en System Center Configuration Manager puede estar disponible en el Centro de software. Puede implementar un sistemas operativo en Centro de software en los siguientes escenarios de implementación de sistema operativo:  

-   [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Actualizar Windows a la versión más reciente](upgrade-windows-to-the-latest-version.md)  

 Complete los pasos de uno de los escenarios de implementación de sistema operativo y luego use las secciones siguientes para prepararse para las implementaciones disponibles en el Centro de software.  

## <a name="configure-deployment-settings"></a>Configurar la implementación  
 Cuando quiera que la implementación del sistema operativo esté disponible en el Centro de software, debe configurar la implementación para que el sistema operativo esté disponible para los clientes de Configuration Manager. Puede configurar esto en la página **Configuración de implementación** del Asistente para implementar Software o en la pestaña **Configuración de implementación** en las propiedades de la implementación.  Para la configuración **Estar disponible para** , configure **Solo clientes de Configuration Manager** o **PXE, medios y clientes de Configuration Manager**. Después de implementar el sistema operativo, se mostrará en el Centro de software para los miembros de la recopilación de destino.  

##  <a name="a-namebkmkdeploya-deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a> Implemente la secuencia de tareas en los equipos.  
 Implemente el sistema operativo en una recopilación de destino. Para obtener más información, vea [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Al implementar sistemas operativos para el Centro de software, puede configurar si la implementación es necesaria o está disponible.  

-   **Implementación necesaria**: las implementaciones necesarias harán que el sistema operativo esté disponible en el Centro de software, pero se iniciará automáticamente según la programación de asignación configurada.  

-   **Implementación disponible**: el sistema operativo estará disponible en el Centro de software y el usuario puede instalarlo a petición.  



<!--HONumber=Nov16_HO1-->


