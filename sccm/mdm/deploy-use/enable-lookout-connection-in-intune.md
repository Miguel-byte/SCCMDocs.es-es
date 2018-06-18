---
title: Habilitar Lookout MTD en Intune
titleSuffix: Configuration Manager
description: Habilite Lookout Mobile Threat Defense (MTD) en el portal de Microsoft Intune.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0de1859d97eed804eced58028d6459ab682f9b3f
ms.sourcegitcommit: 9cff0702c2cc0f214173b47ec241f7e5a40f84e6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34745442"
---
# <a name="enable-lookout-mtd-connection-in-the-intune-admin-console"></a>Habilitar la conexión de Lookout MTP en la consola de administración de Intune

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se muestra cómo habilitar la conexión de Lookout Mobile Threat Defense (MTD) en Microsoft Intune. Ya debe haber configurado el conector de Intune en la consola de Lookout antes de realizar este paso. Si todavía no lo ha hecho, siga los pasos que se describen en [Configurar su suscripción con Lookout Mobile Threat Defense](set-up-your-subscription-with-lookout.md).



## <a name="enable-the-lookout-mtd-connector"></a>Habilitar el conector de Lookout MTD

1. Vaya a [Azure Portal](https://portal.azure.com) e inicie sesión con sus credenciales de Intune. Una vez que haya iniciado sesión correctamente, verá el **panel de Azure**.  

2. En el menú izquierdo del **panel de Azure**, seleccione **Todos los servicios** y, a continuación, escriba **Intune** en el filtro de cuadro de texto.  

3. Seleccione **Intune**; se abrirá el **panel de Intune**.  

4. En el **panel de Intune**, seleccione **Conformidad de dispositivos**. Después, en la sección **Configurar**, seleccione **Mobile Threat Defense**.  

5. En el panel **Mobile Threat Defense**, seleccione **Agregar**.  

6. Seleccione **Lookout** en la lista desplegable **Mobile Threat Defense connector to setup** (Conector de Mobile Threat Defense que se va a configurar).  

7. Habilite las opciones de alternancia de acuerdo con los requisitos de su organización.  



## <a name="mtd-toggle-options"></a>Opciones de alternancia de MTD

Las opciones de alternancia de MTD que habilite dependerán de los requisitos de su organización. A continuación tiene más detalles:

- **Conectar dispositivos Android 4.1+ a Lookout for Work MTD** (Conectar dispositivos Android 4.1+ a Lookout for Work MTD): cuando se habilita esta opción, los dispositivos Android 4.1+ pueden informar a Intune de los riesgos para la seguridad.  
    - **Mark as noncompliant if no data is received** (Marcar como no conforme si no se reciben datos): si Intune no recibe datos acerca de un dispositivo en esta plataforma de Lookout, se considera que el dispositivo no es compatible.  

- **Connect iOS 8.0+ devices to Lookout for Work MTD** (Conectar dispositivos iOS 8.0+ a Lookout for Work MTD): cuando se habilita esta opción, los dispositivos iOS 8.0+ pueden informar a Intune de los riesgos para la seguridad.
    - **Mark as noncompliant if no data is received** (Marcar como no conforme si no se reciben datos): si Intune no recibe datos acerca de un dispositivo en esta plataforma de Lookout, se considera que el dispositivo no es compatible.  

> [!TIP]  
> En el panel de Mobile Threat Defense, puede ver el **estado de la conexión** y la hora de la **última sincronización** entre Intune y Lookout.



## <a name="next-steps"></a>Pasos siguientes
Esto completa la configuración de la integración de Lookout e Intune. Los siguientes pasos para implementar esta solución implican la implementación de las [aplicaciones Lookout for Work](configure-and-deploy-lookout-for-work-apps.md) y la configuración de la directiva de [cumplimiento](enable-device-threat-protection-rule-compliance-policy.md).

>[!IMPORTANT]
> *Debe* configurar la aplicación Lookout for Work antes de crear las reglas de la directiva de cumplimiento y configurar el acceso condicional. Esta acción garantiza que la aplicación está lista y disponible para que los usuarios finales la instalen antes de que puedan obtener acceso a su correo electrónico o a otros recursos de la empresa.

[Configurar la aplicación Lookout for Work](configure-and-deploy-lookout-for-work-apps.md)
