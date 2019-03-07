---
title: Planear la MDM local
titleSuffix: Configuration Manager
description: Planear la administración de dispositivos móviles local administrar dispositivos móviles en Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bb9349a8c3f107f2da139148e4476537fe6aa7ed
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558089"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Planear la MDM local en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Administración local de dispositivos móviles (MDM) le permite administrar dispositivos móviles mediante las capacidades de administración integradas en el sistema operativo del dispositivo. La función de administración se basa en el estándar de administración de dispositivos (DM) Open Mobile Alliance (OMA) y muchas plataformas de dispositivo usan este estándar para permitir que se administren los dispositivos. Estos dispositivos se denominan *dispositivos modernos* en la documentación y la consola de Configuration Manager. Este término distingue de otros dispositivos que requieren el cliente de Configuration Manager administrarlos.  

Tenga en cuenta los siguientes requisitos antes de preparar la infraestructura de Configuration Manager para controlar la MDM local.



## <a name="bkmk_devices"></a> Dispositivos compatibles  

La rama actual de Configuration Manager admite la inscripción en la administración local de dispositivos móviles para dispositivos con los sistemas operativos siguientes:  
  
- Windows 10 Enterprise  
- Windows 10 Pro  
- Windows 10 Team   
- Windows 10 Mobile  
- Windows 10 Mobile Enterprise
- Windows 10 IoT Enterprise   



##  <a name="bkmk_intune"></a> La suscripción a Microsoft Intune  

Para empezar a usar MDM local, necesita una suscripción a Microsoft Intune. La suscripción solo es necesario para realizar el seguimiento de licencias de los dispositivos y no se usa para administrar o almacenar la información de administración de los dispositivos. Todos los datos de administración se almacena en su organización mediante la infraestructura de Configuration Manager en el entorno local.  

