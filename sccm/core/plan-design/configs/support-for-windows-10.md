---
title: Compatibilidad con Windows 10
titleSuffix: Configuration Manager
description: Obtenga información sobre las versiones de Windows 10 que se admiten como clientes o para OSD con System Center Configuration Manager.
ms.date: 04/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 947392d4c11b419e0e373fbe83db42522d3c5f25
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="support-for-windows-10-in-system-center-configuration-manager"></a>Compatibilidad con Windows 10 en System Center Configuration Manager  

*Se aplica a: System Center Configuration Manager (Rama actual)*


Obtenga información sobre las versiones de Windows 10 que admite Configuration Manager, incluidas:
 -  [Windows 10 como cliente de Configuration Manager](#windows-10-as-a-client)
 -  [Windows Assessment and Deployment Kit (ADK) para Windows 10](#windows-10-adk)



## <a name="windows-10-as-a-client"></a>Windows 10 como cliente
Configuration Manager intenta proporcionar compatibilidad como cliente para cada versión nueva de Windows 10 tan pronto como es posible después de que se encuentre disponible. Como los productos tienen programaciones independientes de lanzamiento y desarrollo, la compatibilidad que Configuration Manager proporciona depende de cuándo se encuentra disponible cada una.

Por ejemplo, una versión de Configuration Manager se quitará de la matriz después de que finalice la [compatibilidad con esa versión](/sccm/core/servers/manage/current-branch-versions-supported). De forma similar, la compatibilidad con versiones de Windows 10 como Enterprise 2015 LTSB o 1511 se quitará de la matriz cuando se eliminen del soporte técnico. Para obtener más información, consulte [Sistemas operativos en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).

-   Esta información complementa a [Sistemas operativos compatibles con dispositivos y clientes](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).  

-   Si usa la rama de mantenimiento a largo plazo de Configuration Manager, vea [Configuraciones admitidas para la rama de mantenimiento a largo plazo](/sccm/core/understand/supported-configurations-for-ltsb).  

<br/>
En la tabla siguiente se enumeran las versiones de Windows 10 que puede usar como cliente con diferentes versiones de Configuration Manager.

| Versión de Windows 10 | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802 |
|---------------------|-----|-----|-----|
| Enterprise 2015 LTSB            <!--10/14/2025-->   | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
| Enterprise 2016 LTSB            <!--10/13/2026-->   | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
| 1607   <br />(*Véanse las ediciones*)   <!--04+6/10/2018-->   | ![Compatible](media/green_check.png) <sup>1</sup> | ![Compatible](media/green_check.png) <sup>1</sup> | ![Compatible](media/green_check.png) <sup>1</sup> |
| 1703   <br />(*Véanse las ediciones*)   <!--10+6/09/2018-->   | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
| 1709   <br />(*Véanse las ediciones*)   <!--04+6/09/2019-->   | ![Compatible con versiones anteriores](media/blue_compat.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
| 1803   <br />(*Véanse las ediciones*)   <!--11/12/2019-->   | ![No compatible](media/Red_X.png) | ![No compatible](media/Red_X.png) | ![Compatible.](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

**Ediciones**: Enterprise, Pro, Education, Pro Education   

<sup>1</sup> Para obtener más información, vea [Hoja de datos del ciclo de vida de Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) y la sección "Extensión de mantenimiento para las ediciones Enterprise y Education".

| Clave |
|--|
| ![Compatible](media/green_check.png) = **Compatible**  |
| ![Compatible con versiones anteriores](media/blue_compat.png)  = **Compatible con versiones anteriores** <br/> Las características de administración de cliente existentes deben funcionar con la nueva versión Windows 10. Por ejemplo, las actualizaciones de inventario de software, inventario de hardware y de software. Informaremos de cualquier problema conocido o advertencia. <br><br>Este enfoque proporciona la capacidad de implementar y administrar nuevas versiones de Windows directamente con la compatibilidad de aplicaciones, sin requerir una versión de actualización nueva de Configuration Manager. |
| ![No compatible](media/Red_X.png) = **Not supported** |

 > [!NOTE]  
 > A partir de la versión 1802, Configuration Manager es compatible con el cliente en dispositivos ARM64 de Windows 10. Las características de administración de cliente existentes deben funcionar con estos nuevos dispositivos. Por ejemplo, el inventario de hardware y software, las actualizaciones de software y la administración de aplicaciones. La implementación de SO no se admite actualmente. <!-- 1353704 --> 



## <a name="windows-10-adk"></a>Windows 10 ADK
Cuando se implementan sistemas operativos con Configuration Manager, [Windows ADK es una dependencia externa](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) que es necesaria.

En la tabla siguiente se enumeran las versiones de Windows 10 ADK que puede usar con diferentes versiones de Configuration Manager.

| Versión del ADK de Windows 10  | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802   |
|--------------------|-----|-----|-----|
| 1703  | ![Compatible.](media/green_check.png) | ![Compatible con versiones anteriores](media/blue_compat.png) | ![Compatible con versiones anteriores](media/blue_compat.png) |
| 1709  | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
| 1803  | ![No compatible](media/Red_X.png)   | ![No compatible](media/Red_X.png) | ![Compatible.](media/green_check.png) |

|Clave|
|--|
| ![Compatible](media/green_check.png) = **Compatible** <br/> Windows recomienda el uso de la versión de Windows ADK que coincida con la de Windows que va a implementar. Por ejemplo, use la versión 1703 de Windows ADK para Windows 10 al implementar Windows 10 versión 1703. Para obtener más información sobre la compatibilidad del componente Windows ADK, consulte [DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) (Plataformas compatibles con DISM) y [USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1) (Requisitos de USMT). |
| ![Compatible con versiones anteriores](media/blue_compat.png)  = **Compatible con versiones anteriores** <br/> Esta combinación no se ha probado pero debería funcionar. Informaremos de cualquier problema conocido o advertencia. |
| ![No compatible](media/Red_X.png) = **Not supported** |

 > [!Note]  
 > Configuration Manager solo admite componentes x86 y amd64 de Windows 10 ADK. Actualmente no admite componentes ARM o ARM64. 