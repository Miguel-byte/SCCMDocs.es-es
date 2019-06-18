---
title: Implementación piloto
titleSuffix: Configuration Manager
description: Guía de procedimientos para implementar en un grupo piloto de análisis de escritorio.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5ee3d2c35424820658f91628b5f6e23be41498b2
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159132"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Implementación piloto con análisis de escritorio

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Una de las ventajas del análisis de escritorio es ayudar a identificar el conjunto más pequeño de dispositivos que proporcionan la cobertura más amplia de factores. Se centra en los factores que son más importantes para una prueba piloto de actualizaciones de Windows. Asegurándose de que tiene más éxito del piloto le permite mover más rápidamente y con confianza a las implementaciones amplias en producción.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]


## <a name="identify-devices"></a>Identificar los dispositivos

El primer paso es identificar los dispositivos que desea incluir en la prueba piloto. Análisis de escritorio recomienda dispositivos basándose en los datos del informe, y puede incluir o reemplazar los dispositivos de esta lista.

1. Vaya a la [portal de análisis de escritorio](https://aka.ms/desktopanalytics)y en la selección de grupo administrar **planes de implementación**.

1. Seleccione un plan de implementación.

1. En el grupo de preparación del menú del plan de implementación, seleccione **identificar piloto**.

Verá los datos de análisis de escritorio que muestra el número de dispositivos, que recomienda incluir la cobertura mejor. Este algoritmo se basa principalmente en el uso de las aplicaciones importantes y esenciales y la amplitud de las configuraciones de hardware.

Realizar las siguientes acciones para obtener la lista de dispositivos recomendadas adicionales:

- **Agregar todo al piloto**: Agrega todos los dispositivos recomendados para el grupo piloto
- **Agregar proyecto piloto**: Agregar solo los dispositivos individuales
- **Reemplace** cualquier dispositivos específicos de la prueba piloto
- **Recalcular** cuando haya terminado de realizar los cambios

También puede tomar decisiones de todo el sistema acerca de las colecciones de Configuration Manager para incluir o excluir de pilotos. En el menú principal de análisis de escritorio, en el grupo de configuración Global, seleccione **piloto Global**.

### <a name="example"></a>Ejemplo

- Configurar la conexión de escritorio Analytics en Configuration Manager al destino la **todos los sistemas** colección. Esta acción inscribe a todos los clientes del servicio.
- También configurar colecciones adicionales para sincronizarse con análisis de escritorio:
    - Todos los clientes de Windows 10
    - Todos los dispositivos de TI
    - Oficina del director ejecutivo
- En el **piloto Global** configuración, incluye el **dispositivos informáticos todas** colecciones. Excluir la **office CEO** colección.
- Crear un plan de implementación y seleccione **todo Windows 10 clientes** colección como su **grupo de destino**.
- El **piloto dispositivos incluidos** lista contiene el subconjunto de los dispositivos en su **grupo de destino**: **Todos los clientes de Windows 10** que también están en el proyecto piloto Global *inclusión* lista: **Todos los dispositivos de TI**  
- El **dispositivos adicionales recomienda** listas contiene un conjunto de dispositivos de su **grupo de destino** que proporcionan la máxima cobertura y redundancia para los recursos importantes.  Análisis de escritorio excluyen de esta lista los dispositivos en la prueba piloto global *exclusión* lista: **Oficina del director ejecutivo**


## <a name="address-issues"></a>Solucionar problemas

Use el portal de análisis de escritorio para revisar cualquier problema notificado a los recursos que podrían bloquear la implementación. A continuación, aprobar, rechazar o modificar la corrección sugerida. Todos los elementos se deben marcar **listo** o **listo (con la corrección)** antes de que comience la implementación piloto.

1. Vaya a la [portal de análisis de escritorio](https://aka.ms/desktopanalytics)y en la selección de grupo administrar **planes de implementación**.  

2. Seleccione un plan de implementación.  

3. En el grupo de preparación del menú del plan de implementación, seleccione **preparación piloto**.  

4. En el **aplicaciones** pestaña, revise las aplicaciones que necesitan sus comentarios.  

5. Para cada aplicación, seleccione el nombre de la aplicación. En el panel de información, revise la recomendación y seleccione la decisión de actualización. Si elige **no revisado** o **no se puede**, a continuación, análisis de escritorio no incluye los dispositivos con esta aplicación en la implementación piloto. Si elige **listo (con la corrección)** , utilice el **notas de la corrección** para capturar las acciones que realizar para solucionar un problema, como *reinstalar* o *encontrar el versión recomendada del fabricante*.

6. Repita esta revisión para otros activos.  


## <a name="create-software"></a>Creación de software

Antes de poder implementar Windows, crear los objetos de software en Configuration Manager. Para obtener más información, consulte [secuencia de tareas de actualización en contexto de Windows 10](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).


## <a name="deploy-to-pilot-devices"></a>Implementar en dispositivos pilotos

Configuration Manager usa los datos de análisis de escritorio para crear colecciones para las implementaciones piloto y de producción. Para asegurarse de que los dispositivos están en buen Estados después de cada fase de implementación, use el procedimiento siguiente para crear una implementación por fases integrado de análisis de escritorio:

1. En la consola de Configuration Manager, vaya a la **biblioteca de Software**, expanda **Desktop Analytics mantenimiento**y seleccione el **planes de implementación** nodo.  

2. Seleccione el plan de implementación y, a continuación, seleccione **detalles del Plan de implementación** en la cinta de opciones.  

3. Seleccione **Crear implementación por fases** en la cinta de opciones. Esta acción inicia al Asistente para crear implementación por fases.

    > [!Tip]  
    > Seleccione si desea crear una implementación de secuencia de tareas clásica para la colección de piloto, **implementar** en el **piloto estado** icono. Esta acción inicia al Asistente para implementar Software. Para obtener más información, vea [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence).  

4. Escriba un nombre para la implementación y seleccione la secuencia de tareas para usar. Utilice la opción de **crear automáticamente una implementación predeterminada de la fase dos**y, a continuación, configure las siguientes colecciones:  

    - **Primera colección**: Busque y seleccione el **piloto** colección para este plan de implementación. La convención de nomenclatura estándar para esta colección es `<deployment plan name> (Pilot)`.

    - **Segunda colección**: Busque y seleccione el **producción** colección para este plan de implementación. La convención de nomenclatura estándar para esta colección es `<deployment plan name> (Production)`.

    > [!Note]  
    > Con la integración de análisis de escritorio, Configuration Manager crea automáticamente las recopilaciones de piloto y de producción para el plan de implementación. Puede tardar hasta 10 minutos para estas colecciones sincronizar antes de usarlos.<!-- 3887891 -->
    >
    > Estas colecciones están reservadas para los dispositivos de plan de implementación de escritorio Analytics. No se admiten cambios manuales en estas colecciones.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Complete el Asistente para configurar la implementación por fases. Para más información, vea [Crear implementaciones por fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).

    > [!Note]  
    > Usar la configuración predeterminada para **iniciar automáticamente esta fase tras un período de aplazamiento (en días)** . Para que la segunda fase de inicio, se deben cumplir los siguientes criterios:
    >
    > 1. La primera fase alcanza el **porcentaje de éxito de implementación** criterios de éxito. Esta configuración en la implementación por fases.
    > 1. Debe revisar y tomar decisiones de actualización en el escritorio de análisis para marcar recursos importantes y esenciales como *listo*. Para obtener más información, consulte [revisar los recursos que necesitan una decisión de actualización](/sccm/desktop-analytics/deploy-prod#bkmk_review).
    > 1. Análisis de escritorio sincroniza a las colecciones de Configuration Manager los dispositivos de producción que cumplen el *listo* criterios.

> [!Important]  
> Estas colecciones continuarán con la sincronización como sus cambios de pertenencia. Por ejemplo, si identifica un problema con un recurso y márquelo como **no se puede**, los dispositivos con ese recurso ya no cumplen la *listo* criterios. Estos dispositivos se quitan de la colección de la implementación de producción.


## <a name="monitor"></a>Monitor

### <a name="configuration-manager-console"></a>Consola de Configuration Manager

Abra el plan de implementación. El **decisión de actualizar preparación - estado general** icono proporciona un resumen del estado del plan de implementación. Este estado es para colecciones de la prueba y de producción. Los dispositivos pueden pertenecer a una de las siguientes categorías:

- **Al día**: Los dispositivos se han actualizado a la versión de Windows de destino para este plan de implementación

- **Completa de la decisión de actualización**: Uno de los siguientes estados:
    - Los dispositivos a los recursos importantes que son **listo** o **preparado con la corrección**
    - El estado del dispositivo es **bloqueado**, [ **dispositivo reemplazar** ](/sccm/desktop-analytics/about-deployment-plans#plan-assets) o **volver a instalar el dispositivo**

- **No se ha revisado**: Dispositivos con activos notables **no revisado** o **revisión en curso**

Actualiza el estado del dispositivo en el **piloto estado** y **el estado de producción** iconos con las siguientes acciones:

- Realizar cambios en la evaluación de compatibilidad
- Los dispositivos se actualizan a la versión de destino de Windows
- La que progresa de implementación

También puede usar el mismo que cualquier otra implementación de secuencia de tareas de supervisión de implementación de Configuration Manager. Para obtener más información, consulte [las implementaciones de SO Monitor](/sccm/osd/deploy-use/monitor-operating-system-deployments).


### <a name="desktop-analytics-portal"></a>Portal de análisis de escritorio

Use la [portal de análisis de escritorio](https://aka.ms/desktopanalytics) para ver el estado de cualquier plan de implementación. Seleccione el plan de implementación y, a continuación, seleccione **Introducción a los planes**.

![Captura de pantalla de información general del plan de implementación en escritorio Analytics](media/deployment-plan-overview.png)

Seleccione el **piloto** icono. Resume el estado actual de la implementación piloto. Este icono también muestra los datos para el número de dispositivos no iniciados, en curso, completado, o al devolver los problemas.

También se enumeran los dispositivos que informan de errores u otros problemas en el área de detalles de la prueba piloto a la derecha. Para obtener detalles del problema notificado, seleccione **revisión**. Esta acción cambia la vista a la **estado de implementación** página

El **estado de implementación** página enumera los dispositivos en las siguientes categorías:

- No iniciado
- En curso
- Completado
- Necesita atención: los dispositivos
- Necesita atención - problemas

El **necesita atención** categorías muestran la misma información, pero ordenados de manera diferente.

Seleccione una lista específica en cualquiera de las vistas para obtener más detalles sobre el problema detectado.

Medida que se abordan estos problemas de implementación, el panel seguirá mostrando el progreso de los dispositivos. Actualiza como mover dispositivos de **necesita atención** a **completado**.


## <a name="next-steps"></a>Pasos siguientes

Permiten la ejecución piloto durante un tiempo recopilar datos operativos. Anime a los usuarios de dispositivos pilotos para probar aplicaciones.

Cuando la implementación piloto cumple los criterios de éxito, vaya al siguiente artículo para implementar en producción.
> [!div class="nextstepaction"]  
> [Implementar en producción](/sccm/desktop-analytics/deploy-prod)  
