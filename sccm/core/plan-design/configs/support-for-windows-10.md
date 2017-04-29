---
title: Compatibilidad para Windows 10 | Microsoft Docs
description: "Obtenga información sobre qué versiones de Windows 10 son compatibles para ejecutar el cliente de System Center Configuration Manager."
ms.custom: na
ms.date: 3/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: db258a09ce21627ffba37eb1f3d521c1ea0341ed
ms.openlocfilehash: 7df4bde6970b63262eee9e785d983addbeac0908
ms.lasthandoff: 04/13/2017

---
# <a name="support-for-windows-10-as-a-client-of-system-center-configuration-manager"></a>Compatibilidad para Windows 10 como un cliente de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


 En este tema se identifican las versiones de Windows 10 que puede usar como un cliente con las diferentes versiones de la Rama actual de System Center Configuration Manager.

- Esto complementa a [Sistemas operativos compatibles con clientes y dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
- Si usa la Rama de mantenimiento a largo plazo de Configuration Manager, vea [Configuraciones admitidas de la Rama de mantenimiento a largo plazo de System Center Configuration Manager](/sccm/core/understand/supported-configurations-for-ltsb).

Configuration Manager intenta proporcionar compatibilidad para cada nueva versión de Windows 10 tan pronto como sea posible después de que se presente esa versión de Windows. Como los productos tienen programaciones independientes de lanzamiento y desarrollo, la compatibilidad que Configuration Manager proporciona depende de cuándo se presentan las versiones y las ramas de cada producto.

Por ejemplo, una versión de Configuration Manager se quitará de la matriz después de que finalice la [compatibilidad con esa versión](/sccm/core/servers/manage/current-branch-versions-supported). De forma similar, la compatibilidad con versiones de Windows 10 como Enterprise 2015 LTSB o 1607 (CBB) se quitará de la matriz cuando se eliminen de la lista de configuraciones compatibles de Configuration Manager. Vea [Sistemas operativos en desuso](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems) para más información.



|Versiones de Windows 10                    |Configuration Manager 1606          |Configuration Manager 1610          |    Configuration Manager 1702 |
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB                   |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) |
|1507 <br />(*Véanse las ediciones*)            |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) |
|1511 (CB), (CBB)<br />(*Véanse las ediciones*) |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) |
|Enterprise 2016 LTSB                   |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) |
|1607 (CB)    <br />Actualización de aniversario<br />(*Véanse las ediciones*)      |![Compatible con versiones anteriores](media/blue_compat.png) |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) |
|1607 (CBB)    <br />Actualización de aniversario<br />(*Véanse las ediciones*)      |![No compatible](media/Red_X.png)   |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) |
|1703 (CB)    <br />Creators Update<br />(*Véanse las ediciones*)      |![No compatible](media/Red_X.png)   |![No compatible](media/Red_X.png) |![Compatible con versiones anteriores](media/blue_compat.png) |



**Ediciones:** Enterprise, Pro, Education, Pro Education   

|Clave|
|--|
|![Compatible](media/green_check.png) = **Compatible**  |
|![No compatible](media/blue_compat.png)  = **Compatible con versiones anteriores**: Esto significa que las características de administración de clientes existentes (inventario de hardware y de software, actualizaciones de software, etc.) deben funcionar con la nueva compilación de la Rama actual de Windows 10. Se documentará cualquier advertencia o problema conocido. <br><br>Este enfoque le proporciona la capacidad de implementar y administrar nuevas compilaciones de CB de Windows 10 en un día con la compatibilidad de aplicaciones sin requerir una nueva versión de actualización de Configuration Manager. |
|![Compatible](media/Red_X.png) = **No compatible**|

