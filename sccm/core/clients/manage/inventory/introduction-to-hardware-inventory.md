---
title: 'Inventario de hardware '
titleSuffix: Configuration Manager
description: Obtenga una introducción al inventario de hardware en System Center Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 688bb6dc57f5d50e1807bff40a1d1a4c66f4b349
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="introduction-to-hardware-inventory-in-system-center-configuration-manager"></a>Introducción al inventario de hardware en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use el inventario de hardware en System Center Configuration Manager para recopilar información sobre la configuración del hardware de dispositivos cliente en su organización. Para recopilar el inventario de hardware, la opción **Habilitar inventario de hardware en clientes** debe estar habilitada en la configuración de cliente.  

 Después de habilitar el inventario de hardware y de que el cliente ejecute un ciclo de inventario de hardware, el cliente envía la información a un punto de administración en el sitio del cliente. Después, el punto de administración reenvía la información de inventario al servidor de sitio de Configuration Manager, que almacena la información de inventario en la base de datos del sitio. El inventario de hardware se ejecuta en los clientes según la programación que especifique en la configuración de cliente.  

 Puede usar varios métodos para ver los datos de inventario de hardware que Configuration Manager recopila. Estos incluyen:  

-   [Crear consultas que devuelven los dispositivos que se basan en una configuración de hardware específica.](../../../../core/servers/manage/queries-technical-reference.md)  

-   [Crear recopilaciones basadas en consultas en función de una configuración de hardware específica.](../../../../core/clients/manage/collections/introduction-to-collections.md) Las pertenencias a recopilación basadas en consultas se actualizan automáticamente según una programación. Puede usar las recopilaciones para varias tareas, que incluyen la implementación de software .  

-   [Ejecutar informes que muestran detalles específicos acerca de las configuraciones de hardware de su organización.](../../../../core/servers/manage/reporting.md)   

-   [Utilizar el Explorador de recursos](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) para ver información detallada acerca de el inventario de hardware que se recopila de los dispositivos cliente.   

 Cuando se ejecuta el inventario de hardware en un dispositivo cliente, los primeros datos de inventario que el cliente devuelve son siempre un inventario completo. La información de inventario posterior contiene solo la información de inventario diferencial. El servidor de sitio procesa la información de inventario diferencial en el orden en que se recibe. Si falta información diferencial para un cliente, el servidor de sitio rechaza la información diferencial adicional e indica al cliente que ejecute un ciclo de inventario completo.  

 Configuration Manager proporciona compatibilidad limitada con equipos de arranque dual. Configuration Manager puede detectar equipos de arranque dual, pero solo devuelve información de inventario del sistema operativo que estaba activo cuando se ejecutó el ciclo de inventario.  

> [!NOTE]  
>  Para obtener información sobre cómo usar el inventario de hardware con clientes que ejecutan Linux y UNIX, consulte [Hardware inventory for Linux and UNIX in System Center Configuration Manager (Inventario de hardware para Linux y UNIX en System Center Configuration Manager)](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Inventario ampliado de hardware con Configuration Manager  
 Además del inventario de hardware integrado en Configuration Manager, también puede usar uno de los siguientes métodos para ampliar el inventario de hardware para recopilar información adicional:  

- Puede habilitar, deshabilitar, agregar y quitar clases de inventario de hardware personalizado desde la consola de Configuration Manager.|  
- Use archivos NOIDMIF para recopilar información sobre los dispositivos cliente que Configuration Manager no puede inventariar. Por ejemplo, podría desea recopilar información número de dispositivos activos que sólo existe como una etiqueta en el dispositivo. Inventario NOIDMIF se asocia automáticamente con el dispositivo de cliente que se recopilaron de.  
- Use archivos IDMIF para recopilar información acerca de los activos que no están asociados con un cliente de Configuration Manager, por ejemplo, proyectores, fotocopiadoras e impresoras de red.  

 Para obtener más información sobre cómo usar estos métodos para ampliar el inventario de hardware de Configuration Manager, consulte [How to configure hardware inventory in System Center Configuration Manager (Cómo configurar el inventario de hardware en System Center Configuration Manager)](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
