---
title: Diagnósticos y datos de uso
titleSuffix: Configuration Manager
description: Obtenga información sobre los datos de uso y diagnóstico que System Center Configuration Manager recopila sobre sí mismo.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 132604418ce810fb78b397f3d5f322b10abe6bb3
ms.sourcegitcommit: 1439817f1309658b31008d7bafaab32fc5ef8789
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52820023"
---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Diagnósticos y datos de uso para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager recopila datos de uso y diagnóstico sobre sí mismo, que Microsoft usa para mejorar la experiencia de instalación, la calidad y la seguridad de las versiones futuras.  

 Los datos de uso y diagnóstico están habilitados para cada jerarquía de Configuration Manager. Consta de las consultas de SQL Server que se ejecutan de forma semanal en cada sitio primario y en el sitio de administración central. Cuando la jerarquía usa un sitio de administración central, los datos de los sitios primario se replican en ese sitio. En el sitio de nivel superior de la jerarquía, el punto de conexión de servicio envía esta información cuando busca actualizaciones. Si el punto de conexión de servicio está en modo sin conexión, la información se transfiere mediante la herramienta de conexión de servicio.  

> [!NOTE]  
>  Configuration Manager solamente recopila datos de la base de datos de SQL Server del sitio y no recopila datos directamente de los clientes ni de los servidores de sitios.  

 Para obtener más información, vea la [Declaración de privacidad de Microsoft](https://go.microsoft.com/fwlink/?LinkID=626527).  

## <a name="articles"></a>Artículos
 Obtenga más información sobre los datos de uso y diagnóstico para Configuration Manager en los artículos siguientes:  

-   [Cómo se usan los datos de uso y diagnóstico](/sccm/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used)  

-   Niveles de recopilación de datos de uso para diagnóstico:
    - [Datos de diagnóstico de la versión 1810](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1810)  

    - [Datos de diagnóstico de la versión 1806](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1806)  

    - [Datos de diagnóstico de la versión 1802](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1802)  
    
    - [Datos de diagnóstico de la versión 1710](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1710)  

-   [Cómo se recopilan los datos de uso y diagnóstico](/sccm/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected)  

-   [Visualización de datos de diagnóstico y uso](/sccm/core/plan-design/diagnostics/view-diagnostics-and-usage-data)  

-   [Programa para la mejora de la experiencia del usuario (CEIP)](/sccm/core/plan-design/diagnostics/customer-experience-improvement-program-ceip)  

     > [!Note]  
     > A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto.  


-   [Preguntas frecuentes acerca de datos de diagnóstico y uso](/sccm/core/understand/frequently-asked-questions-about-diagnostics-and-usage-data)  



## <a name="see-also"></a>Véase también  
 [Acerca del punto de conexión de servicio](/sccm/core/servers/deploy/configure/about-the-service-connection-point)
