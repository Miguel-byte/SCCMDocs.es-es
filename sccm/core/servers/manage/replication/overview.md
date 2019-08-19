---
title: Solución de problemas de replicación de SQL
titleSuffix: Configuration Manager
description: Use estos diagramas para ayudar a comprender y solucionar problemas de la replicación de SQL entre sitios Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e4f1506ce7931fdb95a447695fbd9bf0c12146e0
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957805"
---
# <a name="troubleshoot-sql-replication"></a>Solución de problemas de replicación de SQL

En una jerarquía de varios sitios, Configuration Manager usa la replicación de SQL para transferir datos entre sitios. Para más información, consulte [Replicación de la base de datos](/sccm/core/plan-design/hierarchy/database-replication).

Para comprender mejor al solución de problemas con la replicación de SQL, use estos diagramas.

- [Replicación de SQL](/sccm/core/servers/manage/replication/sql-replication)
- [Configuración de SQL](/sccm/core/servers/manage/replication/sql-configuration)
- [Rendimiento de SQL](/sccm/core/servers/manage/replication/sql-performance)
- [Reinicialización de replicación de SQL (reinit)](/sccm/core/servers/manage/replication/sql-replication-reinit)
- [Reinicialización de datos globales](/sccm/core/servers/manage/replication/global-data-reinit)
- [Reinicialización de datos de sitio](/sccm/core/servers/manage/replication/site-data-reinit)
- [Mensaje de que falta reinicialización](/sccm/core/servers/manage/replication/reinit-missing-message)

Estos diagramas de solución de problemas están interconectados. Use el siguiente diagrama para entender sus relaciones:

![Diagrama de información general del proceso para solucionar problemas de replicación de SQL](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

Para más información, vea la siguiente serie de blogs de Soporte técnico de Microsoft:

- [Mecanismos de sincronización de DRS de Configuration Manager](https://blogs.technet.microsoft.com/umairkhan/2019/06/01/configmgr-drs-synchronization-internals/)
- [Servicio de replicación de datos (DRS) de Configuration Manager 2012 sin límites](https://blogs.technet.microsoft.com/umairkhan/2014/02/17/configmgr-2012-data-replication-service-drs-unleashed/)
- [DRS de Configuration Manager 2012: preguntas más frecuentes sobre la solución de problemas](https://blogs.technet.microsoft.com/umairkhan/2014/03/24/configmgr-2012-drs-troubleshooting-faqs/)
- [Mecanismos de inicialización de DRS de Configuration Manager 2012](https://blogs.technet.microsoft.com/umairkhan/2015/01/21/configmgr-2012-drs-initialization-internals/)
- [Configuration Manager 2012: problemas de certificado de SQL Server Service Broker y DRS](https://blogs.technet.microsoft.com/umairkhan/2013/12/12/configmgr-2012-drs-and-sql-service-broker-certificate-issues/)
