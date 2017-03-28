---
title: Perfiles de VPN en System Center Configuration Manager | Microsoft Docs
description: "Perfiles de VPN en dispositivos móviles en System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 8c7bf901caa49c8585a9ed3913d4a5a2aac57013
ms.openlocfilehash: 82f7db908f83d69a86c82ed97b845ff84e78f8b3
ms.lasthandoff: 03/21/2017

---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>Perfiles de VPN en dispositivos móviles en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use perfiles de VPN en System Center Configuration Manager para implementar la configuración de VPN en los usuarios de dispositivos móviles de la organización. Mediante la implementación de esta configuración, se minimiza la intervención del usuario final necesaria para conectarse a los recursos de la red de la empresa.  

 Por ejemplo, quiere aprovisionar todos los dispositivos que ejecutan el sistema operativo iOS con la configuración necesaria para conectarse a un recurso compartido de archivos de la red corporativa. Puede crear un perfil de VPN que contiene la configuración necesaria para conectarse a la red corporativa y, después, implementar este perfil a todos los usuarios de la jerarquía que tienen dispositivos que ejecutan iOS. Los usuarios de dispositivos iOS verán la conexión VPN en la lista de redes disponibles y pueden conectarse a esta red con un esfuerzo mínimo.  

 Cuando cree un perfil de VPN, puede incluir una amplia gama de opciones de seguridad, incluidos certificados para la validación del servidor y la autenticación del cliente aprovisionados mediante perfiles de certificado de System Center Configuration Manager. Para obtener más información sobre los perfiles de certificado, consulte [Certificate profiles in System Center Configuration Manager](../../protect/deploy-use/introduction-to-certificate-profiles.md) (Perfiles de certificado en Configuration Manager).  

 ## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Perfiles de VPN en Configuration Manager con Intune

 Para implementar perfiles en dispositivos iOS, Android, Windows Phone y Windows 8.1, estos dispositivos deben inscribirse en Microsoft Intune. También se pueden inscribir en Intune dispositivos de otras plataformas. Para obtener información sobre cómo realizar la inscripción, consulte [Manage mobile devices with Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx) (Administrar dispositivos móviles con Microsoft Intune). En esta tabla se muestra qué tipo de conexión se admite para cada plataforma de dispositivo:  

 |Tipo de conexión|iOS y Mac OS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop y Mobile|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|Sí|Sí|No|No|No|No|Sí (OMA-URI)|  
 |Pulse Secure|Sí|Sí|Sí|No|Sí|Sí|Sí|  
 |F5 Edge Client|Sí|Sí|Sí|No|Sí|Sí|Sí|  
 |Dell SonicWALL Mobile Connect|Sí|Sí|Sí|No|Sí|Sí|Sí|  
 |VPN móvil de punto de comprobación|Sí|Sí|Sí|No|Sí|Sí|Sí|  
 |Microsoft SSL (SSTP)|No|No|Sí|Sí|Sí|No|No|  
 |Microsoft Automatic|No|No|Sí|Sí|Sí|No|Sí (OMA-URI)|  
 |IKEv2|Sí (directiva personalizada)|No|Sí|Sí|Sí|Sí|Sí (OMA-URI)|  
 |PPTP|Sí|No|Sí|Sí|Sí|No|Sí (OMA-URI)|  
 |L2TP|Sí|No|Sí|Sí|Sí|No|Sí (OMA-URI)|  

## <a name="create-vpn-profiles"></a>Crear perfiles de VPN
[Cómo crear perfiles de VPN en System Center Configuration Manager](../../protect/deploy-use/create-vpn-profiles.md) proporciona información general sobre cómo crear perfiles de VPN.

###   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Características de VPN de Windows 10 disponibles cuando se usa Configuration Manager con Intune  


> [!NOTE]  
> El nombre de un perfil de VPN que usa las características de VPN de Windows 10 no puede estar en formato Unicode ni incluir caracteres especiales.


