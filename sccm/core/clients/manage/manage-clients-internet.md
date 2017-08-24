---
title: Administrar clientes en Internet en Configuration Manager | Microsoft Docs
description: "Obtenga información sobre cómo administrar clientes con la puerta de enlace de administración en la nube y la administración de clientes basada en Internet en Configuration Manager."
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 1b6752be448e1062c97a3225db4fa8af9f4832a6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Administrar clientes en Internet con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En Configuration Manager, la mayoría de los equipos y servidores que están administrándose se encuentran normalmente de manera física en la misma red corporativa o privada interna que los servidores de sistema de sitio que realizan funciones de administración. En cambio, puede administrar equipos cliente fuera de su red corporativa si están conectados a Internet sin necesitar que los clientes se conecten mediante redes privadas virtuales para llegar a los servidores del sistema de sitio.

Configuration Manager proporciona dos maneras de administrar los clientes conectados a Internet:

-   Puerta de enlace de administración en la nube

-   Administración de cliente basada en Internet

## <a name="cloud-management-gateway"></a>Puerta de enlace de administración en la nube

A partir de la versión 1610, Configuration Manager presenta la puerta de enlace de administración en la nube. En este nuevo método se proporciona una manera de administrar los clientes basados en Internet con una combinación de un servicio en la nube que se ha implementado en Microsoft Azure y un nuevo rol de sistema de sitio que se comunica con ese servicio. Por lo tanto, los clientes usan el servicio para comunicarse con Configuration Manager.

Ventajas:

-   No se necesita ninguna inversión adicional en infraestructura.

-   No expone la infraestructura local en Internet.

-   Las máquinas virtuales en la nube que ejecutan el servicio se administran completamente con Azure y no necesitan mantenimiento.

-   Se instala y configura fácilmente en la consola de Configuration Manager.

Desventajas:

-   Costo de la suscripción en la nube.

-   Los datos de administración se envían a través del servicio en la nube.

Para obtener más información, consulte [Plan for cloud management gateway (Plan para la puerta de enlace de administración en la nube)](plan-cloud-management-gateway.md).

## <a name="internet-based-client-management"></a>Administración de cliente basada en Internet

Este método se basa en los servidores del sistema de sitio con conexión a Internet con los que se comunican los clientes con fines de administración. Este método necesita que los clientes y los servidores del sistema de sitio se configuren para la administración basada en Internet.

Ventajas:

-   No hay dependencia de servicio en la nube.

-   No hay ningún costo adicional asociado con una suscripción a la nube.

-   Control completo de los servidores y los roles que proporcionan el servicio.

Desventajas:

-   Se necesita una inversión adicional en infraestructura.

-   Costos generales y operativos de la infraestructura adicional.

-   La infraestructura debe exponerse en Internet.

Para obtener más información, consulte [Plan for Internet-based client management (Plan para la administración de cliente basada en Internet)](plan-internet-based-client-management.md).
