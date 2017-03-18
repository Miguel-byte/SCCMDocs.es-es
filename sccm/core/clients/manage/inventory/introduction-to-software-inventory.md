---
title: Inventario de software | Microsoft Docs
description: "Obtenga una introducción al inventario de software en System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
caps.latest.revision: 5
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: 969f2d28649853ddc95860fe72597d6d2c9a94e9
ms.lasthandoff: 03/04/2017


---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Introducción al inventario de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use el inventario de software para recopilar información sobre archivos en dispositivos cliente. El inventario de software también puede recopilar archivos de dispositivos cliente y almacenarlos en el servidor de sitio. El inventario de software se recopila cuando selecciona la opción **Habilitar inventario de software en clientes** en la configuración de cliente, donde también puede programar la operación.  

Después de habilitar el inventario de software y de que los clientes ejecuten un ciclo de inventario de software, el cliente envía la información a un punto de administración en el sitio del cliente. Después, el punto de administración reenvía la información de inventario al servidor de sitio de Configuration Manager, que almacena la información en la base de datos del sitio.   

 Aquí se muestran algunas maneras de ver los datos de inventario de software:  

-   [Crear consultas](../../../../core/servers/manage/queries-technical-reference.md) que devuelven dispositivos con archivos especificados.   

-   Crear [recopilaciones basadas en consultas](../../../../core/clients/manage/collections/introduction-to-collections.md) que incluyen dispositivos con archivos especificados.   

-   [Ejecutar informes](../../../../core/servers/manage/reporting.md) que proporcionan detalles sobre archivos en dispositivos.

-   Usar el [Explorador de recursos](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) para examinar la información detallada sobre los archivos inventariados y recopilados de los dispositivos cliente.   

 Cuando se ejecuta el inventario de software en un dispositivo cliente, el primer informe es un inventario completo. Los informes posteriores contienen solo información de inventario diferencial. El servidor de sitio procesa la información diferencial en el orden recibido. Si falta información diferencial para un cliente, el servidor de sitio rechaza la información diferencial adicional e indica al cliente que ejecute un inventario completo.  

 Configuration Manager puede detectar equipos de arranque dual, pero solo devuelve información de inventario del sistema operativo que estaba activo en el momento del inventario.  

**Dispositivos móviles:** vea el [inventario de software para dispositivos móviles inscritos con Microsoft Intune](../../../../mdm/deploy-use/software-inventory-mobile-devices.md) para obtener información sobre la recopilación de inventario de aplicaciones instaladas en dispositivos móviles.

