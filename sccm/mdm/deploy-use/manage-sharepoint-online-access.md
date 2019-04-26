---
title: Administrar el acceso a SharePoint Online
titleSuffix: Configuration Manager
description: Obtenga información acerca de cómo usar la directiva de acceso condicional de SharePoint Online de System Center Configuration Manager para administrar el acceso a OneDrive.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 69a160a3c7833f196d50185e551f619d68dc0925
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62255618"
---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>Administrar el acceso a SharePoint Online en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


La directiva de acceso condicional de Configuration Manager para **SharePoint Online** administra el acceso a los archivos de OneDrive para la Empresa, que se almacenan en SharePoint Online. El acceso se basa en las condiciones que especifique.
Puede controlar el acceso a SharePoint Online desde las siguientes aplicaciones para plataformas que se indican:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)

Las aplicaciones de escritorio de Office pueden tener acceso a SharePoint Online en equipos que ejecutan:  

-   Office 2013 de escritorio y posterior con [autenticación moderna](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) habilitada.  

-   Windows 7.0 o Windows 8.1  

> [!NOTE]  
>  Los equipos deben estar unidos a un dominio o ser compatibles con las directivas establecidas en Intune.  



 Cuando un usuario determinado intenta conectarse a un archivo mediante una aplicación compatible, como por ejemplo OneDrive, en su dispositivo, se produce la siguiente evaluación:  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 Para conectarse a los archivos requeridos, el dispositivo que ejecuta OneDrive debe:  

- Estar inscrito con Microsoft Intune o un PC unido a dominio.  

- Registrar el dispositivo en Azure Active Directory (Azure AD). Este registro se produce automáticamente cuando el dispositivo se inscribe con Intune.  

   Para equipos unidos a un dominio, debe configurarlos para que se [registren automáticamente](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) con Azure AD.  

- Ser compatible con las directivas de cumplimiento implementadas de Configuration Manager.  

  Azure AD almacena el estado del dispositivo. Concede o bloquea el acceso a los archivos, según las condiciones especificadas.  

  Si no se cumple una condición, se presenta al usuario uno de los mensajes siguientes cuando inicie sesión:  

- Si el dispositivo no está inscrito con Intune o no está registrado en Azure AD, se muestra un mensaje con instrucciones sobre cómo instalar la aplicación Portal de empresa e inscribirse.  

- Si el dispositivo no es compatible, se muestra un mensaje que dirige al usuario al portal web de Intune. Allí se puede encontrar información sobre el problema y sobre cómo resolverlo.  

- Para dispositivos móviles:

  Puede restringir el acceso a SharePoint Online cuando dicho acceso se realice desde un explorador de dispositivos en **iOS** y **Android**. Solo se permite el acceso a través de exploradores admitidos en dispositivos compatibles:  
  - Safari (iOS)
  - Chrome (Android)
  - Managed Browser (iOS y Android)  

    Los exploradores no compatibles se bloquean.  

- Para un equipo PC:  


  -   Si se establece la directiva para requerir la unión a un dominio, pero el equipo no está unido a ningún dominio, se muestra un mensaje para ponerse en contacto con el administrador de TI.  

  -   Si la directiva está establecida para requerir que el equipo esté marcado como compatible o esté unido a un dominio, pero el equipo no cumple estos requisitos, se muestra un mensaje con instrucciones sobre cómo instalar la aplicación Portal de empresa e inscribirse.  

Puede bloquear el acceso a SharePoint Online desde las siguientes aplicaciones:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)  



## <a name="configure-conditional-access-for-sharepoint-online"></a>Configuración del acceso condicional para SharePoint Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Paso 1: Configurar grupos de seguridad de Active Directory  
 Antes de empezar, configure los grupos de seguridad de Azure AD para la directiva de acceso condicional. Puede configurar estos grupos en el **centro de administración de Microsoft 365**, o el **portal de cuentas de Intune**. Estos grupos contienen los usuarios de destino o que están exentos de la directiva. Cuando un usuario es destinatario de una directiva, cada dispositivo que use debe estar marcado como compatible para poder acceder a los recursos.  

 Se pueden especificar dos tipos de grupo en una directiva de SharePoint Online:  

- **Grupos destinatarios**: Contiene grupos de usuarios al que se aplica la directiva  

- **Grupos exentos**: Contiene grupos de usuarios que están exentos de la directiva (opcional)  

  Si un usuario pertenece a ambos grupos, estará exento de la directiva.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Paso 2: Configurar e implementar una directiva de cumplimiento  
 Cree e implemente una directiva de cumplimiento para todos los dispositivos que sean destinatarios de la directiva de SharePoint Online.  

> [!NOTE]   
>  Aunque las directivas de cumplimiento se implementan en grupos de Intune o recopilaciones de Configuration Manager, las directivas de acceso condicional se destinan a grupos de seguridad de Azure AD.  

 Para más información sobre cómo configurar la directiva de cumplimiento, consulte [Administrar directivas de cumplimiento de dispositivo en System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!IMPORTANT]  
>  Si no ha implementado una directiva de cumplimiento y luego habilita la directiva de SharePoint Online, se concede acceso a todos los dispositivos que son destinatarios de la directiva.  

   

