---
title: Panel de administración conjunta
titleSuffix: Configuration Manager
description: Utilice el panel de administración conjunta para revisar información sobre los dispositivos administrados conjuntamente.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ad76140285df1c0125fcd2efab0f4794ed4881bf
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52455958"
---
# <a name="co-management-dashboard-in-configuration-manager"></a>Panel de administración conjunta en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

A partir de la versión 1802, vea un panel con información sobre la administración conjunta. El panel le ayudará a revisar los equipos que se administran conjuntamente en el entorno. Los gráficos ayudan a identificar los dispositivos que podrían requerir atención.<!--1356648-->

En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y haga clic en el nodo **Administración conjunta**.

A partir de la versión 1810, el panel de administración conjunta se ha mejorado con información más detallada. <!--1358980-->



## <a name="dashboard-tiles"></a>Mosaicos del panel 

El panel de administración conjunta muestra diferentes mosaicos en función de la versión del sitio. 


### <a name="co-managed-devices"></a>Dispositivos administrados conjuntamente

*Se aplica a las versiones 1802 y 1806*

Muestra el porcentaje de dispositivos administrados conjuntamente en todo el entorno.
 ![Mosaico de dispositivos administrados conjuntamente](media\co-management-dashboard\Percent-Co-managed-graph.PNG)


### <a name="client-os-distribution"></a>Distribución del sistema operativo cliente

*Se aplica a todas las versiones* 

Muestra el número de dispositivos cliente en función del sistema operativo por versión. Se usan las siguientes agrupaciones:  
- Windows 7 y 8.x  
- Windows 10 anterior a la versión 1709  
- Windows 10 1709 y versiones posteriores  

    > [!Tip]  
    > Windows 10, versión 1709 y versiones posteriores, es un requisito previo para la administración conjunta.  

Mantenga el puntero sobre una sección del gráfico para mostrar el porcentaje de dispositivos que forman parte de ese grupo de sistemas operativos.
 ![Mosaico de la distribución del sistema operativo cliente](media\co-management-dashboard\Co-management-OS-distribution-graph.PNG)


### <a name="co-management-status-donut"></a>Estado de la administración conjunta (anillo)

*Se aplica a las versiones 1802 y 1806*

Muestra el desglose de los dispositivos que se ejecutan correctamente o con error en las categorías siguientes:
- Se ejecuta correctamente, Unidos a Azure AD híbrido  
- Se ejecuta correctamente, Unido a Azure AD  
- Error: Error de inscripción automática  

Mantenga el puntero sobre una sección del gráfico para ver el porcentaje de los dispositivos en esa categoría. 
 ![Mosaico del estado de la administración conjunta (anillo)](media\co-management-dashboard\Co-management-status-graph.PNG)

Seleccione una sección del gráfico para ver la lista de dispositivos de esa categoría.
 ![Lista de dispositivos de error de inscripción](media\co-management-dashboard\Enrollment-Failure_Device-List.PNG)


### <a name="co-management-status-funnel"></a>Estado de la administración conjunta (embudo)

*Se aplica a la versión 1810 y posteriores*

Un gráfico de embudo que muestra el número de dispositivos con los siguientes estados del proceso de inscripción:  
- Dispositivos aptos  
- Programado  
- Inscripción iniciada  
- Inscritos  

![Mosaico del estado de la administración conjunta (embudo)](media\co-management-dashboard\1358980-status-funnel.png)


### <a name="co-management-enrollment-status"></a>Estado de la inscripción de administración conjunta

*Se aplica a la versión 1810 y posteriores*

Muestra un desglose del estado de los dispositivos en las categorías siguientes:
- Se ejecuta correctamente, unido a Azure AD híbrido  
- Se ejecuta correctamente, unido a Azure AD  
- Inscribiendo, unido a Azure AD híbrido  
- Error, unido a Azure AD híbrido  
- Error, unido a Azure AD  
- Inicio de sesión de usuario pendiente  

Seleccione un estado del icono para explorar en profundidad una lista de dispositivos de ese estado.  

![Mosaico del estado de la inscripción de administración conjunta](media\co-management-dashboard\1358980-enrollment-status.png)


### <a name="enrollment-errors"></a>Errores de inscripción

*Se aplica a la versión 1810 y posteriores*

Una tabla en la que se muestra el recuento de los errores de inscripción de los dispositivos.  


### <a name="workload-transition"></a>Transición de la carga de trabajo

*Se aplica a todas las versiones*

Muestra un gráfico de barras con el número de dispositivos que se han pasado a Microsoft Intune para las cargas de trabajo disponibles. La lista de las cargas de trabajo varía según la versión de Configuration Manager. Para obtener más información, vea [Cargas de trabajo que se pueden pasar a Intune](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune).

Mantenga el puntero sobre una sección del gráfico para ver el número de dispositivos que se ha pasado para la carga de trabajo. 
 ![Gráfico de barras de la transición de la carga de trabajo](media\co-management-dashboard\Workload-Transition.PNG)


## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la administración conjunta, vea:
 - [Administración conjunta para dispositivos Windows 10](/sccm/core/clients/manage/co-management-overview)
 - [Preparación de dispositivos Windows 10 para la administración conjunta](/sccm/core/clients/manage/co-management-prepare)

    
