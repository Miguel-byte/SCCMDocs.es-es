---
title: Referencia de instalación
titleSuffix: Configuration Manager
description: Consulte esta referencia para prepararse para instalar un sitio o jerarquía de Configuration Manager.
ms.date: 04/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c1b3e1506114cf931fb61d8c2c4c05eb8942ea49
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70888822"
---
# <a name="reference-for-system-center-configuration-manager-setup"></a>Referencia de la instalación de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

El programa de instalación de System Center Configuration Manager ofrece vínculos a varios temas que se indican en las secciones siguientes. La información que encontrará aquí puede ayudarle a preparar la instalación de un sitio o jerarquía de Configuration Manager, así como ayudarle a preparar algunas de las decisiones que necesita tomar durante la instalación.  


##  <a name="bkmk_start"></a> Antes de comenzar  
Antes de instalar nuevos sitios de Configuration Manager, asegúrese de revisar la información siguiente, que puede resultarle útil para preparar correctamente un diseño de implementación:  

-   [Aspectos básicos de System Center Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Planear la infraestructura de System Center Configuration Manager](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Preparar la instalación de sitios de System Center Configuration Manager](prepare-to-install-sites.md)  

##  <a name="bkmk_assess"></a> Evaluar la preparación del servidor  
Antes de empezar la instalación de un nuevo sitio, asegúrese de que el servidor de sitio y los servidores del sistema de sitio remoto que quiera usar para el sitio (por ejemplo, el servidor que hospeda la base de datos del sitio) cumplan todos los requisitos previos de configuración. Estos temas de la biblioteca de documentación pueden resultarle útiles:  

-   [Configuraciones admitidas para System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Comprobador de requisitos previos](prerequisite-checker.md)  

##  <a name="bkmk_Addclients"></a> Clientes para sistemas operativos adicionales  
Puede descargar el software cliente de Configuration Manager desde el Centro de descarga de Microsoft para los siguientes sistemas operativos:  

-   Mac (Apple)  
-   UNIX  
-   Linux  

Use los vínculos siguientes para descargar los clientes de la versión de Configuration Manager que use:  

-   Consulte [Microsoft System Center Configuration Manager: clientes para sistemas operativos adicionales](https://www.microsoft.com/download/details.aspx?id=47719)  

##  <a name="bkmk_usage"></a> Configuración y niveles de datos de uso  
Al instalar el primer sitio de System Center Configuration Manager, Configuration Manager instala y configura automáticamente un nuevo rol de sistema de sitio (el **punto de conexión de servicio**) en el servidor de sitio. El punto de conexión de servicio tiene esta configuración predeterminada:  

-   Modo **con conexión** (también hay disponible un modo sin conexión)  
-   Nivel **mejorado** de recopilación de datos (también hay disponibles otros dos niveles de recopilación de datos, básico y completo)  

Cuando el rol de sistema de sitio del punto de conexión de servicio está con conexión, Microsoft puede recopilar automáticamente información de uso y diagnósticos por Internet. La información recopilada nos ayuda a realizar las siguientes tareas:  

-   Identificar y solucionar problemas  
-   Mejorar nuestros productos y servicios  
-   Identificar las actualizaciones de Configuration Manager que se aplican a la versión de Configuration Manager actualmente en uso  

### <a name="levels-of-data-collection"></a>Niveles de recopilación de datos  
En la recopilación de datos se incluyen estos tres niveles:

-   En el nivel **básico** se incluyen datos sobre la instalación y la actualización, como el número de sitios y las características de Configuration Manager que están habilitadas. No se transmite información de identificación personal.  

-   En el nivel **mejorado** se incluyen los datos de la configuración del nivel básico y, además, se transmiten datos sobre la jerarquía, el uso de cada característica (en frecuencia y duración) e información de diagnóstico mejorada, como el estado de memoria del servidor si se produce un bloqueo del sistema o de una aplicación. No se transmite información de identificación personal.  

-   En el nivel **completo** se incluyen los datos de la configuración de los niveles básico y mejorado y, además, se envía información de diagnóstico avanzada, como archivos del sistema e instantáneas de memoria. Con esta opción podría incluirse información de identificación personal, pero no usaremos esa información para identificarle o ponernos en contacto con usted, ni para enviarle publicidad.  

Para obtener más información, incluida la divulgación de los detalles recopilados por cada nivel, consulte [Diagnósticos y datos de uso para System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

Para ver la declaración de privacidad en línea de System Center Configuration Manager, vaya a [https://go.microsoft.com/fwlink/?LinkID=626527](https://go.microsoft.com/fwlink/?LinkID=626527).
