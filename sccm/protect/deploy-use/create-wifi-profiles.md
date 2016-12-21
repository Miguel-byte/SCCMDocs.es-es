---
title: Crear perfiles de Wi-Fi | Microsoft Docs
description: "Aprenda a usar perfiles de Wi-Fi en System Center Configuration Manager para implementar la configuración de red inalámbrica para los usuarios de su organización."
ms.custom: na
ms.date: 12/11/2016
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
ms.sourcegitcommit: 22a74f3b12fe4f4559b682a8fcb287863a7686af
ms.openlocfilehash: 1262cb7d524fdce21f778e2179275bd177e9330f


---
# <a name="how-to-create-wi-fi-profiles-in-system-center-configuration-manager"></a>Cómo crear perfiles de Wi-Fi en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


Use perfiles de Wi-Fi en System Center Configuration Manager para implementar la configuración de red inalámbrica para los usuarios de su organización. Al implementar estas opciones, les resultará más fácil a los usuarios conectarse a la Wi-Fi.  

 Por ejemplo, tiene una red Wi-Fi en la que desea permitir la conexión de todos los dispositivos de iOS. Cree un perfil de Wi-Fi que contenga la configuración necesaria para conectarse a la red inalámbrica. A continuación, implemente el perfil para todos los usuarios que tengan dispositivos iOS en la jerarquía. Los usuarios de dispositivos iOS ven la red de la compañía en la lista de redes inalámbricas y pueden conectarse fácilmente a esta red.  

 Puede configurar los siguientes tipos de dispositivos con perfiles de Wi-Fi:  

-   Dispositivos con Windows 8.1 de 32 bits  

-   Dispositivos con Windows 8.1 de 64 bits  

-   dispositivos con Windows RT 8.1  

-   Dispositivos con Windows Phone 8.1  

-   Dispositivos con Windows 10 Desktop o Mobile  

-   Dispositivos IPhone con iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos IPad con iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos Android con la versión 4 o posterior

> [!IMPORTANT]  
>  Para implementar perfiles en dispositivos Android, iOS, Windows Phone y Windows 8.1 o posterior inscritos, estos dispositivos deben inscribirse en Microsoft Intune. Para obtener información sobre cómo inscribir dispositivos, consulte [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune) (Inscribir dispositivos para la administración en Intune).  

 Cuando se crea un perfil de Wi-Fi, puede incluir una amplia gama de opciones de seguridad. Estas incluyen certificados para la validación de servidor y la autenticación de cliente que se han insertado mediante perfiles de certificado de Configuration Manager. Para obtener más información sobre los perfiles de certificado, consulte [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Perfiles de certificado en Configuration Manager).  

## <a name="create-a-wi-fi-profile"></a>Crear un perfil de Wi-Fi  

1.  En la consola de Configuration Manager, elija **Activos y compatibilidad** > **Configuración de cumplimiento** >  **Acceso a los recursos de la compañía** > **Perfiles Wi-Fi**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, elija **Crear perfil de Wi-Fi**.  

1.  En la página **General**, escriba un nombre único y una descripción para el perfil de Wi-Fi.  Si desea usar la configuración de otro perfil de Wi-Fi, seleccione **Importar un elemento de perfil de Wi-Fi existente desde un archivo**.  

    > [!IMPORTANT]  
    >  Asegúrese de que el perfil de Wi-Fi que desea importar contiene XML válido para un perfil de Wi-Fi. Configuration Manager no valida el perfil al importar el archivo.  

3.  En **Gravedad de la falta de compatibilidad de los informes**, especifique el nivel de gravedad que se notificará si el perfil de Wi-Fi no es compatible con los dispositivos cliente (por ejemplo, si se produce un error en la instalación del perfil). Los niveles de gravedad disponibles son los siguientes:  

    -   **Ninguno**: los equipos que no cumplan esta regla de compatibilidad no notificarán ninguna gravedad de error en los informes de Configuration Manager.  

    -   **Información**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Información** en los informes de Configuration Manager.  

    -   **Advertencia**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Advertencia** en los informes de Configuration Manager.  

    -   **Crítico**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager.  

    -   **Crítico con evento**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager. Este nivel de gravedad también se registra como evento de Windows en el registro de eventos de la aplicación.  

1.  En la página **Perfil de Wi-Fi** proporcione nombre que los dispositivos mostrarán como nombre de red.  

    > [!IMPORTANT]  
    >  Configuration Manager no admite el uso de los caracteres apóstrofo (**â€˜**) o coma (**,**) en el nombre de red.  

2.  Especificar mayúsculas y minúsculas **SSID**
3.  Elija otras opciones de conectividad adecuadas, incluidos.   **Conectarse cuando la red no está difundiendo su nombre (SSID)**, si existe la posibilidad de que el SSID esté oculto  

