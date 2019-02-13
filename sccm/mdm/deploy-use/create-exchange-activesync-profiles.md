---
title: Creación de perfiles de correo electrónico de Exchange ActiveSync
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo crear y configurar perfiles de correo electrónico en System Center Configuration Manager que funcionen con Microsoft Intune.
ms.date: 07/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3bf178465f5aff508daca1d87b1b548a42db931d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139279"
---
# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Perfiles de correo electrónico de Exchange ActiveSync en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Al usar Microsoft Intune y Exchange ActiveSync, puede configurar dispositivos con restricciones y perfiles de correo electrónico. Así, los usuarios pueden acceder a los correos electrónicos corporativos desde sus dispositivos con un trabajo de configuración mínimo por su parte.  

 Puede configurar los siguientes tipos de dispositivo con los perfiles de correo electrónico:  

- Windows 10
- Windows Phone 8.1
- Dispositivos iPhone con iOS 9 y versiones posteriores 
- Dispositivos iPad con iOS 9 y versiones posteriores 
- Samsung KNOX Standard (4 y posterior)
- Android for Work

Para implementar los perfiles de correo electrónico en los dispositivos, debe inscribirlos en Intune. Para obtener información sobre cómo inscribir dispositivos, consulte [Administrar dispositivos móviles con Microsoft Intune](https://technet.microsoft.com/library/dn646962.aspx).

> [!NOTE]
> Intune proporciona dos perfiles de correo electrónico de Android for Work, uno para cada una de las aplicaciones de correo electrónico, que son Gmail y Nine Work. Estas aplicaciones están disponibles en Google Play Store y admiten conexiones a Exchange. Para habilitar la conectividad de correo electrónico, implementar una de estas aplicaciones de correo electrónico en dispositivos de los usuarios y después crear e implementar el perfil adecuado. Es posible que las aplicaciones de correo electrónico como Nine Work no sean gratuitas. Revise los detalles de licencias de la aplicación o póngase en contacto con la empresa de la aplicación para plantear cualquier pregunta.

 Además de configurar una cuenta de correo electrónico en el dispositivo, también puede configurar opciones de sincronización de contactos, calendarios y tareas.  

 Cuando cree un perfil de correo electrónico, puede incluir una amplia gama de opciones de seguridad. Estas opciones incluyen certificados para la identidad, el cifrado y la firma que se han configurado mediante de perfiles de certificado de System Center Configuration Manager. Para obtener más información sobre los perfiles de certificado, consulte [Certificate profiles in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles.md) (Perfiles de certificado en Configuration Manager).    

## <a name="create-an-exchange-activesync-email-profile"></a>Creación de un perfil de correo electrónico de Exchange ActiveSync  

Para crear un perfil, use el Asistente para crear perfiles de correo electrónico de Exchange ActiveSync. 

1. En la consola de Configuration Manager, elija **Activos y compatibilidad**.  

2. En el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y **Acceso a los recursos de la compañía** y, a continuación, elija **Perfiles de correo electrónico**.  

3. En el grupo **Crear** de la pestaña **Inicio**, elija **Crear perfil de correo electrónico de Exchange ActiveSync** para iniciar el asistente.

4. En la página **General** del asistente, configure lo siguiente:

   - **Nombre**. Proporcione un nombre descriptivo para el perfil de correo electrónico.

   - **Descripción**. Si quiere, escriba una descripción para el perfil de correo electrónico que facilite su identificación en la consola de Configuration Manager.

   - **Este perfil de correo electrónico es para Android for Work**. Elija esta opción si va a implementar este perfil de correo electrónico solo en dispositivos Android for Work. Si activa esta casilla, no se muestra la página del asistente **Plataformas admitidas**. Solo se configuran los perfiles de correo electrónico de Android for Work.

5. En la página **Exchange ActiveSync** del asistente, especifique la información siguiente:  

   - **Host de Exchange ActiveSync**. Especifique el nombre de host del servidor de Exchange Server de su empresa que hospeda los servicios de Exchange ActiveSync.  

   - **Nombre de cuenta**. Especifique el nombre para mostrar de la cuenta de correo electrónico tal y como se mostrará para los usuarios en sus dispositivos.  

   - **Nombre de usuario de la cuenta**. Elija cómo se configura el nombre de usuario de la cuenta de correo electrónico en los dispositivos cliente. Puede elegir una de las siguientes opciones de la lista desplegable:  

     -   **Nombre principal de usuario**. Use el nombre principal de usuario completo para iniciar sesión en Exchange.  

     -   **AccountName**. Use el nombre de cuenta de usuario completo de Active Directory.

     -   **Dirección SMTP principal**. Use la dirección SMTP principal del usuario para iniciar sesión en Exchange.  

   - **Dirección de correo electrónico**. Elija cómo se genera la dirección de correo electrónico para el usuario en cada dispositivo cliente. Puede elegir una de las siguientes opciones de la lista desplegable:  

     -   **Dirección SMTP principal**. Use la dirección SMTP principal del usuario para iniciar sesión en Exchange.  

     -   **Nombre principal de usuario**. Use el nombre principal de usuario completo como dirección de correo electrónico.  

   - **Dominio de cuenta**. Elija una de las siguientes opciones:  

     - **Obtener desde Active Directory**  

     - **Personalizado**  

       Este campo solo es aplicable si se ha seleccionado **sAMAccountName** en la lista desplegable **Nombre de usuario de la cuenta**.  

   - **Método de autenticación**. elija uno de los siguientes métodos de autenticación para autenticar la conexión a Exchange ActiveSync:  

     -   **Certificados**. Se usará un certificado de identidad para autenticar la conexión de Exchange ActiveSync.  

     -   **Nombre de usuario y contraseña**. El usuario del dispositivo debe proporcionar una contraseña para conectarse a Exchange ActiveSync. (El nombre de usuario está configurado como parte del perfil de correo electrónico).  

   - **Certificado de identidad**. Elija **Seleccionar** y, después, elija un certificado para usarlo para la identidad.  

      Los certificados de identidad deben ser SCEP; no se pueden usar certificados PFX.  Para obtener más información, consulte [Perfiles de certificado en System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

      Esta opción está disponible únicamente si ha elegido **Certificados** en **Método de autenticación**.  

   - **Utilizar S/MIME**. Envíe correos electrónicos salientes mediante cifrado S/MIME. Esta opción es válida únicamente en dispositivos iOS. Elija entre las siguientes opciones:

     - **Certificados de firma**.  Elija **Seleccionar** y, después, seleccione un perfil de certificado para usarlo con fines de cifrado.  

       El perfil puede ser un certificado SCEP o PFX.  Sin embargo, si se usan la firma y el cifrado, debe seleccionar los perfiles de certificado PFX para *ambos*.

     - **Certificados de cifrado**. Elija **Seleccionar** y, después, elija un certificado para usarlo para el cifrado. Solo puede elegir un certificado PFX que se usará como un certificado de cifrado.

     - Para cifrar todos los mensajes de correo electrónico en dispositivos iOS, active la casilla **Requerir cifrado**.    

       Debe crear perfiles de certificado antes de elegirlos en esta pantalla.  Para obtener más información, consulte [Perfiles de certificado en System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

## <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>Configuración de la sincronización para el perfil de correo electrónico de Exchange ActiveSync  

Especifique la siguiente información en la página **Configurar sincronización** del Asistente para crear perfiles de correo electrónico de Exchange ActiveSync:  

-   **Programación**. Elija la programación con la que los dispositivos sincronizarán los datos de Exchange Server. Esta opción es válida únicamente en dispositivos Windows Phone. Elija de entre las siguientes opciones:  

    -   **No configurado**. No hay ninguna programación de sincronización en vigor. Esto permite que los usuarios puedan configurar su propia programación de sincronización.  

    -   **Conforme lleguen mensajes**. Los datos, como los mensajes de correo electrónico y los elementos de calendario, se sincronizarán automáticamente cuando vayan llegando.  

    -   **15 minutos**. Los datos, como los mensajes de correo electrónico y los elementos de calendario, se sincronizarán automáticamente cada 15 minutos.  

    -   **30 minutos**. Los datos, como los mensajes de correo electrónico y los elementos de calendario, se sincronizarán automáticamente cada 30 minutos.  

    -   **60 minutos**. Los datos, como los mensajes de correo electrónico y los elementos de calendario, se sincronizarán automáticamente cada 60 minutos.  

    -   **Manual**. El usuario del dispositivo debe iniciar manualmente la sincronización.  

-   **Número de días para sincronizar el correo electrónico**. En la lista desplegable, elija el número de días de correo electrónico que quiere sincronizar. Elija uno de los siguientes valores:  

    -   **No configurado**. La configuración no tiene efecto. Esto permite que los usuarios puedan configurar la cantidad de correos electrónicos que se descargan en su dispositivo.  

    -   **Ilimitado**. Se sincronizan todos los correos electrónicos disponibles.  

    -   **1 día**  

    -   **3 días**  

    -   **1 semana**  

    -   **2 semanas**  

    -   **1 mes**  

-   **Permitir que los mensajes se muevan a otras cuentas de correo electrónico**. Elija esta opción para permitir a los usuarios mover los mensajes de correo electrónico entre las distintas cuentas que han configurado en su dispositivo. Esta opción es válida únicamente en dispositivos iOS.  

-   **Permitir que se envíe correo electrónico desde aplicaciones de terceros**. Elija esta opción para permitir que los usuarios envíen correos electrónicos desde algunas aplicaciones de correo electrónico no predeterminadas de terceros. Esta opción es válida únicamente en dispositivos iOS.  

-   **Sincronizar las direcciones de correo electrónico usadas recientemente**. Elija esta opción para sincronizar la lista de direcciones de correo electrónico que se han utilizado recientemente en el dispositivo. Esta opción es válida únicamente en dispositivos iOS.  

-   **Usar SSL**. Elija esta opción para usar la comunicación de Capa de sockets seguros (SSL) al enviar y recibir correos electrónicos y comunicarse con Exchange Server.  

-   **Tipo de contenido para sincronizar**. Elija los tipos de contenido que quiere sincronizar con los dispositivos. Esta opción es válida únicamente en dispositivos Windows Phone. Elija de entre las siguientes opciones:  

    -   **Correo electrónico**  

    -   **Contactos**  

    -   **Calendarioio**  

    -   **Tareas**  

## <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>Especificar las plataformas admitidas para el perfil de correo electrónico de Exchange ActiveSync  

1.  En la página **Plataformas admitidas** del Asistente para crear perfiles de correo electrónico de Exchange ActiveSync, elija los sistemas operativos en los que se instalará el perfil de correo electrónico. También puede hacer clic en **Seleccionar todo** para instalar el perfil de correo electrónico en todos los sistemas operativos disponibles.  

2.  Finalice el asistente.

Para obtener más información sobre cómo implementar perfiles de correo electrónico de Exchange ActiveSync, consulte [How to deploy profiles in System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) (Cómo implementar perfiles en System Center Configuration Manager).  
