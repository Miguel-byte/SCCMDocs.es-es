---
title: Inventario de software
titleSuffix: Configuration Manager
description: Obtenga una introducción al inventario de software en System Center Configuration Manager.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d0ca25d64f3dd0e86ddbd89e2d86ae13da170891
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67550745"
---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Introducción al inventario de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use el inventario de software para recopilar información sobre archivos en dispositivos cliente. El inventario de software también puede recopilar archivos de dispositivos cliente y almacenarlos en el servidor de sitio. El inventario de software se recopila cuando se selecciona la opción **Habilitar inventario de software en clientes** en la configuración de cliente. También puede programar la operación en la configuración de cliente.  

Después de habilitar el inventario de software y de que los clientes ejecuten un ciclo de inventario de software, el cliente envía la información a un punto de administración en el sitio del cliente. Después, el punto de administración reenvía la información de inventario al servidor de sitio de Configuration Manager, que almacena la información en la base de datos del sitio.

 Hay varias maneras de ver los datos de inventario de software:  

- [Crear consultas](../../../../core/servers/manage/create-queries.md) que devuelven dispositivos con archivos especificados.   

- Crear [recopilaciones basadas en consultas](../../../../core/clients/manage/collections/introduction-to-collections.md) que incluyen dispositivos con archivos especificados.   

- [Ejecutar informes](../../../../core/servers/manage/reporting.md) que proporcionan detalles sobre archivos en dispositivos.

- Usar el [Explorador de recursos](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) para examinar la información detallada sobre los archivos inventariados y recopilados de los dispositivos cliente.   

 Cuando se ejecuta el inventario de software en un dispositivo cliente, el primer informe es un inventario completo. Los informes posteriores contienen solo información de inventario diferencial. El servidor de sitio procesa la información diferencial en el orden recibido. Si falta información diferencial para un cliente, el servidor de sitio rechaza la información diferencial adicional e indica al cliente que ejecute un inventario completo.  

 Configuration Manager puede detectar equipos de arranque dual, pero solo devuelve información de inventario del sistema operativo que esté activo en el momento del inventario.  

**Dispositivos móviles:** consulte [Inventario de software para dispositivos móviles inscritos con Microsoft Intune](../../../../mdm/deploy-use/software-inventory-mobile-devices.md) para obtener información sobre la recopilación de inventario de aplicaciones instaladas en dispositivos móviles.
