---
title: Configuración de SQL
titleSuffix: Configuration Manager
description: Use este diagrama para iniciar la solución de problemas de configuración de SQL para Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 95ab8cbd-0807-4422-823a-f5f9314ba623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 515f3ef86dff0d60f16aa908759e785a4c8e4e0b
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957625"
---
# <a name="sql-configuration"></a>Configuración de SQL

En una jerarquía de varios sitios, Configuration Manager usa la replicación de SQL para transferir datos entre sitios. Para más información, consulte [Replicación de la base de datos](/sccm/core/plan-design/hierarchy/database-replication).

Use el siguiente diagrama para iniciar la solución de problemas de la configuración de SQL relacionados con SQL Service Broker:

![Diagrama para solucionar problemas de configuración de SQL](media/sql-configuration.svg)

## <a name="queries"></a>Consultas

Este diagrama tiene las siguientes consultas y acciones:

### <a name="check-if-sql-can-deliver-ssb-messages"></a>Comprobar si SQL puede entregar mensajes SSB

```sql
SELECT transmission_status, *
FROM sys.transmission_queue
ORDER BY enqueue_time DESC
```

## <a name="remediation-actions"></a>Acciones correctivas

### <a name="remediate-the-issues-reported-from-transmission_status"></a>Corregir los problemas notificados de transmission_status

Problemas comunes:

- Configuración de firewall
- Configuración de red
- Certificado SSB mal configurado

### <a name="run-sql-profiler-to-trace-ssb-events"></a>Ejecución del generador de perfiles de SQL para realizar el seguimiento de eventos SSB

Ejecute el generador de perfiles de SQL en la base de datos del sitio primario y CAS para realizar un seguimiento de los eventos relacionados con SQL Service Broker:

- **Auditar el inicio de sesión de Broker**
- **Auditar la conversación de Broker**
- Eventos en la categoría **Broker**
