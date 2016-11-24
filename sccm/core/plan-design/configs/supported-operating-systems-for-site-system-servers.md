---
title: Servidores de sistema de sitio compatibles | System Center Configuration Manager
description: "Obtenga información sobre qué versiones de Windows puede usar para hospedar un sitio o rol de sistema de sitio de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: 44
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 00d5d8d9ce90b2da79485250d25f943ca1c4547b


---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>Sistemas operativos compatibles con servidores de sistema de sitio de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


En este artículo, se detallan las versiones de Windows que puede usar para hospedar un sitio o rol de sistema de sitio de System Center Configuration Manager.


Utilice la información de este tema con la información de los siguientes artículos:
-   [Hardware recomendado para Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md)
-   [Sitio y requisitos previos de sistema de sitio para Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Números de tamaño y escala para Configuration Manager](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016---standard-datacenter"></a>Windows Server 2016: Standard, Datacenter
Windows Server 2016 se admite a partir de la versión 1606 de Configuration Manager con el paquete acumulativo de revisiones de KB3186654 (o la versión de línea base de 1606 que se ha publicado en octubre de 2016).

**Servidores de sitio:**  

-   Sitio de administración central  

-   Sitio primario  

-   Sitio secundario  

**Servidores de sistema de sitio:**  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de sincronización de Asset Intelligence  

-   Punto de registro de certificado  

-   Punto de distribución  

     Los puntos de distribución admiten varias configuraciones distintas cada una con requisitos diferentes y, en algunos casos, admiten la instalación no solo en servidores, sino también en sistemas operativos cliente. Para obtener más información sobre las opciones disponibles para los puntos de distribución, consulte [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto de Endpoint Protection  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

-   Punto de estado de reserva  

-   Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.  

-   Punto de conexión de servicio  

-   Servidor de base de datos del sitio  

     No se admiten servidores de base de datos del sitio en un controlador de dominio de solo lectura (RODC). Para obtener más información, consulte [Puede encontrar problemas al instalar a SQL Server en un controlador de dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) en Microsoft Knowledge Base. Además, los servidores de sitio secundario no se admiten en ningún controlador de dominio.  

-   SMS_Provider  

-   Punto de actualización de software  

-   Punto de migración de estado

## <a name="windows-server-2012-r2-x64---standard-datacenter"></a>Windows Server 2012 R2 (x64): Standard, Datacenter  
**Servidores de sitio:**  

-   Sitio de administración central  

-   Sitio primario  

-   Sitio secundario  

**Servidores de sistema de sitio:**  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de sincronización de Asset Intelligence  

-   Punto de registro de certificado  

-   Punto de distribución  

     Los puntos de distribución admiten varias configuraciones distintas cada una con requisitos diferentes y, en algunos casos, admiten la instalación no solo en servidores, sino también en sistemas operativos cliente. Para obtener más información sobre las opciones disponibles para los puntos de distribución, consulte [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto de Endpoint Protection  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

-   Punto de estado de reserva  

-   Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.  

-   Punto de conexión de servicio  

-   Servidor de base de datos del sitio  

     No se admiten servidores de base de datos del sitio en un controlador de dominio de solo lectura (RODC). Para obtener más información, consulte [Puede encontrar problemas al instalar a SQL Server en un controlador de dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) en Microsoft Knowledge Base. Además, los servidores de sitio secundario no se admiten en ningún controlador de dominio.  

-   SMS_Provider  

-   Punto de actualización de software  

-   Punto de migración de estado  

## <a name="windows-server-2012-x64---standard-datacenter"></a>Windows Server 2012 (x64): Standard, Datacenter  
**Servidores de sitio:**  

-   Sitio de administración central  

-   Sitio primario  

-   Sitio secundario  

**Servidores de sistema de sitio:**  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de sincronización de Asset Intelligence  

-   Punto de registro de certificado  

-   Punto de distribución  

     Los puntos de distribución admiten varias configuraciones distintas cada una con requisitos diferentes y, en algunos casos, admiten la instalación no solo en servidores, sino también en sistemas operativos cliente. Para obtener más información sobre las opciones disponibles para los puntos de distribución, consulte [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto de Endpoint Protection  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

-   Punto de estado de reserva  

-   Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.  

-   Punto de conexión de servicio  

-   Servidor de base de datos del sitio  

     No se admiten servidores de base de datos del sitio en un controlador de dominio de solo lectura (RODC). Para obtener más información, consulte [Puede encontrar problemas al instalar a SQL Server en un controlador de dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) en Microsoft Knowledge Base. Además, los servidores de sitio secundario no se admiten en ningún controlador de dominio.  

-   SMS_Provider  

-   Punto de actualización de software  

-   Punto de migración de estado  

## <a name="windows-server-2008-r2-with-sp1-x64---standard-enterprise-datacenter"></a>Windows Server 2008 R2 con SP1 (x64): Standard, Enterprise, Datacenter  
 Windows Server 2008 R2 goza ahora de soporte extendido, y ya no está dentro del soporte estándar, tal y como se detalla en el  [Ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle). Para obtener más información sobre la compatibilidad futura de estos sistemas operativos como servidores de sistema de sitio con Configuration Manager, consulte [Características eliminadas y en desuso de System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

**Servidores de sitio:**  

-   Sitio de administración central  

-   Sitio primario  

-   Sitio secundario  

**Servidores de sistema de sitio:**  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de sincronización de Asset Intelligence  

-   Punto de registro de certificado  

-   Punto de distribución  

     Los puntos de distribución admiten varias configuraciones distintas cada una con requisitos diferentes y, en algunos casos, admiten la instalación no solo en servidores, sino también en sistemas operativos cliente. Para obtener más información sobre las opciones disponibles para los puntos de distribución, consulte [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto de Endpoint Protection  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

-   Punto de estado de reserva  

-   Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.  

-   Punto de conexión de servicio  

-   Servidor de base de datos del sitio  

     No se admiten servidores de base de datos del sitio en un controlador de dominio de solo lectura (RODC). Para obtener más información, consulte [Puede encontrar problemas al instalar a SQL Server en un controlador de dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) en Microsoft Knowledge Base. Además, los servidores de sitio secundario no se admiten en ningún controlador de dominio.  

-   SMS_Provider  

-   Punto de actualización de software  

-   Punto de migración de estado  

## <a name="windows-server-2008-with-sp2-x86-x64---standard-enterprise-datacenter"></a>Windows Server 2008 con SP2 (x86, x64): Standard, Enterprise, Datacenter  
 Windows Server 2008 goza ahora de soporte extendido, y ya no está dentro del soporte estándar, tal y como se detalla en el  [Ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle). Para obtener más información sobre la compatibilidad futura de estos sistemas operativos como servidores de sistema de sitio con Configuration Manager, consulte [Características eliminadas y en desuso de System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

**Servidores de sitio:**  

-   Sitio de administración central  

-   Sitio primario  

-   Sitio secundario  

**Servidores de sistema de sitio:**  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de sincronización de Asset Intelligence  

-   Punto de registro de certificado  

-   Punto de distribución  

    -   Los puntos de distribución en esta versión del sistema operativo no son compatibles con Multidifusión.  

    -   Los puntos de distribución en este sistema operativo son compatibles con PXE, pero no admiten el arranque de red de los equipos cliente en modo EFI. Se admiten los equipos cliente con arranque de EFI o BIOS en modo heredado.  

    -   Los puntos de distribución admiten varias configuraciones distintas cada una con requisitos diferentes y, en algunos casos, admiten la instalación no solo en servidores, sino también en sistemas operativos cliente. Para obtener más información sobre las opciones disponibles para los puntos de distribución, consulte [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto de Endpoint Protection  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

-   Punto de estado de reserva  

-   Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.  

-   Punto de conexión de servicio  

-   Servidor de base de datos del sitio  

     No se admiten servidores de base de datos del sitio en un controlador de dominio de solo lectura (RODC). Para obtener más información, consulte [Puede encontrar problemas al instalar a SQL Server en un controlador de dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) en Microsoft Knowledge Base. Además, los servidores de sitio secundario no se admiten en ningún controlador de dominio.  

-   SMS_Provider  

-   Punto de actualización de software  

-   Punto de migración de estado  

## <a name="windows-10-x86-x64---pro-enterprise"></a>Windows 10 (x86, x64): Pro, Enterprise  
**Servidores de sistema de sitio:**  

-   Punto de distribución  

    -   Los puntos de distribución en este sistema operativo no son compatibles con PXE.  

    -   Los puntos de distribución en esta versión del sistema operativo no son compatibles con Multidifusión.  

    -   Los puntos de distribución admiten varias configuraciones distintas cada una con requisitos diferentes y, en algunos casos, admiten la instalación no solo en servidores, sino también en sistemas operativos cliente. Para obtener más información sobre las opciones disponibles para los puntos de distribución, consulte [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-81-x86-x64---professional-enterprise"></a>Windows 8.1 (x86, x64): Professional, Enterprise  
**Servidores de sistema de sitio:**  

-   Punto de distribución  

    -   Los puntos de distribución en este sistema operativo no son compatibles con PXE.  

    -   Los puntos de distribución en esta versión del sistema operativo no son compatibles con Multidifusión.  

    -   Los puntos de distribución admiten varias configuraciones distintas cada una con requisitos diferentes y, en algunos casos, admiten la instalación no solo en servidores, sino también en sistemas operativos cliente. Para obtener más información sobre las opciones disponibles para los puntos de distribución, consulte [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-8-x86-x64---professional-enterprise-distribution-point"></a>Windows 8 (x86, x64): punto de distribución Professional, Enterprise  
**Servidores de sistema de sitio:**  

-   Punto de distribución  

    -   Los puntos de distribución en este sistema operativo no son compatibles con PXE.  

    -   Los puntos de distribución en esta versión del sistema operativo no son compatibles con Multidifusión.  

    -   Los puntos de distribución admiten varias configuraciones distintas cada una con requisitos diferentes y, en algunos casos, admiten la instalación no solo en servidores, sino también en sistemas operativos cliente. Para obtener más información sobre las opciones disponibles para los puntos de distribución, consulte [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-7-with-sp1-x86-x64---professional-enterprise-ultimate"></a>Windows 7 con SP1 (x86, x64): Professional, Enterprise, Ultimate  
**Servidores de sistema de sitio:**  

-   Punto de distribución  

    -   Los puntos de distribución en este sistema operativo no son compatibles con PXE.  

    -   Los puntos de distribución en esta versión del sistema operativo no son compatibles con Multidifusión.  

    -   Los puntos de distribución admiten varias configuraciones distintas cada una con requisitos diferentes y, en algunos casos, admiten la instalación no solo en servidores, sino también en sistemas operativos cliente. Para obtener más información sobre las opciones disponibles para los puntos de distribución, consulte [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="the-server-core-installation-of-windows-server-2012"></a>La instalación Server Core de Windows Server 2012  
 Además de los sistemas operativos anteriores, la instalación Server Core de Windows Server 2012 se puede usar como punto de distribución con las siguientes limitaciones:  

-   Solo se admite x64  

-   Los puntos de distribución en este sistema operativo no son compatibles con PXE o Multidifusión.  

## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>La instalación de Server Core de Windows Server 2012 R2  
 Además de los sistemas operativos anteriores, la instalación Server Core de Windows Server 2012 R2 se puede usar como punto de distribución con las siguientes limitaciones:  

-   Solo se admite x64  

-   Los puntos de distribución en este sistema operativo no son compatibles con PXE o Multidifusión.  



<!--HONumber=Nov16_HO1-->


