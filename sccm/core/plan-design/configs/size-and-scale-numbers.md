---
title: "Tamaño y escala | System Center Configuration Manager"
description: "Identifique el número de roles de sistema de sitio y sitios que necesitará para admitir los dispositivos en su entorno de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: aeeb902fad7444534cafa7f9cb984ce8764471b0

---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>Números de tamaño y escala de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*



Cada implementación de System Center Configuration Manager tendrá un número máximo de sitios, roles de sistema de sitio y dispositivos que podrá admitir. Estos números varían en función de la estructura de jerarquía (qué tipos y el número de sitios que usa) y los roles de sistema de sitio que implementa.  La información de los siguientes temas puede ayudarle a identificar el número de roles de sistema de sitio y sitios que necesitará para admitir los dispositivos que espera administrar con su entorno.

Utilice la información de este tema con la información de los siguientes artículos:
-   [Hardware recomendado](../../../core/plan-design/configs/recommended-hardware.md)
-   [Sistemas operativos compatibles con servidores de sistema de sitio](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Supported operating systems for clients and devices](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) (Sistemas operativos compatibles con clientes y dispositivos)
-   [Requisitos previos de sitio y sistema de sitio](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)

Los números de compatibilidad de este artículo se basan en el uso del hardware recomendado de Configuration Manager. Si no se usa el hardware recomendado, el rendimiento de los sistemas de sitio puede disminuir y podría no satisfacer los niveles de compatibilidad afirmados.

##  <a name="a-namebkmksitesystemscalea-site-types"></a><a name="bkmk_SiteSystemScale"></a> Tipos de sitio  
 **Sitio de administración central:**  

-   Un sitio de administración central admite hasta 25 sitios primarios o secundarios.  

**Sitio primario:**  

-   Cada sitio primario admite hasta 250 sitios secundarios.  

