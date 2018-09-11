---
title: Administrar clientes en Internet
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo administrar clientes con Cloud Management Gateway y la administración de clientes basados en Internet en Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 198b044a66bf81ea846d5e4febe655b78c04dd13
ms.sourcegitcommit: 316899b08f2ef372993909e08e069f7edfed1d33
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2018
ms.locfileid: "44111083"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Administrar clientes en Internet con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Normalmente en Configuration Manager, la mayoría de los equipos y servidores administrados se encuentran físicamente en la misma red interna que los servidores de sistema de sitio que realizan funciones de administración. Pero los clientes se pueden administrar fuera de la red interna si están conectados a Internet. Esta capacidad no requiere que los clientes se conecten a través de VPN para tener acceso a los servidores de sistema de sitio.

Configuration Manager proporciona dos maneras de administrar los clientes conectados a Internet:

-   Puerta de enlace de administración en la nube

-   Administración de cliente basada en Internet


## <a name="cloud-management-gateway"></a>Puerta de enlace de administración en la nube

Cloud Management Gateway (CMG) proporciona administración de clientes basados en Internet. Usa una combinación de un servicio de nube de Microsoft Azure y un nuevo rol de sistema de sitio que se comunica con ese servicio. Los clientes basados en Internet usan el servicio en la nube para comunicarse con la instancia local de Configuration Manager.

#### <a name="advantages"></a>Ventajas  

-   No se necesita ninguna inversión adicional en infraestructura.  

-   No expone la infraestructura local en Internet.  

-   Las máquinas virtuales en la nube que ejecutan el servicio se administran completamente con Azure y no necesitan mantenimiento.  

-   Se instala y configura fácilmente en la consola de Configuration Manager.  

#### <a name="disadvantages"></a>Desventajas  

-   Costo de la suscripción en la nube.  

-   Los datos de administración se envían a través del servicio en la nube.  

Para obtener más información, consulte [Plan for cloud management gateway (Plan para la puerta de enlace de administración en la nube)](plan-cloud-management-gateway.md).  



## <a name="internet-based-client-management"></a>Administración de cliente basada en Internet

Este método se basa en los servidores de sistema de sitio con conexión a Internet con los que se comunican los clientes con fines de administración. Requiere que los clientes y los servidores de sistema de sitio se configuren para la administración basada en Internet.

#### <a name="advantages"></a>Ventajas  

-   No hay dependencia de servicio en la nube.  

-   No hay ningún costo adicional asociado con una suscripción a la nube.  

-   Control completo de los servidores y los roles que proporcionan el servicio.  

#### <a name="disadvantages"></a>Desventajas  

-   Se necesita una inversión adicional en infraestructura.  

-   Costos generales y operativos de la infraestructura adicional.  

-   La infraestructura se debe exponer en Internet.  

Para obtener más información, vea [Plan para la administración de cliente basada en Internet](plan-internet-based-client-management.md).  
