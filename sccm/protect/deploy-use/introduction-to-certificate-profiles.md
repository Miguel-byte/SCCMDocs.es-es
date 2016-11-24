---
title: "Introducción a los perfiles de certificado | System Center Configuration Manager"
description: "Obtenga información sobre cómo funcionan los perfiles de certificado en System Center Configuration Manager con Servicios de certificados de Active Directory."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
caps.latest.revision: 7
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 41567ba411732baf9e920595203f699179dcb20a


---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Introducción a los perfiles de certificado en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


Los perfiles de certificado en System Center Configuration Manager funcionan con Servicios de certificados de Active Directory y el rol Servicio de inscripción de dispositivos de red para aprovisionar certificados de autenticación para dispositivos administrados a fin de que los usuarios puedan obtener acceso a los recursos de la compañía con facilidad. Por ejemplo, puede crear e implementar perfiles de certificado para proporcionar los certificados necesarios para que los usuarios inicien conexiones VPN e inalámbricas.  

 En System Center Configuration Manager, los perfiles de certificado proporcionan las siguientes capacidades de administración:  

-   Inscripción y renovación de certificados desde una entidad de certificación (CA) empresarial para dispositivos que ejecutan iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop y Mobile y Android. Estos certificados se pueden usar en conexiones Wi-Fi y VPN.  

-   Implementación de certificados de entidad de certificación raíz de confianza y certificados de entidad de certificación intermedios para configurar una cadena de confianza en dispositivos para conexiones VPN y Wi-Fi, cuando se requiere autenticación de servidor.  

-   Supervisar los certificados instalados y notificar acerca de ellos.  

 Los perfiles de certificado pueden configurar automáticamente dispositivos de usuario para tener acceso a los recursos de la compañía, como las redes Wi-Fi y los servidores VPN, sin tener que instalar manualmente los certificados o usar un proceso fuera de banda. Los perfiles de certificado también pueden ayudar a proteger los recursos de empresa porque permite usar una configuración más segura que es compatible con la infraestructura de clave pública (PKI) de su empresa. Por ejemplo, puede requerir la autenticación de servidor para todas las conexiones VPN y Wi-Fi porque ha aprovisionado los certificados necesarios en los dispositivos administrados.  

 **Ejemplo:** Todos los empleados deben poder conectarse a puntos de conexión Wi-Fi en diversas ubicaciones corporativas. Para ello, puede implementar los certificados necesarios para realizar la conexión Wi-Fi y, en System Center Configuration Manager, implementar también los perfiles Wi-Fi que hacen referencia al certificado correcto que se debe usar de modo que la conexión Wi-Fi se establezca sin problemas para los usuarios.  

 **Ejemplo:** Dispone de una PKI local y quiere optar por un método más flexible y seguro de aprovisionamiento de certificados que permita a los usuarios obtener acceso a los recursos de empresa desde sus dispositivos personales sin poner en riesgo la seguridad. Para ello, puede configurar perfiles de certificado con las opciones y los protocolos que se admiten en la plataforma de dispositivo específica. Los dispositivos pueden solicitar automáticamente estos certificados desde un servidor de inscripción accesible desde Internet. Después, puede configurar los perfiles de VPN para que usen estos certificados y que el dispositivo pueda acceder a los recursos de empresa.  

## <a name="types-of-certificate-profile"></a>Tipos de perfiles de certificado  
 Puede crear tres tipos de perfiles de certificado en System Center Configuration Manager:  

-   **Certificado de CA de confianza** : permite implementar un certificado de CA raíz o un certificado de CA intermedio de confianza para formar una cadena de confianza si el dispositivo debe autenticar un servidor.  

-   **Protocolo de inscripción de certificados simple (SCEP)**: permite solicitar un certificado para un dispositivo o usuario mediante el protocolo SCEP y el Servicio de inscripción de dispositivos de red en un servidor que ejecuta Windows Server 2012 R2.
-   -   **Intercambio de información personal (.pfx)**: permite solicitar un certificado para un dispositivo o usuario mediante el protocolo SCEP y el Servicio de inscripción de dispositivos de red en un servidor que ejecuta Windows Server 2012 R2.

    > [!NOTE]  
    >  Debe crear un perfil de certificado del tipo **Certificado de CA de confianza** antes de crear un perfil de certificado del tipo **Configuración de Protocolo de inscripción de certificados simple (SCEP)**.  

