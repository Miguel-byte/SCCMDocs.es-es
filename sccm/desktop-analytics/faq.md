---
title: Preguntas más frecuentes sobre análisis de escritorio
titleSuffix: Configuration Manager
description: Preguntas frecuentes sobre el análisis de escritorio.
ms.date: 04/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4596923f9a6a42ad98dc17257b22925ad0bc5eed
ms.sourcegitcommit: 9af73f5c1b93f6ccaea3e6a096f75a5fecd65c2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2019
ms.locfileid: "64562452"
---
# <a name="desktop-analytics-faq"></a>Preguntas más frecuentes de análisis de escritorio

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

## <a name="windows-upgrade"></a>Actualización de Windows

### <a name="can-i-upgrade-windows-and-change-architecture"></a>¿Puedo actualizar de Windows y cambiar la arquitectura?

Escritorio Analytics está diseñado para las actualizaciones in situ de mejor soporte técnico. Actualizaciones en contexto no admiten migraciones de arquitectura de 32 bits a 64 bits. Si necesita migrar equipos que en este escenario, utilice el escenario de actualización. Escritorio insights Analytics todavía resultan valiosos en este escenario, pero puede pasar por alto instrucciones específicas de la actualización.

Para obtener más información, consulte [Actualizar un equipo existente con una nueva versión de Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>¿Puedo cambiar de BIOS a UEFI cuando se actualiza Windows?

Sí. Para obtener más información, consulte [conversión de BIOS a UEFI durante una actualización en contexto](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>¿Puedo usar análisis de escritorio con Windows 10 LTSC?

Aunque puede usar análisis de escritorio para ayudar con la actualización de los dispositivos de Windows 10 a largo plazo de mantenimiento canal (LTSC) en canal semianual de Windows 10, análisis de escritorio no admite las actualizaciones de Windows 10 LTSC. Este canal de Windows 10 no está pensada para un uso extenso y no recibe actualizaciones de características, por lo que no es un destino compatible con análisis de escritorio. Para obtener más información, consulte [Windows como una información general del servicio](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).

## <a name="privacy"></a>Privacidad

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>¿Análisis de escritorio se puede usar sin una conexión directa desde el cliente al servicio de administración de datos de Microsoft?

No, todo el servicio funciona con datos de diagnóstico de Windows, lo que requiere que los dispositivos tienen esta conectividad directa.

### <a name="can-i-choose-the-data-center-location"></a>¿Puedo elegir la ubicación del centro de datos?

Para Azure Log Analytics: Sí, al configurar el análisis de escritorio y crear el área de trabajo de Log Analytics.

Para el servicio de administración de datos de Microsoft y análisis de almacenamiento de Azure: No, estos dos servicios se hospedan en los Estados Unidos.

### <a name="where-is-my-organizations-data-stored"></a>¿Dónde se almacenan los datos de mi organización?

Datos de diagnóstico de Windows desde los equipos se cifran, enviados a y procesadas en centros de datos segura administrada por Microsoft ubicados en Estados Unidos. Nuestro análisis de los datos relacionados con el análisis de escritorio, a continuación, se proporciona a usted a través de la solución de análisis de escritorio en el portal de Azure. Análisis de escritorio se admiten en todas las regiones de Azure. Seleccionar una región de Azure internacional no impedirá datos de diagnóstico enviados a y procesarse en los centros de datos seguros de Microsoft en Estados Unidos.
