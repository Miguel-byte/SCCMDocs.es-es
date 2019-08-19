---
title: Reinicialización de la replicación de SQL
titleSuffix: Configuration Manager
description: Use este diagrama para iniciar la solución de problemas de reinicialización de la replicación de SQL entre sitios de Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: ce4a1ca8-6433-4447-819f-19dd5faa6f46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ddc80fe039745930bfd5ecbdfedc5b028849f4d4
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957635"
---
# <a name="sql-replication-reinit"></a>Reinicialización de la replicación de SQL

En una jerarquía de varios sitios, Configuration Manager usa la replicación de SQL para transferir datos entre sitios. Para más información, consulte [Replicación de la base de datos](/sccm/core/plan-design/hierarchy/database-replication).

Use el siguiente diagrama para iniciar la solución de problemas de la reinicialización de la replicación de SQL (reinit):

![Diagrama para solucionar problemas de la reinicialización de la replicación de SQL](media/sql-replication-reinit.svg)

## <a name="queries"></a>Consultas

En este diagrama se usan las siguientes consultas:

### <a name="check-if-site-is-in-maintenance-mode"></a>Comprobar si el sitio está en modo de mantenimiento

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

### <a name="check-which-replication-group-hasnt-completed-reinit"></a>Comprobar qué grupo de replicación no ha completado la reinicialización

```sql
SELECT * FROM RCM_DrsInitializationTracking
WHERE InitializationStatus NOT IN (6,7)
```

### <a name="check-global-data"></a>Comprobar los datos globales

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'GLOBAL'
```

### <a name="check-site-data"></a>Comprobar los datos del sitio

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

## <a name="next-steps"></a>Pasos siguientes

- [Reinicialización de datos globales](/sccm/core/servers/manage/replication/global-data-reinit)
- [Reinicialización de datos de sitio](/sccm/core/servers/manage/replication/site-data-reinit)
- [Configuración de SQL](/sccm/core/servers/manage/replication/sql-configuration)
