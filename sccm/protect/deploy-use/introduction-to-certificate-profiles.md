---
title: Introducción a los perfiles de certificado
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo funcionan los perfiles de certificado en System Center Configuration Manager con Servicios de certificados de Active Directory.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 07d6ecefb2cc4cded7ce43bad3f681f8f335ec4e
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500450"
---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Introducción a los perfiles de certificado en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


Los perfiles de certificado funcionan con Servicios de certificados de Active Directory y el Servicio de inscripción de dispositivos de red (NDES). Cree e implemente certificados de autenticación para dispositivos móviles que permitan a los usuarios tener acceso fácilmente a los recursos de la empresa. Por ejemplo, puede crear e implementar perfiles de certificado para proporcionar los certificados necesarios para que los usuarios se conecten a redes VPN e inalámbricas.

Los perfiles de certificado pueden configurar automáticamente dispositivos de usuario. Los usuarios tienen acceso a recursos de la empresa como redes Wi-Fi y servidores VPN sin instalar certificados manualmente ni usar un proceso fuera de banda. Los perfiles de certificado contribuyen a proteger los recursos de empresa, porque le permiten usar una configuración más segura que es compatible con la infraestructura de clave pública (PKI) de su empresa. Por ejemplo, puede requerir la autenticación de servidor en todas las conexiones VPN y Wi-Fi, ya que ha implementado los certificados necesarios en los dispositivos administrados.   

Los perfiles de certificado proporcionan las siguientes capacidades de administración:  

-   Inscripción y renovación de certificados desde una entidad de certificación (CA) empresarial para dispositivos que ejecutan iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop y Mobile, y Android. Estos certificados se pueden usar en conexiones Wi-Fi y VPN.  

-   Implementación de certificados de entidades de certificación raíz de confianza y de certificados de entidades de certificación intermedias. Estos certificados configuran una cadena de confianza en dispositivos para conexiones VPN y Wi-Fi cuando se requiere autenticación de servidor.  

-   Supervisar los certificados instalados y notificar acerca de ellos.  

**Ejemplo:** Todos los empleados deben poder conectarse a puntos de conexión Wi-Fi en diversas ubicaciones corporativas. Para permitir una conexión de usuario sencilla, implemente primero los certificados necesarios para conectarse a Wi-Fi. Después, implemente los perfiles de Wi-Fi que hacen referencia al certificado.  

**Ejemplo:** tiene una PKI y quiere cambiar a un método más flexible y seguro de implementar certificados. Los usuarios deben poder tener acceso a los recursos de la empresa desde sus dispositivos personales sin poner en peligro la seguridad. Configure perfiles de certificados con las opciones y los protocolos admitidos en la plataforma específica del dispositivo. Los dispositivos pueden solicitar automáticamente estos certificados desde un servidor de inscripción accesible desde Internet. Después, configure los perfiles de VPN para que usen estos certificados y que el dispositivo pueda acceder a los recursos de empresa.  



## <a name="types-of-certificate-profiles"></a>Tipos de perfiles de certificado  
 Hay tres tipos de perfiles de certificado:  

-   **Certificado de entidad de certificación confianza**: implemente un certificado de entidad de certificación raíz de confianza o un certificado de entidad de certificación intermedia. Estos certificados forman una cadena de confianza cuando el dispositivo debe autenticarse en un servidor.  

-   **Protocolo de inscripción de certificados simple (SCEP)**: solicite un certificado para un dispositivo o usuario por medio del protocolo SCEP. Este tipo requiere el rol Servicio de inscripción de dispositivos de red (NDES) en un servidor que ejecuta Windows Server 2012 R2 o posterior.

    Para crear un perfil de certificado de **Protocolo de inscripción de certificados simple (SCEP)**, cree primero un perfil de **Certificado de CA de confianza**.

