---
title: Administrar el acceso a SharePoint Online | Microsoft Docs
description: "Obtenga información acerca de cómo usar la directiva de acceso condicional de SharePoint Online de System Center Configuration Manager para administrar el acceso a OneDrive."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
caps.latest.revision: "11"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: c564c1fc25c5156a2d9ddfa1b4123024c658bf61
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>Administrar el acceso a SharePoint Online en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


Use la directiva de acceso condicional de **SharePoint Online** para administrar el acceso a los archivos de OneDrive para la Empresa que se encuentran en SharePoint Online, en función de las condiciones que especifique.
Puede controlar el acceso a SharePoint Online desde las siguientes aplicaciones para plataformas que se indican:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)

Las aplicaciones de escritorio de Office pueden tener acceso a SharePoint Online en equipos que ejecutan:  

-   Office 2013 de escritorio y posterior con [autenticación moderna](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) habilitada.  

-   Windows 7.0 o Windows 8.1  

> [!NOTE]  
>  Los equipos deben estar unidos a un dominio o ser compatibles con las directivas establecidas en Intune.  



 Cuando un usuario determinado intenta conectarse a un archivo con una aplicación compatible como OneDrive en su dispositivo, se produce la siguiente evaluación:  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 Para conectarse a los archivos requeridos, el dispositivo que ejecuta OneDrive debe:  

-   Estar inscrito con Microsoft Intune o un PC unido a dominio.  

-   Registrar el dispositivo en Azure Active Directory, lo que se lleva a cabo automáticamente si el dispositivo está inscrito con Intune.  

     Para equipos unidos a un dominio, debe configurarlos para [registrarse automáticamente](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) con Azure Active Directory.  

-   Ser compatible con las directivas de cumplimiento implementadas de Configuration Manager.  

 El estado del dispositivo se almacena en Azure Active Directory, que concede o bloquea el acceso a los archivos según las condiciones especificadas.  

 Si no se cumple una condición, se presentará al usuario uno de los mensajes siguientes cuando inicie sesión:  

-   Si el dispositivo no está inscrito con Intune, o registrado en Azure Active Directory, se muestra un mensaje con instrucciones sobre cómo instalar la aplicación de portal de empresa e inscribirse.  

-   Si el dispositivo no es conforme, se muestra un mensaje que dirige al usuario al portal web de Intune, donde puede encontrar información sobre el problema y sobre cómo resolverlo.  

- Para dispositivos móviles:

  Al acceso a SharePoint Online se puede restringir cuando dicho acceso se realice desde un explorador de dispositivos **iOS** y **Android**.  Solo se permitirá el acceso a través exploradores admitidos en dispositivos compatibles:
* Safari (iOS)
* Chrome (Android)
* Managed Browser (iOS y Android)

  Los exploradores no compatibles se bloquearán.
-   Para un equipo PC:  


    -   Si se establece la directiva para requerir unión a un dominio y el equipo no está unido a ningún dominio, se muestra un mensaje para ponerse en contacto con el administrador de TI.  

    -   Si se establece la directiva para requerir unión a un dominio o ser conforme y el equipo no cumple con estos requisitos, se muestra un mensaje con instrucciones sobre cómo instalar la aplicación del portal de empresa e inscribirse.  

 Puede bloquear el acceso a SharePoint Online desde las siguientes aplicaciones:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)  

## <a name="configure-conditional-access-for-sharepoint-online"></a>Configuración del acceso condicional para SharePoint Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Paso 1: Configurar grupos de seguridad de Active Directory  
 Antes de empezar, configure los grupos de seguridad de Azure Active Directory para la directiva de acceso condicional. Estos grupos se pueden configurar en el **Centro de administración de Office 365**o el **portal de cuentas de Intune**. Estos grupos contienen los usuarios de destino o exentos de la directiva. Cuando un usuario es destinatario de una directiva, cada dispositivo que use debe ser conforme con el fin de obtener acceso a los recursos.  

 Se pueden especificar dos tipos de grupo en una directiva de SharePoint Online:  

-   **Grupos destinatarios**: contiene grupos de usuarios a los que se aplicará la directiva.  

-   **Grupos exentos**: contiene grupos de usuarios que están exentos de la directiva (opcional).  

 Si un usuario pertenece a ambos grupos, estará exento de la directiva.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Paso 2: Configurar e implementar una directiva de cumplimiento  
 Asegúrese de que crea e implementa una directiva de cumplimiento para todos los dispositivos a los que se destinará la directiva de SharePoint Online.  

> [!NOTE]  
>  Aunque las directivas de cumplimiento se implementan en grupos de Intune o recopilaciones de Configuration Manager, las directivas de acceso condicional se destinan a grupos de seguridad de Azure Active Directory.  

 Para más información sobre cómo configurar la directiva de cumplimiento, consulte [Administrar directivas de cumplimiento de dispositivo en System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!IMPORTANT]  
>  Si no ha implementado una directiva de cumplimiento y luego habilita la directiva de SharePoint Online, se concederá acceso a todos los dispositivos a los que se dirija la directiva.  

 Cuando esté listo, continúe con el **paso 3**.  

