---
title: Supervisión de cumplimiento de Mobile Threat Defense
titleSuffix: Configuration Manager
description: Supervisión del estado de cumplimiento del asociado Mobile Threat Defense en la consola de administrador de Configuration Manager
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cc5b38894155df35812d14397fb0d3aaea79c585
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62228412"
---
# <a name="monitor-mobile-threat-defense-compliance"></a>**Supervisión de cumplimiento de Mobile Threat Defense**

*Se aplica a: System Center Configuration Manager (Rama actual)*

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
|**Gravedad de amenaza**| Sí | Gravedad de amenaza es la definición de una amenaza individual según la configuración del administrador en la consola del asociado Mobile Threat Defense. Tiene uno de los tres valores: **Baja**, **medio** o **alta** |
|**Estado de amenaza**| Sí | El estado actual de la amenaza en el dispositivo. Estados posibles: **Active**, **resuelto** o **pasa por alto:** Indica que el usuario ha ignorado la amenaza en sus dispositivos, pero sigue estando presente la amenaza. |
|**Tipo de amenaza**| Sí | Tipo de amenaza según el asociado Mobile Threat Defense. Valores posibles: **Aplicación**, **archivo** o **OS** |
|**Id. de cuenta de AAD**| No | El identificador único de Azure Active Directory. |
|**Clasificación**| Sí | Clasificación de la amenaza según el asociado Mobile Threat Defense. Valores posibles: **Habilitador de raíz, Riskware, Adware, Chargeware, fuga de datos, troyano, gusano, Virus, contra vulnerabilidades de seguridad, puerta trasera, Bot, AppDropper, fraude por clic, correo no deseado, Spyware, vigilancia, vulnerabilidad, desconocido, Jailbreak, conectividad, fraude de tasas, aplicación instalada como prueba de raíz** |
|**Id. de dispositivo**| No | El identificador de objeto de Active Directory de Azure que representa el dispositivo unido a un área de trabajo con información de amenazas. |
|**Id. de amenaza**| No | Identificador único generado por el asociado Mobile Threat Defense para la amenaza. El identificador de amenaza se utiliza para realizar el seguimiento de la resolución. |
|**URL de amenaza**| No | Se trata de los vínculos a la dirección URL de la amenaza, si están disponibles, que remiten a la vista de la consola de administración de esta amenaza concreta en el asociado Mobile Threat Defense. |

> [!TIP] 
> Asegúrese de habilitar las columnas que no están **visibles de forma predeterminada** para ver más detalles sobre el estado de cumplimiento de Mobile Threat Defense de sus dispositivos.
