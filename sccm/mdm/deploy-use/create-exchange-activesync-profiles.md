---
title: "Crear perfiles de correo electrónico de Exchange ActiveSync | Microsoft Docs"
description: "Obtenga información sobre cómo crear y configurar perfiles de correo electrónico en System Center Configuration Manager que funcionen con Microsoft Intune."
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
caps.latest.revision: 4
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: aa8924a013ebdbee888cab33001fddbe7ad2d67e
ms.openlocfilehash: a0353c49360cd99bc92b4546e12a52c3d13d1d14
ms.lasthandoff: 03/30/2017


---

# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Perfiles de correo electrónico de Exchange ActiveSync en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los perfiles de correo electrónico funcionan con Microsoft Intune para permitirle aprovisionar dispositivos con perfiles de correo electrónico y restricciones mediante Exchange ActiveSync. Así, los usuarios pueden acceder al correo electrónico corporativo desde sus dispositivos con solo realizar una mínima configuración por su parte.  

 Puede configurar los siguientes tipos de dispositivo con los perfiles de correo electrónico:  

- Windows 10
- Windows Phone 8.1
- Windows Phone 8.0
- iPhone que ejecuta iOS 5, iOS 6, iOS 7 y iOS 8  
- iPad que ejecuta iOS 5, iOS 6, iOS 7 y iOS 8  
- Samsung KNOX Standard (4 y posterior)
- Android for Work

Para implementar los perfiles de correo electrónico en los dispositivos, deben inscribirse en Intune. Para obtener información sobre cómo inscribir dispositivos, consulte [Administrar dispositivos móviles con Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).

>[!NOTE]
>Intune proporciona dos perfiles de correo electrónico de Android for Work, uno para cada una de las aplicaciones de correo electrónico, que son Gmail y Nine Work. Estas aplicaciones están disponibles en Google Play Store y admiten conexiones a Exchange. Para habilitar la conectividad de correo electrónico, implementar una de estas aplicaciones de correo electrónico en dispositivos de los usuarios y después crear e implementar el perfil adecuado. Las aplicaciones de correo electrónico como Nine Work pueden no ser gratuitas. Revise los detalles de licencias de la aplicación o póngase en contacto con la empresa de la aplicación para plantear cualquier pregunta.

 Además de configurar una cuenta de correo electrónico en el dispositivo, también puede configurar las opciones de sincronización de contactos, calendarios y tareas.  

 Al crear un perfil de correo electrónico, puede incluir una amplia gama de opciones de seguridad, como los certificados para identidad, cifrado y firma aprovisionados mediante perfiles de certificado de System Center Configuration Manager. Para obtener más información sobre los perfiles de certificado, consulte [Certificate profiles in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles) (Perfiles de certificado en Configuration Manager).    

## <a name="create-a-new-exchange-activesync-email-profile"></a>Crear un perfil de correo electrónico de Exchange ActiveSync  

Iniciar el Asistente para crear perfiles de correo electrónico de Exchange ActiveSync  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , expanda **Configuración de cumplimiento**y **Acceso a los recursos de la compañía**y, a continuación, haga clic en **Perfiles de correo electrónico**.  

3.  En el grupo **Crear** de la pestaña **Inicio**, haga clic en **Crear perfil de correo electrónico de Exchange ActiveSync**.
4.  En la página General del asistente, configure lo siguiente:
    - **Nombre**: proporcione un nombre descriptivo para el perfil de correo electrónico.
    - **Descripción**: si lo desea, escriba una descripción para el perfil de correo electrónico que facilite su identificación en la consola de Configuration Manager.
    - **Este perfil de correo electrónico es para Android for Work**: seleccione esta opción si solo va a implementar este perfil de correo electrónico en dispositivos Android for Work. Si activa esta casilla, la página del asistente **Plataformas admitidas** no se muestra. Solo se configuran los perfiles de correo electrónico de Android for Work.
4.  Especifique la siguiente información en la página **Exchange ActiveSync** del Asistente para crear perfiles de correo electrónico de Exchange ActiveSync:  

    -   **Host de Exchange ActiveSync:** especifique el nombre de host de Exchange Server de su compañía que hospeda los servicios de Exchange ActiveSync.  

    -   **Nombre de cuenta:** escriba el nombre para mostrar de la cuenta de correo electrónico tal y como se va a mostrar a los usuarios en sus dispositivos.  

    -   **Nombre de usuario de la cuenta:** seleccione cómo se va a configurar el nombre de usuario de la cuenta de correo electrónico en los dispositivos cliente. Puede seleccionar una de las siguientes opciones de la lista desplegable:  

        -   **Nombre principal de usuario** Se usa el nombre principal de usuario completo para iniciar sesión en Exchange.  

        -   **AccountName** Se usa el nombre de cuenta de usuario completo de Active Directory.

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
        >  Para poder seleccionar un certificado de identidad, antes hay que configurar un perfil de certificado de Protocolo de inscripción de certificados simple (SCEP). Para obtener más información sobre los perfiles de certificado, consulte [Certificate profiles in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles) (Perfiles de certificado en Configuration Manager).  

         Esta opción está disponible únicamente si ha seleccionado **Certificados** en **Método de autenticación**.  

    -   **Usar S/MIME** (solo para dispositivos iOS) El correo electrónico saliente se envía mediante cifrado S/MIME. Elija entre las siguientes opciones:


        -   **Certificados de cifrado:** haga clic en **Seleccionar** y, después, seleccione el certificado que se va a usar para el cifrado. Esta opción es válida únicamente en dispositivos iOS. Solo puede seleccionar un certificado PFX que se usará como un certificado de cifrado.

        Si selecciona un certificado de cifrado y un certificado de firma, ambos deben tener el formato PFX.

        > [!NOTE]  
        >  Para poder seleccionar certificados, antes hay que configurarlos como un perfil de certificado PFX o de Protocolo de inscripción de certificados simple (SCEP). Para obtener más información sobre los perfiles de certificado, consulte [Certificate profiles in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles) (Perfiles de certificado en Configuration Manager).  




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

Para obtener más información sobre cómo implementar perfiles de correo electrónico de Exchange ActiveSync, consulte [How to deploy profiles in System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) (Cómo implementar perfiles en System Center Configuration Manager).  