|Opción|Más información|Tipo de conexión|  
    |------------|----------------------|---------------------|  
    |**Omitir VPN al conectarse a la red Wi-Fi de empresa**|La conexión VPN no se usará cuando el dispositivo se conecte a la red Wi-Fi de la empresa. Escriba el nombre de red de confianza que se ha usado para determinar si el dispositivo está conectado a la red de la empresa.|Todos|  
    |**Reglas de tráfico de red**|Defina qué protocolos, puertos locales y remotos e intervalos de direcciones se habilitarán para la conexión VPN.<br /><br /> **Nota:** Si no se crea ninguna regla de tráfico de red, se habilitan todos los protocolos, puertos e intervalos de direcciones. Una vez creada una regla, la conexión VPN solo usará los protocolos, puertos e intervalos de direcciones que especifique en esa regla o en reglas adicionales.|Todos|  
    |**Rutas**|Rutas que usará la conexión VPN. Tenga en cuenta que la creación de más de 60 rutas puede producir un error en la directiva. |Todos|  
    |**Servidores DNS**|Qué servidores DNS usa la conexión VPN una vez establecida la conexión.|Todos|  
    |**Aplicaciones que se conectan automáticamente a la VPN**|Puede agregar aplicaciones o importar una lista de aplicaciones que usarán automáticamente la conexión VPN. El tipo de aplicación determinará el identificador de la aplicación. Para una aplicación de escritorio, proporcione la ruta del archivo de la aplicación. Para una aplicación universal, proporcione el nombre de familia de paquete (PFN). Para obtener información sobre cómo buscar el PFN de una aplicación, consulte [Find a package family name for per-app VPN](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md) (Buscar un nombre de familia de paquete para VPN por aplicación). |Todos|

> [!IMPORTANT]
> Se recomienda que proteja todas las listas de aplicaciones asociadas que se compilan para su uso en la configuración de VPN por aplicación. Si un usuario no autorizado modifica la lista y usted la importa en la lista de aplicaciones de VPN por aplicación, podría autorizar el acceso a VPN a aplicaciones que no deberían tener acceso. Una forma de proteger las listas de aplicaciones consiste en usar una lista de control de acceso (ACL).


1.  En la página **Método de autenticación** del asistente, especifique:  

    -   **Método de autenticación:** seleccione el método de autenticación que usará la conexión VPN. Métodos disponibles dependiendo del tipo de conexión como se muestra en esta tabla.  

        |Método de autenticación|Tipos de conexión admitidos|  
        |---------------------------|--------------------------------|  
        |**Certificados**<br /><br /> **Nota:** Si el certificado de cliente se usa para autenticar un servidor RADIUS, por ejemplo, un Servidor de directivas de redes, el nombre alternativo del sujeto en el certificado debe configurarse como el nombre principal de usuario.|- <br />                            Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN móvil de punto de comprobación|  
        |**Nombre de usuario y contraseña**|- <br />                            Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN móvil de punto de comprobación|  
        |**Microsoft EAP-TTLS**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - IKEv2<br /><br /> - L2TP|  
        |**EAP (PEAP) protegido de Microsoft**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Contraseña segura de Microsoft (EAP-MSCHAP v2)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Tarjeta inteligente u otro certificado**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**MSCHAP v2**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**RSA SecurID** (solo iOS)|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Usar certificados de máquina**|IKEv2|  

         En función de las opciones que seleccione, se le podría solicitar que especifique más información, como la siguiente:  

        -   **Recordar las credenciales de usuario en cada inicio de sesión**: las credenciales de usuario se recuerdan, de manera que el usuario no tiene que escribirlas cada vez que se conecte.  

        -   **Seleccionar un certificado de cliente para la autenticación de cliente**: seleccione el [certificado SCEP](create-pfx-certificate-profiles.md) de cliente que ha creado previamente y que se usará para autenticar la conexión VPN.   

            > [!NOTE]  
            >  Para dispositivos iOS, el perfil SCEP que seleccione se incrustará en el perfil de VPN. Para otras plataformas, se agrega una regla de aplicabilidad para garantizar que el perfil de VPN no se instala si el certificado no está presente o no es conforme.  
            >   
            >  Si el certificado SCEP que especifique no es compatible o no se implementó, el perfil de VPN no se instalará en el dispositivo.
            >  
            >  Los dispositivos que ejecutan iOS solo admiten RSA SecurID y MSCHAP v2 como métodos de autenticación cuando el tipo de conexión es PPTP. Para evitar errores, implemente un perfil de VPN PPTP independiente en los dispositivos que ejecutan iOS.  

        - **Acceso condicional**
            - Pulse **Habilitar acceso condicional para esta conexión VPN** para asegurarse de que los dispositivos que se conectan a la VPN se prueban para el cumplimiento del acceso condicional antes de la conexión. Las directivas de cumplimiento se describen en [Device compliance policies in System Center Configuration Manager (Directivas de cumplimiento de dispositivos en System Center Configuration Manager)](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md).
            - Pulse **Habilitar inicio de sesión único (SSO) con certificado alternativo** para elegir un certificado diferente al certificado de autenticación de VPN para el cumplimiento del dispositivo. Si elige esta opción, proporcione el **EKU** (lista separada por comas) y el **Hash del emisor** para el certificado correcto que el cliente de VPN debe buscar.

         - **Windows Information Protection**: proporcione la identidad corporativa administrada por la empresa, que normalmente es el dominio principal de la organización, por ejemplo, *contoso.com*. Puede especificar varios dominios que sean propiedad de la organización separándolos con el carácter "|". Por ejemplo, *contoso.com|newcontoso.com*.   
              Para obtener más información sobre Windows Information Protection, consulte [Crear una directiva de Windows Information Protection (WIP) con Microsoft Intune](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune).   

         ![Configurar el acceso condicional para VPN](media/vpn-conditional-access.png)


