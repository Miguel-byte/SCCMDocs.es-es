---
title: "Restricción del acceso basada en el riesgo | Microsoft Docs"
description: "Restrinja el acceso a los recursos de la empresa según el dispositivo, la red y el riesgo de aplicación."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: d2925e9ba8faacceb13520605e71bf9c4a84c302
ms.lasthandoff: 03/06/2017


---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Administrar el acceso a los recursos de la empresa según el dispositivo, la red y el riesgo de aplicación

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede controlar el acceso desde dispositivos móviles a recursos corporativos, basándose en la evaluación de riesgo dirigida por Lookout; una solución de protección contra amenazas de dispositivo que se integra en Microsoft Intune. El riesgo se basa en la telemetría que recopila el servicio de Lookout de los dispositivos para las vulnerabilidades de sistema operativo (SO), aplicaciones malintencionadas instaladas y perfiles de red malintencionados. 

Basándose en la evaluación de riesgos que Lookout ha notificado que se ha habilitado mediante las directivas de cumplimiento de System Center Configuration Manager (SCCM), puede configurar directivas de acceso condicional y permitir o bloquear los dispositivos que se han determinado como no conformes debido a las amenazas detectadas en ellos.  

## <a name="what-problem-does-this-solve"></a>¿Qué problema soluciona?
Las empresas y las organizaciones necesitan proteger los datos confidenciales de amenazas emergentes que incluyen amenazas físicas, basadas en la red y en la aplicación, así como vulnerabilidades de sistema operativo.

Históricamente, las empresas y las organizaciones han adoptado una posición activa para proteger los equipos contra los ataques malintencionados. Los dispositivos móviles son un área emergente que a menudo no está protegida. Aunque las plataformas móviles tienen protección integrada del sistema operativo con técnicas como el aislamiento de aplicaciones y las tiendas de aplicaciones de cliente supervisadas, estas plataformas siguen siendo vulnerables a los ataques sofisticados. Como los empleados usan cada vez más los dispositivos móviles para trabajar y necesitan acceder a información que puede ser confidencial y valiosa, estos dispositivos necesitan protegerse de una variedad de ataques sofisticados.

