---
title: Ver el inventario de hardware | Explorador de recursos | System Center Configuration Manager
description: Use el Explorador de recursos para ver el inventario de hardware en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: 7
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 12bf49b6a68d277c7f505ddfe37556363d0e3e53


---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>Cómo usar el Explorador de recursos para ver el inventario de hardware en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use el Explorador de recursos en System Center Configuration Manager para ver información sobre el inventario de hardware recopilado de los clientes de la jerarquía.  

> [!NOTE]  
>  Explorador de recursos no mostrará ningún inventario datos hasta que ha ejecutado un ciclo de inventario de hardware en el cliente se conectan a.  

 El Explorador de recursos de Configuration Manager contiene las siguientes secciones relacionadas con el inventario de hardware:  

-   **Hardware**: contiene el inventario de hardware más reciente recopilado del dispositivo cliente de Configuration Manager especificado. Puede revisar el artículo de inventario **estado de la estación de trabajo** para detectar la hora y fecha cuando realizó un inventario de hardware por última vez el dispositivo.  

-   **Historial de hardware**: contiene un historial de elementos inventariados que han cambiado desde que se realizó el último inventario de hardware. Cada elemento de la lista contiene un nodo **Actual** y uno o más nodos *<fecha>\>*. Puede comparar la información del nodo actual a uno de los nodos históricos para detectar los elementos que han cambiado en el inventario de hardware de los equipos cliente.  

    > [!NOTE]  
    >  Configuration Manager conserva el historial de inventario de hardware durante el número de días especificado en la tarea de mantenimiento de sitio **Eliminar historial de inventario antiguo**.  

> [!NOTE]  
>  Para obtener información sobre cómo ver el inventario de hardware de clientes que ejecutan Linux y UNIX, consulte [How to monitor clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md) (Cómo supervisar clientes para servidores Linux y UNIX en System Center Configuration Manager).  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Ejecución del Explorador de recursos desde la consola de Configuration Manager  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Dispositivos** o abra cualquier recopilación que muestre dispositivos.  

3.  Haga clic en el equipo que contiene el inventario que quiere ver y, a continuación, en la pestaña **Inicio** , en el grupo **Dispositivos** , haga clic en **Iniciar** y, a continuación, haga clic en **Explorador de recursos**. El **Resource Explorer** se abrirá la ventana.  

4.  Puede hacer clic con el botón derecho en cualquier elemento del panel derecho de la ventana **Explorador de recursos** y, a continuación, hacer clic en **Propiedades** para abrir el cuadro de diálogo **Propiedades** de *<nombre del elemento\>* que le ayudará a ver la información de inventario recopilada en un formato más legible.  

5.  Cuando haya terminado, cierre la ventana **Explorador de recursos** .  



<!--HONumber=Nov16_HO1-->


