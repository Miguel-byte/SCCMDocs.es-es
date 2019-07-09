---
title: Administración de consultas
titleSuffix: Configuration Manager
description: Aprenda a administrar sus consultas. Incluye una tabla de referencia detallada.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 456289520e25fe94da7e94f6a795537f68ba069e
ms.sourcegitcommit: 3a3f40f3d39cbecfb9219a64c0185ea4b2ef9671
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/04/2019
ms.locfileid: "67561974"
---
# <a name="how-to-manage-queries-in-system-center-configuration-manager"></a>Cómo administrar consultas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Este artículo puede ayudarlo a administrar consultas en System Center Configuration Manager.  

 Para obtener información acerca de cómo crear consultas, vea [How to create queries in System Center Configuration Manager](../../../core/servers/manage/create-queries.md) (Creación de consultas en System Center Configuration Manager).  

## <a name="manage-queries"></a>Administración de consultas
 En el área de trabajo **Supervisión** , seleccione **Consultas**, seleccione la consulta que se debe administrar y luego seleccione una tarea de administración.  

 En la tabla siguiente se incluye información sobre las tareas de administración.  

|Tarea de administración|Detalles| 
|---------------------|-------------|
|**Ejecutar**|Ejecuta la consulta seleccionada y muestra los resultados en la consola de Configuration Manager.|
|**Instalar cliente**|Abre el **Asistente para instalación de cliente** que le permite instalar el cliente de Configuration Manager en los equipos devueltos por la consulta seleccionada.<br /><br /> Esta opción no está disponible para consultas que devuelven dispositivos móviles, usuarios o grupos de usuarios. <br /><br /> Para obtener más información sobre cómo instalar clientes de Configuration Manager mediante la inserción de cliente, consulte [Implementar clientes en equipos Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).| 
|**Exportarar**|Abre el **Asistente para exportar objetos**. Este asistente le permite exportar la consulta a un archivo Managed Object Format (MOF) que luego puede importar en otro sitio.
|**Moverr**|Abre el cuadro de diálogo **Mover elementos seleccionados**. Este cuadro de diálogo le permite mover la consulta seleccionada a una carpeta que haya creado anteriormente en el nodo **Consultas**.|

## <a name="next-steps"></a>Pasos siguientes 
 [Cómo crear consultas en System Center Configuration Manager](../../../core/servers/manage/create-queries.md)
