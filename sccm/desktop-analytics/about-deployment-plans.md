---
title: Planes de implementación en análisis de escritorio
titleSuffix: Configuration Manager
description: Obtenga información sobre los planes de implementación de análisis de escritorio.
ms.date: 08/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 65dff1dbf8e8154bc2d481e274dd47d352aa9d6e
ms.sourcegitcommit: fe8934487158ed3bd15c7a6a456c3cafe58aed64
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2019
ms.locfileid: "68995392"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Acerca de los planes de implementación en el análisis de escritorio

> [!Note]  
> Esta información está relacionada con un servicio de vista previa que se puede modificar sustancialmente antes de que se publique comercialmente. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Análisis de escritorio recopila y analiza los datos de dispositivos, aplicaciones y controladores de la organización. En función de este análisis y de la entrada, puede usar el servicio para crear planes de implementación para Windows 10. Los planes de implementación tienen las siguientes características:  

- Recomendar automáticamente los dispositivos que se van a incluir en los pilotos  

- Identificar problemas de compatibilidad y sugerir mitigaciones  

- Evaluar el estado de la implementación antes, durante y después de las actualizaciones  

- Seguimiento del progreso de la implementación  

Como parte del plan de implementación, realice las siguientes acciones:  

- Definir qué versiones de Windows 10 desea implementar  

- Elegir los grupos de dispositivos en los que se va a implementar  

- Crear reglas de preparación para la implementación  

- Definir la importancia de las aplicaciones  

- Elección de dispositivos piloto basados en recomendaciones automáticas  

- Decidir cómo corregir problemas con aplicaciones basadas en recomendaciones de análisis de escritorio  

