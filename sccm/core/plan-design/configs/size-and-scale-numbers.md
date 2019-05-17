---
title: Tamaño y escala
titleSuffix: Configuration Manager
description: Determine el número de roles de sistema de sitio y los sitios que necesitará para admitir los dispositivos en el entorno.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6545b6ce29085041f15a330f02165407a4feafb2
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499523"
---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>Números de tamaño y escala de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*



Cada implementación de Configuration Manager tiene un número máximo de sitios, roles de sistema de sitio y dispositivos que puede admitir. Estos números varían en función de la estructura de la jerarquía, los tipos y números de sitios que se usen y los roles de sistema de sitio que se implementen. La información de este artículo puede ayudar a identificar el número de roles de sistema de sitio y los sitios que se necesitan para admitir los dispositivos que se esperan administrar.

Use la información de este tema junto con la información de los siguientes artículos:
-   [Hardware recomendado](../../../core/plan-design/configs/recommended-hardware.md)
-   [Sistemas operativos compatibles con servidores de sistema de sitio](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Supported operating systems for clients and devices](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) (Sistemas operativos compatibles con clientes y dispositivos)
-   [Requisitos previos de sitio y sistema de sitio](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)


Estos números de compatibilidad se basan en el uso del hardware recomendado para Configuration Manager. También se basan en la configuración predeterminada para todas las características disponibles de Configuration Manager. Si no usa el hardware recomendado o usa una configuración personalizada más agresiva, el rendimiento de los sistemas de sitio puede verse afectado. Es posible que los sistemas de sitio no cumplan los niveles de compatibilidad indicados. (Un ejemplo de configuración de cliente más agresiva es la ejecución de inventario de hardware o software con más frecuencia que los valores predeterminados de una vez cada siete días).

##  <a name="bkmk_SiteSystemScale"></a> Tipos de sitio  

### <a name="central-administration-site"></a>Sitio de administración central  

-   Un sitio de administración central admite hasta 25 sitios primarios o secundarios.  


### <a name="primary-site"></a>Sitio primario  

- Cada sitio primario admite hasta 250 sitios secundarios.  

