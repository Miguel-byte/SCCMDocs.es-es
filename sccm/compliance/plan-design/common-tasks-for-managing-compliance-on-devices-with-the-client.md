---
title: Tareas comunes para administrar el cumplimiento en dispositivos con el cliente de System Center Configuration Manager | System Center Configuration Manager
description: "Obtenga información sobre la configuración de cumplimiento de System Center Configuration Manager al repasar algunos escenarios comunes."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9be045df8433463d01d6cfca9271f230b5bf991d


---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-system-center-configuration-manager-client"></a>Tareas comunes para administrar el cumplimiento en dispositivos que tienen el cliente de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los escenarios de este tema ofrecen una introducción al uso de la configuración de cumplimiento de System Center Configuration Manager al repasar algunos escenarios habituales que podría encontrarse.  

 Si ya está familiarizado con la configuración de cumplimiento, encontrará documentación detallada sobre todas las características que usa en la sección [Configuration items for devices managed with the System Center Configuration Manager client (Elementos de configuración de dispositivos administrados con el cliente de System Center Configuration Manager)](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md).  

 Antes de empezar, lea [Get started with compliance settings (Introducción a la configuración de cumplimiento)](../../compliance/get-started/get-started-with-compliance-settings.md) para conocer algunos conceptos básicos sobre la configuración de cumplimiento y lea también [Planear y configurar las opciones de cumplimiento](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) para implementar los requisitos previos necesarios.  

## <a name="general-information-for-each-scenario"></a>Información general de cada escenario  
 En cada escenario, creará un elemento de configuración que realiza una tarea específica. Abra el Asistente para crear elemento de configuración y siga estos pasos:  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Elementos de configuración**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear elemento de configuración**.  

4.  En la pestaña **General** del Asistente para crear elemento de configuración que se muestra a continuación, especifique un nombre y una descripción para el elemento de configuración y luego elija el tipo de elemento de configuración adecuado para cada escenario de este tema.  

     ![Muestra la página general del Asistente para crear elemento de configuración.](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-10-devices-managed-with-the-configuration-manager-client"></a>Escenarios para dispositivos Windows 10 administrados con el cliente de Configuration Manager  

### <a name="scenario-disable-the-use-of-bluetooth-on-windows-10-devices"></a>Escenario: deshabilitar el uso de Bluetooth en dispositivos Windows 10  
 En este escenario, el departamento de seguridad ha identificado la característica Bluetooth en los dispositivos como un medio que podría usarse para transmitir información corporativa confidencial fuera de la empresa. Recientemente ha actualizado todos los equipos a Windows 10 y ahora decide deshabilitar la característica Bluetooth en estos dispositivos.  

1.  En la página **General** del Asistente para crear elemento de configuración, seleccione el tipo de elemento de configuración **Windows 10** y luego haga clic en **Siguiente**.  

2.  En la página **Plataformas admitidas** del asistente, seleccione todas las plataformas Windows 10.  

3.  En la página **Configuración del dispositivo** , seleccione **Dispositivo**y haga clic en **Siguiente**.  

4.  En la página **Dispositivo** , seleccione **Prohibido** como el valor de **Bluetooth**.  

5.  Seleccione **Corregir configuraciones no compatibles** para asegurarse de que el cambio se aplique en todos los dispositivos Windows 10.  

6.  Complete el asistente para crear el elemento de configuración.  

 Ahora puede usar la información del tema [Tareas comunes para crear e implementar líneas de base de configuración con System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) como ayuda para implementar la configuración que ha creado en los dispositivos.  

## <a name="scenarios-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Escenarios para equipos de escritorio y servidores de Windows administrados con el cliente de Configuration Manager  
 En los equipos Mac que ejecutan el cliente de Configuration Manager, hay dos opciones para evaluar el cumplimiento:  

-   Evaluar un archivo de preferencias (.plist) de Mac OS X.  

-   Usar un script personalizado y evaluar los resultados devueltos por la secuencia de comandos.  

 Para más información, vea [How to create configuration items for Mac OS X devices managed with the System Center Configuration Manager client (Cómo crear elementos de configuración para dispositivos Mac OS X administrados con el cliente de System Center Configuration Manager)](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

### <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Escenario: corregir un valor incorrecto del Registro en los equipos de escritorio de Windows  
 En este escenario, descubre que una aplicación de línea de negocio importante no se ejecuta correctamente en algunos equipos que usted administra y que ejecutan Windows 8.1. Después de investigar, descubre que la causa es una clave del Registro denominada **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** que tiene establecido un valor de **0** en algunos equipos. Para que la aplicación de línea de negocio se ejecute correctamente, este valor debe establecerse en **1**.  

 En este procedimiento, creará un elemento de configuración que supervise y corrija automáticamente los valores incorrectos de clave del Registro que ha detectado.  

1.  En la página **General** del Asistente para crear elemento de configuración, seleccione el tipo de elemento de configuración **Escritorios y servidores de Windows (personalizado)** y luego haga clic en **Siguiente**.  

2.  En la página **Plataformas admitidas** del asistente, seleccione **Windows 8.1** (para asegurarse de que el elemento de configuración solo se aplique a los equipos afectados).  

3.  En la página **Configuración** , haga clic en **Nuevo** para crear una nueva configuración.  

4.  En la pestaña **General** del cuadro de diálogo **Crear configuración** , configure los siguientes elementos:  

    -   **Nombre** > **Configuración de ejemplo**  

    -   **Tipo de configuración** > **Valor del Registro**  

    -   **Tipo de datos** > **Entero** (porque el valor contiene solo un número)  

    -   **Subárbol** > **HKEY_LOCAL_MACHINE**  

    -   **Clave** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

    -   **Valor** > **1** (el valor necesario)  

5.  En la pestaña **Reglas de compatibilidad** del cuadro de diálogo **Crear configuración** , haga clic en **Nuevo**y luego, en el cuadro de diálogo **Crear regla** , configure los elementos siguientes:  

    -   **Nombre** > **Regla de ejemplo**  

    -   **Configuración seleccionada** : compruebe que la configuración seleccionada sea **Configuración de ejemplo**.  

    -   **Tipo de regla** > **Valor**  

    -   **La configuración debe ser compatible con la regla siguiente** : compruebe que el nombre de la configuración sea correcto y configure la opción para especificar que el valor de configuración debe ser igual a **1**.  

    -   **Corregir las reglas no compatibles cuando se admita**: active esta casilla para garantizar que Configuration Manager restablecerá el valor de la clave del Registro al valor correcto, si no lo era.  

6.  Complete el asistente para crear el elemento de configuración.  

 Ahora puede usar la información del tema [Tareas comunes para crear e implementar líneas de base de configuración](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) como ayuda para implementar la configuración que ha creado en los dispositivos.  



<!--HONumber=Nov16_HO1-->


