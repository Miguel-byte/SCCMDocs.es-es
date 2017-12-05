---
title: "Configuración de sitios"
titleSuffix: Configuration Manager
description: "Consulte esta lista de comprobación para asegurarse de tener en cuenta las configuraciones más comunes que afectan a los sitios y las jerarquías."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: "15"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 55daf30e3386e53f3711c07fa971750d6aa33423
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2017
---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>Configurar sitios y jerarquías para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Después de instalar el primer sitio de System Center Configuration Manager o de agregar sitios adicionales a la jerarquía, use la siguiente lista de comprobación para asegurarse de tener en cuenta las configuraciones más comunes que afectan tanto a los sitios como a las jerarquías.  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>Lista de comprobación de configuraciones comunes de sitios nuevos y adicionales  
Tenga en cuenta las notas siguientes sobre la configuración que son válidas para la mayoría de las implementaciones:

-   Algunas opciones se basan en otras (por ejemplo, la Detección de bosques de Active Directory, los límites y los grupos de límites).  

-   Varias de estas configuraciones tienen valores predeterminados que se pueden usar sin cambios, al menos temporalmente.  

-   Otras, tales como los grupos de límites y los grupos de puntos de distribución, deben configurarse antes de usarlas.  

|Acción|Detalles|  
|------------|-------------|  
|Configurar la administración basada en roles|Separe las asignaciones administrativas para controlar qué usuarios administrativos pueden ver y administrar los distintos objetos y datos de su entorno de Configuration Manager.<br /><br /> Las configuraciones de la administración basada en roles se comparten con todos los sitios de una jerarquía.   <br/><br/>Para obtener más información, consulte [Configurar la administración basada en roles de System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).|  
|Publicar datos del sitio en Servicios de dominio de Active Directory (AD DS)|Permita que los clientes encuentren fácilmente servicios y que usen de manera eficiente los recursos del sitio.<br /><br /> Primero necesita [extender el esquema de Active Directory para System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) y, después, tendrá que configurar cada sitio de forma individual para [publicar datos de sitio para System Center Configuration Manager](../../../../core/servers/deploy/configure/publish-site-data.md).|  
|Configurar un punto de conexión de servicio|Planee la instalación y configuración del punto de conexión de servicio en el sitio de nivel superior de la jerarquía. Para obtener más información, consulte [Acerca del punto de conexión de servicio en System Center Configuration Manager](../../../../core/servers/deploy/configure/about-the-service-connection-point.md).|  
|Agregar roles de sistema de sitio|Instale uno o varios roles de sistema de sitio adicionales para sitios individuales.  Para obtener más información, consulte [Agregar roles de sistema de sitio para System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md).|  
|Configurar límites de sitio y grupos de límites|Especifique límites que definan ubicaciones de red de la intranet que puede contener los dispositivos que quiere administrar. Después, configure los grupos de límites para que los clientes en esas ubicaciones de red puedan encontrar recursos de Configuration Manager. Para obtener más información, consulte [Definir los límites del sitio y los grupos de límites para System Center Configuration Manager](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).|  
|Configurar grupos de puntos de distribución|Configure grupos lógicos de puntos de distribución para facilitar la administración de implementaciones. Para obtener más información, consulte [Administrar grupos de puntos de distribución](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) en [Instalación y configuración de puntos de distribución de System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).|  
|Ejecutar la detección|Ejecute la detección para buscar recursos en la red, incluidos usuarios, dispositivos e infraestructura de red.<br /><br /> Para obtener más información, consulte [Ejecutar la detección para System Center Configuration Manager](../../../../core/servers/deploy/configure/run-discovery.md).|  
|Agregar redundancia y capacidad para los administradores de la infraestructura|Puede instalar proveedores de SMS adicionales y consolas de Configuration Manager para expandir la capacidad de los administradores para administrar la infraestructura:<br /><br /> **Instale proveedores de SMS adicionales** para proporcionar redundancia a los puntos de contacto para administrar el sitio y la jerarquía. Para obtener más información, consulte [Administración del proveedor de SMS](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) en [Modificar la infraestructura de System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).<br /><br /> **Instale consolas de Configuration Manager adicionales** para proporcionar acceso a otros usuarios administrativos. Para obtener más información, consulte [Instalar la consola de System Center Configuration Manager](../../../../core/servers/deploy/install/install-consoles.md).|  
|Configurar componentes de sitio|Puede configurar componentes de sitio en cada sitio para modificar el comportamiento de los roles de sistema de sitio y los informes de estado de sitio. Para obtener más información, consulte [Componentes de sitio para System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md).|  
|Crear recopilaciones personalizadas|Con la información detectada sobre los dispositivos y usuarios, cree colecciones personalizadas de objetos para simplificar las tareas de administración futuras. Para obtener más información, consulte [Cómo crear recopilaciones en System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|Configurar opciones para administrar implementaciones de alto riesgo|Defina la configuración en un sitio que muestre una advertencia a los usuarios administrativos al crear una implementación de una secuencia de tareas de alto riesgo.  Para obtener más información, consulte [Configuración para administrar implementaciones de alto riesgo para System Center Configuration Manager](../../../../protect/understand/settings-to-manage-high-risk-deployments.md).|  
|Configurar réplicas de bases de datos para puntos de administración|Configure una réplica de base de datos para reducir la carga de CPU que los puntos de administración colocan en el servidor de base de datos del sitio al atender las solicitudes de servicio de los clientes. Para obtener más información, consulte [Réplicas de bases de datos para puntos de administración de System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).|  
|Configurar un grupo de disponibilidad AlwaysOn de SQL Server para hospedar la base de datos del sitio|A partir de la versión 1602, configure grupos de disponibilidad como soluciones de alta disponibilidad y recuperación ante desastres para hospedar la base de datos del sitio en sitios primarios y en el sitio de administración central. Para obtener más información, consulte [SQL Server AlwaysOn para una base de datos de sitio de alta disponibilidad para System Center Configuration Manager](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).|  
|Modificar la replicación entre sitios|Consulte [Transferencias de datos entre sitios en System Center Configuration Manager](../../../../core/servers/manage/data-transfers-between-sites.md) para más información acerca de los siguientes temas:<br /><br /> Configurar la [replicación basada en archivos](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute) entre sitios secundarios<br /><br /> Configurar [vínculos de replicación de base de datos](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> Configurar [vistas distribuidas](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  
