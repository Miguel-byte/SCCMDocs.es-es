---
title: Reinicialización de datos globales
titleSuffix: Configuration Manager
description: Use este diagrama para iniciar la solución de problemas de reinicialización de la replicación de SQL para datos globales en una jerarquía de Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: d36622c0-776c-493b-971a-4a586fc394d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 646a8c93b3bc5f90d711e6985983a41d87c38826
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70892088"
---
# <a name="troubleshoot-global-data-reinit"></a>Solución de problemas de reinicialización de datos globales

En una jerarquía de varios sitios, Configuration Manager usa la replicación de SQL para transferir datos entre sitios. Para más información, consulte [Replicación de la base de datos](/sccm/core/plan-design/hierarchy/database-replication).

Use el siguiente diagrama para iniciar la solución de problemas de reinicialización (reinit) de la replicación de SQL para datos globales en una jerarquía de Configuration Manager:

![Diagrama para solucionar problemas de reinicialización de datos globales](media/global-data-reinit.svg)

## <a name="queries"></a>Consultas

En este diagrama se usan las siguientes consultas:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Comprobar si la replicación del sitio no ha finalizado la reinicialización

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>Obtener el GUID de seguimiento y el estado desde el sitio primario

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>Obtener el GUID de seguimiento y el estado desde CAS

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-request-status-for-the-tracking-id"></a>Comprobar el estado de la solicitud para el identificador de seguimiento

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Pasos siguientes

- [Mensaje de que falta reinicialización](/sccm/core/servers/manage/replication/reinit-missing-message)
