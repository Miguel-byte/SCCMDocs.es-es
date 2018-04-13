---
title: Panel de administración conjunta
titleSuffix: System Center Configuration Manager
description: Revise la información sobre la administración conjunta mediante el panel.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
caps.latest.revision: 1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 380ca748921a806a0e5edf608a62e8a44edf4d84
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2018
---
# <a name="co-management-dashboard-in-system-center-configuration-manager"></a>Panel de administración conjunta en System Center Configuration Manager
*Se aplica a: System Center Configuration Manager (Rama actual)*

A partir de la versión 1802, puede ver un panel con información sobre la administración conjunta. El panel le ayudará a revisar los equipos que se administran conjuntamente en el entorno. Los gráficos ayudan a identificar los dispositivos que podrían requerir atención.<!--1356648-->

## <a name="open-the-co-management-dashboard"></a>Abrir el panel de administración conjunta
Para abrir el panel de administración conjunta, siga estos pasos: 

1. Abra la consola de Configuration Manager. 
2. Haga clic en el nodo **Supervisión**. 
3. Para cargar el panel, haga clic en **Administración conjunta**.

## <a name="reviewing-information-in-the-co-management-dashboard"></a>Revisión de la información en el panel de administración conjunta

En el panel de administración conjunta se muestran cuatro gráficos para el entorno. 

- **Dispositivos administrados conjuntamente**: proporciona el porcentaje de los dispositivos administrados conjuntamente en todo el entorno.

    ![Gráfico de los dispositivos administrados conjuntamente](media\co-management-dashboard\Percent-Co-managed-graph.PNG)

- **Distribución del sistema operativo cliente**: muestra el número de dispositivos cliente por sistema operativo por versión. Se usan las agrupaciones siguientes: </br>
    - Windows 7 y 8.x
    - Windows 10 anterior a la versión 1709
    - Windows 10 1709 y versiones posteriores

         > [!NOTE] 
         > Windows 10, versión 1709 y versiones posteriores, es un requisito previo para la administración conjunta.

     Al mantener el puntero sobre una sección del gráfico se proporciona el porcentaje de los dispositivos en la agrupación de sistema operativo seleccionada.

     ![Gráfico de la distribución de sistemas operativos de cliente](media\co-management-dashboard\Co-management-OS-distribution-graph.PNG)

- **Estado de la administración conjunta**: el desglose de los dispositivos que se ejecutan correctamente o con error en las categorías siguientes:
    - Se ejecuta correctamente, Unidos a Azure AD híbrido
    - Se ejecuta correctamente, Unido a Azure AD
    - Error: Error de inscripción automática
    
     Al mantener el puntero sobre una sección del gráfico se proporciona el porcentaje de los dispositivos en la categoría. 

     ![Gráfico de estado de la administración conjunta](media\co-management-dashboard\Co-management-status-graph.PNG)

     Al hacer clic en una sección del gráfico se tiene acceso a una lista de dispositivos para la categoría.
 
     ![Lista de dispositivos de error de inscripción](media\co-management-dashboard\Enrollment-Failure_Device-List.PNG)


- **Transición de la carga de trabajo**: muestra un gráfico de barras con el número de dispositivos que se han pasado a Microsoft Intune para las cuatro cargas de trabajo disponibles:
    - Directivas de cumplimiento
    - Acceso a los recursos
    - Windows Update para empresas
    - Endpoint Protection

     Al mantener el puntero sobre una sección del gráfico se proporciona el número de dispositivos que se ha pasado para la carga de trabajo. 
     ![Gráfico de barras de la transición de la carga de trabajo](media\co-management-dashboard\Workload-Transition.PNG)


## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la administración conjunta, vea:
 - [Administración conjunta para dispositivos Windows 10](/sccm/core/clients/manage/co-management-overview.md)
 - [Preparación de dispositivos Windows 10 para la administración conjunta](/sccm/core/clients/manage/co-management-prepare.md)

    
