---
title: Actualizaciones en el análisis de escritorio
titleSuffix: Configuration Manager
description: Obtenga información sobre la seguridad y las actualizaciones de características en análisis de escritorio.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0cceaf6f4475a024b8f3375ef962a6dfc2dddc4d
ms.sourcegitcommit: e0d303d87c737811c2d3c40d01cd3d260a5c7bde
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69974762"
---
# <a name="updates-in-desktop-analytics"></a>Actualizaciones en el análisis de escritorio

> [!Note]  
> Esta información está relacionada con un servicio de vista previa que se puede modificar sustancialmente antes de que se publique comercialmente. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

En el portal de análisis de escritorio, vea el estado de las actualizaciones de seguridad y características. Seleccione estos nodos en el grupo supervisar del menú principal de análisis de escritorio. Estos nodos proporcionan información sobre el estado de estas actualizaciones en su entorno.


## <a name="security-updates"></a>Actualizaciones de seguridad

Para revisar el estado actual de las actualizaciones de seguridad, seleccione **actualizaciones de seguridad** en la sección **supervisión** de análisis de escritorio:

![Nodo actualizaciones de seguridad del análisis de escritorio](media/security-updates.png)

Esta vista resume las actualizaciones de *seguridad* para los dispositivos que ejecutan Windows 10. Los dispositivos del gráfico de barras se clasifican por las siguientes etiquetas:

#### <a name="latest"></a>Avanzada

Los dispositivos ejecutan la actualización de seguridad más reciente de esa versión y canal.

#### <a name="latest-1"></a>Más reciente: 1

Los dispositivos ejecutan una actualización de seguridad una versión anterior a la última actualización disponible en dicho canal.

#### <a name="older"></a>Más

Los dispositivos ejecutan una actualización de seguridad anterior a la última-1.

#### <a name="not-measured"></a>No se mide

El análisis de escritorio no ha evaluado el dispositivo. Este estado incluye los dispositivos que ejecutan Windows 7, Windows 8.1 o dispositivos Windows 10 registrados para el programa Windows Insider.  

Si un dispositivo de Windows 10 *no se autentica* con un cuenta de Microsoft, Windows no informa de estos datos. Esta autenticación se realiza normalmente como parte de la instalación de Windows de la experiencia rápida (OOBE).<!-- 5148153 -->


## <a name="feature-updates"></a>Actualizaciones de características

Para revisar el estado actual de las actualizaciones de características, seleccione **actualizaciones de características** en la sección **supervisión** de análisis de escritorio:

![Nodo actualizaciones de características de análisis de escritorio](media/feature-updates.png)

Esta vista resume las actualizaciones de *características* de los dispositivos que ejecutan Windows 10.

Para obtener más información sobre los períodos de servicio, consulte la [hoja de hechos de ciclo de vida de Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).  

Los dispositivos del gráfico de barras se clasifican por las siguientes etiquetas:

#### <a name="in-service"></a>En servicio

Los dispositivos ejecutan la actualización de características más reciente de esa versión y canal.  

#### <a name="near-end-of-service"></a>Cerca del final del servicio

Los dispositivos ejecutan una actualización de características que se encuentra en un plazo de 90 días a partir del final del servicio.

#### <a name="end-of-service"></a>Fin de servicio

Los dispositivos ejecutan una actualización de características que está más allá del final de la fecha de servicio. Para obtener más información acerca de las fechas de fin de servicio, consulte la [hoja de hechos de ciclo de vida de Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

#### <a name="not-measured"></a>No se mide

El análisis de escritorio no ha evaluado el dispositivo. Este estado incluye los dispositivos que ejecutan Windows 7, Windows 8.1 o dispositivos Windows 10 registrados para el programa Windows Insider.

Si un dispositivo de Windows 10 *no se autentica* con un cuenta de Microsoft, Windows no informa de estos datos. Esta autenticación se realiza normalmente como parte de la instalación de Windows de la experiencia rápida (OOBE).<!-- 5148153 -->


## <a name="next-steps"></a>Pasos siguientes

- [Más información sobre los activos de análisis de escritorio](/sccm/desktop-analytics/about-assets): dispositivos, controladores y aplicaciones  

- [Más información sobre los planes de implementación](/sccm/desktop-analytics/about-deployment-plans)  
