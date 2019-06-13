---
title: Supervisión de estado de conexión
titleSuffix: Configuration Manager
description: Obtener más información sobre cómo supervisar los Estados de mantenimiento y el dispositivo de conexión para el análisis de escritorio en Configuration Manager.
ms.date: 06/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: a7dc9b67dbf57c1803ed732f36e1cb110260146d
ms.sourcegitcommit: e3c1eb0b75d79c05a750d49354c851d15d5e26a3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/13/2019
ms.locfileid: "67039736"
---
# <a name="monitor-connection-health"></a>Supervisión de estado de conexión

Use la **mantenimiento de la conexión** panel en Configuration Manager para profundizar en categorías por estado de dispositivos. En la consola de Configuration Manager, vaya a la **biblioteca de Software** área de trabajo, expanda el **escritorio Analytics mantenimiento** nodo y seleccione el **estado de conexión** panel.  

![Captura de pantalla del panel de mantenimiento de conexión de Configuration Manager](media/connection-health-dashboard.png)

Cuando se configura por primera vez el análisis de escritorio, estos gráficos no pueden mostrar datos completos. Puede tardar 2 y 3 días para los dispositivos activos enviar datos de diagnóstico para el servicio de análisis de escritorio, el servicio para procesar los datos y, a continuación, sincronizar con el sitio de Configuration Manager.<!-- 4098037 -->


## <a name="connection-details"></a>Detalles de conexión

Este icono muestra la siguiente información básica acerca de la conexión desde Configuration Manager para el análisis de escritorio:

- **Nombre del inquilino**: El nombre de la conexión de escritorio Analytics en el **Azure Services** nodo

- **Colección de destino**: El mismo *recopilación de destino* que especificó al conectar Configuration Manager para análisis del escritorio. Esta colección incluye todos los dispositivos de Configuration Manager se configura con el Id. comercial y la configuración de datos de diagnóstico. Es el conjunto completo de los dispositivos que Configuration Manager se conecta al servicio de análisis de escritorio.

