---
title: "Tareas comunes de líneas base de configuración en Configuration Manager | Microsoft Docs"
description: "Aprenda a crear e implementar líneas base de configuración de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 991eff171dce95590a7f050e0d3b07f98c0224b3
ms.openlocfilehash: 5682cacb43af5bf9248446f1c35b08f137bdae9d


---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-system-center-configuration-manager"></a>Tareas comunes para crear e implementar líneas de base de configuración con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Este tema contiene escenarios comunes para obtener información sobre cómo crear e implementar líneas de base de configuración de System Center Configuration Manager.  

 Si ya está familiarizado con la configuración de cumplimiento, encontrará documentación detallada sobre todas las características que usa en los temas [Crear una línea base de configuración](../../compliance/deploy-use/create-configuration-baselines.md) y [Deploy configuration baselines (Implementar líneas de base de configuración)](../../compliance/deploy-use/deploy-configuration-baselines.md).  

 Antes de empezar, lea [Get started with compliance settings in System Center Configuration Manager (Introducción a la configuración de cumplimiento de System Center Configuration Manager)](../../compliance/get-started/get-started-with-compliance-settings.md) para conocer algunos conceptos básicos sobre la configuración de cumplimiento y lea también [Planear y configurar la configuración de cumplimiento](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) para implementar los requisitos previos necesarios.  

## <a name="create-a-configuration-baseline"></a>Crear una línea base de configuración  
 En este ejemplo ha creado un elemento de configuración solo para equipos de Windows 10 que ejecutan el cliente de Configuration Manager.  

 Este elemento de configuración aplica una contraseña necesaria de al menos 6 caracteres en equipos con Windows 10. El elemento de configuración se denomina **Windows 10 Password Enforcement**.  

En el procedimiento siguiente, aprenderá a agregar este elemento de configuración a una línea base de configuración para preparar la implementación.  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Líneas base de configuración**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear línea de base de configuración**.  

4.  En el cuadro de diálogo **Crear línea de base de configuración** , configure lo siguiente:  

    -   **Nombre** : escriba **Contraseñas de Windows 10** (u otro nombre de su elección).  

5.  Haga clic en **Agregar** > **Elementos de configuración**.  

6.  En el cuadro de diálogo **Agregar elementos de configuración** , seleccione el elemento de configuración **Windows 10 Password Enforcement** previamente creado y, a continuación, haga clic en **Agregar**.  

7.  Haga clic en Aceptar para cerrar el cuadro de diálogo **Agregar elementos de configuración** y vuelva al cuadro de diálogo **Crear línea de base de configuración** que debe ser similar a esta captura de pantalla:  

     ![Cuadro de diálogo Crear línea de base de configuración](/sccm/compliance/plan-design/media/Create-Configuration-Baseline.png)  

8.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Crear línea de base de configuración** .  

 Ahora puede ver la línea base de configuración que acaba de crear en el nodo **Líneas de base de configuración** de la consola de Configuration Manager.  

## <a name="deploy-the-configuration-baseline"></a>Implementar la línea base de configuración  
 En este ejemplo, va a implementar la línea base de configuración que creó en el procedimiento anterior para una recopilación de equipos.  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Líneas base de configuración**.  

3.  En la lista de líneas base de configuración, seleccione **Contraseñas de Windows 10**.  

4.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.  

5.  En el cuadro de diálogo **Crear líneas de base de configuración** , configure lo siguiente:  

    -   **Líneas de base de configuración seleccionadas** : asegúrese de que la línea base de configuración de **Contraseñas de Windows 10** se agregó automáticamente a esta lista.  

    -   **Corregir las reglas no compatibles cuando se admita**: active esta casilla para garantizar que si la configuración correcta no está presente en los dispositivos de destino, Configuration Manager la corregirá.  

    -   **Recopilación** : haga clic en **Examinar** para elegir la recopilación de equipos en la que se evaluará la línea base de configuración y se corregirá para cumplimiento. En este ejemplo, la línea base de configuración se implementó en la recopilación integrada de **Todos los clientes de escritorio y servidor** .  

        > [!TIP]  
        >  No se preocupe si la recopilación que elige contiene equipos o dispositivos que no ejecutan Windows 10. Siempre que haya configurado plataformas admitidas en el elemento de configuración que creó, se evaluarán solo los equipos con Windows 10 para cumplimiento.  

    -   Si es necesario, configure la programación por la que se evaluará la línea base de configuración. De lo contrario, mantenga el valor predeterminado de **7 días**.  

6.  El cuadro de diálogo será ahora similar a:  

     ![Cuadro de diálogo Implementar líneas base de configuración](/sccm/compliance/plan-design/media/Deploy-configuration-baselines.png)  

7.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Implementar líneas de base de configuración** y crear la implementación.  

 Si quiere echar un vistazo rápido a las estadísticas de cumplimiento para esta implementación, en el área de trabajo **Supervisión** , haga clic en **Implementaciones**. En la parte inferior de la pantalla, verá un gráfico **Estadísticas de compatibilidad** .  

 Para más información sobre cómo supervisar líneas de base de configuración, vea [Monitor compliance settings (Supervisar la configuración de cumplimiento)](../../compliance/deploy-use/monitor-compliance-settings.md)  



<!--HONumber=Jan17_HO4-->


