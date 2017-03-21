---
title: "Habilitación de Lookout MTP en Intune | Microsoft Docs"
description: "Habilite Lookout Mobile Threat Protection en la consola de administración de Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 65d3dff359987e1d3175b06aa7a03827d48bc97d
ms.lasthandoff: 03/06/2017


---
# <a name="enable-lookout-mtp-connection-in-the-intune-admin-console"></a>Habilitar la conexión de Lookout MTP en la consola de administración de Intune

*Se aplica a: System Center Configuration Manager (Rama actual)*

Este tema le muestra cómo habilitar la conexión de Lookout MTP en Intune. Ya debe haber configurado el conector de Intune en la consola de Lookout antes de realizar este paso.  Si todavía no lo ha hecho, realice los pasos que se describen en [Set up your subscription with Lookout mobile threat protection (Configurar su suscripción con Lookout Mobile Threat Protection)](set-up-your-subscription-with-lookout.md).

Para habilitar la conexión de Lookout MTP en Intune, en la página **Administración** en la [consola de administrador de Microsoft Intune](https://manage.microsoft.com), pulse **Third Party Service Integration (Integración de servicio de terceros)**. Pulse **Estado de Lookout** y habilite la **Sincronización con MTP** con el botón de alternancia.

![captura de pantalla de la página de sincronización de Lookout con el botón de alternancia Habilitar resaltado](media/lookout-intune-synchronization.png)

Esto completa la configuración de la integración de Lookout e Intune en la consola de administrador de Intune.  Los siguientes pasos para implementar esta solución implican la implementación de las [aplicaciones Lookout for Work](configure-and-deploy-lookout-for-work-apps.md) y la configuración de la directiva de [cumplimiento](enable-device-threat-protection-rule-compliance-policy.md).

>[!IMPORTANT]
> **Debe** configurar la aplicación Lookout for Work antes de crear las reglas de la directiva de cumplimiento y configurar el acceso condicional. Esto garantiza que la aplicación está lista y disponible para que los usuarios finales la instalen antes de que puedan obtener acceso a su correo electrónico o a otros recursos de la empresa.

## <a name="next-steps"></a>Pasos siguientes
[Configurar e implementar aplicaciones Lookout for Work](configure-and-deploy-lookout-for-work-apps.md)
