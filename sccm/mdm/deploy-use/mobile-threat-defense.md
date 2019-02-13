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
ms.openlocfilehash: 90098dc0243e8513fe78692fe91a8390f7936eba
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56119656"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Administrar el acceso a los recursos de la empresa según el dispositivo, la red y el riesgo de aplicación

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los conectores de Mobile Threat Defense le permiten aprovechar el proveedor de Mobile Threat Defense seleccionado como origen de información para el cumplimiento de directivas y reglas de acceso condicional. Esto le permite agregar un nivel de protección a sus recursos corporativos, como Exchange y Sharepoint, específicamente desde dispositivos móviles en peligro.

> [!Important]  
> Desde el 14 de agosto de 2018, la administración híbrida de dispositivos móviles es una [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para más información, vea [¿Qué es la Administración híbrida de dispositivos móviles (MDM)?](/sccm/mdm/understand/hybrid-mobile-device-management). <!--Intune feature 2683117-->  



## <a name="what-problem-does-this-solve"></a>¿Qué problema soluciona?

Las organizaciones necesitan proteger los datos confidenciales de amenazas emergentes que incluyen amenazas físicas, basadas en la red y en la aplicación, así como vulnerabilidades de sistema operativo.

Históricamente, las organizaciones han sido proactivas a la hora de proteger sus PC contra ataques, pero los dispositivos móviles no se supervisan ni protegen. Las plataformas móviles tienen protección integrada, como el aislamiento de aplicaciones y las tiendas de aplicaciones de cliente supervisadas, pero estas plataformas siguen siendo vulnerables a los ataques sofisticados. Hoy en día, cada vez más empleados usan dispositivos para el trabajo y necesitan acceder a información confidencial. Los dispositivos necesitan estar protegidos contra ataques cada vez más sofisticados.



## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>¿Cómo funcionan los conectores de Mobile Threat Defense para Intune?

El conector protege los recursos de la organización creando un canal de comunicación entre Intune y el proveedor de Mobile Threat Defense elegido. Los asociados de Mobile Threat Defense para Intune ofrecen una forma intuitiva y sencilla de implementar aplicaciones para dispositivos móviles que exploran y analizan activamente la información de amenazas para compartir con Intune. Utilice esta información para fines de creación de informes o cumplimiento. 

Por ejemplo, una aplicación de Mobile Threat Defense conectada informa al proveedor de Mobile Threat Defense de que un dispositivo está conectado actualmente a una red que es vulnerable a ataques de tipo Man-in-the-middle. Esta información se comparte y se clasifica por categorías en función del nivel de riesgo apropiado: bajo, medio o alto. Compare este riesgo con sus asignaciones de nivel de riesgo configuradas en Intune para determinar si se debe revocar el acceso a determinados recursos de su elección mientras el dispositivo está en peligro.



## <a name="sample-scenarios"></a>Escenarios de ejemplo

Cuando un dispositivo se considera infectado por la solución Mobile Threat Defense:

![Dispositivo infectado con Mobile Threat Defense](../media/mtp/MTD-image-1.png)

Se concede acceso cuando el dispositivo se repara:

![Acceso concedido de Mobile Threat Defense](../media/mtp/MTD-image-2.png)



## <a name="next-steps"></a>Pasos siguientes

Aprenda a proteger el acceso a los recursos de la compañía según el riesgo de los dispositivos, la red y las aplicaciones con:

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)
