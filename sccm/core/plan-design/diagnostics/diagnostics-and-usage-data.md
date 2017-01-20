---
title: "Datos de uso y diagnóstico | System Center Configuration Manager"
description: "Obtenga información sobre los datos de uso y diagnóstico que System Center Configuration Manager recopila sobre sí mismo."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 996efaeb89926b04d2f071cf600dcf45bd2edc89


---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Diagnósticos y datos de uso para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

System Center Configuration Manager recopila datos de uso y diagnóstico sobre sí mismo que Microsoft emplea para mejorar la experiencia de instalación, la calidad y la seguridad de las versiones futuras.  

 Los datos de uso y diagnóstico están habilitados para cada jerarquía de System Center Configuration Manager. Consta de las consultas de SQL Server que se ejecutan de forma semanal en cada sitio primario y en el sitio de administración central. Cuando la jerarquía usa un sitio de administración central, los datos de los sitios primario se replican en ese sitio. En el sitio de nivel superior de la jerarquía, el punto de conexión de servicio envía esta información cuando busca actualizaciones. Si el punto de conexión de servicio está en modo sin conexión, la información se transfiere mediante la herramienta de conexión de servicio.  

> [!NOTE]  
>  Configuration Manager solamente recopila datos de la base de datos de SQL Server de sitios y no recopila datos directamente de los clientes ni de los servidores de sitios.  

 Para obtener más información, vea [Información General sobre la Declaración de Privacidad de System Center Configuration Manager Server](http://go.microsoft.com/fwlink/?LinkID=626527).  

 Obtenga más información sobre los datos de uso y diagnóstico para System Center Configuration Manager en los temas siguientes:  

-   [How diagnostics and usage data is used for System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md) (Cómo se usan los datos de uso y diagnóstico para System Center Configuration Manager)  

-   Niveles de recopilación de datos de uso para diagnóstico:
    - [Datos de diagnóstico para 1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
    - [Datos de diagnóstico para 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [Datos de diagnóstico para 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)  
    

-   [How diagnostics and usage data is collected by System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md) (Cómo System Center Configuration Manager recopila los datos de uso y diagnóstico)  

-   [How to view diagnostics and usage data for System Center Configuration Manager](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md) (Visualización de datos de diagnóstico y uso para System Center Configuration Manager)  

-   [Customer Experience Improvement Program (CEIP) for System Center Configuration Manager](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md) (Programa para la mejora de la experiencia del usuario (CEIP) para System Center Configuration Manager)  

-   [Frequently asked questions about diagnostics and usage data for System Center Configuration Manager](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md) (Preguntas frecuentes acerca de datos de diagnóstico y uso para System Center Configuration Manager)  

## <a name="see-also"></a>Véase también  
 [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md) (Acerca del punto de conexión de servicio en System Center Configuration Manager)



<!--HONumber=Nov16_HO1-->


