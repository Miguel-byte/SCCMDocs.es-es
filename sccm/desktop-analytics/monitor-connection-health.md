---
title: Supervisión del estado de conexión
titleSuffix: Configuration Manager
description: Detalles sobre cómo supervisar el estado de la conexión y los Estados de los dispositivos de análisis de escritorio en Configuration Manager.
ms.date: 06/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7139175a564ffff50d325daf808e32efb7d3436b
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70891773"
---
# <a name="monitor-connection-health"></a>Supervisión del estado de conexión

Use el panel de estado de la **conexión** en Configuration Manager para profundizar en las categorías por estado de dispositivo. En la consola de Configuration Manager, vaya al área de trabajo **biblioteca de software** , expanda el nodo servicio de **análisis de escritorio** y seleccione el panel estado de la **conexión** .  

![Captura de pantalla del panel de estado de conexión de Configuration Manager](media/connection-health-dashboard.png)

La primera vez que se configura el análisis de escritorio, es posible que estos gráficos no muestren datos completos. Los dispositivos activos pueden tardar 2-3 días en enviar datos de diagnóstico al servicio de análisis de escritorio, el servicio para procesar los datos y, a continuación, realizar la sincronización con el sitio de Configuration Manager.<!-- 4098037 -->


## <a name="connection-details"></a>Detalles de conexión

Este icono muestra la siguiente información básica sobre la conexión desde Configuration Manager hasta el análisis de escritorio:

- **Nombre del inquilino**: El nombre de la conexión de análisis de escritorio en el nodo **servicios de Azure**

- **Colección de destino**: La misma *recopilación de destino* que especificó al conectarse Configuration Manager al análisis de escritorio. Esta colección incluye todos los dispositivos que Configuration Manager configura con el identificador comercial y la configuración de datos de diagnóstico. Es el conjunto completo de dispositivos que Configuration Manager se conecta al servicio de análisis de escritorio.