- **Los dispositivos de destino**: Todos los dispositivos de la colección de destino, menos los siguientes tipos de dispositivos:

    - Dado de baja
    - Obsoleto
    - inactivo
    - no administrado

    Para obtener más información sobre estos Estados de dispositivo, consulte [acerca del estado de cliente](/sccm/core/clients/manage/monitor-clients#bkmk_about).

    > [!Note]  
    > Administrador de configuración de carga en el análisis de escritorio de todos los dispositivos de la colección de destino menos clientes retirados y obsoletos.

- **Los dispositivos aptos para DA**: El número de dispositivos de destino menos dispositivos que no son aptos para el análisis de escritorio. Por ejemplo, dispositivos de la colección de destino que ejecutan canal mantenimiento a largo plazo (LTSC) de Windows Server o Windows 10.


## <a name="last-sync-details"></a>Detalles de la última sincronización

Este icono muestra cuando Configuration Manager se sincroniza con el servicio de análisis de escritorio en la nube y cuántos dispositivos se sincroniza.

- **Dispositivos sincronizados**: El número de dispositivos únicos que Configuration Manager envía al análisis de escritorio. El servicio incluye estos dispositivos en la instantánea actualmente visible.

- **Última sincronización del servicio**: Igual que el **actualizó por última vez** tiempo en el portal de análisis de escritorio.

- **A continuación del servicio sincronización**: Cuando puede esperar la siguiente instantánea diaria en análisis de escritorio.

> [!Note]  
> Ninguno de estos valores se actualizan automáticamente cuando se solicita una instantánea y a petición. Para obtener más información, consulte [latencia de datos](/sccm/desktop-analytics/troubleshooting#data-latency).

Si piensa que algunos dispositivos no están visibles en el escritorio de análisis, asegúrese de que los dispositivos son compatibles con análisis de escritorio. Para obtener más información, consulte [Requisitos previos](/sccm/desktop-analytics/overview#prerequisites).


## <a name="connection-health"></a>Estado de conexión

El **mantenimiento de la conexión** gráfico muestra el número de dispositivos en los siguientes estados de mantenimiento:  

- [Correctamente inscrito](#properly-enrolled): El dispositivo aparece en el escritorio de análisis con un inventario completo
- [No se puede inscribir](#unable-to-enroll): Hay un problema de bloqueo que evita la inscripción de dispositivos
- [Alerta de configuración](#configuration-alert): El dispositivo no aparece en el escritorio de análisis o aparece con un inventario incompleto. Administrador de configuración también había identificado un problema con la inscripción del dispositivo.
- [En espera de inscripción](#awaiting-enrollment): Configuration Manager configura el dispositivo, pero aún no aparece en el escritorio de análisis
- [Estado pendiente](#status-pending): Configuration Manager todavía se está configurando este dispositivo, o no tiene suficientes datos desde el dispositivo para determinar su estado
- [Faltan datos](#missing-data): Configuration Manager configura el dispositivo, pero el análisis de escritorio solo tiene datos parciales

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

El número total de dispositivos en este gráfico debe ser el mismo que el **dispositivos aptos para DA** valor en el icono de detalles de la conexión.

Seleccione el segmento del gráfico para explorar en profundidad una lista de dispositivos con ese estado. Para obtener más información, consulte [lista de dispositivos](#device-list).

Seleccione el nombre de categoría en la leyenda para quitar o agregarlo en el gráfico. Esta acción ayuda a acercar el gráfico para que pueda ver los tamaños relativos de segmentos más pequeños.

### <a name="properly-enrolled"></a>Correctamente inscrito

El dispositivo tiene los siguientes atributos:

- Una versión 1902 o posterior del cliente de Configuration Manager  
- No hay ningún error de configuración  
- Escritorio Analytics recibe datos de diagnóstico completados de este dispositivo en los últimos 28 días  
- Escritorio Analytics tiene un inventario completo de la configuración del dispositivo y las aplicaciones instaladas  

### <a name="unable-to-enroll"></a>No se puede inscribir

Configuration Manager detecta uno o varios problemas de bloqueo que impiden la inscripción del dispositivo. Para obtener más información, consulte la lista de [propiedades de dispositivo de escritorio Analytics en Configuration Manager](#bkmk_config-issues).  

Por ejemplo, el cliente de Configuration Manager no es de al menos la versión 1902 (5.0.8790). Actualice al cliente a la versión más reciente. Considere la posibilidad de habilitar la actualización automática del cliente para el sitio de Configuration Manager. Para obtener más información, vea [Actualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

### <a name="configuration-alert"></a>Alerta de configuración

El dispositivo no aparece en el escritorio de análisis o aparece con un inventario incompleto. Administrador de configuración también había identificado un problema con la inscripción del dispositivo. Para obtener más información, consulte la lista de [propiedades de dispositivo de escritorio Analytics en Configuration Manager](#bkmk_config-issues).

Por ejemplo, el dispositivo no tiene conectividad con el servicio. Para obtener más información, consulte [conectividad de punto de conexión de diagnóstico de Windows](#windows-diagnostic-endpoint-connectivity).

### <a name="awaiting-enrollment"></a>Esperando la inscripción

Análisis de escritorio no tienen datos de diagnóstico para este dispositivo. Este problema puede deberse a recientemente se agregó el dispositivo a la colección de destino y aún no envió los datos. También puede significar el dispositivo no se están comunicando correctamente con el servicio y los datos de diagnóstico más recientes tiene más de 28 días de antigüedad.

Asegúrese de que el dispositivo puede comunicarse con el servicio. Para obtener más información, consulte [extremos](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

### <a name="status-pending"></a>Estado pendiente

Configuration Manager todavía se está configurando este dispositivo, o no tiene suficientes datos desde el dispositivo para determinar su estado.

### <a name="missing-data"></a>Datos que faltan

Configuration Manager configurado correctamente el dispositivo, pero escritorio Analytics no se puede crear una evaluación de compatibilidad. No tiene un conjunto de datos completo para la configuración del dispositivo (del censo) o instalar aplicaciones (inventario).

A menudo, este problema se corrige automáticamente cuando el dispositivo intenta enviar. Si persiste, asegúrese de que el dispositivo puede comunicarse con el servicio. Para obtener más información, consulte [extremos](/sccm/desktop-analytics/enable-data-sharing#endpoints).  


## <a name="device-list"></a>Lista de dispositivos

Para ver una lista específica de dispositivos por estado, comience con la **mantenimiento de la conexión** panel. Seleccione uno de los segmentos de la **mantenimiento de la conexión** icono y explorar en profundidad una lista de dispositivos en este estado. Esta vista personalizada del dispositivo muestra las siguientes columnas de análisis de escritorio de forma predeterminada:

- Configuración de Id. comercial
- Actualización de compatibilidad mínimo
- Opción datos de diagnóstico de Windows
- Participación datos comerciales en Windows
- Conectividad de punto de conexión de diagnóstico de Windows

> [!Note]  
> Omitir la columna para **conectividad de punto de conexión de diagnóstico de Office**. Está reservado para futuras funcionalidad.

Estas columnas corresponden a la clave [requisitos previos](/sccm/desktop-analytics/overview#prerequisites) los dispositivos para comunicarse con el análisis de escritorio.

![Lista de dispositivos de captura de pantalla de correctamente inscrito](media/sccm-device-list-properly-enrolled.png)

Seleccione un dispositivo para ver la lista completa de las propiedades disponibles en el panel de detalles. También puede agregar cualquiera de estas propiedades como columnas a la lista de dispositivos.


## <a name="bkmk_config-issues"></a> Propiedades del dispositivo

Las siguientes propiedades de dispositivo de escritorio Analytics están disponibles como columnas en la lista de dispositivos de Configuration Manager:

- [Configuración de Appraiser](#appraiser-configuration)  
- [Actualización de compatibilidad mínimo](#minimum-compatibility-update)  
- [Versión Appraiser](#appraiser-version)  
- [Última ejecución completa correcta de Appraiser](#last-successful-full-run-of-appraiser)  
- [Recopilación de datos Appraiser](#appraiser-data-collection)  
- [Última ejecución completa correcta del censo](#last-successful-full-run-of-census)  
- [Recopilación de datos del censo](#census-data-collection)  
- [Conectividad de punto de conexión de diagnóstico de Windows](#windows-diagnostic-endpoint-connectivity)  
- [Comprobar los datos de diagnóstico para el usuario final](#check-end-user-diagnostic-data)  
- [Comprobar el proxy de usuario](#check-user-proxy)  
- [Configuración de Id. comercial](#commercial-id-configuration)  
- [Participación datos comerciales en Windows](#windows-commercial-data-opt-in)  
- [Compruebe el nombre del dispositivo en los datos de diagnóstico](#check-device-name-in-diagnostic-data)  
- [Configuración del servicio DiagTrack](#diagtrack-service-configuration)  
- [Versión DiagTrack](#diagtrack-version)  
- [Recuperación de Id. de SQM](#sqm-id-retrieval)  
- [Recuperación del identificador de dispositivo único](#unique-device-identifier-retrieval)  
- [Opción datos de diagnóstico de Windows](#windows-diagnostic-data-opt-in)  

> [!Note]  
> Omitir las propiedades de **conectividad de punto de conexión de diagnóstico de Office** y **opt datos de diagnóstico de Office**. Están reservadas para la funcionalidad de futuras.

El **más frecuentes bloqueadores de inscripción y alertas de configuración** icono del panel de estado de conexión muestra las propiedades que los dispositivos con mayor frecuencia se notifican como un problema.

### <a name="appraiser-configuration"></a>Configuración de Appraiser

<!--20,21-->
Appraiser es el componente de Windows que se corresponde con el [actualizaciones de compatibilidad](/sccm/desktop-analytics/enroll-devices#update-devices). Evalúa las aplicaciones y los controladores del dispositivo para la compatibilidad con la versión más reciente de Windows. 

Si esta comprobación se realiza correctamente, el componente appraiser está configurado correctamente en el dispositivo.

En caso contrario, es posible que aparezca uno de los errores siguientes:

- No se puede configurar la recopilación de datos de compatibilidad de aplicación de dispositivo (SetRequestAllAppraiserVersions). Compruebe los registros para obtener los detalles de excepción  

- No se puede configurar la recopilación de datos de compatibilidad de aplicación de dispositivo (SetRequestAllAppraiserVersions). Compruebe los registros para obtener los detalles de excepción  

- No se puede escribir la clave RequestAllAppraiserVersions a la clave del registro `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`. Compruebe los permisos  

Compruebe los permisos de esta clave del registro. Asegúrese de que la cuenta sistema local puede tener acceso a esta clave para el cliente de Configuration Manager establecer.  

Para obtener más información, revise M365AHandler.log en el cliente.  

### <a name="minimum-compatibility-update"></a>Actualización de compatibilidad mínimo

<!--18,19,32-->
La actualización de compatibilidad (appraiser.dll) no está instalado o no está actualizada en el dispositivo. Es más antigua que el requisito mínimo para el análisis de escritorio, 10.0.17763.

Instale la actualización de compatibilidad más reciente. Para obtener más información, consulte [actualizaciones de compatibilidad](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser).

### <a name="appraiser-version"></a>Versión Appraiser

Esta propiedad muestra la versión actual del componente Appraiser en el dispositivo. Muestra la versión del archivo en `%windir%\System32\appraiser.dll`, sin las decimales. Por ejemplo, la versión del archivo 10.0.17763 muestra como 10017763.

### <a name="last-successful-full-run-of-appraiser"></a>Última ejecución completa correcta de Appraiser

Esta propiedad muestra la fecha y hora en que el dispositivo correctamente ejecutó por última Appraiser.

### <a name="appraiser-data-collection"></a>Recopilación de datos Appraiser

<!--Appraiser run status-->
<!--22,33-->
Esta propiedad muestra el resultado más reciente de Windows que ejecuta el componente appraiser.

Si no se realiza correctamente, puede que aparezca uno de los errores siguientes:

- No se pueden recopilar datos de compatibilidad de aplicaciones (RunAppraiser). Compruebe los registros para obtener más información  

- Colección de datos de compatibilidad de aplicaciones (CompatTelRunner.exe) finalizó con un código de error  

Para obtener más información, revise M365AHandler.log en el cliente.

Busque el siguiente archivo: `%windir%\System32\CompatTelRunner.exe`. Si no existe, vuelva a instalar los [actualizaciones de compatibilidad](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Asegúrese de que ningún otro componente del sistema es eliminar este archivo, como la directiva de grupo o un servicio antimalware.

Si el archivo M365Handler.log en el cliente incluye uno de los errores siguientes: `RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1`
`RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005`
`RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005`  

Para ayudar a corregir estos errores, ejecute los siguientes comandos desde una consola de Windows PowerShell con privilegios elevados en el cliente afectado:

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

Esta propiedad muestra la fecha y hora en que el dispositivo por última vez ejecutó correctamente del censo.

### <a name="census-data-collection"></a>Recopilación de datos del censo

<!-- Census run status -->
<!--51,52-->
Census es el componente de Windows que incluya el dispositivo. Estos datos de inventario se usan para comprender el dispositivo y su configuración.

Esta propiedad muestra el resultado más reciente de Windows que ejecuta el componente del censo.

Si no se realiza correctamente, puede que aparezca uno de los errores siguientes:

- No se pueden recopilar datos sobre el dispositivo y su configuración (RunCensus). Compruebe los registros para obtener los detalles de excepción  

- Dispositivos y configuración de herramienta recopilación de datos (devicecensus.exe) no encontrado  

Para obtener más información, revise M365AHandler.log en el cliente.

Busque el siguiente archivo: `%windir%\System32\DeviceCensus.exe`. Si no existe, vuelva a instalar los [actualizaciones de compatibilidad](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Asegúrese de que ningún otro componente del sistema es eliminar este archivo, como la directiva de grupo o un servicio antimalware.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Conectividad de punto de conexión de diagnóstico de Windows

<!--12,15-->
Si esta comprobación se realiza correctamente, el dispositivo puede conectarse al extremo de experiencia del usuario y telemetría (Vortex).

En caso contrario, puede mostrar uno de los errores siguientes:  

- No se puede conectar al usuario conectado experiencia y telemetría de punto de conexión (Vortex). Compruebe la configuración de red o proxy  

- No se puede comprobar la conectividad con el usuario conectado experiencia y telemetría de punto de conexión (CheckVortexConnectivity). Compruebe los registros para obtener los detalles de excepción  

Dispositivos comprueban la conectividad con una solicitud GET al punto de conexión siguiente en función de la versión del sistema operativo:

| Versión de SO | punto de conexión |
|------------|----------|
| Windows 10, versión 1803 o posterior con la actualización acumulativa más reciente | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Actualización de la versión 1803 o posterior sin el 09 de 2018 o posterior acumulativa de Windows 10 | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, versión 1709 o versiones anterior | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 o Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Asegúrese de que el dispositivo puede comunicarse con el servicio. Esta comprobación valida algunos pero no todos los puntos de conexión necesarios. Para obtener más información, consulte [extremos](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

Para obtener más información, revise M365AHandler.log en el cliente.  

### <a name="check-end-user-diagnostic-data"></a>Comprobar los datos de diagnóstico para el usuario final

<!--1004-->
Si esta comprobación no se realiza correctamente, un usuario seleccionó una menor datos de diagnóstico de Windows en el dispositivo. También puede deberse mediante un objeto de directiva de grupo en conflicto. Para obtener más información, consulte [configuración Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).

Dependiendo de sus requisitos empresariales, puede deshabilitar la elección del usuario a través de la directiva de grupo. Use la configuración para **interfaz de usuario de participación en la configuración de telemetría configurar**. Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).

### <a name="check-user-proxy"></a>Comprobar el proxy de usuario

<!--30,35-->
La configuración de DisableEnterpriseAuthProxy está habilitada de forma predeterminada para Windows 7. Para equipos Windows 8.1, Configuration Manager establece el valor de DisableEnterpriseAuthProxy en 0 (no está deshabilitado).

Esta propiedad puede mostrar los errores siguientes:

- Autenticación proxy está habilitado. Establezca DisableEnterpriseAuthProxy en 0 en `HKLM\Software\Policies\Microsoft\Windows\DataCollection`

- No puede comprobar el estado de autenticación proxy. Compruebe los registros para obtener los detalles de excepción

Para obtener más información, revise M365AHandler.log en el cliente.  

Compruebe los permisos de esta clave del registro. Asegúrese de que la cuenta sistema local puede tener acceso a esta clave para el cliente de Configuration Manager establecer. También puede deberse mediante un objeto de directiva de grupo en conflicto. Para obtener más información, consulte [configuración Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

### <a name="commercial-id-configuration"></a>Configuración de Id. comercial

<!--9, 11, 53-->
Microsoft usa un único identificador comercial para asignar la información de dispositivos al área de trabajo de análisis de escritorio. Al integrar Configuration Manager con análisis de escritorio, consulta automáticamente el servicio para este identificador. Administrador de configuración debe aplicar automáticamente este identificador a los clientes que sean destinatarios configuración de análisis de escritorio.

Si esta comprobación es correcta, a continuación, el dispositivo está configurado correctamente con un Id. comercial.

En caso contrario, puede mostrar uno de los errores siguientes:

- No se puede escribir el CommercialId a la clave del registro `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Compruebe los permisos  

- No se puede actualizar el CommercialId en la clave del registro `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Compruebe los registros para obtener los detalles de excepción  

- Proporcione el valor correcto de CommercialId en `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Para obtener más información, revise M365AHandler.log en el cliente.  

Compruebe los permisos de esta clave del registro. Asegúrese de que la cuenta sistema local puede tener acceso a esta clave para el cliente de Configuration Manager establecer. También puede deberse mediante un objeto de directiva de grupo en conflicto. Para obtener más información, consulte [configuración Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Hay un identificador distinto para el dispositivo. Esta clave del registro está usando la directiva de grupo. Tiene prioridad sobre el identificador proporcionado por el Administrador de configuración.  

<a name="bkmk_ViewCommercialID"></a> Para ver el identificador comercial en el portal de análisis de escritorio, use el procedimiento siguiente:

1. Vaya al portal de Analytics de escritorio y seleccione **servicios conectados** en el grupo de configuración Global.  

2. En el **servicios conectados** panel, el **inscribir dispositivos** panel está activado de forma predeterminada. En el panel de dispositivos de inscripción, la sección de información muestra la clave de Id. comercial.  

![Captura de pantalla de identificador comercial en el portal de análisis de escritorio](media/commercial-id.png)

> [!Important]  
> Solo **clave de Id. nuevo Get** cuando no se puede usar actual. Si regenera el identificador comercial, [volver a inscribir sus dispositivos con el nuevo identificador](/sccm/desktop-analytics/enroll-devices#device-enrollment). Este proceso podría provocar la pérdida de datos de diagnóstico durante la transición.  

### <a name="windows-commercial-data-opt-in"></a>Participación datos comerciales en Windows

<!--64-->
Esta propiedad es específica de los dispositivos que ejecutan Windows 7 o Windows 8.1. Ejecute pruebas similares como [opción datos de diagnóstico de Windows](#windows-diagnostic-data-opt-in), excepto para el CommercialDataOptIn de valor.

### <a name="check-device-name-in-diagnostic-data"></a>Compruebe el nombre del dispositivo en los datos de diagnóstico

<!--56,58-->
Si esta comprobación se realiza correctamente, el dispositivo está configurado correctamente para compartir el nombre del dispositivo.

En caso contrario, puede mostrar uno de los errores siguientes:

- No puede comprobar el nombre del dispositivo para enviarse a Microsoft como parte de los datos de diagnóstico de Windows. Compruebe los registros para obtener los detalles de excepción  

- No se puede escribir AllowDeviceNameInTelemetry a la clave del registro `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`. Compruebe los permisos  

Para obtener más información, revise M365AHandler.log en el cliente.  

Compruebe los permisos de esta clave del registro. Asegúrese de que la cuenta sistema local puede tener acceso a esta clave para el cliente de Configuration Manager establecer. También puede deberse mediante un objeto de directiva de grupo en conflicto. Para obtener más información, consulte [configuración Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Asegúrese de que otro mecanismo de directiva, como la directiva de grupo, no es si deshabilita a esta configuración.

### <a name="diagtrack-service-configuration"></a>Configuración del servicio DiagTrack

<!--44,45,50-->
Si esta comprobación se realiza correctamente, el componente DiagTrack está configurado correctamente en el dispositivo. La versión mínima requerida por el análisis de escritorio es 10010586 (10.0.10586).

En caso contrario, es posible que aparezca uno de los errores siguientes:

- Conecta la experiencia del usuario y el componente de telemetría (diagtrack.dll) está obsoleto. Comprobar los requisitos  

- No se encuentra el componente de telemetría (diagtrack.dll) y la experiencia del usuario. Comprobar los requisitos  

- Habilitar e iniciar el servicio de telemetría y experiencias del usuario conectado para enviar datos a Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Instale las actualizaciones más recientes. Para obtener más información, consulte [actualizaciones del dispositivo](/sccm/desktop-analytics/enroll-devices#update-devices).

Asegúrese de que el **telemetría y experiencias del usuario conectado** se está ejecutando el servicio en el dispositivo.

### <a name="diagtrack-version"></a>Versión DiagTrack

Esta propiedad muestra la versión actual del componente experiencia del usuario y telemetría en el dispositivo. Muestra la versión del archivo en `%windir%\System32\diagtrack.dll`, sin las decimales. Por ejemplo, la versión del archivo 10.0.10586 muestra como 10010586.

### <a name="sqm-id-retrieval"></a>Recuperación de Id. de SQM

<!--38-->
Esta propiedad es principalmente para los dispositivos de Windows 7. Se puede usar con versiones posteriores de sistema operativo como un identificador de reserva para el dispositivo.

Si no se realiza correctamente, puede mostrar el siguiente error:

- No se puede recuperar el identificador de dispositivo antiguo de la telemetría (SQM Id.)

Para obtener más información, revise M365AHandler.log en el cliente.  

Asegúrese de que no tiene identificadores duplicados en su entorno. Por ejemplo, si se han implementado los dispositivos con una imagen de sistema operativo que no se ha generalizado.

### <a name="unique-device-identifier-retrieval"></a>Recuperación del identificador de dispositivo único

<!--54-->
Análisis de escritorio usa el servicio de Microsoft Account para una identidad de dispositivo más confiable.

Asegúrese de que el **cuenta de inicio de sesión de Ayudante de Microsoft** el servicio no está deshabilitado. El tipo de inicio debe ser **Manual (desencadenador de inicio)** .

Para deshabilitar el acceso de cuenta de Microsoft del usuario final, use la configuración de directiva en lugar de bloquear este punto de conexión. Para obtener más información, consulte [cuenta Microsoft en la empresa](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

### <a name="windows-diagnostic-data-opt-in"></a>Opción datos de diagnóstico de Windows

<!--8,40,55,62-->
Esta propiedad comprueba que Windows está configurado correctamente para permitir que los datos de diagnóstico. Comprueba el valor de AllowTelemetry en las siguientes claves del registro:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Compruebe los permisos de estas claves del registro. Asegúrese de que la cuenta sistema local puede tener acceso a estas claves para el cliente de Configuration Manager establecer. También puede deberse mediante un objeto de directiva de grupo en conflicto. Para obtener más información, consulte [configuración Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Para obtener más información, revise M365AHandler.log en el cliente.  



## <a name="see-also"></a>Consulte también

[Solución de problemas de análisis de escritorio](/sccm/desktop-analytics/troubleshooting)