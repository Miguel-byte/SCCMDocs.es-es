---
title: Perfiles de VPN
titleSuffix: Configuration Manager
description: "Perfiles de VPN en dispositivos móviles en System Center Configuration Manager."
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
caps.latest.revision: "18"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: b60a1b9e85b00cbaba54db4ea4cd92a1038c3fcf
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>Perfiles de VPN en dispositivos móviles en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use perfiles de VPN en System Center Configuration Manager para implementar la configuración de VPN en los usuarios de dispositivos móviles de la organización. Mediante la implementación de esta configuración, se minimiza la intervención del usuario final necesaria para conectarse a los recursos de la red de la empresa.  

 Por ejemplo, quiere configurar todos los dispositivos que ejecutan el sistema operativo iOS con los parámetros necesarios para conectarse a un recurso compartido de archivos en la red corporativa. Puede crear un perfil de VPN que tenga la configuración necesaria para conectarse a la red corporativa y, después, implementar este perfil a todos los usuarios de la jerarquía que tengan dispositivos que ejecuten iOS. Los usuarios de dispositivos iOS verán la conexión VPN en la lista de redes disponibles y pueden conectarse a esta red con un esfuerzo mínimo.  

 Cuando se crea un perfil de VPN, puede incluir una amplia gama de opciones de seguridad. Por ejemplo, puede especificar certificados para la validación de servidor y la autenticación de cliente que se han configurado mediante perfiles de certificado de System Center Configuration Manager. Para obtener más información sobre los perfiles de certificado, consulte la información sobre [perfiles de certificado en Configuration Manager](../../protect/deploy-use/introduction-to-certificate-profiles.md).  

 ## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Perfiles de VPN en Configuration Manager con Intune

 Para implementar perfiles en dispositivos iOS, Android, Windows Phone y Windows 8.1, estos dispositivos deben inscribirse en Microsoft Intune. También se pueden inscribir en Intune dispositivos de otras plataformas. Para obtener información sobre cómo realizar la inscripción, consulte [Manage mobile devices with Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx) (Administrar dispositivos móviles con Microsoft Intune). En esta tabla se muestra qué tipo de conexión se admite para cada plataforma de dispositivo:  

 |Tipo de conexión|iOS y macOS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop y Mobile|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|Sí|Sí|No|No|No|No|Sí|
 |Cisco (IPsec)|Solo iOS|No|No|No|No|No|No|  
 |Pulse Secure|Sí|Sí|Sí|No|Sí|Sí|Sí|  
 |F5 Edge Client|Sí|Sí|Sí|No|Sí|Sí|Sí|  
 |Dell SonicWALL Mobile Connect|Sí|Sí|Sí|No|Sí|Sí|Sí|  
 |VPN móvil de punto de comprobación|Sí|Sí|Sí|No|Sí|Sí|Sí|  
 |Microsoft SSL (SSTP)|No|No|Sí|Sí|Sí|No|No|  
 |Microsoft Automatic|No|No|Sí|Sí|Sí|No|Sí|  
 |IKEv2|Sí (directiva personalizada, iOS 9 y versiones posteriores)|No|Sí|Sí|Sí|Sí|Sí|  
 |PPTP|Sí|No|Sí|Sí|Sí|No|Sí|  
 |L2TP|Sí|No|Sí|Sí|Sí|No|Sí (OMA-URI)|  

## <a name="create-vpn-profiles"></a>Crear perfiles de VPN
En [Cómo crear perfiles de VPN en System Center Configuration Manager](../../protect/deploy-use/create-vpn-profiles.md) se proporciona información general sobre cómo crear perfiles de VPN.

## <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Características de VPN de Windows 10 disponibles cuando se usa Configuration Manager con Intune  


> [!NOTE]  
> El nombre de un perfil de VPN que usa las características de VPN de Windows 10 no puede estar en formato Unicode ni incluir caracteres especiales.


|Opción|Más información|Tipo de conexión|  
    |------------|----------------------|---------------------|  
    |**Omitir VPN al conectarse a la red Wi-Fi de empresa**|La conexión VPN no se usará cuando el dispositivo se conecte a la red Wi-Fi de la empresa. Escriba el nombre de red de confianza que se ha usado para determinar si el dispositivo está conectado a la red de la empresa.|Todos|  
    |**Reglas de tráfico de red**|Defina qué protocolos, puertos local y remoto e intervalos de direcciones se habilitarán para la conexión VPN.<br /><br /> **Nota:** Si no se crea ninguna regla de tráfico de red, se habilitan todos los protocolos, puertos e intervalos de direcciones. Una vez creada una regla, la conexión VPN solo usará los protocolos, puertos e intervalos de direcciones que especifique en esa regla o en reglas adicionales.|Todos|  
    |**Rutas**|Rutas que usará la conexión VPN. Tenga en cuenta que la creación de más de 60 rutas puede producir un error en la directiva. |Todos|  
    |**Servidores DNS**|Servidores DNS que usa la conexión VPN una vez establecida la conexión.|Todos|  
    |**Aplicaciones que se conectan automáticamente a la VPN**|Puede agregar aplicaciones o importar listas de aplicaciones que usarán automáticamente la conexión VPN. El tipo de aplicación determinará el identificador de la aplicación. Para una aplicación de escritorio, proporcione la ruta del archivo de la aplicación. Para una aplicación universal, proporcione el nombre de familia de paquete (PFN). Para obtener información sobre cómo buscar el PFN de una aplicación, consulte [Find a package family name for per-app VPN](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md) (Buscar un nombre de familia de paquete para VPN por aplicación). |Todos|

