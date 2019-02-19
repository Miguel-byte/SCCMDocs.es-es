---
title: En desuso para servidores de sitio
titleSuffix: Configuration Manager
description: Obtenga información sobre los productos y los sistemas operativos que Configuration Manager ya no admite para los servidores de sitio.
ms.date: 01/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a1a15d803077f183897f182ef162d36896eb238a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126476"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Elementos eliminados y en desuso de los servidores de sitio de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se describen los productos y los sistemas operativos que dejaron de ser compatibles con los servidores de sitio de Configuration Manager o que dejarán de serlo en una actualización futura (en desuso). Se proporcionan notificaciones anticipadas sobre los cambios futuros que es posible que afecten al uso de Configuration Manager.  

Esta información podría cambiar en el futuro. Puede que no incluya cada característica, producto o sistema operativo en desuso.  



## <a name="server-os"></a>SO de servidor  

|**Sistemas operativos**|**Primer anuncio del desuso**|**Soporte eliminado** |  
|-|-|-| 
|Windows Server 2008 R2 con SP1|10 de julio de 2015| Versión 1702 <sup>[Nota 1](#bkmk_note1)</sup>| 
|Windows Server 2008 con SP2|10 de julio de 2015|Versión 1511 <sup>[Nota 2](#bkmk_note2)</sup>|  

#### <a name="bkmk_note1"></a> Nota 1: Windows Server 2008 R2 con SP1
Windows Server 2008 R2 con Service Pack 1 no se admite en servidores de sitio ni en la mayoría de los roles de sistema de sitio. Este sistema operativo todavía se admite para el rol de punto de distribución. Esta compatibilidad incluye puntos de distribución de extracción, PXE y multidifusión. 

> [!Important]  
> La fecha de finalización del soporte técnico extendido para Windows Server 2008 R2 con SP1 es el 14 de enero de 2020. Después de esta fecha, Configuration Manager no será compatible con este SO en ningún rol de sistema de sitio. 

Puede actualizar el sistema operativo del servidor de sitio de Windows Server 2008 R2 a Windows Server 2012 R2. Para más información, vea [Actualización inmediata del sistema operativo de los servidores de sitio que ejecutan Windows Server 2008 R2](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2).  


#### <a name="bkmk_note2"></a> Nota 2: Windows Server 2008 con SP2
Windows Server 2008 con Service Pack 2 no se admite en servidores de sitio ni en la mayoría de los roles de sistema de sitio. Este sistema operativo todavía se admite para el rol de punto de distribución. Esta compatibilidad incluye puntos de distribución de extracción, PXE y multidifusión. 

> [!Important]  
> La fecha de finalización del soporte técnico extendido para Windows Server 2008 con SP2 es el 14 de enero de 2020. Después de esta fecha, Configuration Manager no será compatible con este SO en ningún rol de sistema de sitio.  



## <a name="sql-server"></a>SQL Server   

|**Versiones de SQL Server**|**Primer anuncio del desuso**|**Soporte eliminado**|   
|-|-|-| 
|SQL Server 2008 R2|10 de julio de 2015|Versión 1702| 
|SQL Server 2008|10 de julio de 2015|Versión 1511|  


Si tiene que actualizar la versión de SQL Server, se recomienda seguir estos métodos, del más sencillo al más complicado:

1. [Realice una actualización local de SQL Server](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recomendado).  

2. Instale una nueva versión de SQL Server en un equipo nuevo. Después, para que el servidor de sitio apunte a la nueva instancia de SQL Server, [use la opción de mover la base de datos](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) del programa de instalación de Configuration Manager.  

3. Use [Copia de seguridad y recuperación](/sccm/protect/understand/backup-and-recovery).  



## <a name="more-information"></a>Más información

Vea los siguientes artículos para más información: 

- [Elementos eliminados y en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)  

- [Directiva de ciclo de vida de Microsoft](https://support.microsoft.com/lifecycle)  

- [Compatibilidad con versiones de la rama actual de Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)  

