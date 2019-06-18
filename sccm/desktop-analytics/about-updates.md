---
title: Actualizaciones en el análisis de escritorio
titleSuffix: Configuration Manager
description: Obtenga información acerca de las actualizaciones de seguridad y la característica de análisis de escritorio.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7fc673cfa11224394df785f2e13e77ad2e0f5888
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159214"
---
# <a name="updates-in-desktop-analytics"></a>Actualizaciones en el análisis de escritorio

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

En el portal de análisis de escritorio, ver el estado de actualizaciones de seguridad y la característica. Seleccionar estos nodos en el grupo de Monitor del menú principal de análisis de escritorio. Estos nodos ofrecen información sobre el estado de estas actualizaciones en su entorno.



## <a name="security-updates"></a>Actualizaciones de seguridad

Para revisar el estado actual de las actualizaciones de seguridad, seleccione **las actualizaciones de seguridad** en el **Monitor** sección de análisis de escritorio:

![Nodo de actualizaciones de seguridad de escritorio de análisis](media/security-updates.png)

Esta vista se resume *seguridad* actualizaciones para los dispositivos que ejecutan Windows 10. Los dispositivos en el gráfico de barras se clasifican en las siguientes etiquetas:

#### <a name="latest"></a>Más reciente

Los dispositivos se está ejecutando la última actualización de seguridad de esa versión y el canal.

#### <a name="latest-1"></a>1 de la versión más reciente

Los dispositivos ejecutan una seguridad actualización de una versión anterior a la última actualización disponible en ese canal.

#### <a name="older"></a>Anterior

Los dispositivos están ejecutando una actualización de seguridad anterior a la versión más reciente-1.

#### <a name="not-measured"></a>No se ha medido

Análisis de escritorio no ha evaluado el dispositivo. Este estado incluye los dispositivos que ejecutan Windows 7, Windows 8.1 o Windows 10 dispositivos registrados para el programa de Windows Insider.  



## <a name="feature-updates"></a>Actualizaciones de características

Para revisar el estado actual de las actualizaciones de características, seleccione **las actualizaciones de características** en el **Monitor** sección de análisis de escritorio:

![Nodo de actualizaciones de características de análisis de escritorio](media/feature-updates.png)

Esta vista se resume *característica* actualizaciones para los dispositivos que ejecutan Windows 10.

Para obtener más información sobre los períodos de servicio, consulte [hoja de información del ciclo de vida de Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).  

Los dispositivos en el gráfico de barras se clasifican en las siguientes etiquetas:

#### <a name="in-service"></a>En el servicio

Los dispositivos se está ejecutando la última actualización de características para esa versión y el canal.  

#### <a name="near-end-of-service"></a>Cerca del final del servicio

Los dispositivos están ejecutando una actualización de características que menos de 90 días de alcanzar el final del servicio.

#### <a name="end-of-service"></a>Extremo de servicio

Los dispositivos están ejecutando una actualización de la función que está más allá de la fecha de finalización del servicio. Para obtener más información acerca de la finalización de las fechas de servicio, consulte [hoja de información del ciclo de vida de Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

#### <a name="not-measured"></a>No se ha medido

Análisis de escritorio no ha evaluado el dispositivo. Este estado incluye los dispositivos que ejecutan Windows 7, Windows 8.1 o Windows 10 dispositivos registrados para el programa de Windows Insider.



## <a name="next-steps"></a>Pasos siguientes

- [Obtenga información acerca de los activos de análisis de escritorio](/sccm/desktop-analytics/about-assets): dispositivos, aplicaciones y controladores  

- [Obtenga información sobre los planes de implementación](/sccm/desktop-analytics/about-deployment-plans)  
