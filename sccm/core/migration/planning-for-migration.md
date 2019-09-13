---
title: Planeamiento de la migración
titleSuffix: Configuration Manager
description: Obtenga información sobre sitios y jerarquías antes de migrar datos a una jerarquía de destino de System Center Configuration Manager.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 286378fd354375fcf52030b0b27ed41802524bfa
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70891507"
---
# <a name="plan-for-migration-to-system-center-configuration-manager"></a>Planear la migración a System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Antes de migrar datos a una jerarquía de destino de System Center Configuration Manager, asegúrese de estar familiarizado con las jerarquías y los sitios de Configuration Manager. Para más información sobre sitios y jerarquías, vea [Aspectos básicos de System Center Configuration Manager](../../core/understand/fundamentals.md).  

 Debe instalar una jerarquía de System Center Configuration Manager que sea la jerarquía de destino para poder migrar datos desde una jerarquía de origen admitida.  

 Después de instalar la jerarquía de destino, configure las funciones y características de administración que quiera usar en la jerarquía de destino antes de empezar a migrar los datos.  

 Además, tendrá que planear la superposición entre la jerarquía de origen y la jerarquía de destino. Por ejemplo, podría configurar la jerarquía de origen para usar los mismos límites o ubicaciones de red que la jerarquía de destino. Luego podría instalar nuevos clientes en la jerarquía de destino y usar la asignación automática de sitios. En este escenario, debido a que un cliente de Configuration Manager recién instalado puede seleccionar un sitio de cualquier jerarquía al que unirse, el cliente podría asignarse incorrectamente a su jerarquía de origen. Por lo tanto, planee la asignación de cada cliente nuevo en la jerarquía de destino a un sitio específico en dicha jerarquía en lugar de usar la asignación automática de sitios.  

 Para más información sobre las asignaciones de sitio, vea [Consideraciones sobre la asignación de sitio de cliente](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) en [Interoperabilidad entre diferentes versiones de System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

## <a name="plan-topics"></a>Temas para planear  
 Use los temas siguientes para planear la migración de una jerarquía de origen a una jerarquía de destino de System Center Configuration Manager:

-   [Requisitos previos para la migración en System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md)  

-   [Listas de comprobación de administrador para planear la migración en System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Determinar si se migrarán datos a System Center Configuration Manager](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Planear una estrategia de jerarquía de origen en System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Listas de comprobación de administrador para planear la migración en System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Planear una estrategia de migración de clientes en System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Planear una estrategia de migración de implementación de contenido en System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Planear la migración de objetos de Configuration Manager a System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Planear la supervisión de la actividad de migración en System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Planear la finalización de la migración en System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md)  
