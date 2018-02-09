---
title: Servidores de sistema de sitio admitidos
titleSuffix: Configuration Manager
description: "Obtenga información sobre qué versiones de Windows puede usar para hospedar un sitio o rol de sistema de sitio de System Center Configuration Manager."
ms.custom: na
ms.date: 06/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 18df431f0fd1b355b1ad629a10126907187ddbbd
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2018
---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>Sistemas operativos compatibles con servidores de sistema de sitio de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


En este artículo, se detallan las versiones de Windows que puede usar para hospedar un sitio o rol de sistema de sitio de System Center Configuration Manager.


Use la información de este artículo con la información de los artículos siguientes:
-   [Hardware recomendado para Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md)
-   [Sitio y requisitos previos de sistema de sitio para Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Números de tamaño y escala para Configuration Manager](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016-standard-and-datacenter"></a>Windows Server 2016: Standard y Datacenter
A partir de la versión 1606 con el paquete acumulativo de revisiones de KB3186654 (o la versión de línea base de 1606 publicada en octubre de 2016), el sistema operativo admite lo siguiente:

**Servidores de sitio:**  

-   Sitio de administración central  

-   Sitio primario  

-   Sitio secundario  

**Servidores de sistema de sitio:**  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de sincronización de Asset Intelligence  

-   Punto de registro de certificados  

-   Punto de distribución  

     Los puntos de distribución admiten varias configuraciones diferentes y cada uno tiene requisitos diferentes. En algunos casos, estas configuraciones admiten la instalación no solo en los servidores sino también en sistemas operativos de clientes. Para obtener más información sobre las opciones disponibles para los puntos de distribución, vea [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto de Endpoint Protection  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

-   Punto de estado de reserva  

-   Punto de administración

-   Punto de servicios de informes  

-   Punto de conexión de servicio  

-   Servidor de base de datos del sitio  

     No se admiten servidores de base de datos del sitio en un controlador de dominio de solo lectura (RODC). Para obtener más información, consulte [Puede encontrar problemas al instalar a SQL Server en un controlador de dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) en Microsoft Knowledge Base. Además, los servidores de sitio secundario no se admiten en ningún controlador de dominio.  

-   SMS_Provider  

-   Punto de actualización de software  

-   Punto de migración de estado

## <a name="windows-server-2012-r2-x64-standard-and-datacenter"></a>Windows Server 2012 R2 (x64): Standard y Datacenter  
**Servidores de sitio:**  

-   Sitio de administración central  

-   Sitio primario  

-   Sitio secundario  

**Servidores de sistema de sitio:**  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de sincronización de Asset Intelligence  

-   Punto de registro de certificados  

-   Punto de distribución  

     Los puntos de distribución admiten varias configuraciones diferentes y cada uno tiene requisitos diferentes. En algunos casos, estas configuraciones admiten la instalación no solo en los servidores sino también en sistemas operativos de clientes. Para obtener más información sobre las opciones disponibles para los puntos de distribución, vea [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto de Endpoint Protection  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

-   Punto de estado de reserva  

-   Punto de administración

-   Punto de servicios de informes  

-   Punto de conexión de servicio  

-   Servidor de base de datos del sitio  

     No se admiten servidores de base de datos del sitio en un controlador de dominio de solo lectura (RODC). Para obtener más información, consulte [Puede encontrar problemas al instalar a SQL Server en un controlador de dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) en Microsoft Knowledge Base. Además, los servidores de sitio secundario no se admiten en ningún controlador de dominio.  

-   SMS_Provider  

-   Punto de actualización de software  

-   Punto de migración de estado  

## <a name="windows-server-2012-x64-standard-and-datacenter"></a>Windows Server 2012 (x64): Standard y Datacenter  
**Servidores de sitio:**  

-   Sitio de administración central  

-   Sitio primario  

-   Sitio secundario  

**Servidores de sistema de sitio:**  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de sincronización de Asset Intelligence  

-   Punto de registro de certificados  

-   Punto de distribución  

     Los puntos de distribución admiten varias configuraciones diferentes y cada uno tiene requisitos diferentes. En algunos casos, estas configuraciones admiten la instalación no solo en los servidores sino también en sistemas operativos de clientes. Para obtener más información sobre las opciones disponibles para los puntos de distribución, vea [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto de Endpoint Protection  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

-   Punto de estado de reserva  

-   Punto de administración

-   Punto de servicios de informes  

-   Punto de conexión de servicio  

-   Servidor de base de datos del sitio  

     No se admiten servidores de base de datos del sitio en un controlador de dominio de solo lectura (RODC). Para obtener más información, consulte [Puede encontrar problemas al instalar a SQL Server en un controlador de dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) en Microsoft Knowledge Base. Además, los servidores de sitio secundario no se admiten en ningún controlador de dominio.  

-   SMS_Provider  

-   Punto de actualización de software  

-   Punto de migración de estado  

## <a name="windows-server-2008-r2-with-sp1-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 R2 con SP1 (x64): Standard, Enterprise y Datacenter  
 Windows Server 2008 R2 tiene ahora soporte extendido y ya no está dentro del soporte estándar, tal y como se detalla en el [Ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle). Para obtener más información sobre la compatibilidad futura de estos sistemas operativos como servidores de sistema de sitio con Configuration Manager, consulte [Deprecated server operating systems](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems) (Sistemas operativos de servidor en desuso).  

 A partir de la versión 1702 de Configuration Manager, este sistema operativo no es compatible para los servidores de sitio o la mayoría de los roles de sistema de sitio, pero se seguirá admitiendo para el rol de sistema de sitio del punto de distribución (incluidos los puntos de distribución de extracción, así como para el entorno PXE y multidifusión).

 Las versiones anteriores a la 1702 continuarán admitiendo su uso para lo siguiente.


**Servidores de sitio:**  

-   Sitio de administración central  

-   Sitio primario  

-   Sitio secundario  

**Servidores de sistema de sitio:**  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de sincronización de Asset Intelligence  

-   Punto de registro de certificados  

-   Punto de distribución  

     Los puntos de distribución admiten varias configuraciones diferentes y cada uno tiene requisitos diferentes. En algunos casos, estas configuraciones admiten la instalación no solo en los servidores sino también en sistemas operativos de clientes. Para obtener más información sobre las opciones disponibles para los puntos de distribución, vea [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto de Endpoint Protection  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

-   Punto de estado de reserva  

-   Punto de administración

-   Punto de servicios de informes  

-   Punto de conexión de servicio  

-   Servidor de base de datos del sitio  

     No se admiten servidores de base de datos del sitio en un controlador de dominio de solo lectura (RODC). Para obtener más información, consulte [Puede encontrar problemas al instalar a SQL Server en un controlador de dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) en Microsoft Knowledge Base. Además, los servidores de sitio secundario no se admiten en ningún controlador de dominio.  

-   SMS_Provider  

-   Punto de actualización de software  

-   Punto de migración de estado  

## <a name="windows-server-2008-with-sp2-x86-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 con SP2 (x86, x64): Standard, Enterprise y Datacenter  
 Windows Server 2008 tiene ahora soporte extendido y ya no está dentro del soporte estándar, tal y como se detalla en el [Ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle). Para obtener más información sobre la compatibilidad futura de estos sistemas operativos como servidores de sistema de sitio con Configuration Manager, consulte [Deprecated server operating systems](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems) (Sistemas operativos de servidor en desuso).  

No se admite este sistema operativo para servidores de sitio o roles de sistema de sitio con la excepción del punto de distribución y el punto de distribución de extracción. Puede seguir usando este sistema operativo como un punto de distribución hasta que se anuncie que esta compatibilidad queda obsoleta o expire el período extendido de soporte técnico de este sistema operativo. Para más información, vea [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095) (La instalación de System Center Configuration Manager CB y LTBS produce un error en Windows Server 2008).

**Servidores de sistema de sitio:**  
-   Punto de distribución  

    -   Los puntos de distribución en esta versión del sistema operativo no son compatibles con Multidifusión.  

    -   Los puntos de distribución en este sistema operativo son compatibles con PXE, pero no admiten el arranque de red de los equipos cliente en modo EFI. Se admiten los equipos cliente con arranque de EFI o BIOS en modo heredado.  

    -   Los puntos de distribución admiten varias configuraciones diferentes y cada uno tiene requisitos diferentes. En algunos casos, estas configuraciones admiten la instalación no solo en los servidores sino también en sistemas operativos de clientes. Para obtener más información sobre las opciones disponibles para los puntos de distribución, vea [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-10-x86-x64-pro-and-enterprise"></a>Windows 10 (x86, x64): Pro y Enterprise  
**Servidores de sistema de sitio:**  

-   Punto de distribución  

    -   Los puntos de distribución en este sistema operativo no son compatibles con PXE.  

    -   Los puntos de distribución en esta versión del sistema operativo no son compatibles con Multidifusión.  

    -   Los puntos de distribución admiten varias configuraciones diferentes y cada uno tiene requisitos diferentes. En algunos casos, estas configuraciones admiten la instalación no solo en los servidores sino también en sistemas operativos de clientes. Para obtener más información sobre las opciones disponibles para los puntos de distribución, vea [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-81-x86-x64-professional-and-enterprise"></a>Windows 8.1 (x86, x64): Professional y Enterprise  
**Servidores de sistema de sitio:**  

-   Punto de distribución  

    -   Los puntos de distribución en este sistema operativo no son compatibles con PXE.  

    -   Los puntos de distribución en esta versión del sistema operativo no son compatibles con Multidifusión.  

    -   Los puntos de distribución admiten varias configuraciones diferentes y cada uno tiene requisitos diferentes. En algunos casos, estas configuraciones admiten la instalación no solo en los servidores sino también en sistemas operativos de clientes. Para obtener más información sobre las opciones disponibles para los puntos de distribución, vea [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

<!--## Windows 8 (x86, x64): Professional and Enterprise
**Site system servers:**  

-   Distribution point  

    -   Distribution points on this operating system are not supported for PXE.  

    -   Distribution points on this operating system version do not support Multicast.  

    -   Distribution points support several different configurations that each have different requirements. In some cases, these configurations support installation not only on servers, but on client operating systems. For more information about the options that are available for distribution points, see [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  
   
    -  - -removed Jan 12,2018 sms505863-->

## <a name="windows-7-with-sp1-x86-x64-professional-enterprise-and-ultimate"></a>Windows 7 con SP1 (x86, x64): Professional, Enterprise y Ultimate  
**Servidores de sistema de sitio:**  

-   Punto de distribución  

    -   Los puntos de distribución en este sistema operativo no son compatibles con PXE.  

    -   Los puntos de distribución en esta versión del sistema operativo no son compatibles con Multidifusión.  

    -   Los puntos de distribución admiten varias configuraciones diferentes y cada uno tiene requisitos diferentes. En algunos casos, estas configuraciones admiten la instalación no solo en los servidores sino también en sistemas operativos de clientes. Para obtener más información sobre las opciones disponibles para los puntos de distribución, vea [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


## <a name="the-server-core-installation-of-windows-server-2016"></a>La instalación Server Core de Windows Server 2016
A partir de la versión 1606 con el paquete acumulativo de revisiones de KB3186654 (o la versión de línea base de 1606 publicada en octubre de 2016), el sistema operativo puede usarse como punto de distribución, con las siguientes limitaciones:  
  -   Solo se admite la versión de 64 bits.
  -   Los puntos de distribución de este sistema operativo no son compatibles con PXE o Multidifusión.  


## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>La instalación de Server Core de Windows Server 2012 R2  
 Además de los sistemas operativos anteriores que se muestran, la instalación Server Core de Windows Server 2012 R2 se admite para su uso como un punto de distribución con las siguientes limitaciones:  

-   Solo se admite la versión de 64 bits.

-   Los puntos de distribución de este sistema operativo no son compatibles con PXE o Multidifusión.  

## <a name="the-server-core-installation-of-windows-server-2012"></a>La instalación Server Core de Windows Server 2012  
 Además de los sistemas operativos anteriores que se muestran, la instalación Server Core de Windows Server 2012 también se admite para su uso como un punto de distribución con las siguientes limitaciones:  

-   Solo se admite la versión de 64 bits.  

-   Los puntos de distribución de este sistema operativo no son compatibles con PXE o Multidifusión.