> [!IMPORTANT]
> Se recomienda que proteja todas las listas de aplicaciones asociadas que se compilan para su uso en la configuración de VPN por aplicación. Si un usuario no autorizado modifica la lista y usted la importa en la lista de aplicaciones de VPN por aplicación, podría autorizar el acceso a VPN a aplicaciones que no deberían tener acceso. Una forma de proteger las listas de aplicaciones consiste en usar una lista de control de acceso (ACL).

1. En la página **Plataformas admitidas** del **Asistente para crear perfil de VPN**, seleccione los sistemas operativos en los que se instalará el perfil de VPN o elija **Seleccionar todo** para instalar el perfil de VPN en todos los sistemas operativos disponibles.  
2.  En la página **Método de autenticación** del asistente, especifique:  

    -   **Método de autenticación:** seleccione el método de autenticación que usará la conexión VPN. Métodos disponibles dependiendo del tipo de conexión como se muestra en esta tabla.  

        |Método de autenticación|Tipos de &nbsp;conexión&nbsp; admitidos|  
        |---------------------------|--------------------------------|  
        |**Certificados**<br /><br /> **Notas:**<ul><li>Si el certificado de cliente se autentica en un servidor RADIUS, como un Servidor de directivas de redes, el nombre alternativo del sujeto en el certificado debe configurarse como el nombre principal de usuario.</li><li>En el caso de las implementaciones de Android, seleccione el identificador EKU y el valor de hash de huella digital del emisor de certificados.  De lo contrario, los usuarios deben seleccionar manualmente el certificado adecuado.</li></ul>  |<ul><li>Cisco AnyConnect</li><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> VPN móvil de punto de comprobación</li></ul>|  
        |**Nombre de usuario y contraseña**|<ul><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> VPN móvil de punto de comprobación</li></ul>|  
        |**Microsoft EAP-TTLS**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>IKEv2</li><li>L2TP</li></ul>|  
        |**EAP (PEAP) protegido de Microsoft**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Contraseña segura de Microsoft (EAP-MSCHAP v2)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Tarjeta inteligente u otro certificado**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**MSCHAP v2**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**RSA SecurID** (solo iOS)|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Usar certificados de máquina**|<ul><li>IKEv2</li></ul>|  

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
            - Pulse **Habilitar acceso condicional para esta conexión VPN** para asegurarse de que los dispositivos que se conectan a la VPN se prueban para el cumplimiento del acceso condicional antes de la conexión. Las directivas de cumplimiento se describen en [Directivas de cumplimiento de dispositivo en System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md).
            - Seleccione **Habilitar inicio de sesión único (SSO) con certificado alternativo** para elegir un certificado diferente al certificado de autenticación de VPN para el cumplimiento del dispositivo. Si elige esta opción, proporcione el **EKU** (lista separada por comas) y el **Hash del emisor** para el certificado correcto que el cliente de VPN debe buscar.

         - Para **Windows Information Protection**, proporcione la identidad corporativa administrada por la empresa, que normalmente es el dominio principal de la organización, por ejemplo, *contoso.com*. Puede especificar varios dominios que sean propiedad de la organización separándolos con el carácter "|". Por ejemplo, *contoso.com|newcontoso.com*.   
            Para obtener más información sobre Windows Information Protection, consulte [Crear una directiva de Windows Information Protection (WIP) con Microsoft Intune](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune).   

         ![Configurar el acceso condicional para VPN](media/vpn-conditional-access.png)

         Cuando lo admita la versión de Windows que ejecuta Configuration Manager _y_ el método de autorización seleccionado, puede hacer clic en **Configurar** para abrir el cuadro de diálogo de propiedades de Windows y configurar las propiedades del método de autenticación.  Si **Configurar** está deshabilitado, utilice medios alternativos para configurar las propiedades del método de autenticación.

3.  En la página **Configuración de proxy** del **Asistente para crear perfil de VPN**, active la casilla **Configurar configuración de proxy para este perfil de VPN** si su conexión VPN usa un servidor proxy. Después, proporcione la información del servidor proxy. Para obtener más información, consulte la documentación de Windows Server.  

    > [!NOTE]  
    >  En los equipos Windows 8.1, el perfil de VPN no mostrará la información de proxy hasta que se conecte a la VPN con ese equipo.  


4. Configure opciones de DNS adicionales (si es necesario).  

5. Finalice el asistente. El nuevo perfil de VPN se muestra en el nodo **Perfiles de VPN** en el área de trabajo **Activos y compatibilidad** .  


**Implementar**: consulte [Implementar perfiles de VPN en System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) para obtener información sobre la implementación de perfiles de VPN.

## <a name="next-steps"></a>Pasos siguientes  
 Use los temas siguientes para planear, configurar, operar y mantener perfiles de VPN en Configuration Manager.  

-   [Requisitos previos de los perfiles de VPN en System Center Configuration Manager](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Seguridad y privacidad de los perfiles de VPN en System Center Configuration Manager](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
