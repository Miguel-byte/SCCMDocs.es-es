---
title: "Visualización del inventario de software con el Explorador de recursos"
titleSuffix: Configuration Manager
description: Use el Explorador de recursos para ver el inventario de software en System Center Configuration Manager.
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 242bd336fcb13172097e26187a48c924dbd9acb6
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>Cómo usar el Explorador de recursos para ver el inventario de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use el Explorador de recursos en System Center Configuration Manager para ver información sobre el inventario de software recopilado de los equipos de la jerarquía.  

> [!NOTE]  
>  El Explorador de recursos no mostrará ningún dato de inventario hasta que se haya ejecutado un ciclo de inventario de software en el cliente.  

 El Explorador de recursos proporciona la siguiente información de inventario de software:  

-   **Software**:  

    -   **Archivos recopilados**: archivos que se han recopilado durante el inventario de software.  

    -   **Detalles de archivo**: archivos incluidos en el inventario durante el inventario de software que no están asociados a un fabricante o producto específico.  

    -   **Última exploración de software**: fecha y hora del último inventario de software y recopilación de archivos para el equipo cliente.  

    -   **Detalles del producto**: productos de software que se han inventariado en el inventario de software, agrupados por fabricante.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Para ejecutar el Explorador de recursos desde la consola de Configuration Manager  

1.  En la consola de Configuration Manager, pulse **Activos y compatibilidad**.

2.  En el área de trabajo **Activos y compatibilidad**, pulse **Dispositivos** o abra cualquier recopilación que muestre dispositivos.  

3.  Seleccione el equipo que contiene el inventario que quiere ver y, después, en la pestaña **Inicio** > grupo **Dispositivos**, pulse **Iniciar** > **Explorador de recursos**.

4.  Puede hacer clic con el botón derecho en cualquier elemento del panel derecho de la ventana Explorador de recursos y pulsar **Propiedades** para ver la información de inventario recopilada en un formato más legible.  
 
