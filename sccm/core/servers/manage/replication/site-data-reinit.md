---
title: Reinicialización de datos de sitio
titleSuffix: Configuration Manager
description: Use este diagrama para iniciar la solución de problemas de reinicialización de la replicación de SQL para datos de sitio en una jerarquía de Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 19741d45-2d42-438e-a9f3-15bb365d63ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ed35f296b888d9e13d42114aa2bef2932c715a38
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70892052"
---
# <a name="troubleshoot-site-data-reinit"></a>Solución de problemas de reinicialización de datos de sitio

En una jerarquía de varios sitios, Configuration Manager usa la replicación de SQL para transferir datos entre sitios. Para más información, consulte [Replicación de la base de datos](/sccm/core/plan-design/hierarchy/database-replication).

Use el siguiente diagrama para iniciar la solución de problemas de reinicialización (reinit) de la replicación de SQL para datos de sitio en una jerarquía de Configuration Manager:

![Diagrama para solucionar problemas de reinicialización de datos de sitio](media/site-data-reinit.svg)

## <a name="queries"></a>Consultas

En este diagrama se usan las siguientes consultas:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Comprobar si la replicación del sitio no ha finalizado la reinicialización

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Site'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>Obtener el GUID de seguimiento y el estado desde CAS

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>Obtener el GUID de seguimiento y el estado desde el sitio primario

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-primary-site-isnt-in-maintenance-mode"></a>Comprobar que el sitio primario no está en modo de mantenimiento

```sql
SELECT * FROM ServerData
WHERE SiteStatus = 125
AND SiteCode=dbo.fnGetSiteCode()
AND ServerRole=N'Peer'
```

### <a name="check-request-status-for-the-tracking-id"></a>Comprobar el estado de la solicitud para el identificador de seguimiento

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Pasos siguientes

- [Mensaje de que falta reinicialización](/sccm/core/servers/manage/replication/reinit-missing-message)
- [Reinicialización de datos globales](/sccm/core/servers/manage/replication/global-data-reinit)
