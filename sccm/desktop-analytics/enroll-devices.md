---
title: Inscripción de dispositivos en el análisis de escritorio
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo inscribir dispositivos en el análisis de escritorio.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 59cd27ac63430a8b9073e7b178b53f9a5cc23da6
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/05/2019
ms.locfileid: "70377891"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Cómo inscribir dispositivos en el análisis de escritorio

> [!Note]  
> Esta información está relacionada con un servicio de vista previa que se puede modificar sustancialmente antes de que se publique comercialmente. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Al [conectar Configuration Manager](/sccm/desktop-analytics/connect-configmgr) a análisis de escritorio, se configuran los valores para inscribir dispositivos en el análisis de escritorio. Puede cambiar esta configuración en cualquier momento. Asegúrese también de que los dispositivos estén actualizados.



## <a name="update-devices"></a>Actualizar dispositivos

Hay dos tipos de actualizaciones que debe aplicar para obtener la mejor experiencia con el análisis de escritorio:

- [Actualizaciones de compatibilidad](#bkmk_appraiser)  
- [Experiencias de usuario y servicio de telemetría conectadas](#bkmk_diagtrack)


### <a name="bkmk_appraiser"></a>Actualizaciones de compatibilidad

El componente de compatibilidad (evaluador) ejecuta diagnósticos en el dispositivo Windows para evaluar su estado de compatibilidad con las versiones más recientes de Windows 10.

Microsoft incrementa regularmente las actualizaciones de este componente, pero el número de KB asociado no cambia. Asegúrese de tener siempre la versión más reciente de la actualización.

Reinicie los dispositivos después de instalar las actualizaciones de compatibilidad por primera vez.

> [!Tip]  
> Use Configuration Manager para instalar automáticamente la versión más reciente de estas actualizaciones. Para obtener más información, consulte [Deploy software updates](/sccm/sum/deploy-use/deploy-software-updates) (Implementación de actualizaciones de software).  

> [!Note]  
> Hay una actualización opcional relacionada, [KB 3150513](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=3150513). Esta actualización proporciona configuraciones y definiciones actualizadas para las actualizaciones de compatibilidad anteriores. Para obtener más información, consulte [actualización de la definición de compatibilidad más reciente para Windows](https://support.microsoft.com/help/3150513).  

#### <a name="windows-10"></a>Windows 10

Windows 10 incluye el componente de compatibilidad. Para obtener la actualización de compatibilidad más reciente, instale la actualización acumulativa más reciente de Windows 10.

#### <a name="windows-81"></a>Windows 8.1

Descargue la actualización: [KB 2976978](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2976978) 

Ejecuta diagnósticos en los sistemas Windows 8.1 que participan en el Programa para la mejora de la experiencia del usuario de Windows. Estos diagnósticos ayudan a determinar si puede tener problemas de compatibilidad al actualizar a Windows 10.

Para obtener más información, consulte [actualización de compatibilidad para mantener Windows actualizado en Windows 8.1](https://support.microsoft.com/help/2976978).

#### <a name="windows-7-with-service-pack-1"></a>Windows 7 con Service Pack 1

Descargue la actualización: [KB 2952664](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2952664) 

Ejecuta diagnósticos en los sistemas Windows 7 con Service Pack 1 (SP1) que participan en el Programa para la mejora de la experiencia del usuario de Windows. Estos diagnósticos ayudan a determinar si puede tener problemas de compatibilidad al actualizar a Windows 10.

Para obtener más información, consulte [actualización de compatibilidad para mantener Windows actualizado en Windows 7](https://support.microsoft.com/help/2952664).


### <a name="bkmk_diagtrack"></a>Experiencias de usuario y servicio de telemetría conectadas

Con los datos de diagnóstico de Windows habilitados, la experiencia del usuario y el servicio de telemetría conectados (DiagTrack) recopilan datos del sistema, de la aplicación y del controlador. Microsoft analiza estos datos y los comparte con usted a través de análisis de escritorio.

Para obtener la mejor experiencia, instale las siguientes actualizaciones en función de la versión del sistema operativo.

> [!Note]  
> Al instalar estas actualizaciones, se esperan los comportamientos siguientes:
> 
> - Los dispositivos que se inscriben en el análisis de escritorio se muestran en el servicio en menos de una hora.  
> - Los dispositivos informan rápidamente del estado de las actualizaciones de calidad y características de Windows  
>
> Sin estas actualizaciones, estos procesos pueden tardar más de 48 horas en informar a análisis de escritorio.  


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

Instale el paquete acumulativo de actualizaciones mensuales de octubre de 2018, [KB4462926](https://support.microsoft.com/help/4462926)

#### <a name="windows-7"></a>Windows 7

Instale el paquete acumulativo de actualizaciones mensuales de octubre de 2018, [KB4462923](https://support.microsoft.com/help/4462923)



## <a name="device-enrollment"></a>Inscripción de dispositivos

El servicio de análisis de escritorio no tiene agentes para instalar. La inscripción de dispositivos requiere configurar las opciones en los dispositivos que desea supervisar. Estas opciones controlan a qué instancia de análisis de escritorio el dispositivo debe enviar sus datos y otras opciones de configuración.

> [!Note]  
> Si ya usa Windows Analytics, use esa misma área de trabajo para el análisis de escritorio. Debe volver a inscribir dispositivos en el análisis de escritorio que se inscribió anteriormente en Windows Analytics.
>
> Solo puede tener un área de trabajo de análisis de escritorio por inquilino de Azure AD. Los dispositivos solo pueden enviar datos de diagnóstico a un área de trabajo.  

Configuration Manager proporciona una experiencia integrada para administrar e implementar esta configuración en clientes de. Para obtener la mejor experiencia, use Configuration Manager.

Al conectar Configuration Manager a análisis de escritorio, configure los valores para inscribir dispositivos. Para obtener más información, consulte [conexión de Configuration Manager con el análisis de escritorio](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

Para cambiar esta configuración, use el procedimiento siguiente:

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**. Seleccione la conexión a análisis de escritorio y elija **propiedades** en la cinta de opciones.

2. En la página **datos de diagnóstico** , realice los cambios necesarios en la configuración siguiente:  

    - **ID. comercial**: este valor se debe rellenar automáticamente con el identificador de la organización. Si no es así, asegúrese de que el servidor proxy está configurado para permitir todos los [puntos de conexión](/sccm/desktop-analytics/enable-data-sharing#endpoints) necesarios antes de continuar. También puede recuperar el ID. comercial manualmente desde el [portal de análisis de escritorio](/sccm/desktop-analytics/monitor-connection-health#bkmk_ViewCommercialID).   

    - **Nivel de datos de diagnóstico de Windows 10**: Para obtener más información, vea [niveles de datos de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

    - **Permitir el nombre del dispositivo en los datos de diagnóstico**: Para obtener más información, consulte [nombre del dispositivo](#device-name).  

    Al realizar cambios en esta página, la página **funcionalidad disponible** muestra una vista previa de la funcionalidad de análisis de escritorio con la configuración de datos de diagnóstico seleccionada.  

3. En la página de **conexión de análisis de escritorio** , realice los cambios necesarios para la configuración siguiente:

    - **Nombre para mostrar**: El portal de análisis de escritorio muestra esta conexión Configuration Manager con este nombre.  

    - **Recopilación de destino**: Esta colección incluye todos los dispositivos que Configuration Manager configura con el identificador comercial y la configuración de datos de diagnóstico. Es el conjunto completo de dispositivos que Configuration Manager se conecta al servicio de análisis de escritorio.  

    - **Los dispositivos de la recopilación de destino usan un proxy autenticado por el usuario para la comunicación saliente**: De forma predeterminada, este valor es **no**. Si es necesario en su entorno, establezca en **sí**. Para obtener más información, consulte [autenticación del servidor proxy](/sccm/desktop-analytics/enable-data-sharing#proxy-server-authentication).  

    - **Seleccione recopilaciones específicas para sincronizar con el análisis de escritorio**: Seleccione **Agregar** para incluir recopilaciones adicionales de la jerarquía de **recopilación de destino** . Estas colecciones están disponibles en el portal de análisis de escritorio para agrupar con planes de implementación. Asegúrese de incluir recopilaciones piloto y de exclusión piloto.  <!-- 4097528 -->

        > [!Important] 
        > Estas colecciones continúan sincronizando a medida que cambian sus pertenencias. Por ejemplo, el plan de implementación utiliza una recopilación con una regla de pertenencia de Windows 7. Cuando esos dispositivos se actualizan a Windows 10 y Configuration Manager evalúa la pertenencia a la recopilación, dichos dispositivos salen de la colección y del plan de implementación.  


### <a name="windows-settings"></a>Configuración de Windows

Configuration Manager establece la siguiente configuración de Windows en la ruta de `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`acceso de la directiva local:

| Directiva   | Value  |
|----------|--------|
| **CommercialId** | Para que un dispositivo se muestre en el análisis de escritorio, configúrelo con el identificador comercial de su organización. |
| **AllowTelemetry**  | Se `1` estableceen Basic `2` , para **mejorado**o `3` para datos de diagnóstico **completos** . El análisis de escritorio requiere al menos datos de diagnóstico básicos. Microsoft recomienda usar el nivel mejorado (limitado) con el análisis de escritorio. Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | *Se aplica a Windows 10, versión 1709 y posteriores*: Esta configuración solo se aplica cuando el valor de `2`AllowTelemetry es. Limita los eventos de datos de diagnóstico mejorados enviados a Microsoft a los eventos necesarios para el análisis de escritorio. Para obtener más información, consulte los [eventos y los campos de datos de diagnóstico mejorados de Windows 10, versión 1709 y usados por Windows Analytics](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields).|
| **AllowDeviceNameInTelemetry** | *Se aplica a Windows 10, versión 1803 y posteriores*: Se requiere una suscripción independiente para permitir que los dispositivos sigan enviando el nombre del dispositivo.<br> <br>Nota: De forma predeterminada, el nombre del dispositivo no se envía a Microsoft. Si no envía el nombre del dispositivo, aparece en análisis de escritorio como "desconocido". Este comportamiento puede dificultar la identificación y la evaluación de los dispositivos. Para obtener más información, consulte [nombre del dispositivo](#device-name). |
| **CommercialDataOptIn** | *Se aplica a Windows 7 y Windows 8.1*: Se requiere un `1` valor de para el análisis de escritorio. Para obtener más información, consulte participación de los [datos comerciales en Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |

Vea esta configuración en el editor de directivas de grupo en la siguiente ruta de acceso:Configuración > del equipo > **plantillas administrativas** > la**recopilación de datos de componentes de Windows y versiones preliminares**.

> [!Important]  
> En la mayoría de los casos, use solo Configuration Manager para configurar estas opciones. No aplique también esta configuración en los objetos de directiva de grupo de dominio. Para obtener más información, vea [resolución de conflictos](#conflict-resolution).<!-- SCCMDocs-pr 3120 -->

### <a name="device-name"></a>Nombre del dispositivo

A partir de Windows 10, versión 1803, el nombre del dispositivo ya no se recopila de forma predeterminada. Recopilar el nombre del dispositivo con los datos de diagnóstico requiere una suscripción independiente. Sin el nombre del dispositivo, es más difícil identificar los dispositivos que requieren atención al evaluar una actualización a una nueva versión de Windows.

Si no envía el nombre del dispositivo, aparece en análisis de escritorio como "desconocido".

![Lista de dispositivos de análisis de escritorio que muestra nombres "desconocidos"](media/unknown-device-name.png)

Hay una opción en la Configuration Manager configuración de análisis de escritorio para configurar esta opción: **Permita el nombre del dispositivo en los datos de diagnóstico**. Esta configuración de Configuration Manager controla la configuración de directiva de Windows, AllowDeviceNameInTelemetry.
 

### <a name="conflict-resolution"></a>Resolución de conflictos

En general, use colecciones de Configuration Manager para la inscripción y la configuración de análisis de escritorio. Use la pertenencia directa o consultas para incluir o excluir dispositivos de la recopilación. Para obtener más información, vea [Creación de recopilaciones](/sccm/core/clients/manage/collections/create-collections).

Configuration Manager solo configura las opciones de Windows si aún no existe un valor. Si necesita configurar diferentes valores para un grupo de dispositivos único, puede usar la Directiva de [Grupo](#windows-settings). La configuración de destino de la Directiva de grupo tiene prioridad sobre la configuración de Configuration Manager.

Si el destino es Configuration Manager clientes con la configuración de Windows Analytics y análisis de escritorio, la configuración de análisis de escritorio tiene prioridad.

Al configurar el nivel de datos de diagnóstico, se establece el límite superior para el dispositivo. De forma predeterminada, en Windows 10, versión 1803 y versiones posteriores, los usuarios pueden elegir establecer un nivel inferior. Puede controlar este comportamiento mediante la configuración de directiva de grupo **configurar la interfaz de usuario de configuración de la telemetría**. Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).



## <a name="next-steps"></a>Pasos siguientes

Avance al siguiente artículo para crear planes de implementación en análisis de escritorio.
> [!div class="nextstepaction"]  
> [Crear planes de implementación](/sccm/desktop-analytics/create-deployment-plans)  
