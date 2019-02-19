---
title: Visualización del inventario de software con el Explorador de recursos
titleSuffix: Configuration Manager
description: Use el Explorador de recursos para ver el inventario de software en System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 341f1530e0b5bc9486cf062b5f16ede2154439ed
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129653"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>Cómo usar el Explorador de recursos para ver el inventario de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

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
 
