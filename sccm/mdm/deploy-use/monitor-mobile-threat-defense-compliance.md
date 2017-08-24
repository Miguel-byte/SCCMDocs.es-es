---
title: "Supervisión de cumplimiento de Mobile Threat Defense | System Center Configuration Manager"
description: "Supervisión del estado de cumplimiento del asociado Mobile Threat Defense en la consola de administrador de Configuration Manager"
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 8edf83a0f761dfc16274ce49c3aa2b878c7fe6cd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-mobile-threat-defense-compliance"></a>**Supervisión de cumplimiento de Mobile Threat Defense**

*Se aplica a: System Center Configuration Manager (rama actual)*

## <a name="to-monitor-the-overall-compliance-status"></a>Para supervisar el estado de cumplimiento general

Para supervisar el estado de Mobile Threat Defense:

1.  En la consola de Configuration Manager, haga clic en el área de trabajo **Supervisión**.

2.  En el área de trabajo **Supervisión**, haga clic en el nodo **Seguridad**.

Puede ver un resumen del estado de cumplimiento con niveles diferentes de amenazas, que se muestra en un formato de gráfico visual. Puede hacer clic en las secciones individuales de los gráficos para obtener más información, como: 

- El número de dispositivos que la plataforma identifica como no compatibles
- Los errores relacionados con el estado de cumplimiento del dispositivo

![](http://i.imgur.com/bmPsiWk.png)

## <a name="to-monitor-the-individual-compliance-status"></a>Para supervisar el estado de cumplimiento individual

También puede ver el estado individual de cada dispositivo:

1.  En la consola de Configuration Manager, haga clic en el área de trabajo **Activos y compatibilidad**.

2.  Haga clic en **Dispositivos**.

> [!TIP] 
> Puede agregar las columnas **Cumplimiento de amenaza de dispositivo** y **Nivel de amenaza de dispositivo** para ver el estado. Estas columnas no se muestran de manera predeterminada.

## <a name="device-threat-protection-tab"></a>Pestaña Protección contra amenazas de dispositivo

Además, en la pantalla **Dispositivos**, puede seleccionar dispositivos específicos y luego hacer clic en la pestaña **Protección contra amenazas de dispositivo**, que proporciona más detalles sobre el estado de cumplimiento del dispositivo. A continuación, puede consultar las descripciones de las columnas y los valores previstos para facilitar el análisis del estado de cumplimiento del dispositivo.

> [!IMPORTANT] 
> La pestaña Protección contra amenazas de dispositivo solo aparece si el dispositivo seleccionado es un dispositivo móvil.

|Nombre de columna|Visible de forma predeterminada|Descripción| 
|-|-|-|
|**Descripción**| Sí | Detalles sobre la amenaza proporcionados por el asociado Mobile Threat Defense. |
|**Hora de última actualización**| Sí | La última vez que el asociado Mobile Threat Defense ha enviado a Intune detalles actualizados sobre la amenaza. |
|**Gravedad de amenaza**| Sí | Gravedad de amenaza es la definición de una amenaza individual según la configuración del administrador en la consola del asociado Mobile Threat Defense. Tiene uno de los tres valores: **Baja**, **Media** o **Alta**. |
|**Estado de amenaza**| Sí | El estado actual de la amenaza en el dispositivo. Estados posibles: **Activa**, **Resuelta** u **Omitida:** indica que el usuario ha ignorado la amenaza en el dispositivo, pero que esta aún existe. |
|**Tipo de amenaza**| Sí | Tipo de amenaza según el asociado Mobile Threat Defense. Valores posibles: **Aplicación**, **Archivo** o **SO** |
|**Id. de cuenta de AAD**| No | El identificador único de Azure Active Directory. |
|**Clasificación**| Sí | Clasificación de la amenaza según el asociado Mobile Threat Defense. Valores posibles: **Habilitador de acceso a raíz, Riskware, Adware, Chargeware, Fuga de datos, Troyano, Gusano, Virus, Vulnerabilidad de seguridad, Puerta trasera, Bot, Instalador de malware de aplicaciones, Fraude por clic, Correo no deseado, Spyware, Vigilancia, Vulnerabilidad, Desconocido, Jailbreak de raíz, Conectividad, Fraude de tasas y Aplicación instalada como prueba** |
|**Id. de dispositivo**| No | El identificador de objeto de Active Directory de Azure que representa el dispositivo unido a un área de trabajo con información de amenazas. |
|**Id. de amenaza**| No | Identificador único generado por el asociado Mobile Threat Defense para la amenaza. El identificador de amenaza se utiliza para realizar el seguimiento de la resolución. |
|**URL de amenaza**| No | Se trata de los vínculos a la dirección URL de la amenaza, si están disponibles, que remiten a la vista de la consola de administración de esta amenaza concreta en el asociado Mobile Threat Defense. |

> [!TIP] 
> Asegúrese de habilitar las columnas que no están **visibles de forma predeterminada** para ver más detalles sobre el estado de cumplimiento de Mobile Threat Defense de sus dispositivos.
