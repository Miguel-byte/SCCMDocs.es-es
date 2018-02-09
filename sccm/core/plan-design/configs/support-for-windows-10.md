---
title: Compatibilidad con Windows 10
titleSuffix: Configuration Manager
description: Conozca las versiones de Windows 10 que se admiten como clientes o para OSD con System Center Configuration Manager.
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2dfe9b63e9e7c41a4f8457dc5622f386c7cceec2
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2018
---
# <a name="support-for-windows-10-for-system-center-configuration-manager"></a>Compatibilidad con Windows 10 para System Center Configuration Manager  

*Se aplica a: System Center Configuration Manager (Rama actual)*


 En este tema se detallan las versiones de Windows 10 que puede usar con las diferentes versiones de la Rama actual de System Center Configuration Manager. Esta compatibilidad incluye:
 -  Windows 10 como cliente de Configuration Manager
 -  Windows Assessment and Deployment Kit (ADK) para Windows 10

## <a name="windows-10-as-a-client"></a>Windows 10 como cliente
Configuration Manager intenta proporcionar compatibilidad como cliente para cada nueva versión de Windows 10 tan pronto como es posible después de que se encuentra disponible. Como los productos tienen programaciones independientes de lanzamiento y desarrollo, la compatibilidad que Configuration Manager proporciona depende de cuándo se encuentra disponible cada una.

Por ejemplo, una versión de Configuration Manager se quitará de la matriz después de que finalice la [compatibilidad con esa versión](/sccm/core/servers/manage/current-branch-versions-supported). De forma similar, la compatibilidad con versiones de Windows 10 como Enterprise 2015 LTSB o 1511 se quitará de la matriz cuando se eliminen del soporte técnico. Para obtener más información, consulte [Sistemas operativos en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).


-   La siguiente información complementa a [Sistemas operativos compatibles con clientes y dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
-   Si usa la Rama de mantenimiento a largo plazo de Configuration Manager, vea [Configuraciones admitidas de la Rama de mantenimiento a largo plazo de System Center Configuration Manager](/sccm/core/understand/supported-configurations-for-ltsb).

|Versión de Windows 10                    |  Configuration Manager 1702          |    Configuration Manager 1706 |Configuration Manager 1710          |  
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB                   |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
|Enterprise 2016 LTSB                   |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
|1607   <br />(También conocida como la Actualización de aniversario)<br />(*Véanse las ediciones*)   |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png)            |![Compatible.](media/green_check.png) |
|1703   <br />(También conocida como Creators Update)<br />(*Véanse las ediciones*)      |![Compatible con versiones anteriores](media/blue_compat.png) |![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
|1709   <br />(También conocida como Fall Creators Update)<br />(*Véanse las ediciones*) |![No compatible](media/Red_X.png)   |![Compatible con versiones anteriores](media/blue_compat.png) | ![Compatible.](media/green_check.png) |



**Ediciones:** Enterprise, Pro, Education, Pro Education   

|Clave|
|--|
|![Compatible](media/green_check.png) = **Compatible**  |
|![No compatible](media/blue_compat.png)  = **Compatible con versiones anteriores**: las características de administración de clientes existentes (inventario de hardware y de software, actualizaciones de software, etc.) deben funcionar con la nueva versión de Windows 10. Informaremos de cualquier problema conocido o advertencia. <br><br>Este enfoque le proporciona la capacidad de implementar y administrar nuevas compilaciones de Windows en un día con la compatibilidad de aplicaciones sin requerir una nueva versión de actualización de Configuration Manager. |
|![Compatible](media/Red_X.png) = **No compatible**|


## <a name="windows-10-adk"></a>Windows 10 ADK
Cuando se implementan sistemas operativos con Configuration Manager, [Windows ADK es una dependencia externa](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) que es necesaria.

En la tabla siguiente se enumeran las versiones de Windows 10 ADK que puede usar con diferentes versiones de Configuration Manager.

|Versión del ADK de Windows 10  |Configuration Manager 1702   |Configuration Manager 1706 |Configuration Manager 1710 |
|--------------------|-----|-----|-----|
|1607  |![Compatible con versiones anteriores](media/blue_compat.png) |![No compatible](media/Red_X.png)| ![No compatible](media/Red_X.png) |
|1703  |![Compatible.](media/green_check.png)            |![Compatible.](media/green_check.png) | ![Compatible con versiones anteriores](media/blue_compat.png)|
|1709  |![No compatible](media/Red_X.png)              |![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png)|

|Clave|
|--|
|![Compatible](media/green_check.png) = **Compatible**: Windows recomienda el uso de la versión de Windows ADK que coincida con la de Windows que va a implementar. Por ejemplo, use la versión 1703 de Windows ADK para Windows 10 al implementar Windows 10 versión 1703. Para obtener más información sobre la compatibilidad del componente Windows ADK, consulte [DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) (Plataformas compatibles con DISM) y [USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1) (Requisitos de USMT). |
|![Compatible con versiones anteriores](media/blue_compat.png)  = **Compatible con versiones anteriores**: esta combinación no está probada pero debería funcionar. Informaremos de cualquier problema conocido o advertencia. |
|![Compatible](media/Red_X.png) = **No compatible**|
