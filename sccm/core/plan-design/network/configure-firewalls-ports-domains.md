---
title: Infraestructura de red
titleSuffix: Configuration Manager
description: Configure firewalls, puertos y dominios para preparar las comunicaciones de Configuration Manager.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 60a24e06d650b0e25007fb8490eb0c7d8c1996a1
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285615"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Consideraciones sobre la infraestructura de red para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Para preparar la red a fin de admitir Configuration Manager, es posible que tenga que configurar algunos componentes de infraestructura. Por ejemplo, abra los puertos del firewall para pasar las comunicaciones que usa Configuration Manager.  

## <a name="ports-and-protocols"></a>Puertos y protocolos

Las distintas características de Configuration Manager usan distintos puertos de red. Algunos puertos son obligatorios y otros los puede personalizar.

La mayoría de las comunicaciones de Configuration Manager usan puertos comunes, como el puerto 80 para HTTP o el puerto 443 para HTTPS. Algunos roles de sistema de sitio permiten usar sitios web y puertos personalizados. Para más información, consulte [Sitios web para servidores de sistema de sitio](/sccm/core/plan-design/network/websites-for-site-system-servers).

Antes de implementar Configuration Manager, identifique los puertos que planea usar y configure los firewalls según sea necesario.

Después de instalar Configuration Manager, si necesita cambiar un puerto, no olvide actualizar los firewalls de los dispositivos y la red. Además, cambie la configuración del puerto en Configuration Manager.

Vea los siguientes artículos para más información:

- [Configurar puertos de comunicación de cliente](/sccm/core/clients/deploy/configure-client-communication-ports)
- [Puertos usados en Configuration Manager](/sccm/core/plan-design/hierarchy/ports)


## <a name="internet-access-requirements"></a>Requisitos de acceso a Internet

Algunas características de Configuration Manager se basan en la conectividad de Internet para obtener la funcionalidad completa. Si la organización restringe la comunicación de red con Internet mediante un dispositivo proxy o firewall, asegúrese de permitir los puntos de conexión necesarios.

Para más información, consulte los [requisitos de acceso a Internet](/sccm/core/plan-design/network/internet-endpoints).


## <a name="proxy-servers"></a>Servidores proxy

Puede especificar distintos servidores proxy para los diferentes clientes y servidores de sistema de sitio. Puede realizar estas configuraciones cuando instala un cliente o un rol de sistema de sitio, o bien cambiarlas más adelante en caso de ser necesario.

Para obtener más información, vea [Compatibilidad de servidor proxy](/sccm/core/plan-design/network/proxy-server-support).