###  <a name="BKMK_OneDrive"></a> Paso 3: Configurar la directiva de SharePoint Online  

 A continuación, configure la directiva para requerir que solo los dispositivos administrados y conformes puedan tener acceso a SharePoint Online. Esta directiva se almacena en Azure AD.

 >[!NOTE]
 >También puede crear la directiva de acceso condicional en la consola de administración de Azure AD. La consola de administración de Azure AD permite crear las directivas de acceso condicional del dispositivo de Intune. Azure AD hace referencia a estas directivas como la directiva de acceso condicional basado en el dispositivo. También puede crear otras directivas de acceso condicional, como la autenticación multifactor. En el portal, puede configurar directivas de acceso condicional para aplicaciones empresariales de terceros que sean compatibles con Azure AD, como Salesforce y Box. Para más información, vea [Configuración de directivas de acceso condicional basadas en dispositivos de Azure Active Directory](/azure/active-directory/active-directory-conditional-access-policy-connected-applications).  

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2. Seleccione **Habilitar directiva de acceso condicional para SharePoint Online**.  

    ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3. En **Acceso a la aplicación**, en el caso de Outlook y las aplicaciones que usan la autenticación moderna, puede elegir restringir el acceso solo a los dispositivos compatibles con cada plataforma.  

   > [!TIP]
   >  **Autenticación moderna** proporciona el inicio de sesión basado en Active Directory Authentication Library (ADAL) a los clientes de Office.  
   > 
   > - La autenticación basada en ADAL permite a los clientes de Office realizar la autenticación basada en explorador (también conocida como autenticación pasiva). Para realizar la autenticación, se envía al usuario a una página web de inicio de sesión.  
   >   -   Este nuevo método de inicio de sesión permite nuevos escenarios, como el acceso condicional en función de la **compatibilidad del dispositivo** y de si se realizó la **autenticación multifactor**.  
   > 
   >   Para más información, vea [Cómo funciona la autenticación moderna para las aplicaciones de cliente de Office 2013 y Office 2016](https://support.office.com/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517).  

    Para los equipos con Windows, el equipo debe estar unido a un dominio o inscrito con Intune y ser conforme. Puede establecer los requisitos siguientes:  

   -   **Los dispositivos deben estar unidos al dominio o conforme**: Los equipos deben estar unido al dominio o cumplir con las directivas establecidas en Intune. Si el equipo no cumple alguno de estos requisitos, se le solicita al usuario que inscriba el dispositivo en Intune.  

   -   **Los dispositivos deben estar unidos a un dominio**: Los equipos deben estar unidos al dominio para tener acceso a Exchange Online. Si el equipo no está unido a un dominio, el acceso al correo se bloquea y el usuario debe ponerse en contacto con el administrador de TI.  

   -   **Los dispositivos deben ser compatibles**: Los equipos deben inscribirse en Intune y ser conformes. Si el equipo no está inscrito, se muestra un mensaje con instrucciones sobre cómo inscribirlo.  

4. En **acceso al explorador** a SharePoint Online y OneDrive para la empresa, puede elegir permitir el acceso a Exchange Online solo a través de los exploradores admitidos: Safari (iOS) y Chrome (Android). Se bloquea el acceso desde otros exploradores. Las mismas restricciones de plataforma que seleccionó para el acceso a las aplicaciones para OneDrive también se aplica aquí.

   En dispositivos **Android**, los usuarios deben activar la opción **Habilitar acceso al explorador** en el dispositivo inscrito como se indica aquí:
   1.  Abra la **aplicación del portal de empresa**.
   2.  Vaya a la página **Configuración** desde los tres puntos (...) o el botón de menú de hardware.
   3.  Presione el botón **Habilitar acceso al explorador** .
   4.  En el Explorador de Chrome, cierre sesión en Office 365 y reinicie Chrome.

   En las plataformas **iOS y Android**, para identificar el dispositivo que se usa para acceder al servicio, Azure AD emite un certificado de TLS para el dispositivo. El dispositivo muestra el certificado con un símbolo del sistema para el usuario final seleccione el certificado tal como se muestra en las capturas de pantalla siguiente: El usuario final debe seleccionar este certificado para que pueden continuar usando el explorador.

    **iOS**

    ![captura de pantalla de la solicitud de certificado en un iPad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

    **Android**

     ![captura de pantalla de la solicitud de certificado en un dispositivo Android](media/mdm-browser-ca-android-cert-prompt.png)

5. En la pestaña **Inicio** , en el grupo **Vínculos** , haga clic en **Configurar directiva de acceso condicional en la consola de Intune**. Puede que deba proporcionar el nombre de usuario y la contraseña de la cuenta utilizada para conectar Configuration Manager con Intune.  

    Se abre la consola de administración de Intune.  

6. En la consola de [Consola de administración de Microsoft Intune](https://manage.microsoft.com), haga clic en **Directiva** > **Acceso condicional** > **SharePoint Online Directiva**.  

7. Seleccione **Bloquear el acceso de las aplicaciones a SharePoint Online si el dispositivo no es conforme**.  

8. En **Grupos destinatarios**, haga clic en **Modificar** para seleccionar los grupos de seguridad de Azure AD a los que se aplica la directiva.  

9. Opcionalmente, en **Grupos exentos** puede hacer clic en **Modificar** para seleccionar los grupos de seguridad de Azure AD que se excluyen de esta directiva.  

10. Cuando haya terminado, haga clic en **Guardar**.  

    No es necesario implementar la directiva de acceso condicional, ya que surte efecto inmediatamente.  

    Consulte [Restringir el acceso a SharePoint Online con Microsoft Intune](/intune-classic/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune) para obtener información sobre cómo supervisar la directiva desde la consola de Intune.  

### <a name="see-also"></a>Consulte también  

 [Manage access to services in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md) (Administración del acceso a servicios en System Center Configuration Manager)
