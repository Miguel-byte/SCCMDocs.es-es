---
title: Preguntas más frecuentes sobre análisis de escritorio
titleSuffix: Configuration Manager
description: Preguntas frecuentes sobre el análisis de escritorio.
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 663490349bcb61f243980c5e1a3fe1f5651d8573
ms.sourcegitcommit: 448cc0d9094a3c9e23f011c4673cd1e8b956280a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67860831"
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

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>¿Se puede reducir la cantidad de tiempo que tardan los datos actualizar en el portal de Mis análisis de escritorio?

Hay dos tipos de datos en el portal de análisis de escritorio: Datos del administrador y los datos de diagnóstico. Para actualizar los datos de administrador a petición, abra la ventana flotante de moneda de datos y seleccione **aplicar cambios**. Esta acción desencadena inmediatamente una actualización única de los cambios de administrador en las áreas de trabajo pendientes. Los cambios propagan y están generalmente disponibles dentro de 15 a 60 minutos. El tiempo depende del tamaño del área de trabajo y el ámbito de los cambios pendientes. Puede solicitar una actualización de datos y a petición hasta seis veces en un plazo de 24 horas. 

Todos los datos se actualizan automáticamente una vez al día, incluso si no solicita una actualización de datos y a petición. No hay ninguna manera de desencadenar una actualización de la petición de datos de diagnóstico. Para obtener más información sobre los diferentes tipos de datos de análisis de escritorio, consulte [latencia de datos](/sccm/desktop-analytics/troubleshooting#data-latency).

## <a name="privacy"></a>Privacidad

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>¿Análisis de escritorio se puede usar sin una conexión directa desde el cliente al servicio de administración de datos de Microsoft?

No, todo el servicio funciona con datos de diagnóstico de Windows, lo que requiere que los dispositivos tienen esta conectividad directa.

### <a name="can-i-choose-the-data-center-location"></a>¿Puedo elegir la ubicación del centro de datos?

Para Azure Log Analytics: Sí, al configurar el análisis de escritorio y crear el área de trabajo de Log Analytics.

Para el servicio de administración de datos de Microsoft y análisis de almacenamiento de Azure: No, estos dos servicios se hospedan en los Estados Unidos.

### <a name="where-is-my-organizations-data-stored"></a>¿Dónde se almacenan los datos de mi organización?

Datos de diagnóstico de Windows desde los equipos se cifran, enviados a y procesadas en centros de datos segura administrada por Microsoft ubicados en Estados Unidos. Nuestro análisis de los datos relacionados con el análisis de escritorio, a continuación, se proporciona a usted a través de la solución de análisis de escritorio en el portal de Azure. Análisis de escritorio se admiten en todas las regiones de Azure. Seleccionar una región de Azure internacional no impedirá datos de diagnóstico enviados a y procesarse en los centros de datos seguros de Microsoft en Estados Unidos.

## <a name="other"></a>Otros

### <a name="can-i-use-desktop-analytics-for-my-office-365-proplus-upgrades"></a>¿Puedo usar análisis de escritorio para Mis actualizaciones de Office 365 ProPlus?

No, análisis de escritorio se centra en Windows. Microsoft desarrolló el análisis de escritorio en estrecha colaboración con muchos clientes. A través del programa de vista previa, los comentarios del cliente eran acerca de cómo mejorar el análisis de escritorio su capacidad para administrar las implementaciones de Windows de confianza. También nos dijeron que querían [preparación para Office 365 ProPlus ](/sccm/sum/deploy-use/office-365-dashboard#bkmk_o365_readiness) más estrechamente integrado con herramientas de administración de office en Configuration Manager e Intune. Microsoft seguirá al realizar inversiones en esas áreas, al centrarse en escenarios de Windows en el escritorio de análisis.
