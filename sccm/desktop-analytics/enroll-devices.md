---
title: Inscripción de dispositivos de escritorio Analytics
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo inscribir dispositivos en el escritorio de análisis.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: bfe3094f63440d26a64d8d82cc44007141dd60df
ms.sourcegitcommit: 65753c51fbf596f233fc75a5462ea4a44005c70b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/03/2019
ms.locfileid: "66463010"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Cómo inscribir dispositivos en el escritorio de análisis

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Cuando se [conectar Configuration Manager](/sccm/desktop-analytics/connect-configmgr) para análisis de escritorio, configuración para inscribir dispositivos para el análisis de escritorio. Puede cambiar esta configuración en cualquier momento. Además, asegúrese de que los dispositivos están actualizados.



## <a name="update-devices"></a>Actualizar dispositivos

Hay dos tipos de actualizaciones que necesita para solicitar la mejor experiencia con análisis de escritorio:

- [Actualizaciones de compatibilidad](#bkmk_appraiser)  
- [Servicio de telemetría y experiencias del usuario conectado](#bkmk_diagtrack)


### <a name="bkmk_appraiser"></a> Actualizaciones de compatibilidad

El componente de compatibilidad (Appraiser) ejecuta diagnósticos en el dispositivo de Windows para evaluar su estado de compatibilidad con las versiones más recientes de Windows 10.

Microsoft incrementa regularmente las actualizaciones para este componente, pero no cambia el número KB asociado. Asegúrese de que siempre tiene la versión más reciente de la actualización.

Reiniciar dispositivos después de instalar las actualizaciones de compatibilidad por primera vez.

> [!Tip]  
> Use el Administrador de configuración para instalar automáticamente la versión más reciente de estas actualizaciones. Para obtener más información, consulte [Deploy software updates](/sccm/sum/deploy-use/deploy-software-updates) (Implementación de actualizaciones de software).  

> [!Note]  
> Hay una actualización opcional relacionada, [3150513 KB](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=3150513). Esta actualización proporciona definiciones para las actualizaciones más antiguas de compatibilidad y configuración actualizada. Para obtener más información, consulte [última actualización de definición de compatibilidad de Windows](https://support.microsoft.com/help/3150513).  

#### <a name="windows-10"></a>Windows 10

Windows 10 incluye el componente de compatibilidad. Para obtener la última actualización de compatibilidad, instale la actualización acumulativa más reciente de Windows 10.

#### <a name="windows-81"></a>Windows 8.1

Descargue la actualización: [KB 2976978](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2976978) 

Ejecuta diagnósticos en los sistemas de Windows 8.1 que participan en Windows Customer Experience Improvement Program. Estos diagnósticos ayudan a determinar si es posible que tienen problemas de compatibilidad al actualizar a Windows 10.

Para obtener más información, consulte [Compatibility update para mantener Windows actualizado en Windows 8.1](https://support.microsoft.com/help/2976978).

#### <a name="windows-7-with-service-pack-1"></a>Windows 7 con Service Pack 1

Descargue la actualización: [KB 2952664](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2952664) 

Ejecuta diagnósticos en el 7 de Windows con sistemas de Service Pack 1 (SP1) que participan en Windows Customer Experience Improvement Program. Estos diagnósticos ayudan a determinar si es posible que tienen problemas de compatibilidad al actualizar a Windows 10.

Para obtener más información, consulte [Compatibility update para mantener actualizadas en Windows 7 Windows](https://support.microsoft.com/help/2952664).


### <a name="bkmk_diagtrack"></a> Servicio de telemetría y experiencias del usuario conectado

Con datos de diagnóstico de Windows habilitados, el servicio de la experiencia del usuario y telemetría (DiagTrack) recopila datos del sistema, aplicación y controlador. Microsoft analiza estos datos y lo comparte con usted a través de escritorio de análisis.

Para obtener la mejor experiencia, instale las actualizaciones siguientes en función de la versión del sistema operativo.

> [!Note]  
> Al instalar estas actualizaciones, esperar los comportamientos siguientes:
> 
> - Los dispositivos que inscriba a Desktop Analytics aparecen en el servicio en menos de una hora  
> - Dispositivos rápidamente informan del estado de las actualizaciones de calidad y la característica de Windows  
>
> Sin estas actualizaciones, estos procesos pueden tardar más de 48 horas para un dispositivo notificar al análisis de escritorio.  


#### <a name="windows-10"></a>Windows 10

Instale la actualización acumulativa más reciente de Windows 10.

<!-- 
- Windows 10 1809: Included in RTM build
- Windows 10 1803: [KB4458469](https://support.microsoft.com/help/4458469) (OS Build 17134.319)
- Windows 10 1709: [KB4457136](https://support.microsoft.com/help/4457136) (OS Build 16299.697)
- Windows 10 1703: [KB4457141](https://support.microsoft.com/help/4457141) (OS Build 15063.1358)
- Windows 10 1607: [KB4457127](https://support.microsoft.com/help/4457127) (OS Build 14393.2517)
 -->

#### <a name="windows-81"></a>Windows 8.1

Instalar el paquete mensual de octubre de 2018, [KB4462926](https://support.microsoft.com/help/4462926)

#### <a name="windows-7"></a>Windows 7

Instalar el paquete mensual de octubre de 2018, [KB4462923](https://support.microsoft.com/help/4462923)



## <a name="device-enrollment"></a>Inscripción de dispositivos

El servicio de análisis de escritorio no tiene ningún agente para instalar. Inscripción de dispositivos requiere configuración en los dispositivos que desea supervisar. Esta configuración controla a qué instancia de análisis de escritorio, el dispositivo debe enviar sus datos y otras opciones de configuración.

> [!Note]  
> Si ya utiliza Windows Analytics, use esa misma área de trabajo para el análisis de escritorio. Deberá volver a inscribir dispositivos para el análisis de escritorio que ya tiene inscritos en Windows Analytics.
>
> Solo puede tener un área de trabajo de análisis de escritorio por inquilino de Azure AD. Los dispositivos solo pueden enviar datos de diagnóstico a un área de trabajo.  

Configuration Manager proporciona una experiencia integrada para administrar e implementar estas opciones a los clientes. Para obtener la mejor experiencia, use Configuration Manager.

Cuando se conecta Configuration Manager para el análisis de escritorio, configure la configuración para inscribir dispositivos. Para obtener más información, consulte [cómo conectar Configuration Manager con análisis de escritorio](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

Para cambiar esta configuración, use el procedimiento siguiente:

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**. Seleccione la conexión a escritorio Analytics y elija **propiedades** en la cinta de opciones.

2. En el **datos de diagnóstico** página, realice los cambios necesarios a la siguiente configuración:  

    - **Id. comercial**: este valor se debería rellenar automáticamente con el identificador de. su organización Si no, asegúrese de que el servidor proxy está configurado para permitir que todo lo necesario [extremos](/sccm/desktop-analytics/enable-data-sharing#endpoints) antes de continuar. También puede recuperar el identificador comercial desde el **Connected Services** panel en el [portal de análisis de escritorio](https://aka.ms/m365aprod).   

    - **Nivel de datos de diagnóstico de Windows 10**: Para obtener más información, consulte [niveles de datos de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

    - **Permitir que el nombre del dispositivo en los datos de diagnóstico**: Para obtener más información, consulte [nombre de dispositivo](#device-name).  

    Al realizar cambios en esta página, el **funcionalidad disponible** página muestra una vista previa de la funcionalidad de análisis de escritorio con la configuración de los datos de diagnóstico seleccionado.  

3. En el **Analytics la conexión a escritorio** página, realice los cambios necesarios a la siguiente configuración:

    - **Nombre para mostrar**: El portal de análisis de escritorio muestra esta conexión de Configuration Manager con este nombre.  

    - **Recopilación de destino**: Esta colección incluye todos los dispositivos de Configuration Manager se configura con el Id. comercial y la configuración de datos de diagnóstico. Es el conjunto completo de los dispositivos que Configuration Manager se conecta al servicio de análisis de escritorio.  

    - **Los dispositivos de la recopilación de destino usa un proxy de usuario autenticado para la comunicación saliente**: De forma predeterminada, este valor es **No**. Si es necesario en su entorno, se establece en **Sí**. Para obtener más información, consulte [autenticación del servidor Proxy](/sccm/desktop-analytics/enable-data-sharing#proxy-server-authentication).  

    - **Seleccione las recopilaciones específicas para sincronizar con análisis de escritorio**: Seleccione **agregar** para incluir las colecciones adicionales desde su **recopilación de destino** jerarquía. Estas colecciones están disponibles en el portal de análisis de escritorio para su agrupación con planes de implementación. No olvide incluir colecciones de exclusión de pruebas y pruebas.  <!-- 4097528 -->

        > [!Important] 
        > Estas colecciones continuarán con la sincronización como sus cambios de pertenencia. Por ejemplo, el plan de implementación usa una colección con una regla de pertenencia a Windows 7. Como esos dispositivos se actualización a Windows 10 y Configuration Manager evalúa la pertenencia a recopilación, quitar esos dispositivos fuera de la recopilación y el plan de implementación.  


### <a name="windows-settings"></a>Configuración de Windows

Configuration Manager establece las siguientes opciones de Windows en `Microsoft\Windows\DataCollection`:

| Directiva   | Valor  |
|----------|--------|
| **CommercialId** | En orden para un dispositivo en aparecer en el análisis de escritorio, configúrelo con identificador comercial de. su organización |
| **AllowTelemetry**  | Establecer `1` para **básica**, `2` para **mejorado**, o `3` para **completa** datos de diagnóstico. Escritorio Analytics requiere al menos básica de datos de diagnóstico. Microsoft recomienda que utilice el nivel mejorado (limitado) con análisis de escritorio. Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | *Se aplica a Windows 10, versión 1709 y versiones posterior*: Esta configuración solo se aplica cuando el valor de AllowTelemetry es `2`. Limita los eventos de datos de diagnóstico mejorado enviados a Microsoft a únicamente los eventos necesarios para el análisis de escritorio. Para obtener más información, consulte [Windows 10, versión 1709 mejorada de los eventos de datos de diagnóstico y los campos que usa Windows Analytics](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields).|
| **AllowDeviceNameInTelemetry** | *Se aplica a Windows 10, versión 1803 y posteriores*: Se requiere una participación en independiente para habilitar dispositivos para seguir enviando el nombre del dispositivo.<br> <br>Nota: De forma predeterminada, el nombre del dispositivo no se envía a Microsoft. Si no envía el nombre del dispositivo, aparece en el escritorio de análisis como "Desconocido". Este comportamiento puede dificultar a identificar y evaluar los dispositivos. Para obtener más información, consulte [nombre de dispositivo](#device-name). |
| **CommercialDataOptIn** | *Se aplica a Windows 7 y Windows 8.1*: Un valor de `1` es necesario para el análisis de escritorio. Para obtener más información, consulte [participación en datos comerciales en Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |

Ver los valores en el editor de directivas de grupo en la siguiente ruta: **Configuración del equipo** > **plantillas administrativas** > **componentes de Windows** > **datos de colección y la vista previa Compilaciones**.

> [!Important]  
> En la mayoría de los casos, sólo use Configuration Manager para configurar estas opciones. No se aplican también estos valores en objetos de directiva de grupo de dominio. Para obtener más información, consulte [resolución de conflictos](#conflict-resolution).<!-- SCCMDocs-pr 3120 -->

### <a name="device-name"></a>Nombre del dispositivo

El nombre del dispositivo a partir de Windows 10, versión 1803, ya no se recopila de forma predeterminada. Recopilar el nombre del dispositivo con los datos de diagnóstico requiere una participación en independiente. Sin el nombre del dispositivo, es más difícil de identificar los dispositivos que requieren atención al evaluar una actualización a una nueva versión de Windows.

Si no envía el nombre del dispositivo, aparece en el escritorio de análisis como "Desconocido".

![Lista de dispositivos escritorio Analytics que muestra los nombres de "desconocidos"](media/unknown-device-name.png)

Hay una opción en la configuración del Administrador de configuración para el análisis de escritorio configurar esta opción: **Permitir que el nombre del dispositivo en los datos de diagnóstico**. Esta configuración de Configuration Manager controla la configuración de directiva de Windows, AllowDeviceNameInTelemetry.
 

### <a name="conflict-resolution"></a>resolución de conflictos

En general, utilice las colecciones de Configuration Manager para tener como destino la inscripción y la configuración de análisis de escritorio. Utilice la pertenencia directa o consultas para incluir o excluir los dispositivos de la colección. Para obtener más información, vea [Creación de recopilaciones](/sccm/core/clients/manage/collections/create-collections).

Configuration Manager configura sólo la configuración de Windows si aún no existe un valor. Si necesita configurar diferentes valores para un único grupo de dispositivos, puede usar [directiva de grupo](#windows-settings). Configuración de directiva de grupo de destino tiene prioridad sobre la configuración de Configuration Manager.

Si su objetivo de los clientes de Configuration Manager con la configuración de Windows Analytics y análisis de escritorio, la configuración para el análisis de escritorio tiene prioridad.

Al configurar el nivel de datos de diagnóstico, establezca el límite superior para el dispositivo. De forma predeterminada en Windows 10, versión 1803 y posteriores, los usuarios pueden elegir establecer un nivel inferior. Puede controlar este comportamiento mediante la configuración de directiva de grupo **interfaz de usuario de participación en la configuración de telemetría configurar**. Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).



## <a name="next-steps"></a>Pasos siguientes

Avance al siguiente artículo para crear planes de implementación en escritorio Analytics.
> [!div class="nextstepaction"]  
> [Crear planes de implementación](/sccm/desktop-analytics/create-deployment-plans)  