## <a name="requirements-and-supported-platforms"></a>Requisitos y plataformas admitidas  
 Para implementar perfiles de certificado que usan el Protocolo de inscripción de certificados simple, es preciso instalar el punto de registro de certificado en un servidor del sistema de sitios en el sitio de administración central o en un sitio primario. También debe instalar un módulo de directivas para el Servicio de inscripción de dispositivos de red, el módulo de directivas de Configuration Manager, en un servidor que ejecuta Windows Server 2012 R2 con el rol Servicios de certificados de Active Directory y un Servicio de inscripción de dispositivos de red operativo y al que los dispositivos que precisan certificados puedan acceder. Para los dispositivos inscritos por Microsoft Intune, se requiere poder tener acceso al Servicio de inscripción de dispositivos de red desde Internet, por ejemplo, en una subred filtrada (también se conoce como red perimetral).  

 Para obtener más información sobre la compatibilidad del Servicio de inscripción de dispositivos de red y un módulo de directivas para que System Center Configuration Manager pueda implementar certificados, consulte [Using a Policy Module with the Network Device Enrollment Service (Uso de un módulo de directivas con el Servicio de inscripción de dispositivos de red)](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

 System Center Configuration Manager admite la implementación de certificados en varios almacenes de certificados distintos en función de los requisitos, el tipo de dispositivo y el sistema operativo. Se admiten los dispositivos y los sistemas operativos siguientes:  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop y Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Para implementar perfiles en dispositivos Android, iOS, Windows Phone y Windows 8.1 o posterior inscritos, estos dispositivos deben inscribirse en Microsoft Intune. Para obtener información sobre cómo inscribir dispositivos, consulte [Administrar dispositivos móviles con Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 Un escenario habitual de System Center Configuration Manager es instalar certificados de CA raíz de confianza para autenticar servidores Wi-Fi y VPN si la conexión usa los protocolos de autenticación EAP-TLS, EAP-TTLS y PEAP, y los protocolos de túnel VPN Cisco IPsec, IKEv2 y L2TP/IPsec.  

 Debe asegurarse de que un certificado de CA raíz empresarial está instalado en el dispositivo para que este pueda solicitar certificados mediante el perfil de certificado de SCEP.  

 Puede especificar diversas opciones de configuración en un perfil de certificado de SCEP para solicitar los certificados personalizados para distintos entornos o requisitos de conectividad. El **Asistente para crear perfil de certificado** contiene dos páginas para parámetros de inscripción. La primera, **Inscripción de SCEP**, contiene la configuración de la solicitud de inscripción y la ubicación de instalación del certificado. La segunda, **Propiedades de certificado**, describe el certificado solicitado.  

## <a name="deploying-certificate-profiles"></a>Implementación de perfiles de certificado  
 Al implementar un perfil de certificado, los archivos de certificado en el perfil se instalan en los dispositivos cliente. También se implementarán los parámetros de SCEP. Las solicitudes de SCEP se procesarán en el dispositivo cliente. Puede implementar perfiles de certificado para recopilaciones de usuarios o de dispositivos y especificar el almacén de destino de cada certificado. Las reglas de aplicación determinan si los certificados se pueden instalar en el dispositivo. Cuando los perfiles de certificado se implementan en recopilaciones de usuarios, la afinidad de dispositivo de usuario determina los dispositivos de los usuarios que instalarán los certificados. Cuando los perfiles de certificado que contienen certificados de usuario se implementan en recopilaciones de dispositivos, los certificados se instalarán en todos los dispositivos primarios de los usuarios de manera predeterminada. Para modificar este comportamiento, instale el certificado en cualquiera de los dispositivos de los usuarios en la página **Inscripción de SCEP** del **Asistente para crear perfil de certificado**. Además, los certificados de usuario no se implementarán en los dispositivos si son equipos de grupo de trabajo.  

## <a name="monitoring-certificate-profiles"></a>Supervisión de perfiles de certificado  
 Puede supervisar las implementaciones de perfil de certificado mediante el nodo **Implementaciones** del área de trabajo **Supervisión** en la consola de System Center Configuration Manager.  

 También puede usar uno de los siguientes informes de System Center Configuration Manager para supervisar los perfiles de certificado:  

-   **Historial de certificados emitidos por el punto de registro de certificado**  

-   **Lista de activos por estado de emisión de certificado para certificados inscritos por el punto de registro de certificado**  

-   **Lista de activos con certificados a punto de expirar**  

## <a name="automatic-revocation-of-certificates"></a>Revocación automática de certificados  
 System Center Configuration Manager revoca automáticamente certificados de usuario y de equipo que se implementaron mediante perfiles de certificado en las circunstancias siguientes:  

-   El dispositivo se retira de la administración de System Center Configuration Manager.  

-   El dispositivo se borra de forma selectiva.  

-   El dispositivo se bloquea de la jerarquía de System Center Configuration Manager.  

 Para revocar los certificados, el servidor de sitio envía un comando de revocación a la entidad de certificación emisora. El motivo de la revocación es **Cese de operación**.  



<!--HONumber=Nov16_HO1-->


