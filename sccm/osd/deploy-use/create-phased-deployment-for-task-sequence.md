---
title: Creación de una implementación por fases
titleSuffix: Configuration Manager
description: Use las implementaciones por fases para automatizar la implementación de software a varias colecciones.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ab238b2cf98da3d7ea1e86ef6462a721d7347e8
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383623"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>Crear implementaciones por fases con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las implementaciones por fases automatizan una implementación coordinada y secuencial de software en varias implementaciones. Por ejemplo, implemente el software en una colección piloto y luego continúe automáticamente con la implementación según los criterios de éxito. Cree implementaciones por fases con el valor predeterminado de dos fases o bien configure manualmente varias fases. La implementación por fases de las secuencias de tareas no es compatible con la instalación de medios o PXE. A partir de la versión 1806, se puede crear una implementación por fases para una aplicación.<!--1358147-->  

> [!Tip]
> La característica de implementación por fases se introdujo por primera vez en la versión 1802 como una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). A partir de la versión 1806, ya no es de versión preliminar.<!--1356837-->



## <a name="prerequisites"></a>Requisitos previos

#### <a name="security-scope"></a>Ámbito de seguridad
Las implementaciones creadas por las implementaciones por fases no son visibles para los usuarios administrativos que no tengan el ámbito de seguridad **Todos**. Para obtener más información, consulte [Ámbitos de seguridad](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope).

#### <a name="distribute-application-content"></a>Distribuir contenido de aplicaciones
Antes de crear una implementación por fases para una aplicación, distribuya el contenido a un punto de distribución.<!--518293-->



## <a name="bkmk_settings"></a> Configuración de fase

Estos valores son únicos para las implementaciones por fases. Configure estas opciones al crear o editar las fases para controlar la programación y el comportamiento del proceso de implementación por fases. 


#### <a name="criteria-for-success-of-the-first-phase"></a>Criterios para considerar que la primera fase se ha completado correctamente  

- **Porcentaje de éxito de la implementación**: especifique el porcentaje de dispositivos necesario para completar correctamente la implementación para que la primera fase tenga éxito. De forma predeterminada, este valor es 95 %. En otras palabras, el sitio considera que la primera fase se realiza correctamente si el estado de cumplimiento del 95 % de los dispositivos es **Correcto** para esta implementación. Después, el sitio continúa con la segunda fase y crea una implementación del software a la siguiente colección.  


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>Condiciones para comenzar la segunda fase de implementación una vez que la primera se complete correctamente  

- **Iniciar automáticamente esta fase tras un período de aplazamiento (en días)**: elija el número de días que se esperará antes de comenzar la segunda fase después del éxito de la primera. De forma predeterminada, este valor es un día.  

- **Iniciar manualmente la segunda fase de implementación**: el sitio no iniciará automáticamente la segunda fase después de que la primera fase se realice correctamente. Esta opción requiere que inicie manualmente la segunda fase. Para obtener más información, consulte [Pasar a la siguiente fase](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_move).  

    > [!Note]  
    > Esta opción no está disponible para las implementaciones por fases de las aplicaciones.  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>Poner este software a disposición de los usuarios gradualmente en este período de tiempo (en días)
<!--1358578--> A partir de la versión 1806, configure estas opciones para que el lanzamiento en cada fase sea gradual. Este comportamiento ayuda a mitigar el riesgo de problemas de implementación y disminuye la carga en la red provocada por la distribución de contenido a los clientes. El sitio habilita la disponibilidad del software de forma gradual en función de la configuración de cada fase. Cada cliente de una fase tiene una fecha límite en relación con el tiempo de disponibilidad del software. La ventana de tiempo entre el tiempo disponible y la fecha límite es la misma para todos los clientes de una fase. El valor predeterminado de esta configuración es cero, por lo que de forma predeterminada la implementación no está limitada. No establezca un valor mayor que 30.<!--SCCMDocs-pr issue 2767--> 


#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>Configurar el comportamiento de fecha límite relativo a la disponibilidad del software  

- **La instalación se requiere lo antes posible**: establezca la fecha límite para la instalación en el dispositivo en cuanto el dispositivo se selecciona.  

- **Es necesario instalar después de este período de tiempo**: establezca una fecha límite para la instalación un número determinado de días después de que el dispositivo se establezca como objetivo. De forma predeterminada, este valor es siete días.   


<!--### Examples
Include a timeline diagram
-->



## <a name="bkmk_auto"></a> Crear automáticamente una implementación predeterminada de dos fases

1. Inicie el asistente Crear implementaciones por fases en la consola de Configuration Manager. Esta acción varía según el tipo de software que se va a implementar:  

    - **Aplicación** (solo en la versión 1806 y posteriores): vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione **Aplicaciones**. Seleccione una aplicación existente y después haga clic en **Crear implementación por fases** en la cinta.  

    - **Secuencia de tareas**: vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**. Seleccione una secuencia de tareas existente y después haga clic en **Crear implementación por fases** en la cinta.  

2. En la página **General** asigne un **nombre** y una **descripción** (opcional) a la implementación por fases y seleccione **Crear automáticamente una implementación de dos fases predeterminada**.  

