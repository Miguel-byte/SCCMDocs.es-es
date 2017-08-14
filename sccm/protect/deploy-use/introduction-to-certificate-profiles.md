---
title: "Introducción a los perfiles de certificado | Microsoft Docs"
description: "Obtenga información sobre cómo funcionan los perfiles de certificado en System Center Configuration Manager con Servicios de certificados de Active Directory."
ms.custom: na
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
caps.latest.revision: 7
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: c0d94b8e6ca6ffd82e879b43097a9787e283eb6d
ms.openlocfilehash: 7b1c0e449f3d1ef42e279e8707df6bf1df163b3f
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---

# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Introducción a los perfiles de certificado en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


Los perfiles de certificado trabajan con los Servicios de certificados de Active Directory y el rol Servicio de inscripción de dispositivos de red para aprovisionar certificados de autenticación para dispositivos administrados para que los usuarios puedan acceder sin problemas a los recursos de empresa. Por ejemplo, puede crear e implementar perfiles de certificado para proporcionar los certificados necesarios para que los usuarios inicien conexiones VPN e inalámbricas. 

Los perfiles de certificado pueden configurar automáticamente dispositivos de usuario para tener acceso a los recursos de la compañía, como las redes Wi-Fi y los servidores VPN, sin tener que instalar manualmente los certificados o usar un proceso fuera de banda. Los perfiles de certificado también pueden ayudar a proteger los recursos de empresa porque permite usar una configuración más segura que es compatible con la infraestructura de clave pública (PKI) de su empresa. Por ejemplo, puede requerir la autenticación de servidor para todas las conexiones VPN y Wi-Fi porque ha aprovisionado los certificados necesarios en los dispositivos administrados.   

Los perfiles de certificado proporcionan las siguientes capacidades de administración:  

-   Inscripción y renovación de certificados desde una entidad de certificación (CA) empresarial para dispositivos que ejecutan iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop y Mobile, y Android. Estos certificados se pueden usar en conexiones Wi-Fi y VPN.  

-   Implementación de certificados de entidad de certificación raíz de confianza y certificados de entidad de certificación intermedios para configurar una cadena de confianza en dispositivos para conexiones VPN y Wi-Fi, cuando se requiere autenticación de servidor.  

-   Supervisar los certificados instalados y notificar acerca de ellos.  

**Ejemplo:** Todos los empleados deben poder conectarse a puntos de conexión Wi-Fi en diversas ubicaciones corporativas. Implemente los certificados necesarios para conectarse a la red Wi-Fi, e implemente perfiles de Wi-Fi que hagan referencia al certificado para habilitar la conexión de usuario sin problemas.  

**Ejemplo:** Dispone de una PKI local y quiere optar por un método más flexible y seguro de aprovisionamiento de certificados que permita a los usuarios obtener acceso a los recursos de empresa desde sus dispositivos personales sin poner en riesgo la seguridad. Configure perfiles de certificados con las opciones y los protocolos admitidos en la plataforma específica del dispositivo. Los dispositivos pueden solicitar automáticamente estos certificados desde un servidor de inscripción accesible desde Internet. Después, configure los perfiles de VPN para que usen estos certificados y que el dispositivo pueda acceder a los recursos de empresa.  

## <a name="types-of-certificate-profiles"></a>Tipos de perfiles de certificado  
 Hay tres tipos de perfiles de certificado:  

-   **Certificado de CA de confianza**: permite implementar un certificado de CA raíz o un certificado de CA intermedio de confianza para formar una cadena de confianza si el dispositivo debe autenticar un servidor.  

-   **Protocolo de inscripción de certificados simple (SCEP)**: permite solicitar un certificado para un dispositivo o usuario mediante el protocolo SCEP y el Servicio de inscripción de dispositivos de red en un servidor que ejecuta Windows Server 2012 R2.

    Para crear un perfil de certificado de **Protocolo de inscripción de certificados simple (SCEP)**, primero cree uno del tipo **Certificado de CA de confianza**.

