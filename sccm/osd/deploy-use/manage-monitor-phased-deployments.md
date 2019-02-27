---
title: Administración y supervisión de implementaciones por fases
titleSuffix: Configuration Manager
description: Aprenda a administrar y supervisar las implementaciones por fases para el software en Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5ebf89e46b33649f12ea5770d6e771e811a66094
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125738"
---
# <a name="manage-and-monitor-phased-deployments"></a>Administración y supervisión de implementaciones por fases

En este artículo se describe cómo administrar y supervisar las implementaciones por fases. Las tareas de administración incluyen iniciar manualmente la siguiente fase y suspender o reanudar una fase. 

En primer lugar, deberá crear una implementación por fases: 
- [Aplicación](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  
- [Actualización de software](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [Secuencia de tareas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)  



## <a name="bkmk_move"></a> Pasar a la fase siguiente

Cuando se selecciona la opción **Iniciar manualmente la segunda fase de implementación** el sitio no inicia automáticamente la siguiente fase según los criterios de éxito. Debe mover la implementación por fases a la siguiente fase.  

1. Cómo se inicia esta acción varía según el tipo de software implementado:  

    - **Aplicación** (solo en la versión 1806 o posteriores): vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**.   

    - **Actualización de software** (solo en la versión 1810 o posteriores): vaya al área de trabajo **Biblioteca de software** y, después, seleccione uno de los nodos siguientes:    
        - Actualizaciones de software  
            - **Todas las actualizaciones de software**  
            - **Grupos de actualizaciones de software**   
        - Mantenimiento de Windows 10, **Todas las actualizaciones de Windows 10**  
        - Administración de cliente de Office 365, **Actualizaciones de Office 365**  

    - **Secuencia de tareas**: En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y seleccione **Secuencias de tareas**.   

2. Seleccione el software con la implementación por fases.  

3. En el panel de detalles, cambie a la pestaña **Implementaciones por fases**.  

4. Seleccione la implementación por fases y haga clic en **Pasar a la siguiente fase** en la cinta.  

    ![Clic con el botón derecho en el menú para mostrar acciones en una implementación por fases](media/Suspend-phased-deployment.PNG)



## <a name="bkmk_suspend"></a> Suspender y reanudar fases 

Puede suspender o reanudar manualmente una implementación por fases. Por ejemplo, usted crea una implementación por fases para una secuencia de tareas. Durante la supervisión de la fase de su grupo piloto, observa un gran número de errores. Suspende la implementación por fases para evitar que más dispositivos ejecuten la secuencia de tareas. Después de resolver el problema, reanuda la implementación por fases para continuar con la implementación. 

1. Cómo se inicia esta acción varía según el tipo de software implementado:  

    - **Aplicación** (solo en la versión 1806 o posteriores): vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**.   

    - **Actualización de software** (solo en la versión 1810 o posteriores): vaya al área de trabajo **Biblioteca de software** y, después, seleccione uno de los nodos siguientes:    
        - Actualizaciones de software  
            - **Todas las actualizaciones de software**  
            - **Grupos de actualizaciones de software**   
        - Mantenimiento de Windows 10, **Todas las actualizaciones de Windows 10**  
        - Administración de cliente de Office 365, **Actualizaciones de Office 365**  

    - **Secuencia de tareas**: En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y seleccione **Secuencias de tareas**. Seleccione una secuencia de tareas existente y después haga clic en **Crear implementación por fases** en la cinta.  

2. Seleccione el software con la implementación por fases.  

3. En el panel de detalles, cambie a la pestaña **Implementaciones por fases**.  

4. Seleccione la implementación por fases y haga clic en **Suspender** o **Reanudar** en la cinta.  

<!-- Removed for 1806, need to clarify behavior with engineering
When you suspend a phased deployment, it sets the available and deadline times on the active deployments to a future time. When you resume, it generates a new schedule based on when you resume the phased deployment. The new schedule helps to avoid problems if you resume after the original deadline. For example, the initial schedule has the required deadline seven days after the deployment is available. You suspend it on the second day. If you aren't ready to resume it until day eight, you don't want the deployment to be immediately past the deadline. So it generates a new deadline starting from when you resume the phased deployment on day eight. 
-->


## <a name="bkmk_monitor"></a> Supervisar
<!--1358577-->

A partir de la versión 1806, las implementaciones por fases ahora tienen una experiencia de supervisión nativa. En el nodo **Implementaciones** del área de trabajo **Supervisión**, seleccione una implementación por fases y luego haga clic en **Estado de implementación por fases** en la cinta de opciones.

![Panel de estado de implementación por fases que muestra el estado de dos fases](media/1358577-phased-deployment-status.png)

Este panel muestra la siguiente información para cada fase de la implementación:  

- **Dispositivos en total**: número de dispositivos que abarca esta fase.  

- **Estado**: indica el estado actual de esta fase. Cada fase puede tener uno de los siguientes estados:  

    - **Implementación creada**: la implementación por fases creó una implementación del software en la colección para esta fase. Los clientes son destinos activos con este software.  

    - **En espera**: la fase anterior aún no ha alcanzado los criterios de idoneidad para que la implementación continúe en esta fase.  

    - **Suspendida**: un administrador ha suspendido la implementación.  

- **Progreso**: estados de implementación con códigos de color de los clientes. Por ejemplo: Correcto, En curso, Error, Requisitos no cumplidos y Desconocido. 

#### <a name="success-criteria-tile"></a>Icono Criterios de éxito

Use el menú desplegable **Fase de selección** para cambiar la vista al icono **Criterios de éxito**. Este icono compara el **Objetivo de la fase** con el cumplimiento actual de la implementación. Con la configuración predeterminada, el objetivo de esta fase es 95 %. Este valor significa que la implementación necesita un cumplimiento del 95 % para pasar a la siguiente fase. 

En este ejemplo, el objetivo de esta fase es el 65 %, y el cumplimiento actual es un 66,7 %. La implementación por fases se mueve automáticamente a la segunda fase, porque la primera fase cumple los criterios de éxito.  

![Icono Criterios de éxito de ejemplo de Estado de implementación por fases](media/pod-status-success-criteria-tile.png)

El objetivo de esta fase es el mismo que el **Porcentaje de éxito de la implementación** en la Configuración de fase de la *siguiente* fase. Para que la implementación por fases inicie la fase siguiente, esa segunda fase define los criterios de éxito de la primera fase. Para ver esta configuración: 

1. Vaya al objeto de implementación por fases en el software y abra Propiedades de implementación por fases.  

2. Cambie a la pestaña **Fases**. Seleccione **Fase 2** y haga clic en **Ver**.  

3. En la ventana Propiedades de la fase, cambie a la pestaña **Configuración de fase**.  

4. Vea el valor de **Porcentaje de éxito de la implementación** en el grupo *Criterios de éxito de la fase anterior*.  

Por ejemplo, las siguientes propiedades son para la misma fase que el icono de criterio de éxito que se muestra anteriormente, donde el criterio es el 65 %:  
![Pestaña de configuración de fase en las propiedades de fase](media/phase-properties-phase-settings.png)

