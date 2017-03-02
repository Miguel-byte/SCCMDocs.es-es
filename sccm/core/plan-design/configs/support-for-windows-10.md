---
title: Compatibilidad para Windows 10 | Microsoft Docs
description: "Obtenga información sobre qué versiones de Windows 10 son compatibles para ejecutar el cliente de System Center Configuration Manager."
ms.custom: na
ms.date: 2/10/2017
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
ms.sourcegitcommit: 3702993d6cf9644d5aebaadd168749668fbcb62c
ms.openlocfilehash: 4b90384621dd20475ab9ea33ea062c24f5ecf5fa
ms.lasthandoff: 02/22/2017

---
# <a name="support-for-windows-10-as-a-client-of-system-center-configuration-manager"></a>Compatibilidad para Windows 10 como un cliente de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


 En este tema se identifican las versiones de Windows 10 que puede usar como un cliente con las diferentes versiones de la Rama actual de System Center Configuration Manager.

- Esto complementa a [Sistemas operativos compatibles con clientes y dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
- Si usa la Rama de mantenimiento a largo plazo de Configuration Manager, vea [Configuraciones admitidas de la Rama de mantenimiento a largo plazo de System Center Configuration Manager](/sccm/core/understand/supported-configurations-for-ltsb).

Configuration Manager intenta proporcionar compatibilidad para cada nueva versión de Windows 10 tan pronto como sea posible después de que se presente esa versión de Windows. Como los productos tienen programaciones independientes de lanzamiento y desarrollo, la compatibilidad que Configuration Manager proporciona depende de cuándo se presentan las versiones y las ramas de cada producto.  



|Versiones de Windows 10 |Configuration Manager 1602|Configuration Manager 1606|Configuration Manager 1610|
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) |
|1507 <br />Enterprise, Pro | ![Compatible.](media/green_check.png)| ![Compatible.](media/green_check.png)|![Compatible.](media/green_check.png) |
|1511 <br />Enterprise, Pro <br />(CB), (CBB) |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) |![Compatible.](media/green_check.png) |
|Enterprise 2016 LTSB    |![No compatible](media/Red_X.png) |![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png)|
|1607 <br />Enterprise, Pro<br /> (CB)    |![No compatible](media/Red_X.png) |![Compatible con versiones anteriores](media/blue_compat.png) |![Compatible.](media/green_check.png) |
|1607 <br />Enterprise, Pro <br />(CBB)    |![No compatible](media/Red_X.png) |![Compatible con versiones anteriores](media/Red_X.png) |![Compatible.](media/green_check.png) |


|Clave|
|--|
|![Compatible](media/green_check.png) = **Compatible**  |
|![No compatible](media/blue_compat.png)  = **Compatible con versiones anteriores**: Esto significa que las características de administración de clientes existentes (inventario de hardware y de software, actualizaciones de software, etc.) deben funcionar con la nueva compilación de la Rama actual de Windows 10. Se documentará cualquier advertencia o problema conocido. <br><br>Este enfoque le proporciona la capacidad de implementar y administrar nuevas compilaciones de CB de Windows 10 en un día con la compatibilidad de aplicaciones sin requerir una nueva versión de actualización de Configuration Manager. |
|![Compatible](media/Red_X.png) = **No compatible**|

