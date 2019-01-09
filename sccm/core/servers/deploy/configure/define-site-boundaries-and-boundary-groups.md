---
title: Uso de límites y grupos de límites
titleSuffix: Configuration Manager
description: Utilice los límites y grupos de límites para definir ubicaciones de red y sistemas de sitio accesibles para dispositivos administrados.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 85d7dbb494f1d6288ad7a45fad98e24a6ad2b393
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421151"
---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>Definir los límites del sitio y los grupos de límites para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los límites de System Center Configuration Manager definen ubicaciones de red de la intranet que pueden contener los dispositivos que quiere administrar. Los grupos de límites son grupos lógicos de límites que puede configurar.

 Una jerarquía puede contener cualquier número de grupos de límites, y cada uno de los grupos de límites puede contener cualquier combinación de los siguientes tipos de límites:  

-   Subred de IP,  
-   Nombre de sitio de Active Directory  
-   Prefijo IPv6  
-   Intervalo de direcciones IP  

Los clientes de la intranet evalúan su ubicación de red actual y después usan esa información para identificar los grupos de límites a los que pertenecen.  

 Los clientes usan grupos de límites para lo siguiente:  
-   **Encontrar un sitio asignado:** los grupos de límites permiten a los clientes buscar un sitio primario para la asignación del cliente (asignación automática de sitios).  
-   **Encontrar determinados roles de sistema de sitio que puedan usar:** al asociar un grupo de límites con determinados roles de sistema de sitio, el grupo de límites proporciona esa lista de sistemas de sitio a los clientes para que la usen durante la ubicación de contenido y como puntos de administración preferidos.  

Los clientes que están en Internet o están configurados como clientes de Internet únicamente no usan la información de límites. Estos clientes no pueden usar la asignación automática de sitio y siempre pueden descargar contenido de cualquier punto de distribución desde su sitio asignado, si el punto de distribución se configura para permitir conexiones de cliente desde Internet.  

**Para comenzar:**
- En primer lugar, [defina ubicaciones de red como límites](/sccm/core/servers/deploy/configure/boundaries).
- Después, [configure grupos de límites](/sccm/core/servers/deploy/configure/boundary-groups) para asociar los clientes de esos límites a los servidores de sistema de sitio que pueden usar.



##  <a name="BKMK_BoundaryBestPractices"></a> Procedimientos recomendados para límites y grupos de límites  

- **Use una combinación del mínimo de límites que satisfagan sus necesidades:**  
  Antes, se recomendaba usar ciertos tipos de límites en lugar de otros. Con los cambios introducidos para mejorar el rendimiento, ahora se recomienda usar cualquier tipo de límites que funcionen para el entorno y que permitan usar el menor número posible de límites para simplificar las tareas de administración.      

- **Evite la superposición de límites en la asignación automática de sitio:**  
   Aunque los grupos de límites admiten tanto configuraciones de asignación de sitio como configuraciones de ubicación de contenido, se recomienda crear un conjunto de grupos de límites independiente que se vaya a usar solo para la asignación de sitio. Es decir, asegúrese de que cada uno de los límites de un grupo de límites, no forme parte de otro grupo de límites con una asignación de sitio diferente. El motivo es el siguiente:  

  - Un único límite puede incluirse en varios grupos de límites  

  - Los grupos de límites pueden asociarse con un sitio principal diferente para la asignación de sitio  

  - Un cliente en un límite que es miembro de dos grupos de límites diferentes con asignaciones de sitio diferentes, seleccionará un sitio al que unirse al azar, que puede no ser el sitio que determinó para el cliente.  Esta configuración se denomina superposición de límites.  

    La superposición de límites no es un problema para la ubicación de contenido, sino que a menudo es una configuración deseada que proporciona recursos o ubicaciones de contenido adicionales a los clientes.  
