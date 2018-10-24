---
title: Servidores de sistema de sitio admitidos
titleSuffix: Configuration Manager
description: Obtenga información sobre qué versiones de Windows puede usar para hospedar un sitio o rol de sistema de sitio de Configuration Manager.
ms.date: 10/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fd8e815ab57730ad2186a7e75cd51f21012383a
ms.sourcegitcommit: 265d38d55ca0db043e3a7131a56f123e1d98aa5b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/03/2018
ms.locfileid: "48236181"
---
# <a name="supported-operating-systems-for-configuration-manager-site-system-servers"></a>Sistemas operativos compatibles con servidores de sistema de sitio de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


En este artículo, se detallan las versiones de Windows que puede usar para hospedar un sitio o un rol de sistema de sitio de Configuration Manager.


Use la información de este artículo con la información de los artículos siguientes:
-   [Hardware recomendado para Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware)
-   [Sitio y requisitos previos de sistema de sitio para Configuration Manager](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
-   [Números de tamaño y escala para Configuration Manager](/sccm/core/plan-design/configs/size-and-scale-numbers)



## <a name="bkmk_2016"></a> Windows Server 2016: Standard y Datacenter

Con el paquete acumulativo de actualizaciones 1 para Configuration Manager versión 1606 ([KB3186654](https://support.microsoft.com/help/3186654)), se admite esta versión de sistema operativo para estos roles:

#### <a name="site-servers"></a>Servidores de sitio

-   Sitio de administración central  
-   Sitio primario  
-   Sitio secundario  

#### <a name="site-system-servers"></a>Servidores de sistema de sitio

-   Punto de servicio web del catálogo de aplicaciones  
-   Punto de sitios web del catálogo de aplicaciones  
-   Punto de sincronización de Asset Intelligence  
-   Punto de registro de certificados  
-   Punto de conexión de Cloud Management Gateway  
-   Punto de servicio de almacenamiento de datos  
-   Punto de distribución <sup>[Nota 1](#bkmk_note1)</sup>  
-   Punto de Endpoint Protection  
-   Punto de inscripción  
-   Punto de proxy de inscripción  
-   Punto de estado de reserva  
-   Punto de administración
-   Punto de servicios de informes  
-   Punto de conexión de servicio  
-   Servidor de base de datos del sitio <sup>[Nota 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   Punto de actualización de software  
-   Punto de migración de estado



## <a name="bkmk_stor2016"></a> Windows Storage Server 2016

#### <a name="site-system-server"></a>Servidor de sistema de sitio

-   Punto de distribución <sup>[Nota 1](#bkmk_note1)</sup>  



## <a name="bkmk_2012r2"></a> Windows Server 2012 R2 (x64): Standard y Datacenter  

#### <a name="site-servers"></a>Servidores de sitio

-   Sitio de administración central  
-   Sitio primario  
-   Sitio secundario  

#### <a name="site-system-servers"></a>Servidores de sistema de sitio

-   Punto de servicio web del catálogo de aplicaciones  
-   Punto de sitios web del catálogo de aplicaciones  
-   Punto de sincronización de Asset Intelligence  
-   Punto de registro de certificados  
-   Punto de conexión de Cloud Management Gateway  
-   Punto de servicio de almacenamiento de datos  
-   Punto de distribución <sup>[Nota 1](#bkmk_note1)</sup>  
-   Punto de Endpoint Protection  
-   Punto de inscripción  
-   Punto de proxy de inscripción  
-   Punto de estado de reserva  
-   Punto de administración
-   Punto de servicios de informes  
-   Punto de conexión de servicio  
-   Servidor de base de datos del sitio <sup>[Nota 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   Punto de actualización de software  
-   Punto de migración de estado  



## <a name="bkmk_2012"></a> Windows Server 2012 (x64): Standard y Datacenter  

#### <a name="site-servers"></a>Servidores de sitio

-   Sitio de administración central  
-   Sitio primario  
-   Sitio secundario  

#### <a name="site-system-servers"></a>Servidores de sistema de sitio

-   Punto de servicio web del catálogo de aplicaciones  
-   Punto de sitios web del catálogo de aplicaciones  
-   Punto de sincronización de Asset Intelligence  
-   Punto de registro de certificados  
-   Punto de conexión de Cloud Management Gateway  
-   Punto de servicio de almacenamiento de datos  
-   Punto de distribución <sup>[Nota 1](#bkmk_note1)</sup>  
-   Punto de Endpoint Protection  
-   Punto de inscripción  
-   Punto de proxy de inscripción  
-   Punto de estado de reserva  
-   Punto de administración
-   Punto de servicios de informes  
-   Punto de conexión de servicio  
-   Servidor de base de datos del sitio <sup>[Nota 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   Punto de actualización de software  
-   Punto de migración de estado  



## <a name="bkmk_2008r2sp1"></a> Windows Server 2008 R2 con SP1 (x64): Standard, Enterprise y Datacenter  

Windows Server 2008 R2 tiene ahora soporte extendido y ya no está dentro del soporte estándar, tal y como se detalla en el [Ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle). Para obtener más información sobre la compatibilidad futura de estos sistemas operativos como servidores de sistema de sitio con Configuration Manager, consulte [Deprecated server operating systems](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems) (Sistemas operativos de servidor en desuso).  

Este sistema operativo no es compatible con servidores de sitio o la mayoría de los roles del sistema de sitio. Todavía se admite para el rol de sistema de sitio del punto de distribución, incluidos los puntos de distribución de extracción y para el entorno PXE y la multidifusión.

#### <a name="site-system-servers"></a>Servidores de sistema de sitio
-   Punto de distribución <sup>[Nota 1](#bkmk_note1)</sup>  

    - Los puntos de distribución de este sistema operativo son compatibles con el entorno PXE y multidifusión.  



## <a name="bkmk_2008sp2"></a> Windows Server 2008 con SP2 (x86, x64): Standard, Enterprise y Datacenter  

Windows Server 2008 tiene ahora soporte extendido y ya no está dentro del soporte estándar, tal y como se detalla en el [Ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle). Para obtener más información sobre la compatibilidad futura de estos sistemas operativos como servidores de sistema de sitio con Configuration Manager, consulte [Deprecated server operating systems](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems) (Sistemas operativos de servidor en desuso).  

Este sistema operativo no se admite para servidores de sitio o roles del sistema de sitio, excepto para el punto de distribución y el punto de distribución de extracción. Siga usando este sistema operativo como un punto de distribución hasta que se anuncie que esta compatibilidad queda obsoleta, o bien expire el período extendido de soporte técnico de este sistema operativo. Para más información, vea [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095) (La instalación de System Center Configuration Manager CB y LTBS produce un error en Windows Server 2008).

#### <a name="site-system-servers"></a>Servidores de sistema de sitio
-   Punto de distribución <sup>[Nota 1](#bkmk_note1)</sup>  

    -   Los puntos de distribución de este sistema operativo son compatibles con el entorno PXE y multidifusión.  

    -   Los puntos de distribución de este sistema operativo no admiten el arranque de red de los equipos cliente en modo EFI. Se admiten los equipos cliente con arranque de EFI o BIOS en modo heredado.  



## <a name="bkmk_win10"></a> Windows 10 (x86, x64): Pro y Enterprise  

#### <a name="site-system-servers"></a>Servidores de sistema de sitio

-   Punto de distribución <sup>[Nota 1](#bkmk_note1)</sup>  

    -   Los puntos de distribución de este sistema operativo no son compatibles para el entorno PXE con los Servicios de implementación de Windows predeterminados. A partir de la versión 1806, puede habilitar para el entorno PXE un punto de distribución de este sistema operativo con la opción **Habilitar un respondedor PXE sin Servicios de implementación de Windows**. Para obtener más información, vea [Instalación y configuración de puntos de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   Los puntos de distribución en esta versión del sistema operativo no son compatibles con multidifusión.  



## <a name="bkmk_win81"></a> Windows 8.1 (x86, x64): Professional y Enterprise  

#### <a name="site-system-servers"></a>Servidores de sistema de sitio

-   Punto de distribución <sup>[Nota 1](#bkmk_note1)</sup>  

    -   Los puntos de distribución de este sistema operativo no son compatibles para el entorno PXE con los Servicios de implementación de Windows predeterminados. A partir de la versión 1806, puede habilitar para el entorno PXE un punto de distribución de este sistema operativo con la opción **Habilitar un respondedor PXE sin Servicios de implementación de Windows**. Para obtener más información, vea [Instalación y configuración de puntos de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   Los puntos de distribución en esta versión del sistema operativo no son compatibles con multidifusión.  



## <a name="bkmk_win7sp1"></a> Windows 7 con SP1 (x86, x64): Professional, Enterprise y Ultimate  

#### <a name="site-system-servers"></a>Servidores de sistema de sitio

-   Punto de distribución <sup>[Nota 1](#bkmk_note1)</sup>  

    -   Los puntos de distribución de este sistema operativo no son compatibles para el entorno PXE con los Servicios de implementación de Windows predeterminados. A partir de la versión 1806, puede habilitar para el entorno PXE un punto de distribución de este sistema operativo con la opción **Habilitar un respondedor PXE sin Servicios de implementación de Windows**. Para obtener más información, vea [Instalación y configuración de puntos de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   Los puntos de distribución en esta versión del sistema operativo no son compatibles con multidifusión.  



## <a name="bkmk_core1803"></a> Instalación básica de Windows Server, versión 1803
<!--503702--> A partir de Configuration Manager 1802, se admite [Windows Server, versión 1803](https://docs.microsoft.com/windows-server/get-started/get-started-with-1803) como punto de distribución con las limitaciones siguientes:  

  -   Solo se admite la versión de 64 bits.  

  -   Los puntos de distribución de este sistema operativo no admiten el entorno PXE ni multidifusión con los Servicios de implementación de Windows predeterminados. A partir de la versión 1806, puede habilitar para el entorno PXE un punto de distribución de este sistema operativo con la opción **Habilitar un respondedor PXE sin Servicios de implementación de Windows**. Para obtener más información, vea [Instalación y configuración de puntos de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core1709"></a> Instalación básica de Windows Server, versión 1709

A partir de Configuration Manager 1710, se admite [Windows Server, versión 1709](https://docs.microsoft.com/windows-server/get-started/get-started-with-1709) como punto de distribución con las limitaciones siguientes:  

  -   Solo se admite la versión de 64 bits.  

  -   Los puntos de distribución de este sistema operativo no admiten el entorno PXE ni multidifusión con los Servicios de implementación de Windows predeterminados. A partir de la versión 1806, puede habilitar para el entorno PXE un punto de distribución de este sistema operativo con la opción **Habilitar un respondedor PXE sin Servicios de implementación de Windows**. Para obtener más información, vea [Instalación y configuración de puntos de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core2016"></a> Instalación básica de Windows Server 2016

Con el paquete acumulativo de actualizaciones 1 para Configuration Manager versión 1606 ([KB3186654](https://support.microsoft.com/help/3186654)), se admite esta versión de sistema operativo para usarla como un punto de distribución con estas limitaciones:  

  -   Solo se admite la versión de 64 bits.  

  -   Los puntos de distribución de este sistema operativo no admiten el entorno PXE ni multidifusión con los Servicios de implementación de Windows predeterminados. A partir de la versión 1806, puede habilitar para el entorno PXE un punto de distribución de este sistema operativo con la opción **Habilitar un respondedor PXE sin Servicios de implementación de Windows**. Para obtener más información, vea [Instalación y configuración de puntos de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core2012r2"></a> Instalación básica de Windows Server 2012 R2  

La instalación de Server Core de Windows Server 2012 R2 se puede usar como punto de distribución con las limitaciones siguientes:  

-   Solo se admite la versión de 64 bits.

-   Los puntos de distribución de este sistema operativo no admiten el entorno PXE ni multidifusión con los Servicios de implementación de Windows predeterminados. A partir de la versión 1806, puede habilitar para el entorno PXE un punto de distribución de este sistema operativo con la opción **Habilitar un respondedor PXE sin Servicios de implementación de Windows**. Para obtener más información, vea [Instalación y configuración de puntos de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core2012"></a> Instalación básica de Windows Server 2012  

La instalación de Server Core de Windows Server 2012 se puede usar como punto de distribución con las limitaciones siguientes:  

-   Solo se admite la versión de 64 bits.  

-   Los puntos de distribución de este sistema operativo no admiten el entorno PXE ni multidifusión con los Servicios de implementación de Windows predeterminados. A partir de la versión 1806, puede habilitar para el entorno PXE un punto de distribución de este sistema operativo con la opción **Habilitar un respondedor PXE sin Servicios de implementación de Windows**. Para obtener más información, vea [Instalación y configuración de puntos de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).



## <a name="general-notes"></a>Notas generales

#### <a name="bkmk_note1"></a> Nota 1: puntos de distribución
Los puntos de distribución admiten varias configuraciones diferentes y cada uno tiene requisitos diferentes. En algunos casos, estas configuraciones admiten la instalación no solo en los servidores sino también en sistemas operativos de clientes. Para obtener más información, consulte [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure) (Administración del contenido y de la infraestructura de contenido).  

#### <a name="bkmk_note2"></a> Nota 2: servidores de base de datos del sitio
Los servidores de base de datos de sitio no se admiten en un controlador de dominio de solo lectura (RODC). Para más información, vea el artículo [Puede encontrar problemas al instalar a SQL Server en un controlador de dominio](https://support.microsoft.com/help/2032911) del Soporte técnico de Microsoft. 

Además, los servidores de sitio secundario no se admiten en ningún controlador de dominio.  
