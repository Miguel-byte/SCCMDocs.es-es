---
title: "Administrar acceso al correo electrónico | Microsoft Docs"
description: "Aprenda a usar el acceso condicional de System Center Configuration Manager para administrar el acceso al correo electrónico de Exchange."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa648e73-5fb8-4818-ab57-7466ffaf888e
caps.latest.revision: "24"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: a5c2a8912cd2ef95a778b81d0b7f1f98315b8413
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="manage-email-access-in-system-center-configuration-manager"></a>Administrar el acceso a correo electrónico en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use el acceso condicional de System Center Configuration Manager para administrar el acceso al correo electrónico de Exchange según las condiciones que especifique.  

Puede administrar el acceso a:  

-   Microsoft Exchange local  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated

Puede controlar el acceso a Exchange Online y Exchange local desde el cliente de correo electrónico integrada en las siguientes plataformas:  

-   Android 4.0 y versiones posteriores, Samsung KNOX Standard 4.0 y versiones posteriores  

-   iOS 7.1 y versiones posteriores  

-   Windows Phone 8.1 y versiones posteriores  

-   Aplicación de correo en Windows 8.1 y posterior

Las aplicaciones de escritorio de Office pueden tener acceso a Exchange Online en equipos que ejecutan:  

-   Office 2013 de escritorio y posterior con [autenticación moderna](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) habilitada.  

-   Windows 7.0 o Windows 8.1  

> [!NOTE]  
>  Los equipos deben estar unidos a un dominio o ser compatibles con las directivas establecidas en Intune.  


## <a name="device-requirements"></a>Requisitos de los dispositivos
 Si configura el acceso condicional, el dispositivo que usen los usuarios debe cumplir las condiciones siguientes para que puedan conectarse al correo electrónico:  

-   Estar inscrito con Intune o ser un equipo unido a un dominio.  

-   Registrar el dispositivo en Azure Active Directory, lo que se lleva a cabo automáticamente cuando el dispositivo está inscrito con Intune (solo para Exchange Online). Además, el id. de Exchange ActiveSync del cliente debe registrarse con Azure Active Directory (no se aplica a dispositivos de Windows y Windows Phone que se conectan a Exchange local).  

     Los equipos PC unidos a un dominio deben configurarse para que se registren automáticamente con Azure Active Directory.  En la sección**Acceso condicional para equipos** del tema [Administrar el acceso a servicios en System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md) se enumeran todos los requisitos para habilitar el acceso condicional de equipos PC.  

-   Cumplir todas las directivas de cumplimiento de Configuration Manager implementadas en el dispositivo  

 Si no se cumple una condición de acceso condicional, el usuario recibirá uno de los dos mensajes siguientes cuando inicie sesión:  

-   Si el dispositivo no está inscrito en Intune o no está registrado en Azure Active Directory, se muestra un mensaje con instrucciones sobre cómo instalar la aplicación de portal de empresa, inscribir el dispositivo y (para dispositivos iOS y Android) activar el correo electrónico, que asocia el identificador de Exchange ActiveSync del dispositivo con el registro del dispositivo en Azure Active Directory.  

-   Si el dispositivo no es conforme, se muestra un mensaje que dirige al usuario al portal web de Intune, donde puede encontrar información sobre el problema y sobre cómo resolverlo.  

**Para dispositivos móviles:**

Puede restringir el acceso a **Outlook Web Access (OWA)** en Exchange Online cuando se tiene acceso desde un explorador en dispositivos **iOS** y **Android** .  Solo se permitirá el acceso a través exploradores admitidos en dispositivos compatibles:

* Safari (iOS)
* Chrome (Android)
* Managed Browser (iOS y Android)