- El número de sitios secundarios por cada sitio primario se basa en conexiones de red de área extensa (WAN) confiables y continuamente conectadas. Para las ubicaciones que tienen menos de 500 clientes, considere la posibilidad de un punto de distribución en lugar de un sitio secundario.  

  Para obtener más información sobre el número de clientes y dispositivos que un sitio primario puede admitir, vea [Número de clientes para sitios y jerarquías](#bkmk_clientnumbers).  


### <a name="secondary-site"></a>Sitio secundario  

-   Los sitios secundarios no admiten otros sitios secundarios.  



## <a name="bkmk_roles"></a> Roles de sistema de sitio    


### <a name="application-catalog-web-service-point"></a>Punto de servicio web del catálogo de aplicaciones  

-   Puede instalar varias instancias del punto de servicio web del catálogo de aplicaciones en los sitios primarios.  

    > [!TIP]  
    >  Como procedimiento recomendado, instale el punto de sitios web del catálogo de aplicaciones y el punto de servicio web del catálogo de aplicaciones juntos en el mismo sistema de sitio cuando brinden servicio a clientes que están en la intranet.  

    -   Para mejorar el rendimiento, planee admitir hasta 50.000 clientes por instancia.  

    -   Cada instancia de este rol de sistema de sitio admite el número máximo de clientes que son compatibles con la jerarquía.  


### <a name="application-catalog-website-point"></a>Punto de sitios web del catálogo de aplicaciones  

-   Puede instalar varias instancias del punto de sitios web del catálogo de aplicaciones en los sitios primarios.  

    > [!TIP]  
    >  Como procedimiento recomendado, instale el punto de sitios web del catálogo de aplicaciones y el punto de servicio web del catálogo de aplicaciones juntos en el mismo sistema de sitio cuando brinden servicio a clientes que están en la intranet.  

    -   Para mejorar el rendimiento, planee admitir hasta 50.000 clientes por instancia.  

    -   Cada instancia de este rol de sistema de sitio admite el número máximo de clientes que son compatibles con la jerarquía.  


### <a name="bkmk_cmg"></a> Cloud Management Gateway

- Se pueden instalar varias instancias de Cloud Management Gateway (CMG) en los sitios primarios o el sitio de administración central.  

    > [!Tip]  
    > En una jerarquía, cree la instancia de CMG en el sitio de administración central.  

    - Una instancia de CMG admite hasta 16 instancias de máquina virtual (VM) en el servicio de nube de Azure.  

    - Cada instancia de VM de CMG admite 6000 conexiones de cliente simultáneas. Cuando CMG soporta una carga elevada debido a que el número de clientes es mayor que el admitido, sigue administrando las solicitudes, pero pueden producirse retrasos.  

Para obtener más información, vea [Rendimiento y escalabilidad](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#performance-and-scale) de CMG.


### <a name="cloud-management-gateway-connection-point"></a>Punto de conexión de Cloud Management Gateway

- Se pueden instalar varias instancias del punto de conexión de Cloud Management Gateway en los sitios primarios.  

- Un punto de conexión de CMG puede admitir una instancia de CMG con hasta cuatro instancias de máquina virtual. Si la instancia de CMG tiene más de cuatro instancias de máquina virtual, agregue un segundo punto de conexión de CMG para equilibrar la carga. Una instancia de CMG con 16 instancias de máquina virtual debe estar vinculada a cuatro puntos de conexión de CMG.

Para obtener más información, vea [Rendimiento y escalabilidad](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#performance-and-scale) de CMG.


### <a name="distribution-point"></a>Punto de distribución  

-   Puntos de distribución por sitio:  

    -   Cada sitio primario y secundario admite hasta 250 puntos de distribución.  

    -   Cada sitio primario y secundario admite hasta 2000 puntos de distribución adicionales configurados como puntos de distribución de extracción. **Por ejemplo**, un único sitio primario admite 2250 puntos de distribución cuando 2000 de esos puntos de distribución se configuran como puntos de distribución de extracción.  

    -   Cada punto de distribución admite conexiones de hasta 4.000 clientes.  

    -   Un punto de distribución de extracción actúa como un cliente cuando tiene acceso a contenido desde un punto de distribución de origen.  

-   Cada sitio primario admite un total combinado de hasta 5.000 puntos de distribución. Este total incluye todos los puntos de distribución en el sitio primario y todos los puntos de distribución que pertenecen a los sitios secundarios del sitio primario.  

-   Cada punto de distribución es compatible con un total combinado de hasta 10.000 paquetes y aplicaciones.  

> [!WARNING]  
>  El número real de clientes que puede admitir un punto de distribución depende de la velocidad de la red y la configuración de hardware del servidor.  
>   
>  El número de puntos de extracción que puede admitir un punto de distribución de origen depende también de la velocidad de la red y la configuración de hardware del punto de distribución de origen. Pero este número también se ve afectado por la cantidad de contenido que haya implementado. Este efecto se debe a que, a diferencia de los clientes que suelen tener acceso a contenido en distintos momentos durante una implementación, todos los puntos de distribución de extracción solicitan el contenido al mismo tiempo. Los puntos de distribución de extracción pueden solicitar todo el contenido disponible, no solo el contenido que les corresponde. Cuando se coloca una carga de procesamiento elevada en un punto de distribución de origen, se pueden producir retrasos inesperados al distribuir el contenido a los puntos de distribución de destino.  


### <a name="fallback-status-point"></a>Punto de estado de reserva  

-   Cada punto de estado de reserva puede admitir hasta 100.000 clientes.  


### <a name="management-point"></a>Punto de administración  

- Cada sitio primario admite hasta 15 puntos de administración.  

  > [!TIP]  
  >  No instale puntos de administración en servidores que atraviesen un vínculo lento desde el servidor de sitio primario o el servidor de base de datos del sitio.  

- Cada sitio secundario admite un solo punto de administración que se debe instalar en el servidor de sitio secundario.  

  Para obtener más información sobre el número de clientes y dispositivos que un punto de administración puede admitir, vea la sección [Puntos de administración](#bkmk_mp).  


### <a name="software-update-point"></a>Punto de actualización de software  

-   Un punto de actualización de software que está instalado en el servidor de sitio puede admitir hasta 25.000 clientes.   

-   Un punto de actualización de software remoto del servidor de sitio puede admitir hasta 150 000 clientes cuando el equipo remoto cumple los requisitos de Windows Server Update Services (WSUS) para admitir este número de clientes.  



##  <a name="bkmk_clientnumbers"></a> Número de clientes para sitios y jerarquías  
 Use la siguiente información para determinar cuántos clientes, y de qué tipo, se pueden admitir en un sitio o en una jerarquía.  


###  <a name="bkmk_cas"></a> Jerarquía con un sitio de administración central  
Un sitio de administración central admite un número total de dispositivos que incluye el número máximo de dispositivos indicados para los tres grupos siguientes:  

- 700 000 equipos de escritorio (equipos que ejecutan Windows, Linux y UNIX) Consulte también la compatibilidad con [los dispositivos con Windows Embedded](#embedded).

- 25 000 dispositivos que ejecutan Mac y Windows CE 7.0  

- Uno de los siguientes, según el modo en que su implementación admita la administración de dispositivos móviles (MDM):  

  -   100 000 dispositivos que administra mediante MDM local  

  -   300 000 dispositivos basados en la nube  

  Por ejemplo, puede admitir 700 000 equipos de escritorio, hasta 25 000 dispositivos Mac y Windows CE 7.0, y hasta 300 000 dispositivos basados en la nube al integrar Microsoft Intune. Esta jerarquía admite un total de 1 025 000 dispositivos. Si se admiten los dispositivos administrados por MDM local, el total de la jerarquía es de 825 000 dispositivos.  

> [!IMPORTANT]  
>  En una jerarquía donde el sitio de administración central usa SQL Server Standard Edition, la jerarquía admite un máximo de 50 000 equipos de escritorio y dispositivos. Para admitir más de 50 000 equipos de escritorio y dispositivos, debe usar una edición Enterprise de SQL Server. Este requisito solo se aplica a un sitio de administración central. No se aplica a un sitio primario independiente o un sitio primario secundario. La edición de SQL Server que se usa para un sitio primario no limita su capacidad para admitir el número de clientes indicado.   


 La edición de SQL Server que se usa en un sitio primario independiente no limita la capacidad del sitio para admitir el número de clientes indicado.  


###  <a name="bkmk_chipri"></a> Sitio primario secundario  
Cada sitio primario secundario de una jerarquía con un sitio de administración central admite el número de clientes siguiente:  

-   150 000 clientes y dispositivos en total, sin limitarse a un grupo o tipo específico, siempre y cuando no se supere el número admitido para la jerarquía. Consulte también la compatibilidad con [los dispositivos con Windows Embedded](#embedded).

Por ejemplo, un sitio primario admite 25 000 dispositivos Mac y Windows CE 7.0. Este número es el límite de una jerarquía. Después, este sitio primario puede admitir 125 000 equipos de escritorio adicionales. El número total de dispositivos admitidos por el sitio primario secundario es el límite máximo admitido de 150 000.


###  <a name="bkmk_pri"></a> Sitio primario independiente  
Un sitio primario independiente admite el siguiente número de dispositivos:  

-   175 000 clientes y dispositivos en total, en esta proporción:  

    -   150 000 equipos de escritorio (equipos que ejecutan Windows, Linux y UNIX) Consulte también la compatibilidad con [los dispositivos con Windows Embedded](#embedded).

    -   25 000 dispositivos que ejecutan Mac y Windows CE 7.0

    -   Uno de los siguientes, según el modo en que su implementación admita la administración de dispositivos móviles:  

        -   50 000 dispositivos que administra mediante MDM local  

        -   150 000 dispositivos basados en la nube  


Por ejemplo, un sitio primario independiente que admite 150 000 equipos de escritorio y 10 000 equipos Mac o Windows CE 7.0 solo puede admitir 15 000 dispositivos adicionales. Esos dispositivos pueden estar en la nube o administrase mediante MDM local.  


### <a name="embedded"></a> Sitios principales y dispositivos con Windows Embedded
Los sitios principales admiten dispositivos con Windows Embedded que tienen habilitados los filtros de escritura basados en archivos (FBWF). Cuando los dispositivos insertados no tienen filtros de escritura habilitados, un sitio primario puede admitir una serie de dispositivos insertados, hasta el máximo permitido para ese sitio. Cuando los dispositivos incrustados tienen FBWF o filtros de escritura unificados (UWF) habilitados, un sitio primario puede admitir un máximo de 10 000 dispositivos incrustados de Windows. Estos dispositivos se deben configurar con las excepciones enumeradas en la nota importante que se encuentra en [Planeamiento de la implementación de clientes en dispositivos de Windows Embedded](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices). Un sitio principal admite solo 3000 dispositivos con Windows Embedded que tienen habilitado EWF y que no están configurados para las excepciones.


###  <a name="bkmk_sec"></a> Sitios secundarios  
Los sitios secundarios admiten el número de dispositivos siguiente:  

-   15 000 equipos de escritorio (equipos que ejecutan Windows, Linux y UNIX)  


###  <a name="bkmk_mp"></a> Puntos de administración  
Cada punto de administración puede admitir el siguiente número de dispositivos:  

-   25 000 clientes y dispositivos en total, en esta proporción:  

    -   25 000 equipos de escritorio (equipos que ejecutan Windows, Linux y UNIX)  

    -   Uno de los siguientes (no ambos):  

        -   10 000 dispositivos que administra mediante MDM local  

        -   10 000 dispositivos que ejecutan clientes Mac y Windows CE 7.0
