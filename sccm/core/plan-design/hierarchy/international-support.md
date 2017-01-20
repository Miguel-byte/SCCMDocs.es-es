---
title: Compatibilidad internacional | System Center Configuration Manager
description: "Configure System Center Configuration Manager para que cumpla con los requisitos internacionales específicos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 592ae2b8fbf55fa59afe909071a81b6bd3159ef7


---
# <a name="international-support-in-system-center-configuration-manager"></a>Compatibilidad internacional en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

En las secciones siguientes se proporcionan detalles técnicos para que pueda configurar System Center Configuration Manager de manera que sea compatible con determinados requisitos internacionales.  

## <a name="gb18030-requirements"></a>Requisitos de GB18030  
 Configuration Manager cumple los estándares definidos en GB18030 para poder usar Configuration Manager en China. Una implementación de Configuration Manager debe tener la configuración siguiente para cumplir los requisitos de GB18030:  

-   Los equipos de servidor de sitio y de SQL Server que se usan con Configuration Manager deben usar un sistema operativo chino.  

-   Las bases de datos del sitio y las instancias de SQL Server en la jerarquía deben utilizar la misma intercalación, y debe ser una las siguientes:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Estas intercalaciones de base de datos son una excepción de los requisitos que se mencionan en [Support for SQL Server versions for System Center Configuration Manager (Compatibilidad con versiones de SQL Server para System Center Configuration Manager)](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   Debe colocar un archivo de nombre **GB18030.SMS** en la carpeta raíz del volumen de sistema de cada equipo de servidor de sitio en la jerarquía. Este archivo no contiene datos y puede ser un archivo de texto vacío con este nombre para cumplir el requisito.  



<!--HONumber=Nov16_HO1-->