4.  En la página **Configuración de seguridad**, seleccione el protocolo de seguridad que la red inalámbrica utiliza, o seleccione **Sin autenticación (sistema abierto)** si la red no es segura.
    > [!IMPORTANT]  
    >  Si va a crear un perfil de Wi-Fi para la Administración de dispositivos móviles local, la rama actual de Configuration Manager solo admite las siguientes configuraciones de seguridad de Wi-Fi:  
    >   
    >  Tipos de seguridad: **WPA2 Enterprise** o **WPA2 Personal**  
    > Tipos de cifrado: **AES** o **TKIP**  
    > Tipos de EAP: **Tarjeta inteligente u otro certificado** o **PEAP**  
  
    > Para dispositivos Android no se admiten los tipos de seguridad **WPA-Personal**, **WPA2 – Personal** y **WEP** .  

2.  seleccione el método de cifrado que la red inalámbrica usa.  

3.  seleccione el tipo de EAP que se usa para realizar la autenticación con la red inalámbrica.  

     Solo para dispositivos Windows Phone: no se admiten los tipos de EAP **LEAP** y **EAP-FAST** .  

4.  Haga clic en **Configurar** para especificar las propiedades para el tipo de EAP seleccionado. Es posible que esta opción no esté disponible para algunos tipos de EAP seleccionados.  

    > [!IMPORTANT]  
    >  Al hacer clic en **Configurar**, el cuadro de diálogo que se abre es un cuadro de diálogo de Windows. Debido a esto, debe asegurarse de que el sistema operativo del equipo que ejecuta la consola de Configuration Manager admite la configuración del tipo de EAP seleccionado.  
    >   
    >  Para dispositivos iOS, si elige un método no EAP para la autenticación, independientemente del método que elija, se usará MS-CHAP v2 para la conexión.  

5.  Si quiere almacenar las credenciales de usuario para que los usuarios no tengan que escribir las credenciales en cada inicio de sesión, seleccione **Recordar las credenciales de usuario en cada inicio de sesión**.  

6. **Solo para dispositivos iOS:**  
 configure la información de los certificados necesarios para la conexión Wi-Fi. Debe configurar el certificado de cliente y el nombre de certificado del servidor de confianza o el certificado raíz de la manera siguiente:  

    -   **Nombres de certificado de servidor de confianza**: si el servidor al que se conecta el dispositivo usa un certificado de autenticación de servidor para identificar el servidor y proteger el canal de comunicación, escriba el nombre o los nombres en el nombre del sujeto o nombre alternativo del sujeto del certificado. El nombre o los nombres suelen ser el nombre de dominio completo del servidor. Por ejemplo, si el certificado del servidor tiene un nombre común de srv1.contoso.com en el firmante del certificado, escriba **srv1.contoso.com**. Si el certificado del servidor tiene varios nombres especificados en el nombre alternativo del sujeto, escriba los nombres separados por un punto y coma.  

    > [!TIP]  
    >  Si el certificado de cliente que se selecciona para EAP o autenticación de cliente para un dispositivo iOS se va a usar para realizar la autenticación en un servidor de Servicio de autenticación remota telefónica de usuario (RADIUS) como, por ejemplo, un servidor que ejecuta Servidor de directivas de redes, debe configurar el nombre alternativo del sujeto como nombre principal de usuario.  

    -   **Seleccionar certificados raíz para la validación del servidor:**: si el servidor al que se conecta el dispositivo usa un certificado de autenticación de servidor en el que el dispositivo no confía, seleccione el perfil de certificado que contenga el certificado raíz para el certificado de servidor, a fin de crear una cadena de certificados de confianza en el dispositivo.  

    -   **Seleccionar un certificado de cliente para autenticación de cliente**: si el servidor o dispositivo de red requiere un certificado de cliente para autenticar el dispositivo que se conecta, seleccione el perfil de certificado que contiene el certificado de autenticación del cliente.  

    > [!NOTE]  
    >  Antes de poder seleccionar el certificado raíz y el certificado de cliente, primero debe configurarlos e implementarlos como un perfil de certificado. Para obtener más información sobre los perfiles de certificado, consulte [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Perfiles de certificado en Configuration Manager).  

7.  En la página **Configuración avanzada**, especifique opciones avanzadas del perfil de Wi-Fi, como el modo de autenticación, las opciones de inicio de sesión único y la compatibilidad con FIPS (Estándar federal de procesamiento de información). Para obtener más información, consulte la documentación de Windows. Es posible que la configuración avanzada no esté disponible o que pueda variar según las opciones seleccionadas en la página **Configuración de seguridad** del asistente.  

1.  En la página **Configuración de proxy**, seleccione **Configurar proxy para este perfil de Wi-Fi** si su red inalámbrica usa un servidor proxy y, a continuación, proporcione la información de configuración.  

2. En la página **Plataformas admitidas**, seleccione los sistemas operativos en los que desea instalar el perfil de Wi-Fi. O bien, haga clic en **Seleccionar todo** para instalar el perfil de Wi-Fi en todos los sistemas operativos disponibles.  

### <a name="next-steps"></a>Pasos siguientes
 Para obtener más información sobre cómo implementar el perfil de Wi-Fi, consulte [How to deploy Wi-Fi profiles in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md) (Cómo implementar perfiles de Wi-Fi en System Center Configuration Manager).  



<!--HONumber=Dec16_HO3-->


