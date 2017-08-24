---
title: Ver el inventario de hardware | Microsoft Docs | Explorador de recursos
description: Use el Explorador de recursos para ver el inventario de hardware en System Center Configuration Manager.
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: "7"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: e39fa60a5d215fa1b0a98d4463058497e63a4d4f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>Cómo usar el Explorador de recursos para ver el inventario de hardware en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use el Explorador de recursos en System Center Configuration Manager para ver información sobre el inventario de hardware recopilado de los clientes de la jerarquía.  

> [!NOTE]  
>  Explorador de recursos no mostrará ningún inventario datos hasta que ha ejecutado un ciclo de inventario de hardware en el cliente se conectan a.  

 El Explorador de recursos tiene las siguientes secciones relacionadas con el inventario de hardware:  

-   **Hardware**: contiene el inventario de hardware más reciente recopilado del dispositivo cliente especificado.  **Estado de estación de trabajo** tiene la hora y la fecha en la que el dispositivo ha realizado por última vez un inventario de hardware.  

-   **Historial de hardware**: contiene un historial de elementos inventariados que han cambiado desde que se realizó el último inventario de hardware. Cada elemento contiene un nodo **Actual** y uno o más nodos *<fecha\>*. Puede comparar la información del nodo actual con la de uno de los nodos históricos para detectar los elementos que han cambiado.  

    > [!NOTE]  
    >  Configuration Manager conserva el historial de inventario de hardware durante el número de días especificado en la tarea de mantenimiento de sitio **Eliminar historial de inventario antiguo**.  

> [!NOTE]  
>  Para obtener información sobre cómo ver el inventario de hardware de clientes que ejecutan Linux y UNIX, consulte [Cómo supervisar clientes para servidores Linux y UNIX en System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md).  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Ejecución del Explorador de recursos desde la consola de Configuration Manager  

1.  En la consola de Configuration Manager, pulse **Activos y compatibilidad** > **Dispositivos**, o abra cualquier recopilación que muestre dispositivos.  

3.  Seleccione el equipo que contiene el inventario que quiere ver y, después, en la pestaña **Inicio** > grupo **Dispositivos**, pulse **Iniciar** >  **Explorador de recursos**.   

4.  Haga clic con el botón derecho en cualquier elemento del panel derecho de la ventana **Explorador de recursos** y pulse **Propiedades** para abrir el cuadro de diálogo **Propiedades** de *<nombre del elemento\>* para ver la información de inventario recopilada en un formato más legible.  

