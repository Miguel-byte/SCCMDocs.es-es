---
title: Administrar acceso al correo electrónico
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo usar el acceso condicional de Configuration Manager para administrar el acceso al correo electrónico de Exchange.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: fa648e73-5fb8-4818-ab57-7466ffaf888e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2ee4ed8f102507b4d62a1ccbfe1cc38240e85df9
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/19/2019
ms.locfileid: "58196864"
---
# <a name="manage-email-access-in-configuration-manager"></a>Administrar el acceso de correo electrónico en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use el Administrador de configuración acceso condicional para administrar el acceso al correo electrónico de Exchange según las condiciones que especifique.  

Puede administrar el acceso a:  

- Microsoft Exchange local  

- Microsoft Exchange Online  

- Exchange Online Dedicated  

Puede controlar el acceso a Exchange Online y Exchange local desde el cliente de correo electrónico integrada en las siguientes plataformas:  

- Android 4.0 y versiones posteriores, Samsung KNOX Standard 4.0 y versiones posteriores  

- iOS 9.0 y versiones posteriores  

- Windows Phone 8.1 y versiones posteriores  

- Aplicación de correo en Windows 8.1 y posterior  

Las aplicaciones de escritorio de Office pueden tener acceso a Exchange Online en equipos que ejecutan:  

- Office 2013 de escritorio y posterior con [autenticación moderna](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) habilitada.  

- Windows 7.0 o Windows 8.1  

> [!NOTE]  
> Los equipos deben estar unidos al dominio o ser compatibles con las directivas establecidas en Intune.  


## <a name="device-requirements"></a>Requisitos de los dispositivos
Si configura el acceso condicional, el dispositivo que usen los usuarios debe cumplir las condiciones siguientes para que puedan conectarse al correo electrónico:  

- Estar inscrito con Intune o ser un equipo unido a un dominio.  

- Registrar el dispositivo en Azure Active Directory, lo que se lleva a cabo automáticamente cuando el dispositivo está inscrito con Intune (solo para Exchange Online). Además, el id. de Exchange ActiveSync del cliente debe registrarse con Azure Active Directory (no se aplica a dispositivos de Windows y Windows Phone que se conectan a Exchange local).  

    Los equipos PC unidos a un dominio deben configurarse para que se registren automáticamente con Azure Active Directory. El **acceso condicional para equipos** sección la [administrar el acceso a servicios](../../protect/deploy-use/manage-access-to-services.md) artículo enumera todos los requisitos para habilitar el acceso condicional para equipos.  

- Cumplir todas las directivas de cumplimiento de Configuration Manager implementadas en el dispositivo  

    Si no se cumple una condición de acceso condicional, se presenta al usuario con uno de los mensajes siguientes cuando inicie sesión:  

- Si el dispositivo no está inscrito con Intune o no está registrado en Azure Active Directory, se muestra un mensaje con instrucciones sobre cómo instalar la aplicación de portal de empresa, inscribir el dispositivo y (para dispositivos iOS y Android), activar el correo electrónico, que asocia la Identificador de dispositivo Exchange ActiveSync con el registro del dispositivo en Azure Active Directory.  

- Si el dispositivo no es conforme, se muestra un mensaje que dirige al usuario al portal web de Intune donde puede encontrar información sobre el problema y cómo resolverlo.  

#### <a name="for-mobile-devices"></a>Para dispositivos móviles

Puede restringir el acceso a **Outlook Web Access (OWA)** en Exchange Online cuando se tiene acceso desde un explorador en dispositivos **iOS** y **Android** . Solo se permitirá el acceso a través exploradores admitidos en dispositivos compatibles:  

- Safari (iOS)  
- Chrome (Android)  
- Managed Browser (iOS y Android)  

Los exploradores no compatibles se bloquearán. No se admiten las aplicaciones OWA para iOS y Android. Deben bloquearse mediante reglas de notificaciones ADFS:  

