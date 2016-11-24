---
title: "Crear perfiles de correo electrónico de Exchange ActiveSync | System Center Configuration Manager"
description: "Obtenga información sobre cómo crear y configurar perfiles de correo electrónico en System Center Configuration Manager que funcionen con Microsoft Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 15f0fd50-e196-44e5-b435-234d7ff6a5cd
caps.latest.revision: 4
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 613ed15742322e2eb90eec3c9f493e3b1755d93a


---

# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Perfiles de correo electrónico de Exchange ActiveSync en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los perfiles de correo electrónico funcionan con Microsoft Intune para permitirle aprovisionar dispositivos con perfiles de correo electrónico y restricciones mediante Exchange ActiveSync. Así, los usuarios pueden acceder al correo electrónico corporativo desde sus dispositivos con solo realizar una mínima configuración por su parte.  

 Puede configurar los siguientes tipos de dispositivo con los perfiles de correo electrónico:  

-   Dispositivos que ejecutan Windows Phone 8  

-   Dispositivos que ejecutan Windows Phone 8.1  

-   Dispositivos que ejecutan Windows 10 Mobile  

-   Dispositivos iPhone que ejecutan iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos iPad que ejecutan iOS 5, iOS 6, iOS 7 e iOS 8  

> [!IMPORTANT]  
>  Para implementar perfiles en dispositivos iOS, Android Samsung KNOX, Windows Phone, Windows 8.1 o Windows 10, estos dispositivos se deben inscribir en Intune. Para obtener información sobre cómo inscribir dispositivos, consulte [Administrar dispositivos móviles con Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 Además de configurar una cuenta de correo electrónico en el dispositivo, también puede configurar las opciones de sincronización de contactos, calendarios y tareas.  

 Al crear un perfil de correo electrónico, puede incluir una amplia gama de opciones de seguridad, como los certificados para identidad, cifrado y firma aprovisionados mediante perfiles de certificado de System Center Configuration Manager. Para obtener más información sobre los perfiles de certificado, consulte [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Perfiles de certificado en Configuration Manager).    


## <a name="create-a-new-exchange-activesync-email-profile"></a>Crear un perfil de correo electrónico de Exchange ActiveSync  

Iniciar el Asistente para crear perfiles de correo electrónico de Exchange ActiveSync  

1.  En la consola de System Center Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , expanda **Configuración de cumplimiento**y **Acceso a los recursos de la compañía**y, a continuación, haga clic en **Perfiles de correo electrónico**.  

3.  En el grupo **Crear** de la pestaña **Inicio** , haga clic en **Crear perfil de Exchange ActiveSync**. 

4.  Siga las instrucciones del asistente.   

### <a name="to-configure-exchange-activesync-settings-for-the-exchange-activesync-email-profile"></a>Para configurar Exchange ActiveSync para el perfil de correo electrónico de Exchange ActiveSync  

1.  Especifique la siguiente información en la página **Exchange ActiveSync** del Asistente para crear perfiles de correo electrónico de Exchange ActiveSync:  

    -   **Host de Exchange ActiveSync:** especifique el nombre de host de Exchange Server de su compañía que hospeda los servicios de Exchange ActiveSync.  

    -   **Nombre de cuenta:** escriba el nombre para mostrar de la cuenta de correo electrónico tal y como se va a mostrar a los usuarios en sus dispositivos.  

    -   **Nombre de usuario de la cuenta:** seleccione cómo se va a configurar el nombre de usuario de la cuenta de correo electrónico en los dispositivos cliente. Puede seleccionar una de las siguientes opciones de la lista desplegable:  

        -   **Nombre principal de usuario** Se usa el nombre principal de usuario completo para iniciar sesión en Exchange.  

        -   **sAMAccountName** Se usa  

        -   **Dirección SMTP principal** Se usa la dirección SMTP principal de los usuarios para iniciar sesión en Exchange.  

    -   **Dirección de correo electrónico:** seleccione cómo se genera la dirección de correo electrónico para el usuario en cada dispositivo cliente. Puede seleccionar una de las siguientes opciones de la lista desplegable:  

        -   **Dirección SMTP principal** Se usa la dirección SMTP principal de los usuarios para iniciar sesión en Exchange.  

        -   **Nombre principal de usuario** Se usa el nombre principal de usuario completo como dirección de correo electrónico.  

    -   **Dominio de cuenta:** elija una de las siguientes opciones:  

        -   **Obtener desde Active Directory**  

        -   **Personalizado**  

         Este campo solo es aplicable si se ha seleccionado **sAMAccountName** en la lista desplegable **Nombre de usuario de la cuenta** .  

    -   **Método de autenticación:** elija uno de los siguientes métodos de autenticación para autenticar la conexión a Exchange ActiveSync:  

        -   **Certificados** Se usará un certificado de identidad para autenticar la conexión de Exchange ActiveSync.  

        -   **Nombre de usuario y contraseña** El usuario del dispositivo debe proporcionar una contraseña para conectarse a Exchange ActiveSync (el nombre de usuario está configurado como parte del perfil de correo electrónico).  

    -   **Certificado de identidad:** haga clic en **Seleccionar** y, después, seleccione el certificado que se va a usar para la identidad.  

        > [!NOTE]  
        >  Para poder seleccionar un certificado de identidad, antes hay que configurar un perfil de certificado de Protocolo de inscripción de certificados simple (SCEP). Para obtener más información sobre los perfiles de certificado, consulte [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Perfiles de certificado en Configuration Manager).  

         Esta opción está disponible únicamente si ha seleccionado **Certificados** en **Método de autenticación**.  

    -   **Usar S/MIME** El correo electrónico saliente se envía mediante cifrado S/MIME. Esta opción es válida únicamente en dispositivos iOS.  

    -   **Certificados de cifrado:** haga clic en **Seleccionar** y, después, seleccione el certificado que se va a usar para el cifrado. Esta opción es válida únicamente en dispositivos iOS.  

        > [!NOTE]  
        >  Para poder seleccionar un certificado de cifrado, antes hay que configurar un perfil de certificado de Protocolo de inscripción de certificados simple (SCEP). Para obtener más información sobre los perfiles de certificado, consulte [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Perfiles de certificado en Configuration Manager).  

         Esta opción está disponible únicamente si ha seleccionado **Usar S/MIME**.  

    -   **Certificados de firma:** haga clic en **Seleccionar** y, después, seleccione el certificado que se va a usar para la firma. Esta opción es válida únicamente en dispositivos iOS.  

        > [!NOTE]  
        >  Para poder seleccionar un certificado de firma, antes hay que configurar un perfil de certificado de Protocolo de inscripción de certificados simple (SCEP). Para obtener más información sobre los perfiles de certificado, consulte [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Perfiles de certificado en Configuration Manager).  

         Esta opción está disponible únicamente si ha seleccionado **Usar S/MIME**.  

###   <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>configurar la sincronización para el perfil de correo electrónico de Exchange ActiveSync.  

1.  Especifique la siguiente información en la página **Configurar sincronización** del Asistente para crear perfiles de correo electrónico de Exchange ActiveSync:  

    -   **Programación:** seleccione la programación por la que los dispositivos sincronizarán los datos de Exchange Server. Esta opción es válida únicamente en dispositivos Windows Phone. Elija de entre las siguientes opciones:  

        -   **No configurado** No hay ninguna programación de sincronización en vigor. Esto permite que los usuarios puedan configurar su propia programación de sincronización.  

        -   **Conforme lleguen mensajes** Los datos como los mensajes de correo electrónico y los elementos de calendario se sincronizarán automáticamente cuando vayan llegando.  

        -   **15 minutos** Los datos como los mensajes de correo electrónico y los elementos de calendario se sincronizarán automáticamente cada 15 minutos.  

        -   **30 minutos** Los datos como los mensajes de correo electrónico y los elementos de calendario se sincronizarán automáticamente cada 30 minutos.  

        -   **60 minutos** Los datos como los mensajes de correo electrónico y los elementos de calendario se sincronizarán automáticamente cada 60 minutos.  

        -   **Manual** El usuario del dispositivo deberá iniciar manualmente la sincronización.  

    -   **Número de días de correo electrónico para sincronizar:** En la lista desplegable, seleccione el número de días de correo electrónico que quiere sincronizar. Elija uno de los siguientes valores:  

        -   **No configurado** La configuración no tiene efecto. Esto permite que los usuarios puedan configurar la cantidad de correo electrónico que se descarga en su dispositivo.  

        -   **Ilimitado** Se sincroniza todo el correo electrónico disponible.  

        -   **1 día**  

        -   **3 días**  

        -   **1 semana**  

        -   **2 semanas**  

        -   **1 mes**  

    -   **Permitir que los mensajes se muevan a otras cuentas de correo electrónico** Seleccione esta opción para permitir a los usuarios mover mensajes de correo electrónico entre distintas cuentas que tengan configuradas en su dispositivo. Esta opción es válida únicamente en dispositivos iOS.  

    -   **Permitir el envío de correo electrónico desde aplicaciones de otros fabricantes** Seleccione esta opción para permitir a los usuarios enviar correo electrónico desde algunas aplicaciones de correo electrónico no predeterminadas de otros fabricantes. Esta opción es válida únicamente en dispositivos iOS.  

    -   **Sincronizar direcciones de correo electrónico usadas recientemente** Seleccione esta opción para sincronizar la lista de direcciones de correo electrónico que se ha usado recientemente en el dispositivo. Esta opción es válida únicamente en dispositivos iOS.  

    -   **Usar SSL** Seleccione esta opción para usar la comunicación de Capa de sockets seguros (SSL) al enviar y recibir correo electrónico y comunicarse con el servidor de Exchange.  

    -   **Tipo de contenido para sincronizar:** seleccione los tipos de contenido que quiere sincronizar con los dispositivos. Esta opción es válida únicamente en dispositivos Windows Phone. Elija de entre las siguientes opciones:  

        -   **Correo electrónico**  

        -   **Contactos**  

        -   **Calendarioio**  

        -   **Tareas**  

###  <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>especificar las plataformas admitidas para el perfil de correo electrónico de Exchange ActiveSync.  
 
1.  En la página **Plataformas admitidas** del Asistente para crear perfiles de correo electrónico de Exchange ActiveSync, seleccione los sistemas operativos en los que se va a instalar el perfil de correo electrónico o haga clic en **Seleccionar todo** para instalarlo en todos los sistemas operativos disponibles.  

2.  Complete el asistente.

Para obtener más información sobre cómo implementar perfiles de correo electrónico de Exchange ActiveSync, consulte [How to deploy profiles in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md) (Cómo implementar perfiles en System Center Configuration Manager).  



<!--HONumber=Nov16_HO1-->


