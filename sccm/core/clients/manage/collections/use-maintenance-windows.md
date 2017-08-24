---
title: Usar ventanas de mantenimiento | Microsoft Docs
description: Use recopilaciones y ventanas de mantenimiento para administrar eficazmente los clientes en System Center Configuration Manager.
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: fa67cf597c73bab47209c9b98539f97e174ae70b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>Cómo usar ventanas de mantenimiento en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Las ventanas de mantenimiento le permiten definir un período en el que pueden realizarse operaciones de Configuration Manager en una recopilación de dispositivos. Puede usar las ventanas de mantenimiento para ayudar a garantizar que los cambios en la configuración de cliente se produzcan durante períodos que no afecten a la productividad.  

 Las siguientes operaciones admiten ventanas de mantenimiento:  

-   Implementaciones de software  

-   Implementaciones de actualización de software  

-   Implementación y evaluación de la configuración de cumplimiento  

-   Implementaciones del sistema operativo  

-   Implementaciones de secuencia de tareas  

 Configure ventanas de mantenimiento con una fecha de inicio, una hora de inicio y de finalización y un patrón de periodicidad. La duración máxima de una ventana tiene que ser inferior a 24 horas. De manera predeterminada, los reinicios de equipo ocasionados por una implementación no se permiten fuera de una ventana de mantenimiento, pero puede invalidar el valor predeterminado. Las ventanas de mantenimiento afectan solo al tiempo en que se ejecuta el programa de implementación; las aplicaciones configuradas para descargarse y ejecutarse de manera local pueden descargar contenido fuera de la ventana.  

 Si un equipo cliente es miembro de una recopilación de dispositivos que tiene una ventana de mantenimiento, un programa de implementación solo se ejecuta si el tiempo de ejecución máximo permitido no supera la duración configurada para la ventana. Si el programa no se ejecuta, se genera una alerta y la implementación se vuelve a ejecutar durante la siguiente ventana de mantenimiento programada que tenga tiempo disponible.  

## <a name="using-multiple-maintenance-windows"></a>Usar varias ventanas de mantenimiento  
 Si un equipo cliente forma parte de varias recopilaciones de dispositivos que tienen ventanas de mantenimiento, se aplican estas reglas:  

-   Si no se superponen las ventanas de mantenimiento, se consideran dos ventanas de mantenimiento independientes.  

-   Si las ventanas de mantenimiento se superponen, se tratan como una ventana de mantenimiento único que abarca el período de tiempo cubierto por ambas ventanas de mantenimiento. Por ejemplo, si dos ventanas, cada una de una hora de duración, se superponen durante 30 minutos, la duración efectiva de la ventana de mantenimiento será de 90 minutos.  

 Cuando un usuario inicia la instalación de una aplicación desde el Centro de software, la aplicación se instala de inmediato, independientemente de que haya o no alguna ventana de mantenimiento.  

 Si la implementación de una aplicación con un propósito de **Requerido** alcanza su fecha límite de instalación fuera del horario laboral configurado por un usuario en el Centro de software, la aplicación se instalará.  

### <a name="how-to-configure-maintenance-windows"></a>Cómo configurar ventanas de mantenimiento  

1.  En la consola de Configuration Manager, pulse **Activos y compatibilidad**>  **Recopilaciones de dispositivos**.  

3.  En la lista **Recopilaciones de dispositivos**, seleccione una recopilación. No se puede crear ventanas de mantenimiento para la recopilación **Todos los sistemas** .  

4.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

5.  En la pestaña **Ventanas de mantenimiento** del cuadro de diálogo **Propiedades de &lt;\>nombre de recopilación**, pulse el icono **Nueva**.  

6.  Complete el cuadro de diálogo **&lt;Nueva\> programación**.  

7.  Haga una selección en la lista desplegable **Aplicar esta programación a**.  

8.  Pulse **Aceptar** y, después, cierre el cuadro de diálogo **&lt;Propiedades\> de nombre de recopilación**.  