- Configure reglas de notificaciones de ADFS para bloquear protocolos de autenticación no moderna. Se proporcionan instrucciones detalladas en el escenario 3 a [bloquear todo el acceso a Office 365 excepto las aplicaciones basadas en explorador](https://technet.microsoft.com/library/dn592182.aspx).  

#### <a name="for-pcs"></a>Para equipos

- Si el requisito de la directiva de acceso condicional es permitir **unido al dominio** o **conforme**, se muestra un mensaje con instrucciones sobre cómo inscribir el dispositivo. Si el equipo no cumple con alguno de estos requisitos, se le solicitará al usuario que inscriba el dispositivo con Intune.  

- Si el requisito de la directiva de acceso condicional se establece para permitir solo los dispositivos de Windows unidos a un dominio, el dispositivo se bloquea y aparece un mensaje para ponerse en contacto con el administrador de TI.  

Puede bloquear el acceso al correo electrónico de Exchange desde el cliente de correo electrónico de Exchange ActiveSync integrado en los dispositivos en las siguientes plataformas:  

- Android 4.0 y versiones posteriores, Samsung KNOX Standard 4.0 y versiones posteriores  

- iOS 9.0 y versiones posteriores  

- Windows Phone 8.1 y versiones posteriores  

- La aplicación **Correo** en Windows 8.1 y versiones posteriores  

Las aplicaciones Outlook para iOS y Android y de escritorio de Outlook 2013 y posteriores solo son compatibles con Exchange Online.  

El **conector de Exchange local** entre Configuration Manager y Exchange es necesario para que funcione el acceso condicional.  

Puede configurar una directiva de acceso condicional para Exchange local desde la consola de Configuration Manager. Al configurar una directiva de acceso condicional para Exchange Online, puede comenzar el proceso en la consola de Configuration Manager, que inicia la consola de Intune donde puede completar el proceso.  



## <a name="configure-conditional-access"></a>Configuración de acceso condicional

### <a name="step-1-evaluate-the-effect-of-the-conditional-access-policy"></a>Paso 1: Evaluar el impacto de la directiva de acceso condicional  

Una vez que haya configurado el **Exchange connector local**, puede usar el Administrador de configuración **lista de dispositivos por estado de acceso condicional** informe para identificar los dispositivos que tendrán bloqueados acceso a Exchange después de configurar la directiva de acceso condicional. Este informe también requiere:  

- Una suscripción a Intune  

- El punto de conexión de servicio se debe configurar e implementar.  

En los parámetros del informe, seleccione el grupo de Intune que desea evaluar y, si es necesario, las plataformas de dispositivos a las que se aplicará la directiva.  

Para obtener más información sobre cómo crear informes, consulte [Reporting in Configuration Manager](/sccm/core/servers/manage/reporting).  

Después de ejecutar el informe, examine estas cuatro columnas para determinar si un usuario se bloqueará:  

- **Canal de administración**: El dispositivo se administra mediante Intune, Exchange ActiveSync o ambos.  

- **Registrado en AAD**: El dispositivo está registrado con Azure Active Directory (conocido como el área de trabajo).  

- **Conforme**: El dispositivo es compatible con las directivas de cumplimiento que ha implementado.  

- **EAS activado**: dispositivos iOS y Android deben tener su Id. de ActiveSync de Exchange asociado con el registro del dispositivo en Azure Active Directory. Esto sucede cuando el usuario hace clic en el vínculo **Activar correo electrónico** en el correo electrónico de cuarentena.  

    > [!NOTE]  
    > Los dispositivos Windows Phone siempre muestran un valor en esta columna.  

Los dispositivos que forman parte de una recopilación o un grupo de destino tendrán bloqueado el acceso a Exchange, a menos que los valores de la columna coincidan con los de la tabla siguiente:  

|Canal de administración|Registrado en AAD|conforme|EAS activado|Acción resultante|  
|------------------------|--------------------|---------------|-------------------|----------------------|  
|**Administrado por Microsoft Intune y Exchange ActiveSync**|Sí|Sí|Se muestra**Sí** o **No** |Acceso a correo electrónico concedido|  
|Cualquier otro valor|No|No|No se muestra ningún valor|Acceso a correo electrónico bloqueado|  

Puede exportar el contenido del informe y utilizar la columna **Dirección de correo electrónico** para informar a los usuarios de que se les va a bloquear.  


### <a name="step-2-configure-user-groups-or-collections-for-the-conditional-access-policy"></a>Paso 2: Configurar grupos de usuarios o las colecciones de la directiva de acceso condicional  

El destino de las directivas de acceso condicional se define en distintos grupos o recopilaciones de usuarios en función de los tipos de directiva. Estos grupos contienen los usuarios de destino o exentos de la directiva. Cuando un usuario es destinatario de una directiva, cada dispositivo que use debe ser conforme con el fin de obtener acceso al correo electrónico.  

- **Directiva de Exchange Online**: para grupos de usuarios de seguridad de Azure Active Directory. Puede configurar estos grupos en el **centro de administración de Microsoft 365**, o el **portal de cuentas de Intune**.  

- **Directiva de Exchange local**: para recopilaciones de usuarios de Configuration Manager. Puede configurar estas opciones en el área de trabajo **Activos y compatibilidad** .  

Se pueden especificar dos tipos de grupo en cada directiva:  

- **Grupos destinatarios**: Grupos de usuarios o las colecciones a la que se aplica la directiva  

- **Grupos exentos**: Grupos de usuarios o las colecciones que están exentas de la directiva (opcional)  

Si un usuario pertenece a ambos, estará exento de la directiva.  

Solo los grupos o las recopilaciones que son destinatarios de la directiva de acceso condicional se evalúan para el acceso a Exchange.  


### <a name="step-3-configure-and-deploy-a-compliance-policy"></a>Paso 3: Configurar e implementar una directiva de cumplimiento  

Asegúrese de que ha creado e implementado una directiva de cumplimiento para todos los dispositivos a los que se destinará la directiva de acceso condicional a Exchange.  

Para obtener más información sobre cómo configurar la directiva de cumplimiento, vea [Administración de directivas de cumplimiento del dispositivo](device-compliance-policies.md).  

> [!IMPORTANT]  
> Si aún no ha implementado una directiva de cumplimiento y, a continuación, habilita una directiva de acceso condicional de Exchange, todos los dispositivos de destino se permitirá acceso.  


### <a name="step-4-configure-the-conditional-access-policy"></a>Paso 4: Configurar la directiva de acceso condicional  

#### <a name="for-exchange-online-and-tenants-in-the-new-exchange-online-dedicated-environment"></a>Para Exchange Online (y los inquilinos del nuevo entorno de Exchange Online dedicado)

> [!NOTE]  
> También puede crear la directiva de acceso condicional en la consola de administración de Azure AD. La consola de administración de Azure AD le permite crear las directivas de acceso condicional de dispositivos de Intune (denominada directiva de acceso condicional basada en dispositivos en Azure AD), además de otras directivas de acceso condicional, como la autenticación multifactor. También puede configurar directivas de acceso condicional para aplicaciones empresariales de terceros, como Salesforce y Box, compatibles con Azure AD. Para obtener más información, consulte [How To: Requerir que los dispositivos administrados para el acceso a la aplicación en la nube con acceso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

Las directivas de acceso condicional de Exchange Online utilizan el siguiente flujo para evaluar si se permitirá o bloqueará el acceso a los dispositivos.  

![Flujo de acceso condicional](media/ConditionalAccess8-1.png)  

Para acceder al correo electrónico, el dispositivo debe:  

- Inscribirse con Intune  

- Los equipos deben estar unido al dominio o estar inscritos y cumplir con las directivas establecidas en Intune  

- Registrar el dispositivo en Azure AD. Esto sucede automáticamente cuando el dispositivo está inscrito con Intune. Equipos unidos a un dominio, debe configurarlo para [registrar automáticamente el dispositivo](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-manual-steps) con Azure AD.  

- Tener activado el correo electrónico, que asocia el identificador de Exchange ActiveSync del dispositivo con el registro del dispositivo en Azure Active Directory (aplicable solo a dispositivos iOS y Android).  

- Cumplir todas las directivas de cumplimiento implementadas.  

El estado del dispositivo se almacena en Azure Active Directory, que concede o bloquea el acceso al correo electrónico según las condiciones evaluadas.  

Si no se cumple una condición, se presenta al usuario con uno de los mensajes siguientes cuando inician sesión en:  

- Si el dispositivo no está inscrito o registrado en Azure AD, se muestra un mensaje con instrucciones sobre cómo instalar la aplicación de portal de empresa e inscribirse  

- Si el dispositivo no es conforme, se muestra un mensaje que dirige al usuario al sitio Web del Portal de empresa de Intune o a la aplicación de Portal de empresa donde puede encontrar información sobre el problema y cómo resolverlo.  

- Para un equipo PC:  

    - Si la directiva está establecida para requerir unión a dominio y el equipo no está unido al dominio, se muestra un mensaje para ponerse en contacto con el Administrador de TI.  

    - Si la directiva está establecida para requerir unión a dominio o ser compatibles y el equipo no cumple estos requisitos, se muestra un mensaje con instrucciones sobre cómo instalar la aplicación de portal de empresa e inscribirse.  

El mensaje se muestra en el dispositivo para los usuarios de Exchange Online y los inquilinos en el nuevo entorno de Exchange Online dedicado, y se envía a la bandeja de entrada de correo electrónico de los usuarios de Exchange local y los dispositivos heredados dedicado de Exchange Online dedicados.  

> [!NOTE]  
> Las reglas de acceso condicional de Configuration Manager reemplazan, permiten, bloquean y ponen en cuarentena las reglas que se han definido en la consola de administración de Exchange Online.  
> 
> Debe configurar la directiva de acceso condicional en la consola de Intune. Los siguientes pasos comienzan accediendo a la consola de Intune a través de Configuration Manager. Si se le solicita, inicie sesión con las mismas credenciales que se usaron para configurar el punto de conexión de servicio entre Configuration Manager e Intune.  

##### <a name="to-enable-the-exchange-online-policy"></a>Para habilitar la directiva de Exchange Online  

1. En la consola de Configuration Manager, seleccione **activos y compatibilidad**.  

2. Expanda **configuración de cumplimiento**, expanda **acceso condicional**y, a continuación, seleccione **Exchange Online**.  

3. En el **inicio** ficha la **vínculos** grupo, seleccione **configurar Directiva de acceso condicional en la consola de Intune**. Probablemente tendrá que proporcionar el nombre de usuario y la contraseña de la cuenta que usó para conectar Configuration Manager con cualquier administrador global del servicio Intune. Se abre la consola de administración de Intune.  

4. En el portal de Microsoft Intune, seleccione **directiva** > **acceso condicional** > **directiva de Exchange Online**.  

    ![HybridOnlineSetupIntune](media/HybridOnlineSetupIntune.png)  

5. En la página **Directivas de Exchange Online** , seleccione **Habilitar directiva de acceso condicional para Exchange Online**. Si selecciona esta opción, el dispositivo debe ser conforme. Si no se activa esta característica no se aplica el acceso condicional.  

    > [!NOTE]  
    > Si aún no ha implementado una directiva de cumplimiento y, a continuación, habilite la directiva de Exchange Online, todos los dispositivos de destino se considerarán conformes.  
   >   
   >  Independientemente del estado de cumplimiento, todos los usuarios a los que se aplique la directiva deberán inscribir sus dispositivos en Intune.  

6. En **acceso a la aplicación**, para Outlook y otras aplicaciones que usan autenticación moderna, puede elegir restringir el acceso únicamente a dispositivos que son conformes para cada plataforma. Los dispositivos de Windows deben estar unidos a un dominio o estar inscritos en Intune y ser compatibles.  

    > [!TIP]  
    > **Autenticación moderna** proporciona el inicio de sesión basado en Active Directory Authentication Library (ADAL) a los clientes de Office.  
    > 
    > - La autenticación basada en ADAL permite a los clientes de Office realizar la autenticación basada en explorador (también conocida como autenticación pasiva). Para realizar la autenticación, se envía al usuario a una página web de inicio de sesión.  
    > - Este nuevo método de inicio de sesión permite nuevos escenarios, como el acceso condicional, según el **cumplimiento de los dispositivos** y si se realizó la **autenticación multifactor** .  
    > 
    >  Para más información, vea [Cómo funciona la autenticación moderna para las aplicaciones de cliente de Office 2013 y Office 2016](https://docs.microsoft.com/office365/enterprise/modern-auth-for-office-2013-and-2016).  

    Si usa Exchange Online con Configuration Manager e Intune, no solo podrá administrar dispositivos móviles con acceso condicional, sino que también podrá administrar equipos de escritorio. Los equipos deben estar unido al dominio o estar inscritos en Intune y ser compatibles. Puede establecer los requisitos siguientes:  

    - **Los dispositivos deben estar unidos a un dominio o ser conformes.** Los equipos deben estar unido al dominio o cumplir las directivas. Si un equipo no cumple alguno de estos requisitos, se solicita al usuario al inscribir el dispositivo con Intune.  

    - **Los dispositivos deben estar unidos a un dominio.** Los equipos deben estar unidos al dominio para tener acceso a Exchange Online. Si el equipo no unido al dominio, se bloquea el acceso al correo electrónico y el usuario deberá ponerse en contacto con el Administrador de TI.  

    - **Los dispositivos deben ser conformes.** Los equipos deben inscribirse en Intune y ser conformes. Si el equipo no está inscrito, se muestra un mensaje con instrucciones sobre cómo inscribirse.  

7. En **acceso web de Outlook (OWA)**, puede elegir permitir el acceso a Exchange Online solo a través de los exploradores admitidos: Safari (iOS) y Chrome (Android). Se bloqueará el acceso desde otros exploradores. Las mismas restricciones de plataforma que seleccionó para el acceso a las aplicaciones para Outlook también se aplica aquí.  

    - En los dispositivos **Android** , los usuarios tienen que habilitar el acceso de explorador. Para realizar esta acción, el usuario debe habilitar la opción "Habilitar acceso de explorador" en el dispositivo inscrito como sigue:  

        1. Abra la **aplicación del portal de empresa**.  

        2. Vaya a la página **Configuración** desde los tres puntos (...) o el botón de menú de hardware.  

        3. Presione el botón **Habilitar acceso al explorador** .  

        4. En el Explorador de Chrome, cierre sesión en Office 365 y reinicie Chrome.  

    - En **iOS y Android** plataformas, para identificar el dispositivo que se usa para tener acceso al servicio, Azure AD emitirá un certificado TLS para el dispositivo. El dispositivo muestra el certificado con un símbolo del sistema para el usuario para seleccionar el certificado, tal como se muestra en las capturas de pantalla siguiente. El usuario debe seleccionar este certificado para que pueden continuar usando el explorador.  

        - **iOS**  

        ![captura de pantalla de la solicitud de certificado en un ipad](media/mdm-browser-ca-ios-cert-prompt_v2.png)  

        - **Android**  

        ![captura de pantalla de la solicitud de certificado en un dispositivo Android](media/mdm-browser-ca-android-cert-prompt.png)  

8. En las**aplicaciones de correo Exchange ActiveSync**, puede bloquear el acceso del correo electrónico a Exchange Online si el dispositivo no cumple los requisitos y elegir si quiere permitir o bloquear el acceso al correo electrónico cuando Intune no pueda administrar el dispositivo.  

9. En **Grupos de destino**, seleccione los grupos de seguridad de Active Directory a los que se aplicará la directiva.  

    > [!NOTE]  
    > Para los usuarios que se encuentran en los grupos de destino, el de Intune reemplazarán las directivas y reglas de Exchange.  
    > 
    > Exchange solo aplicará sus directivas y sus reglas de permiso, bloqueo y cuarentena si:  
    > 
    > - El usuario no tiene licencia para Intune.  
    > - El usuario tiene licencia para Intune, pero el usuario no pertenece a los grupos de seguridad de destino de la directiva de acceso condicional.  

10. En **Grupos exentos**, seleccione los grupos de seguridad de Active Directory que se van a excluir de la directiva. Si un usuario está en los grupos de destino y exentos, que se van a excluir de la directiva y tendrán acceso al correo electrónico.  

11. Cuando termine, haga clic en **Guardar**.  


Revise las notas siguientes sobre esta directiva:  

- No tiene que implementar la directiva de acceso condicional; ya que surte efecto inmediatamente.  

- Cuando un usuario crea una cuenta de correo electrónico, el dispositivo se bloquea inmediatamente.  

- Si un usuario bloqueado inscribe el dispositivo con Intune (o corrige la no conformidad), el acceso al correo electrónico se desbloquea en dos minutos.  

- Si el usuario anula la inscripción del dispositivo, el correo electrónico se bloquea transcurridas unas 6 horas.  


### <a name="for-exchange-on-premises-and-tenants-in-the-legacy-exchange-online-dedicated-environment"></a>Para Exchange local (y los inquilinos del entorno heredado de Exchange Online dedicado)  
Las directivas de acceso condicional de Exchange local y los inquilinos del entorno heredado de Exchange Online dedicado utilizan el siguiente flujo para evaluar si se deben permitir o bloquear los dispositivos.  

![ConditionalAccess8 & #45; 2](media/ConditionalAccess8-2.png)  

#### <a name="to-enable-the-exchange-on-premises-policy"></a>Para habilitar la directiva de Exchange local  

1. En la consola de Configuration Manager, seleccione **activos y compatibilidad**.  

2. Expanda **configuración de cumplimiento**, expanda **acceso condicional**y, a continuación, seleccione **Exchange local**.  

3. En el **inicio** ficha la **Exchange local** grupo, seleccione **configurar Directiva de acceso condicional**.  

4. En el **General** página de la **Asistente para configurar directivas de acceso condicional**, especifique si desea invalidar la regla predeterminada de Exchange Active Sync. Seleccione esta opción si desea inscritos y tener acceso dispositivos conformes siempre tengan acceso al correo electrónico, incluso cuando la regla predeterminada se establece en cuarentena o bloquearlo.  

    > [!NOTE]  
    > Hay un problema con la invalidación predeterminada para dispositivos Android. Si se establece la regla de acceso predeterminada del servidor de Exchange en **Bloquear** y se habilita la directiva de acceso condicional de Exchange con la opción de invalidación de regla predeterminada, es posible que los dispositivos Android de los usuarios de destino no se desbloqueen incluso si son dispositivos inscritos y conformes con Intune. Para solucionar este problema, establezca la regla de acceso predeterminada de Exchange en **Cuarentena**. El dispositivo no obtiene acceso a Exchange de forma predeterminada, y el administrador puede obtener un informe desde el servidor de Exchange en la lista de dispositivos que se ponen en cuarentena.  

    Si no lo ha hecho programa de instalación de una cuenta de correo electrónico de notificación al configurar el conector de Exchange, verá una advertencia en esta página y el **siguiente** botón está deshabilitado.  Para continuar, debe configurar primero las opciones de correo electrónico de notificación en el conector de Exchange y, a continuación, volver al **Asistente de configuración de directivas de acceso condicional** para completar el proceso.  

     ![HybridCondAccessWiz1](media/HybridCondAccessWiz1.PNG)  

5. En la página **Colecciones objetivo** , agregue una o varias recopilaciones de usuarios. Para tener acceso a Exchange, los usuarios de estas recopilaciones deben inscribir sus dispositivos en Intune y también cumplir las directivas de cumplimiento que se han implementado.  

     ![HybridCondAccessWiz2](media/HybridCondAccessWiz2.PNG)  

6. En la página **Colecciones exentas** , agregue las recopilaciones de usuarios que desea excluir de la directiva de acceso condicional. Los usuarios de estos grupos, no necesitan inscribir sus dispositivos con Intune y es necesario cumplir las directivas de cumplimiento implementadas para tener acceso a Exchange.  

     ![HybridCondAccessWiz3](media/HybridCondAccessWiz3.png)  

    Si un usuario está incluido en listas objetivo y exentas, estarán exentos de la directiva de acceso condicional.  

7. En la página **Editar notificación de usuario**, configure el correo electrónico que Intune envía a los usuarios con instrucciones sobre cómo desbloquear el dispositivo (además del correo electrónico que envía Exchange).  

    Puede modificar el mensaje predeterminado y usar etiquetas HTML para formatear el aspecto del texto. Asimismo, también puede enviar de antemano un correo electrónico a los empleados, para informarles sobre los próximos cambios y enviarles instrucciones acerca de cómo inscribir sus dispositivos.  

     ![HybridCondAccessWiz4](media/HybridCondAccessWiz4.PNG)  

    > [!NOTE]  
    > Dado que el correo electrónico de notificación de Intune que contiene instrucciones de corrección se envía al buzón de Exchange del usuario, en caso de que el dispositivo del usuario se bloquee antes de recibir el mensaje de correo electrónico, puede usar un dispositivo desbloqueado u otro método para acceder a Exchange y ver el mensaje.  
    > 
    > Para que Exchange pueda enviar el correo electrónico de notificación, configurar la cuenta que se usará para enviar el correo electrónico de notificación. Puede hacerlo cuando configure las propiedades del conector de Exchange Server.  
    >   
    > Para obtener más información, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  

8. En el **resumen** , revise la configuración y, a continuación, complete el asistente.  


Revise las notas siguientes sobre esta directiva:  

- No es necesario implementar la directiva de acceso condicional, ya que surte efecto inmediatamente.  

- Después de que un usuario configure un perfil de Exchange ActiveSync, tardará uno a tres horas en bloquearse (si no está administrado por Intune) el dispositivo.  

- Si un usuario bloqueado luego inscribe el dispositivo con Intune (o corrige la no conformidad), acceso al correo electrónico se desbloqueará en dos minutos.  

- Si el usuario anula-inscripción de Intune puede tardar uno a tres horas en bloquear el dispositivo.  


## <a name="see-also"></a>Consulte también  

[Administrar el acceso a servicios](/sccm/protect/deploy-use/manage-access-to-services)
