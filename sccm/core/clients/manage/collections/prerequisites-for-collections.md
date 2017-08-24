---
title: Requisitos previos de las recopilaciones | Microsoft Docs
description: Cumpla los requisitos previos para usar recopilaciones en System Center Configuration Manager.
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
caps.latest.revision: "7"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 41fc3eb20a7441939eb0dc80bc121c8f3ea322b2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Requisitos previos de las recopilaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Las recopilaciones de System Center Configuration Manager solo contienen dependencias dentro del producto.  

## <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  

|Dependencia|Más información|  
|----------------|----------------------|  
|Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.|El rol de sistema de sitio de punto de servicios de informes debe instalarse antes de poder ejecutar informes para las recopilaciones. Para obtener más información, consulte [Generación de informes en System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Para administrar recopilaciones, se deben tener permisos de seguridad específicos.|Debe tener los siguientes permisos de seguridad para administrar la configuración de cumplimiento:<br /><br /> - Para crear y administrar recopilaciones: **Crear**, **Eliminar**, **Modificar**, **Modificar carpeta**, **Mover objeto**, **Leer** y **Leer recurso** para el objeto **Collection**.<br /><br /> - Para administrar la configuración de recopilaciones: **Modificar configuración de recopilación** para el objeto **Collection**.<br /><br /> El permiso **Modificar carpeta** es necesario para todas las carpetas de la recopilación, incluida la carpeta raíz.|  
