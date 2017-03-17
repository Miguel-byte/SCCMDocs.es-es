---
title: Acceso condicional | Microsoft Docs
description: "Aprenda a usar el acceso condicional en System Center Configuration Manager para ayudar a proteger el correo electrónico y otros servicios."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
caps.latest.revision: 26
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: ea9184cd4fdc87513ed489f0f568efa6d64c1caa
ms.lasthandoff: 03/06/2017


---

# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>Administrar el acceso a servicios en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


## <a name="conditional-access-in-system-center-configuration-manager"></a>Acceso condicional en System Center Configuration Manager
Use el **acceso condicional**para ayudar a proteger el correo electrónico y otros servicios en los dispositivos que están inscritos en Microsoft Intune, según las condiciones que especifique.  

 Para obtener información sobre el **acceso condicional en los equipos que se administran con System Center Configuration Manager** y la evaluación de la compatibilidad, consulte [Manage access to O365 services for PCs managed by System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md) (Administración del acceso a servicios de O365 para equipos administrados por System Center Configuration Manager).  


 A continuación se muestra un ejemplo de flujo típico de acceso condicional:  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 Usar acceso condicional para administrar el acceso a los servicios siguientes:  

-   Microsoft Exchange local  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated  

-   SharePoint Online  

-   Skype Empresarial Online

-   Dynamics CRM Online

 Para implementar el acceso condicional, se configuran dos tipos de directivas en Configuration Manager:  

-   **Las directivas de cumplimiento** son directivas opcionales que se pueden implementar en las recopilaciones de usuarios y evaluar opciones como:  

    -   Código de acceso  

    -   Cifrado  

    -   Si el dispositivo está desbloqueado o modificado  

    -   Si el correo electrónico en el dispositivo está administrado por una directiva de Configuration Manager o Intune  

     **Si no hay ninguna directiva de cumplimiento implementada en un dispositivo, las directivas de acceso condicional aplicables tratarán el dispositivo como compatible**.  

-   Las**directivas de acceso condicional** se configuran para un servicio particular y definen reglas, como qué grupos de usuarios de seguridad de Azure Active Directory o recopilaciones de usuarios de Configuration Manager serán objetos de su acción o estarán exentos.  

     Puede configurar una directiva de acceso condicional para Exchange local desde la consola de Configuration Manager. Sin embargo, cuando se configura una directiva de Exchange Online o SharePoint Online, se abrirá la consola del administrador de Intune donde se configura la directiva.  

     A diferencia de otras directivas de Intune o Configuration Manager, no se implementan directivas de acceso condicional. En su lugar, al configurar estas una vez, se aplicarán a todos los usuarios objetivo.  

 Cuando los dispositivos no cumplen las condiciones que configure, se indica al usuario el proceso que debe seguir para registrar el dispositivo en cuestión y corregir el problema que impide que cumpla los requisitos.  

**Antes** de empezar a utilizar el acceso condicional, asegúrese de que tiene los **requisitos** adecuados vigentes:  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Requisitos para Exchange Online (mediante el entorno de varios inquilinos compartido)
El acceso condicional a Exchange Online admite dispositivos que ejecutan:
-   Windows 8.1 y versiones posteriores (cuando están inscritos en Intune)
-   Windows 7.0 o Windows 8.1 (si están unidos a un dominio)
-   Windows Phone 8.1 y versiones posteriores
-   iOS 7.1 y versiones posteriores
-   Android 4.0 y versiones posteriores, Samsung KNOX Standard 4.0 y versiones posteriores

 **Además**:
-   Los dispositivos deben estar combinados en el área de trabajo, que registra el dispositivo con el servicio de registro del dispositivo de Azure Active Directory (AAD DRS).<br />     
- Los equipos unidos a un dominio se deben registrar automáticamente con Azure Active Directory a través de una directiva de grupo o MSI.

  En la sección **Acceso condicional para equipos** de este tema se describen todos los requisitos para habilitar el acceso condicional para un equipo.<br />     
  AAD DRS se activará automáticamente para los clientes de Intune y Office 365. Los clientes que ya hayan implementado el servicio de registro de dispositivos de ADFS no podrán ver los dispositivos registrados en la instancia local de Active Directory.
