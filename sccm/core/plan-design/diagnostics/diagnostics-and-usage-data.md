---
title: Diagnósticos y datos de uso
titleSuffix: Configuration Manager
description: Obtenga información sobre los datos de uso y diagnóstico que Configuration Manager recopila sobre sí mismo.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 68a5787b4c4fa2caf05c1a8c9c6e64bbdd437279
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536772"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Diagnósticos y datos de uso para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager recopila datos de uso y diagnóstico sobre sí mismo, que Microsoft usa para mejorar la experiencia de instalación, la calidad y la seguridad de las versiones futuras.  

Los datos de uso y diagnóstico están habilitados para cada jerarquía de Configuration Manager. Consta de las consultas de SQL Server que se ejecutan de forma semanal en cada sitio primario y en el sitio de administración central. Cuando la jerarquía usa un sitio de administración central, los datos de los sitios primario se replican en ese sitio. En el sitio de nivel superior de la jerarquía, el punto de conexión de servicio envía esta información cuando busca actualizaciones. Si el punto de conexión de servicio está en modo sin conexión, la información se transfiere mediante la herramienta de conexión de servicio.  

> [!NOTE]  
> Configuration Manager solamente recopila datos de la base de datos de SQL Server del sitio y no recopila datos directamente de los clientes ni de los servidores de sitios.  

Para obtener más información, vea la [Declaración de privacidad de Microsoft](https://go.microsoft.com/fwlink/?LinkID=626527).  

## <a name="articles"></a>Artículos

Obtenga más información sobre los datos de uso y diagnóstico para Configuration Manager en los artículos siguientes:  

- [Cómo se usan los datos de uso y diagnóstico](/sccm/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used)  

- Niveles de recopilación de datos de uso para diagnóstico:

    - [Datos de diagnóstico de la versión 1906](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906)  

    - [Datos de diagnóstico de la versión 1902](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1902)  

    - [Datos de diagnóstico de la versión 1810](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1810)  

    - [Datos de diagnóstico de la versión 1806](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1806)  

- [Cómo se recopilan los datos de uso y diagnóstico](/sccm/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected)  

- [Visualización de datos de diagnóstico y uso](/sccm/core/plan-design/diagnostics/view-diagnostics-and-usage-data)  

- [Preguntas frecuentes acerca de datos de diagnóstico y uso](/sccm/core/understand/frequently-asked-questions-about-diagnostics-and-usage-data)  


## <a name="see-also"></a>Consulte también

[Acerca del punto de conexión de servicio](/sccm/core/servers/deploy/configure/about-the-service-connection-point)
