---
title: Recursos de análisis de escritorio
titleSuffix: Configuration Manager
description: Obtenga información sobre los dispositivos, controladores y las aplicaciones de escritorio de análisis.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b0e47541d7acf5e1f5a74a58f6d39603bfcb9269
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159233"
---
# <a name="assets-in-desktop-analytics"></a>Recursos de análisis de escritorio

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Después de que los dispositivos notificarán datos a Analytics de escritorio, proporciona un inventario de los recursos siguientes:

- Dispositivos  
- Controladores de hardware  
- Aplicaciones instaladas  

En el portal de servicios, seleccione **activos** en el menú de análisis de escritorio.


## <a name="devices"></a>Dispositivos

El **dispositivos** ficha muestra información esencial sobre todos los dispositivos de su organización que se inscribe a análisis de escritorio. Se puede ordenar cualquier columna o filtrar determinados valores.

> [!NOTE]  
> Si el panel no notifica el número de dispositivos que espera para su entorno, consulte [solución de problemas de análisis de escritorio](/sccm/desktop-analytics/troubleshooting).  

En un plan de implementación, hay más detalles acerca de los dispositivos. Para obtener más información, consulte [Plan activos](/sccm/desktop-analytics/about-deployment-plans#plan-assets)

## <a name="apps"></a>Aplicaciones

El **aplicaciones** pestaña aplicaciones muestra todos los instalada que detecta el servicio de los dispositivos de Windows.

**Merece la pena comentar** aplicaciones están instaladas en más de 2% de los dispositivos inscritos.

Configurar la **importancia** de aplicaciones si se establece alguna de las siguientes categorías:

- Crítica
- Importante
- Ignorar
- No se ha revisado

Seleccione la aplicación en la lista y seleccione **editar**. Esta acción muestra los detalles de la aplicación. Seleccione el **importancia** menú desplegable y establezca un valor. También puede asignar un **propietario**. Si realiza cambios, seleccione **guardar**.

En un plan de implementación, también puede establecer el **decisión de actualización**. Para obtener más información, consulte [Plan activos](/sccm/desktop-analytics/about-deployment-plans#plan-assets)


## <a name="next-steps"></a>Pasos siguientes

- [Obtenga información acerca de los planes de implementación de análisis de escritorio](/sccm/desktop-analytics/about-deployment-plans)  

- [Obtenga información acerca de las actualizaciones de seguridad y la característica](/sccm/desktop-analytics/about-updates)  

- [Evaluación de compatibilidad de análisis de escritorio](/sccm/desktop-analytics/compat-assessment)  
