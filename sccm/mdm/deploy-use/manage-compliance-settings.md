---
title: "Administración del cumplimiento en dispositivos administrados con Intune | Microsoft Docs"
description: "Obtenga información sobre la configuración de cumplimiento de System Center Configuration Manager al repasar algunos escenarios comunes."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e83007f-e81c-4b7e-b47e-b01d7b19cfbc
caps.latest.revision: "5"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: b3a63f6c55c317c9c84d4394dfdcb9f1cbbbc90b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="managing-compliance-on-devices-managed-with-intune"></a>Administración del cumplimiento en dispositivos administrados con Intune

*Se aplica a: System Center Configuration Manager (rama actual)*

Estos escenarios ofrecen una introducción al uso de la configuración de cumplimiento de System Center Configuration Manager al repasar algunos escenarios habituales que podría encontrarse.  

 Si ya está familiarizado con la configuración de cumplimiento, encontrará documentación detallada sobre todas las características que usa en la sección [Elementos de configuración para dispositivos administrados con Intune](#configuration-items-for-devices-managed-with-intune).  

 [Introducción a la configuración de cumplimiento](../../compliance/get-started/get-started-with-compliance-settings.md) proporciona conceptos básicos sobre la configuración de cumplimiento y [Planear y configurar la configuración de cumplimiento](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) le ayuda a implementar todos los requisitos previos necesarios.  

## <a name="general-information-for-each-scenario"></a>Información general de cada escenario  
 En cada escenario, creará un elemento de configuración que realiza una tarea específica. Abra el Asistente para crear elemento de configuración y siga estos pasos:  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Elementos de configuración**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear elemento de configuración**.  

4.  En la pestaña **General** del Asistente para crear elemento de configuración que se muestra a continuación, especifique un nombre y una descripción para el elemento de configuración y luego elija el tipo de elemento de configuración adecuado para cada escenario de este tema.  

     ![Muestra la página general del Asistente para crear elemento de configuración.](media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-81-and-windows-10-devices-managed-with-intune"></a>Escenarios para dispositivos Windows 8.1 y Windows 10 administrados con Intune  

### <a name="scenario-restrict-access-to-the-app-store-on-all-windows-pcs"></a>Escenario: restringir el acceso a la tienda de aplicaciones en todos los equipos Windows  
 En este escenario, usted es el administrador de TI de una compañía que se encarga de información sumamente confidencial. Debido a esto, restringe las aplicaciones que los usuarios pueden instalar. Quiere impedir que los usuarios de todos los equipos con Windows 10 descarguen aplicaciones de la Tienda Windows, por lo que toma las siguiente medidas.  

1.  En la página **General** del Asistente para crear elemento de configuración, seleccione el tipo de elemento de configuración **Windows 8.1 y Windows 10** y luego haga clic en **Siguiente**.  

2.  En la página **Plataformas admitidas**, seleccione todas las plataformas Windows 10.  

3.  En la página **Configuración del dispositivo** , seleccione **Tienda**y haga clic en **Siguiente**.  

4.  En la página **Tienda** , seleccione **Prohibido** como el valor de **Tienda de aplicaciones**.  

5.  Seleccione **Corregir configuraciones no compatibles** para asegurarse de que el cambio se aplique en todos los equipos.  

6.  Complete el asistente para crear el elemento de configuración.  

 Ahora puede usar la información del tema [Tareas comunes para crear e implementar líneas de base de configuración](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) como ayuda para implementar la configuración que ha creado en los dispositivos.  

## <a name="scenarios-for-windows-phone-devices-managed-with-intune"></a>Escenarios para dispositivos Windows Phone administrados con Intune  

### <a name="scenario-disable-the-use-of-screen-capture-on-a-windows-phone"></a>Escenario: deshabilitar el uso de la captura de pantalla en Windows Phone  
 En este escenario, se usan dispositivos Windows Phone 8.1 en su empresa. Estos dispositivos ejecuten una aplicación de ventas que contiene información confidencial. Para proteger la empresa, quiere deshabilitar el uso de la función de captura de pantalla en el dispositivo, ya que podría usarse potencialmente para transmitir información confidencial fuera de la empresa.  

1.  En la página **General** del Asistente para crear elemento de configuración, seleccione el tipo de elemento de configuración **Windows Phone** y luego haga clic en **Siguiente**.  

2.  En la página **Plataformas admitidas**, seleccione **Todo Windows Phone 8.1** como el valor para las plataformas.  

3.  En la página **Configuración del dispositivo** , seleccione **Dispositivo**y haga clic en **Siguiente**.  

4.  En el **Dispositivo** página, seleccione **Deshabilitado** como el valor de **Captura de pantalla**.  

5.  Seleccione **Corregir configuraciones no compatibles** para asegurarse de que el cambio se aplique en todos los dispositivos Windows Phone 8.1.  

6.  Complete el asistente para crear el elemento de configuración.  

 Ahora puede usar la información del tema [Tareas comunes para crear e implementar líneas de base de configuración con System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) como ayuda para implementar la configuración que ha creado en los dispositivos.  

## <a name="scenarios-for-ios-and-mac-os-x-devices-managed-with-intune"></a>Escenarios para dispositivos iOS y Mac OS X administrados con Intune  

### <a name="scenario-disable-the-camera-on-ios-devices"></a>Escenario: deshabilitar la cámara en dispositivos iOS  
 En este escenario, la empresa produce planos de los nuevos diseños de producto. Estos planos contienen información confidencial que no debe divulgarse. Dado que la compañía ofrece dispositivos iPhone o iPad a todos los empleados, quiere deshabilitar el uso de la cámara en estos dispositivos para evitar que se tomen fotografías de los planos.  

1.  En la página **General** del Asistente para crear elemento de configuración, seleccione el tipo de elemento de configuración **iOS y Mac OS X** y luego haga clic en **Siguiente**.  

2.  En la página **Plataformas admitidas**, seleccione todas las plataformas de dispositivos iPhone e iPad.  

3.  En la página **Configuración del dispositivo** , seleccione **Seguridad**y haga clic en **Siguiente**.  

4.  En la página **Seguridad** , seleccione **Prohibido** como el valor de **Cámara**.  

5.  Seleccione **Corregir configuraciones no compatibles** para asegurarse de que el cambio se aplique en todos los dispositivos iOS.  

6.  Complete el asistente para crear el elemento de configuración.  

 Ahora puede usar la información del tema [Tareas comunes para crear e implementar líneas de base de configuración con System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) como ayuda para implementar la configuración que ha creado en los dispositivos.  

## <a name="scenarios-for-android-and-samsung-knox-standard-devices-managed-with-intune"></a>Escenarios para dispositivos Android y Samsung KNOX Standard administrados con Intune  

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

## <a name="configuration-items-for-devices-managed-with-intune"></a>Elementos de configuración para dispositivos administrados con Intune

Los siguientes tipos de elementos de configuración de System Center Configuration Manager están disponibles para dispositivos que no administrada el cliente de Configuration Manager, por ejemplo, los dispositivos que están inscritos en Microsoft Intune.  

 -   [Creación de elementos de configuración para dispositivos Windows 8.1 y Windows 10 administrados con Intune](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)  

 -   [Creación de elementos de configuración para dispositivos Windows Phone administrados con Intune](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)  

 -   [Creación de elementos de configuración para dispositivos iOS y Mac OS X administrados con Intune](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)  

 -   [Creación de elementos de configuración para dispositivos Android y Samsung KNOX Standard administrados con Intune](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)  
