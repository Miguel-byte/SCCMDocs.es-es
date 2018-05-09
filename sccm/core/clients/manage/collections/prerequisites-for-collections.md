---
title: Requisitos previos de las recopilaciones
titleSuffix: Configuration Manager
description: Cumpla los requisitos previos para usar recopilaciones en System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 12cbffb63ce449afedb9159174409fb5b1f7583f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Requisitos previos de las recopilaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las recopilaciones de System Center Configuration Manager solo contienen dependencias dentro del producto.  

## <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  

|Dependencia|Más información|  
|----------------|----------------------|  
|Punto de servicios de informes|El rol de sistema de sitio de punto de servicios de informes debe instalarse antes de poder ejecutar informes para las recopilaciones. Para obtener más información, consulte [Reporting in System Center Configuration Manager](../../../../core/servers/manage/reporting.md) (Generación de informes en System Center Configuration Manager).|  
|Para administrar recopilaciones, se deben tener permisos de seguridad específicos.|Debe tener los siguientes permisos de seguridad para administrar la configuración de cumplimiento:<br /><br /> - Para crear y administrar recopilaciones: **Crear**, **Eliminar**, **Modificar**, **Modificar carpeta**, **Mover objeto**, **Leer** y **Leer recurso** para el objeto **Collection**.<br /><br /> - Para administrar la configuración de recopilaciones: **Modificar configuración de recopilación** para el objeto **Collection**.<br /><br /> El permiso **Modificar carpeta** es necesario para todas las carpetas de la recopilación, incluida la carpeta raíz.|  
