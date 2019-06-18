---
title: Cómo crear planes de implementación
titleSuffix: Configuration Manager
description: Guía de procedimientos para crear planes de implementación en escritorio Analytics.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 696d2ecedc659330715d42c05ecc046f0a6cc7ff
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159168"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Cómo crear planes de implementación en escritorio Analytics

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

En este artículo proporciona los pasos para crear un plan de implementación en escritorio Analytics. Antes de empezar, primero [Obtenga información sobre los planes de implementación](/sccm/desktop-analytics/about-deployment-plans).

## <a name="create-a-plan-for-windows-10"></a>Crear un plan para Windows 10

Siga los pasos descritos en esta sección para usar análisis de escritorio para crear un plan para implementar Windows 10.

1. Abra el [portal de análisis de escritorio](https://aka.ms/desktopanalytics). Use las credenciales que tienen al menos **colaboradores del área de trabajo** permisos.  

2. Seleccione **planes de implementación** en el grupo de administración.  

3. En el **planes de implementación** panel, seleccione **crear**.  

4. En el **Crear plan de implementación** panel, configure las siguientes opciones:  

    - **Nombre**: Un nombre único para el plan de implementación  

    - **Productos y versiones**: Elija qué versión de Windows 10 para implementar. Microsoft recomienda crear planes de implementación que usan la versión más reciente.  

    - **Grupos de dispositivos**: Seleccione uno o más grupos y, a continuación, seleccione **establecer como destino grupos**. Grupos con **SCCM** como el origen son colecciones sincronizadas desde Configuration Manager.  

    - **Las reglas de preparación**: Estas reglas ayudan a determinar qué dispositivos necesarios para actualización. Para obtener más información, consulte [reglas de preparación](#readiness-rules).  

    - **Fecha de finalización**: Elija la fecha por el que se deberían implementar totalmente Windows en todos los dispositivos de destino.  

5. Seleccione **crear**. El nuevo plan aparece en la lista de planes de implementación mientras se está procesando. Para acelerar el procesamiento, solicitar una actualización de datos y a petición. Para obtener más información, consulte [preguntas más frecuentes sobre análisis de escritorio](/sccm/desktop-analytics/faq##can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

6. Abrir el plan de implementación, seleccione su nombre.  

7. En el menú del plan de implementación, en el **preparar** grupo, seleccione **identificar importancia**.  

    1. En el **aplicaciones** pestaña, seleccione esta opción para mostrar sólo **no revisado** activos.  

    2. Seleccione cada aplicación y, a continuación, seleccione **editar**. Puede seleccionar más de una aplicación para editar al mismo tiempo.  

    3. Elija un nivel de importancia de la **importancia** lista. Si desea que el análisis de escritorio para validar la aplicación durante el programa piloto, seleccione **crítico** o **importante**. No valida las aplicaciones marcadas como **importante no**. Evalúe su [compatibilidad](/sccm/desktop-analytics/compat-assessment) y otra información del plan al asignar niveles de importancia.  

        Al asignar niveles de importancia, también puede elegir la decisión de actualización.  

    4. Seleccione **guardar** cuando haya terminado.  

8. En el menú del plan de implementación, en el **preparar** grupo, seleccione **identificar piloto**.  

    1. Revise los dispositivos recomendados para la prueba piloto.  

    2. Seleccione cada dispositivo y seleccione **agregar piloto**. Si no está de acuerdo con la recomendación, seleccione **reemplazar**.  

        Para obtener más información sobre cómo escritorio Analytics hace que estas recomendaciones, seleccione el icono de información en la esquina superior derecha de la **identificar piloto** panel.

## <a name="readiness-rules"></a>Reglas de preparación

Estas reglas ayudan a determinar qué dispositivos cumple los requisitos para la actualización en contexto. Estas reglas se pueden establecer al crear el plan de implementación, o modificarlos más adelante.

Para cambiar las reglas de preparación:

1. En el portal de análisis de escritorio, seleccione el plan de implementación.
1. Junto al nombre, seleccione **editar**.
1. Seleccione **reglas de preparación**.
1. Seleccione **Windows OS**.
1. Realizar cambios según sea necesario y seleccione **guardar**.

Para **Windows OS** las actualizaciones, hay dos reglas: Controladores de dispositivos y aplicaciones de Windows.

### <a name="device-drivers"></a>Controladores de dispositivo

Configurar si los dispositivos obtención controladores desde Windows Update. Este valor es **desactivar** de forma predeterminada. Habilite esta regla cuando usa Windows Update para empresas a administrar actualizaciones de controladores. Si está usando Configuration Manager para administrar las actualizaciones de software, establezca esta regla en **desactivar**.

### <a name="windows-applications"></a>Aplicaciones de Windows

Las aplicaciones que se muestran los análisis de escritorio como *notable* se basan en el umbral de recuento de instalación baja. Establezca este umbral en las reglas de preparación para el plan de implementación. De forma predeterminada, este umbral es **2.0%** . Puede cambiar el valor de `0.0` a `10.0`.


## <a name="next-steps"></a>Pasos siguientes

Avance al siguiente artículo para implementar en dispositivos pilotos.
> [!div class="nextstepaction"]  
> [Implementación piloto](/sccm/desktop-analytics/deploy-pilot)  
