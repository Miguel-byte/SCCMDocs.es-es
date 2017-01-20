---
title: Configurar sitios | System Center Configuration Manager
description: "Consulte esta lista de comprobación para asegurarse de tener en cuenta las configuraciones más comunes que afectan a los sitios y las jerarquías."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: 15
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 470efc428045398588345f4546eb27831837715c


---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>Configurar sitios y jerarquías para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Después de instalar el primer sitio de System Center Configuration Manager o de agregar sitios adicionales a la jerarquía, use la siguiente lista de comprobación para asegurarse de tener en cuenta las configuraciones más comunes que afectan tanto a los sitios como a las jerarquías.  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>Lista de comprobación de configuraciones comunes de sitios nuevos y adicionales  
 En la mayoría de las implementaciones, no necesitará configurar las opciones siguientes en ningún orden específico:  

-   Algunas opciones se basan en otras como, por ejemplo, la Detección de bosques de Active Directory, los límites y los grupos de límites.  

-   Varias de estas configuraciones tienen valores predeterminados que se pueden usar sin cambios, al menos temporalmente.  

-   Otras, tales como los grupos de límites y los grupos de puntos de distribución, deben configurarse antes de usarlas.  

|Acción|Detalles|  
|------------|-------------|  
|Configurar la administración basada en roles|La administración basada en roles se usa para separar las asignaciones administrativas para controlar qué usuarios administrativos pueden ver y administrar los distintos objetos y datos de su entorno de Configuration Manager.<br /><br /> Las configuraciones de la administración basada en roles se comparten con todos los sitios de una jerarquía.   <br />Consulte [Configurar la administración basada en roles de System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).|  
|Publicar datos del sitio en Servicios de dominio de Active Directory (AD DS)|Publicar datos del sitio en AD DS permite que los clientes encuentren fácilmente los servicios y usen de forma eficaz los recursos del sitio.<br /><br /> Primero debe [Extender el esquema de Active Directory para System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md), y, a continuación, es necesario configurar cada sitio para [Publicar datos de sitio para System Center Configuration Manager](../../../../core/servers/deploy/configure/publish-site-data.md) individualmente.|  
|Configurar un punto de conexión de servicio|En el sitio de nivel superior de la jerarquía, debe planear la instalación y configuración del punto de conexión del servicio. Para más información, consulte [Acerca del punto de conexión de servicio en System Center Configuration Manager](../../../../core/servers/deploy/configure/about-the-service-connection-point.md).|  
|Agregar roles de sistema de sitio|Instale uno o varios roles de sistema de sitio adicionales para los sitios individuales.  Consulte [Add site system roles for System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md).|  
|Configurar límites de sitio y grupos de límites|Especifique los límites que definen las ubicaciones de red de la intranet que pueden contener los dispositivos que quiere administrar y después configure los grupos de límites para que los clientes de dichas ubicaciones de red puedan encontrar los recursos de servicios de Configuration Manager. Consulte [Definir los límites del sitio y los grupos de límites para System Center Configuration Manager](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).|  
|Configurar grupos de puntos de distribución|Configure grupos lógicos de puntos de distribución para facilitar la administración de implementaciones. Consulte [Administrar grupos de puntos de distribución](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) en [Install and configure distribution points for System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) (Instalación y configuración de puntos de distribución de System Center Configuration Manager).|  
|Ejecutar la detección|Ejecute la detección para buscar recursos en la red, incluidos usuarios, dispositivos e infraestructura de red.<br /><br /> Consulte [Run discovery for System Center Configuration Manager](../../../../core/servers/deploy/configure/run-discovery.md).|  
|Agregar redundancia y capacidad para los administradores de la infraestructura|Puede instalar proveedores de SMS adicionales y consolas de Configuration Manager para expandir la capacidad de los administradores para administrar la infraestructura:<br /><br /> **Instale proveedores de SMS adicionales** para proporcionar redundancia a los puntos de contacto para administrar el sitio y la jerarquía. Vea [Manage the SMS Provider](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) en [Modify your System Center Configuration Manager enfrastructure](../../../../core/servers/manage/modify-your-infrastructure.md).<br /><br /> **Instale consolas de Configuration Manager adicionales** para proporcionar acceso a usuarios administrativos adicionales al mismo tiempo. Consulte [Instalar una consola de Configuration Manager](../../../../core/servers/deploy/install/install-consoles.md).|  
|Configurar componentes de sitio|Puede configurar componentes de sitio en cada sitio para modificar el comportamiento de los roles de sistema de sitio y los informes de estado de sitio. Consulte [Site components for System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md).|  
|Crear recopilaciones personalizadas|Con la información detectada sobre los usuarios y los dispositivos, cree recopilaciones personalizadas de objetos para simplificar las tareas de administración futuras. Consulte [Cómo crear recopilaciones en System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|Configurar opciones para administrar implementaciones de alto riesgo|Defina la configuración en un sitio que avisará a los usuarios administrativos si crean una implementación de una secuencia de tareas de alto riesgo.  Consulte [Settings to manage high-risk deployments for System Center Configuration Manager](../../../../protect/understand/settings-to-manage-high-risk-deployments.md).|  
|Configurar réplicas de bases de datos para puntos de administración|Configure una réplica de base de datos para reducir la carga de CPU que los puntos de administración colocan en el servidor de base de datos del sitio mientras atienden las solicitudes de servicio de los clientes. Consulte [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).|  
|Configure un grupo de disponibilidad AlwaysOn de SQL Server para hospedar la base de datos del sitio|A partir de la versión 1602, puede configurar grupos de disponibilidad como una solución de alta disponibilidad y recuperación ante desastres para hospedar la base de datos del sitio en sitios primarios y en el sitio de administración central. Consulte [SQL Server AlwaysOn para una base de datos de sitio de alta disponibilidad para System Center Configuration Manager](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).|  
|Modificar la replicación entre sitios|Consulte [Transferencias de datos entre sitios en System Center Configuration Manager](../../../../core/servers/manage/data-transfers-between-sites.md) para más información acerca de los siguientes temas:<br /><br /> Configurar [File-based replication](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute) entre sitios secundarios<br /><br /> Configurar [Database replication links](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> Configurar [Distributed views](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  



<!--HONumber=Nov16_HO1-->


