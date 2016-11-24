---
title: "Usar multidifusión para implementar Windows a través de la red | Configuration Manager"
description: "Use multidifusión en su entorno de System Center Configuration Manager para que varios equipos puedan descargar simultáneamente la imagen de sistema operativo."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
caps.latest.revision: 13
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: da83037a28194e3bae1e6afe4d4bca1ce43f2bf6


---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Usar multidifusión para implementar Windows a través de la red con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Multidifusión es un método de optimización de red que puede usar en el entorno de System Center Configuration Manager si es probable que varios clientes descarguen la misma imagen de sistema operativo al mismo tiempo. Cuando se usa multidifusión, varios equipos descargan la imagen de sistema operativo de forma simultánea a medida que el punto de distribución la reparte mediante multidifusión, en lugar de que el punto de distribución envíe una copia de los datos a cada cliente a través de una conexión separada.  

 Puede implementar sistemas operativos a través de la red mediante multidifusión en los siguientes escenarios de implementación de sistema operativo:  

-   [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)  

 Complete los pasos de uno de los escenarios de implementación de sistema operativo y luego use las secciones siguientes para admitir la multidifusión.  

##  <a name="a-namebkmkconfigurea-configure-a-distribution-point-to-support-multicast"></a><a name="BKMK_Configure"></a> Configurar un punto de distribución para admitir la multidifusión  
 Antes de usar la multidifusión durante la implementación del sistema operativo, debe configurar un punto de distribución para admitir la multidifusión. Para obtener más información, consulte [Configure distribution points to support multicast](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast) (Configuración de puntos de distribución para admitir la multidifusión).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>Preparar una imagen de sistema operativo para implementaciones de multidifusión  
 Para configurar el paquete de imagen de sistema operativo para admitir la multidifusión, consulte [Prepare the operating system image for multicast deployments](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast) (Preparar la imagen de sistema operativo para implementaciones de multidifusión).  

##  <a name="a-namebkmkdeploya-deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Implementar la secuencia de tareas  
 Implemente el sistema operativo en una recopilación de destino. Para obtener más información, vea [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  



<!--HONumber=Nov16_HO1-->


