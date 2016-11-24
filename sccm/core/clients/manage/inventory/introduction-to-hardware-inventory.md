---
title: Inventario de hardware | System Center Configuration Manager
description: "Obtenga una introducción al inventario de hardware en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6a0addd31f6e8cd7ef91303cc664d9242c22e0f2


---
# <a name="introduction-to-hardware-inventory-in-system-center-configuration-manager"></a>Introducción al inventario de hardware en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use el inventario de hardware en System Center Configuration Manager para recopilar información sobre la configuración del hardware de dispositivos cliente en su organización. Para recopilar el inventario de hardware, la opción **Habilitar inventario de hardware en clientes** debe estar habilitada en la configuración de cliente.  

 Después de habilitar el inventario de hardware y de que el cliente ejecute un ciclo de inventario de hardware, el cliente envía la información de inventario que se ha recopilado a un punto de administración en el sitio del cliente. Después, el punto de administración reenvía la información de inventario al servidor de sitio de Configuration Manager, que almacena la información de inventario en la base de datos del sitio. El inventario de hardware se ejecuta en los clientes según la programación que especifique en la configuración de cliente.  

 Puede usar varios métodos para ver los datos de inventario de hardware que Configuration Manager recopila. Estos incluyen:  

-   Crear consultas que devuelven los dispositivos que se basan en una configuración de hardware específica. Para obtener más información, consulte [Referencia técnica de consultas para System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

-   Crear recopilaciones basadas en consultas en función de una configuración de hardware específica. Las pertenencias a recopilación basadas en consultas se actualizan automáticamente según una programación. Puede usar las recopilaciones para varias tareas, que incluyen la implementación de software. Para obtener más información, consulte [Referencia técnica de recopilaciones de System Center Configuration Manager](../../../../core/clients/manage/collections/collections-technical-reference.md).  

-   Ejecutar informes que muestran detalles específicos sobre las configuraciones de hardware de su organización. Para obtener más información, consulte [Generación de informes en System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

-   Utilizar el Explorador de recursos para ver información detallada sobre el inventario de hardware que se recopila de los dispositivos cliente. Para obtener más información, consulte [Cómo usar el Explorador de recursos para ver el inventario de hardware en System Center Configuration Manager](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

 Cuando se ejecuta el inventario de hardware en un dispositivo cliente, los primeros datos de inventario que el cliente devuelve son siempre un inventario completo. La información de inventario posterior contiene solo la información de inventario diferencial. El servidor de sitio procesa la información de inventario diferencial en el orden en que se recibe. Si falta información de inventario diferencial para un cliente, el servidor de sitio rechaza la información de inventario diferencial adicional e indica al cliente que ejecute un ciclo de inventario completo.  

 Configuration Manager proporciona compatibilidad limitada con equipos de arranque dual. Configuration Manager puede detectar equipos de arranque dual, pero solo devuelve información de inventario del sistema operativo que estaba activo cuando se ejecutó el ciclo de inventario.  

> [!NOTE]  
>  Para obtener información sobre cómo usar el inventario de hardware con clientes que ejecutan Linux y UNIX, consulte [Hardware inventory for Linux and UNIX in System Center Configuration Manager (Inventario de hardware para Linux y UNIX en System Center Configuration Manager)](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Inventario ampliado de hardware con Configuration Manager  
 Además del inventario de hardware integrado en Configuration Manager, también puede usar uno de los siguientes métodos para ampliar el inventario de hardware para recopilar información adicional:  

|Método|Descripción|  
|------------|-----------------|  
|Agregar y quitar clases de inventario desde la consola de Configuration Manager|En Configuration Manager, puede habilitar, deshabilitar, agregar y quitar clases de inventario de hardware personalizado desde la consola de Configuration Manager.|  
|Archivos NOIDMIF|Use archivos NOIDMIF para recopilar información sobre los dispositivos cliente que Configuration Manager no puede inventariar. Por ejemplo, podría desea recopilar información número de dispositivos activos que sólo existe como una etiqueta en el dispositivo. El inventario NOIDMIF se asocia automáticamente con el dispositivo cliente del que se recopiló.|  
|Archivos IDMIF|Use archivos IDMIF para recopilar información sobre los activos de la organización que no están asociados con un cliente de Configuration Manager, por ejemplo, proyectores, fotocopiadoras e impresoras de red.|  

 Para obtener más información sobre cómo usar estos métodos para ampliar el inventario de hardware de Configuration Manager, consulte [How to configure hardware inventory in System Center Configuration Manager (Cómo configurar el inventario de hardware en System Center Configuration Manager)](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  



<!--HONumber=Nov16_HO1-->


