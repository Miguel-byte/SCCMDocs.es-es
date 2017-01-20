---
title: Inventario de software | System Center Configuration Manager
description: "Obtenga una introducción al inventario de software en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8d664616e222119f7821a70a7c8f9cdbfca38538


---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Introducción al inventario de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use el inventario de software en System Center Configuration Manager para recopilar información sobre los archivos contenidos en dispositivos cliente en su organización. Además, el inventario de software puede recopilar archivos de dispositivos cliente y almacenarlos en el servidor de sitio. El inventario de software se recopila cuando la opción **Habilitar inventario de software en clientes** está habilitada en la configuración de cliente.  

 Después de habilitar el inventario de software y de que los clientes ejecuten un ciclo de inventario de software, el cliente envía la información de inventario a un punto de administración en el sitio del cliente. Después, el punto de administración reenvía la información de inventario al servidor de sitio de Configuration Manager, que almacena la información de inventario en la base de datos del sitio. El inventario de software se ejecuta en los clientes según la programación que especifique en la configuración de cliente.  

 Puede usar varios métodos para ver los datos de inventario de software que Configuration Manager recopila. Estos incluyen:  

-   Crear consultas que devuelvan dispositivos basados en los archivos que especifique que se encuentran en los dispositivos. Para obtener más información, consulte [Referencia técnica de consultas para System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

-   Crear recopilaciones basadas en consultas que se basan en los archivos que especifique que se encuentran en los dispositivos. Las pertenencias a recopilación basadas en consultas se actualizan automáticamente según una programación. Puede usar recopilaciones de una serie de tareas como implementación de software. Para obtener más información, consulte [Referencia técnica de recopilaciones de System Center Configuration Manager](../../../../core/clients/manage/collections/collections-technical-reference.md).  

-   Ejecutar informes que muestren detalles específicos sobre los archivos en dispositivos de su organización. Para obtener más información, consulte [Generación de informes en System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

-   Usar el Explorador de recursos para examinar la información detallada sobre los archivos inventariados y recopilados de los dispositivos cliente. Para obtener más información, consulte [Cómo usar el Explorador de recursos para ver el inventario de software en System Center Configuration Manager](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

 Cuando se ejecuta el inventario de software en un dispositivo cliente, el primer informe de inventario devuelto es siempre un inventario completo. Los informes de inventario posteriores contienen solo información de inventario diferencial. El servidor de sitio procesa la información de inventario diferencial en el orden en que se recibe. Si falta información de inventario diferencial para un cliente, el servidor de sitio rechaza la información de inventario diferencial adicional e indica al cliente que ejecute un ciclo de inventario completo.  

 Configuration Manager proporciona compatibilidad limitada con equipos de arranque dual. Configuration Manager puede detectar equipos de arranque dual, pero solo devuelve información de inventario del sistema operativo que estaba activo en el momento del inventario.  

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventario de software para dispositivos móviles inscritos con Microsoft Intune  
 Puede recopilar inventario en aplicaciones instaladas en dispositivos móviles. Las aplicaciones que se incluyen en el inventario dependerán de si el dispositivo es propiedad de la empresa o personal. Para dispositivos personales, las únicas aplicaciones inventariadas son las administradas por Microsoft Intune.  

> [!NOTE]  
>  El inventario de las aplicaciones instaladas en dispositivos móviles se recopila como parte del proceso de inventario de hardware en Configuration Manager. Para obtener más información, consulte [Cómo configurar el inventario de hardware en dispositivos móviles inscritos mediante Microsoft Intune y System Center Configuration Manager](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md).  

 En la siguiente tabla se enumeran qué aplicaciones están inventariadas para dispositivos de propiedad personal o de empresa.  

|Plataforma|Para dispositivos personales|Para dispositivos de la compañía|  
|--------------|---------------------------------|--------------------------------|  
|Windows 8.1 (sin el cliente de Configuration Manager)|Solo aplicaciones administradas|Solo aplicaciones administradas|  
|Windows Phone 8|Solo aplicaciones administradas|Solo aplicaciones administradas|  
|Windows RT|Solo aplicaciones administradas|Solo aplicaciones administradas|  
|iOS|Solo aplicaciones administradas|Todas las aplicaciones instaladas en el dispositivo|  
|Android|Solo aplicaciones administradas|Todas las aplicaciones instaladas en el dispositivo|  



<!--HONumber=Nov16_HO1-->


