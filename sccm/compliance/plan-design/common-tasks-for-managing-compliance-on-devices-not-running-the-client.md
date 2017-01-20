---
title: Tareas comunes para administrar el cumplimiento en dispositivos sin el cliente de System Center Configuration Manager | System Center Configuration Manager
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
ms.assetid: 116cca2a-0a98-43fd-ac9e-e3daeddefce3
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f69250fbe51ea8902a0446a613d66be390ea7434


---
# <a name="common-tasks-for-managing-compliance-on-devices-not-running-the-system-center-configuration-manager-client"></a>Tareas comunes para administrar el cumplimiento en dispositivos que no ejecutan el cliente de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Estos escenarios ofrecen una introducción al uso de la configuración de cumplimiento de System Center Configuration Manager al repasar algunos escenarios habituales que podría encontrarse.  

 Si ya está familiarizado con la configuración de cumplimiento, encontrará documentación detallada sobre todas las características que usa en la sección [Configuration items for devices managed without the System Center Configuration Manager client (Elementos de configuración de dispositivos administrados sin el cliente de System Center Configuration Manager)](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md).  

 Antes de empezar, lea [Get started with compliance settings (Introducción a la configuración de cumplimiento)](../../compliance/get-started/get-started-with-compliance-settings.md) para conocer algunos conceptos básicos sobre la configuración de cumplimiento y lea también [Planear y configurar las opciones de cumplimiento](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) para implementar los requisitos previos necesarios.  

## <a name="general-information-for-each-scenario"></a>Información general de cada escenario  
 En cada escenario, creará un elemento de configuración que realiza una tarea específica. Abra el Asistente para crear elemento de configuración y siga estos pasos:  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Elementos de configuración**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear elemento de configuración**.  

