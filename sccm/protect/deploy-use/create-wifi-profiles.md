---
title: Perfiles de Wi-Fi | System Center Configuration Manager
description: "Aprenda a usar perfiles de Wi-Fi en System Center Configuration Manager para implementar la configuración de red inalámbrica para los usuarios de su organización."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
caps.latest.revision: 13
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 295ccc2ce7c1dae55c45113cc8ff826e30f7079a


---
# <a name="how-to-create-wi-fi-profiles-in-system-center-configuration-manager"></a>Cómo crear perfiles de Wi-Fi en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


Use perfiles de Wi-Fi en System Center Configuration Manager para implementar la configuración de red inalámbrica para los usuarios de su organización. Al implementar estas opciones, les resultará más fácil a los usuarios conectarse a la Wi-Fi.  

 Por ejemplo, ha instalado una nueva red Wi-Fi denominada **Contoso Wi-Fi**. Quiere aprovisionar todos los dispositivos que ejecutan el sistema operativo iOS con la configuración necesaria para conectarse a esta red. Puede crear un perfil de Wi-Fi que contiene la configuración necesaria para conectarse a la red inalámbrica **Contoso Wi-Fi** . Después, puede implementar este perfil para todos los usuarios que tienen dispositivos que ejecutan iOS. Los usuarios de dispositivos iOS ven la red de la compañía en la lista de redes inalámbricas y pueden conectarse fácilmente a esta red.  

 Puede configurar los siguientes tipos de dispositivos con perfiles de Wi-Fi:  

-   Dispositivos con Windows 8.1 de 32 bits  

-   Dispositivos con Windows 8.1 de 64 bits  

-   dispositivos con Windows RT 8.1  

-   Dispositivos con Windows Phone 8.1  

-   Dispositivos con Windows 10 Desktop o Mobile  

-   Dispositivos IPhone con iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos IPad con iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos Android con la versión 4  

> [!IMPORTANT]  
>  Para implementar perfiles en dispositivos Android, iOS, Windows Phone y Windows 8.1 o posterior inscritos, estos dispositivos deben inscribirse en Microsoft Intune. Para obtener información sobre cómo inscribir dispositivos, consulte [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune) (Inscribir dispositivos para la administración en Intune).  

 Cuando se crea un perfil de Wi-Fi, puede incluir una amplia gama de opciones de seguridad. Estas incluyen certificados para la validación de servidor y la autenticación de cliente que se han aprovisionado mediante perfiles de certificado de Configuration Manager. Para obtener más información sobre los perfiles de certificado, consulte [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Perfiles de certificado en System Center Configuration Manager).  

## <a name="steps-to-create-a-wi-fi-profile"></a>Pasos para crear un perfil de Wi-Fi  
 Utilice los pasos siguientes para crear un perfil de Wi-Fi mediante el **Asistente para crear perfil de Wi-Fi**.  

