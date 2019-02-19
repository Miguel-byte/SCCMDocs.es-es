---
title: Planeación de informes
titleSuffix: Configuration Manager
description: Desde la información de instalación hasta la seguridad y el ancho de banda de red, es importante planear los informes en Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9920b8b16f076fe9f0ebf807f4231e262fcabf33
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123168"
---
# <a name="planning-for-reporting-in-system-center-configuration-manager"></a>Planeación de informes en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los informes de System Center Configuration Manager proporcionan un conjunto de herramientas y recursos para usar funciones avanzadas de informes de SQL Server Reporting Services. Use las siguientes secciones para planear informes en Configuration Manager.  

##  <a name="BKMK_InstallReportingServicesPoint"></a> Decidir la ubicación de la instalación del punto de servicios de informes  
 Cuando ejecuta informes de Configuration Manager en un sitio, los informes tienen acceso a la información en la base de datos del sitio al que se conectan. Utilice las secciones siguientes para decidir la ubicación de la instalación del punto de servicios de informes y el origen de datos que se debe usar.  

> [!NOTE]  
>  Para obtener más información sobre la planeación de sistemas de sitio en Configuration Manager, consulte [Add site system roles](../deploy/configure/add-site-system-roles.md) (Agregar roles de sistema de sitio).  

###  <a name="BKMK_SupportedSiteServers"></a> Servidores de sistema de sitio admitidos  
 Puede instalar el punto de servicios de informes en un sitio de administración central y en sitios primarios, y en varios sistemas de sitio en un sitio y en otros sitios en la jerarquía. El punto de servicios de informes no se admite en sitios secundarios. El primer punto de servicios de informes en un sitio está configurado como el servidor de informes predeterminado. Puede agregar más puntos de servicios de informes en un sitio, pero los informes de Configuration Manager usan activamente el servidor de informes predeterminado de cada sitio. Puede instalar el punto de servicios de informes en un servidor de sitio o en un sistema de sitio remoto. Sin embargo, por motivos de rendimiento, se recomienda utilizar Reporting Services en un servidor de sistema de sitio remoto.  

###  <a name="BKMK_DataReplication"></a> Consideraciones de replicación de datos  
 Configuration Manager clasifica los datos que replica como datos globales o datos de sitio. Los datos globales hacen referencia a objetos creados por usuarios administrativos que se replican en todos los sitios de la jerarquía, mientras que los sitios secundarios solo reciben un subconjunto de los datos globales. Entre los ejemplos de datos globales se incluyen implementaciones de software, actualizaciones de software, recopilaciones y ámbitos de seguridad de administración basada en roles. Los datos de sitio hacen referencia a información operativa creada por sitios primarios de Configuration Manager y los clientes que se comunican con los sitios primarios. Los datos de sitio se replican en el sitio de administración central pero no en otros sitios primarios. Entre los ejemplos de datos de sitio se incluyen datos de inventario de hardware, mensajes de estado, alertas y los resultados de las recopilaciones basadas en consultas. Los datos de sitio solo son visibles en el sitio de administración central y en el sitio primario en el que se originan los datos.  

 Tenga en cuenta los factores siguientes para determinar la ubicación de la instalación de los puntos de servicios de informes:  

-   Un punto de servicios de informes con la base de datos del sitio de administración central como origen de datos de informes tiene acceso a todos los datos globales y datos de sitio en la jerarquía de Configuration Manager. Si necesita informes que contienen datos de sitio de varios sitios en la jerarquía, considere la opción de instalar el punto de servicios de informes en un sistema de sitio en el sitio de administración central y use la base de datos del sitio de administración central como el origen de datos de informes.  

-   Un punto de servicios de informes con la base de datos del sitio primario secundario como origen de datos de informes tiene acceso a los datos globales y a los datos de sitio solo del sitio primario local y de los sitios secundarios. Los datos de sitio de otros sitios primarios en la jerarquía de Configuration Manager no se replican en el sitio primario y, por lo tanto, Reporting Services no puede acceder a los mismos. Si precisa informes que contengan datos de sitio de un determinado sitio primario o datos globales, pero no desea que el usuario de informes tenga acceso a los datos de sitio de otros sitios primarios, instale un punto de servicios de informes en un sistema de sitio en el sitio primario y use la base de datos del sitio primario como origen de datos de informes.  

###  <a name="BKMK_NetworkBandwidth"></a> Consideraciones de ancho de banda de red  
 Los servidores de sistema de sitio en el mismo sitio se comunican entre ellos mediante el uso del protocolo de bloque de mensajes del servidor (SMB), HTTP o HTTPS, en función de la configuración del sitio. Como estas comunicaciones no están administradas y pueden producirse en cualquier momento sin control de ancho de banda de red, revise el ancho de banda de red disponible antes de instalar el rol de punto de servicios de informes en un sistema de sitio.  

> [!NOTE]  
>  Para obtener más información sobre la planeación de sistemas de sitio, consulte [Add site system roles](../deploy/configure/add-site-system-roles.md) (Agregar roles de sistema de sitio).  

##  <a name="BKMK_RoleBaseAdministration"></a> Planeación de la administración basada en roles para informes  
 La seguridad de los informes es como la de otros objetos en Configuration Manager: puede asignar roles y permisos de seguridad a los usuarios administrativos. Los usuarios administrativos solo pueden ejecutar y modificar informes para los que tengan los derechos de seguridad apropiados. Para ejecutar informes en la consola de Configuration Manager, debe tener derechos de **Lectura** para el permiso de **Sitio** y los permisos configurados para los objetos correspondientes.  

 Pero, a diferencia de otros objetos en Configuration Manager, los derechos de seguridad que configura para usuarios administrativos en la consola de Configuration Manager también deben configurarse en Reporting Services. Cuando configura los derechos de seguridad en la consola de Configuration Manager, el punto de servicios de informes se conecta a Reporting Services y configura los permisos adecuados para los informes. Por ejemplo, el rol de seguridad **Administrador de actualizaciones de software** tiene asociados los permisos **Ejecutar informe** y **Modificar informe** . Los usuarios administrativos a los que solo se asigna el rol **Administrador de actualizaciones de software** solo pueden ejecutar y modificar informes de actualizaciones de software. Los informes de otros objetos no se muestran en la consola de Configuration Manager, pero, como excepción a esta regla, algunos informes no están asociados a ningún objeto protegible de Configuration Manager específico. Para estos informes, el usuario administrativo debe tener el derecho de **Leer** para que el permiso **Sitio** ejecute informes, y el derecho **Modificar** para que el permiso **Sitio** modifique informes.  

 Los informes están totalmente habilitados para la administración basada en roles. Los datos de todos los informes incluidos con Configuration Manager se filtran en función de los permisos del usuario administrativo que ejecuta el informe. Los usuarios administrativos con roles específicos solo pueden ver la información definida para sus roles.  

 Para obtener más información sobre los derechos de seguridad de los informes, consulte [Configure reporting](configuring-reporting.md) (Configurar los informes).  

 Para obtener más información sobre la administración basada en roles en Configuration Manager, consulte [Configurar la administración basada en roles](../deploy/configure/configure-role-based-administration.md).  

## <a name="next-steps"></a>Pasos siguientes  
 Utilice los temas adicionales siguientes para planear informes en Configuration Manager:  

-   [Requisitos previos de los informes en System Center Configuration Manager](../../../core/servers/manage/prerequisites-for-reporting.md)  
-   [Prácticas recomendadas para la generación de informes en System Center Configuration Manager](../../../core/servers/manage/best-practices-for-reporting.md)  
