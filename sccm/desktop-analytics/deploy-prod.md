---
title: Cómo se implementa en producción
titleSuffix: Configuration Manager
description: Guía de procedimientos para implementar en un grupo de producción de análisis de escritorio.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 599da20674c581501d69333f85ad0e91ee158da2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755561"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Cómo se implementa en producción con análisis de escritorio

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Cuando se haya [implementado piloto](/sccm/desktop-analytics/deploy-pilot) y revisar el estado de sus activos, está listo para actualizar el resto de su entorno de producción. 

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]


Hay tres partes principales para llevar a cabo la implementación de las actualizaciones de dispositivos de producción:

1. [Revise los recursos que necesitan una decisión de actualización](#bkmk_review): Para que los dispositivos esté listo para la implementación de producción, sus activos (aplicaciones, aplicaciones de Office, complementos de Office y las macros de Office) deben tener establecida en su decisión de actualización **listo** o **listo, las correcciones necesarias**.  

2. [Implementar en dispositivos que están preparados](#bkmk_deploy): Use el Administrador de configuración para actualizar los dispositivos que están listos. Análisis de escritorio proporciona la lista de dispositivos listos para la implementación de producción e informes para supervisar el éxito de la implementación.  

3. [Supervisar el estado de dispositivos actualizados](#bkmk_monitor): Medida que avanza a la implementación de actualización, supervise el estado de los recursos importantes. Si algunos necesitan atención, solucionar y corregir esos problemas. Si decide no se puede corregir los problemas, detener la implementación en los dispositivos afectados estableciendo su decisión de actualizar **no se puede**.  

> [!NOTE]  
> Cuando esté seguro en el éxito de la implementación piloto, iniciar la implementación de producción en cualquier momento. No hay ningún requisito que todos los dispositivos pilotos alcanzar el estado "completado" en primer lugar.  



## <a name="bkmk_review"></a> Revise los recursos que necesitan una decisión de actualización

Escritorio Analytics le guía a través del proceso de revisión de los recursos para la implementación de producción. En el portal de Azure, vaya a **planes de implementación**, seleccione un plan de implementación y, a continuación, seleccione **preparar producción** en el menú izquierdo.

![Vista de captura de pantalla de preparación de producción en análisis de escritorio](media/prepare-production.png)

Revise el estado de las aplicaciones, aplicaciones de Office, complementos de Office y las macros de Office. Usar esa información para establecer la decisión de actualización para cada uno de esos recursos.

Utilizar cada una de las pestañas para revisar el estado de las aplicaciones, aplicaciones de Office, complementos de Office y las macros de Office. En cada vista con pestañas, puede filtrar los resultados para mostrar los dispositivos que están en camino para la actualización, necesitan su atención, los dispositivos con resultados mixtos y los dispositivos en un estado indeterminado.

El **Macros de Office** vista muestra avisos relacionados con los archivos habilitado para macros. No muestra los archivos reales habilitado para macros. Seleccione un aviso específico para ver detalles adicionales. <!-- You can also export this list for later use, such as to run the Readiness Toolkit on this subgroup for still more detail about reported issues like the names of the files for which the advisories were raised. -->

Seleccione **metas reunión** para filtrar la vista a los recursos que están listas para la probabilidad para la implementación de producción según los criterios siguientes:

- Riesgo: una evaluación previas a la actualización de los riesgos conocidos para actualizar los dispositivos que tienen este activo instalado  

- Estado de mantenimiento: una evaluación posteriores a la actualización de los dispositivos en otras implementaciones y si ha tenido problemas después de instala la actualización. Para obtener más información sobre el estado, consulte [supervisar el estado de dispositivos actualizados](#montor-the-health-of-updated-devices).  

Para aprobar un recurso para la actualización, seleccione el nombre de la lista y, a continuación, seleccione una de las siguientes opciones de la **decisión de actualización** lista:
- Revisión en curso
- Listo
- Listo (con la corrección)
- No se puede
- No se ha revisado

Para establecer este valor para varias aplicaciones a la vez, utilice la primera columna para **seleccionar este elemento**y, a continuación, elija **establecer decisión de actualizar**. 

![Establecer la opción de decisión de actualización en varias aplicaciones](media/prep-prod-set-upgrade-decision.png)

Seleccione **ningún dato** para ver los activos que no se pudieron clasificar. Por lo general, estos activos son los activos que no tienen suficiente cobertura para el análisis de escritorio realizar un análisis del estado de salud o riesgo. Para mejorar la cobertura, agregar dispositivos adicionales con estos activos del proyecto piloto o pedir a los usuarios pilotos para probar estos activos.

También podría haber recursos en el **atención necesitado** o **resultados mixtos** estado. Estos recursos pueden requerir revisión adicional antes de tomar una decisión de actualización para ellos. 

Revise todos los complementos de Office, aplicaciones de Office y aplicaciones. Una vez que un dispositivo determinado tiene una decisión de actualización positiva para todos los activos, a continuación, su estado cambia a "listo para producción". Ver el recuento actual en la página principal para el plan de implementación seleccionando el tercer paso de implementación, **implementar**.



## <a name="bkmk_deploy"></a> Implementar en dispositivos que están preparados

Configuration Manager usa los datos de análisis de escritorio para crear una colección para la implementación de producción. No implemente la secuencia de aplicación o tarea mediante una implementación tradicional. Utilice el procedimiento siguiente para crear una implementación integrada de análisis de escritorio:

1. En la consola de Configuration Manager, vaya a la **biblioteca de Software**, expanda **Desktop Analytics mantenimiento**y seleccione el **planes de implementación** nodo.  

2. Seleccione el plan de implementación y, a continuación, seleccione **detalles del Plan de implementación** en la cinta de opciones.  

3. En el **el estado de producción** icono, elija uno de los siguientes tipos de objeto en la lista desplegable:  

    - **Aplicación** para Office 365 ProPlus  

    - **Secuencia de tareas** para Windows 10  
  
   Seleccione **implementar**. Esta acción inicia al Asistente para implementar Software para el tipo de objeto seleccionado. 


Vea los siguientes artículos para más información:  

- [Implementar una aplicación](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy)  

- [Implementación de una secuencia de tareas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)  


Si el plan de implementación es para Windows 10 y Office 365, repita este proceso para crear una segunda implementación. Por ejemplo, si es la primera implementación para la secuencia de tareas, cree una segunda implementación para la aplicación.


### <a name="address-deployment-alerts"></a>Alerta de implementación de dirección

Como con la implementación piloto, análisis de escritorio le advierte de los problemas que requieran su atención durante la implementación de producción. En el escritorio de análisis, vaya al plan de implementación y seleccione **estado de implementación** en el menú izquierdo. La vista de estado de implementación enumera los dispositivos en las siguientes categorías:  

- No iniciado
- En curso
- Completado
- Necesita atención - dispositivos (ordenados por nombre de dispositivo)
- Necesita atención - problemas (ordenados por tipo de problema)

![Producción de captura de pantalla de escritorio Analytics estado de implementación](media/prod-deployment-status.png)



## <a name="bkmk_monitor"></a> Supervisar el estado de dispositivos actualizados

El **preparar producción** página se centra en ayudar a realizar decisiones de los recursos de actualización. Esa página de forma predeterminada muestra sólo los activos que no están aún en la **listo** estado. El **supervisar el estado** página muestra los problemas de mantenimiento en cualquier recurso de interés, incluidos los activos que están marcados **listo**. Si detecta problemas, solución de problemas y corregir el problema o cambiar la decisión de actualización **no se puede**. Cuando se cambia la decisión de actualización, esta acción evita que las actualizaciones futuras en dispositivos con ese recurso.

Filtrar esta página por los recursos con los siguientes estados de mantenimiento:

| Filtro de estado de mantenimiento | Descripción |
|----------------------|-------------|
| **Atención necesitado** | (Filtro de forma predeterminada) Escritorio Analytics detecta una regresión estadísticamente significativa a alguna métrica de mantenimiento para ese activo
| **Objetivos de reunión** | Escritorio Analytics no detecta ninguna regresión de comportamiento |
| **Datos insuficientes** | Análisis de escritorio no tienen suficientes datos acerca de este recurso para hacer recomendaciones |
| **No hay datos** | No hay datos de uso todavía está disponible para este recurso | 

Para mostrar una vista sin filtrar de todos los recursos, seleccione el filtro actual. Esta acción quita el filtro.

> [!NOTE]  
> Para reducir el número de activos con datos insuficientes, escritorio Analytics supervisa los recursos en todos los dispositivos que se han actualizado a la versión de Office especificado en el plan de implementación o el destino de Windows. Estos dispositivos incluyen no están incluidos en el plan de implementación específicos.  

El criterio de ordenación predeterminado es el número de dispositivos que han tenido un incidente con ese recurso específico, por lo que puede ver rápidamente las que causan la mayoría de los problemas. Por ejemplo, cuando se visualizan **aplicaciones**, ordena por **dispositivos con la aplicación se bloquea últimas dos semanas**.

Si desea observar el estado de todos los activos, incluidos los activos con suficientes datos para análisis de escritorio realizar inferencias estadísticas, utilice el siguiente proceso:

1. Seleccione la lista desplegable en el **dispositivos con los incidentes en las últimas dos semanas** columna. Agregar un filtro a sólo los activos que han tenido incidentes en un número mínimo de dispositivos para ser interesante. Por ejemplo, mostrar los elementos con valores **mayor** 100.  

2. Seleccione la lista desplegable en el **% dispositivos con los incidentes en las últimas dos semanas** columna y seleccione esta opción para ordenar por **descendente**.  

    La vista resultante muestra los activos con la tarifa más alta del incidente en un número mínimo de incidentes.  

3. Seleccione el recurso para obtener más detalles o cambiar su decisión de actualización.  


Para obtener más información, consulte [supervisión de estado de mantenimiento](/sccm/desktop-analytics/health-status-monitoring).
