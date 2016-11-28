---
title: Requisitos previos de las recopilaciones | System Center Configuration Manager
description: Cumpla los requisitos previos para usar recopilaciones en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 99ddc0ba39778db4e8e45d6e954894464c7e047c


---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Requisitos previos de las recopilaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Las recopilaciones de System Center Configuration Manager solo contienen dependencias dentro del producto.  

## <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  

|Dependencia|Más información|  
|----------------|----------------------|  
|Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.|El rol de sistema de sitio de punto de servicios de informes debe instalarse antes de poder ejecutar informes para las recopilaciones. Para obtener más información, consulte [Generación de informes en System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Para administrar recopilaciones, se deben tener permisos de seguridad específicos.|Debe tener los siguientes permisos de seguridad para administrar la configuración de cumplimiento:<br /><br /> - Para crear y administrar recopilaciones: **Crear**, **Eliminar**, **Modificar**, **Modificar carpeta**, **Mover objeto**, **Leer** y **Leer recurso** para el objeto **Collection**.<br /><br /> - Para administrar la configuración de recopilaciones: **Modificar configuración de recopilación** para el objeto **Collection**.<br /><br /> El permiso **Modificar carpeta** es necesario para todas las carpetas de la recopilación, incluida la carpeta raíz.|  



<!--HONumber=Nov16_HO1-->