###  <a name="BKMK_OneDrive"></a> Paso 3: Configurar la directiva de SharePoint Online  


 A continuación, configure la directiva para requerir que solo los dispositivos administrados y conformes puedan tener acceso a SharePoint Online. Esta directiva se almacenará en Azure Active Directory.

 >[!NOTE]
 >También puede crear la directiva de acceso condicional en la consola de administración de Azure AD. La consola de administración de Azure AD le permite crear las directivas de acceso condicional de dispositivos de Intune (denominada directiva de acceso condicional basada en dispositivos en Azure AD), además de otras directivas de acceso condicional, como la autenticación multifactor. También puede configurar directivas de acceso condicional para aplicaciones empresariales de terceros, como Salesforce y Box, compatibles con Azure AD. Para obtener más información, consulte [Establecimiento de una directiva de acceso condicional basado en dispositivos de Azure Active Directory para el control de acceso a aplicaciones conectadas a Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-policy-connected-applications/).  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  Seleccione **Habilitar directiva de acceso condicional para SharePoint Online**.  

     ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3.  En **Acceso a la aplicación**, en el caso de Outlook y las aplicaciones que usan la autenticación moderna, puede elegir restringir el acceso solo a los dispositivos compatibles con cada plataforma.  

    > [!TIP]  
    >  **Autenticación moderna** proporciona el inicio de sesión basado en Active Directory Authentication Library (ADAL) a los clientes de Office.  
    >   
    >  -   La autenticación basada en ADAL permite a los clientes de Office realizar la autenticación basada en explorador (también conocida como autenticación pasiva).  Para realizar la autenticación, se envía al usuario a una página web de inicio de sesión.  
    > -   Este nuevo método de inicio de sesión permite nuevos escenarios, como el acceso condicional, según el **cumplimiento de los dispositivos** y si se realizó la **autenticación multifactor** .  
    >   
    >  En este [artículo](https://support.office.com/en-US/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) se incluye información más detallada sobre cómo funciona la autenticación moderna.  

     Para los equipos con Windows, el equipo debe estar unido a un dominio o inscrito con Intune y ser conforme. Puede establecer los requisitos siguientes:  

    -   **Los dispositivos deben estar unidos a un dominio o ser conformes.** Esto significa que los equipos deben estar unidos a un dominio o cumplir con las directivas establecidas en Intune. Si el equipo no cumple con alguno de estos requisitos, se le solicita al usuario que inscriba el dispositivo con Intune.  

    -   **Los dispositivos deben estar unidos a un dominio.** Esto significa que los equipos deben estar unidos a un dominio para tener acceso a Exchange Online. Si el equipo no está unido a un dominio, el acceso al correo electrónico se bloquea y el usuario debe ponerse en contacto con el administrador de TI.  

    -   **Los dispositivos deben ser conformes.** Esto significa que los equipos deben inscribirse en Intune y ser conformes. Si el equipo no está inscrito, se muestra un mensaje con instrucciones sobre cómo inscribirse.  

4.  En **Acceso de explorador** a SharePoint Online y OneDrive for Business, se puede elegir permitir el acceso solo a Exchange Online a través de los exploradores admitidos: Safari (iOS) y Chrome (Android). El acceso desde otros exploradores estará bloqueado.  Las mismas restricciones de plataforma que seleccionó para el acceso a las aplicaciones para OneDrive también se aplica aquí.

    En los dispositivos **Android** , los usuarios tienen que habilitar el acceso de explorador.  Para ello, el usuario final tiene que habilitar la opción "Habilitar acceso al explorador" en el dispositivo inscrito de la manera siguiente:
    1.  Abra la **aplicación del portal de empresa**.
    2.  Vaya a la página **Configuración** desde los tres puntos (...) o el botón de menú de hardware.
    3.  Presione el botón **Habilitar acceso al explorador** .
    4.  En el Explorador de Chrome, cierre sesión en Office 365 y reinicie Chrome.

    En las plataformas **iOS y Android** , para identificar el dispositivo que se utiliza para tener acceso al servicio, Azure Active Directory emitirá un certificado de Seguridad de la capa de transporte (TLS) para el dispositivo.  El dispositivo muestra el certificado con un aviso para que el usuario final seleccione el certificado, como se ve en las siguientes capturas de pantalla. El usuario final tiene que seleccionar este certificado para poder continuar usando el explorador.

     **iOS**

     ![captura de pantalla de la solicitud de certificado en un ipad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

     **Android**

      ![captura de pantalla de la solicitud de certificado en un dispositivo Android](media/mdm-browser-ca-android-cert-prompt.png)

4.  En la pestaña **Inicio** , en el grupo **Vínculos** , haga clic en **Configurar directiva de acceso condicional en la consola de Intune**. Puede que deba proporcionar el nombre de usuario y la contraseña de la cuenta utilizada para conectar Configuration Manager con Intune.  

     Se abrirá la consola de administración de Intune.  

5.  En la consola de [Consola de administración de Microsoft Intune](https://manage.microsoft.com), haga clic en **Directiva** > **Acceso condicional** > **SharePoint Online Directiva**.  

6.  Seleccione **Bloquear el acceso de las aplicaciones a SharePoint Online si el dispositivo no es conforme**.  

7.  En **Grupos de destino**, haga clic en **Modificar** para seleccionar los grupos de seguridad de Azure Active Directory a los que se aplicará la directiva.  

8.  En **Grupos exentos**, opcionalmente, haga clic en **Modificar** para seleccionar los grupos de seguridad de Azure Active Directory que se van a excluir de la directiva.  

9. Cuando haya terminado, haga clic en **Guardar**.  

 No es necesario implementar la directiva de acceso condicional, ya que surte efecto inmediatamente.  

 Consulte [Restringir el acceso a SharePoint Online con Microsoft Intune](https://technet.microsoft.com/library/dn705844.aspx) para obtener información sobre cómo supervisar la directiva desde la consola de Intune.  

### <a name="see-also"></a>Consulte también  

 [Manage access to services in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md) (Administración del acceso a servicios en System Center Configuration Manager)
