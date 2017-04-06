---
title: Requisitos previos de los informes | Microsoft Docs
description: Analice varias dependencias que afectan al uso de los informes en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
caps.latest.revision: 5
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 70034213442f4c3d5a28ab65c2ceb51aa64320ad
ms.openlocfilehash: 2e624eb2ea061a4eb7d92365410fada335640224
ms.lasthandoff: 03/31/2017


---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>Requisitos previos de los informes en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

La generación de informes en System Center Configuration Manager tiene dependencias externas y dependencias dentro del producto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependencias externas a Configuration Manager  
 La tabla siguiente muestra las dependencias externas de los informes.  

|Requisito previo|Más información|  
|------------------|----------------------|  
|SQL Server Reporting Services|Para poder usar los informes en Configuration Manager, debe instalar y configurar SQL Server Reporting Services.<br /><br /> Para obtener información acerca de cómo planificar e implementar Reporting Services en su entorno, consulte la sección [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=212032) en Libros en pantalla de SQL Server 2008.|  
|Dependencias de rol de sistema de sitio para los equipos que ejecutan el punto de servicios de informes.|[Configuraciones admitidas para System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Dependencias internas de Configuration Manager  
 En la siguiente tabla se muestran las dependencias de los informes en Configuration Manager.  

|Requisito previo|Más información|  
|------------------|----------------------|  
|Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.|A fin de poder usar los informes en Configuration Manager, primero debe configurarse el rol de sistema de sitio del punto de servicios de informes. Para obtener más información sobre cómo instalar y configurar un punto de servicios de informes, consulte [Configuración de informes en System Center Configuration Manager](../../../core/servers/manage/configuring-reporting.md).|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>Versiones de SQL Server admitidas para el punto de servicios de informes  
 La base de datos de Reporting Services puede instalarse en la instancia predeterminada o en una instancia con nombre de una instalación de SQL Server de 64 bits. La instancia de SQL Server puede coexistir con el servidor de sistema del sitio, o en un equipo remoto.  

 La tabla siguiente muestra las versiones de SQL Server que son compatibles con el punto de servicios de informes.  

|Versión de SQL Server|Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.|  
|------------------------|------------------------------|  
|SQL Server 2008 SP2 con la actualización acumulativa 9 como mínimo<br /><br /> -   Estándar<br />-   Enterprise<br />-   Centro de datos|Sí|  
|SQL Server 2008 SP3 con la actualización acumulativa 4 como mínimo<br /><br /> -   Estándar<br />-   Enterprise<br />-   Centro de datos|Sí|  
|SQL Server 2008 R2 con SP1 y la actualización acumulativa 6 como mínimo<br /><br /> -   Estándar<br />-   Enterprise<br />-   Centro de datos|Sí|  
|SQL Server 2008 R2 con SP2<br /><br /> -   Estándar<br />-   Enterprise<br />-   Centro de datos|Sí|  
|SQL Server Express 2008 R2 con SP1 y la actualización acumulativa 4 como mínimo|No compatible.|  
|SQL Server Express 2008 R2 con SP2|No compatible.|  
|SQL Server 2012 con la actualización acumulativa 2 como mínimo<br /><br /> -   Estándar<br />-   Enterprise|Sí|  
|SQL Server 2012 con SP1 y ninguna actualización acumulativa mínima<br /><br /> -   Estándar<br />-   Enterprise|Sí|  
|SQL Server 2014<br /><br /> -   Estándar<br />-   Enterprise|Sí|
|SQL Server 2016<br /><br /> -   Estándar<br />-   Enterprise|Sí|
|SQL Server 2016 con SP1<br /><br /> -   Estándar<br />-   Enterprise|Sí|
## <a name="next-steps"></a>Pasos siguientes
[Operaciones y mantenimiento de informes](operations-and-maintenance-for-reporting.md)

