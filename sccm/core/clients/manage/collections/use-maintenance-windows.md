---
title: Usar ventanas de mantenimiento | System Center Configuration Manager
description: Use recopilaciones y ventanas de mantenimiento para administrar eficazmente los clientes en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: c29d8a1bc0d224113a1c906893308d5582894a01


---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>Cómo usar ventanas de mantenimiento en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Las ventanas de mantenimiento en System Center Configuration Manager proporcionan un medio para que los usuarios administrativos definan un período de tiempo durante el cual es posible que se realicen varias operaciones de Configuration Manager en los miembros de una recopilación de dispositivos. Puede usar las ventanas de mantenimiento para ayudar a garantizar que los cambios en la configuración de cliente se produzcan durante períodos que no afecten la productividad de la organización.  

 Las siguientes operaciones de Configuration Manager admiten ventanas de mantenimiento:  

-   Implementaciones de software  

-   Implementaciones de actualización de software  

-   Implementación y evaluación de la configuración de cumplimiento  

-   Implementaciones del sistema operativo  

-   Implementaciones de secuencia de tareas  

 Las ventanas de mantenimiento se configuran para una recopilación con fecha de inicio, hora de inicio y de finalización, y un patrón de periodicidad. Cada ventana de mantenimiento debe tener una duración de menos de 24 horas. De forma predeterminada, los reinicios de equipo ocasionados por una implementación no se permiten fuera de una ventana de mantenimiento, pero puede invalidar el valor predeterminado en la configuración de cada implementación. Las ventanas de mantenimiento afectan solo al tiempo en que se ejecuta el programa de implementación; las aplicaciones configuradas para descargarse y ejecutarse de forma local pueden descargar contenido fuera de la ventana de mantenimiento.  

 Si un equipo cliente es miembro de una recopilación de dispositivos que tiene configurada una ventana de mantenimiento, un programa de implementación solo se ejecuta si el tiempo de ejecución máximo permitido no supera la duración configurada para la ventana de mantenimiento. Si el programa no se ejecuta, se genera una alerta y la implementación se vuelve a ejecutar durante la siguiente ventana de mantenimiento programada que tenga tiempo disponible.  

## <a name="using-multiple-maintenance-windows"></a>Usar varias ventanas de mantenimiento  
 Si un equipo cliente forma parte de varias recopilaciones de dispositivos que tienen configuradas ventanas de mantenimiento, se aplican las siguientes reglas:  

-   Si no se superponen las ventanas de mantenimiento, se consideran dos ventanas de mantenimiento independientes.  

-   Si las ventanas de mantenimiento se superponen, se tratan como una ventana de mantenimiento único que abarca el período de tiempo cubierto por ambas ventanas de mantenimiento. Por ejemplo, si dos ventanas de mantenimiento, cada una de una hora de duración, se superponen durante 30 minutos, la duración efectiva de la ventana de mantenimiento sería de 90 minutos.  

 Cuando un usuario inicia la instalación de una aplicación desde el Centro de software, la aplicación se instala de inmediato, independientemente de que haya o no alguna ventana de mantenimiento configurada.  

 Si la implementación de una aplicación con un propósito de **Requerido** alcanza su fecha límite de instalación fuera del horario laboral configurado por un usuario en el Centro de software, la aplicación se instalará.  

### <a name="how-to-configure-maintenance-windows"></a>Cómo configurar ventanas de mantenimiento  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Recopilaciones de dispositivos**.  

3.  En la lista **Recopilaciones de dispositivos** , seleccione la recopilación para la que desea configurar una ventana de mantenimiento.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5.  En la pestaña **Ventanas de mantenimiento** del cuadro de diálogo **Propiedades de &lt;\>nombre de recopilación**, haga clic en el icono **Nueva**.  

    > [!NOTE]  
    >  No se puede crear ventanas de mantenimiento para la recopilación **Todos los sistemas** .  

6.  En el cuadro de diálogo **Programación &lt;nueva\>**, especifique un nombre, una programación y un patrón de periodicidad para la ventana de mantenimiento. También puede habilitar la opción de aplicar la programación a secuencias de tareas únicamente.  

7.  Desde la lista desplegable **Aplicar esta programación a** , seleccione si la ventana de mantenimiento se aplica a todas las implementaciones, solo a actualizaciones de software o solo a secuencias de tareas.  

8.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Programación &lt;nueva\>** y cree la nueva ventana de mantenimiento.  

9. Cierre el cuadro de diálogo **Propiedades de &lt;nombre de recopilación\>**.  



<!--HONumber=Nov16_HO1-->