-   **Intercambio de información personal (.pfx)**: permite solicitar un certificado .pfx (también conocido como PKCS #12) para un dispositivo o usuario.

    Puede crear perfiles de certificado PFX [importando las credenciales](/sccm/mdm/deploy-use/import-pfx-certificate-profiles.md) de certificados existentes o [definiendo una autoridad de certificación](/sccm/mdm/deploy-use/create-pfx-certificate-profiles.md) para procesar las solicitudes.

    A partir de la versión 1706, puede usar Microsoft o Entrust como entidades de certificación de certificados **Intercambio de información personal (.pfx)**.


## <a name="requirements-and-supported-platforms"></a>Requisitos y plataformas admitidas  
Para implementar perfiles de certificado que usan el SCEP, debe instalar el punto de registro de certificado en un servidor del sistema de sitios en el sitio de administración central o en un sitio primario. También debe instalar un módulo de directivas para NDES, el módulo de directivas de Configuration Manager, en un servidor que ejecute Windows Server 2012 R2 con el rol Servicios de certificados de Active Directory y un NDES operativo y al que los dispositivos que precisan certificados puedan acceder. Para los dispositivos inscritos por Microsoft Intune, se requiere poder tener acceso al NDES desde Internet, por ejemplo, en una subred filtrada (también se conoce como red perimetral).  

Los certificados PFX también requieren un punto de registro de certificados en un servidor del sistema de sitios en el sitio de administración central o en un sitio primario.  También debe especificar la entidad de certificación (CA) del certificado y especificar las credenciales de acceso pertinentes.  A partir de la versión 1706, puede especificar Microsoft o Entrust como entidades de certificación.  

Para obtener más información sobre la compatibilidad del Servicio de inscripción de dispositivos de red con un módulo de directivas para que Configuration Manager pueda implementar certificados, vea [Uso de un módulo de directivas con el servicio de inscripción de dispositivos de red](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

Configuration Manager admite la implementación de certificados en varios almacenes de certificados distintos en función de los requisitos, el tipo de dispositivo y el sistema operativo. Se admiten los dispositivos y los sistemas operativos siguientes:  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop y Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Para implementar perfiles en dispositivos Android, iOS, Windows Phone y Windows 8.1 o posterior inscritos, estos dispositivos deben [inscribirse en Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).   

Un escenario habitual de System Center Configuration Manager es instalar certificados de CA raíz de confianza para autenticar servidores Wi-Fi y VPN si la conexión usa los protocolos de autenticación EAP-TLS, EAP-TTLS y PEAP, y los protocolos de túnel VPN Cisco IPsec, IKEv2 y L2TP/IPsec.  

Debe asegurarse de que un certificado de CA raíz empresarial está instalado en el dispositivo para que este pueda solicitar certificados mediante el perfil de certificado de SCEP.  

Puede especificar diversas opciones de configuración en un perfil de certificado de SCEP para solicitar los certificados personalizados para distintos entornos o requisitos de conectividad. El **Asistente para crear perfil de certificado** contiene dos páginas para parámetros de inscripción. La primera, **Inscripción de SCEP**, contiene la configuración de la solicitud de inscripción y la ubicación de instalación del certificado. La segunda, **Propiedades de certificado**, describe el certificado solicitado.  

## <a name="deploying-certificate-profiles"></a>Implementación de perfiles de certificado  
 Al implementar un perfil de certificado, los archivos de certificado en el perfil se instalan en los dispositivos cliente. También se implementarán los parámetros de SCEP. Las solicitudes de SCEP se procesarán en el dispositivo cliente. Puede implementar perfiles de certificado para recopilaciones de usuarios o de dispositivos y especificar el almacén de destino de cada certificado. Las reglas de aplicación determinan si los certificados se pueden instalar en el dispositivo. Cuando los perfiles de certificado se implementan en recopilaciones de usuarios, la afinidad de dispositivo de usuario determina el dispositivo del usuario que instalará los certificados. Cuando los perfiles de certificado que contienen certificados de usuario se implementan en recopilaciones de dispositivos, los certificados se instalarán en todos los dispositivos primarios de los usuarios de manera predeterminada. Para modificar este comportamiento, instale el certificado en cualquiera de los dispositivos de los usuarios en la página **Inscripción de SCEP** del **Asistente para crear perfil de certificado**. Además, los certificados de usuario no se implementarán en los dispositivos si son equipos de grupo de trabajo.  

## <a name="monitoring-certificate-profiles"></a>Supervisión de perfiles de certificado  

Puede supervisar las implementaciones de perfil de certificado viendo los informes o resultados de cumplimiento. Estos enfoques se describen en [Cómo supervisar perfiles de certificado](/sccm/protect/deploy-use/monitor-certificate-profiles).


## <a name="automatic-revocation-of-certificates"></a>Revocación automática de certificados  
 System Center Configuration Manager revoca automáticamente certificados de usuario y de equipo que se implementaron mediante perfiles de certificado en las circunstancias siguientes:  

-   El dispositivo se retira de la administración de System Center Configuration Manager.  

-   El dispositivo se borra de forma selectiva.  

-   El dispositivo se bloquea de la jerarquía de System Center Configuration Manager.  

 Para revocar los certificados, el servidor de sitio envía un comando de revocación a la entidad de certificación emisora. El motivo de la revocación es **Cese de operación**.  