- **Dispositivos de destino**: Todos los dispositivos de la recopilación de destino, menos los siguientes tipos de dispositivos:

    - Baja
    - Obsoleto
    - Inactivo
    - No administrado
    - Dispositivos que ejecutan las versiones de canal de mantenimiento a largo plazo (LTSC) de Windows 10
    - Dispositivos que ejecutan Windows Server

    Para obtener más información sobre estos Estados de dispositivo, consulte [acerca del estado de cliente](/sccm/core/clients/manage/monitor-clients#bkmk_about).

    > [!Note]  
    > Configuration Manager carga en el análisis de escritorio de todos los dispositivos de la recopilación de destino menos los clientes obsoletos y desusados.

- **Dispositivos válidos para da**: El número de dispositivos destinados menos dispositivos que no son válidos para el análisis de escritorio. Por ejemplo, los dispositivos de la recopilación de destino que ejecutan el canal de mantenimiento a largo plazo (LTSC) de Windows Server o Windows 10.


## <a name="last-sync-details"></a>Detalles de la última sincronización

Este icono muestra Cuándo Configuration Manager sincroniza con el servicio en la nube de análisis de escritorio y el número de dispositivos que se sincronizan.

- **Dispositivos sincronizados**: El número de dispositivos únicos que Configuration Manager enviaron a análisis de escritorio. El servicio incluye estos dispositivos en la instantánea actualmente visible.

- **Última sincronización del servicio**: Lo mismo que la hora de la **última actualización** en el portal de análisis de escritorio.

- **Siguiente sincronización del servicio**: Cuando pueda esperar la siguiente instantánea diaria en análisis de escritorio.

> [!Note]  
> La primera vez que se inscriben dispositivos en el análisis de escritorio, los datos pueden tardar varios días en cargarse y procesarse. Durante este tiempo, el icono de detalles de la **última sincronización** puede aparecer en blanco. Además, ninguno de los valores de este icono se actualiza automáticamente cuando se solicita una instantánea a petición. Para obtener más información, consulte [latencia de datos](/sccm/desktop-analytics/troubleshooting#data-latency).

Si cree que algunos dispositivos no se muestran en el análisis de escritorio, asegúrese de que los dispositivos son compatibles con el análisis de escritorio. Para obtener más información, consulte [Requisitos previos](/sccm/desktop-analytics/overview#prerequisites).


## <a name="connection-health"></a>Estado de la conexión

El gráfico de estado de la **conexión** muestra el número de dispositivos en los siguientes Estados de mantenimiento:  

- [Correctamente inscrito](#properly-enrolled): El dispositivo aparece en el análisis de escritorio con un inventario completo
- [No se puede inscribir](#unable-to-enroll): Hay un problema de bloqueo que impide la inscripción de dispositivos
- [Alerta de configuración](#configuration-alert): El dispositivo no aparece en el análisis de escritorio o aparece con un inventario incompleto. Configuration Manager también identificó un problema con la inscripción de dispositivos.
- [Esperando la inscripción](#awaiting-enrollment): Configuration Manager configurado el dispositivo, pero todavía no aparece en el análisis de escritorio
- [Estado pendiente](#status-pending): Configuration Manager todavía está configurando este dispositivo o no tiene suficientes datos del dispositivo para determinar su estado
- [Faltan datos](#missing-data): Configuration Manager configurado el dispositivo, pero el análisis de escritorio solo tiene datos parciales

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

El número total de dispositivos en este gráfico debe ser el mismo que los **dispositivos válidos para** el valor de da en el icono de detalles de la conexión.

Seleccione el sector en el gráfico para explorar en profundidad una lista de dispositivos con ese estado. Para obtener más información, consulte [lista de dispositivos](#device-list).

Seleccione el nombre de la categoría en la leyenda que se va a quitar o agregar del gráfico. Esta acción ayuda a ampliar el gráfico para que pueda ver los tamaños relativos de segmentos más pequeños.

### <a name="properly-enrolled"></a>Inscrito correctamente

El dispositivo tiene los siguientes atributos:

- Un cliente de Configuration Manager versión 1902 o posterior  
- No hay errores de configuración  
- Análisis de escritorio ha recibido datos de diagnóstico completos de este dispositivo en los últimos 28 días  
- Análisis de escritorio tiene un inventario completo de la configuración del dispositivo y de las aplicaciones instaladas  

### <a name="unable-to-enroll"></a>No se puede inscribir

Configuration Manager detecta uno o más problemas de bloqueo que impiden la inscripción del dispositivo. Para obtener más información, consulte la lista de [propiedades de dispositivo de análisis de escritorio en Configuration Manager](#bkmk_config-issues).  

Por ejemplo, el Configuration Manager cliente no es al menos la versión 1902 (5.0.8790). Actualice el cliente a la versión más reciente. Considere la posibilidad de habilitar la actualización de cliente automática para el sitio Configuration Manager. Para obtener más información, vea [Actualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

### <a name="configuration-alert"></a>Alerta de configuración

El dispositivo no aparece en el análisis de escritorio o aparece con un inventario incompleto. Configuration Manager también identificó un problema con la inscripción de dispositivos. Para obtener más información, consulte la lista de [propiedades de dispositivo de análisis de escritorio en Configuration Manager](#bkmk_config-issues).

Por ejemplo, el dispositivo no tiene conectividad con el servicio. Para obtener más información, consulte [conectividad de extremo de diagnóstico de Windows](#windows-diagnostic-endpoint-connectivity).

### <a name="awaiting-enrollment"></a>Esperando inscripción

El análisis de escritorio no tiene datos de diagnóstico para este dispositivo. Este problema puede deberse a que ha agregado el dispositivo recientemente a la recopilación de destino y aún no ha enviado datos. También puede significar que el dispositivo no se comunica correctamente con el servicio y que los datos de diagnóstico más recientes tienen más de 28 días de antigüedad.

Asegúrese de que el dispositivo puede comunicarse con el servicio. Para obtener más información, consulte [puntos de conexión](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

### <a name="status-pending"></a>Estado pendiente

Configuration Manager todavía está configurando este dispositivo o no tiene suficientes datos del dispositivo para determinar su estado.

### <a name="missing-data"></a>Faltan datos

Configuration Manager el dispositivo se configuró correctamente, pero el análisis de escritorio no puede crear una evaluación de compatibilidad. No tiene un conjunto de datos completo para la configuración del dispositivo (censo) o las aplicaciones instaladas (inventario).

Este problema se suele corregir automáticamente cuando el dispositivo vuelve a intentarlo. Si persiste, asegúrese de que el dispositivo puede comunicarse con el servicio. Para obtener más información, consulte [puntos de conexión](/sccm/desktop-analytics/enable-data-sharing#endpoints).  


## <a name="device-list"></a>Lista de dispositivos

Para ver una lista específica de dispositivos por estado, empiece con el panel de estado de la **conexión** . Seleccione uno de los segmentos del icono **Estado** de la conexión y explore en profundidad una lista de dispositivos en este estado. Esta vista de dispositivo personalizada muestra las siguientes columnas de análisis de escritorio de forma predeterminada:

- Configuración de ID. comercial
- Actualización de compatibilidad mínima
- Participación en los datos de diagnóstico de Windows
- Participación en los datos comerciales de Windows
- Conectividad de extremo de diagnóstico de Windows

> [!Note]  
> Omita la columna para la **Conectividad del extremo de diagnóstico de Office**. Está reservado para una funcionalidad futura.

Estas columnas corresponden a los [requisitos previos](/sccm/desktop-analytics/overview#prerequisites) de clave para que los dispositivos se comuniquen con el análisis de escritorio.

![Captura de pantalla de la lista de dispositivos inscritos correctamente](media/sccm-device-list-properly-enrolled.png)

Seleccione un dispositivo para ver la lista completa de las propiedades disponibles en el panel de detalles. También puede agregar cualquiera de estas propiedades como columnas a la lista de dispositivos.


## <a name="bkmk_config-issues"></a>Propiedades del dispositivo

Las siguientes propiedades de dispositivo de análisis de escritorio están disponibles como columnas en la lista de dispositivos Configuration Manager:

- [Configuración del evaluador](#appraiser-configuration)  
- [Actualización de compatibilidad mínima](#minimum-compatibility-update)  
- [Versión del evaluador](#appraiser-version)  
- [Última ejecución completa correcta del evaluador](#last-successful-full-run-of-appraiser)  
- [Recopilación de datos de evaluador](#appraiser-data-collection)  
- [Última ejecución completa correcta del censo](#last-successful-full-run-of-census)  
- [Recopilación de datos de censo](#census-data-collection)  
- [Conectividad de extremo de diagnóstico de Windows](#windows-diagnostic-endpoint-connectivity)  
- [Comprobar los datos de diagnóstico del usuario final](#check-end-user-diagnostic-data)  
- [Comprobar el proxy del usuario](#check-user-proxy)  
- [Configuración de ID. comercial](#commercial-id-configuration)  
- [Participación en los datos comerciales de Windows](#windows-commercial-data-opt-in)  
- [Comprobar el nombre del dispositivo en los datos de diagnóstico](#check-device-name-in-diagnostic-data)  
- [Configuración del servicio DiagTrack](#diagtrack-service-configuration)  
- [Versión de DiagTrack](#diagtrack-version)  
- [Recuperación de identificador de SQM](#sqm-id-retrieval)  
- [Recuperación de identificador de dispositivo único](#unique-device-identifier-retrieval)  
- [Participación en los datos de diagnóstico de Windows](#windows-diagnostic-data-opt-in)  

> [!Note]  
> Omitir las propiedades de **conectividad de extremo de diagnóstico de Office** y datos de diagnóstico de **Office**. Están reservadas para futuras funciones.

En el icono de notificaciones de **configuración y bloqueadores de inscripción más frecuentes** del panel de estado de la conexión se muestran las propiedades que los dispositivos suelen informar como un problema.

### <a name="appraiser-configuration"></a>Configuración del evaluador

<!--20,21-->
El evaluador es el componente de Windows que corresponde a las [actualizaciones de compatibilidad](/sccm/desktop-analytics/enroll-devices#update-devices). Evalúa las aplicaciones y los controladores del dispositivo para comprobar la compatibilidad con la versión más reciente de Windows. 

Si esta comprobación se realiza correctamente, el componente del evaluador está configurado correctamente en el dispositivo.

De lo contrario, podría mostrar uno de los siguientes errores:

- No se puede configurar la recopilación de datos de compatibilidad de aplicaciones de dispositivo (SetRequestAllAppraiserVersions). Compruebe los registros para ver los detalles de la excepción  

- No se puede configurar la recopilación de datos de compatibilidad de aplicaciones de dispositivo (SetRequestAllAppraiserVersions). Compruebe los registros para ver los detalles de la excepción  

- No se puede escribir RequestAllAppraiserVersions en la `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`clave del registro. Comprobar permisos  

Compruebe los permisos de esta clave del registro. Asegúrese de que la cuenta de sistema local puede tener acceso a esta clave para que el cliente de Configuration Manager establezca.  

Para obtener más información, revise M365AHandler. log en el cliente.  

### <a name="minimum-compatibility-update"></a>Actualización de compatibilidad mínima

<!--18,19,32-->
La actualización de compatibilidad (evaluador. dll) no está instalada o no está actualizada en el dispositivo. Es más antiguo que el requisito mínimo para el análisis de escritorio, 10.0.17763.

Instale la actualización de compatibilidad más reciente. Para obtener más información, consulte [actualizaciones de compatibilidad](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser).

### <a name="appraiser-version"></a>Versión del evaluador

Esta propiedad muestra la versión actual del componente del evaluador en el dispositivo. Muestra la versión del archivo en `%windir%\System32\appraiser.dll`, sin los separadores decimales. Por ejemplo, la versión del archivo 10.0.17763 se muestra como 10017763.

### <a name="last-successful-full-run-of-appraiser"></a>Última ejecución completa correcta del evaluador

Esta propiedad muestra la fecha y la hora de la última vez que el dispositivo ejecutó el evaluador correctamente.

### <a name="appraiser-data-collection"></a>Recopilación de datos de evaluador

<!--Appraiser run status-->
<!--22,33-->
Esta propiedad muestra el resultado más reciente de Windows que ejecuta el componente del evaluador.

Si no se realiza correctamente, podría mostrarse uno de los siguientes errores:

- No se pueden recopilar datos de compatibilidad de aplicaciones (RunAppraiser). Consulte los registros para obtener más información  

- La recopilación de datos de compatibilidad de aplicaciones (CompatTelRunner. exe) finalizó con un código de error  

Para obtener más información, revise M365AHandler. log en el cliente.

Busque el siguiente archivo: `%windir%\System32\CompatTelRunner.exe`. Si no existe, vuelva a instalar las [actualizaciones de compatibilidad](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser)necesarias. Asegúrese de que ningún otro componente del sistema está quitando este archivo, como la Directiva de grupo o un servicio antimalware.

Si el archivo M365AHandler. log en el cliente incluye uno de los siguientes errores:

``` Log
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

Para ayudar a solucionar estos errores, ejecute los siguientes comandos desde una consola de Windows PowerShell con privilegios elevados en el cliente afectado:

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>Última ejecución completa correcta del censo

Esta propiedad muestra la fecha y la hora en que el dispositivo ejecutó correctamente el censo.

### <a name="census-data-collection"></a>Recopilación de datos de censo

<!-- Census run status -->
<!--51,52-->
Censo es el componente de Windows que realiza el inventario del dispositivo. Estos datos de inventario se usan para comprender el dispositivo y su configuración.

Esta propiedad muestra el resultado más reciente de Windows que ejecuta el componente de censo.

Si no se realiza correctamente, podría mostrarse uno de los siguientes errores:

- No se pueden recopilar datos sobre el dispositivo y su configuración (RunCensus). Compruebe los registros para ver los detalles de la excepción  

- No se encontró la herramienta de recopilación de datos de configuración y el dispositivo (devicecensus. exe)  

Para obtener más información, revise M365AHandler. log en el cliente.

Busque el siguiente archivo: `%windir%\System32\DeviceCensus.exe`. Si no existe, vuelva a instalar las [actualizaciones de compatibilidad](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser)necesarias. Asegúrese de que ningún otro componente del sistema está quitando este archivo, como la Directiva de grupo o un servicio antimalware.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Conectividad de extremo de diagnóstico de Windows

<!--12,15-->
Si esta comprobación se realiza correctamente, el dispositivo puede conectarse a la experiencia del usuario conectada y al punto de conexión de telemetría (Vortex).

De lo contrario, puede mostrar uno de los siguientes errores:  

- No se puede conectar a la experiencia del usuario conectada y al punto de conexión de telemetría (Vortex). Comprobar la configuración de la red o el proxy  

- No se puede comprobar la conectividad con la experiencia del usuario conectada y el punto de conexión de telemetría (CheckVortexConnectivity). Compruebe los registros para ver los detalles de la excepción  

Los dispositivos comprueban la conectividad con una solicitud GET al siguiente punto de conexión en función de la versión del sistema operativo:

| Versión del SO | Punto de conexión |
|------------|----------|
| Windows 10, versión 1803 o posterior con la actualización acumulativa más reciente | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10, versión 1803 o posterior sin la actualización acumulativa 2018-09 o posterior | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, versión 1709 o anterior | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 o Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Asegúrese de que el dispositivo puede comunicarse con el servicio. Esta comprobación valida algunos de los puntos de conexión necesarios, pero no todos. Para obtener más información, consulte [puntos de conexión](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

Para obtener más información, revise M365AHandler. log en el cliente.  

### <a name="check-end-user-diagnostic-data"></a>Comprobar los datos de diagnóstico del usuario final

<!--1004-->
Si esta comprobación no se realiza correctamente, el usuario seleccionó un nivel inferior de datos de diagnóstico de Windows en el dispositivo. También puede deberse a un objeto de directiva de grupo en conflicto. Para obtener más información, consulte [configuración de Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).

En función de los requisitos de su empresa, puede deshabilitar la elección del usuario a través de la Directiva de grupo. Use la opción para **configurar la interfaz de usuario de configuración de participación en la telemetría**. Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).

### <a name="check-user-proxy"></a>Comprobar el proxy del usuario

<!--30,35-->
El valor DisableEnterpriseAuthProxy está habilitado de forma predeterminada para Windows 7. En Windows 8.1 equipos, Configuration Manager establece el valor de DisableEnterpriseAuthProxy en 0 (no deshabilitado).

Esta propiedad puede mostrar los errores siguientes:

- El proxy de autenticación está habilitado. Establezca DisableEnterpriseAuthProxy en 0 en`HKLM\Software\Policies\Microsoft\Windows\DataCollection`

- No se puede comprobar el estado del proxy de autenticación. Compruebe los registros para ver los detalles de la excepción

Para obtener más información, revise M365AHandler. log en el cliente.  

Compruebe los permisos de esta clave del registro. Asegúrese de que la cuenta de sistema local puede tener acceso a esta clave para que el cliente de Configuration Manager establezca. También puede deberse a un objeto de directiva de grupo en conflicto. Para obtener más información, consulte [configuración de Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

### <a name="commercial-id-configuration"></a>Configuración de ID. comercial

<!--9, 11, 53-->
Microsoft usa un identificador comercial único para asignar información de dispositivos al área de trabajo de análisis de escritorio. Al integrar Configuration Manager con el análisis de escritorio, consulta automáticamente el servicio para este identificador. Configuration Manager debe aplicar este identificador automáticamente a los clientes a los que se dirige la configuración de análisis de escritorio.

Si esta comprobación se realiza correctamente, el dispositivo se configura correctamente con un ID. comercial.

De lo contrario, puede mostrar uno de los siguientes errores:

- No se puede escribir CommercialId en la `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`clave del registro. Comprobar permisos  

- No se puede actualizar CommercialId en la `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`clave del registro. Compruebe los registros para ver los detalles de la excepción  

- Proporcione el valor de CommercialId correcto en`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Para obtener más información, revise M365AHandler. log en el cliente.  

Compruebe los permisos de esta clave del registro. Asegúrese de que la cuenta de sistema local puede tener acceso a esta clave para que el cliente de Configuration Manager establezca. También puede deberse a un objeto de directiva de grupo en conflicto. Para obtener más información, consulte [configuración de Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Hay un identificador diferente para el dispositivo. Esta clave del registro la usa la Directiva de grupo. Tiene prioridad sobre el identificador proporcionado por Configuration Manager.  

<a name="bkmk_ViewCommercialID"></a>Para ver el ID. comercial en el portal de análisis de escritorio, use el siguiente procedimiento:

1. Vaya al portal de análisis de escritorio y seleccione **servicios conectados** en el grupo configuración global.  

2. En el panel **servicios conectados** , el panel **inscribir dispositivos** está seleccionado de forma predeterminada. En el panel inscribir dispositivos, la sección Información muestra la clave de ID. comercial.  

![Captura de pantalla de ID. comercial en el portal de análisis de escritorio](media/commercial-id.png)

> [!Important]  
> Obtenga solo una **nueva clave de identificador** cuando no pueda usar la actual. Si vuelve a generar el ID. comercial, [vuelva a inscribir los dispositivos con el nuevo identificador](/sccm/desktop-analytics/enroll-devices#device-enrollment). Este proceso podría provocar la pérdida de datos de diagnóstico durante la transición.  

### <a name="windows-commercial-data-opt-in"></a>Participación en los datos comerciales de Windows

<!--64-->
Esta propiedad es específica de los dispositivos que ejecutan Windows 7 o Windows 8.1. Ejecuta pruebas similares a medida que se opta por los [datos de diagnóstico de Windows](#windows-diagnostic-data-opt-in), excepto por el valor de CommercialDataOptIn.

### <a name="check-device-name-in-diagnostic-data"></a>Comprobar el nombre del dispositivo en los datos de diagnóstico

<!--56,58-->
Si esta comprobación se realiza correctamente, el dispositivo está configurado correctamente para compartir el nombre del dispositivo.

De lo contrario, puede mostrar uno de los siguientes errores:

- No se puede comprobar el nombre del dispositivo que se va a enviar a Microsoft como parte de los datos de diagnóstico de Windows. Compruebe los registros para ver los detalles de la excepción  

- No se puede escribir AllowDeviceNameInTelemetry en `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`la clave del registro. Comprobar permisos  

Para obtener más información, revise M365AHandler. log en el cliente.  

Compruebe los permisos de esta clave del registro. Asegúrese de que la cuenta de sistema local puede tener acceso a esta clave para que el cliente de Configuration Manager establezca. También puede deberse a un objeto de directiva de grupo en conflicto. Para obtener más información, consulte [configuración de Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Asegúrese de que otro mecanismo de directivas, como la Directiva de grupo, no deshabilite esta configuración.

### <a name="diagtrack-service-configuration"></a>Configuración del servicio DiagTrack

<!--44,45,50-->
Si esta comprobación se realiza correctamente, el componente DiagTrack está configurado correctamente en el dispositivo. La versión mínima requerida por el análisis de escritorio es 10010586 (10.0.10586).

De lo contrario, podría mostrar uno de los siguientes errores:

- El componente experiencia del usuario y telemetría (diagtrack. dll) conectado está obsoleto. Comprobar requisitos  

- No se encuentra el componente de telemetría y la experiencia del usuario conectado (diagtrack. dll). Comprobar requisitos  

- Habilitar e iniciar el servicio de telemetría y experiencias del usuario conectado para enviar datos a Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Instale las actualizaciones más recientes. Para obtener más información, consulte [actualizaciones de dispositivos](/sccm/desktop-analytics/enroll-devices#update-devices).

Asegúrese de que se está ejecutando el servicio de **telemetría y experiencias del usuario conectado** en el dispositivo.

### <a name="diagtrack-version"></a>Versión de DiagTrack

Esta propiedad muestra la versión actual de la experiencia del usuario y el componente de telemetría conectados en el dispositivo. Muestra la versión del archivo en `%windir%\System32\diagtrack.dll`, sin los separadores decimales. Por ejemplo, la versión del archivo 10.0.10586 se muestra como 10010586.

### <a name="sqm-id-retrieval"></a>Recuperación de identificador de SQM

<!--38-->
Esta propiedad es principalmente para dispositivos Windows 7. Se puede usar en versiones posteriores del sistema operativo como identificador de reserva para el dispositivo.

Si no se realiza correctamente, puede mostrarse el siguiente error:

- No se puede recuperar el identificador de telemetría de dispositivo heredado (ID. de SQM)

Para obtener más información, revise M365AHandler. log en el cliente.  

Asegúrese de que no tiene identificadores duplicados en su entorno. Por ejemplo, si los dispositivos se implementaron con una imagen de sistema operativo que no se generalizaba.

### <a name="unique-device-identifier-retrieval"></a>Recuperación de identificador de dispositivo único

<!--54-->
El análisis de escritorio usa el servicio de cuentas de Microsoft para una identidad de dispositivo más confiable.

Asegúrese de que el servicio **ayudante para el inicio de sesión en la cuenta Microsoft** no esté deshabilitado. El tipo de inicio debe ser **manual (desencadenar Inicio)** .

Para deshabilitar el acceso cuenta de Microsoft el usuario final, use la configuración de directiva en lugar de bloquear este punto de conexión. Para obtener más información, consulte [el cuenta de Microsoft de la empresa](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

### <a name="windows-diagnostic-data-opt-in"></a>Participación en los datos de diagnóstico de Windows

<!--8,40,55,62-->
Esta propiedad comprueba que Windows esté configurado correctamente para permitir datos de diagnóstico. Comprueba el valor de AllowTelemetry en las siguientes claves del registro:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Compruebe los permisos de estas claves del registro. Asegúrese de que la cuenta de sistema local puede tener acceso a estas claves para que el cliente de Configuration Manager establezca. También puede deberse a un objeto de directiva de grupo en conflicto. Para obtener más información, consulte [configuración de Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Para obtener más información, revise M365AHandler. log en el cliente.  



## <a name="see-also"></a>Consulte también

[Solución de problemas de Análisis de escritorio](/sccm/desktop-analytics/troubleshooting)
