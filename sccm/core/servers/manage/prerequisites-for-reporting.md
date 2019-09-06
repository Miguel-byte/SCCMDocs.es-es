---
title: Requisitos previos de los informes
titleSuffix: Configuration Manager
description: Analice varias dependencias que afectan al uso de los informes en System Center Configuration Manager.
ms.date: 01/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 226a2632f8aa827975a764f0d22aea0a05ec6d96
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/05/2019
ms.locfileid: "70379763"
---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>Requisitos previos de los informes en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La generación de informes en System Center Configuration Manager tiene dependencias externas y dependencias dentro del producto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependencias externas a Configuration Manager  
 La tabla siguiente muestra las dependencias externas de los informes.  

|Requisito previo|Más información|  
|------------------|----------------------|  
|SQL Server Reporting Services|Para poder usar los informes en Configuration Manager, debe instalar y configurar SQL Server Reporting Services.<br /><br /> Para obtener información acerca de cómo planificar e implementar Reporting Services en su entorno, consulte la sección [SQL Server Reporting Services](https://go.microsoft.com/fwlink/p/?LinkId=212032) en Libros en pantalla de SQL Server 2008.|  
|Dependencias de rol de sistema de sitio para los equipos que ejecutan el punto de servicios de informes.|[Configuraciones admitidas para System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Dependencias internas de Configuration Manager  
 En la siguiente tabla se muestran las dependencias de los informes en Configuration Manager.  

|Requisito previo|Más información|  
|------------------|----------------------|  
|Punto de servicios de informes|A fin de poder usar los informes en Configuration Manager, primero debe configurarse el rol de sistema de sitio del punto de servicios de informes. Para obtener más información sobre cómo instalar y configurar un punto de servicios de informes, consulte [Configuración de informes en System Center Configuration Manager](../../../core/servers/manage/configuring-reporting.md).|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>Versiones de SQL Server admitidas para el punto de servicios de informes  
 La base de datos de Reporting Services puede instalarse en la instancia predeterminada o en una instancia con nombre de una instalación de SQL Server de 64 bits. La instancia de SQL Server puede coexistir con el servidor de sistema del sitio, o en un equipo remoto.  

 La tabla siguiente muestra las versiones de SQL Server que son compatibles con el punto de servicios de informes.  

|Versión de SQL Server|Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.|  
|------------------------|------------------------------|
|SQL Server 2017 con la actualización acumulativa 2 como mínimo<br /><br /> -   Estándar<br />-   Enterprise|Sí, a partir de la versión 1710 de Configuration Manager|  
|SQL Server 2016 con SP1<br /><br /> -   Estándar<br />-   Enterprise|Sí| 
|SQL Server 2016<br /><br /> -   Estándar<br />-   Enterprise|Sí|
|SQL Server 2014 con SP2<br /><br /> -   Estándar<br />-   Enterprise|Sí|
|SQL Server 2014 con SP1<br /><br /> -   Estándar<br />-   Enterprise|Sí|
|SQL Server 2012 con SP4 <br /><br /> -   Estándar<br />-   Enterprise|Sí|  
|SQL Server 2012 con SP3 <br /><br /> -   Estándar<br />-   Enterprise|Sí|  
|SQL Server 2008 R2 con SP3<br /><br /> -   Estándar<br />-   Enterprise<br />-   Centro de datos|Sí, para las versiones compatibles de Configuration Manager anteriores a la 1702.|  
|SQL Server Express 2008 R2 con SP3|No compatible.| 




## <a name="next-steps"></a>Pasos siguientes
[Operaciones y mantenimiento de informes](operations-and-maintenance-for-reporting.md)
