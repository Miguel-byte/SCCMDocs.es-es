---
title: Tareas comunes de administración de cumplimiento
titleSuffix: Configuration Manager
description: Aprenda sobre la configuración de cumplimiento de Configuration Manager mediante el trabajo sobre algunos escenarios comunes.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: da92506d291ca24af807db7b4f4b73473359e12f
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70890649"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-configuration-manager-client"></a>Tareas comunes para administrar el cumplimiento en dispositivos con el cliente de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se ofrece una introducción al uso de la configuración de cumplimiento de System Center Configuration Manager, que le guiará a través de algunos escenarios comunes que podría encontrar.  

 Si ya está familiarizado con la configuración de cumplimiento, encontrará documentación detallada sobre todas las características que usa en la sección [Elementos de configuración de dispositivos administrados con el cliente de System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items.md).  

 Antes de empezar, Lea Introducción a la [configuración de cumplimiento](../../compliance/get-started/get-started-with-compliance-settings.md) para conocer algunos aspectos básicos sobre la configuración de cumplimiento. Lea [Plan for and configure Compliance Settings](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) para obtener información sobre los requisitos previos necesarios.  

## <a name="general-information-for-each-scenario"></a>Información general de cada escenario  
 En cada escenario, creará un elemento de configuración que realiza una tarea específica. Para abrir el Asistente para crear elemento de configuración y comenzar, siga estos pasos:  

1.  En la consola de Configuration Manager, seleccione **Activos y compatibilidad** > **Configuración de cumplimiento** > **Elementos de configuración**.  

1.  En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear elemento de configuración**.  

1.  En la página **General** del Asistente para crear elemento de configuración, que se muestra en la siguiente captura de pantalla, especifique un nombre y una descripción para el elemento de configuración. A continuación, elija el tipo de elemento de configuración adecuado para cada escenario de este artículo.  

     ![Página general del Asistente para crear elemento de configuración](/sccm/mdm/deploy-use/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenario-disable-bluetooth-on-windows-10-devices"></a>Escenario: deshabilitar Bluetooth en dispositivos Windows 10

 En este escenario, el departamento de seguridad ha determinado que la funcionalidad Bluetooth de los dispositivos podría usarse para transmitir información corporativa confidencial fuera de la empresa. Recientemente, ha actualizado todos los equipos a Windows 10. Decide deshabilitar Bluetooth en estos dispositivos.  

1. En la página **General** del Asistente para crear elemento de configuración, seleccione el tipo de elemento de configuración **Windows 10** y, luego, haga clic en **Siguiente**.  

2. En la página **Plataformas admitidas** del asistente, seleccione todas las plataformas Windows 10.  

3. En la página **configuración del dispositivo** , seleccione **dispositivo**y, a continuación, seleccione **siguiente**.  

4. En la página **Dispositivo** , seleccione **Prohibido** como el valor de **Bluetooth**.  

5. Seleccione **Corregir configuraciones no compatibles** para asegurarse de que el cambio se aplique en todos los dispositivos Windows 10.  

6. Complete el asistente para crear el elemento de configuración.  

 Ahora puede usar la información del artículo [Tareas comunes para crear e implementar líneas de base de configuración con System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) como ayuda para implementar la configuración que ha creado en los dispositivos.  

## <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Escenario: corregir un valor incorrecto del Registro en los equipos de escritorio de Windows

> [!NOTE] 
> En los equipos Mac que ejecutan el cliente de Configuration Manager, hay dos opciones para evaluar el cumplimiento:  
> - Evaluar un archivo de preferencias (.plist) de Mac OS X.
> - Usar un script personalizado y evaluar los resultados devueltos por la secuencia de comandos.  
>
>Para más información, vea [How to create configuration items for Mac OS X devices managed with the System Center Configuration Manager client (Cómo crear elementos de configuración para dispositivos Mac OS X administrados con el cliente de System Center Configuration Manager)](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

 En este escenario, descubre que una aplicación de línea de negocio importante no se ejecuta correctamente en algunos Windows 8.1 equipos que administra. Determinará que la causa es una clave del Registro denominada **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** que tiene establecido un valor de **0** en algunos equipos. Para que la aplicación de línea de negocio se ejecute correctamente, este valor debe establecerse en **1**.  

 En este procedimiento, creará un elemento de configuración que supervise y corrija automáticamente los valores incorrectos de clave del Registro que ha detectado.  

1. En la página **General** del Asistente para crear elemento de configuración, seleccione el tipo de elemento de configuración **Escritorios y servidores de Windows (personalizado)** y luego seleccione **Siguiente**.  

2. En la página **Plataformas admitidas** del asistente, seleccione **Windows 8.1** (para asegurarse de que el elemento de configuración solo se aplique a los equipos afectados).  

3. En la página **Configuración**, seleccione **Nuevo** para crear una nueva configuración.  

4. En la pestaña **General** del cuadro de diálogo **Crear configuración**, configure los siguientes valores:  

   -   **Nombre** > **Configuración de ejemplo**  

   -   **Tipo de configuración** > **Valor del Registro**  

   -   **Tipo de datos** > **Entero** (porque el valor contiene solo un número)  

   -   **Subárbol** > **HKEY_LOCAL_MACHINE**  

   -   **Clave** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

   -   **Valor** > **1** (el valor necesario)  

5. En la pestaña **reglas de compatibilidad** del cuadro de diálogo **crear configuración** , seleccione **nuevo**. En el cuadro de diálogo **crear regla** , configure estas opciones:  

   -   **Nombre** > **Regla de ejemplo**  

   -   **Configuración seleccionada**: compruebe que la configuración seleccionada sea **Configuración de ejemplo**.

   -   **Tipo de regla** > **Valor**  

   -   **La configuración debe ser compatible con la regla siguiente**: compruebe que el nombre de la configuración sea correcto y configure la opción para especificar que el valor de configuración debe ser igual a **1**.  

   -   **Corregir las reglas no compatibles cuando se admita**: active esta casilla para garantizar que Configuration Manager restablecerá el valor de la clave del Registro al valor correcto, si no lo era.  

6. Complete el asistente para crear el elemento de configuración.  

 Ahora puede usar la información del artículo [Tareas comunes para crear e implementar líneas de base de configuración](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) como ayuda para implementar la configuración que ha creado en los dispositivos.  

## <a name="next-steps"></a>Pasos siguientes

[Crear e implementar líneas base de configuración](/sccm/compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines)
