---
title: Ver el inventario de software | Explorador de recursos | System Center Configuration Manager
description: Use el Explorador de recursos para ver el inventario de software en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b4ecb27cfb119ae80d1ed7d90d84c61a87b183c8


---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>Cómo usar el Explorador de recursos para ver el inventario de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use el Explorador de recursos en System Center Configuration Manager para ver información sobre el inventario de software recopilado de los equipos de la jerarquía.  

> [!NOTE]  
>  El Explorador de recursos no mostrará ningún dato de inventario hasta que se haya ejecutado un ciclo de inventario de software en el cliente al que se está conectando.  

 El Explorador de recursos de Configuration Manager contiene las siguientes secciones relacionadas con el inventario de software:  

-   **Software**: la sección de software del Explorador de recursos contiene cuatro secciones:  

    -   **Archivos recopilados**: muestra información sobre los archivos que se recopilaron durante el inventario de software.  

    -   **Detalles de archivo**: muestra información sobre los archivos incluidos en el inventario durante el inventario de software que no están asociados a un fabricante o producto específico.  

    -   **Última exploración de software**: muestra la fecha y hora del último inventario de software y recopilación de archivos que se ejecutó en el equipo cliente.  

    -   **Detalles del producto**: muestra información sobre los productos de software que se han inventariado en el inventario de software, agrupados por fabricante.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Para ejecutar el Explorador de recursos desde la consola de Configuration Manager  
 Use el siguiente procedimiento para ejecutar el Explorador de recursos en Configuration Manager.  

#### <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Para ejecutar el Explorador de recursos desde la consola de Configuration Manager  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Dispositivos** o abra cualquier recopilación que muestre dispositivos.  

3.  Haga clic en el equipo que contiene el inventario que quiere ver y, a continuación, en la pestaña **Inicio** , en el grupo **Dispositivos** , haga clic en **Iniciar** y, a continuación, haga clic en **Explorador de recursos**. Se abrirá la ventana **Explorador de recursos** .  

4.  Puede hacer clic con el botón derecho en cualquier elemento del panel derecho de la ventana del Explorador de recursos y, después, hacer clic en **Propiedades** para abrir el cuadro de diálogo **Propiedades** de *<nombre del elemento\>*, que le ayudará a ver la información de inventario recopilada en un formato más legible.  

5.  Cuando haya terminado, cierre la ventana **Explorador de recursos** .  



<!--HONumber=Nov16_HO1-->


