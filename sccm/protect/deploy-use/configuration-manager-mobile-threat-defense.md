---
title: Mobile Threat Defense
titleSuffix: Configuration Manager
description: Restricción del acceso a recursos de la compañía según el riesgo de las aplicaciones, la red y los dispositivos mediante Configuration Manager y asociados de Mobile Threat Defense para Intune
ms.date: 03/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 4c0e6824-2dfe-4700-b817-d5631e0eb872
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6aeed0c7e509ee96b226f5d1c7649bcf84af3af8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="intune-mobile-threat-defense-connectors-in-configuration-manager"></a>Conectores de Mobile Threat Defense para Intune en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La [implementación de MDM híbrida (SCCM con Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) y la integración entre Intune y los asociados de Mobile Threat Defense le proporcionan la capacidad de controlar el acceso a los recursos de la empresa y a los datos basándose en la evaluación de riesgo de los dispositivos.

Los conectores de Mobile Threat Defense para Intune le permiten aprovechar el proveedor de Mobile Threat Defense seleccionado como una fuente de información para el cumplimiento de directivas y reglas de acceso condicional. Esto permite a los administradores de TI agregar un nivel de protección a sus recursos corporativos, como Exchange y Sharepoint, específicamente desde dispositivos móviles en peligro.

## <a name="what-problem-does-this-solve"></a>¿Qué problema soluciona?

Las compañías necesitan proteger los datos confidenciales de amenazas emergentes que incluyen amenazas físicas, basadas en la red y en la aplicación, así como vulnerabilidades del sistema operativo.
Históricamente, las compañías han sido proactivas a la hora de proteger sus PC contra ataques, pero los dispositivos móviles no se supervisan ni protegen. Las plataformas móviles tienen protección integrada, como el aislamiento de aplicaciones y las tiendas de aplicaciones de cliente supervisadas, pero estas plataformas siguen siendo vulnerables a los ataques sofisticados. Hoy en día, cada vez más empleados usan dispositivos para el trabajo y necesitan acceder a información confidencial. Los dispositivos necesitan estar protegidos contra ataques cada vez más sofisticados.

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>¿Cómo funcionan los conectores de Mobile Threat Defense para Intune?

El conector protege los recursos de la compañía creando un canal de comunicación entre Intune y el proveedor de Mobile Threat Defense elegido. Los asociados de Mobile Threat Defense para Intune ofrecen una forma intuitiva y sencilla de implementar aplicaciones para dispositivos móviles que exploran y analizan activamente la información de amenazas para compartir con Intune, ya sea por motivos de elaboración de informes o de cumplimiento. Por ejemplo, si una aplicación de Mobile Threat Defense conectada informa al proveedor de Mobile Threat Defense de que un teléfono de la red está actualmente conectado a una red que es vulnerable a ataques de tipo “Man in the Middle”, esta información se comparte y se categoriza con un nivel de riesgo apropiado (bajo, medio o alto), que después se puede comparar con sus asignaciones de nivel de riesgo configuradas en Intune para determinar si se debe revocar el acceso a determinados recursos de su elección mientras el dispositivo está en riesgo.

## <a name="sample-scenarios"></a>Escenarios de ejemplo

Cuando un dispositivo se considera infectado por la solución Mobile Threat Defense:

![](http://i.imgur.com/Li1WUOU.png)

Se concede acceso cuando el dispositivo se repara:

![](http://i.imgur.com/VCIwpdz.png)

## <a name="mobile-threat-defense-partners"></a>Asociados de Mobile Threat Defense

Aprenda a proteger el acceso a los recursos de la compañía según el riesgo de los dispositivos, la red y las aplicaciones con:

- [Lookout](https://docs.microsoft.com/sccm/protect/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)
