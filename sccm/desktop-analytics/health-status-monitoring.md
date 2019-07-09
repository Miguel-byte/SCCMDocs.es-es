---
title: Supervisión del estado de mantenimiento
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo funciona la supervisión de estado de mantenimiento en el análisis de escritorio.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4b32105304354e9b9d4473451a32f52162f80d02
ms.sourcegitcommit: 20bbb870baf624c7809d3972f2d09a8d2df79cda
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/08/2019
ms.locfileid: "67623335"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Estado de mantenimiento de supervisión de análisis de escritorio

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Como se [implementa una actualización en producción](/sccm/desktop-analytics/deploy-prod), usar análisis de escritorio para ayudar a supervisar el estado de mantenimiento de los dispositivos. En este artículo se explica en detalle cómo funciona la supervisión de estado.

Para obtener más información sobre cómo usar esta característica, consulte [supervisar el estado de dispositivos actualizados](/sccm/desktop-analytics/deploy-prod#bkmk_monitor).

![Captura de pantalla de la página de supervisión de estado de análisis de escritorio](media/monitor-health.png)

> [!NOTE]  
> Análisis escritorio solamente recopila datos de estado de los dispositivos que proporcionan datos de uso que puede usar como denominador. Esto significa que no incluye los dispositivos que ejecutan Windows 7 y Windows 10 que no se establecen para compartir datos de diagnóstico en el nivel mejorado (limitado). Si se establecen más del 10% de los dispositivos que ejecutan Windows 10 para compartir datos de diagnóstico en niveles que no sean mejorado (limitado), el **supervisar el estado** página muestra una advertencia en el área del titular.  

Para obtener más información acerca de una aplicación específica, selecciónela en la lista.



## <a name="apps"></a>Aplicaciones

![Factores de estado de mantenimiento para una aplicación de escritorio Analytics](media/monitor-health-status-factors.png)

Escritorio Analytics supervisa los siguientes factores de estado de mantenimiento para las aplicaciones:

- **% De dispositivos con los bloqueos**: El número de dispositivos en el que se ha bloqueado esta aplicación en particular para las últimas dos semanas, dividido entre el número de dispositivos en el que se ha utilizado la aplicación. Esta vista le permite ver si la estabilidad de la aplicación ha aumentado o disminuido en la nueva versión del sistema operativo. Análisis de escritorio calcula este porcentaje de los siguientes conjuntos:  

    - **Después de la actualización**: Dispositivos que se han actualizado a la versión de sistema operativo de destino especificada en el plan de implementación. Para reducir el número de activos con datos insuficientes, escritorio Analytics recopila estos datos para todos los dispositivos actualizados. Este conjunto incluye los dispositivos que no está en el plan de implementación.  

    - **Antes de la actualización**: Dispositivos que están en una versión de SO anterior a lo especificado en el plan de implementación. Esta lista no incluye los dispositivos que ejecutan Windows 7.  

    - **Promedio comercial**: El promedio (avg) tasa de bloqueos en todos los dispositivos comerciales. Este promedio se calcula en *todas* versiones de la aplicación. Si su versión muestra una tasa de bloqueo por encima del promedio comercial, puede haber una versión más estable disponibles.  

- **% De las sesiones con los bloqueos**: Es similar al anterior, pero el porcentaje de sesiones con bloqueos en las últimas dos semanas de recuentos.  

Para determinar el estado de mantenimiento de una aplicación, análisis de escritorio requiere datos de al menos 20 dispositivos. De lo contrario notifica **datos insuficientes** para la aplicación. El servicio calcula el estado de mantenimiento según el *tasa de bloqueo de sesión* desde estos dispositivos. La tasa de bloqueo del dispositivo se proporciona solo meramente informativos. No se utiliza en el cálculo del estado de mantenimiento.

En la parte inferior de la página de detalles de la aplicación, las tres pestañas siguientes pueden ayudarle a solucionar problemas:

- **Otras versiones**: Una lista de versiones alternativas de esta aplicación. Para cada versión, muestra los cambios relativos a los tipos de bloqueo dentro de su organización y el promedio comercial. Si encuentra una versión posterior de la aplicación con una tasa menor de bloqueo, la actualización de la aplicación puede ayudar.  

    También muestra si la versión tiene un **listos para Windows** señal. Para obtener más información, consulte [Compatibility assessment de](compat-assessment.md#driver-risk-assessment).  

- **Problemas principales de**: Recuento de identificadores de instancia de una lista de los errores más frecuentes. Identifica el seguimiento de pila asociado con el bloqueo con un identificador de error. Puede usar este identificador cuando se llama el proveedor de la aplicación para obtener soporte técnico.  

- **Bloqueos recientes**:  Una lista de dispositivos en el que la aplicación recientemente se ha bloqueado. Puede filtrar por Id. de error y otros criterios. Utilice esta información para solucionar el problema mediante la recopilación de registros o intentar correcciones en ciertos dispositivos antes de intentar una implementación más amplia.  

Si observa una regresión grave de mantenimiento que no puede corregir, cambiar la aplicación **decisión de actualización** a **no se puede**. Esta acción evita que la implementación futura de la actualización a los dispositivos con este recurso.


## <a name="see-also"></a>Vea también

- [Evaluación de compatibilidad de análisis de escritorio](/sccm/desktop-analytics/compat-assessment)  

- [Cómo se implementa en producción con análisis de escritorio](/sccm/desktop-analytics/deploy-prod)  
