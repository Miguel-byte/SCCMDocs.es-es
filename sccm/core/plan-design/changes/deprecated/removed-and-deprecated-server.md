---
title: En desuso para los servidores de sitios de Configuration Manager
titleSuffix: Configuration Manager
description: Obtenga información sobre los productos y los sistemas operativos que System Center Configuration Manager ya no admite para los servidores de sitios.
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b92eb8083ce886fcab4d9957b2a79999d72a1a5a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332770"
---
# <a name="removed-and-deprecated-for-system-center-configuration-manager-site-servers"></a>Elementos eliminados y en desuso de servidores de sitios de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se describen los productos y los sistemas operativos que dejaron de ser compatibles con los servidores de sitios de System Center Configuration Manager o que dejarán de serlo en una actualización futura (en desuso). En este artículo se proporciona información anticipada sobre los cambios futuros que puedan afectar a su uso de Configuration Manager.  

Esta información está sujeta a cambios en versiones futuras y puede no incluir todas las características, productos o sistemas operativos en desuso.  


## <a name="deprecated-server-operating-systems"></a>Sistemas operativos de servidor en desuso  

|**Sistemas operativos**|**Primer anuncio del desuso**|**Soporte eliminado** |  
|-|-|-| 
|Windows Server 2008 R2|10 de julio de 2015| Versión 1702 (vea la nota 1)| 
|Windows Server 2008|10 de julio de 2015|Versión 1511 </br></br>Se quitó la compatibilidad como un sistema de sitio. Vea la nota 2.|  

>[!NOTE]
>-   A partir de la versión 1702, Windows Server 2008 R2 no se admite en servidores de sitios ni en la mayoría de los roles de sistema de sitios. Sin embargo, las versiones anteriores a la 1702 continuarán admitiendo su uso. Este sistema operativo se seguirá admitiendo para el rol de sistema de sitio del punto de distribución (incluidos los puntos de distribución de extracción, así como para el entorno PXE y multidifusión) hasta que se anuncie que la compatibilidad está en desuso o hasta que expire el período extendido de soporte técnico de este sistema operativo. A partir de la versión 1602, puede actualizar in situ el sistema operativo de un servidor de sitio de Windows Server 2008 R2 a Windows Server 2012 R2.  
>- Para obtener más información sobre la actualización local de un sistema operativo de servidores de sitio, consulte la sección [In-place upgrade the operating system of site servers that run Windows Server 2008 R2](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2) (Actualización local del sistema operativo de los servidores del sitio que ejecutan Windows Server 2008 R2) del artículo [Actualizar la infraestructura local que es compatible con System Center Configuration Manager](/sccm/core/servers/manage/upgrade-on-premises-infrastructure).

>[!NOTE]
>-   Windows Server 2008 no se admite para servidores del sitio o roles del sistema de sitio excepto para el punto de distribución y el punto de distribución de extracción. Puede seguir usando este sistema operativo como un punto de distribución hasta que se anuncie que esta compatibilidad queda obsoleta o hasta que expire el período extendido de soporte técnico de este sistema operativo. Para más información, vea [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095) (La instalación de System Center Configuration Manager CB y LTBS produce un error en Windows Server 2008).

## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>Compatibilidad en desuso con versiones de SQL Server como base de datos de sitio  

|**Versiones de SQL Server**|**Primer anuncio del desuso**|**Soporte eliminado**|   
|-|-|-| 
|SQL Server 2008 R2|10 de julio de 2015|Versión 1702| 
|SQL Server 2008|10 de julio de 2015|Versión 1511|  


Si tiene que actualizar la versión de SQL Server, se recomiendan los métodos siguientes, del más sencillo al más complicado.
1. [Realice una actualización local de SQL Server](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recomendado).
2. Instale una nueva versión de SQL Server en un equipo nuevo. Después, [use la opción de mover la base de datos](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) del programa de instalación de Configuration Manager para que el servidor de sitio señale al nuevo servidor SQL Server.
3. Use [Copia de seguridad y recuperación](/sccm/protect/understand/backup-and-recovery).


## <a name="more-information"></a>Más información
Para obtener más información, vea:
 - [Elementos eliminados y en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - Sitio web de la [directiva de ciclos de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle).
 - [Compatibilidad con versiones de la rama actual de Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).