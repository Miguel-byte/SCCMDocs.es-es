---
title: Power Viewer Tool
titleSuffix: Configuration Manager
description: Use Power Viewer Tool para ver el estado de la característica de administración de energía en un cliente de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 09b1cf553aaa5fd75dbf0f7500246263a9bed7a6
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500832"
---
# <a name="power-viewer-tool"></a>Power Viewer Tool

*Se aplica a: System Center Configuration Manager (Rama actual)*

Power Viewer Tool es una de las [herramientas de Configuration Manager](/sccm/core/support/tools). Úsela para ver el estado de la característica de administración de energía en un cliente de Configuration Manager.

Ejecute **PowerVwr.exe** como administrador. Cuando la herramienta se inicia, muestra las capacidades de energía y la configuración de energía del equipo local en la pestaña **Configuración de energía**. 

Para ver los datos de administración de energía de un equipo remoto:  

1. Vaya al menú **Archivo** y haga clic en **Conectar**. 

2. Escriba el nombre del **equipo** y un **nombre de usuario** y **contraseña**, si es necesario. 

Hay tres pestañas en Power Viewer:  

- **Configuración de energía**: vea las funciones de energía y la configuración de energía del equipo de destino.  

- **Actividad diaria**: vea los gráficos de la actividad diaria del cliente, que incluyen la siguiente información:  

    - **Equipo activado**: el estado de energía del equipo en un día. En el modo de suspensión se considera que el equipo está desactivado.  

    - **Supervisión activada**: estado activado o desactivado de la supervisión en un día.  

    - **Usuario activo**: información de la actividad de usuario en un día.  

- **Eventos de energía**: permite visualizar todos los eventos de energía diarios. El cliente resume estos eventos a las 12:00. Este resumen genera datos para el diagrama de actividad diaria.  
