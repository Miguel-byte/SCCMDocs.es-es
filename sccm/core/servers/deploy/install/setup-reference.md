---
title: "Referencia del programa de instalación | System Center Configuration Manager"
description: "Consulte esta referencia para prepararse para instalar un sitio o jerarquía de Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 06bab7e01fee2c0b030a2879fa67fd455bf668fe


---
# <a name="reference-for-system-center-configuration-manager-setup"></a>Referencia de la instalación de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

El programa de instalación de System Center Configuration Manager proporciona vínculos a varios temas que se detallan en las secciones siguientes. La información de las siguientes secciones puede ayudarle a preparar la instalación de un sitio o una jerarquía de Configuration Manager, así como a tomar algunas de las decisiones que serán necesarias durante la instalación:  

-   [Antes de comenzar](#bkmk_start)  

-   [Evaluar la preparación del servidor](#bkmk_assess)  

-   [Clientes para sistemas operativos adicionales](#bkmk_Addclients)  

-   [Diagnósticos y datos de uso para System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)  

##  <a name="a-namebkmkstarta-before-you-begin"></a><a name="bkmk_start"></a> Antes de comenzar  
 Antes de instalar nuevos sitios de Configuration Manager, asegúrese de revisar la siguiente información que puede ayudarle a preparar el terreno para lograr un diseño de implementación correcto:  

-   [Aspectos básicos de System Center Configuration Manager](../../../../core/understand/fundamentals.md)  

-   [Planear la infraestructura de System Center Configuration Manager](../../../plan-design/network/configure-firewalls-ports-domains.md)  

-   [Preparar la instalación de sitios de System Center Configuration Manager](prepare-to-install-sites.md)  

##  <a name="a-namebkmkassessa-assess-server-readiness"></a><a name="bkmk_assess"></a> Evaluar la preparación del servidor  
 Antes de comenzar con la instalación de un nuevo sitio, asegúrese de que el servidor de sitio y los servidores remotos de sistema de sitio que planea usar para el sitio (por ejemplo, el servidor que hospede la base de datos del sitio) cumplen todos los requisitos previos de configuración. Los siguientes temas de la biblioteca de documentación pueden resultar de utilidad:  

-   [Configuraciones admitidas para System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  

-   [Comprobador de requisitos previos](https://technet.microsoft.com/library/mt590813.aspx#bkmk_PreqChk)  

##  <a name="a-namebkmkaddclientsa-clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a> Clientes para sistemas operativos adicionales  
 Puede descargar el software cliente de Configuration Manager desde el Centro de descarga de Microsoft para los sistemas operativos siguientes:  

-   Mac (Apple)  

-   UNIX  

-   Linux  

**Use los vínculos siguientes para descargar los clientes de la versión de Configuration Manager que usa:**  

-   [System Center Configuration Manager (rama actual)](http://www.microsoft.com/download/details.aspx?id=47719)  

-   [System Center 2012 R2 Configuration Manager SP1 y System Center 2012 SP2 Configuration Manager SP2](http://go.microsoft.com/fwlink/?LinkID=626550)  

-   [System Center 2012 R2 Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=316448)  

-   [System Center 2012 Configuration Manager SP1](http://www.microsoft.com/en-pk/download/details.aspx?id=36212)  

##  <a name="a-namebkmkusagea-usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> Configuración y niveles de datos de uso  
Cuando se instala el primer sitio de System Center Configuration Manager, se instala y configura de forma automática un nuevo rol de sistema de sitio en el servidor de sitio, el **punto de conexión de servicio** con la configuración predeterminada siguiente:  

-   Modo**en línea** (también se admite un modo sin conexión).  

-   Un nivel de recopilación de datos del tipo **Mejorado** (se admiten otros dos niveles de recopilación de datos, Básico y Completo).  

Cuando esta rol está en línea, permite que Microsoft recopile automáticamente información de uso y diagnóstico a través de Internet. La información recopilada nos ayuda a realizar las siguientes tareas:  

-   Identificar y solucionar problemas  

-   Mejorar nuestros productos y servicios  

-   Identificar las actualizaciones de Configuration Manager que se aplican a la versión de Configuration Manager actualmente en uso  

Los tres niveles de recopilación de datos incluyen:  

-   **Básico** incluye datos sobre la instalación y la actualización, como el número de sitios y qué características de Configuration Manager están habilitadas. No se enviará ninguna información personal que pueda identificarle.  

-   **Mejorado** incluye los datos de la opción de configuración Básico y, además, transmite datos sobre la jerarquía, cómo se usa cada característica (frecuencia y duración) e información de diagnóstico mejorada, como el estado de la memoria del servidor cuando se produce un bloqueo del sistema o de una aplicación. No se enviará información de identificación personal.  

-   **Completo** incluye los datos de las opciones de configuración Básico y Mejorado y, además, envía información de diagnóstico avanzada, como archivos de sistema e instantáneas de la memoria. Esta opción puede incluir información de identificación personal, pero no la usaremos para identificarle o ponernos en contacto con usted ni para enviarle anuncios dirigidos.  

Para obtener más información, incluida la divulgación de los detalles que se recopilan en cada nivel, consulte [Diagnósticos y datos de uso para System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

[Declaración de privacidad de System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626527)



<!--HONumber=Nov16_HO1-->