-   Debe utilizar una suscripción de Office 365 que incluya Exchange Online (por ejemplo, E3) y los usuarios deben tener licencia para Exchange Online.
-   El **conector de Exchange Server** es opcional, conecta Configuration Manager a Microsoft Exchange Online y ayuda a supervisar la información del dispositivo a través de la consola de Configuration Manager (consulte [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) [Administración de dispositivos móviles mediante System Center Configuration Manager y Exchange]).
No necesita usar el conector para utilizar directivas de cumplimiento ni de acceso condicional, pero sí para ejecutar informes que ayuden a evaluar el impacto del acceso condicional.

## <a name="requirements-for-exchange-online-dedicated"></a>Requisitos para Exchange Online dedicado
El acceso condicional a Exchange Online Dedicated admite dispositivos que ejecutan:
-   Windows 8 y versiones posteriores (cuando están inscritos en Intune)
-   Windows 7.0 o Windows 8.1 (si están unidos a un dominio)

  Acceso condicional a equipos unidos a un dominio solo con inquilinos en el nuevo entorno dedicado de Exchange Online.
-   Windows Phone 8 y versiones posteriores
-   Cualquier dispositivo iOS que utilice un cliente de correo electrónico de Exchange ActiveSync (EAS)
-   Android 4 y versiones más recientes.
-   Para los inquilinos en el **entorno heredado de Exchange Online dedicado**:    

  Debe usar el **conector de Exchange Server** que conecta Configuration Manager con Microsoft Exchange local. Esto permite administrar dispositivos móviles y habilitar el acceso condicional (consulte [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) [Administración de dispositivos móviles mediante System Center Configuration Manager y Exchange]).
-   Para los inquilinos en el **nuevo entorno de Exchange Online dedicado***:     
  El **conector de Exchange Server opcional** conecta Configuration Manager a Microsoft Exchange Online y ayuda a administrar la información del dispositivo (consulte [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) [Administración de dispositivos móviles mediante System Center Configuration Manager y Exchange]). No necesita usar el conector para utilizar directivas de cumplimiento ni de acceso condicional, pero sí para ejecutar informes que ayuden a evaluar el impacto del acceso condicional.  

## <a name="requirements-for-exchange-on-premises"></a>Requisitos para Exchange local
El acceso condicional a Exchange local admite lo siguiente:
-   Windows 8 y versiones posteriores (cuando están inscritos en Intune)
-   Windows Phone 8 y versiones posteriores
-   Aplicación de correo electrónico nativo de iOS
-   Aplicación de correo electrónico nativo de Android 4 o posterior
-   No se admite la aplicación Microsoft Outlook (iOS y Android).

**Además**:

-  Su versión de Exchange debe ser Exchange 2010 o posterior. Se admite la matriz del servidor de acceso de cliente (CAS) del servidor de Exchange.

> [!TIP]
> Si su entorno de Exchange se encuentra en una configuración de servidor CAS, debe configurar el conector de Exchange local de modo que apunte a uno de los servidores CAS.
- Debe usar el **conector de Exchange Server** que conecta Configuration Manager con Microsoft Exchange local. Esto permite administrar dispositivos móviles y habilitar el acceso condicional (consulte [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) [Administración de dispositivos móviles mediante System Center Configuration Manager y Exchange]).
  - Asegúrese de que está usando la versión más reciente del **conector de Exchange local**. El conector de Exchange local debe configurarse a través de la consola de Configuration Manager. Para obtener un tutorial detallado, consulte [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) (Administración de dispositivos móviles mediante System Center Configuration Manager y Exchange).
  - El conector debe estar configurado solo en el sitio primario de System Center Configuration Manager.</li><li>Este conector es compatible con el entorno de CAS de Exchange. <br />        Al configurar el conector, debe establecerse para hablar con uno de los servidores CAS de Exchange.

- Exchange ActiveSync se puede configurar con autenticación basada en certificados o con la entrada de credenciales de usuario


