---
title: Replicación de SQL
titleSuffix: Configuration Manager
description: Use este diagrama para iniciar la solución de problemas de replicación de SQL entre sitios de Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: adb198c4-da3c-49c3-8fbd-6d1361272869
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35c807010e821f5a9857e7cc9d18354db5758298
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957745"
---
# <a name="sql-replication"></a>Replicación de SQL

En una jerarquía de varios sitios, Configuration Manager usa la replicación de SQL para transferir datos entre sitios. Para más información, consulte [Replicación de la base de datos](/sccm/core/plan-design/hierarchy/database-replication).

Use el siguiente diagrama para iniciar la solución de problemas de la replicación de SQL cuando un vínculo da error:

![Diagrama para solucionar problemas de replicación de SQL](media/sql-replication.svg)

## <a name="queries"></a>Consultas

En este diagrama se usan las siguientes consultas:

### <a name="check-if-the-replication-group-link-is-in-degraded-or-failed-state"></a>Comprobar si el vínculo del grupo de replicación está en estado degradado o con errores

```sql
SELECT * FROM RCM_ReplicationLinkStatus
WHERE Status IN (8, 9)
```

### <a name="check-if-replication-group-link-is-recently-calculated"></a>Comprobar si el vínculo del grupo de replicación se calculó recientemente

```sql
DECLARE @cutoffTime DATETIME
SELECT @cutoffTime = DATEADD(minute, -30, GETUTCDATE())
SELECT * FROM RCM_ReplicationLinkStatus
WHERE UpdateTime >@cutoffTime
```

### <a name="check-sql-maintenance-mode"></a>Comprobar el modo de mantenimiento de SQL

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

## <a name="next-steps"></a>Pasos siguientes

- [Reinicialización de replicación de SQL (reinit)](/sccm/core/servers/manage/replication/sql-replication-reinit)
- [Rendimiento de SQL](/sccm/core/servers/manage/replication/sql-performance)
- [Configuración de SQL](/sccm/core/servers/manage/replication/sql-configuration)
