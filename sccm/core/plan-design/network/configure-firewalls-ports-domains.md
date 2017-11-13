---
title: Firewalls y dominios
titleSuffix: Configuration Manager
description: Configure firewalls, puertos y dominios para preparar las comunicaciones de System Center Configuration Manager.
ms.custom: na
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
caps.latest.revision: "15"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 3bcfeb4517797b5c04615f36a166e55a3f2e4058
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="set-up-firewalls-ports-and-domains-for-system-center-configuration-manager"></a>Configurar firewalls, puertos y dominios para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Para preparar la red para que admita System Center Configuration Manager, planee la configuración de la infraestructura (como los firewalls) para pasar las comunicaciones usadas por Configuration Manager.  

|Consideración|Detalles|  
|-------------------|-------------|  
|**Puertos y protocolos** que usan las diferentes funciones de Configuration Manager. Algunos puertos son obligatorios y puede personalizar otros **dominios y servicios**.|La mayoría de las comunicaciones de Configuration Manager usan puertos comunes, como el puerto 80 para HTTP o el puerto 443 para la comunicación HTTPS. En cambio, [algunos roles de sistema de sitio permiten usar sitios web personalizados](/sccm/core/plan-design/network/websites-for-site-system-servers) y puertos personalizados.<br /><br /> **Antes de implementar Configuration Manager**, identifique los puertos que tiene previsto usar y configure los firewalls en consecuencia.<br /><br /> **Si necesita cambiar un puerto** después de instalar Configuration Manager, no se olvide de actualizar los firewalls en los dispositivos y la red, así como cambiar la configuración del puerto desde Configuration Manager.<br /><br /> Para más información, vea: </br>- [Cómo configurar números de puerto de comunicación del cliente](../../../core/clients/deploy/configure-client-communication-ports.md) </br>- [Ports used in Configuration Manager (Puertos usados en Configuration Manager)](../../../core/plan-design/hierarchy/ports.md) </br>- [Internet access requirements for the service connection point (Requisitos de acceso a Internet para el punto de conexión de servicio)](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)|  
|**Dominios y servicios** a los que necesitan acceder los clientes y servidores de sitios.|Puede que las funciones de Configuration Manager necesiten que los clientes y servidores de sitios accedan a servicios y dominios específicos de Internet, como Windowsudpate.microsoft.com o el servicio de Microsoft Intune.<br /><br /> Si va a usar Microsoft Intune para administrar dispositivos móviles, también tendrá que configurar el acceso a los [puertos y dominios necesarios para Intune](https://docs.microsoft.com/en-us/intune/get-started/network-infrastructure-requirements-for-microsoft-intune).|  
|**Servidores proxy** para los servidores de sistema de sitio y las comunicaciones de cliente. Puede especificar distintos servidores proxy para los diferentes clientes y servidores de sistema de sitio.|Como estas configuraciones se realizan cuando se instala un cliente o un rol de sistema de sitio, solo necesitará conocer las configuraciones del servidor proxy más adelante cuando configure los clientes y roles de sistema de sitio.<br /><br /> Si no está seguro de si la implementación necesitará usar servidores proxy, vea [Proxy server support in System Center Configuration Manager (Compatibilidad de servidor proxy en System Center Configuration Manager)](../../../core/plan-design/network/proxy-server-support.md) para obtener información sobre los roles de sistema de sitio y las acciones de cliente que pueden usar un servidor proxy.|   
|  
