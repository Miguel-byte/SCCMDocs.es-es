---
title: Cómo crear planes de implementación
titleSuffix: Configuration Manager
description: Guía de procedimientos para crear planes de implementación en escritorio Analytics.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 35e8e883acafaa1d606d81402b868b8a755d0887
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62208048"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Cómo crear planes de implementación en escritorio Analytics 

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

En este artículo proporciona los pasos para crear un plan de implementación en escritorio Analytics. Antes de empezar, primero [Obtenga información sobre los planes de implementación](/sccm/desktop-analytics/about-deployment-plans).

Siga los pasos descritos en este artículo para usar un análisis de escritorio para crear un plan para la implementación de Windows 10 y Office 365 ProPlus. Crear planes de implementación para Windows 10, Office 365 ProPlus o ambos.

1. Abra el [portal de análisis de escritorio](https://aka.ms/m365aprod). Use las credenciales que tienen al menos **colaboradores del área de trabajo** permisos.  

2. Seleccione **planes de implementación** en el grupo de administración.  

3. En el **planes de implementación** panel, seleccione **crear**.  

4. En el **Crear plan de implementación** panel, configure las siguientes opciones:  

    - **Nombre**: Un nombre único para el plan de implementación  

    - **Productos y versiones**: Elija qué productos y versiones para implementar. Microsoft recomienda crear planes de implementación para Office y Windows juntos y usar las versiones más recientes.  

    - **Grupos de dispositivos**: Seleccione uno o más grupos y, a continuación, seleccione **establecer como destino grupos**. Grupos con **SCCM** como el origen son colecciones sincronizadas desde Configuration Manager.  

    - **Las reglas de preparación**: Estas reglas ayudan a determinar qué dispositivos necesarios para actualización. 

    - **Fecha de finalización**: Elija la fecha por el que Windows y Office deben distribuirse completamente en todos los dispositivos de destino.  

5. Seleccione **crear**. El nuevo plan aparece en la lista de planes de implementación mientras se está procesando. Proceso puede tardar hasta 48 horas antes de continuar con el paso siguiente.   

6. Abrir el plan de implementación, seleccione su nombre.  

7. En el menú del plan de implementación, en el **preparar** grupo, seleccione **identificar importancia**.  

    1. En el **aplicaciones** pestaña, seleccione esta opción para mostrar sólo **no revisado** activos.  

    2. Seleccione cada aplicación y, a continuación, seleccione **editar**. Puede seleccionar más de una aplicación para editar al mismo tiempo.   

    3. Elija un nivel de importancia de la **importancia** lista. Si desea que el análisis de escritorio para validar el complemento durante el programa piloto, seleccione **crítico** o **importante**. No valida los complementos marcados como **importante no**. Tenga en cuenta la [riesgo compatibilidad](/sccm/desktop-analytics/compat-risk) y otra información del plan al asignar niveles de importancia.  

        Al asignar niveles de importancia, también puede elegir la decisión de actualización.  

    4. Seleccione **guardar** cuando haya terminado.  

    5. Repita estos pasos para la **complementos de Office**.  

8. En el menú del plan de implementación, en el **preparar** grupo, seleccione **identificar piloto**.  

    1. Revise los dispositivos recomendados para la prueba piloto.  

    2. Seleccione cada dispositivo y seleccione **agregar piloto**. Si no está de acuerdo con la recomendación, seleccione **reemplazar**.  

        Para obtener más información sobre cómo escritorio Analytics hace que estas recomendaciones, seleccione el icono de información en la esquina superior derecha de la **identificar piloto** panel.



### <a name="next-steps"></a>Pasos siguientes

Avance al siguiente artículo para implementar en dispositivos pilotos.
> [!div class="nextstepaction"]  
> [Implementación piloto](/sccm/desktop-analytics/deploy-pilot)  
