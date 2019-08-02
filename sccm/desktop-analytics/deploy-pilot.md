---
title: Cómo realizar la implementación en Pilot
titleSuffix: Configuration Manager
description: Guía de procedimientos para la implementación en un grupo piloto de análisis de escritorio.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aa7566779fe346ddecfd546dc89dc8618fb39953
ms.sourcegitcommit: ef7800a294e5db5d751921c34f60296c1642fc1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68712655"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Cómo realizar una implementación piloto con el análisis de escritorio

> [!Note]  
> Esta información está relacionada con un servicio de vista previa que se puede modificar sustancialmente antes de que se publique comercialmente. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Una de las ventajas de análisis de escritorio es ayudar a identificar el conjunto más pequeño de dispositivos que proporcionan la mayor cobertura de factores. Se centra en los factores que son más importantes para una prueba piloto de actualizaciones y actualizaciones de Windows. Asegurarse de que el piloto es más satisfactorio le permite moverse con mayor rapidez y confianza a implementaciones amplias en producción.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]


## <a name="identify-devices"></a>Identificar dispositivos

El primer paso es identificar los dispositivos que se van a incluir en el programa piloto. El análisis de escritorio recomienda dispositivos basados en los datos de los informes, y puede incluir o reemplazar dispositivos en esta lista.

