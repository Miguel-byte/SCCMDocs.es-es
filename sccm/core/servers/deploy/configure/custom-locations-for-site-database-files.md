---
title: Ubicaciones personalizadas de archivos de base de datos | Microsoft Docs
description: "Obtenga información sobre cómo especificar ubicaciones personalizadas para archivos de base de datos de SQL Server."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: cfac2c03c1b71b40c68d8acd5fbd96c5e98caaa9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="custom-locations-for-system-center-configuration-manager-site-database-files"></a>Ubicaciones personalizadas para archivos de base de datos del sitio de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

 System Center Configuration Manager es compatible con las ubicaciones personalizadas para archivos de base de datos de SQL Server.  

> [!NOTE]  
>  La opción de especificar ubicaciones de archivos no predeterminadas no está disponible cuando se usa un clúster de SQL Server.  

 **Durante la configuración** de un nuevo sitio principal o un sitio de administración central, puede hacer lo siguiente:  

-   **Especificar ubicaciones de archivo no predeterminadas para la base de datos del sitio**: el programa de instalación de Configuration Manager crea después la base de datos del sitio mediante el uso de esas ubicaciones.  

-   **Especificar el uso de una base de datos de SQL Server creada previamente que usa ubicaciones de archivo personalizadas**: el programa de instalación de Configuration Manager usa dicha base de datos creada previamente y sus ubicaciones de archivo preconfiguradas.  

**Después de la configuración**, puede cambiar la ubicación de los archivos de la base de datos del sitio. Para ello, es necesario detener el sitio y editar la ubicación de los archivos en SQL Server:  

-   En el servidor de sitio de Configuration Manager, detenga el servicio **SMS_Executive**.  

-   Use la documentación de su versión de SQL Server para obtener información sobre cómo mover una base de datos de usuario. Por ejemplo, si usa SQL Server 2014, vea [Mover bases de datos de usuario](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) en TechNet.  

-   Después de completar el movimiento de archivos de la base de datos, reinicie el servicio **SMS_Executive** en el servidor de sitio de Configuration Manager.  
