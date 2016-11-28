---
title: Planificar la base de datos del sitio | System Center Configuration Manager
description: "Tenga en cuenta la base de datos y el rol de servidor de base de datos de sitio cuando planifique la jerarquía de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 40ebfaa9b82a65a6265f0c031dbbd0bcdb85da6e


---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>Planificar la base de datos del sitio de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

El servidor de base de datos de sitio es un equipo que ejecuta una versión compatible de Microsoft SQL Server que almacena la información para sitios de Configuration Manager. Cada sitio de una jerarquía de Configuration Manager contiene una base de datos del sitio y un servidor al que se asigna el rol de servidor de base de datos de sitio.  

-   En los sitios de administración centrales y primarios, puede instalar SQL Server en el servidor de sitio o puede instalar SQL Server en un equipo distinto del servidor de sitio.  

-   En los sitios secundarios, puede usar SQL Server Express en lugar de una instalación completa de SQL Server; sin embargo, el servidor de la base de datos debe ejecutarse en el servidor de sitio secundario.  

Si utiliza un equipo de servidor de base de datos remoto, asegúrese de que la conexión de red que intervenga sea una conexión de red de alta disponibilidad y ancho de banda alto. Esto se debe a que el servidor de sitio y algunos roles de sistema de sitio deben comunicarse constantemente con el SQL Server que aloja la base de datos del sitio.  


**Al seleccionar la ubicación de un servidor de base de datos remoto, tenga en cuenta lo siguiente:**  

-   La cantidad de ancho de banda requerida para las comunicaciones con el servidor de base de datos depende de una combinación de muchas configuraciones de sitio y cliente distintas, por lo que es posible que no se prediga adecuadamente el ancho de banda realmente necesario.  

-   Cada equipo que ejecuta el proveedor de SMS y que se conecta a la base de datos del sitio aumenta los requisitos de ancho de banda de red.  

-   El equipo que ejecuta SQL Server debe estar ubicado en un dominio que tenga una confianza bidireccional con el servidor de sitio y con todos los equipos que ejecutan el proveedor de SMS.  

-   No puede utilizar un SQL Server en clúster para el servidor de base de datos del sitio cuando la base de datos del sitio comparte ubicación con el servidor de sitio.  


Normalmente, un servidor de sistema de sitio admite roles de sistema de sitio solamente de un único sitio de Configuration Manager; no obstante, puede usar instancias diferentes de SQL Server, de servidores en clúster o de servidores que no están en clúster que ejecutan SQL Server, para alojar una base de datos de diferentes sitios de Configuration Manager. Para admitir bases de datos de sitios diferentes, debe configurar cada instancia de SQL Server para usar puertos exclusivos para la comunicación.  


**Las siguientes configuraciones de SQL Server se pueden utilizar para hospedar la base de datos del sitio:**  

-   La instancia predeterminada de SQL Server  

-   Una instancia con nombre en un único equipo que ejecute SQL Server  

-   Una instancia con nombre en una instancia en clúster de SQL Server  

-   Un grupo de disponibilidad de SQL Server AlwaysOn (a partir de la versión 1602)


**Requisitos previos de la base de datos del sitio:**  

-   Para hospedar la base de datos de sitio, SQL Server debe cumplir los requisitos detallados en [Support for SQL Server versions for System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md) (Compatibilidad con versiones de SQL Server para System Center Configuration Manager).  



<!--HONumber=Nov16_HO1-->


