---
title: Conexión de nube con administración conjunta
titleSuffix: Configuration Manager
description: La administración conjunta ofrece valor inmediato cuando la habilita.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d878443-90e7-46e4-9cd3-99e2a19b2ad0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed92d6249e4459f1902f639840b142977994df9e
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "56755570"
---
# <a name="cloud-connecting-with-co-management"></a>Conexión de nube con administración conjunta

![Banner de la serie Blastoff](media/blastoff-banner.png)

La administración conjunta agrega una funcionalidad nueva a la implementación de Configuration Manager existente, sin cambiar la forma de trabajar actual. Cuando habilita la administración conjunta, de inmediato empieza a recibir las ventajas de la nube. Puede aplicar ese valor a los procesos y la infraestructura de administración existentes.

En esta serie de tutoriales de inicio rápido para la administración conjunta verá cómo puede generar rápidamente nuevo valor de administración. La administración conjunta está diseñada para crear características y herramientas que puede usar de inmediato.


En el vídeo siguiente, el Vicepresidente Corporativo de Microsoft, Brad Anderson, presenta esta serie sobre la administración conjunta:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Cloud-Connecting-with-Co-Management/player]


| Valor inmediato | Introducción |
|-----------------|-----------------|
| - [Acceso condicional](#bkmk_ca)<br> - [Acciones remotas de Intune](#bkmk_remote)<br> - [Estado de cliente](#bkmk_client-health)<br> - [Azure AD híbrido](#bkmk_hybrid-aad)<br> - [Windows Autopilot](#bkmk_autopilot) | - [Rutas hacia la administración conjunta](#bkmk_paths)<br> - [Configuración de Azure AD híbrido](#bkmk_setup-hybrid-aad)<br> - [Actualización a Windows 10](#bkmk_upgrade-win10)<br> - [Migración desde MDM híbrida](#bkmk_migrate-hybrid-mdm)<br> - [Ayuda de FastTrack](#bkmk_fasttrack) | 



## <a name="immediate-value"></a>Valor inmediato

| | | |
|-|-|-|
| <a name="bkmk_ca"></a>**Acceso condicional con cumplimiento de dispositivos** | Controle el acceso a recursos corporativos según las reglas de cumplimiento de Intune. | [![Miniatura de vídeo sobre el acceso condicional](media/thumbnail-conditional-access.png)](/sccm/comanage/quickstart-conditional-access) |
| <a name="bkmk_remote"></a>**Acciones remotas de Intune** | Ejecute acciones remotas desde Intune para dispositivos administrados conjuntamente. Por ejemplo, borrar y restablecer un dispositivo y mantener la inscripción y la cuenta. | [![Miniatura de vídeo sobre las acciones remotas](media/thumbnail-remote-action.png)](/sccm/comanage/quickstart-remote-actions) |
| <a name="bkmk_client-health"></a>**Estado del cliente de Configuration Manager** | Mantenga la visibilidad del estado de cliente de Configuration Manager desde Intune en Azure Portal. | [![Miniatura de vídeo sobre el estado del cliente](media/thumbnail-client-health.png)](/sccm/comanage/quickstart-client-health) |
| <a name="bkmk_hybrid-aad"></a>**Azure Active Directory (Azure AD)** | Con Azure AD puede aprovechar la productividad mejorada para sus usuarios y la seguridad para sus recursos, tanto en la nube como en los entornos locales. | [![Miniatura de vídeo sobre Azure AD híbrido](media/thumbnail-azure-ad.png)](/sccm/comanage/quickstart-hybrid-aad) |
| <a name="bkmk_autopilot"></a>**Windows Autopilot** | Reduzca el tiempo, los recursos y la complejidad asociados con la implementación, administración y retirada o reciclaje de los dispositivos. Autopilot también crea una mejor experiencia para los usuarios finales. | [![Miniatura de vídeo sobre Windows Autopilot](media/thumbnail-autopilot.png)](/sccm/comanage/quickstart-autopilot) |



## <a name="getting-started"></a>Introducción

Si quiere habilitar la administración conjunta, empiece aquí para solucionar los problemas técnicos que pueda tener.

| | | |
|-|-|-|
| <a name="bkmk_paths"></a>**Rutas hacia la administración conjunta** | Hay dos métodos principales para configurar la administración conjunta y es importante comprender los requisitos previos de cada ruta.  Cada ruta requiere alguna combinación de Azure AD, ConfigMgr, Intune y cliente Windows. | [![Miniatura de la diapositiva sobre las rutas de administración conjunta](media/thumbnail-paths.png)](/sccm/comanage/quickstart-paths) |
| <a name="bkmk_setup-hybrid-aad"></a>**Configuración de Azure AD híbrido** | Si el entorno actualmente tiene dispositivos Windows 10 unidos al dominio, configure Azure AD híbrido antes de habilitar la administración conjunta. | [![Miniatura de vídeo sobre la configuración de Azure AD híbrido](media/thumbnail-setup-azure-ad.png)](/sccm/comanage/quickstart-setup-hybrid-aad) |
| <a name="bkmk_upgrade-win10"></a>**Actualización a Windows 10** | La administración conjunta requiere la versión 1709 o posteriores de Windows 10. | [![Miniatura de vídeo sobre la actualización de Windows 10](media/thumbnail-upgrade-win10.png)](/sccm/comanage/quickstart-upgrade-win10) |
| <a name="bkmk_migrate-hybrid-mdm"></a>**Migración desde MDM híbrida** | La MDM híbrida (Intune integrado con Configuration Manager) está en desuso. La administración conjunta requiere Intune independiente. | [![Miniatura de vídeo sobre la migración de MDM híbrida](media/thumbnail-migrate-hybrid-mdm.png)](/sccm/comanage/quickstart-migrate-hybrid-mdm) |
| <a name="bkmk_fasttrack"></a>**Ayuda de FastTrack** | La organización de FastTrack es un gran grupo de ingenieros de Microsoft que se especializan en ayudar a todos los tipos de organizaciones que implementan aplicaciones de Microsoft 365, incluida la configuración de la administración conjunta. | [![Miniatura de vídeo de FastTrack](media/thumbnail-fasttrack.png)](/sccm/comanage/quickstart-fasttrack) |

