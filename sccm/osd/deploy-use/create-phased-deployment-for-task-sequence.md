---
title: Creación de una implementación por fases para una secuencia de tareas
titleSuffix: Configuration Manager
description: Creación de implementaciones por fases para una secuencia de tareas
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2bda41cfd01e5ef90771350e650f68a27c3af6ed
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348640"
---
# <a name="create-phased-deployments-for-a-task-sequence-with-system-center-configuration-manager"></a>Creación de implementaciones por fases para una secuencia de tareas con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las implementaciones por fases automatizan una implementación coordinada y secuencial de una secuencia de tareas en varias recopilaciones. Puede crear implementaciones por fases con el valor predeterminado de dos fases, o bien configurar manualmente varias fases. La implementación por fases de las secuencias de tareas no es compatible con la instalación de medios o PXE. 

>[!NOTE]
> La implementación por fases es una característica de versión preliminar incluida en Configuration Manager 1802. <!--1356837-->

## <a name="security-scope-and-log-file-information"></a>Información y ámbito de seguridad del archivo de registro

**Ámbito de seguridad**:</br>
Las implementaciones creadas por las implementaciones por fases no son visibles para los usuarios que no tengan el ámbito de seguridad **Todos**.

**Archivos de registro**: </br>
SMS_PhasedDeployment.log

## <a name="create-a-default-two-phased-deployment-for-a-task-sequence"></a>Creación de una implementación de dos fases predeterminada para una secuencia de tareas

Use las instrucciones siguientes para crear una implementación por fases. 

1. En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.

2. Haga clic con el botón derecho en una secuencia de tareas existente y seleccione **Create Phased Deployment** (Crear implementación por fases). 

3. En la pestaña **General** asigne un nombre y una descripción (opcional) a la implementación por fases y seleccione **Automatically create a default two phase deployment** (Crear automáticamente una implementación de dos fases predeterminada). 

4. Rellene los campos **First Collection** (Primera recopilación) y **Second Collection** (Segunda recopilación). Seleccione **Siguiente**.

5. En la pestaña **Configuración**, elija una opción para cada una de las opciones de programación y haga clic en **Siguiente** cuando haya terminado. 
    - **Criterios para considerar que la primera fase se ha completado correctamente.** 
        - **Porcentaje de éxito de la implementación**: especifique el porcentaje de dispositivos que completan correctamente la implementación para los criterios de éxito de la fase. 
    - **Condiciones para iniciar la segunda fase de implementación tras el éxito de la primera** (seleccione una):
        - **Iniciar automáticamente esta fase tras un período de aplazamiento (en días)**: elija el número de días que se esperará antes de comenzar la segunda fase después del éxito de la primera. 
        - **Iniciar manualmente la segunda fase de implementación**: no iniciar la segunda fase automáticamente después del éxito de la primera. Requiere que se inicie de forma manual. 
    - **Una vez seleccionado un dispositivo, instalar el software** (seleccione una):
        - **Lo antes posible**: establece la fecha límite para la instalación en el dispositivo en cuanto el dispositivo se selecciona.
        - **Hora límite (relativa a la hora de destino del dispositivo)**: establece la fecha límite para la instalación en un número determinado de días después de que se seleccione el dispositivo. 

6. En el pestaña **Fases**, haga clic en la primera fase y después en **Editar**.  Especifique **Experiencia del usuario** como **Notificaciones al usuario** y **Tratamiento de filtros de escritura para dispositivos de Windows Embedded**. Haga clic en **Aplicar**.

7. Especifique las opciones de **Puntos de distribución** para la fase en la pestaña **Puntos de distribución**. Haga clic en **Aplicar** y **Aceptar**.        

8. En la pestaña **Fases**, modifique la segunda fase para **Experiencia del usuario** y **Puntos de distribución**. Haga clic en **Aplicar** y **Aceptar**.

9. Confirme las selecciones en la pestaña **Resumen** y después haga clic en **Siguiente** para continuar con el asistente.

>[!WARNING]
>Las implementaciones por fases no notificarán si una implementación de secuencia de tareas es de [alto riesgo](/sccm/protect/understand/settings-to-manage-high-risk-deployments.md). 


## <a name="suspend-and-resume-phases-or-move-to-the-next-phase"></a>Suspender y reanudar fases, o pasar a la siguiente fase
En algunas ocasiones, será necesario suspender manualmente una implementación por fases, reanudar una implementación por fases suspendida o pasar a la fase siguiente. 

### <a name="move-to-the-next-phase"></a>Pasar a la fase siguiente
Cuando se selecciona la opción **Iniciar manualmente la segunda fase de implementación**, será necesario iniciar la segunda fase. Use las instrucciones siguientes para pasar a la segunda fase: 

1. En la consola de Configuration Manager, seleccione **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.
2. Resalte la secuencia de tareas.
3. Haga clic en la pestaña **Implementación por fases** situada cerca de la parte inferior de la consola. 
4. Haga clic con el botón derecho en la implementación por fases y seleccione **Move to next phase** (Pasar a la siguiente fase).
![Suspender, reanudar o pasar a la siguiente fase](media/Suspend-phased-deployment.PNG)

### <a name="suspend-or-resume-a-phased-deployment"></a>Suspender o reanudar una implementación por fases
1. En la consola de Configuration Manager, seleccione **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.
2. Resalte la secuencia de tareas y haga clic en la pestaña **Implementación por fases** situada cerca de la parte inferior de la consola. 
3. Seleccione la implementación por fases y haga clic en **Suspender** o **Reanudar** en la cinta.

## <a name="next-steps"></a>Pasos siguientes
[Crear una secuencia de tareas personalizada](create-a-custom-task-sequence.md) </br>
[Crear una secuencia de tareas para implementaciones que no son de sistema operativo](create-a-task-sequence-for-non-operating-system-deployments.md). 








