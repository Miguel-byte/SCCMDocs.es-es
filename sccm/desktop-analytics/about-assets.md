---
title: Activos en análisis de escritorio
titleSuffix: Configuration Manager
description: Obtenga información acerca de los dispositivos, los controladores y las aplicaciones de análisis de escritorio.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 63800bf6c8fa1d35eac44f64f2f03bde4f1d5022
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68535950"
---
# <a name="assets-in-desktop-analytics"></a>Activos en análisis de escritorio

> [!Note]  
> Esta información está relacionada con un servicio de vista previa que se puede modificar sustancialmente antes de que se publique comercialmente. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Después de que los dispositivos informen los datos en el análisis de escritorio, se proporciona un inventario de los siguientes recursos:

- Dispositivos
- Aplicaciones instaladas  

En el portal de servicios, seleccione **recursos** en el menú Análisis de escritorio.


## <a name="devices"></a>Dispositivos

La pestaña **dispositivos** muestra información clave sobre todos los dispositivos de la organización que se inscriben en el análisis de escritorio. Puede ordenar por cualquier columna o filtro para valores concretos.

> [!NOTE]  
> Si el panel no informa del número de dispositivos que espera ver para su entorno, consulte [solución de problemas de análisis de escritorio](/sccm/desktop-analytics/troubleshooting).  

En un plan de implementación, hay más detalles sobre los dispositivos. Para obtener más información, consulte [planear recursos](/sccm/desktop-analytics/about-deployment-plans#plan-assets)

## <a name="apps"></a>Aplicaciones

En la pestaña **aplicaciones** se muestran todas las aplicaciones instaladas que el servicio detecta en los dispositivos Windows.

Las aplicaciones **destacadas** se instalan en más del 2% de los dispositivos inscritos.

Configure la **importancia** de las aplicaciones mediante la configuración de una de las siguientes categorías:

- Crítica
- Aún
- Ignorar
- No revisado

Seleccione la aplicación en la lista y seleccione **Editar**. Esta acción muestra los detalles de la aplicación. Seleccione el menú desplegable **importancia** y establezca un valor. También puede asignar un **propietario**. Si realiza cambios, seleccione **Guardar**.

En un plan de implementación, también puede establecer la **decisión de actualización**. Para obtener más información, consulte [planear recursos](/sccm/desktop-analytics/about-deployment-plans#plan-assets)


## <a name="next-steps"></a>Pasos siguientes

- [Más información sobre los planes de implementación de análisis de escritorio](/sccm/desktop-analytics/about-deployment-plans)  

- [Más información sobre la seguridad y las actualizaciones de características](/sccm/desktop-analytics/about-updates)  

- [Evaluación de compatibilidad en análisis de escritorio](/sccm/desktop-analytics/compat-assessment)  
