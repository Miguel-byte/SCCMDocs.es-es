---
title: Supervisión del estado de mantenimiento
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo funciona la supervisión de estado de mantenimiento en el análisis de escritorio.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 834b7d30aa5331ae73125e1cdfc3c9c7095d58b7
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62255219"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Estado de mantenimiento de supervisión de análisis de escritorio

Como se [implementa una actualización en producción](/sccm/desktop-analytics/deploy-prod), usar análisis de escritorio para ayudar a supervisar el estado de mantenimiento de los dispositivos. En este artículo se explica en detalle cómo funciona la supervisión de estado.

Para obtener más información sobre cómo usar esta característica, consulte [supervisar el estado de dispositivos actualizados](/sccm/desktop-analytics/deploy-prod#bkmk_monitor).

![Captura de pantalla de la página de supervisión de estado de análisis de escritorio](media/monitor-health.png)

> [!NOTE]  
> Análisis escritorio solamente recopila datos de estado de los dispositivos que proporcionan datos de uso que puede usar como denominador. Esto significa que no incluye los dispositivos que ejecutan Windows 7 y Windows 10 que no se establecen para compartir datos de diagnóstico en el nivel mejorado (limitado). Si se establecen más del 10% de los dispositivos que ejecutan Windows 10 para compartir datos de diagnóstico en niveles que no sean mejorado (limitado), el **supervisar el estado** página muestra una advertencia en el área del titular.  

Para obtener más información acerca de una aplicación específica o la macro asesoramiento, selecciónela en la lista. 



## <a name="apps-and-office-apps"></a>Las aplicaciones y las aplicaciones de Office

![Factores de estado de mantenimiento para una aplicación de escritorio Analytics](media/monitor-health-status-factors.png)

Escritorio Analytics supervisa los siguientes factores de estado de mantenimiento para las aplicaciones y las aplicaciones de Office:

- **% De dispositivos con los bloqueos**: El número de dispositivos en el que se ha bloqueado esta aplicación en particular para las últimas dos semanas, dividido entre el número de dispositivos en el que se ha utilizado la aplicación. Esta vista le permite ver si la estabilidad de la aplicación ha aumentado o disminuido en la nueva versión del sistema operativo. Análisis de escritorio calcula este porcentaje de los siguientes conjuntos:  

    - **Después de la actualización**: Dispositivos que se han actualizado a la versión de sistema operativo de destino especificada en el plan de implementación. Para reducir el número de activos con datos insuficientes, escritorio Analytics recopila estos datos para todos los dispositivos actualizados. Este conjunto incluye los dispositivos que no está en el plan de implementación.  

    - **Antes de la actualización**: Dispositivos que están en una versión de SO anterior a lo especificado en el plan de implementación. Esta lista no incluye los dispositivos que ejecutan Windows 7.   

    - **Promedio comercial**: El promedio (avg) tasa de bloqueos en todos los dispositivos comerciales. Este promedio se calcula en *todas* versiones de la aplicación. Si su versión muestra una tasa de bloqueo por encima del promedio comercial, puede haber una versión más estable disponibles.  

- **% De las sesiones con los bloqueos**: Es similar al anterior, pero el porcentaje de sesiones con bloqueos en las últimas dos semanas de recuentos.  

Para determinar el estado de mantenimiento de una aplicación, análisis de escritorio requiere datos de al menos 20 dispositivos. De lo contrario notifica **datos insuficientes** para la aplicación. El servicio calcula el estado de mantenimiento según el *tasa de bloqueo de sesión* desde estos dispositivos. La tasa de bloqueo del dispositivo se proporciona solo meramente informativos. No se utiliza en el cálculo del estado de mantenimiento.

En la parte inferior de la página de detalles de la aplicación, las tres pestañas siguientes pueden ayudarle a solucionar problemas:

- **Otras versiones**: Una lista de versiones alternativas de esta aplicación. Para cada versión, muestra los cambios relativos a los tipos de bloqueo dentro de su organización y el promedio comercial. Si encuentra una versión posterior de la aplicación con una tasa menor de bloqueo, la actualización de la aplicación puede ayudar.  

    También muestra si la versión tiene un **listos para Windows** señal. Para obtener más información, consulte [riesgo de compatibilidad de aplicaciones de Windows](/sccm/desktop-analytics/compat-risk#risk-assessment-engine).  

- **Problemas principales de**: Recuento de identificadores de instancia de una lista de los errores más frecuentes. Identifica el seguimiento de pila asociado con el bloqueo con un identificador de error. Puede usar este identificador cuando se llama el proveedor de la aplicación para obtener soporte técnico.  

- **Bloqueos recientes**:  Una lista de dispositivos en el que la aplicación recientemente se ha bloqueado. Puede filtrar por Id. de error y otros criterios. Utilice esta información para solucionar el problema mediante la recopilación de registros o intentar correcciones en ciertos dispositivos antes de intentar una implementación más amplia.  

Si observa una regresión grave de mantenimiento que no puede corregir, cambiar la aplicación **decisión de actualización** a **no se puede**. Esta acción evita que la implementación futura de la actualización a los dispositivos con este recurso.



## <a name="office-add-ins"></a>Complementos de Office

![Captura de pantalla de factores de estado de mantenimiento para un complemento de Office](media/office-add-in-health-status-factors.png)

Escritorio Analytics supervisa los siguientes factores de estado de mantenimiento para los complementos de Office:

- **% De dispositivos con incidentes**: Un incidente es algo que impide que un complemento funciona correctamente. Por ejemplo, no se puede cargar o deja de responder. Esta sección muestra en las últimas dos semanas, el número de dispositivos en que el complemento seleccionado tenía un incidente dividido por el número de dispositivos en el que se está instalado el complemento. Análisis de escritorio calcula este porcentaje de los siguientes conjuntos:  

    - **Después de la actualización**: Dispositivos que se han actualizado a la versión de Office de destino especificada en el plan de implementación. Para reducir el número de activos con datos insuficientes, escritorio Analytics recopila estos datos para todos los dispositivos actualizados. Este conjunto incluye los dispositivos que no está en el plan de implementación.  

    - **Antes de la actualización**: Dispositivos que ejecutan cualquier versión de Office anterior a la versión que la implementación del plan de destinos. <!-- This does not include {include min version of Office}  --> Para evaluar el estado del complemento, comparar esta métrica para el **después de la actualización** porcentaje.  

    - **Promedio comercial**: La velocidad promedio (avg) incidentes en todos los dispositivos comerciales que usan la misma versión del complemento en la misma versión de Office. Utilice esta velocidad para comparar con los dispositivos de su organización. Si esta versión del complemento está teniendo una mayor tasa de incidentes que el promedio comercial, puede que tenga algún factor del entorno que contribuyen a los incidentes.  

- **% De las sesiones con incidentes**: Es similar al anterior, pero el porcentaje de sesiones con bloqueos en las últimas dos semanas de recuentos.  

Para determinar el estado de mantenimiento de complementos, análisis de escritorio requiere al menos tres dispositivos para la velocidad de incidentes de dispositivo y al menos 10 sesiones para la velocidad de incidentes de la sesión. Para ambos tipos, compara el antes y después los valores para determinar si hay una regresión. No se considera regresión hacia los objetivos de la reunión. 

Escritorio Analytics calcula el estado de mantenimiento general del complemento de Office según una combinación de dispositivo y sesión tarifas incidentes mediante la siguiente matriz:

|  | Datos insuficientes, tiempos de inactividad del dispositivo  | Métricas de bloqueo del dispositivo en buen estado | Regresión en las métricas de bloqueo del dispositivo |
|----------------|---------------------|-----------------------|------------------------|
| **Datos suficientes para las sesiones con los incidentes**| Datos insuficientes| Objetivos de reunión | Datos insuficientes |
| **Métricas en buen estado para las sesiones con los incidentes** | Objetivos de reunión | Objetivos de reunión | Objetivos de reunión |
| **Regresión en las métricas para las sesiones con los incidentes** | Datos insuficientes | Objetivos de reunión | Atención necesitado |


La página de detalles del complemento de Office también incluye los detalles siguientes para ayudarle a solucionar problemas: 

- **Incidentes recientes**: Una lista de los dispositivos en el que se produjo recientemente un incidente de complemento. Use esta lista para solucionar el problema mediante la recopilación de registros o intentar correcciones en esos dispositivos específicos antes de intentar una implementación más amplia.  



## <a name="office-macros"></a>Macros de Office

![Captura de pantalla de factores de estado de mantenimiento para un aviso de macros de Office](media/office-macros-health-status-factors.png)

Escritorio Analytics informa del estado en *avisos de macro*. Avisos de macro son posibles problemas detectados en los archivos de Office que contienen macros. Estos problemas son específicos de una aplicación de Office. Por ejemplo, Word, Excel, PowerPoint o Visio. 

Escritorio Analytics supervisa los siguientes factores de estado de mantenimiento de las macros de Office:

- **% De dispositivos con error de compilación**: Para las últimas dos semanas, el número de dispositivos en los errores relacionados con el aviso se ha producido durante la habilitación de la macro dividida por el número de dispositivos en el que se ha detectado el aviso. Análisis de escritorio calcula este porcentaje de los siguientes conjuntos: 

    - **Después de la actualización**: Los dispositivos en el que la versión de Office es el mismo que destino del plan de implementación  

    - **Antes de la actualización**: Los dispositivos que ejecutan cualquier versión de Office anterior a destino del plan de implementación  

    - **Promedio comercial**: El promedio (avg) de todos los dispositivos comerciales que se ejecuta la misma versión de Office como destino del plan de implementación  

- **% De dispositivos con error en tiempo de ejecución** Similar al anterior, pero en las últimas dos semanas, los dispositivos en el que los errores relacionados con el aviso se produjeron durante la ejecución de la macro dividida por el número de dispositivos en el que se ha detectado el aviso.  

La página de detalles de las macros de Office también incluye los detalles siguientes para ayudarle a solucionar problemas: 

- **Incidentes recientes**: Una lista de dispositivos en qué macro se produjeron recientemente errores en tiempo de ejecución y compilación. Use esta lista para solucionar el problema mediante la recopilación de registros o intentar correcciones en esos dispositivos específicos antes de intentar una implementación más amplia.



## <a name="see-also"></a>Consulte también

- [Riesgos de compatibilidad para aplicaciones de Windows en el análisis de escritorio](/sccm/desktop-analytics/compat-risk)  

- [Cómo se implementa en producción con análisis de escritorio](/sccm/desktop-analytics/deploy-prod)  