La [implementación de MDM híbrida (SSCM con Intune)](https://docs.microsoft.com/en-us/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) le proporciona la capacidad de controlar el acceso a los recursos de la empresa y a los datos basándose en la evaluación de riesgo que proporcionan soluciones de protección contra amenazas de dispositivo como Lookout.

## <a name="how-do-the-hybrid-mdm-deployment-and-lookout-device-threat-protection-help-protect-company-resources"></a>¿Cómo ayudan la implementación de MDM híbrida y la protección contra amenazas de dispositivo de Lookout a proteger los recursos de la empresa?
La aplicación móvil de Lookout (Lookout for Work), que se ejecuta en dispositivos móviles, captura el sistema de archivos, la pila de red, la telemetría de aplicaciones y dispositivos (si está disponible) y lo envía al servicio en la nube de protección contra amenazas de dispositivo de Lookout para calcular un riesgo de dispositivo agregado para las amenazas móviles. También puede cambiar la clasificación del nivel de riesgo de las amenazas en la consola de Lookout para que se adapte a sus necesidades.  

La directiva de cumplimiento en SCCM ahora incluye una nueva regla para Lookout Mobile Threat Protection que se basa en la evaluación de riesgo de amenazas de dispositivo de Lookout. Cuando esta regla está habilitada, el dispositivo se evalúa para su cumplimiento.

Si se determina que el dispositivo es no conforme con la directiva de cumplimiento, el acceso a recursos como Exchange Online y SharePoint Online puede bloquearse con las directivas de acceso condicional. Cuando el acceso se bloquea, a los usuarios finales se les proporciona un tutorial para ayudarles a resolver el problema y obtener acceso a los recursos de la empresa. Este tutorial se inicia con la aplicación de Lookout for Work.

## <a name="supported-platforms"></a>Plataformas compatibles:
* **Android 4.1 y versiones posteriores**, y con inscripción en Microsoft Intune.
* **iOS 8 y versiones posteriores**, y con inscripción en Microsoft Intune.
Para obtener información sobre las plataformas y los idiomas que se admiten en Lookout, consulte este [artículo](https://personal.support.lookout.com/hc/en-us/articles/114094140253).

## <a name="prerequisites"></a>Requisitos previos:
* [Implementación de MDM híbrida](https://docs.microsoft.com/en-us/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)
* Una suscripción a Microsoft Intune y Azure Active Directory.
* Una suscripción de empresa a Lookout Mobile EndPoint Security.  Para obtener más información, consulte [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security).

## <a name="example-scenarios"></a>Escenarios de ejemplo
A continuación se muestran algunos escenarios comunes:
### <a name="control-access-based-on-threat-from-malicious-apps"></a>Controlar el acceso basándose en amenazas de aplicaciones malintencionadas:
Cuando las aplicaciones malintencionadas, como malware, se detectan en el dispositivo, puede impedir que estos dispositivos:
* Se conecten al correo electrónico de la empresa antes de resolver la amenaza.
* Sincronicen archivos corporativos con la aplicación OneDrive para el trabajo.
* Tengan acceso a las aplicaciones esenciales de la empresa.

**Acceso bloqueado cuando se detectan aplicaciones malintencionadas:**

![Diagrama que muestra una directiva de acceso condicional bloqueando el acceso cuando se determina que un dispositivo es no conforme debido a aplicaciones malintencionadas en el dispositivo](media/config-mgr-maliciousapps_blocked.png)

**Dispositivo desbloqueado y que puede tener acceso a los recursos de la empresa cuando se corrige la amenaza:**

![Diagrama que muestra la directiva de acceso condicional concediendo acceso cuando se determina que el dispositivo es conforme después de la corrección](media/config-mgr-maliciousapps-unblocked.png)
### <a name="control-access-based-on-threat-to-network"></a>Controlar el acceso basándose en amenazas en la red:
Detecte amenazas en la red como ataques de tipo "Man in the middle" y restrinja el acceso a redes Wi-Fi en función del riesgo del dispositivo.

**Acceso bloqueado a la red mediante Wi-Fi:**

![Diagrama que muestra el acceso condicional bloqueando el acceso de Wi-Fi basándose en amenazas de red](media/config-mgr-network-wifi-blocked.png)

**Acceso concedido tras la corrección:**

![Diagrama que muestra el acceso condicional permitiendo el acceso tras la corrección de la amenaza](media/config-mgr-network-wifi-unblocked.png)
### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar el acceso a SharePoint Online basándose en amenazas en la red:

Detecte amenazas en la red como ataques de tipo "Man in the middle" e impida la sincronización de archivos corporativos en función del riesgo del dispositivo.

**Acceso bloqueado a SharePoint Online basándose en una amenaza de red detectada en el dispositivo:**

![Diagrama que muestra el acceso condicional bloqueando el acceso del dispositivo a SharePoint Online basándose en la detección de amenazas](media/config-mgr-network-spo-blocked.png)


**Acceso concedido tras la corrección:**

![Diagrama que muestra el acceso condicional permitiendo el acceso después de que la amenaza de red se haya corregido](media/config-mgr-network-spo-unblocked.png)

## <a name="next-steps"></a>Pasos siguientes
Aquí se muestran los pasos principales que debe realizar para implementar esta solución:
1.    [Set up your subscription with Lookout mobile threat protection (Configurar su suscripción con Lookout Mobile Threat Protection)](set-up-your-subscription-with-lookout.md)
2.    [Enable Lookout MTP connection in Intune (Habilitar la conexión de Lookout MTP en Intune)](enable-lookout-connection-in-intune.md)
3.  [Configure and deploy Lookout for work application (Configurar e implementar la aplicación Lookout for Work)](configure-and-deploy-lookout-for-work-apps.md)
4.    [Configure compliance policy (Configurar directiva de cumplimiento)](enable-device-threat-protection-rule-compliance-policy.md)
5.    [Solucionar problemas de integración de Lookout](troubleshoot-lookout-integration.md)

