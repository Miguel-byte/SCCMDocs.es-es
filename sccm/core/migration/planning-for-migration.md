---
title: "Planear la migración | System Center Configuration Manager"
description: "Obtenga información sobre sitios y jerarquías antes de migrar datos a una jerarquía de destino de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a80c7af58f88f76afd00771778411a4842a204c8


---
# <a name="planning-for-migration-to-system-center-configuration-manager"></a>Planear la migración a System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Antes de migrar datos a una jerarquía de destino de System Center Configuration Manager, asegúrese de estar familiarizado con las jerarquías y los sitios de Configuration Manager. Para obtener más información sobre sitios y jerarquías, consulte [Fundamentals of System Center Configuration Manager (Conceptos básicos de System Center Configuration Manager)](../../core/understand/fundamentals.md).  

 Primero debe instalar una jerarquía de System Center Configuration Manager que sea la jerarquía de destino para poder migrar datos desde una jerarquía de origen admitida.  

 Después de instalar la jerarquía de destino, configure las funciones y características de administración que desee utilizar en su jerarquía de destino antes de empezar a migrar los datos.  

 Además, tendrá que planear la superposición entre la jerarquía de origen y la jerarquía de destino. Como ejemplo, suponga que la jerarquía de origen está configurada para utilizar los mismos límites o ubicaciones de red que la jerarquía de destino. A continuación, instala nuevos clientes en la jerarquía de destino y utiliza la asignación automática de sitios. En este escenario, debido a que un cliente de Configuration Manager recién instalado puede seleccionar un sitio de cualquier jerarquía al que unirse, el cliente podría asignarse incorrectamente a su jerarquía de origen. Por lo tanto, planifique la asignación de cada cliente nuevo en la jerarquía de destino a un sitio específico en dicha jerarquía en lugar de utilizar la asignación automática de sitios.  

 Para obtener más información sobre las asignaciones de sitio, consulte la sección [Consideraciones sobre la asignación de sitio de cliente](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) del tema [Interoperabilidad entre las diferentes versiones de System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

## <a name="planning-topics"></a>Temas de planeación  
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



<!--HONumber=Nov16_HO1-->