3. Haga clic en **Examinar** y seleccione una colección de destino para los campos **Primera colección** y **Segunda colección**. Para una secuencia de tareas, seleccione en recopilaciones de dispositivos. Para una aplicación, seleccione en colecciones de usuario o dispositivo. Haga clic en **Siguiente**.  

    > [!Important]  
    > El asistente Crear implementación por fases no notifica si una implementación es potencialmente de alto riesgo. Para obtener más información, vea [Settings to manage high-risk deployments (Configuración para administrar implementaciones de alto riesgo)](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments) y la nota cuando [implemente una secuencia de tareas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  

4. En la página **Configuración**, elija una opción para cada una de las opciones de programación. Para obtener más información, vea [Configuración de fase](#bkmk_settings). Haga clic en **Siguiente** cuando haya terminado.  

5. En la página **Fases**, vea las dos fases que crea el asistente para las colecciones especificadas. Haga clic en **Siguiente**.   

    > [!Note]  
    > En esta sección se describe el procedimiento para crear automáticamente una implementación de dos fases predeterminada. El asistente le permite agregar, quitar, reordenar, editar o ver las fases de una implementación por fases. Para obtener más información sobre estas acciones adicionales, vea [Creación de implementaciones por fases para una secuencia de tareas](#bkmk_manual).  

6. Confirme las selecciones en la pestaña **Resumen** y después haga clic en **Siguiente** para completar el asistente.  



## <a name="bkmk_manual"></a> Creación de una implementación por fases con fases configuradas manualmente
<!--1358148--> 

A partir de la versión 1806, puede crear una implementación por fases con fases configuradas manualmente para una secuencia de tareas. Agregue un máximo de diez fases adicionales desde la pestaña **Fases** del asistente Crear una implementación por fases. 

> [!Note]  
> Actualmente no se pueden crear las fases de una aplicación manualmente. El asistente crea automáticamente dos fases para las implementaciones de aplicaciones.


1. En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. Haga clic con el botón derecho en una secuencia de tareas existente y seleccione **Create Phased Deployment** (Crear implementación por fases).  

3. En la pestaña **General** del asistente Crear implementación por fases, asigne un **nombre** y una **descripción** (opcional) a la implementación por fases y seleccione **Configurar manualmente todas las fases**.  

4. En la página **Fases** del asistente Crear implementación por fases, están disponibles las siguientes acciones:  

    - **Filtrar** la lista de fases de implementación. Escriba una cadena de caracteres para una coincidencia de mayúsculas y minúsculas de las columnas Orden, Nombre o Colección. 

    - **Agregar** una nueva fase:  

        1. En la página **General** del Asistente para agregar fase, especifique un **nombre** para la fase y luego busque la **Recopilación de fase** de destino. La configuración adicional en esta página es la misma que cuando se implementa normalmente una secuencia de tareas.  

        2. En la página **Configuración de fase**del Asistente para agregar fase, configure una opción para cada una de las opciones de programación y haga clic en **Siguiente** cuando haya terminado. Para obtener más información, vea [Configuración](#bkmk_settings).   

            > [!Note]  
            > No se puede editar la configuración de fase **Porcentaje de éxito de la implementación** en la primera fase. Esta configuración solo se aplica a las fases que tienen una fase anterior.  

        3. La configuración en las páginas **experiencia del usuario** y **puntos de distribución** del Asistente para agregar fase es la misma que cuando se implementa normalmente una secuencia de tareas.  

        4. Revise la configuración en la página **Resumen** y después complete el Asistente para agregar fase.  

    - **Editar**: una vez que haya agregado una fase, selecciónela y haga clic en este botón para editarla. Esta acción abre la ventana Propiedades de la fase, que tiene las mismas pestañas que las páginas del Asistente para agregar fases.  

    - **Quitar**: seleccione una fase existente y haga clic en este botón para eliminarla.  

       > [!Warning]  
       > No hay ninguna confirmación y no se puede deshacer esta acción.  

    - **Subir** o **Bajar**: el asistente ordena las fases en el orden en que las agrega. La fase agregada más recientemente es la última en la lista. Para cambiar el orden, seleccione una fase y después haga clic en uno de estos botones para mover la ubicación de la fase en la lista.  

       > [!Important]  
       > Revise la configuración de la fase después de cambiar el orden. Asegúrese de que la siguiente configuración sigue siendo coherente con los requisitos para esta implementación por fases:  
       > 
       > - Criterios de éxito de la fase anterior  
       > - Condiciones para comenzar esta fase de implementación una vez que la anterior se complete correctamente   

5. Haga clic en **Siguiente**. Revise la configuración en la página **Resumen** y después complete el asistente Crear implementación por fases.  


Después de crear una implementación por fases, abra sus propiedades para realizar cambios:  

- **Agregar** fases adicionales a una implementación por fases existente.  

- Si una fase no está activa, puede **editarla**, **quitarla** o **moverla** hacia arriba o hacia abajo. No puede moverla antes de una fase activa.  

- Cuando una fase está activa, es de solo lectura. No puede editarla, quitarla o mover su ubicación en la lista. La única opción es **Ver** las propiedades de la fase.  

- Una implementación por fases de aplicación siempre es de solo lectura.  



## <a name="next-steps"></a>Pasos siguientes
[Administración y supervisión de implementaciones por fases](/sccm/osd/deploy-use/manage-monitor-phased-deployments)