4.  En la pestaña **General** del Asistente para crear elemento de configuración que se muestra a continuación, especifique un nombre y una descripción para el elemento de configuración y luego elija el tipo de elemento de configuración adecuado para cada escenario de este tema.  

     ![Muestra la página general del Asistente para crear elemento de configuración.](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-81-and-windows-10-devices-managed-without-the-configuration-manager-client"></a>Escenarios para dispositivos Windows 8.1 y Windows 10 administrados sin el cliente de Configuration Manager  

### <a name="scenario-restrict-access-to-the-app-store-on-all-windows-pcs"></a>Escenario: restringir el acceso a la tienda de aplicaciones en todos los equipos Windows  
 En este escenario, usted es el administrador de TI de una compañía que se encarga de información sumamente confidencial. Debido a esto, restringe las aplicaciones que los usuarios pueden instalar. Quiere impedir que los usuarios de todos los equipos con Windows 10 descarguen aplicaciones de la Tienda Windows, por lo que toma las siguiente medidas.  

#### <a name="steps"></a>Pasos  

1.  En la página **General** del Asistente para crear elemento de configuración, seleccione el tipo de elemento de configuración **Windows 8.1 y Windows 10** y luego haga clic en **Siguiente**.  

2.  En la página **Plataformas admitidas**, seleccione todas las plataformas Windows 10.  

3.  En la página **Configuración del dispositivo** , seleccione **Tienda**y haga clic en **Siguiente**.  

4.  En la página **Tienda** , seleccione **Prohibido** como el valor de **Tienda de aplicaciones**.  

5.  Seleccione **Corregir configuraciones no compatibles** para asegurarse de que el cambio se aplique en todos los equipos.  

6.  Complete el asistente para crear el elemento de configuración.  

 Ahora puede usar la información del tema [Tareas comunes para crear e implementar líneas de base de configuración](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) como ayuda para implementar la configuración que ha creado en los dispositivos.  

## <a name="scenarios-for-windows-phone-devices-managed-without-the-configuration-manager-client"></a>Escenarios para dispositivos Windows Phone administrados sin el cliente de Configuration Manager  

### <a name="scenario-disable-the-use-of-screen-capture-on-a-windows-phone"></a>Escenario: deshabilitar el uso de la captura de pantalla en Windows Phone  
 En este escenario, se usan dispositivos Windows Phone 8.1 en su empresa. Estos dispositivos ejecuten una aplicación de ventas que contiene información confidencial. Para proteger la empresa, quiere deshabilitar el uso de la función de captura de pantalla en el dispositivo, ya que podría usarse potencialmente para transmitir información confidencial fuera de la empresa.  

1.  En la página **General** del Asistente para crear elemento de configuración, seleccione el tipo de elemento de configuración **Windows Phone** y luego haga clic en **Siguiente**.  

2.  En la página **Plataformas admitidas**, seleccione **Todo Windows Phone 8.1** como el valor para las plataformas.  

3.  En la página **Configuración del dispositivo** , seleccione **Dispositivo**y haga clic en **Siguiente**.  

4.  En el **Dispositivo** página, seleccione **Deshabilitado** como el valor de **Captura de pantalla**.  

5.  Seleccione **Corregir configuraciones no compatibles** para asegurarse de que el cambio se aplique en todos los dispositivos Windows Phone 8.1.  

6.  Complete el asistente para crear el elemento de configuración.  

 Ahora puede usar la información del tema [Tareas comunes para crear e implementar líneas de base de configuración con System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) como ayuda para implementar la configuración que ha creado en los dispositivos.  

## <a name="scenarios-for-ios-and-mac-os-x-devices-managed-without-the-configuration-manager-client"></a>Escenarios para dispositivos iOS y Mac OS X administrados sin el cliente de Configuration Manager  

### <a name="scenario-disable-the-camera-on-ios-devices"></a>Escenario: deshabilitar la cámara en dispositivos iOS  
 En este escenario, la empresa produce planos de los nuevos diseños de producto. Estos planos contienen información confidencial que no debe divulgarse. Dado que la compañía ofrece dispositivos iPhone o iPad a todos los empleados, quiere deshabilitar el uso de la cámara en estos dispositivos para evitar que se tomen fotografías de los planos.  

1.  En la página **General** del Asistente para crear elemento de configuración, seleccione el tipo de elemento de configuración **iOS y Mac OS X** y luego haga clic en **Siguiente**.  

2.  En la página **Plataformas admitidas**, seleccione todas las plataformas de dispositivos iPhone e iPad.  

3.  En la página **Configuración del dispositivo** , seleccione **Seguridad**y haga clic en **Siguiente**.  

4.  En la página **Seguridad** , seleccione **Prohibido** como el valor de **Cámara**.  

5.  Seleccione **Corregir configuraciones no compatibles** para asegurarse de que el cambio se aplique en todos los dispositivos iOS.  

6.  Complete el asistente para crear el elemento de configuración.  

 Ahora puede usar la información del tema [Tareas comunes para crear e implementar líneas de base de configuración con System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) como ayuda para implementar la configuración que ha creado en los dispositivos.  

## <a name="scenarios-for-android-and-samsung-knox-devices-managed-without-the-configuration-manager-client"></a>Escenarios para dispositivos Android y Samsung KNOX administrados sin el cliente de Configuration Manager  

### <a name="scenario-require-a-password-on-all-android-5-devices"></a>Escenario: requerir una contraseña en todos los dispositivos Android 5  
 En este escenario, creará un elemento de configuración para dispositivos Android 5 que solo requerirá a los usuarios que configuren una contraseña de seis caracteres como mínimo en sus dispositivos. Además, si un usuario escribe una contraseña incorrecta cinco veces, se borra el dispositivo.  

1.  En la página **General** del Asistente para crear elemento de configuración, seleccione el tipo de elemento de configuración **Android y Samsung KNOX** y luego haga clic en **Siguiente**.  

2.  En la página **Plataformas admitidas**, seleccione solo **Android 5** (para asegurarse de que la configuración se aplique solo a esa plataforma).  

3.  En la página **Configuración del dispositivo** , seleccione **Contraseña**y haga clic en **Siguiente**.  

4.  En la página **Contraseña** , configure las siguientes opciones:  

    -   **Requerir configuración de contraseña en dispositivos** > **Obligatorio**  

    -   **Longitud de contraseña mínima (caracteres)** > **6**  

    -   **Número de intentos de inicio de sesión incorrectos antes de que se borre el dispositivo** > **5**  

5.  Complete el asistente para crear el elemento de configuración.  

 Ahora puede usar la información del tema [Tareas comunes para crear e implementar líneas de base de configuración](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) como ayuda para implementar la configuración que ha creado en los dispositivos.  




<!--HONumber=Nov16_HO1-->


