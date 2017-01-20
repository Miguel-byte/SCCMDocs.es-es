---
title: "Recopilación de datos de diagnóstico | System Center Configuration Manager"
description: "Obtenga información sobre cómo System Center Configuration Manager recopila datos de uso y diagnóstico sobre sí mismo."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 89292a11d003edd9e3a0eeb7fd367265a6b150b6


---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Cómo System Center Configuration Manager recopila los datos de uso y diagnóstico

*Se aplica a: System Center Configuration Manager (rama actual)*

Para recopilar los datos de uso y diagnóstico para System Center Configuration Manager, cada sitio primario ejecuta consultas de SQL Server con carácter semanal. En una jerarquía de varios sitio, los datos se replican en el sitio de administración central.  

En el sitio de nivel superior de una jerarquía, el rol de sistema de sitio del punto de conexión de servicio envía esta información cuando busca actualizaciones. La forma en que se transfieren los datos depende del modo de punto de conexión de servicio:  

-   **En modo con conexión:** los datos de uso y diagnóstico se envían automáticamente una vez por semana, desde el punto de conexión de servicio al servicio en la nube.  

-   **En modo sin conexión:** los datos de uso y diagnóstico se transfieren manualmente mediante la herramienta de conexión del servicio. Para obtener más información, consulte [Use the Service Connection Tool for System Center Configuration Manager (Usar la herramienta de conexión de servicio para System Center Configuration Manager)](../../../core/servers/manage/use-the-service-connection-tool.md).  

Para obtener más información, consulte [Acerca del punto de conexión de servicio en System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  



<!--HONumber=Nov16_HO1-->


