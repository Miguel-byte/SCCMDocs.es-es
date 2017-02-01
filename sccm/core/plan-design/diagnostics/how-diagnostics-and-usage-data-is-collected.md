---
title: "Recopilación de datos de diagnóstico | Microsoft Docs"
description: "Obtenga información sobre cómo System Center Configuration Manager recopila datos de uso y diagnóstico sobre sí mismo."
ms.custom: na
ms.date: 12/29/2016
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
ms.sourcegitcommit: 24a233516058e645df2a43623855665b97b041b0
ms.openlocfilehash: 9c0165212fe34f460be2ce870d0542b616f3bc4d


---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Cómo System Center Configuration Manager recopila los datos de uso y diagnóstico

*Se aplica a: System Center Configuration Manager (rama actual)*

Para recopilar los datos de uso y diagnóstico para System Center Configuration Manager, cada sitio primario ejecuta consultas de SQL Server con carácter semanal. En una jerarquía de varios sitio, los datos se replican en el sitio de administración central.  

En el sitio de nivel superior de una jerarquía, el rol de sistema de sitio del punto de conexión de servicio envía esta información cuando busca actualizaciones. El modo del punto de conexión de servicio determina cómo se transfieren los datos:  

-   **En modo con conexión:** los datos de uso y diagnóstico se envían automáticamente una vez por semana, desde el punto de conexión de servicio al servicio en la nube.  

-   **En modo sin conexión:** los datos de uso y diagnóstico se transfieren manualmente mediante la herramienta de conexión del servicio. Para obtener más información, consulte [Use the Service Connection Tool for System Center Configuration Manager (Usar la herramienta de conexión de servicio para System Center Configuration Manager)](../../../core/servers/manage/use-the-service-connection-tool.md).  

Para obtener más información, consulte [Acerca del punto de conexión de servicio en System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  



<!--HONumber=Dec16_HO5-->


