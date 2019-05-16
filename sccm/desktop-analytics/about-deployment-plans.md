---
title: Planes de implementación en escritorio Analytics
titleSuffix: Configuration Manager
description: Obtenga información sobre los planes de implementación en escritorio Analytics.
ms.date: 05/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: b44684f897e7aad4365c39e58c9bfd486bde7cbb
ms.sourcegitcommit: 53f2380ac67025fb4a69fc1651edad15d98e0cdd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65673293"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Acerca de los planes de implementación en escritorio Analytics

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Escritorio Analytics recopila y analiza los datos de dispositivos, aplicaciones y controladores de su organización. Según este análisis y la entrada, puede usar el servicio para crear planes de implementación para Windows 10. Planes de implementación tienen las siguientes características:  

- Le recomienda automáticamente los dispositivos que se va a incluir en las pruebas piloto  

- Identificar problemas de compatibilidad y sugerir mitigaciones  

- Evaluar el estado de la implementación antes, durante y después de las actualizaciones  

- Realizar un seguimiento del progreso de la implementación  

Como parte de su plan de implementación, realice las siguientes acciones:  

- Defina qué versiones de Windows 10 que desea implementar  

- Elija qué grupos de dispositivos a la que desea implementar  

- Crear reglas de preparación para la implementación  

- Definir la importancia de las aplicaciones  

- Elegir dispositivos pilotos según las recomendaciones automática  

- Decidir cómo solucionar problemas con las aplicaciones basadas en las recomendaciones de análisis de escritorio  

Análisis de escritorio actualiza diariamente datos del plan de implementación. Los cambios que realice podrían no aparecer durante 24 horas. Estos cambios incluyen asignar importancia a una aplicación, o elegir un dispositivo para incluir en una prueba piloto.  

Después de conectarse a análisis de escritorio a Configuration Manager, seleccione las colecciones de los planes de implementación. A continuación, esta integración le permite implementar Windows a una colección en función de los datos de análisis de escritorio.



## <a name="readiness-rules"></a>Reglas de preparación

Las siguientes reglas de disponibilidad están disponibles en los planes de implementación:

- Si los dispositivos reciban automáticamente controladores de Windows Update. Si los dispositivos reciben las actualizaciones de controladores desde Windows Update, entonces cualquier problema de controlador identificado como parte de la evaluación de preparación se marca automáticamente como **listo**.  

- Instalar bajo el umbral de recuento para las aplicaciones de Windows. Si una aplicación está instalada en un mayor porcentaje de equipos a este umbral, el plan de implementación marca la aplicación como **Noteworthy**. Esta etiqueta significa que puede decidir cuán importante es la prueba durante la fase piloto.  



## <a name="importance"></a>Importancia

Como parte del plan de implementación, configure el *importancia* de las aplicaciones. Escritorio Analytics detecta estas aplicaciones instaladas en los dispositivos de destino. Esta configuración permite a los análisis de escritorio determinar qué dispositivos incluye en la fase piloto de la implementación.

Si una aplicación está instalada en menos de 2% de los dispositivos de destino, se marca **bajo número de instalaciones**. El valor predeterminado es de dos por ciento. Puede ajustar el umbral en la configuración de preparación de 0% al 10%. Escritorio Analytics marca automáticamente estas aplicaciones como **listo para actualizar**.  

Para las aplicaciones, elija una importancia de **crítico**, **importante**, o **importante no**. Si marca una como importante o crítico, análisis de escritorio incluye en la implementación piloto algunos dispositivos con esa aplicación. El servicio incluye en el proyecto piloto de más instancias de una aplicación crítica. Si marca una aplicación como no importante, análisis de escritorio lo establece automáticamente en **listo para actualizar**.



## <a name="pilot-devices"></a>Dispositivos pilotos

Análisis de escritorio combina la información de importancia con la configuración global de piloto. A continuación, crea una recomendación para el que los dispositivos deben formar parte de la implementación piloto. La implementación piloto recomendada incluye dispositivos con distintas configuraciones de hardware y una o varias instancias de todas las aplicaciones críticas e importantes. Si una aplicación se marca crítica, el servicio recomienda más dispositivos con esa aplicación en el proyecto piloto.



## <a name="deployment-plans-in-configuration-manager"></a>Planes de implementación en Configuration Manager

Después de crear un plan de implementación, use Configuration Manager para implementar los productos. Una vez se inicia la implementación, análisis escritorio supervisa la implementación según la configuración en el plan.


## <a name="next-steps"></a>Pasos siguientes

- [Obtenga información acerca de los activos de análisis de escritorio](/sccm/desktop-analytics/about-assets): dispositivos, aplicaciones y controladores  

- [Obtenga información acerca de las actualizaciones de seguridad y la característica](/sccm/desktop-analytics/about-updates)  

- [Crear un plan de implementación](/sccm/desktop-analytics/create-deployment-plans)  
