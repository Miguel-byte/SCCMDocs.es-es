---
title: Restricción del acceso basado en el riesgo
titleSuffix: Configuration Manager
description: Restrinja el acceso a los recursos de la empresa según el dispositivo, la red y el riesgo de aplicación.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50d79da3ab4e7ace9a682baaa5cfd8d2bdbdce10
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678867"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Administrar el acceso a los recursos de la empresa según el dispositivo, la red y el riesgo de aplicación

*Se aplica a: System Center Configuration Manager (Rama actual)*

Controle el acceso desde dispositivos móviles a recursos corporativos en función de la evaluación de riesgos efectuada por Lookout. Lookout es una solución de protección contra amenazas de dispositivos integrada con Microsoft Intune. El riesgo se basa en los datos recopilados por el servicio de Lookout. Recopila datos de dispositivos para comprobar si hay vulnerabilidades del sistema operativo, aplicaciones malintencionadas instaladas y perfiles de red malintencionados. 

En función de la evaluación de riesgos notificada por Lookout y habilitada a través de las directivas de cumplimiento de Configuration Manager, se configuran las directivas de acceso condicional. Estas directivas permiten o bloquean dispositivos que Configuration Manager determina como no conformes debido a las amenazas detectadas en ellos.

> [!Important]  
> Desde el 14 de agosto de 2018, la administración híbrida de dispositivos móviles es una [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para más información, vea [¿Qué es la Administración híbrida de dispositivos móviles (MDM)?](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="how-does-it-work"></a>Cómo funciona

¿Cómo ayudan la implementación de MDM híbrida y la protección contra amenazas de dispositivo de Lookout a proteger los recursos de la empresa?

La aplicación móvil de Lookout (Lookout for Work) se ejecuta en dispositivos móviles. Captura el sistema de archivos, la pila de red y los datos de uso del dispositivo y de la aplicación cuando estén disponibles. La aplicación envía estos datos al servicio en la nube de protección de amenazas de dispositivos de Lookout para calcular un riesgo de dispositivo agregado para amenazas móviles. Use la consola de Lookout para cambiar la clasificación del nivel de riesgo de las amenazas para que se adapte a sus necesidades.  

La directiva de cumplimiento en Configuration Manager ahora incluye una nueva regla para Lookout Mobile Threat Protection que se basa en la evaluación de riesgo de amenazas de dispositivo de Lookout. Al habilitar esta regla, Configuration Manager evalúa el cumplimiento del dispositivo.

Si el dispositivo no está conforme con la directiva de cumplimiento, puede bloquear el acceso a recursos como Exchange Online y SharePoint Online con las directivas de acceso condicional. Cuando el acceso se bloquea, el usuario final recibe un tutorial para ayudarle a resolver el problema y obtener acceso a los recursos de la empresa. El usuario inicia este tutorial a través de la aplicación Lookout for Work.



## <a name="supported-platforms"></a>Plataformas admitidas

- **Android 4.1 y versiones posteriores**, y con inscripción en Microsoft Intune.  

- **iOS 8 y versiones posteriores**, y con inscripción en Microsoft Intune.  


Para obtener información sobre las plataformas y los idiomas que se admiten en Lookout, consulte este [artículo de soporte de Lookout](https://personal.support.lookout.com/hc/articles/114094140253).



## <a name="prerequisites"></a>Requisitos previos

- [MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management)  

- Una suscripción a Microsoft Intune y Azure Active Directory.  

- Una suscripción de empresa a Lookout Mobile EndPoint Security. Para obtener más información, consulte [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security).  



## <a name="example-scenarios"></a>Escenarios de ejemplo


### <a name="control-access-based-on-threat-from-malicious-apps"></a>Control del acceso basándose en amenazas de aplicaciones malintencionadas

Cuando las aplicaciones malintencionadas, como malware, se detectan en el dispositivo, puede impedir que estos dispositivos:

- Se conecten al correo electrónico de la empresa antes de resolver la amenaza.  

- Sincronicen archivos corporativos con la aplicación OneDrive para el trabajo.  

- Tengan acceso a las aplicaciones esenciales de la empresa.  

#### <a name="access-blocked-when-malicious-apps-are-detected"></a>Acceso bloqueado cuando se detectan aplicaciones malintencionadas

![Directiva de acceso condicional que bloquea el acceso cuando se detectan aplicaciones malintencionadas](media/config-mgr-maliciousapps_blocked.png)

#### <a name="device-unblocked-and-is-able-to-access-company-resources-when-the-threat-is-remediated"></a>Dispositivo desbloqueado y que puede tener acceso a los recursos de la empresa cuando se corrige la amenaza

![Directiva de acceso condicional que concede acceso cuando el dispositivo está conforme](media/config-mgr-maliciousapps-unblocked.png)


### <a name="control-access-based-on-threat-to-network"></a>Controlar el acceso basándose en amenazas en la red

Detecte amenazas en la red como ataques de tipo "Man in the middle" y restrinja el acceso a redes Wi-Fi en función del riesgo del dispositivo.

#### <a name="access-to-network-through-wifi-blocked"></a>Acceso bloqueado a la red mediante Wi-Fi

![Acceso condicional bloqueando el acceso de Wi-Fi basándose en amenazas de red](media/config-mgr-network-wifi-blocked.png)

#### <a name="access-granted-on-remediation"></a>Acceso concedido tras la corrección

![Acceso condicional que permite el acceso tras la corrección de la amenaza](media/config-mgr-network-wifi-unblocked.png)


### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar el acceso a SharePoint Online basándose en amenazas en la red

Detecte amenazas en la red como ataques de tipo "Man in the middle" e impida la sincronización de archivos corporativos en función del riesgo del dispositivo.

#### <a name="access-blocked-sharepoint-online-based-on-network-threat-detected-on-the-device"></a>Acceso bloqueado a SharePoint Online basándose en una amenaza de red detectada en el dispositivo

![Acceso condicional que bloquea el acceso del dispositivo a SharePoint Online](media/config-mgr-network-spo-blocked.png)


#### <a name="access-granted-on-remediation"></a>Acceso concedido tras la corrección

![Acceso condicional que permite el acceso después de que la amenaza de red se haya corregido](media/config-mgr-network-spo-unblocked.png)



## <a name="next-steps"></a>Pasos siguientes

Para implementar esta solución, siga estos pasos:  

1. [Set up your subscription with Lookout mobile threat protection (Configurar su suscripción con Lookout Mobile Threat Protection)](set-up-your-subscription-with-lookout.md)
2. [Enable Lookout MTP connection in Intune (Habilitar la conexión de Lookout MTP en Intune)](enable-lookout-connection-in-intune.md)
3.  [Configure and deploy Lookout for work application (Configurar e implementar la aplicación Lookout for Work)](configure-and-deploy-lookout-for-work-apps.md)
4. [Configure compliance policy (Configurar directiva de cumplimiento)](enable-device-threat-protection-rule-compliance-policy.md)
5. [Solucionar problemas de integración de Lookout](troubleshoot-lookout-integration.md)