Se bloquearán los exploradores no admitidos. Igualmente no se admiten las aplicaciones OWA para iOS y Android.  Deben bloquearse mediante reglas de notificaciones ADFS:
* Configure reglas de notificaciones de ADFS para bloquear protocolos de autenticación no moderna. Las instrucciones detalladas se describen en el Escenario 3: [Bloquear todo el acceso externo a Office 365 excepto las aplicaciones basadas en explorador](https://technet.microsoft.com/library/dn592182.aspx).

 **Para los equipos PC:**  

-   Si el requisito de la directiva de acceso condicional es permitir **unido al dominio** o **conforme**, se muestra un mensaje con instrucciones sobre cómo inscribir el dispositivo. Si el equipo no cumple con alguno de estos requisitos, se le solicitará al usuario que inscriba el dispositivo con Intune.  

-   Si el requisito de la directiva de acceso condicional se establece para permitir solo los dispositivos de Windows unidos a un dominio, el dispositivo se bloquea y aparece un mensaje para ponerse en contacto con el administrador de TI.  

 Puede bloquear el acceso al correo electrónico de Exchange desde el cliente de correo electrónico de Exchange ActiveSync integrado en los dispositivos en las siguientes plataformas:  

-   Android 4.0 y versiones posteriores, Samsung KNOX Standard 4.0 y versiones posteriores  

-   iOS 7.1 y versiones posteriores  

-   Windows Phone 8.1 y versiones posteriores  

-   La aplicación **Correo** en Windows 8.1 y versiones posteriores  

 Las aplicaciones Outlook para iOS y Android y de escritorio de Outlook 2013 y posteriores solo son compatibles con Exchange Online.  

 El **conector de Exchange local** entre Configuration Manager y Exchange es necesario para que funcione el acceso condicional.  

 Puede configurar una directiva de acceso condicional para Exchange local desde la consola de Configuration Manager. Al configurar una directiva de acceso condicional para Exchange Online, puede comenzar el proceso en la consola de Configuration Manager, que inicia la consola de Intune donde puede completar el proceso.  

## <a name="configure-conditional-access"></a>Configuración de acceso condicional
### <a name="step-1-evaluate-the-effect-of-the-conditional-access-policy"></a>Paso 1: evaluar el impacto de la directiva de acceso condicional  
 Una vez haya configurado el **conector de Exchange local**, puede usar el informe de la **Lista de dispositivos por estado de acceso condicional** de Configuration Manager para identificar los dispositivos que tendrán bloqueado el acceso a Exchange después de configurar la directiva de acceso condicional. Este informe también requiere:  

-   Una suscripción a Intune  

-   El punto de conexión de servicio se debe configurar e implementar.  

 En los parámetros del informe, seleccione el grupo de Intune que desea evaluar y, si es necesario, las plataformas de dispositivos a las que se aplicará la directiva.  

 Para más información sobre cómo ejecutar informes, consulte [Generación de informes en System Center Configuration Manager](../../core/servers/manage/reporting.md).  

 Después de ejecutar el informe, examine estas cuatro columnas para determinar si un usuario se bloqueará:  

-   **Canal de administración**: indica si Intune, Exchange ActiveSync o ambas aplicaciones administran el dispositivo.  

-   **Registrado en AAD**: indica si el dispositivo está registrado con Azure Active Directory (lo que se conoce como unión al "área de trabajo").  

-   **Conforme**: indica si el dispositivo cumple con las directivas de cumplimiento que se han implementado.  

-   **EAS activado**: los dispositivos iOS y Android deben tener su identificador de Exchange ActiveSync asociado al registro de registro del dispositivo en Azure Active Directory. Esto sucede cuando el usuario hace clic en el vínculo **Activar correo electrónico** en el correo electrónico de cuarentena.  

    > [!NOTE]  
    >  Los dispositivos Windows Phone siempre muestran un valor en esta columna.  

 Los dispositivos que forman parte de una recopilación o un grupo de destino tendrán bloqueado el acceso a Exchange, a menos que los valores de la columna coincidan con los de la tabla siguiente:  

|Canal de administración|Registrado en AAD|conforme|EAS activado|Acción resultante|  
|------------------------|--------------------|---------------|-------------------|----------------------|  
|**Administrado por Microsoft Intune y Exchange ActiveSync**|Sí|Sí|Se muestra**Sí** o **No** |Acceso a correo electrónico concedido|  
|Cualquier otro valor|No|No|No se muestra ningún valor|Acceso a correo electrónico bloqueado|  

 Puede exportar el contenido del informe y utilizar la columna **Dirección de correo electrónico** para informar a los usuarios de que se les va a bloquear.  

### <a name="step-2-configure-user-groups-or-collections-for-the-conditional-access-policy"></a>Paso 2: configurar las recopilaciones o grupos de usuarios de la directiva de acceso condicional  
 El destino de las directivas de acceso condicional se define en distintos grupos o recopilaciones de usuarios en función de los tipos de directiva. Estos grupos contienen los usuarios de destino o exentos de la directiva. Cuando un usuario es destinatario de una directiva, cada dispositivo que use debe ser conforme con el fin de obtener acceso al correo electrónico.  

-   **Directiva de Exchange Online**: dirigida a grupos de usuarios de seguridad de Azure Active Directory. Estos grupos se pueden configurar en el **Centro de administración de Office 365**o el **portal de cuentas de Intune**.  

-   **Directiva de Exchange local**: para recopilaciones de usuarios de Configuration Manager. Puede configurar estas opciones en el área de trabajo **Activos y compatibilidad** .  

 Se pueden especificar dos tipos de grupo en cada directiva:  

-   **Grupos destinatarios**: grupos o recopilaciones de usuarios a los que se aplica la directiva  

-   **Grupos exentos**: grupos o recopilaciones de usuarios que están exentos de la directiva (opcional)  

 Si un usuario pertenece a ambos, estará exento de la directiva.  

 Solo los grupos o las recopilaciones que son destinatarios de la directiva de acceso condicional se evalúan para el acceso a Exchange.  

### <a name="step-3-configure-and-deploy-a-compliance-policy"></a>Paso 3: configurar e implementar una directiva de cumplimiento  
 Asegúrese de que ha creado e implementado una directiva de cumplimiento para todos los dispositivos a los que se destinará la directiva de acceso condicional a Exchange.  

 Para más detalles sobre cómo configurar la directiva de cumplimiento, consulte [Administrar directivas de cumplimiento de dispositivo en System Center Configuration Manager](device-compliance-policies.md).  

> [!IMPORTANT]  
>  Si no ha implementado una directiva de cumplimiento y habilitado la directiva de acceso condicional a Exchange, se permitirá el acceso a todos los dispositivos destinatarios.  

 Cuando esté listo, continúe en el **paso 4**.  

### <a name="step-4-configure-the-conditional-access-policy"></a>Paso 4: configurar la directiva de acceso condicional  

#### <a name="for-exchange-online-and-tenants-in-the-new-exchange-online-dedicated-environment"></a>Para Exchange Online (y los inquilinos del nuevo entorno de Exchange Online dedicado)

>[!NOTE]
>También puede crear la directiva de acceso condicional en la consola de administración de Azure AD. La consola de administración de Azure AD le permite crear las directivas de acceso condicional de dispositivos de Intune (denominada directiva de acceso condicional basada en dispositivos en Azure AD), además de otras directivas de acceso condicional, como la autenticación multifactor. También puede configurar directivas de acceso condicional para aplicaciones empresariales de terceros, como Salesforce y Box, compatibles con Azure AD. Para obtener más información, consulte [Establecimiento de una directiva de acceso condicional basado en dispositivos de Azure Active Directory para el control de acceso a aplicaciones conectadas a Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-policy-connected-applications/).

 Las directivas de acceso condicional de Exchange Online utilizan el siguiente flujo para evaluar si se permitirá o bloqueará el acceso a los dispositivos.  

 ![ConditionalAccess8 &#45; 1](media/ConditionalAccess8-1.png)  

 Para acceder al correo electrónico, el dispositivo debe:  

-   Inscribirse con Intune  

-   Los equipos deben estar unidos a un dominio o estar inscritos y cumplir con las directivas establecidas en Intune.  

-   Registrar el dispositivo en Azure Active Directory, lo que se lleva a cabo automáticamente si el dispositivo está inscrito con Intune.  

     Los equipos unidos a un dominio deben configurarse para que [registren automáticamente el dispositivo](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) con Azure Active Directory.  

-   Tener activado el correo electrónico, que asocia el identificador de Exchange ActiveSync del dispositivo con el registro del dispositivo en Azure Active Directory (aplicable solo a dispositivos iOS y Android).  

-   Cumplir todas las directivas de cumplimiento implementadas.  

 El estado del dispositivo se almacena en Azure Active Directory, que concede o bloquea el acceso al correo electrónico según las condiciones evaluadas.  

 Si no se cumple una condición, el usuario verá uno de los mensajes siguientes cuando inicie sesión:  

-   Si el dispositivo no está inscrito o registrado en Azure Active Directory, se muestra un mensaje con instrucciones sobre cómo instalar la aplicación de portal de empresa e inscribirse.  

-   Si el dispositivo no es conforme, se muestra un mensaje que dirige al usuario al sitio web del portal de empresa Intune o a la aplicación del portal de empresa, donde puede encontrar información sobre el problema y sobre cómo resolverlo.  

-   Para un equipo PC:  

    -   Si se establece la directiva para requerir unión a un dominio y el equipo no está unido a ningún dominio, se muestra un mensaje para ponerse en contacto con el administrador de TI.  

    -   Si se establece la directiva para requerir unión a un dominio o ser conforme y el equipo no cumple con estos requisitos, se muestra un mensaje con instrucciones sobre cómo instalar la aplicación del portal de empresa e inscribirse.  

 El mensaje se muestra en el dispositivo para los usuarios de Exchange Online y los inquilinos en el nuevo entorno de Exchange Online dedicado, y se envía a la bandeja de entrada de correo electrónico de los usuarios de Exchange local y los dispositivos heredados dedicado de Exchange Online dedicados.  

> [!NOTE]  
>  Las reglas de acceso condicional de Configuration Manager reemplazan, permiten, bloquean y ponen en cuarentena las reglas que se han definido en la consola de administración de Exchange Online.  

> [!NOTE]  
>  Debe configurar la directiva de acceso condicional en la consola de Intune. Los siguientes pasos comienzan accediendo a la consola de Intune a través de Configuration Manager. Si se le solicita, inicie sesión con las mismas credenciales que usó para configurar el punto de conexión de servicio entre Configuration Manager e Intune.  

##### <a name="to-enable-the-exchange-online-policy"></a>Para habilitar la directiva de Exchange Online  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  Expanda **Configuración de cumplimiento**, **Acceso condicional**y, a continuación, haga clic en **Exchange Online**.  

3.  En la pestaña **Inicio** , en el grupo **Vínculos** , haga clic en **Configurar directiva de acceso condicional en la consola de Intune**. Probablemente tendrá que proporcionar el nombre de usuario y la contraseña de la cuenta que usó para conectar Configuration Manager con cualquier administrador global del servicio Intune.  

     Se abre la consola de administración de Intune.  

4.  En la consola de [consola de administración de Microsoft Intune](https://manage.microsoft.com), haga clic en **Directiva** > **Acceso condicional** > **Exchange Online Directiva**.  

     ![HybridOnlineSetupIntune](media/HybridOnlineSetupIntune.png)  

5.  En la página **Directivas de Exchange Online** , seleccione **Habilitar directiva de acceso condicional para Exchange Online**. Si selecciona esta opción, el dispositivo debe ser conforme. Si no se selecciona esta opción, el acceso condicional no se aplica.  

    > [!NOTE]  
    >  Si no ha implementado una directiva de cumplimiento y habilita la directiva de Exchange Online, todos los dispositivos de destino se considerarán conformes.  
    >   
    >  Independientemente del estado de cumplimiento, todos los usuarios a los que se aplique la directiva deberán inscribir sus dispositivos en Intune.  

6.  En **Acceso a la aplicación**, para Outlook y otras aplicaciones que usan la autenticación moderna, puede optar por restringir el acceso solo a los dispositivos que cumplen para cada plataforma.  Los dispositivos de Windows deben estar unidos a un dominio o estar inscritos en Intune y ser compatibles.  

    > [!TIP]  
    >  **Autenticación moderna** proporciona el inicio de sesión basado en Active Directory Authentication Library (ADAL) a los clientes de Office.  
    >   
    >  -   La autenticación basada en ADAL permite a los clientes de Office realizar la autenticación basada en explorador (también conocida como autenticación pasiva).  Para realizar la autenticación, se envía al usuario a una página web de inicio de sesión.  
    > -   Este nuevo método de inicio de sesión permite nuevos escenarios, como el acceso condicional, según el **cumplimiento de los dispositivos** y si se realizó la **autenticación multifactor** .  
    >   
    >  En este [artículo](https://support.office.com/en-US/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) se incluye información más detallada sobre cómo funciona la autenticación moderna.  

     Si usa Exchange Online con Configuration Manager e Intune, no solo podrá administrar dispositivos móviles con acceso condicional, sino que también podrá administrar equipos de escritorio. Los equipos deben estar unidos a un dominio o estar inscritos en Intune y ser conformes. Puede establecer los requisitos siguientes:  

    -   **Los dispositivos deben estar unidos a un dominio o ser conformes.** Esto significa que los equipos deben estar unidos a un dominio o cumplir las directivas. Si un equipo no cumple alguno de estos requisitos, se le solicita al usuario que inscriba el dispositivo en Intune.  

    -   **Los dispositivos deben estar unidos a un dominio.** Los equipos deben estar unidos a un dominio para tener acceso a Exchange Online. Si el equipo no está unido a un dominio, el acceso al correo electrónico se bloquea y el usuario debe ponerse en contacto con el administrador de TI.  

    -   **Los dispositivos deben ser conformes.** Los equipos deben inscribirse en Intune y ser conformes. Si el equipo no está inscrito, se muestra un mensaje con instrucciones sobre cómo inscribirse.  

7.  En **Outlook web access (OWA)**, puede elegir permitir el acceso a Exchange Online solo a través de los exploradores admitidos: Safari (iOS) y Chrome (Android). Se bloqueará el acceso desde otros exploradores. Las mismas restricciones de plataforma que seleccionó para el acceso a las aplicaciones para Outlook también se aplica aquí.

    En los dispositivos **Android** , los usuarios tienen que habilitar el acceso de explorador.  Para ello, el usuario final tiene que habilitar la opción "Habilitar acceso al explorador" en el dispositivo inscrito como sigue:
     1. Abra la **aplicación del portal de empresa**.
     2. Vaya a la página **Configuración** desde los tres puntos (...) o el botón de menú de hardware.
      3.    Presione el botón **Habilitar acceso al explorador** .
      4.    En el Explorador de Chrome, cierre sesión en Office 365 y reinicie Chrome.

     En las plataformas **iOS y Android** , para identificar el dispositivo que se utiliza para tener acceso al servicio, Azure Active Directory emitirá un certificado de Seguridad de la capa de transporte (TLS) para el dispositivo.  El dispositivo muestra el certificado con un aviso para que el usuario final seleccione el certificado, como se ve en las siguientes capturas de pantalla. El usuario final tiene que seleccionar este certificado para poder continuar usando el explorador.

     **iOS**

     ![captura de pantalla de la solicitud de certificado en un ipad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

    **Android**

    ![captura de pantalla de la solicitud de certificado en un dispositivo Android](media/mdm-browser-ca-android-cert-prompt.png)

7.  En las**aplicaciones de correo Exchange ActiveSync**, puede bloquear el acceso del correo electrónico a Exchange Online si el dispositivo no cumple los requisitos y elegir si quiere permitir o bloquear el acceso al correo electrónico cuando Intune no pueda administrar el dispositivo.  

8.  En **Grupos de destino**, seleccione los grupos de seguridad de Active Directory a los que se aplicará la directiva.  

    > [!NOTE]  
    >  Para los usuarios que se encuentren en los grupos de destino, las directivas de Intune reemplazarán las directivas y reglas de Exchange.  
    >   
    >  Exchange solo aplicará sus directivas y sus reglas de permiso, bloqueo y cuarentena si:  
    >   
    >  -   El usuario no tiene licencia para Intune.  
    > -   El usuario tiene licencia para Intune pero no pertenece a ningún grupo de seguridad de destino de la directiva de acceso condicional.  

9. En **Grupos exentos**, seleccione los grupos de seguridad de Active Directory que se van a excluir de la directiva. Si un usuario está incluido tanto en los grupos de destino como en los exentos, la directiva no se aplicará a estos grupos y tendrán acceso al correo electrónico del usuario.  

10. Cuando termine, haga clic en **Guardar**.  

-   No es necesario implementar la directiva de acceso condicional, ya que surte efecto inmediatamente.  

-   Cuando un usuario crea una cuenta de correo electrónico, el dispositivo se bloquea inmediatamente.  

-   Si un usuario bloqueado inscribe el dispositivo con Intune (o corrige la no conformidad), el acceso al correo electrónico se desbloquea en dos minutos.  

-   Si el usuario anula la inscripción del dispositivo, el correo electrónico se bloquea transcurridas unas 6 horas.  

### <a name="for-exchange-on-premises-and-tenants-in-the-legacy-exchange-online-dedicated-environment"></a>Para Exchange local (y los inquilinos del entorno heredado de Exchange Online dedicado)  
 Las directivas de acceso condicional de Exchange local y los inquilinos del entorno heredado de Exchange Online dedicado utilizan el siguiente flujo para evaluar si se deben permitir o bloquear los dispositivos.  

 ![ConditionalAccess8 &#45; 2](media/ConditionalAccess8-2.png)  

##### <a name="to-enable-the-exchange-on-premises-policy"></a>Para habilitar la directiva de Exchange local  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  Expanda **Configuración de cumplimiento**, **Acceso condicional**y, a continuación, haga clic en **Exchange local**.  

3.  En la pestaña **Inicio** , en el grupo **Exchange local** , haga clic en **Configurar directiva de acceso condicional**.  

4.  **A partir de la versión 1602 de Configuration Manager**, en la página **General** del **Asistente de configuración de directivas de acceso condicional**, especifique si desea invalidar la regla predeterminada de Exchange Active Sync. Haga clic en esta opción si desea que los dispositivos inscritos y conformes tengan acceso siempre al correo electrónico, incluso cuando la regla predeterminada se configure en cuarentena o bloqueo de acceso.  

    > [!NOTE]  
    >  Hay un problema con la invalidación predeterminada para dispositivos Android. Si se establece la regla de acceso predeterminada del servidor de Exchange en **Bloquear** y se habilita la directiva de acceso condicional de Exchange con la opción de invalidación de regla predeterminada, es posible que los dispositivos Android de los usuarios de destino no se desbloqueen incluso si son dispositivos inscritos y conformes con Intune.  Para solucionar este problema, establezca la regla de acceso predeterminada de Exchange en **Cuarentena**. El dispositivo no obtiene acceso a Exchange de forma predeterminada, y el administrador puede obtener un informe del servidor de Exchange en la lista de dispositivos que se ponen en cuarentena.  

     Si no ha configurada una cuenta de correo electrónico de notificación junto con el conector de Exchange, verá una advertencia en esta página y el botón **Siguiente** estará deshabilitado.  Para continuar, debe configurar primero las opciones de correo electrónico de notificación en el conector de Exchange y, a continuación, volver al **Asistente de configuración de directivas de acceso condicional** para completar el proceso.  

     ![HybridCondAccessWiz1](media/HybridCondAccessWiz1.PNG)  

     Haga clic en **Siguiente**.  

5.  En la página **Colecciones objetivo** , agregue una o varias recopilaciones de usuarios. Para tener acceso a Exchange, los usuarios de estas recopilaciones deben inscribir sus dispositivos en Intune y también cumplir las directivas de cumplimiento que se han implementado.  

     ![HybridCondAccessWiz2](media/HybridCondAccessWiz2.PNG)  

     Haga clic en **Siguiente**.  

6.  En la página **Colecciones exentas** , agregue las recopilaciones de usuarios que desea excluir de la directiva de acceso condicional. Los usuarios de estos grupos no necesitan inscribir sus dispositivos en Intune ni cumplir las directivas de cumplimiento implementadas para tener acceso a Exchange.  

     ![HybridCondAccessWiz3](media/HybridCondAccessWiz3.png)  

     Si un usuario está incluido en listas objetivo y exentas, estarán exentos de la directiva de acceso condicional.  

     Haga clic en **Siguiente**.  

7.  En la página **Editar notificación de usuario**, configure el correo electrónico que Intune envía a los usuarios con instrucciones sobre cómo desbloquear el dispositivo (además del correo electrónico que envía Exchange).  

     Puede modificar el mensaje predeterminado y usar etiquetas HTML para formatear el aspecto del texto. Asimismo, también puede enviar de antemano un correo electrónico a los empleados, para informarles sobre los próximos cambios y enviarles instrucciones acerca de cómo inscribir sus dispositivos.  

     ![HybridCondAccessWiz4](media/HybridCondAccessWiz4.PNG)  

    > [!NOTE]  
    >  Dado que el correo electrónico de notificación de Intune que contiene instrucciones de corrección se envía al buzón de Exchange del usuario, en caso de que el dispositivo del usuario se bloquee antes de recibir el mensaje de correo electrónico, puede usar un dispositivo desbloqueado u otro método para acceder a Exchange y ver el mensaje.  

    > [!NOTE]  
    >  Para que Exchange pueda enviar el correo electrónico de notificación, debe configurar la cuenta que se usará para enviarlo. Puede hacerlo cuando configure las propiedades del conector de Exchange Server.  
    >   
    >  Para más detalles, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

     Haga clic en **Siguiente**.  

8.  En la página  **Resumen** , revise la configuración y, a continuación, complete el asistente.  

-   No es necesario implementar la directiva de acceso condicional, ya que surte efecto inmediatamente.  

-   Después de que un usuario configure un perfil de Exchange ActiveSync, se puede tardar de 1 a 3 horas en bloquear el dispositivo (si no está administrado por Intune).  

-   Si un usuario bloqueado luego inscribe el dispositivo con Intune (o corrige la no conformidad), el acceso al correo electrónico se desbloqueará en dos minutos.  

-   Si el usuario anula la inscripción de Intune, se puede tardar de 1 a 3 horas en desbloquear el dispositivo.  

### <a name="see-also"></a>Consulte también  
 [Manage access to services in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md) (Administración del acceso a servicios en System Center Configuration Manager)