> [!NOTE]  
> Para algunos métodos de autenticación, puede hacer clic en **Configurar** para abrir el cuadro de diálogo de propiedades de Windows (si la versión de Windows en la que ejecuta la consola de Configuration Manager es compatible con este método de autenticación), donde puede configurar las propiedades del método de autenticación.  


1.  En la página **Configuración de proxy** del **Asistente para crear perfil de VPN**, active la casilla **Configurar configuración de proxy para este perfil de VPN** si su conexión VPN usa un servidor proxy. Después, proporcione la información del servidor proxy. Para obtener más información, consulte la documentación de Windows Server.  

    > [!NOTE]  
    >  En los equipos Windows 8.1, el perfil de VPN no mostrará la información de proxy hasta que se conecte a la VPN con ese equipo.  


2. Configurar opciones de DNS adicionales (si es necesario)  
 En la página **Configurar una conexión VPN automática**, puede configurar las opciones siguientes:  

    -   **Habilitar VPN a petición** Use esta opción si quiere configurar opciones de DNS adicionales para dispositivos Windows Phone 8.1. Esta configuración solo se aplica a dispositivos Windows Phone 8.1 y solo se debe habilitar en los perfiles VPN que se van a implementar en dispositivos Windows Phone 8.1.

    -   Lista de sufijos DNS (solo dispositivos Windows Phone 8.1): configura los dominios que establecerán una conexión VPN. Para cada dominio que especifique, debe agregar el sufijo DNS, la dirección del servidor DNS y una de las siguientes acciones a petición:  

        -   **No establecer nunca**: no se abre nunca una conexión VPN.  

        -   **Establecer si es necesario**: solo se abre una conexión VPN si el dispositivo necesita conectarse a recursos.  

        -   **Establecer siempre**: siempre se abre la conexión VPN.  

    -   **Combinar**: copia todos los sufijos DNS que configuró en la **Lista de redes de confianza**.  

    -   **Lista de redes de confianza** (solo dispositivos Windows Phone 8.1): especifique un sufijo DNS en cada línea. Si el dispositivo se encuentra en una red de confianza, no se abrirá la conexión VPN.  

    -   **Lista de búsqueda de sufijos** (solo dispositivos Windows Phone 8.1): especifique un sufijo DNS en cada línea. Al conectarse a un sitio web mediante un nombre corto, se buscará cada sufijo DNS.  

     Por ejemplo, especifica los sufijos DNS **domain1.contoso.com** y **domain2.contoso.com** y, después, visita la dirección URL **http://mywebsite**. Se buscarán las siguientes direcciones:  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

    > [!NOTE]  
    >  Solo para dispositivos Windows Phone 8.1  
    >   
    >  Si se selecciona la opción **Enviar todo el tráfico de red a través de la conexión VPN** y la conexión VPN usa el túnel completo, la conexión VPN se abrirá automáticamente para el primer perfil aprovisionado en el dispositivo. Si desea que otro perfil abra automáticamente una conexión, debe convertirlo en el perfil predeterminado del dispositivo.  
    >   
    >  Si no se selecciona la opción **Enviar todo el tráfico de red a través de la conexión VPN** y la conexión VPN usa el túnel dividido, puede abrirse automáticamente una conexión VPN si se configuran las rutas o un sufijo DNS específico de la conexión.  


1. En la página **Plataformas admitidas** del **Asistente para crear perfil de VPN**, seleccione los sistemas operativos en los que se instalará el perfil de VPN o haga clic en **Seleccionar todo** para instalar el perfil de VPN en todos los sistemas operativos disponibles.  

2. Complete el asistente. El nuevo perfil de VPN se muestra en el nodo **Perfiles de VPN** en el área de trabajo **Activos y compatibilidad** .  


**Implementar**: consulte [Implementar perfiles de VPN en System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) para información sobre la implementación de perfiles de VPN.

### <a name="next-steps"></a>Pasos siguientes  
 Use los temas siguientes para planear, configurar, operar y mantener perfiles de VPN en Configuration Manager.  

-   [Requisitos previos de los perfiles de VPN en System Center Configuration Manager](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Seguridad y privacidad de los perfiles de VPN en System Center Configuration Manager](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)

