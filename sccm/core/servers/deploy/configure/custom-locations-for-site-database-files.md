---
title: Ubicaciones personalizadas de archivos de base de datos | System Center Configuration Manager
description: "Obtenga información sobre cómo especificar ubicaciones personalizadas para archivos de base de datos de SQL Server."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e8625d753fd2832009c9a3dc0b12b9a44f93c091

---
# <a name="custom-locations-for-system-center-configuration-manager-site-database-files"></a>Ubicaciones personalizadas para archivos de base de datos del sitio de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

 System Center Configuration Manager es compatible con las ubicaciones personalizadas para archivos de base de datos de SQL Server.  

> [!NOTE]  
>  La opción de especificar ubicaciones de archivos no predeterminadas no está disponible cuando se usa un clúster de SQL Server.  

 **Durante la instalación** de un nuevo sitio primario o un sitio de administración central, puede hacer lo siguiente:  

-   Especificar ubicaciones de archivo no predeterminadas para la base de datos del sitio: el programa de instalación de Configuration Manager crea después la base de datos del sitio mediante el uso de esas ubicaciones.  

-   Especificar el uso de una base de datos de SQL Server creada previamente que usa ubicaciones de archivo personalizadas: el programa de instalación de Configuration Manager usa dicha base de datos creada previamente y sus ubicaciones de archivo preconfiguradas.  

**Después de la instalación** , puede cambiar la ubicación de los archivos de base de datos del sitio. Para ello, es necesario detener el sitio y editar la ubicación de los archivos en SQL Server:  

-   En el servidor de sitio de Configuration Manager, detenga el servicio **SMS_Executive**.  

-   Vea la documentación de la versión de SQL Server que use para obtener información sobre cómo mover una base de datos de usuario. Por ejemplo, si usa SQL Server 2014, vea [Mover bases de datos de usuario](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) en TechNet.  

-   Después de completar el desplazamiento de archivos de base de datos, reinicie el servicio SMS_Executive en el servidor de sitio de Configuration Manager.  



<!--HONumber=Nov16_HO1-->


