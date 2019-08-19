---
title: Transferencias de datos entre sitios
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo Configuration Manager mueve datos entre sitios y cómo se puede administrar la transferencia de datos a través de la red.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d9d2a318b6516fef8f5336cd738a3d2517014a4
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957915"
---
# <a name="data-transfers-between-sites"></a>Transferencias de datos entre sitios

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager usa la *replicación basada en archivos* y la *replicación de base de datos* para transferir distintos tipos de información entre sitios. Obtenga información sobre cómo Configuration Manager mueve datos entre sitios y cómo se puede administrar la transferencia de datos a través de la red.  

## <a name="types-of-replication"></a>Tipos de replicación

### <a name="a-namebkmk_fileroute--file-based-replication"></a><a name="bkmk_fileroute" /> Replicación basada en archivos

Configuration Manager usa la replicación basada en archivos para transferir datos basados en archivos entre sitios de la jerarquía. Estos datos incluyen las aplicaciones y los paquetes que quiere implementar en puntos de distribución de sitios secundarios. También controla los registros de datos de detección no procesados que el sitio transfiere a su sitio principal y que posteriormente procesa.  

Para más información, consulte [Replicación basada en archivos](/sccm/core/plan-design/hierarchy/file-based-replication).

### <a name="a-namebkmk_dbrep--database-replication"></a><a name="bkmk_dbrep" /> Replicación de base de datos

La replicación de base de datos de Configuration Manager utiliza SQL Server para transferir datos. Utiliza este método para combinar los cambios en su base de datos de sitio con la información de la base de datos de otros sitios de la jerarquía.

Para más información, consulte [Replicación de la base de datos](/sccm/core/plan-design/hierarchy/database-replication).

Para ayuda con la solución de problemas de replicación de SQL, consulte [Solución de problemas de replicación de SQL](/sccm/core/servers/manage/replication/overview).

## <a name="see-also"></a>Consulte también

[Supervisión de la replicación](/sccm/core/servers/manage/monitor-replication)
