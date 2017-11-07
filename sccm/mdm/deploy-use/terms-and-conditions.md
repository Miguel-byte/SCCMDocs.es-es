---
title: "Términos y condiciones"
titleSuffix: Configuration Manager
description: "Implemente términos y condiciones en grupos de usuarios en System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d3f9e6b-4d71-4fc4-9b91-47f1bfbd8c70
caps.latest.revision: "9"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: f616212b216ad4c94b60c7a805e2f45071947e81
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="add-terms-and-conditions-with-system-center-configuration-manager"></a>Incorporación de términos y condiciones con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede implementar los términos y condiciones de System Center Configuration Manager en los grupos de usuarios para explicar en qué afecta la inscripción del dispositivo, el acceso a los recursos de trabajo y el uso del portal de empresa a los dispositivos y los usuarios. Los usuarios deben aceptar los términos y las condiciones para poder usar el portal de empresa a fin de inscribirse y obtener acceso a su trabajo.  

 ## <a name="working-with-terms-and-conditions-policies-in-system-center-configuration-manager"></a>Trabajo con directivas de términos y condiciones en System Center Configuration Manager  
 Puede crear e implementar un conjunto múltiple de términos y condiciones. También puede generar versiones de los mismos términos y condiciones en distintos idiomas e implementarlas en los grupos correspondientes.  

## <a name="to-create-a-terms-and-conditions"></a>Crear términos y condiciones  

1.  En la consola de Administrador de configuración, vaya a **Activos y compatibilidad** > **Introducción** > **Configuración de cumplimiento** > **Términos y condiciones**.  

2.  Haga clic en **Crear términos y condiciones** para crear los nuevos términos y condiciones.  

3.  En la página **General** , especifique la siguiente información:  

    -   **Nombre**: nombre único que aparece en la consola de Configuration Manager  

    -   **Descripción**: detalles que le ayudan a identificar los términos y condiciones en la consola de Configuration Manager  

     A continuación, haga clic en **Siguiente**.  

4.  En la página **Términos** , especifique la siguiente información:  

    -   **Título** : título que se muestra a los usuarios en el portal de empresa  

    -   **Texto para los términos** : los términos y condiciones que se muestran a los usuarios en el portal de empresa  

    -   **Texto para explicar qué significa si el usuario acepta** : los usuarios de etiqueta lo ven según la aceptación. **Ejemplo**: "Acepto los términos y condiciones".  

     A continuación, haga clic en **Siguiente**.  

5.  Complete el asistente para crear nuevos términos y condiciones. Los nuevos términos y condiciones que se muestran en el nodo Términos y condiciones del área de trabajo Activos y compatibilidad.  

## <a name="to-deploy-a-terms-and-conditions"></a>Implementar términos y condiciones  

1.  En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Introducción** > **Configuración de compatibilidad** > **Términos y condiciones**.  

2.  En la lista **Términos y condiciones** , seleccione el elemento que desea implementar y, luego, haga clic en **Implementar**.  

3.  **Examinar** la **Recopilación** en la que quiere implementar los términos y condiciones y luego haga clic en **Aceptar**.  

     Cuando los dispositivos de destino tienen acceso a la aplicación del portal de empresa, esta muestra los términos y las condiciones que implementó. Los usuarios deben aceptar estos términos para tener acceso a los recursos de la empresa.  

    > [!NOTE]  
    >  Si implementa un conjunto de términos en varias recopilaciones de usuario a las que pertenece un usuario, dicho usuario verá varias copias de términos idénticas al abrir el portal de empresa. Puesto que los usuarios solo pueden aceptar o rechazar todos los términos, no existe riesgo de estar en un estado de aceptación ambigua donde el usuario ha aceptado y rechazado los términos al mismo tiempo. El informe de aceptación de términos y condiciones solo incluirá una fila para cada conjunto de términos de cada usuario, de modo que no hay ningún error en el informe.  

## <a name="to-monitor-terms-and-conditions"></a>Para supervisar términos y condiciones  

1.  Puede supervisar las implementaciones de términos y condiciones en la consola de Configuration Manager. En la consola de Configuration Manager, vaya a **Supervisión** > **Información general** > **Implementaciones**.  

2.  Seleccione la implementación de términos y condiciones en la lista de implementaciones.  

     El área de resumen muestra las estadísticas siguientes:  

    -   **Conforme** : los usuarios han aceptado la versión más reciente de los términos y condiciones  

    -   **Error**  

    -   **No conforme** : los usuarios han aceptado una versión de los términos y condiciones, pero no la más reciente  

    -   **Desconocido** : los usuarios no han aceptado nunca los términos y condiciones, incluidos aquellos sin un dispositivo inscrito  

3.  Seleccione una implementación de términos y condiciones y **Ejecutar resumen** para ver el estado de la implementación de los usuarios individuales.  

     En la pantalla de estado de la implementación, puede seleccionar las pestañas de estado para ver los usuarios con ese estado. Puede hacer clic en **Ejecutar resumen** para actualizar los datos en toda la jerarquía. Haga clic en **Actualizar** para actualizar datos en la consola.  

## <a name="to-view--a-terms-and-conditions-report"></a>Para ver un informe de términos y condiciones  

1.  En la consola de Configuration Manager, vaya **Supervisión** > **Información general** > **Creación de informes** > **Informe**.  

2.  Seleccione la **Aceptación de los términos y condiciones** y haga clic en **Ejecutar**. Se abre el informe de aceptación de términos y condiciones. El informe muestra cada usuario para los que se han implementado los términos y condiciones. Los campos son los siguientes:  

    -   Nombre de los términos y condiciones  

    -   Nombre de usuario  

    -   Versión aceptada  

    -   Fecha de aceptación  

    -   Aceptación más reciente  

## <a name="updates-and-version-control-for-terms-and-conditions"></a>Actualizaciones y control de versiones de los términos y condiciones  
 Al editar los términos y condiciones existentes, puede elegir el comportamiento al implementar los términos y condiciones. Use el procedimiento siguiente, que le ayudará a actualizar los términos y condiciones existentes.  

### <a name="how-to-work-with-multiple-versions-of-terms-and-conditions"></a>Cómo trabajar con varias versiones de los términos y las condiciones  

1.  En la consola de Administrador de configuración, vaya a **Activos y compatibilidad** > **Introducción** > **Configuración de cumplimiento** > **Términos y condiciones**.  

2.  Seleccione la instancia de términos y condiciones que quiere modificar y luego haga doble clic para abrirla.  

3.  Puede modificar el contenido en la página **General** o **Términos** para realizar cualquier edición que sea necesaria.  

4.  En la página **Términos** , puede especificar si esta nueva versión requiere que todos los usuarios acepten los términos y las condiciones, o si solo los usuarios nuevos verán la versión nueva.  

     Se recomienda aumentar el número de versión y requerir aceptación cada vez que realice cambios importantes los términos y condiciones. Si va a corregir errores tipográficos o cambiar el formato, por ejemplo, mantenga el número de versión actual.

> [!div class="button"]
[< Paso anterior](configure-intune-subscription.md)  [Paso siguiente >](create-service-connection-point.md)
