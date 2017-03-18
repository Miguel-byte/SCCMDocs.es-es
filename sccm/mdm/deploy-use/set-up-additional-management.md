---
title: "Configuración de administración adicional mediante System Center Configuration Manager | Microsoft Docs"
description: "Configure la administración adicional mediante System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4877d674-6bbc-4e16-810c-daad70c74daa
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 947d2a85f2ac68c7ccaf9a1237fd60e89e7d1d10
ms.lasthandoff: 03/06/2017

---
# <a name="set-up-additional-management-with-system-center-configuration-manager"></a>Configuración de administración adicional con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

(Opcional) Puede configurar administración adicional antes de que se inscriban los dispositivos. Estas soluciones de administración se pueden crear e implementar una vez que los dispositivos están inscritos, aunque muchas organizaciones prefieren implementarlas según se incorporan los dispositivos a la administración.

Los **elementos de configuración** le permiten administrar la configuración (por ejemplo, exigir un PIN o requerir cifrado en dispositivos inscritos) según la plataforma del dispositivo:
- [Dispositivos Windows 10 y Windows 8.1](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Dispositivos Windows Phone](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
- [Dispositivos iOS y Mac](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
- [Dispositivos Android y Samsung KNOX Standard](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)

Se pueden implementar **aplicaciones** en dispositivos administrados:
- [Aplicaciones de iOS](creating-ios-applications.md)
- [Aplicaciones de Mac](../../apps/get-started/creating-mac-computer-applications.md)
- [Aplicaciones de PC Windows](../../apps/get-started/creating-windows-applications.md)
- [Aplicaciones de Windows Phone](creating-windows-phone-applications.md)
- [Aplicaciones de Android](creating-android-applications.md)

El **acceso condicional** le permite administrar el acceso a los recursos de empresa, entre los que se incluyen:  
- [Acceso a correo electrónico](manage-email-access.md)
- [Acceso a SharePoint](manage-sharepoint-online-access.md)
- [Acceso a Skype Empresarial](manage-skype-for-business-online-access.md)
- [Dynamic CRM Online](manage-dynamics-crm-online-access.md)

**Multi-factor Authentication (MFA)** le permite solicitar más de un método de comprobación, lo que agrega un segundo nivel crítico de seguridad a las transacciones e inicios de sesión de usuario.
Anteriormente, tenía que ir a la consola de Intune o a la consola de Configuration Manager para configurar inscripciones de MFA para Intune. Ahora puede iniciar sesión en [Microsoft Azure Portal](https://manage.windowsazure.com) con credenciales de Intune y configurar las opciones de MFA a través de Azure AD. Para más información, vea [Autenticación multifactor para inscripciones de dispositivos de Intune](https://aka.ms/mfa_ad).

> [!div class="button"]
[< Paso anterior](enable-platform-enrollment.md)  [Paso siguiente >](verify-mdm-configuration.md)