-   El número de sitios secundarios por cada sitio primario se basa en conexiones de red de área extensa (WAN) confiables y continuamente conectadas. Para las ubicaciones que tienen menos de 500 clientes, considere la posibilidad de un punto de distribución en lugar de un sitio secundario.  

 Para obtener información sobre los números de clientes y dispositivos que un sitio primario puede admitir, consulte [Número de clientes para sitios y jerarquías](#bkmk_clientnumbers) en este tema.  

**Sitio secundario:**  

-   Los sitios secundarios no admiten otros sitios secundarios.  

-   Un sitio de administración central admite hasta 25 sitios primarios o secundarios.  

**Punto de sitios web del catálogo de aplicaciones:**  

-   Puede instalar varias instancias del punto de sitios web del catálogo de aplicaciones en los sitios primarios.  

    > [!TIP]  
    >  Como procedimiento recomendado, instale el punto de sitios web del catálogo de aplicaciones y el punto de servicio web del catálogo de aplicaciones juntos en el mismo sistema de sitio cuando brinden servicio a clientes que están en la intranet.  

    -   Para mejorar el rendimiento, planee admitir hasta 50.000 clientes por instancia.  

    -   Cada instancia de este rol de sistema de sitio admite el número máximo de clientes compatibles con la jerarquía.  

## <a name="a-namebkmkrolesa-site-system-roles"></a><a name="bkmk_roles"></a> Roles de sistema de sitio    

**Punto de servicio web del catálogo de aplicaciones:**  

-   Puede instalar varias instancias del punto de servicio web del catálogo de aplicaciones en los sitios primarios.  

    > [!TIP]  
    >  Como procedimiento recomendado, instale el punto de sitios web del catálogo de aplicaciones y el punto de servicio web del catálogo de aplicaciones juntos en el mismo sistema de sitio cuando brinden servicio a clientes que están en la intranet.  

    -   Para mejorar el rendimiento, planee admitir hasta 50.000 clientes por instancia.  

    -   Cada instancia de este rol de sistema de sitio admite el número máximo de clientes compatibles con la jerarquía.  

**Punto de distribución:**  

-   Puntos de distribución por sitio:  

    -   Cada sitio primario y secundario admite hasta 250 puntos de distribución.  

    -   Cada sitio primario y secundario admite hasta 2.000 puntos de distribución adicionales configurados como puntos de distribución de extracción. **Por ejemplo**, un único sitio primario admite 2250 puntos de distribución cuando 2000 de esos puntos de distribución se configuran como puntos de distribución de extracción.  

    -   Cada punto de distribución admite conexiones de hasta 4.000 clientes.  

    -   Un punto de distribución de extracción actúa como un cliente cuando tiene acceso a contenido desde un punto de distribución de origen.  

-   Cada sitio primario admite un total combinado de hasta 5.000 puntos de distribución. Este total incluye todos los puntos de distribución en el sitio primario y todos los puntos de distribución que pertenecen a los sitios secundarios del sitio primario.  

-   Cada punto de distribución es compatible con un total combinado de hasta 10.000 paquetes y aplicaciones.  

> [!WARNING]  
>  El número real de clientes que puede admitir un punto de distribución depende de la velocidad de la red y la configuración de hardware del equipo de punto de distribución.  
>   
>  De forma similar, el número de puntos de distribución de extracción que puede admitir un punto de distribución de origen depende de la velocidad de la red y la configuración de hardware del equipo de punto de distribución de origen, pero también se ve afectado por la cantidad de contenido que se ha implementado. Esto es porque, a diferencia de los clientes que suelen tener acceso a contenido en distintos momentos durante el transcurso de una ventana de implementaciones, todos los puntos de distribución de extracción solicitan a a la vez el contenido, y pueden solicitar todo el contenido que haya disponible, en lugar del contenido que solo se aplica a ellos, como haría un cliente. Cuando se coloca demasiada carga de procesamiento en un punto de distribución de origen, se pueden producir retrasos inesperados al distribuir el contenido a los puntos de distribución previstos en el entorno.  


**Punto de estado de reserva:**  

-   Cada punto de estado de reserva puede admitir hasta 100.000 clientes.  

**Punto de administración:**  

-   Cada sitio primario admite hasta 15 puntos de administración.  

    > [!TIP]  
    >  No instale puntos de administración en servidores que atraviesen un vínculo lento desde el servidor de sitio primario o el servidor de base de datos del sitio.  

-   Cada sitio secundario admite un solo punto de administración que se debe instalar en el servidor de sitio secundario.  

 Para obtener información sobre los números de clientes y dispositivos que un punto de administración puede admitir, consulte la sección [Puntos de administración](#bkmk_mp) de este tema.  

**Punto de actualización de software:**  

-   Un punto de actualización de software que está instalado en el servidor de sitio puede admitir hasta 25.000 clientes.  

-   Un punto de actualización de software remoto del servidor de sitio puede admitir hasta 150 000 clientes cuando el equipo remoto cumple los requisitos de WSUS para admitir este número.  

-   De manera predeterminada, Configuration Manager no admite la configuración de puntos de actualización de software como clústeres de NLB. En cambio, puede usar el SDK de Configuration Manager para configurar hasta cuatro puntos de actualización de software en un clúster de NLB.  

##  <a name="a-namebkmkclientnumbersa-client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a> Número de clientes para sitios y jerarquías  
 Utilice la siguiente información para determinar cuántos clientes, y de que tipo, se pueden admitir en un sitio o en una jerarquía.  

###  <a name="a-namebkmkcasa-hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a> Jerarquía con un sitio de administración central  
Un sitio de administración central admite un número total de dispositivos que incluye el número máximo de dispositivos indicados para los tres grupos siguientes:  

-   700 000 equipos de escritorio (equipos que ejecutan Windows, Linux y UNIX)  

-   25 000 dispositivos que ejecutan Mac y Windows CE 7.0  

-   Uno de los siguientes, según el modo en que su implementación admita la administración de dispositivos móviles:  

    -   100 000 dispositivos que se administran con MDM local  

    -   300 000 dispositivos basados en la nube  

 Por ejemplo, en una jerarquía, de un total de 1.025.000 dispositivos, puede admitir 700.000 equipos de escritorio, hasta 25.000 clientes Mac y Windows CE 7.0 y hasta 300.000 dispositivos basados en la nube al integrar Microsoft Intune.  Si se admiten los dispositivos administrados por MDM local, el total de la jerarquía es de 825 000 dispositivos.  

> [!IMPORTANT]  
>  En una jerarquía donde el sitio de administración central usa SQL Server Standard Edition, la jerarquía admite un máximo de 50 000 equipos de escritorio y dispositivos. La edición de SQL Server en uso en un sitio primario independiente no limita la capacidad de los sitios a admitir el número de clientes afirmado.  


###  <a name="a-namebkmkchipria-child-primary-site"></a><a name="bkmk_chipri"></a> Sitio primario secundario  
Cada sitio primario secundario de una jerarquía con un sitio de administración central admite lo siguiente:  

-   150 000 clientes y dispositivos en total, sin limitarse a un grupo o tipo específico, siempre y cuando no se supere el número admitido para la jerarquía  

Por ejemplo, un sitio primario que admite 25.000 equipos que ejecutan Mac y Windows CE 7.0 (ya que es el límite en el caso de una jerarquía) puede admitir 125.000 equipos de escritorio adicionales, lo que aumenta el número total de dispositivos compatibles hasta el límite máximo de 150.000 admitido por los sitios primarios secundarios.

###  <a name="a-namebkmkpria-stand-alone-primary-site"></a><a name="bkmk_pri"></a> Sitio primario independiente  
Un sitio primario independiente admite el siguiente número de dispositivos:  

-   175 000 clientes y dispositivos en total, en esta proporción:  

    -   150 000 equipos de escritorio (equipos que ejecutan Windows, Linux y UNIX)  

    -   25 000 dispositivos que ejecutan Mac y Windows CE 7.0  

    -   Uno de los siguientes, según el modo en que su implementación admita la administración de dispositivos móviles:  

        -   50 000 dispositivos administrados con MDM local  

        -   150 000 dispositivos basados en la nube  

Por ejemplo, un sitio primario independiente que admite 150 000 equipos de escritorio y 10 000 clientes Mac o Windows CE 7.0 puede solo tiene cabida para 15 000 dispositivos adicionales. Esos dispositivos pueden estar en la nube o administrase mediante MDM local.  

###  <a name="a-namebkmkseca-secondary-sites"></a><a name="bkmk_sec"></a> Sitios secundarios  
Los sitios secundarios admiten lo siguiente:  

-   15 000 equipos de escritorio (equipos que ejecutan Windows, Linux y UNIX)  

###  <a name="a-namebkmkmpa-management-points"></a><a name="bkmk_mp"></a> Puntos de administración  
Cada punto de administración puede admitir el siguiente número de dispositivos:  

-   25 000 clientes y dispositivos en total, en esta proporción:  

    -   25 000 equipos de escritorio (equipos que ejecutan Windows, Linux y UNIX)  

    -   Uno de los siguientes (no ambos):  

        -   10 000 dispositivos administrados mediante MDM local  

        -   10 000 dispositivos que ejecutan Mac y Windows CE 7.0  



<!--HONumber=Nov16_HO1-->