-   [Paso 1: iniciar el Asistente para crear perfil de Wi-Fi](#BKMK_Step1)  

-   [Paso 2: proporcionar información general sobre el perfil de Wi-Fi](#BKMK_Step2)  

-   [Paso 3: proporcionar información sobre la red inalámbrica](#BKMK_Step3)  

-   [Paso 4: configurar la seguridad para el perfil de Wi-Fi](#BKMK_Step4)  

-   [Paso 5: configurar opciones avanzadas del perfil de Wi-Fi](#BKMK_Step5)  

-   [Paso 6: configurar el proxy para el perfil de Wi-Fi](#BKMK_Step6)  

-   [Paso 7: configurar las plataformas admitidas para el perfil de Wi-Fi](#BKMK_Step7)  

-   [Paso 8: Completar el asistente](#BKMK_Step8)  

##  <a name="a-namebkmkstep1a-step-1-start-the-create-wi-fi-profile-wizard"></a><a name="BKMK_Step1"></a> Paso 1: Iniciar el Asistente para crear perfil de Wi-Fi  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , expanda **Configuración de cumplimiento**, expanda **Acceso a los recursos de la compañía**y, a continuación, haga clic en **Perfiles de Wi-Fi**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear perfil de Wi-Fi**.  

##  <a name="a-namebkmkstep2a-step-2-provide-general-information-about-the-wi-fi-profile"></a><a name="BKMK_Step2"></a> Paso 2: Proporcionar información general sobre el perfil de Wi-Fi  

1.  En la página **General** del Asistente para crear perfil de Wi-Fi, escriba un nombre único y una descripción para el perfil de Wi-Fi. Puede utilizar un máximo de 256 caracteres.  

2.  Si desea usar la configuración de otro perfil de Wi-Fi, seleccione **Importar un elemento de perfil de Wi-Fi existente desde un archivo**.  

    > [!IMPORTANT]  
    >  Asegúrese de que el perfil de Wi-Fi que desea importar contiene XML válido para un perfil de Wi-Fi. Configuration Manager no valida el perfil al importar el archivo.  

3.  En  
                            **Gravedad de la falta de compatibilidad de los informes**: especifique el nivel de gravedad que se notificará si el perfil de Wi-Fi no es compatible con los dispositivos cliente (por ejemplo, si se produce un error en la instalación del perfil). Los niveles de gravedad disponibles son los siguientes:  

    -   **Ninguno**: los equipos que no cumplan esta regla de compatibilidad no notificarán ninguna gravedad de error en los informes de Configuration Manager.  

    -   **Información**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Información** en los informes de Configuration Manager.  

    -   **Advertencia**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Advertencia** en los informes de Configuration Manager.  

    -   **Crítico**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager.  

    -   **Crítico con evento**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager. Este nivel de gravedad también se registra como evento de Windows en el registro de eventos de la aplicación.  

##  <a name="a-namebkmkstep3a-step-3-provide-information-about-the-wireless-network"></a><a name="BKMK_Step3"></a> Paso 3: Proporcionar información sobre la red inalámbrica  

1.  En la página **perfil de Wi-Fi** del Asistente para crear perfil de Wi-Fi, especifique el nombre descriptivo para la conexión a Internet inalámbrica con un máximo de 32 caracteres. Este es el nombre que los dispositivos mostrarán como nombre de red.  

    > [!IMPORTANT]  
    >  Configuration Manager no admite el uso de los caracteres apóstrofo (**â€˜**) o coma (**,**) en el nombre de red.  

2.  En **SSID**, especifique el nombre (SSID) de la red inalámbrica a la que quiere que puedan conectarse los dispositivos. Puede usar un máximo de 32 caracteres. El nombre de SSID distingue mayúsculas de minúsculas, así que asegúrese de escribirlo exactamente tal y como está configurado.  

3.  Si quiere permitir que los dispositivos se vuelvan a conectar automáticamente a la red inalámbrica cuando esta esté dentro del alcance, seleccione **Conectarse automáticamente cuando esta red esté dentro del alcance**.  

4.  Si quiere permitir que los dispositivos sigan buscando otras redes inalámbricas cuando están conectados a esta red, seleccione  
                            **Buscar otras redes inalámbricas mientras se esté conectado a esta red**.  

5.  Si quiere permitir que los dispositivos se conecten a la red cuando no esté visible en la lista de redes (porque está oculta y no se difunde su nombre), seleccione **Conectarse cuando la red no esté difundiendo su nombre (SSID)**,  

##  <a name="a-namebkmkstep4a-step-4-configure-security-for-the-wi-fi-profile"></a><a name="BKMK_Step4"></a> Paso 4: Configurar la seguridad para el perfil de Wi-Fi  

> [!IMPORTANT]  
>  Si va a crear un perfil de Wi-Fi para la Administración de dispositivos móviles local, la rama actual de Configuration Manager solo admite las siguientes configuraciones de seguridad de Wi-Fi:  
>   
>  Tipos de seguridad: **WPA2 Enterprise** o **WPA2 Personal**  
> Tipos de cifrado: **AES** o **TKIP**  
> Tipos de EAP: **Tarjeta inteligente u otro certificado** o **PEAP**  

1.  En la página **Configuración de seguridad** del Asistente para crear perfil de Wi-Fi, seleccione el protocolo de seguridad que usa la red inalámbrica o seleccione **Sin autenticación (sistema abierto)** si la red no está protegida.  

     Solo para dispositivos Android: no se admiten los tipos de seguridad **WPA â€“ Personal**, **WPA2 â€“ Personal** y **WEP**.  

2.  seleccione el método de cifrado que la red inalámbrica usa.  

3.  seleccione el tipo de EAP que se usa para realizar la autenticación con la red inalámbrica.  

     Solo para dispositivos Windows Phone: no se admiten los tipos de EAP **LEAP** y **EAP-FAST** .  

4.  Haga clic en **Configurar** para especificar las propiedades para el tipo de EAP seleccionado. Es posible que esta opción no esté disponible para algunos tipos de EAP seleccionados.  

    > [!IMPORTANT]  
    >  Al hacer clic en **Configurar**, el cuadro de diálogo que se abre es un cuadro de diálogo de Windows. Debido a esto, debe asegurarse de que el sistema operativo del equipo que ejecuta la consola de Configuration Manager admite la configuración del tipo de EAP seleccionado.  
    >   
    >  Para dispositivos iOS, si elige un método no EAP para la autenticación, independientemente del método que elija, se usará MS-CHAP v2 para la conexión.  

5.  Si quiere almacenar las credenciales de usuario para que los usuarios no tengan que escribir las credenciales en cada inicio de sesión, seleccione **Recordar las credenciales de usuario en cada inicio de sesión**.  

### <a name="for-ios-devices-only"></a>Solo para dispositivos iOS:  
 configure la información de los certificados necesarios para la conexión Wi-Fi. Debe configurar el certificado de cliente y el nombre de certificado del servidor de confianza o el certificado raíz de la manera siguiente:  

-   **Nombres de certificado de servidor de confianza**: si el servidor al que se conecta el dispositivo usa un certificado de autenticación de servidor para identificar el servidor y proteger el canal de comunicación, escriba el nombre o los nombres en el nombre del sujeto o nombre alternativo del sujeto del certificado. El nombre o los nombres suelen ser el nombre de dominio completo del servidor. Por ejemplo, si el certificado del servidor tiene un nombre común de srv1.contoso.com en el firmante del certificado, escriba **srv1.contoso.com**. Si el certificado del servidor tiene varios nombres especificados en el nombre alternativo del sujeto, escriba los nombres separados por un punto y coma.  

    > [!TIP]  
    >  Si el certificado de cliente que se selecciona para EAP o autenticación de cliente para un dispositivo iOS se va a usar para realizar la autenticación en un servidor de Servicio de autenticación remota telefónica de usuario (RADIUS) como, por ejemplo, un servidor que ejecuta Servidor de directivas de redes, debe configurar el nombre alternativo del sujeto como nombre principal de usuario.  

-   **Seleccionar certificados raíz para la validación del servidor:**: si el servidor al que se conecta el dispositivo usa un certificado de autenticación de servidor en el que el dispositivo no confía, seleccione el perfil de certificado que contenga el certificado raíz para el certificado de servidor, a fin de crear una cadena de certificados de confianza en el dispositivo.  

-   **Seleccionar un certificado de cliente para autenticación de cliente**: si el servidor o dispositivo de red requiere un certificado de cliente para autenticar el dispositivo que se conecta, seleccione el perfil de certificado que contiene el certificado de autenticación del cliente.  

> [!NOTE]  
>  Antes de poder seleccionar el certificado raíz y el certificado de cliente, primero debe configurarlos e implementarlos como un perfil de certificado. Para obtener más información sobre los perfiles de certificado, consulte [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Perfiles de certificado en Configuration Manager).  

##  <a name="a-namebkmkstep5a-step-5-configure-advanced-settings-for-the-wi-fi-profile"></a><a name="BKMK_Step5"></a> Paso 5: Configurar opciones avanzadas del perfil de Wi-Fi  
 En la página **Configuración avanzada** del Asistente para crear perfil de Wi-Fi, especifique opciones avanzadas del perfil de Wi-Fi, como el modo de autenticación, las opciones de inicio de sesión único y la compatibilidad con FIPS (Estándar federal de procesamiento de información). Para obtener más información, consulte la documentación de Windows.  

> [!NOTE]  
>  Es posible que la configuración avanzada no esté disponible o que pueda variar según las opciones seleccionadas en la página **Configuración de seguridad** del asistente.  

##  <a name="a-namebkmkstep6a-step-6-configure-proxy-settings-for-the-wi-fi-profile"></a><a name="BKMK_Step6"></a> Paso 6: Configurar el proxy para el perfil de Wi-Fi  

1.  En la página **Configuración de proxy** del Asistente para crear perfil de Wi-Fi, active la casilla **Configurar proxy para este perfil de Wi-Fi** si su red inalámbrica usa un servidor proxy.  

2.  Especifique los detalles sobre el servidor proxy y su configuración. Para obtener más información, consulte la documentación de Windows Server.  

##  <a name="a-namebkmkstep7a-step-7-configure-supported-platforms-for-the-wi-fi-profile"></a><a name="BKMK_Step7"></a> Paso 7: Configurar las plataformas admitidas para el perfil de Wi-Fi  
 En la página **Plataformas admitidas** del Asistente para crear perfil de Wi-Fi, seleccione los sistemas operativos en los que desea instalar el perfil de Wi-Fi. O bien, haga clic en **Seleccionar todo** para instalar el perfil de Wi-Fi en todos los sistemas operativos disponibles.  

##  <a name="a-namebkmkstep8a-step-8-complete-the-wizard"></a><a name="BKMK_Step8"></a> Paso 8: Completar el asistente  
 En la página **Resumen** del asistente, revise las acciones que el asistente realizará y, a continuación, complete el asistente. El nuevo perfil de Wi-Fi se muestra en el nodo **Perfiles de Wi-Fi** en el área de trabajo **Activos y compatibilidad** .  

 Para obtener más información sobre cómo implementar el perfil de Wi-Fi, consulte [How to deploy Wi-Fi profiles in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md) (Cómo implementar perfiles de Wi-Fi en System Center Configuration Manager).  



<!--HONumber=Nov16_HO1-->


