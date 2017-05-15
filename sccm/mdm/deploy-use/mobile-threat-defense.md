---
title: "Restricción del acceso basada en el riesgo | Microsoft Docs"
description: "Restrinja el acceso a los recursos de la empresa según el dispositivo, la red y el riesgo de aplicación."
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: c6a6137fa978e1ea28aefea2aea4e29ba661efd6
ms.openlocfilehash: 250671660c1c6da0ca9b593b06b8f344dfe17ad6
ms.contentlocale: es-es
ms.lasthandoff: 05/04/2017


---

# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Administrar el acceso a los recursos de la empresa según el dispositivo, la red y el riesgo de aplicación

*Se aplica a: System Center Configuration Manager (rama actual)*

Los conectores de Mobile Threat Defense le permiten aprovechar el proveedor de Mobile Threat Defense seleccionado como origen de información para el cumplimiento de directivas y reglas de acceso condicional. Esto permite a los administradores de TI agregar un nivel de protección a sus recursos corporativos, como Exchange y Sharepoint, específicamente desde dispositivos móviles en peligro.

## <a name="what-problem-does-this-solve"></a>¿Qué problema soluciona?

Las compañías necesitan proteger los datos confidenciales de amenazas emergentes que incluyen amenazas físicas, basadas en la red y en la aplicación, así como vulnerabilidades del sistema operativo.
Históricamente, las compañías han sido proactivas a la hora de proteger sus PC contra ataques, pero los dispositivos móviles no se supervisan ni protegen. Las plataformas móviles tienen protección integrada, como el aislamiento de aplicaciones y las tiendas de aplicaciones de cliente supervisadas, pero estas plataformas siguen siendo vulnerables a los ataques sofisticados. Hoy en día, cada vez más empleados usan dispositivos para el trabajo y necesitan acceder a información confidencial. Los dispositivos necesitan estar protegidos contra ataques cada vez más sofisticados.

La [implementación de MDM híbrida (SSCM con Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) le ofrece la posibilidad de controlar el acceso a los recursos de la empresa y a los datos basándose en la evaluación de riesgo que proporcionan soluciones de protección contra amenazas de dispositivo como Mobile Threat Defense.

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>¿Cómo funcionan los conectores de Mobile Threat Defense para Intune?

El conector protege los recursos de la compañía creando un canal de comunicación entre Intune y el proveedor de Mobile Threat Defense elegido. Los asociados de Mobile Threat Defense para Intune ofrecen una forma intuitiva y sencilla de implementar aplicaciones para dispositivos móviles que exploran y analizan activamente la información de amenazas para compartir con Intune, ya sea por motivos de elaboración de informes o de cumplimiento. Por ejemplo, si una aplicación de Mobile Threat Defense conectada informa al proveedor de Mobile Threat Defense de que un teléfono de la red está actualmente conectado a una red que es vulnerable a ataques de tipo “Man in the Middle”, esta información se comparte y se categoriza con un nivel de riesgo apropiado (bajo, medio o alto), que después se puede comparar con sus asignaciones de nivel de riesgo configuradas en Intune para determinar si se debe revocar el acceso a determinados recursos de su elección mientras el dispositivo está en riesgo.

## <a name="sample-scenarios"></a>Escenarios de ejemplo

Cuando un dispositivo se considera infectado por la solución Mobile Threat Defense:

![Dispositivo infectado con Mobile Threat Defense](../media/mtp/MTD-image-1.png)

Se concede acceso cuando el dispositivo se repara:

![Acceso concedido de Mobile Threat Defense](../media/mtp/MTD-image-2.png)

## <a name="next-steps"></a>Pasos siguientes

Aprenda a proteger el acceso a los recursos de la compañía según el riesgo de los dispositivos, la red y las aplicaciones con:

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)