1. Vaya al [portal de análisis de escritorio](https://aka.ms/desktopanalytics)y, en el grupo administrar, seleccione planes de **implementación**.

1. Seleccione un plan de implementación.

1. En el grupo preparar del menú plan de implementación, seleccione **identificar piloto**.

Verá los datos de análisis de escritorio que muestran el número de dispositivos que recomienda, incluida la mejor cobertura. Este algoritmo se basa principalmente en el uso de aplicaciones importantes y críticas, y en el alcance de las configuraciones de hardware.

Realice las siguientes acciones para la lista de dispositivos recomendados adicionales:

- **Agregar todo a Pilot**: Agrega todos los dispositivos recomendados al grupo piloto
- **Agregar a piloto**: Agregar solo dispositivos individuales
- **Reemplazar** cualquier dispositivo específico del piloto
- **Recalcular** cuando haya terminado de realizar cambios

También puede tomar decisiones en todo el sistema sobre qué Configuration Manager recopilaciones incluir o excluir de los pilotos. En el menú principal de análisis de escritorio, en el grupo configuración global, seleccione **piloto global**.

### <a name="example"></a>Ejemplo

- La conexión de análisis de escritorio se configura en Configuration Manager para tener como destino la recopilación **todos los sistemas** . Esta acción inscribe todos los clientes en el servicio.
- También se configuran colecciones adicionales para sincronizar con el análisis de escritorio:
    - Todos los clientes de Windows 10
    - Todos los dispositivos de ti
    - Office CEO
- En la configuración de la **prueba piloto global** , se incluyen todas las recopilaciones de **dispositivos de ti** . Excluya la colección de **Office CEO** .
- Cree un plan de implementación y seleccione **todos los clientes de Windows 10** recopilación como **grupo de destino**.
- La lista de **dispositivos piloto incluidos** contiene el subconjunto de dispositivos del **grupo de destino**: **Todos los clientes de Windows 10** que también están en la lista de *inclusión* del piloto global: **Todos los dispositivos de ti**  
- Las listas de **dispositivos recomendados adicionales** contienen un conjunto de dispositivos del **grupo de destino** que proporcionan la máxima cobertura y redundancia para los recursos importantes.  El análisis de escritorio excluye de esta lista todos los dispositivos de la lista de *exclusión* del piloto global: **Office CEO**


## <a name="address-issues"></a>Solucionar problemas

Use el portal de análisis de escritorio para revisar los problemas detectados con los recursos que podrían bloquear la implementación. A continuación, apruebe, rechace o modifique la corrección sugerida. Todos los elementos deben estar marcados como **listos** o **listos (con corrección)** antes de que se inicie la implementación piloto.

1. Vaya al [portal de análisis de escritorio](https://aka.ms/desktopanalytics)y, en el grupo administrar, seleccione planes de **implementación**.  

2. Seleccione un plan de implementación.  

3. En el grupo preparar del menú plan de implementación, seleccione **preparar piloto**.  

4. En la pestaña **aplicaciones** , revise las aplicaciones que necesitan su entrada.  

5. En cada aplicación, seleccione el nombre de la aplicación. En el panel de información, revise la recomendación y seleccione la decisión de actualización. Si elige **no revisado** o **no es posible**, el análisis de escritorio no incluye los dispositivos con esta aplicación en la implementación piloto. Si elige **listo (con corrección)** , use las notas de **corrección** para capturar las acciones que se deben llevar a cabo para resolver un problema, como reinstalar o *Buscar la versión recomendada del fabricante*.

6. Repita esta revisión para otros activos.  


## <a name="create-software"></a>Crear software

Antes de implementar Windows, primero debe crear los objetos de software en Configuration Manager. Para obtener más información, consulte [secuencia de tareas de actualización en contexto de Windows 10](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).


## <a name="deploy-to-pilot-devices"></a>Implementación en dispositivos piloto

Configuration Manager usa los datos de análisis de escritorio para crear recopilaciones para las implementaciones piloto y de producción. Para asegurarse de que los dispositivos están en buen estado después de cada fase de implementación, use el procedimiento siguiente para crear una implementación por fases integrada en análisis de escritorio:

1. En la consola de Configuration Manager, vaya a la **biblioteca de software**, expanda servicios de análisis de **escritorio**y seleccione el nodo planes de **implementación** .  

2. Seleccione el plan de implementación y, a continuación, seleccione **detalles del plan de implementación** en la cinta de opciones.  

3. Seleccione **crear implementación por fases** en la cinta de opciones. Esta acción inicia el Asistente para crear una implementación por fases.

    > [!Tip]  
    > Si desea crear una implementación de secuencia de tareas clásica solo para la colección piloto, seleccione **implementar** en el icono Estado de la **fase piloto** . Esta acción inicia el Asistente para implementar software. Para obtener más información, vea [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence).  

4. Escriba un nombre para la implementación y seleccione la secuencia de tareas que se va a usar. Use la opción para **crear automáticamente una implementación de dos fases predeterminada**y, a continuación, configure las siguientes recopilaciones:  

    - **Primera recopilación**: Busque y seleccione la colección **piloto** de este plan de implementación. La Convención de nomenclatura estándar para esta colección `<deployment plan name> (Pilot)`es.

    - **Segunda colección**: Busque y seleccione la recopilación de **producción** de este plan de implementación. La Convención de nomenclatura estándar para esta colección `<deployment plan name> (Production)`es.

    > [!Note]  
    > Con la integración de análisis de escritorio, Configuration Manager crea automáticamente colecciones piloto y de producción para el plan de implementación. Antes de poder usarlas, puede tardar tiempo en sincronizarse estas colecciones. Para obtener más información, consulte [solución de problemas: latencia de datos](/sccm/desktop-analytics/troubleshooting#data-latency).<!-- 4984639 -->
    >
    > Estas colecciones están reservadas para los dispositivos del plan de implementación de análisis de escritorio. No se admiten cambios manuales en estas colecciones.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Complete el Asistente para configurar la implementación por fases. Para más información, vea [Crear implementaciones por fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).

    > [!Note]  
    > Utilice la configuración predeterminada para **iniciar automáticamente esta fase después de un período de aplazamiento (en días)** . Se deben cumplir los siguientes criterios para que se inicie la segunda fase:
    >
    > 1. La primera fase alcanza los criterios del **porcentaje de éxito** de la implementación correcta. Esta opción se configura en la implementación por fases.
    > 1. Debe revisar y tomar decisiones de actualización en el análisis de escritorio para marcar los recursos importantes y críticos como *listos*. Para obtener más información, consulte [revisar los activos que necesitan una decisión de actualización](/sccm/desktop-analytics/deploy-prod#bkmk_review).
    > 1. Análisis de escritorio se sincroniza con las colecciones de Configuration Manager los dispositivos de producción que cumplen los criterios *preparados* .

> [!Important]  
> Estas colecciones continúan sincronizando a medida que cambian sus pertenencias. Por ejemplo, si identifica un problema con un recurso y lo marca como **no posible**, los dispositivos con ese recurso dejarán de cumplir los criterios *listos* . Estos dispositivos se quitan de la colección de implementación de producción.


## <a name="monitor"></a>Supervisión

### <a name="configuration-manager-console"></a>Consola de Configuration Manager

Abra el plan de implementación. En el icono **preparando decisiones de actualización-estado general** se proporciona un resumen del estado del plan de implementación. Este estado es para las colecciones piloto y de producción. Los dispositivos pueden estar en una de las siguientes categorías:

- **Actualizado**: Los dispositivos se han actualizado a la versión de Windows de destino para este plan de implementación

- **Decisión de actualización completada**: Uno de los siguientes Estados:
    - Dispositivos con recursos destacados que están **listos** o **preparados con corrección**
    - El estado del dispositivo es **bloqueado**, [**reemplazar dispositivo**](/sccm/desktop-analytics/about-deployment-plans#plan-assets) o reinstalar **dispositivo**

- **No revisado**: Dispositivos con recursos destacados **no** revisados o **revisión en curso**

El estado del dispositivo se actualiza en los iconos estado de la **fase piloto** y **Estado de producción** con las siguientes acciones:

- Realiza cambios en la evaluación de compatibilidad
- Los dispositivos se actualizan a la versión de destino de Windows
- La implementación progresa

También puede usar la supervisión de la implementación de Configuration Manager igual que cualquier otra implementación de la secuencia de tareas. Para obtener más información, consulte [supervisar implementaciones del sistema operativo](/sccm/osd/deploy-use/monitor-operating-system-deployments).


### <a name="desktop-analytics-portal"></a>Portal de análisis de escritorio

Use el [portal de análisis de escritorio](https://aka.ms/desktopanalytics) para ver el estado de cualquier plan de implementación. Seleccione el plan de implementación y, a continuación, seleccione **información general del plan**.

![Captura de pantalla de información general del plan de implementación en análisis de escritorio](media/deployment-plan-overview.png)

Seleccione el icono **piloto** . Resume el estado actual de la implementación piloto. Este icono también muestra los datos para el número de dispositivos no iniciados, en curso, completado o que devuelven problemas.

Los dispositivos que notifican errores u otros problemas también se enumeran en el área de detalles de la prueba piloto de la derecha. Para obtener detalles del problema detectado, seleccione **revisar**. Esta acción cambia la vista a la página **Estado de implementación** .

En la página **Estado de implementación** se muestran los dispositivos en las siguientes categorías:

- No iniciado
- En curso
- Completado
- Requiere atención: dispositivos
- Requiere atención: problemas

Las categorías **necesidades de atención** muestran la misma información, pero se ordenan de manera diferente.

Seleccione una lista concreta en cualquiera de las vistas para obtener más detalles sobre el problema detectado.

A medida que se solucionan estos problemas de implementación, el panel continúa mostrando el progreso de los dispositivos. Se actualiza a medida que los dispositivos pasan dela **atención necesaria** a la finalización.


## <a name="next-steps"></a>Pasos siguientes

Permita que el piloto se ejecute durante un tiempo para recopilar datos operativos. Anime a los usuarios de dispositivos piloto a probar aplicaciones.

Cuando la implementación piloto cumpla los criterios de éxito, vaya al siguiente artículo para implementar en producción.
> [!div class="nextstepaction"]  
> [Implementación en producción](/sccm/desktop-analytics/deploy-prod)  
