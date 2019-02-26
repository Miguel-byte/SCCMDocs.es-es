---
title: Planes de implementación en escritorio Analytics
titleSuffix: Configuration Manager
description: Obtenga información sobre los planes de implementación en escritorio Analytics.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce726ffa0dfc8a46bd0891e50ff087ad4931d901
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755616"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Acerca de los planes de implementación en escritorio Analytics 

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Escritorio Analytics recopila y analiza los datos de dispositivos, aplicaciones y controladores de su organización. Según este análisis y la entrada, puede usar el servicio para crear planes de implementación para Windows 10 y Office 365 ProPlus. Planes de implementación tienen las siguientes características:  

- Le recomienda automáticamente los dispositivos que se va a incluir en las pruebas piloto  

- Identificar problemas de compatibilidad y sugerir mitigaciones  

- Evaluar el estado de la implementación antes, durante y después de las actualizaciones  

- Realizar un seguimiento del progreso de la implementación  


Como parte de su plan de implementación, realice las siguientes acciones:  

 - Defina qué productos y versiones que desea implementar: Windows 10, Office 365 ProPlus, o ambos  

 - Elija qué grupos de dispositivos a la que desea implementar  

 - Crear reglas de preparación para la implementación  

 - Definir la importancia de las aplicaciones y complementos de Office  

 - Elegir dispositivos pilotos según las recomendaciones automática  

 - Decidir cómo solucionar problemas con aplicaciones y complementos de Office según las recomendaciones de análisis de escritorio  


Análisis de escritorio actualiza diariamente datos del plan de implementación. Los cambios que realice podrían no aparecer durante 24 horas. Estos cambios incluyen asignar importancia a una aplicación, o elegir un dispositivo para incluir en una prueba piloto.  

Si se conexión a análisis de escritorio a Configuration Manager, seleccione las colecciones en los planes de implementación. A continuación, esta integración le permite implementar Windows o Office en una colección basada en los datos de análisis de escritorio. 

Si no usa Configuration Manager, puede crear grupos en Log Analytics. Para obtener más información, consulte [búsquedas de registros de grupos de equipos en Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-computer-groups). 



## <a name="readiness-rules"></a>Reglas de preparación

Las siguientes reglas de disponibilidad están disponibles en los planes de implementación:

- Si los dispositivos reciban automáticamente controladores de Windows Update. Si los dispositivos reciben las actualizaciones de controladores desde Windows Update, entonces cualquier problema de controlador identificado como parte de la evaluación de preparación se marca automáticamente como **listo**.  

- Instalar bajo el umbral de recuento para las aplicaciones de Windows. Si una aplicación está instalada en un mayor porcentaje de equipos a este umbral, el plan de implementación marca la aplicación como **Noteworthy**. Esta etiqueta significa que puede decidir cuán importante es la prueba durante la fase piloto.  

- Actualización de Office 365 ProPlus de 32 bits a 64 bits en dispositivos que tienen una versión de 64 bits de Windows. Este comportamiento es el valor predeterminado.  

- Al actualizar desde una versión anterior de Office, deje las aplicaciones de Office más antiguas, incluso si esas aplicaciones no existen en la versión más reciente de Office. Este comportamiento no está en forma predeterminada.  

- Instalar bajo el umbral de recuento de los complementos de Office. El umbral predeterminado es `2%`. Complementos debajo de este umbral se establecen automáticamente en *bajo número de instalaciones*. Análisis de escritorio no validación estos complementos durante la prueba piloto. 

    Si un complemento se instala en un mayor porcentaje de equipos a este umbral, el plan de implementación marca como el complemento *Noteworthy*. A continuación, puede decidir su importancia para la prueba durante la fase piloto.   



## <a name="importance"></a>Importancia

Como parte del plan de implementación, configure el *importancia* de las aplicaciones y complementos de Office. Escritorio Analytics detecta estas aplicaciones instaladas en los dispositivos de destino. Esta configuración permite a los análisis de escritorio determinar qué dispositivos incluye en la fase piloto de la implementación. 

Si una aplicación o el complemento se instala en menos de 2% de los dispositivos de destino, se marca **bajo número de instalaciones**. El valor predeterminado es de dos por ciento. Puede ajustar el umbral en la configuración de preparación de 0% al 10%. Análisis de escritorio marcan automáticamente estas aplicaciones y complementos como **listo para actualizar**.  

Para las aplicaciones y complementos, elija una importancia de **crítico**, **importante**, o **importante no**. Si marca una como importante o crítico, análisis de escritorio incluye en la implementación piloto algunos dispositivos con esa aplicación o complemento. El servicio incluye en el proyecto piloto más instancias de una aplicación crítica o un complemento. Si selecciona una aplicación o complemento como no importante, análisis de escritorio lo establece automáticamente en **listo para actualizar**.



## <a name="pilot-devices"></a>Dispositivos pilotos

Análisis de escritorio combina la información de importancia con la configuración global de piloto. A continuación, crea una recomendación para el que los dispositivos deben formar parte de la implementación piloto. La implementación piloto recomendada incluye dispositivos con distintas configuraciones de hardware y una o varias instancias de todas las aplicaciones críticas e importantes. Si una aplicación se marca crítica, el servicio recomienda más dispositivos con esa aplicación en el proyecto piloto.



## <a name="deployment-plans-in-configuration-manager"></a>Planes de implementación en Configuration Manager

Después de crear un plan de implementación, use Configuration Manager para implementar los productos. Una vez se inicia la implementación, análisis escritorio supervisa la implementación según la configuración en el plan.

<!--more on deployment plans in SCCM-->

<!-- test comment-->

## <a name="next-steps"></a>Pasos siguientes

- [Obtenga información acerca de los activos de análisis de escritorio](/sccm/desktop-analytics/about-assets): dispositivos, aplicaciones, aplicaciones de Office, complementos de Office y las macros de Office  

- [Obtenga información acerca de las actualizaciones de seguridad y la característica](/sccm/desktop-analytics/about-updates)  

- [Crear un plan de implementación](/sccm/desktop-analytics/create-deployment-plans)  