## <a name="requirements-for-skype-for-business-online"></a>Requisitos de Skype Empresarial Online
El acceso condicional a SharePoint Online admite dispositivos que ejecutan:
 -   iOS 7.1 y versiones posteriores
 -   Android 4.0 y versiones posteriores
 -   Samsung KNOX Standard 4.0 o versiones posteriores

**Además**, debe habilitar la autenticación moderna para Skype Empresarial Online. Cumplimente este [formulario de conexión](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) para inscribirse en el programa de autenticación moderna.

Todos los usuarios finales deben usar Skype Empresarial Online. Si tiene una implementación con Skype Empresarial Online y Skype Empresarial local, no se aplicará la directiva de acceso condicional a los usuarios finales que se encuentren en la implementación local.

## <a name="requirements-for-sharepoint-online"></a>Requisitos para SharePoint Online
El acceso condicional a SharePoint Online admite dispositivos que ejecutan:
 -   Windows 8.1 y versiones posteriores (cuando están inscritos en Intune)
 -   Windows 7.0 o Windows 8.1 (si están unidos a un dominio)
 -   Windows Phone 8.1 y versiones posteriores
 -   iOS 7.1 y versiones posteriores
 -   Android 4.0 y versiones posteriores, Samsung KNOX Standard 4.0 y versiones posteriores

 **Además**:
 -   Los dispositivos deben estar combinados en el área de trabajo, que registra el dispositivo con el servicio de registro del dispositivo de Azure Active Directory (AAD DRS).

 Los equipos unidos a un dominio se deben registrar automáticamente con Azure Active Directory a través de una directiva de grupo o MSI. En la sección **Acceso condicional para equipos** de este tema se describen todos los requisitos para habilitar el acceso condicional para un equipo.

 AAD DRS se activará automáticamente para los clientes de Intune y Office 365. Los clientes que ya hayan implementado el servicio de registro de dispositivos de ADFS no podrán ver los dispositivos registrados en la instancia local de Active Directory.
 -   Es necesaria una suscripción de SharePoint Online y los usuarios deben tener licencia para SharePoint Online.

 ### <a name="conditional-access-for-pcs"></a>Acceso condicional para equipos

 Puede configurar el acceso condicional para equipos que ejecutan aplicaciones de escritorio de Office, para que tengan acceso a **Exchange Online** y **SharePoint Online** en los equipos que cumplen los requisitos siguientes:
 -   El equipo debe ejecutar Windows 7.0 o Windows 8.1.
 -   El equipo debe estar unido a un dominio o ser compatible

 Para ser compatible, el equipo debe estar inscrito en Intune y cumplir las directivas.

 Los equipos unidos a un dominio deben configurarse para que [registren automáticamente el dispositivo](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) con Azure Active Directory.
 -   [La autenticación moderna de Office 365 debe estar habilitada](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)y tener las últimas actualizaciones de Office.<br />     La autenticación moderna aporta inicio de sesión basado en Active Directory Authentication Library (AAL) para los clientes de Windows en Office 2013 y habilita una mejor seguridad como la **autenticación multifactor**y la **autenticación basada en certificados**.
 -   Configure reglas de notificaciones de ADFS para bloquear protocolos de autenticación no moderna.  

## <a name="next-steps"></a>Pasos siguientes  
 Lea los siguientes temas para obtener información sobre cómo configurar directivas de cumplimiento y las directivas de acceso condicional para su escenario requiere:  

-   [Manage access to services in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md) (Administración del acceso a servicios en System Center Configuration Manager)  

-   [Manage email access in System Center Configuration Manager](../../protect/deploy-use/manage-email-access.md) (Administración del acceso a correo electrónico en System Center Configuration Manager)  

-   [Manage SharePoint Online access in System Center Configuration Manager](../../protect/deploy-use/manage-sharepoint-online-access.md) (Administración del acceso a SharePointo Online en System Center Configuration Manager)  

-   [Manage Skype for Business Online access](../../protect/deploy-use/manage-skype-for-business-online-access.md) (Administración del acceso a Skype Empresarial Online)  

### <a name="see-also"></a>Consulte también  

 [Get started with compliance settings in System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md) (Introducción a la configuración de cumplimiento en System Center Configuration Manager)

