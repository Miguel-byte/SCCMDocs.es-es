---
title: Compatibilidad para Windows 10 | Microsoft Docs
description: Conozca las versiones de Windows 10 que se admiten como clientes o para OSD con System Center Configuration Manager.
ms.custom: na
ms.date: 05/09/2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 065b1fcb25d7c7845b6f26e757b36e7fb97ce013
ms.openlocfilehash: 2ec25e9b093d9451d8880ba36f4d022ec4bad001
ms.contentlocale: es-es
ms.lasthandoff: 05/10/2017

---
# <a name="support-for-windows-10-for-system-center-configuration-manager"></a>Compatibilidad con Windows 10 para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


 En este tema se detallan las versiones de Windows 10 que puede usar con las diferentes versiones de la rama actual de System Center Configuration Manager. Esto incluye:
 -  Windows 10 como cliente de Configuration Manager.
 -  Windows Assessment y Deployment Kit (ADK) para Windows 10.

## <a name="windows-10-as-a-client"></a>Windows 10 como cliente
Configuration Manager intenta proporcionar compatibilidad como cliente para cada nueva versión de Windows 10 tan pronto como es posible después de que se presenta esa versión de Windows. Como los productos tienen programaciones independientes de lanzamiento y desarrollo, la compatibilidad que Configuration Manager proporciona depende de cuándo se presentan las versiones y las ramas de cada producto.

Por ejemplo, una versión de Configuration Manager se quitará de la matriz después de que finalice la [compatibilidad con esa versión](/sccm/core/servers/manage/current-branch-versions-supported). De forma similar, la compatibilidad con versiones de Windows 10 como Enterprise 2015 LTSB o 1607 (CBB) se quitará de la matriz cuando se eliminen de la lista de configuraciones compatibles de Configuration Manager. Vea [Sistemas operativos en desuso](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems) para más información.

-   La siguiente información complementa a [Sistemas operativos compatibles con clientes y dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
-   Si usa la Rama de mantenimiento a largo plazo de Configuration Manager, vea [Configuraciones admitidas de la Rama de mantenimiento a largo plazo de System Center Configuration Manager](/sccm/core/understand/supported-configurations-for-ltsb).

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


## <a name="windows-10-adk"></a>Windows 10 ADK
Cuando se implementan sistemas operativos con Configuration Manager, [Windows ADK es una dependencia externa](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) que es necesaria.

En la tabla siguiente se enumeran las versiones de Windows 10 ADK que puede usar con diferentes versiones de Configuration Manager.

|Versiones de Windows 10 |Configuration Manager 1606 |Configuration Manager 1610  |Configuration Manager 1702 |
|--------------------|-----|-----|-----|
|1507  |![No compatible](media/Red_X.png)         |![No compatible](media/Red_X.png)  |![No compatible](media/Red_X.png)|
|1511  |![Compatible con versiones anteriores](media/blue_compat.png)|![No compatible](media/Red_X.png)  |![No compatible](media/Red_X.png)|
|1607  |![Compatible.](media/green_check.png)       |![Compatible.](media/green_check.png)|![Compatible con versiones anteriores](media/blue_compat.png) |
|1703  |![No compatible](media/Red_X.png)         |![No compatible](media/Red_X.png)  |![Compatible.](media/green_check.png) |  

|Clave|
|--|
|![Compatible](media/green_check.png) = **Compatible**: Windows recomienda el uso de la versión de Windows ADK que coincida con la de Windows que va a implementar. Por ejemplo, use la versión 1703 de Windows ADK para Windows 10 al implementar Windows 10 versión 1703.  |
|![Compatible con versiones anteriores](media/blue_compat.png)  = **Compatible con versiones anteriores**: esta combinación no está probada pero debería funcionar. Se documentará cualquier advertencia o problema conocido. |
|![Compatible](media/Red_X.png) = **No compatible**|