-   **Intercambio de información personal (.pfx)**: solicite un certificado .pfx (también conocido como PKCS #12) para un dispositivo o un usuario.<!--1321368-->  

    Puede crear perfiles de certificado PFX [importando las credenciales](/sccm/mdm/deploy-use/import-pfx-certificate-profiles) de certificados existentes o [definiendo una autoridad de certificación](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) para procesar las solicitudes.

    > [!Note]  
    > Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

    A partir de la versión 1706, puede usar Microsoft o Entrust como entidades de certificación de certificados **Intercambio de información personal (.pfx)**.


## <a name="requirements-and-supported-platforms"></a>Requisitos y plataformas admitidas  
Para implementar perfiles de certificado que usen SCEP, instale el punto de registro de certificados en un servidor de sistema de sitio. Instale también un módulo de directivas para NDES, el módulo de directivas de Configuration Manager, en un servidor que ejecute Windows Server 2012 R2 o posterior. Este servidor requiere el rol Servicios de certificados de Active Directory y un NDES operativo y al que los dispositivos que precisan certificados puedan tener acceso. En el caso de los dispositivos inscritos por Microsoft Intune, se requiere poder tener acceso al NDES desde Internet, por ejemplo, en una subred filtrada (también conocida como red perimetral).  

Los certificados PFX también requieren un punto de registro de certificados. Especifique también la entidad de certificación (CA) del certificado y las credenciales de acceso pertinentes. A partir de la versión 1706, puede especificar Microsoft o Entrust como entidades de certificación.  

Para obtener más información sobre la compatibilidad del Servicio de inscripción de dispositivos de red con un módulo de directivas para que Configuration Manager pueda implementar certificados, vea [Uso de un módulo de directivas con el servicio de inscripción de dispositivos de red](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

Según cuáles sean los requisitos, Configuration Manager admite la implementación de certificados en distintos almacenes de certificados de varios tipos de dispositivo y sistemas operativos. Se admiten los dispositivos y los sistemas operativos siguientes:  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop y Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Para implementar perfiles en dispositivos Android, iOS, Windows Phone y Windows 8.1 o posterior inscritos, estos dispositivos deben [inscribirse en Microsoft Intune](/intune/device-enrollment).   

Un escenario habitual de Configuration Manager es instalar certificados de CA raíz de confianza para autenticar servidores Wi-Fi y VPN si la conexión usa los protocolos de autenticación EAP-TLS, EAP-TTLS y PEAP, y los protocolos de túnel VPN Cisco IPsec, IKEv2 y L2TP/IPsec.  

Debe haber instalado un certificado de entidad de certificación raíz empresarial en el dispositivo para que este pueda solicitar certificados por medio del perfil de certificado de SCEP.  

Puede especificar opciones de configuración en un perfil de certificado de SCEP para solicitar los certificados personalizados para distintos entornos o requisitos de conectividad. El **Asistente para crear perfil de certificado** tiene dos páginas para parámetros de inscripción. La primera, **Inscripción de SCEP**, contiene la configuración de la solicitud de inscripción y la ubicación de instalación del certificado. La segunda, **Propiedades de certificado**, describe el certificado solicitado.  

## <a name="deploying-certificate-profiles"></a>Implementación de perfiles de certificado  
 Al implementar un perfil de certificado, los archivos de certificado en el perfil se instalan en los dispositivos cliente. También se implementan los parámetros de SCEP. Las solicitudes de SCEP se procesan en el dispositivo cliente. Puede implementar perfiles de certificado para recopilaciones de usuarios o de dispositivos y especificar el almacén de destino de cada certificado. Las reglas de aplicación determinan si los certificados se pueden instalar en el dispositivo. Cuando los perfiles de certificado se implementan en recopilaciones de usuarios, la afinidad de dispositivo de usuario determina el dispositivo del usuario que instala los certificados. Cuando los perfiles de certificado que incluyen certificados de usuario se implementan en recopilaciones de dispositivos, los certificados se instalan en todos los dispositivos primarios de los usuarios de manera predeterminada. Para modificar este comportamiento, instale el certificado en cualquiera de los dispositivos de los usuarios en la página **Inscripción de SCEP** del **Asistente para crear perfil de certificado**. Si los dispositivos son equipos de grupo de trabajo, los certificados de usuario no se implementan.  

## <a name="monitoring-certificate-profiles"></a>Supervisión de perfiles de certificado  

Puede supervisar las implementaciones de perfil de certificado viendo los informes o resultados de cumplimiento. Estos enfoques se describen en [Cómo supervisar perfiles de certificado](/sccm/protect/deploy-use/monitor-certificate-profiles).


## <a name="automatic-revocation-of-certificates"></a>Revocación automática de certificados  
 System Center Configuration Manager revoca automáticamente certificados de usuario y de equipo que se implementaron mediante perfiles de certificado en las circunstancias siguientes:  

- El dispositivo se retira de la administración de System Center Configuration Manager.  

- El dispositivo se borra de forma selectiva.  

- El dispositivo se bloquea de la jerarquía de System Center Configuration Manager.  

  Para revocar los certificados, el servidor de sitio envía un comando de revocación a la entidad de certificación emisora. El motivo de la revocación es **Cese de operación**.  
