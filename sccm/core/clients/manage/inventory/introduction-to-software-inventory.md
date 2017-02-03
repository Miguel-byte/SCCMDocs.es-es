---
title: Inventario de software | Microsoft Docs
description: "Obtenga una introducción al inventario de software en System Center Configuration Manager."
ms.custom: na
ms.date: 12/26/2016
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
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 9206b82eca02877c30eebf146d42bcca7290eb42
ms.openlocfilehash: c9956dd4ef94a1b109d761e44e42f512c42eb8d2


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

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventario de software para dispositivos móviles inscritos con Microsoft Intune  
 Puede recopilar inventario para aplicaciones instaladas en dispositivos móviles. Las aplicaciones que se incluyen en el inventario dependerán de si el dispositivo es propiedad de la empresa o personal. Para dispositivos personales, las únicas aplicaciones inventariadas son las administradas por Microsoft Intune.  

> [!NOTE]  
>  El inventario de las aplicaciones instaladas en dispositivos móviles se recopila como parte del proceso de [inventario de hardware](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md).  

 Aquí se enumeran las aplicaciones que están inventariadas para dispositivos de propiedad personal o de empresa.  

|Plataforma|Para dispositivos personales|Para dispositivos de la compañía|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (sin el cliente de Configuration Manager)|Solo aplicaciones administradas|Solo aplicaciones administradas| 
|Windows 8.1 (sin el cliente de Configuration Manager)|Solo aplicaciones administradas|Solo aplicaciones administradas|  
|Windows Phone 8|Solo aplicaciones administradas|Solo aplicaciones administradas|  
|Windows RT|Solo aplicaciones administradas|Solo aplicaciones administradas|  
|iOS|Solo aplicaciones administradas|Todas las aplicaciones instaladas en el dispositivo|  
|Android|Solo aplicaciones administradas|Todas las aplicaciones instaladas en el dispositivo|  





<!--HONumber=Dec16_HO5-->