> [!Note]  
> A partir de la versión 1810, una conexión a Intune ya no es necesaria para nuevas implementaciones de MDM local.<!--3607730, fka 1359124--> La organización sigue necesitando licencias de Intune para usar esta característica. Actualmente no se puede quitar la conexión de Intune de las implementaciones de MDM locales existentes. Para más información, vea la [entrada del blog de soporte técnico de Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

Si el sitio tiene dispositivos con conectividad a internet, se puede usar el servicio de Intune para notificar a los dispositivos que busquen el punto de administración de dispositivos para las actualizaciones de directiva. Este comportamiento usa Intune estrictamente para la notificación de dispositivos a través de internet. Dispositivos sin conexiones a internet y no se puede contactar con Intune se basan en el intervalo de sondeo configurado para conectarse con roles de sistema de sitio para las funciones de administración.  

> [!TIP]  
> Antes de configurar los roles de sistema de sitio requeridos, configure la suscripción a Intune. Esta acción minimiza el tiempo necesario para que los roles para que sea funcional.  

Para obtener información sobre cómo configurar la suscripción de Intune, consulte [configurar una suscripción de Microsoft Intune para MDM local](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm).  



##  <a name="bkmk_roles"></a> Roles de sistema de sitio  

En el entorno local MDM requiere al menos uno de los siguientes roles de sistema de sitio:  

- **Punto de proxy de inscripción** para admitir las solicitudes de inscripción.  

- **Punto de inscripción** para admitir la inscripción de dispositivos.  

- **Punto de administración de dispositivos** para la entrega de directivas. Este rol de sistema de sitio es una variación del rol de punto de administración que se ha configurado para permitir la administración de dispositivos móviles.  

- **Punto de distribución** para la entrega de contenido.  

- **Punto de conexión de servicio** para conectarse a Intune para notificar a los dispositivos que están fuera del firewall.  

Estos roles de sistema de sitio se pueden instalar en el servidor de sistema de sitio único o se pueden ejecutar por separado en diferentes servidores según las necesidades de su organización. Cada servidor de sistema de sitio que usa para MDM local debe configurarse como un extremo HTTPS para comunicarse con dispositivos de confianza. Para obtener más información, vea [Comunicaciones de confianza requeridas](#bkmk_trustedComs).  

Para obtener más información sobre la planeación para roles de sistema de sitio, consulte [Plan para funciones y los servidores de sistema de sitio de Configuration Manager](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles).  

Para obtener más información sobre cómo agregar los roles de sistema de sitio requeridos, consulte [instalar roles de sistema de sitio para MDM local](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm).  



##  <a name="bkmk_trustedComs"></a> Comunicaciones de confianza  

MDM local requiere roles de sistema de sitio se habiliten para comunicaciones HTTPS. Según sus necesidades, puede usar para establecer las conexiones de confianza entre servidores y dispositivos de certificación de su empresa (CA). También puede usar una entidad de certificación disponible públicamente para ser la autoridad de confianza. En cualquier caso, necesita un certificado de servidor web se deben configurar en IIS en los servidores de sistema de sitio que hospeda los roles de sistema de sitio requeridos. También necesita el certificado raíz de CA instalada en los dispositivos que necesitan conectarse a esos servidores.  

Si usa entidad de certificación de su empresa para establecer comunicaciones de confianza, realice las siguientes tareas:  

- Crear y emitir la plantilla de certificado de servidor web en la entidad de certificación.  

- Solicitar un certificado de servidor web por cada servidor de sistema de sitio que hospede un rol de sistema de sitio.  

- Configurar IIS en el servidor de sistema de sitio para que use el certificado de servidor web solicitado.  

Para dispositivos unidos al dominio de Active Directory corporativo, el certificado raíz de la entidad de certificación de la empresa ya está disponible en el dispositivo para las conexiones de confianza. Este comportamiento significa que se confía automáticamente para las conexiones HTTPS con los servidores de sistema de sitio en dispositivos Unidos a dominio. Sin embargo, los dispositivos no unidos a dominio no obtienen automáticamente el certificado raíz necesario instalado. Para comunicarse correctamente con los servidores de sistema de sitio que admiten MDM local, los dispositivos no unidos a dominio como dispositivos móviles requieren que instale manualmente el certificado raíz en ellos.  

Exporte el certificado raíz de la CA emisora para su uso por dispositivos individuales. Para obtener el archivo de certificado raíz, puede exportarlo con la entidad de certificación. Otro método es usar el certificado de servidor web emitido por la entidad de certificación para extraer la raíz y crear un archivo de certificado raíz. A continuación, el certificado raíz se debe entregar al dispositivo. Algunos métodos de entrega de ejemplo incluyen:

- Sistema de archivos  

- Datos adjuntos de correo electrónico  

- Tarjeta de memoria  

- Dispositivo anclado a red  

- Almacenamiento en la nube (por ejemplo, OneDrive)  

- Conexión NFC (transmisión de datos en proximidad)  

- Escáner de códigos de barras  

- Paquete de aprovisionamiento de configuración rápida (OOBE)  

Para obtener más información, consulte [configurar certificados para comunicaciones de confianza en MDM local](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  



##  <a name="bkmk_enrollment"></a> Inscripción de dispositivos

Para habilitar la inscripción de dispositivos para MDM local,
- Los usuarios deben tener permiso para inscribir 
- Dispositivos deben configurarse para permitir comunicaciones de confianza con los servidores de sistema de sitio que hospeda los roles necesarios  

Conceder a los usuarios permisos para inscribir dispositivos mediante la configuración de un perfil de inscripción en la configuración de cliente de Configuration Manager. Puede usar la configuración de cliente predeterminada para insertar el perfil de inscripción en todos los usuarios detectados. También puede configurar el perfil de inscripción en la configuración de cliente personalizada y la configuración de inserción en una o varias recopilaciones de usuarios.  

Una vez que los usuarios tienen permiso, pueden inscribir sus dispositivos. Para realizar la inscripción, el dispositivo del usuario debe tener el certificado raíz de la entidad de certificación (CA) que emitió el certificado de servidor web utilizado en los servidores de sistema de sitio que hospeda los roles necesarios.  

Como alternativa a la inscripción iniciada por el usuario, puede configurar un paquete de inscripción masiva. Este paquete permite que el dispositivo se inscriba sin intervención del usuario. Puede entregar al dispositivo antes de aprovisionar para su uso o cuando el dispositivo pasa a través de su proceso de OOBE.  

Para obtener más información sobre cómo configurar e inscribir dispositivos, consulte los artículos siguientes: 

- [Configurar la inscripción de dispositivos para MDM local](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

- [Inscribir dispositivos en MDM local](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  

