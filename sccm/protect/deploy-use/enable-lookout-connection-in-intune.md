---
title: Habilitar Lookout MTP en Intune | System Center Configuration Manager
description: "Habilite Lookout Mobile Threat Protection en la consola de administración de Intune."
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9536efdd-0f29-47a8-8283-0edea7714319
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c13c6268fa76ade7feb0981f9c4a6e325e393aca
ms.openlocfilehash: a06f0b3a0080a06a0ccbfa7f3802c575aee2c9b7


---
# <a name="enable-lookout-mtp-connection-in-the-intune-admin-console"></a>Habilitar la conexión de Lookout MTP en la consola de administración de Intune

*Se aplica a: System Center Configuration Manager (Rama actual)*

Este tema le muestra cómo habilitar la conexión de Lookout MTP en Intune. Ya debe haber configurado el conector de Intune en la consola de Lookout antes de realizar este paso.  Si todavía no lo ha hecho, realice los pasos que se describen en [Set up your subscription with Lookout mobile threat protection (Configurar su suscripción con Lookout Mobile Threat Protection)](set-up-your-subscription-with-lookout.md).

Para habilitar la conexión de Lookout MTP en Intune, en la página **Administración** en la [consola de administrador de Microsoft Intune](https://manage.microsoft.com), pulse **Third Party Service Integration (Integración de servicio de terceros)**. Pulse **Estado de Lookout** y habilite la **Sincronización con MTP** con el botón de alternancia.

![captura de pantalla de la página de sincronización de Lookout con el botón de alternancia Habilitar resaltado](../media/lookout-intune-synchronization.png)

Esto completa la configuración de la integración de Lookout e Intune en la consola de administrador de Intune.  Los siguientes pasos para implementar esta solución implican la implementación de las [aplicaciones Lookout for Work](configure-and-deploy-lookout-for-work-apps.md) y la configuración de la directiva de [cumplimiento](enable-device-threat-protection-rule-compliance-policy.md).

>[!IMPORTANT]
> **Debe** configurar la aplicación Lookout for Work antes de crear las reglas de la directiva de cumplimiento y configurar el acceso condicional. Esto garantiza que la aplicación está lista y disponible para que los usuarios finales la instalen antes de que puedan obtener acceso a su correo electrónico o a otros recursos de la empresa.

## <a name="next-steps"></a>Pasos siguientes
[Configurar e implementar aplicaciones Lookout for Work](configure-and-deploy-lookout-for-work-apps.md)



<!--HONumber=Dec16_HO3-->


