---
title: "Nueva versión 1702 | Microsoft Docs"
description: "Conozca en detalle los cambios y las nuevas funciones introducidas en la versión 1702 de System Center Configuration Manager."
ms.custom: na
ms.date: 03/27/2017
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: Brenduns
ms.author: brenduns
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: 473ba742bea74cbfdf8cab550244ccd522523718
ms.lasthandoff: 03/04/2017

---
# <a name="what39s-new-in-version-1702-of-system-center-configuration-manager"></a>Novedades de la versión 1702 de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

La actualización 1702 para la rama actual de System Center Configuration Manager está disponible como actualización en consola para sitios instalados previamente que ejecutan la versión 1606 o 1610. También está disponible como una versión de línea de base que puede utilizar al instalar una nueva implementación.

> [!TIP]  
> Para instalar un sitio nuevo, debe usar una versión de línea base de Configuration Manager.  
>  Más información acerca de:    
>  -   [Instalación de nuevos sitios](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [Instalación de actualizaciones en los sitios](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [Versiones de línea de base y versiones de actualización](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

En las secciones siguientes se proporcionan detalles sobre los cambios y las nuevas funciones introducidas en la versión 1702 de Configuration Manager.  


## <a name="data-warehouse-service-point"></a>Punto de servicio de almacenamiento de datos
Use el punto de servicio de almacenamiento de datos para almacenar y generar informes de datos históricos a largo plazo para su implementación de Configuration Manager.

El almacenamiento de datos admite hasta 2 TB de datos, con marcas de tiempo para el seguimiento de cambios. El almacenamiento de datos se consigue mediante sincronizaciones automatizadas desde la base de datos del sitio de Configuration Manager a la base de datos de almacenamiento de datos. Puede acceder a esta información desde su punto de Reporting Services.



Para más información, consulte [Punto de servicio del almacenamiento de datos](/sccm/core/servers/manage/data-warehouse).