De forma predeterminada, Desktop Analytics actualiza los datos del plan de implementación diariamente. Los cambios que realice en un plan de implementación, como la asignación de importancia a una aplicación o la elección de un dispositivo para incluirlo en una prueba piloto, tardan hasta 24 horas en procesarse. Para acelerar este proceso, solicite una actualización de datos a petición. Para obtener más información, consulte [p + f de análisis de escritorio](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

Después de conectar el análisis de escritorio a Configuration Manager, seleccione sus colecciones en los planes de implementación. Esta integración le permite implementar Windows en una recopilación basada en los datos de análisis de escritorio.



## <a name="readiness-rules"></a>Reglas de preparación

Las siguientes reglas de preparación están disponibles en los planes de implementación:

- Si los dispositivos reciben controladores automáticamente desde Windows Update. Si los dispositivos reciben las actualizaciones de controladores de Windows Update, los problemas de controladores identificados como parte de la evaluación de disponibilidad se marcan automáticamente como **listos**.  

- Umbral de recuento de instalaciones bajas para las aplicaciones de Windows. Si una aplicación se instala en un porcentaje mayor de equipos que este umbral, el plan de implementación marca la aplicación como **digno**de interés. Esta etiqueta significa que puede decidir la importancia de la prueba de la aplicación durante la fase piloto.  


## <a name="plan-assets"></a>Planear recursos

<!-- 4670224 -->

Aunque el área [activos](/sccm/desktop-analytics/about-assets) también muestra dispositivos y aplicaciones, el área **activos del plan** en un plan de implementación específico incluye información adicional.

### <a name="devices"></a>Dispositivos

Consulte la **decisión de actualización de Windows** para cada dispositivo en el plan de implementación.

La decisión de actualización de Windows para **reemplazar el dispositivo** puede deberse a uno de los siguientes motivos:

- No se pudo realizar una comprobación del procesador necesaria para Windows 10. Para obtener más información, consulte [requisitos mínimos de hardware](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor).
- Tiene un bloque de BIOS
- No tiene suficiente memoria
- Un componente crítico para el arranque en el sistema tiene un controlador bloqueado
- La marca y el modelo específicos no pueden actualizarse
- Hay un componente de clase de pantalla con un bloque de controladores que tiene todos los atributos siguientes:
    - No invalide
    - No hay ningún controlador en la nueva versión del sistema operativo
    - Todavía no está en Windows Update
- Hay otro componente plug-and-Play en el sistema que bloquea la actualización
- Hay un componente inalámbrico que usa un controlador emulado de XP
- Un componente de red con una conexión activa perderá su controlador. En otras palabras, después de la actualización, podría perder la conectividad de red.

### <a name="apps"></a>Aplicaciones

Establezca la **decisión de actualización** y la **importancia** de esta aplicación en este plan de implementación. Para obtener más información, vea [Cómo crear planes de implementación](/sccm/desktop-analytics/create-deployment-plans).

En los detalles de la aplicación, también puede ver la siguiente información: Recomendaciones, factores de riesgo de compatibilidad y problemas conocidos de Microsoft. Use esta información para ayudar a establecer la **decisión de actualización**. Para obtener más información, vea [evaluación de compatibilidad](/sccm/desktop-analytics/compat-assessment).

Las aplicaciones que análisis de escritorio muestran como *destacadas* se basan en el umbral de recuento de instalaciones bajas para las reglas de preparación del plan de implementación. Para obtener más información, consulte [reglas de preparación](/sccm/desktop-analytics/create-deployment-plans#readiness-rules).

   > [!Tip]
   > Para obtener más información sobre la categoría de aplicación "no importante", consulte [decisión de actualización automática de aplicaciones del sistema y de la tienda](/sccm/desktop-analytics/about-assets#bkmk_plan-autoapp). <!-- 3587232 -->


### <a name="drivers"></a>Controladores

Consulte la lista de controladores que se incluyen en este plan de implementación. Establezca la **decisión de actualización**, revise la recomendación de Microsoft y vea los factores de riesgo de compatibilidad.


## <a name="importance"></a>Importance

Como parte del plan de implementación, establezca la *importancia* de las aplicaciones. Análisis de escritorio detecta estas aplicaciones tal como están instaladas en los dispositivos de destino. Esta configuración ayuda a análisis de escritorio a determinar qué dispositivos incluye en la fase piloto de la implementación.

Si una aplicación está instalada en menos del 2% de los dispositivos de destino, se marca como **número de instalaciones bajas**. Dos por ciento es el valor predeterminado. Puede ajustar el umbral en la configuración de preparación de 0% a 10%. Análisis de escritorio marca automáticamente estas aplicaciones como **listas para su actualización**.  

En el caso de las aplicaciones, elija una importancia **crítica**, **importante**o **no importante**. Si marca uno como crítico o importante, el análisis de escritorio incluye en la implementación piloto algunos dispositivos con esa aplicación. El servicio incluye en el piloto más instancias de una aplicación crítica. Si marca una aplicación como no importante, el análisis de escritorio lo establece automáticamente en **listo para actualizar**.



## <a name="pilot-devices"></a>Dispositivos piloto

El análisis de escritorio combina su información de importancia con la configuración de la prueba piloto global. A continuación, crea una recomendación para la que los dispositivos deben formar parte de la implementación piloto. La implementación piloto recomendada incluye dispositivos con diferentes configuraciones de hardware y una o más instancias de todas las aplicaciones críticas e importantes. Si una aplicación está marcada como crítica, el servicio recomienda más dispositivos con esa aplicación en el piloto.



## <a name="deployment-plans-in-configuration-manager"></a>Planes de implementación en Configuration Manager

Después de crear un plan de implementación, utilice Configuration Manager para implementar los productos. Una vez que se inicia la implementación, el análisis de escritorio supervisa la implementación en función de la configuración del plan.


## <a name="next-steps"></a>Pasos siguientes

- [Más información sobre los activos de análisis de escritorio](/sccm/desktop-analytics/about-assets): dispositivos, controladores y aplicaciones  

- [Más información sobre la seguridad y las actualizaciones de características](/sccm/desktop-analytics/about-updates)  

- [Crear un plan de implementación](/sccm/desktop-analytics/create-deployment-plans)  
