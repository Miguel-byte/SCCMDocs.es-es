---
title: Archivos de registro para Configuration Manager | Microsoft Docs
description: "Utilice los archivos de registro para solucionar problemas en una jerarquía de System Center Configuration Manager."
ms.custom: na
ms.date: 3/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: b991b4ea27e66c233b04f8e65a412404521d89a6
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017


---
# <a name="log-files-in-system-center-configuration-manager"></a>Archivos de registro en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En System Center Configuration Manager, los componentes de servidor de cliente y sitio registran información de proceso en archivos de registro individuales. Puede usar la información de los archivos de registro para ayudar a solucionar los problemas que pueden producirse en la jerarquía de Configuration Manager. De forma predeterminada, el registro de componentes de cliente y servidor está habilitado en Configuration Manager.   

 En las secciones siguientes se proporcionan detalles sobre los diferentes archivos de registro disponibles. Puede usar esta información para ver y supervisar los detalles operativos de los registros de cliente y servidor de Configuration Manager y para identificar información de errores que pueda ayudarle a solucionar los problemas.  

-   [Acerca de los archivos de registro de Configuration Manager](#BKMK_AboutLogs)  

    -   [Configuración de opciones de registro mediante el Administrador de servicios de Configuration Manager](#BKMK_LogOptions)  

    -   [Búsqueda de registros de Configuration Manager](#BKMK_LogLocation)  

-   [Registros de cliente de Configuration Manager](#BKMK_ClientLogs)  

    -   [Operaciones de cliente](#BKMK_ClientOpLogs)  

    -   [Archivos de registro de instalación de cliente](#BKMK_ClientInstallLog)  

    -   [Cliente para Linux y UNIX](#BKMK_LogFilesforLnU)  

    -   [Cliente para equipos Mac](#BKMK_LogfilesforMac)  

-   [Archivos de registro de servidor de sitio de Configuration Manager](#BKMK_ServerLogs)  

    -   [Registros de servidor de sistema de sitio y servidor de sitio](#BKMK_SiteSiteServerLog)  

    -   [Archivos de registro de instalación de servidor de sitio](#BKMK_SiteInstallLog)  

    -   [Archivos de registro de punto de estado de reserva](#BKMK_FSPLog)  

    -   [Archivos de registro de punto de administración](#BKMK_MPLog)  

    -   [Archivos de registro de punto de actualización de software](#BKMK_SUPLog)  

-   [Archivos de registro para las funcionalidades de Configuration Manager](#BKMK_FunctionLogs)  

    -   [Administración de aplicaciones](#BKMK_AppManageLog)  

    -   [Asset Intelligence](#BKMK_AILog)  

    -   [Copia de seguridad y recuperación](#BKMK_BnRLog)  

    -   [Inscripción de certificado](#BKMK_CertificateEnrollment)

    -   [Notificación de cliente](#BKMK_BGB)

    -   [Puerta de enlace de administración en la nube](#cloud-management-gateway)

    -   [Configuración de cumplimiento y acceso a los recursos de la compañía](#BKMK_CompSettingsLog)  

    -   [Consola de Configuration Manager](#BKMK_ConsoleLog)  

    -   [Administración de contenido](#BKMK_ContentLog)  

    -   [Detección](#BKMK_DiscoveryLog)  

    -   [Endpoint Protection](#BKMK_EPLog)  

    -   [Extensiones](#BKMK_Extensions)  

    -   [Inventario](#BKMK_InventoryLog)  

    -   [Medición](#BKMK_MeteringLog)  

    -   [Migración](#BKMK_MigrationLog)  

    -   [Dispositivos móviles](#BKMK_MDMLog)  

    -   [Implementación de sistema operativo](#BKMK_OSDLog)  

    -   [Administración de energía](#BKMK_PowerMgmtLog)  

    -   [Control remoto](#BKMK_RCLog)  

    -   [Generación de informes](#BKMK_ReportLog)  

    -   [Administración basada en roles](#BKMK_RBALog)  

    -   [Punto de conexión de servicio](#BKMK_WITLog)  

    -   [Actualizaciones de software](#BKMK_SU_NAPLog)  

    -   [Wake On LAN](#BKMK_WOLLog)  

    -   [Mantenimiento de Windows 10](#BKMK_WindowsServicingLog)

    -   [Agente de Windows Update](#BKMK_WULog)  

    -   [Servidor WSUS](#BKMK_WSUSLog)  

##  <a name="BKMK_AboutLogs"></a> Acerca de los archivos de registro de Configuration Manager  
 La mayoría de los procesos de Configuration Manager escriben información operativa en un archivo de registro dedicado al proceso de que se trate. Los archivos de registro se identifican mediante las extensiones de archivo **.log** o **.lo_**. Configuration Manager escribe en un archivo .log hasta que dicho registro alcanza su tamaño máximo. Cuando el registro está lleno, el archivo .log se copia en un archivo con el mismo nombre pero con la extensión .lo_, y el proceso o el componente continúa escribiendo en el archivo .log. Cuando el archivo .log vuelve a alcanzar el tamaño máximo, se sobrescribe el archivo .lo_ y el proceso se repite. Algunos componentes establecen un historial de archivos de registro al anexar una marca de fecha y hora al nombre del archivo de registro y al conservar la extensión .log. Una excepción al tamaño máximo y al uso del archivo .lo_ es el cliente para Linux y UNIX. Para más información sobre el modo en que el cliente para UNIX y Linux usa los archivos de registro, vea [Administrar archivos de registro en el cliente para UNIX y Linux](#BKMK_ManageLinuxLogs) en este tema.  

 Para ver los registros, use la herramienta de visualización de registros de Configuration Manager, CMTrace, que se encuentra en la carpeta \\SMSSetup\\Tools del medio de origen de Configuration Manager. La herramienta CMTrace también se agrega a todas las imágenes de arranque que se agregan a la Biblioteca de software.  

###  <a name="BKMK_LogOptions"></a> Configuración de opciones de registro mediante el Administrador de servicios de Configuration Manager  
 En Configuration Manager, puede cambiar la ubicación de almacenamiento de los archivos de registro y el tamaño de los archivos de registro.  

 Para modificar el tamaño de los archivos de registro, cambiar el nombre y la ubicación de estos archivos y forzar a varios componentes a escribir en un único archivo de registro, siga estos pasos.  

#### <a name="to-modify-logging-for-a-component"></a>Para modificar el registro de un componente  

1.  En la consola de Configuration Manager, seleccione **Supervisión**, **Estado del sistema** y, luego, **Estado del sitio** o **Estado del componente**.  
2.  En la pestaña **Inicio**, en el grupo **Componente**, seleccione **Inicio** y, luego, seleccione **Administración de servicios de Configuration Manager**.  
3.  Cuando se abra el Administrador de servicios de Configuration Manager, conéctese al sitio que quiere administrar. Si no aparece el sitio que quiere administrar, seleccione **Sitio**, **Conectar** y, luego, escriba el nombre del servidor de sitio del sitio correcto.  
4.  Expanda el sitio y vaya a **Componentes** o **Servidores**, según la ubicación de los componentes que quiera administrar.  
5.  En el panel derecho, seleccione uno o más componentes.  
6.  En el menú **Componente**, seleccione **Registro**.  
7.  En el cuadro de diálogo **Registro de componentes de Configuration Manager** , complete las opciones de configuración disponibles para la selección.  
8.  Seleccione **Aceptar** para guardar la configuración.  

###  <a name="BKMK_LogLocation"></a> Búsqueda de registros de Configuration Manager  
Los archivos de registro de Configuration Manager se almacenan en diferentes ubicaciones que dependen del proceso con que se crea el archivo de registro, así como de la configuración de los sistemas de sitio. Habida cuenta de que la ubicación del registro puede variar en un equipo, use la función de búsqueda para localizar los archivos de registro correspondientes en los equipos de Configuration Manager, si necesita solucionar un escenario concreto.  

##  <a name="BKMK_ClientLogs"></a> Registros de cliente de Configuration Manager  
En las siguientes secciones se indican los archivos de registro relacionados con las operaciones de cliente y la instalación de cliente.  

###  <a name="BKMK_ClientOpLogs"></a> Operaciones de cliente  
En la siguiente tabla se muestran los archivos de registro del cliente de Configuration Manager.  

|Nombre del registro|Descripción|  
|--------------|-----------------|  
|CAS.log|Servicio de acceso a contenido. Mantiene la caché del paquete local en el cliente.|  
|Ccm32BitLauncher.log|Registra las acciones para iniciar aplicaciones en el cliente marcadas como "Ejecutar en modo de 32 bits".|  
|CcmEval.log|Registra las actividades de evaluación de estado de cliente de Configuration Manager y los detalles de los componentes necesarios para el cliente de Configuration Manager.|  
|CcmEvalTask.log|Registra las actividades de evaluación de estado de cliente de Configuration Manager iniciadas por la tarea programada de evaluación.|  
|CcmExec.log|Registra actividades del cliente y el servicio de host de agente SMS Este archivo de registro también incluye información acerca de cómo habilitar y deshabilitar el proxy de reactivación.|  
|CcmMessaging.log|Registra actividades relacionadas con la comunicación entre el cliente y los puntos de administración.|  
|CCMNotificationAgent.log|Registra actividades relacionadas con las operaciones de notificación de cliente.|  
|Ccmperf.log|Registra actividades relacionadas con el mantenimiento y la captura de datos relacionados con los contadores de rendimiento de cliente.|  
|CcmRestart.log|Registra la actividad de reinicio del servicio de cliente.|  
|CCMSDKProvider.log|Registra actividades de las interfaces SDK de cliente.|  
|CertificateMaintenance.log|Mantiene los certificados para servicios de dominio de Active Directory y los puntos de administración.|  
|CIDownloader.log|Registra detalles acerca de las descargas de definiciones de elementos de configuración.|  
|CITaskMgr.log|Registra las tareas iniciadas para cada aplicación y tipo de implementación, como las acciones de descarga de contenido e instalación o desinstalación.|  
|ClientAuth.log|Registra la actividad de autenticación y firma del cliente.|  
|ClientIDManagerStartup.log|Crea y mantiene el GUID de cliente e identifica las tareas realizadas durante la asignación y el registro de clientes.|  
|ClientLocation.log|Registra tareas relacionadas con la asignación de sitios de cliente.|  
|CMHttpsReadiness.log|Registra los resultados de ejecución de la herramienta de evaluación de preparación de HTTPS de Configuration Manager. Esta herramienta comprueba si los equipos tienen un certificado de autenticación de cliente de infraestructura de clave pública (PKI) que se pueda usar con Configuration Manager.|  
|CmRcService.log|Registra información del servicio de control remoto.|  
|ContentTransferManager.log|Programa el Servicio de transferencia inteligente en segundo plano (BITS) o el Bloque de mensajes del servidor (SMB) para descargar paquetes u acceder a ellos.|  
|DataTransferService.log|Registra todas las comunicaciones de BITS para el acceso de directiva o paquete.|  
|EndpointProtectionAgent|Registra información sobre la instalación del cliente de System Center Endpoint Protection y la aplicación de directivas antimalware en el cliente.|  
|execmgr.log|Registra detalles acerca de los paquetes y las secuencias de tareas que se ejecutan en el cliente.|  
|ExpressionSolver.log|Registra detalles sobre los métodos de detección mejorada que se usan cuando el registro detallado o de depuración está activado.|  
|ExternalEventAgent.log|Registra el historial de detección de malware de Endpoint Protection y eventos relacionados con el estado de cliente.|  
|FileBITS.log|Registra todas las tareas de acceso de paquetes SMB.|  
|FileSystemFile.log|Registra la actividad del proveedor de Instrumental de administración de Windows (WMI) para la recopilación de archivos e inventario de software.|  
|FSPStateMessage.log|Registra la actividad para los mensajes de estado que el cliente envía al punto de estado de reserva.|  
|InternetProxy.log|Registra la actividad de uso y la configuración de proxy de red del cliente.|  
|InventoryAgent.log|Registra actividades de acciones de inventario de hardware, inventario de software y detección de latido en el cliente.|  
|LocationCache.log|Registra la actividad de uso y mantenimiento de la caché de ubicación del cliente.|  
|LocationServices.log|Registra la actividad del cliente para la localización de puntos de administración, puntos de actualización de software y puntos de distribución.|  
|MaintenanceCoordinator.log|Registra la actividad de tareas de mantenimiento generales del cliente.|  
|Mifprovider.log|Registra la actividad del proveedor de WMI de archivos de formato de información (MIF) de administración.|  
|mtrmgr.log|Supervisa todos los procesos de disponibilidad de software.|  
|PolicyAgent.log|Registra las solicitudes de las directivas que se hayan realizado mediante el servicio de transferencia de datos.|  
|PolicyAgentProvider.log|Registra los cambios de directiva.|  
|PolicyEvaluator.log|Registra los detalles acerca de la evaluación de directivas en los equipos cliente, incluidas las directivas de las actualizaciones de software.|  
|PolicyPlatformClient.log|Registra el proceso de corrección y cumplimiento para todos los proveedores ubicados en \Archivos de programa\Microsoft Policy Platform, excepto el proveedor de archivos.|  
|PolicySdk.log|Registra actividades de interfaces SDK de sistemas de directivas.|  
|Pwrmgmt.log|Registra información acerca de cómo habilitar o deshabilitar y configurar las opciones del cliente de proxy de reactivación.|  
|PwrProvider.log|Registra las actividades del proveedor de administración de energía (PWRInvProvider) hospedado en el servicio WMI. En todas las versiones compatibles de Windows, el proveedor enumera la configuración actual en los equipos durante el inventario de hardware, y aplica la configuración del plan de energía.|  
|SCClient_&lt;*dominio*\>@&lt;*nombreUsuario*\>_1.log|Registra la actividad del Centro de software para el usuario especificado en el equipo cliente.|  
|SCClient_&lt;*dominio*\>@&lt;*nombreUsuario*\>_2.log|Registra la actividad histórica del Centro de software para el usuario especificado en el equipo cliente.|  
|Scheduler.log|Registra las actividades de las tareas programadas para todas las operaciones de cliente.|  
|SCNotify_&lt;*dominio*\>@&lt;*nombreUsuario*\>_1.log|Registra la actividad para informar a los usuarios acerca del software para el usuario especificado.|  
|SCNotify_&lt;*dominio*\>@&lt;*nombreUsuario*\>_1-&lt;*fecha_hora*>.log|Registra la información histórica de notificación de los usuarios acerca del software para el usuario especificado.|  
|setuppolicyevaluator.log|Registra la creación de directivas de configuración e inventario en WMI.|  
|SleepAgent_&lt;*dominio*\>@SYSTEM_0.log|Archivo de registro principal para el proxy de reactivación.|  
|smscliui.log|Registra el uso del cliente de Configuration Manager en el Panel de control.|  
|SrcUpdateMgr.log|Registra la actividad para las aplicaciones instaladas de Windows Installer que se actualizan con ubicaciones de origen de punto de distribución actual.|  
|StatusAgent.log|Registra mensajes de estado creados por los componentes de cliente.|  
|SWMTRReportGen.log|Genera un informe de datos de uso recopilados por el agente de disponibilidad. Estos datos se registran en Mtrmgr.log.|  
|UserAffinity.log|Registra detalles acerca de la afinidad de dispositivo de usuario.|  
|VirtualApp.log|Registra información específica de la evaluación de los tipos de implementación de Application Virtualization (App-V).|  
|Wedmtrace.log|Registra las operaciones relacionadas con escribir filtros en los clientes de Windows Embedded.|  
|wakeprxy-install.log|Registra la información de instalación cuando los clientes reciben la opción de configuración de cliente para activar un proxy de reactivación.|  
|wakeprxy-uninstall.log|Registra información sobre cómo desinstalar el proxy de reactivación cuando los clientes reciben la opción de configuración de cliente para desactivar el proxy de reactivación, si ya se había activado anteriormente.|  

###  <a name="BKMK_ClientInstallLog"></a> Archivos de registro de instalación de cliente  
 En la tabla siguiente se muestran los archivos de registro que contienen información relacionada con la instalación del cliente de Configuration Manager.  

|Nombre del registro|Descripción|  
|--------------|-----------------|  
|ccmsetup.log|Registra tareas de ccmsetup.exe de instalación, actualización y eliminación de cliente. Puede utilizarse para solucionar problemas de instalación de cliente.|  
|ccmsetup-ccmeval.log|Registra tareas de ccmsetup.exe de corrección y estado de cliente.|  
|CcmRepair.log|Registra las actividades de reparación del agente de cliente.|  
|client.msi.log|Registra las tareas de instalación realizadas por client.msi. Puede usarse para solucionar problemas de instalación o eliminación de cliente.|  

###  <a name="BKMK_LogFilesforLnU"></a> Cliente para Linux y UNIX  
 El cliente de Configuration Manager para Linux y UNIX registra información en los siguientes archivos de registro.  

> [!TIP]  
>  A partir de los clientes para Linux y UNIX de la actualización acumulativa 1, puede usar CMTrace para ver los archivos de registro del cliente para Linux y UNIX.  

> [!NOTE]  
>  Cuando utilice la versión de lanzamiento del cliente para Linux y UNIX y consulte la documentación de esta sección, reemplace las referencias siguientes para cada archivo o proceso:  
>   
>  -   Reemplazar **omiserver.bin** con **nwserver.bin**  
> -   Reemplazar **omi** con **nanowbem**  

|Nombre del registro|Detalles|  
|--------------|-------------|  
|Scxcm.log|Archivo de registro para el servicio central del cliente de Configuration Manager para Linux y UNIX (ccmexec.bin). Este archivo de registro contiene información acerca de la instalación y las operaciones en curso de ccmexec.bin.<br /><br /> De forma predeterminada, este archivo de registro se encuentra en **/var/opt/microsoft/scxcm.log**<br /><br /> Para cambiar la ubicación del archivo de registro, edite **/opt/microsoft/configmgr/etc/scxcm.conf** y cambie el campo **PATH**. No es necesario reiniciar el equipo cliente o el servicio para que el cambio surta efecto.<br /><br /> Puede establecer el nivel de registro en una de cuatro opciones distintas.|  
|Scxcmprovider.log|Archivo de registro del servicio CIM del cliente de Configuration Manager para Linux y UNIX (omiserver.bin). Este archivo de registro contiene información acerca de las operaciones en curso de nwserver.bin.<br /><br /> Este registro se encuentra en **/var/opt/microsoft/configmgr/scxcmprovider.log**<br /><br /> Para cambiar la ubicación del archivo de registro, edite **/opt/microsoft/omi/etc/scxcmprovider.conf** y cambie el campo **PATH**. No es necesario reiniciar el equipo cliente o el servicio para que el cambio surta efecto.<br /><br /> Puede establecer el nivel de registro en una de tres opciones.|  

 Ambos archivos de registro admiten varios niveles de registro:  

-   **scxcm.log**. Para cambiar el nivel de registro, edite **/opt/microsoft/configmgr/etc/scxcm.conf** y cambie cada instancia de la etiqueta **MODULE** por el nivel de registro que quiera:  

    -   ERROR: indica problemas que requieren atención  

    -   WARNING: indica posibles problemas en las operaciones de cliente  

    -   INFO: registro más detallado que indica el estado de diversos eventos en el cliente  

    -   TRACE: registro detallado que normalmente se usa para diagnosticar problemas  

-   **scxcmprovider.log**. Para cambiar el nivel de registro, edite **/opt/microsoft/omi/etc/scxcmprovider.conf** y cambie cada instancia de la etiqueta **MODULE** por el nivel de registro que quiera:  

    -   ERROR: indica problemas que requieren atención  

    -   WARNING: indica posibles problemas en las operaciones de cliente

    -   INFO: registro más detallado que indica el estado de diversos eventos en el cliente  

En condiciones normales de funcionamiento, use el nivel de registro ERROR. Este nivel de registro crea el archivo de registro más pequeño. A medida que el nivel de registro aumenta de ERROR a WARNING, INFO y TRACE, se crea un archivo de registro mayor, ya que se escriben más datos en el archivo.  

####  <a name="BKMK_ManageLinuxLogs"></a> Administrar archivos de registro para el cliente UNIX y Linux  
El cliente para Linux y UNIX no limita el tamaño máximo de los archivos de registro de cliente, ni copia automáticamente el contenido de sus archivos .log en otro archivo, como un archivo .lo_. Si desea controlar el tamaño máximo de los archivos de registro, implemente un proceso para administrar los archivos de registro independiente del cliente de Configuration Manager para Linux y UNIX.  

Por ejemplo, puede usar el comando estándar de Linux y UNIX **logrotate** para administrar el tamaño y la rotación de los archivos de registro de cliente. El cliente de Configuration Manager para Linux y UNIX tiene una interfaz que permite a **logrotate** indicar al cliente la finalización de la rotación del registro, lo que permite al cliente reanudar el registro en el archivo de registro.  

Para obtener información acerca de **logrotate**, consulte la documentación de las distribuciones de Linux y UNIX que utiliza.  

###  <a name="BKMK_LogfilesforMac"></a> Cliente para equipos Mac  
El cliente de Configuration Manager para equipos Mac registra información en los siguientes archivos de registro.  

|Nombre del registro|Detalles|  
|--------------|-------------|  
|CCMClient-&lt;*fecha_hora*>.log|Registra actividades relacionadas con operaciones de cliente de Mac, como la administración de aplicaciones, el inventario y el registro de errores.<br /><br /> El archivo de registro se encuentra en la carpeta /Library/Application Support/Microsoft/CCM/Logs del equipo Mac.|  
|CCMAgent-&lt;*fecha_hora*>.log|Registra información relacionada con las operaciones de cliente, como las operaciones de inicio y cierre de sesión de usuario, y la actividad del equipo Mac.<br /><br /> Este archivo de registro se encuentra en la carpeta ~/Library/Logs del equipo Mac.|  
|CCMNotifications-&lt;*fecha_hora*>.log|Registra las actividades relacionadas con las notificaciones de Configuration Manager que se muestran en el equipo Mac.<br /><br /> Este archivo de registro se encuentra en la carpeta ~/Library/Logs del equipo Mac.|  
|CCMPrefPane-&lt;*fecha_hora*>.log|Registra las actividades relacionadas con el cuadro de diálogo de preferencias de Configuration Manager en el equipo Mac, como el estado general y el registro de errores.<br /><br /> Este archivo de registro se encuentra en la carpeta ~/Library/Logs del equipo Mac.|  

El archivo de registro SMS_DM.log en el servidor de sistema de sitio además registra la comunicación entre equipos Mac y el punto de administración que está configurado para dispositivos móviles y equipos Mac.  

##  <a name="BKMK_ServerLogs"></a> Archivos de registro de servidor de sitio de Configuration Manager  
 En las siguientes secciones se indican los archivos de registro que se encuentran en el servidor de sitio o que están relacionados con determinados roles de sistema de sitio.  

###  <a name="BKMK_SiteSiteServerLog"></a> Registros de servidor de sistema de sitio y servidor de sitio  
 En la tabla siguiente se incluyen los archivos de registro que se encuentra en los servidores de sistema de sitio y en el servidor de sitio de Configuration Manager.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Registra la actividad de procesamiento de inscripción.|Servidor de sitio|  
|ADForestDisc.log|Registra acciones de detección de bosques de Active Directory.|Servidor de sitio|  
|ADService.log|Registra la creación de cuentas y los detalles del grupo de seguridad en Active Directory.|Servidor de sitio|  
|adsgdis.log|Registra acciones de detección de grupos de Active Directory.|Servidor de sitio|  
|adsysdis.log|Registra acciones de detección de sistema de Active Directory.|Servidor de sitio|  
|adusrdis.log|Registra acciones de detección de usuarios de Active Directory.|Servidor de sitio|  
|ccm.log|Registra actividades de instalación de inserción de cliente.|Servidor de sitio|  
|CertMgr.log|Registra actividades de certificado de comunicaciones dentro de sitios.|Servidor de sistema de sitio|  
|chmgr.log|Registra las actividades del administrador de mantenimiento del cliente.|Servidor de sitio|  
|Cidm.log|Registra los cambios realizados en la configuración de cliente por el administrador de datos de instalación de cliente (CIDM).|Servidor de sitio|  
|colleval.log|Registra los detalles acerca de la creación, cambio y eliminación de recopilaciones por parte del Evaluador de recopilaciones.|Servidor de sitio|  
|compmon.log|Registra el estado de los subprocesos de componente supervisados del servidor de sitio.|Servidor de sistema de sitio|  
|compsumm.log|Registra tareas del generador de resumen de estado de componente.|Servidor de sitio|  
|ComRegSetup.log|Registra los resultados de la instalación inicial del registro de COM para un servidor de sitio.|Servidor de sistema de sitio|  
|dataldr.log|Registra información sobre el procesamiento de archivos MIF y el inventario de hardware en la base de datos de Configuration Manager.|Servidor de sitio|  
|ddm.log|Registra actividades del administrador de datos de detección.|Servidor de sitio|  
|despool.log|Registra las transferencias de comunicaciones de sitio a sitio entrantes.|Servidor de sitio|  
|distmgr.log|Registra detalles acerca de las actualizaciones de información, la creación, la compresión y la replicación de datos de paquetes.|Servidor de sitio|  
|EPCtrlMgr.log|Registra información sobre la sincronización de información de amenazas de malware desde el servidor de rol de sistema de sitio de Endpoint Protection en la base de datos de Configuration Manager.|Servidor de sitio|  
|EPMgr.log|Registra el estado del rol de sistema de sitio de Endpoint Protection.|Servidor de sistema de sitio|  
|EPSetup.log|Proporciona información sobre la instalación del rol de sistema de sitio de Endpoint Protection.|Servidor de sistema de sitio|  
|EnrollSrv.log|Registra actividades del proceso de servicio de inscripción.|Servidor de sistema de sitio|  
|EnrollWeb.log|Registra actividades del proceso de sitio web de inscripción.|Servidor de sistema de sitio|  
|fspmgr.log|Registra las actividades del rol de sistema de sitio de punto de estado de reserva.|Servidor de sistema de sitio|  
|hman.log|Registra información sobre los cambios de configuración de sitio y la publicación de información de sitio en Servicios de dominio de Active Directory.|Servidor de sitio|  
|Inboxast.log|Registra los archivos que se mueven del punto de administración a la carpeta INBOXES correspondiente en el servidor de sitio.|Servidor de sitio|  
|inboxmgr.log|Registra actividades de transferencia de archivos entre las carpetas de bandeja de entrada.|Servidor de sitio|  
|inboxmon.log|Registra el procesamiento de archivos de la bandeja de entrada y las actualizaciones de contador de rendimiento.|Servidor de sitio|  
|invproc.log|Registra el reenvío de archivos MIF de un sitio secundario a su sitio primario.|Servidor de sitio|  
|migmctrl.log|Registra información sobre las acciones de migración que implican trabajos de migración, puntos de distribución compartidos y actualizaciones de puntos de distribución.|Sitio de nivel superior de la jerarquía de Configuration Manager y cada sitio primario secundario.<br /><br /> En una jerarquía de varios sitios primarios, use el archivo de registro creado en el sitio de administración central.|  
|mpcontrol.log|Registra el registro del punto de administración en el Servicio de nombres de Internet de Windows (WINS). Registra la disponibilidad del punto de administración cada 10 minutos.|Servidor de sistema de sitio|  
|mpfdm.log|Registra las acciones del componente de punto de administración que mueve los archivos de cliente a la carpeta INBOXES correspondiente en el servidor de sitio.|Servidor de sistema de sitio|  
|mpMSI.log|Registra los detalles sobre la instalación de un punto de administración.|Servidor de sitio|  
|MPSetup.log|Registra el proceso empaquetador de instalación de punto de administración.|Servidor de sitio|  
|netdisc.log|Registra acciones de detección de redes.|Servidor de sitio|  
|ntsvrdis.log|Registra la actividad de detección de servidores de sistema de sitio.|Servidor de sitio|  
|Objreplmgr|Registra el procesamiento de notificaciones de cambio de objeto para la replicación.|Servidor de sitio|  
|offermgr.log|Registra actualizaciones de anuncio.|Servidor de sitio|  
|offersum.log|Registra el resumen de mensajes de estado de implementación.|Servidor de sitio|  
|OfflineServicingMgr.log|Registra actividades de aplicación de actualizaciones a archivos de imagen de sistema operativo.|Servidor de sitio|  
|outboxmon.log|Registra el procesamiento de archivos de la bandeja de salida y las actualizaciones de contador de rendimiento.|Servidor de sitio|  
|PerfSetup.log|Registra los resultados de la instalación de contadores de rendimiento.|Servidor de sistema de sitio|  
|PkgXferMgr.log|Registra las acciones del componente SMS_Executive que se encarga de enviar contenido desde un sitio primario a un punto de distribución remoto.|Servidor de sitio|  
|policypv.log|Registra las actualizaciones de las directivas de cliente para reflejar cambios de configuraciones o implementaciones de cliente.|Servidor de sitio primario|  
|rcmctrl.log|Registra las actividades de replicación de base de datos entre los sitios de la jerarquía.|Servidor de sitio|  
|replmgr.log|Registra la replicación de archivos entre los componentes de servidor de sitio y el componente de programador.|Servidor de sitio|  
|ResourceExplorer.log|Registra errores, advertencias e información sobre la ejecución del Explorador de recursos.|Equipo que ejecuta la consola de Configuration Manager|  
|ruleengine.log|Registra detalles acerca de las reglas de implementación automática de identificación, descarga de contenido y creación de grupos de actualizaciones de software e implementación.|Servidor de sitio|  
|schedule.log|Registra detalles acerca de la replicación de archivos y trabajos de sitio a sitio.|Servidor de sitio|  
|sender.log|Registros los archivos que se transfieren mediante la replicación basada en archivos entre sitios.|Servidor de sitio|  
|sinvproc.log|Registra información acerca del procesamiento de datos de inventario de software en la base de datos del sitio.|Servidor de sitio|  
|sitecomp.log|Registra detalles sobre el mantenimiento de los componentes de sitio instalados en todos los servidores de sistema de sitio en el sitio.|Servidor de sitio|  
|sitectrl.log|Registra cambios de configuración de sitio realizados en objetos de control de sitio en la base de datos.|Servidor de sitio|  
|sitestat.log|Registra el proceso de supervisión de disponibilidad y espacio en disco de todos los sistemas de sitio.|Servidor de sitio|  
|SmsAdminUI.log|Registra la actividad de consola de Configuration Manager.|Equipo que ejecuta la consola de Configuration Manager|  
|SMSAWEBSVCSetup.log|Registra las actividades de instalación del servicio web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|smsbkup.log|Registra el resultado de la salida del proceso de copia de seguridad de sitio.|Servidor de sitio|  
|smsdbmon.log|Registra los cambios de la base de datos.|Servidor de sitio|  
|SMSENROLLSRVSetup.log|Registra las actividades de instalación del servicio web de inscripción.|Servidor de sistema de sitio|  
|SMSENROLLWEBSetup.log|Registra las actividades de instalación de sitio web de inscripción.|Servidor de sistema de sitio|  
|smsexec.log|Registra el procesamiento de todos los subprocesos de componente de servidor de sitio.|Servidor de sitio o servidor de sistema de sitio|  
|SMSFSPSetup.log|Registra mensajes generados por la instalación de un punto de estado de reserva.|Servidor de sistema de sitio|  
|SMSPORTALWEBSetup.log|Registra las actividades de instalación del sitio web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|SMSProv.log|Registra el acceso del proveedor de WMI a la base de datos del sitio.|Equipo con el proveedor de SMS|  
|srsrpMSI.log|Registra resultados detallados del proceso de instalación del punto de notificación desde la salida de MSI.|Servidor de sistema de sitio|  
|srsrpsetup.log|Registra los resultados del proceso de instalación del punto de notificación.|Servidor de sistema de sitio|  
|statesys.log|Registra el procesamiento de mensajes de sistema de estado.|Servidor de sitio|  
|statmgr.log|Registra la escritura de todos los mensajes de estado en la base de datos.|Servidor de sitio|  
|swmproc.log|Registra el procesamiento de archivos y configuraciones de disponibilidad.|Servidor de sitio|  

###  <a name="BKMK_SiteInstallLog"></a> Archivos de registro de instalación de servidor de sitio  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la instalación de sitios.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Registra actividades de instalación y evaluación de componente de requisito previo.|Servidor de sitio|  
|ConfigMgrSetup.log|Registra resultados detallados del programa de instalación de servidor de sitio.|Servidor de sitio|  
|ConfigMgrSetupWizard.log|Registra información relacionada con la actividad del Asistente para instalación.|Servidor de sitio|  
|SMS_BOOTSTRAP.log|Registra información sobre el progreso del inicio del proceso de instalación de sitio secundario. Los detalles del proceso de instalación figuran en ConfigMgrSetup.log.|Servidor de sitio|  
|smstsvc.log|Registra información sobre la instalación, el uso y la eliminación de un servicio de Windows que se usa para probar la conectividad de red y los permisos entre servidores, mediante la cuenta de equipo del servidor que inicia la conexión.|Registros de servidor de sistema de sitio y servidor de sitio|  

###  <a name="BKMK_FSPLog"></a> Archivos de registro de punto de estado de reserva  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el punto de estado de reserva.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Registra detalles acerca de las comunicaciones con el punto de estado de reserva de los clientes heredados de dispositivo móvil y los equipos cliente.|Servidor de sistema de sitio|  
|fspMSI.log|Registra mensajes generados por la instalación de un punto de estado de reserva.|Servidor de sistema de sitio|  
|fspmgr.log|Registra las actividades del rol de sistema de sitio de punto de estado de reserva.|Servidor de sistema de sitio|  

###  <a name="BKMK_MPLog"></a> Archivos de registro de punto de administración  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el punto de administración.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Registra actividades de mensajes de cliente en el extremo.|Servidor de sistema de sitio|  
|MP_CliReg.log|Registra la actividad de registro de cliente procesada por el punto de administración.|Servidor de sistema de sitio|  
|MP_Ddr.log|Registra la conversión de registros XML.ddr de clientes y luego los copia en el servidor de sitio.|Servidor de sistema de sitio|  
|MP_Framework.log|Registra las actividades de los componentes principales del punto de administración y del marco de cliente.|Servidor de sistema de sitio|  
|MP_GetAuth.log|Registra la actividad de autorización de cliente.|Servidor de sistema de sitio|  
|MP_GetPolicy.log|Registra las actividades de solicitud de directiva de equipos cliente.|Servidor de sistema de sitio|  
|MP_Hinv.log|Registra detalles acerca de la conversión de registros XML de inventario de hardware de clientes y los copia en el servidor de sitio.|Servidor de sistema de sitio|  
|MP_Location.log|Registra actividades de respuesta y solicitud de ubicación de clientes.|Servidor de sistema de sitio|  
|MP_OOBMgr.log|Registra las actividades de punto de administración relacionadas con la recepción de una OTP de un cliente.|Servidor de sistema de sitio|  
|MP_Policy.log|Registra la comunicación de directivas.|Servidor de sistema de sitio|  
|MP_Relay.log|Registra la transferencia de archivos recopilados del cliente.|Servidor de sistema de sitio|  
|MP_Retry.log|Registra procesos de reintento de inventario de hardware.|Servidor de sistema de sitio|  
|MP_Sinv.log|Registra detalles acerca de la conversión de registros XML de inventario de software de clientes y los copia en el servidor de sitio.|Servidor de sistema de sitio|  
|MP_SinvCollFile.log|Registra los detalles acerca de la recopilación de archivos.|Servidor de sistema de sitio|  
|MP_Status.log|Registra detalles acerca de la conversión de archivos XML.svf de mensaje de estado de clientes y los copia en el servidor de sitio.|Servidor de sistema de sitio|  
|mpcontrol.log|Registra el registro del punto de administración en WINS. Registra la disponibilidad del punto de administración cada 10 minutos.|Servidor de sitio|  
|mpfdm.log|Registra las acciones del componente de punto de administración que mueve los archivos de cliente a la carpeta INBOXES correspondiente en el servidor de sitio.|Servidor de sistema de sitio|  
|mpMSI.log|Registra los detalles sobre la instalación de un punto de administración.|Servidor de sitio|  
|MPSetup.log|Registra el proceso empaquetador de instalación de punto de administración.|Servidor de sitio|  

###  <a name="BKMK_SUPLog"></a> Archivos de registro de punto de actualización de software  
 En la tabla siguiente se indican los archivos de registro que contienen información relacionada con el punto de actualización de software.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Registra detalles sobre la replicación de archivos de notificación de actualizaciones de software de un sitio primario a sitios secundarios.|Servidor de sitio|  
|PatchDownloader.log|Registra detalles sobre el proceso de descarga de actualizaciones de software del origen de actualizaciones al destino de descarga en el servidor de sitio.|Equipo que hospeda la consola de Configuration Manager desde la que se inician las descargas|  
|ruleengine.log|Registra detalles acerca de las reglas de implementación automática de identificación, descarga de contenido y creación de grupos de actualizaciones de software e implementación.|Servidor de sitio|  
|SUPSetup.log|Registra detalles acerca de la instalación de un punto de actualización de software. Cuando se completa la instalación del punto de actualización de software, **Installation was successful** se escribe en este archivo de registro.|Servidor de sistema de sitio|  
|WCM.log|Registra los detalles sobre la configuración del punto de actualización de software y las conexiones con el servidor WSUS para las clasificaciones, idiomas y categorías de actualizaciones suscritas.|Servidor de sitio que se conecta al servidor WSUS|  
|WSUSCtrl.log|Registra los detalles acerca de la configuración, la conectividad de base de datos y el estado del servidor WSUS para el sitio.|Servidor de sistema de sitio|  
|wsyncmgr.log|Registra detalles sobre el proceso de sincronización de actualizaciones de software.|Servidor de sistema de sitio|  
|WUSSyncXML.log|Registra detalles sobre la herramienta de inventario para el proceso de sincronización de Microsoft Updates.|Equipo cliente configurado como host de sincronización para la herramienta de inventario para Microsoft Updates|  

##  <a name="BKMK_FunctionLogs"></a> Archivos de registro para las funcionalidades de Configuration Manager  
 En las secciones siguientes se muestran archivos de registro relacionados con las funciones de Configuration Manager.  

###  <a name="BKMK_AppManageLog"></a> Administración de aplicaciones  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la administración de aplicaciones.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Registra los detalles sobre el estado actual y previsto de las aplicaciones, su aplicabilidad, los tipos de implementación, las dependencias y si se cumplieron los requisitos.|Cliente|  
|AppDiscovery.log|Registra los detalles sobre la detección de aplicaciones en equipos cliente.|Cliente|  
|AppEnforce.log|Registra detalles acerca de las medidas de cumplimiento (instalar y desinstalar) que las aplicaciones llevan a cabo en el cliente.|Cliente|  
|awebsctl.log|Registra actividades de supervisión del rol de sistema de sitio de punto de servicio web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|awebsvcMSI.log|Registra información detallada de instalación del rol de sistema de sitio de punto de servicio web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|CCMSDKProvider.log|Registra las actividades del SDK de administración de aplicaciones.|Cliente|  
|colleval.log|Registra los detalles acerca de la creación, cambio y eliminación de recopilaciones por parte del Evaluador de recopilaciones.|Servidor de sistema de sitio|  
|ConfigMgrSoftwareCatalog.log|Registra la actividad del catálogo de aplicaciones, que incluye el uso de Silverlight.|Cliente|  
|portlctl.log|Registra las actividades de supervisión del rol de sistema de sitio de punto de sitios web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|portlwebMSI.log|Registra la actividad de instalación de MSI del rol de sitio web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|PrestageContent.log|Registra detalles sobre el uso de la herramienta ExtractContent.exe en un punto de distribución preconfigurado remoto. Esta herramienta extrae el contenido que ha sido exportado a un archivo.|Servidor de sistema de sitio|  
|ServicePortalWebService.log|Registra la actividad del servicio web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|ServicePortalWebSite.log|Registra la actividad del sitio web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|SMSdpmon.log|Registra los detalles acerca de la tarea programada de supervisión de estado de punto de distribución configurada en un punto de distribución.|Servidor de sitio|  
|SoftwareCatalogUpdateEndpoint.log|Registra actividades para administrar la dirección URL del catálogo de aplicaciones que se muestra en el Centro de software.|Cliente|  
|SoftwareCenterSystemTasks.log|Registra actividades relacionadas con la validación de componente de requisito previo del Centro de software.|Cliente|  

 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la implementación de paquetes y programas.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|colleval.log|Registra los detalles acerca de la creación, cambio y eliminación de recopilaciones por parte del Evaluador de recopilaciones.|Servidor de sitio|  
|execmgr.log|Registra los detalles acerca de los paquetes y las secuencias de tareas que se ejecutan.|Cliente|  

###  <a name="BKMK_AILog"></a> Asset Intelligence  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con Asset Intelligence.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Registra las actividades de las acciones de inventario de Asset Intelligence.|Cliente|  
|aikbmgr.log|Registra los detalles acerca del procesamiento de archivos XML de la bandeja de entrada para la actualización del catálogo Asset Intelligence.|Servidor de sitio|  
|AIUpdateSvc.log|Registra la interacción del punto de sincronización de Asset Intelligence con System Center Online (SCO), el servicio web en línea.|Servidor de sistema de sitio|  
|AIUSMSI.log|Registra detalles sobre la instalación del rol de sistema de sitio de punto de sincronización de Asset Intelligence.|Servidor de sistema de sitio|  
|AIUSSetup.log|Registra detalles sobre la instalación del rol de sistema de sitio de punto de sincronización de Asset Intelligence.|Servidor de sistema de sitio|  
|ManagedProvider.log|Registra detalles acerca de la detección de software con una etiqueta de identificación de software asociada. También registra actividades relacionadas con el inventario de hardware.|Servidor de sistema de sitio|  
|MVLSImport.log|Registra detalles acerca del procesamiento de archivos de licencia importados.|Servidor de sistema de sitio|  

###  <a name="BKMK_BnRLog"></a> Copia de seguridad y recuperación  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con acciones de copia de seguridad y de recuperación, incluidos el restablecimiento de sitio y los cambios en el proveedor de SMS.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Registra información sobre tareas del programa de instalación y de recuperación cuando Configuration Manager recupera un sitio mediante una copia de seguridad.|Servidor de sitio|  
|smsbkup.log|Registra los detalles acerca de la actividad de la copia de seguridad del sitio.|Servidor de sitio|  
|smssqlbkup.log|Registra la salida del proceso de copia de seguridad de base de datos del sitio cuando se instala SQL Server en un servidor que no es el servidor de sitio.|Servidor de base de datos del sitio|  
|Smswriter.log|Registra información sobre el estado de Configuration Manager VSS Writer utilizado por el proceso de copia de seguridad.|Servidor de sitio|  

###  <a name="BKMK_CertificateEnrollment"></a> Inscripción de certificado  
 En la tabla siguiente se incluyen los archivos de registro de Configuration Manager que contienen información relacionada con la inscripción de certificados. La inscripción de certificados usa el punto de registro de certificado y el módulo de directivas de Configuration Manager en el servidor que ejecuta el servicio de inscripción de dispositivos de red.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|Crp.log|Registra actividades de inscripción.|Punto de registro de certificado|  
|Crpctrl.log|Registra el estado operativo del punto de registro de certificado.|Punto de registro de certificado|  
|Crpsetup.log|Registra detalles sobre la instalación y configuración del punto de registro de certificado.|Punto de registro de certificado|  
|Crpmsi.log|Registra detalles sobre la instalación y configuración del punto de registro de certificado.|Punto de registro de certificado|  
|NDESPlugin.log|Registra actividades de inscripción de certificado y verificación de desafío.|Módulo de directivas de Configuration Manager y el servicio de inscripción de dispositivos de red|  

 Además de los archivos de registro de Configuration Manager, revise los registros de aplicaciones de Windows en el Visor de eventos del servidor que ejecuta el Servicio de inscripción de dispositivos de red y el servidor que hospeda el punto de registro de certificado. Por ejemplo, busque mensajes del origen **NetworkDeviceEnrollmentService**. También puede utilizar los siguientes archivos de registro:  

-   Archivos de registro de IIS para el Servicio de inscripción de dispositivos de red: **&lt;ruta de acceso\>inetpub\logs\LogFiles\W3SVC1**  

-   Archivos de registro de IIS para el punto de registro de certificados: **&lt;ruta de acceso\>\inetpub\logs\LogFiles\W3SVC1**  

-   Archivo de registro de directiva de inscripción de dispositivos de red: **mscep.log**  

    > [!NOTE]  
    >  Este archivo se encuentra en la carpeta del perfil de cuenta de Servicio de inscripción de dispositivos de red, por ejemplo, en C:\Users\SCEPSvc. Para obtener más información sobre cómo habilitar el registro para el Servicio de inscripción de dispositivos de red, consulte [Habilitar registro](http://go.microsoft.com/fwlink/?LinkId=320576) en el artículo Servicio de inscripción de dispositivos de red (NDES) en Servicios de certificados de Active Directory (AD CS) en la wiki de TechNet.  

###  <a name="BKMK_BGB"></a> Notificación de cliente  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la notificación de cliente.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Registra detalles sobre actividades del servidor de sitio relacionadas con tareas de notificación de cliente y procesamiento en línea, y archivos de estado de tarea.|Servidor de sitio|  
|BGBServer.log|Registra las actividades del servidor de notificación, como la comunicación entre cliente y servidor y las tareas de inserción en clientes. También registra información sobre la generación de archivos de estado de tareas y en línea que se enviarán al servidor del sitio.|Punto de administración|  
|BgbSetup.log|Registra las actividades del proceso empaquetador de instalación de servidor de notificaciones durante la instalación y desinstalación.|Punto de administración|  
|bgbisapiMSI.log|Registra los detalles sobre la instalación y desinstalación del servidor de notificaciones.|Punto de administración|  
|BgbHttpProxy.log|Registra las actividades del proxy HTTP de notificación cuando retransmite mensajes de clientes que utilizan HTTP a y desde el servidor de notificaciones.|Cliente|  
|CCMNotificationAgent.log|Registra actividades del agente de notificación, por ejemplo, la comunicación entre cliente y servidor e información sobre las tareas recibidas y enviadas a otros agentes cliente.|Cliente|  

### <a name="cloud-management-gateway"></a>Puerta de enlace de administración en la nube

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la puerta de enlace de administración en la nube.

||||
|-|-|-|
|Nombre del registro|Descripción|Equipo con el archivo de registro|
|CloudMgr.log|Registra detalles sobre la implementación del servicio de puerta de enlace de administración en la nube, el estado del servicio en curso y datos de uso asociados con el servicio.<br>Puede configurar el nivel de registro si modifica el registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_CLOUD_SERVICES_MANAGER\Logging level**|La carpeta **SMS/Registros** del servidor de sistema de sitio|
|CMGSetup.log o CMG-*RoleInstanceID*-CMGSetup.log<sup>1</sup>|Registra detalles sobre la segunda fase de la implementación de Cloud Management Gateway (implementación local en Azure).<br>Puede configurar el nivel de registro mediante la configuración de **Nivel de seguimiento** [**Información** (predeterminada), **Detallado**, **Error**] en la pestaña de **configuración de Azure Portal\Cloud Services**.|**%approot%\logs** en el servidor de Azure o la carpeta SMS/Registros en el servidor de sistema de sitio|
|CMGHttpHandler.log o CMG-*RoleInstanceID*- CMGHttpHandler.log<sup>1</sup>|Registra detalles sobre el enlace el controlador http de Cloud Management Gateway con Internet Information Services en Azure.<br>Puede configurar el nivel de registro mediante la configuración de **Nivel de seguimiento** [**Información** (predeterminada), **Detallado**, **Error**] en la pestaña de **configuración de Azure Portal\Cloud Services**.|**%approot%\logs** en el servidor de Azure o la carpeta SMS/Registros en el servidor de sistema de sitio|
|CMGService.log o CMG-*RoleInstanceID*- CMGService.log<sup>1</sup>|Registra detalles sobre el componente principal del servicio Cloud Management Gateway en Azure.<br>Puede configurar el nivel de registro mediante la configuración de **Nivel de seguimiento** [**Información** (predeterminada), **Detallado**, **Error**] en la pestaña de **configuración de Azure Portal\Cloud Services**.|**%approot%\logs** en el servidor de Azure o la carpeta SMS/Registros en el servidor de sistema de sitio|
|SMS_Cloud_ProxyConnector.log|Registra detalles sobre la configuración de conexiones entre el servicio de puerta de enlace de administración en la nube y el punto de conexión de la puerta de enlace de administración en la nube.|Servidor de sistema de sitio|

<sup>1</sup> Se trata de archivos de registro locales de Configuration Manager que el administrador de servicio en la nube sincroniza desde Azure Storage cada 5 minutos. Cloud Management Gateway insertará registros en Azure Storage cada 5 minutos. Por tanto, el retraso máximo será de 10 minutos. Los modificadores detallados afectarán a los registros locales y remotos.

- Para solucionar problemas con implementaciones, use **CloudMgr.log** y **CMGSetup.log**
- Para solucionar problemas de estado del servicio, utilice **CMGService.log** y **SMS_Cloud_ProxyConnector.log**.
- Para solucionar problemas de tráfico de cliente, utilice **CMGHttpHandler.log**, **CMGService.log** y **SMS_Cloud_ProxyConnector.log**.

###  <a name="BKMK_CompSettingsLog"></a> Configuración de cumplimiento y acceso a los recursos de la compañía  
 En la tabla siguiente se muestran los archivos de registro que contienen información relacionada con la configuración de cumplimiento y el acceso a los recursos de la compañía.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Registra detalles sobre el proceso de corrección y cumplimiento de configuraciones de cumplimiento, actualizaciones de software y administración de aplicaciones.|Cliente|  
|CITaskManager.log|Registra información acerca de la programación de tareas de elemento de configuración.|Cliente|  
|DCMAgent.log|Registra información de alto nivel acerca de la evaluación, notificación de conflictos y corrección de elementos de configuración y aplicaciones.|Cliente|  
|DCMReporting.log|Registra información acerca de resultados de plataforma de directiva de informes en mensajes de estado de elementos de configuración.|Cliente|  
|DcmWmiProvider.log|Registra información sobre la lectura de synclets de elemento de configuración de WMI.|Cliente|  

###  <a name="BKMK_ConsoleLog"></a> Consola de Configuration Manager  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la consola de Configuration Manager.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Registra la instalación de la consola de Configuration Manager.|Equipo que ejecuta la consola de Configuration Manager|  
|SmsAdminUI.log|Registra información acerca del funcionamiento de la consola de Configuration Manager.|Equipo que ejecuta la consola de Configuration Manager|  
|SMSProv.log|Registra las actividades realizadas por el proveedor de SMS. Las actividades de la consola de Configuration Manager usan el proveedor de SMS.|Servidor de sitio o servidor de sistema de sitio|  

###  <a name="BKMK_ContentLog"></a> Administración de contenido  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la administración de contenido.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|CloudDP-&lt;guid\>.log|Registra detalles de un determinado punto de distribución basado en la nube, como información acerca del acceso a almacenamiento y contenido.|Servidor de sistema de sitio|  
|CloudMgr.log|Registra detalles sobre el aprovisionamiento de contenido, la recopilación de estadísticas de ancho de banda y almacenamiento, y las acciones iniciadas por el administrador para detener o iniciar el servicio de nube que ejecuta un punto de distribución basado en la nube.|Servidor de sistema de sitio|  
|DataTransferService.log|Registra todas las comunicaciones de BITS para el acceso de directiva o paquete. Los puntos de distribución de extracción también usan este registro para la administración de contenido.|Equipo configurado como punto de distribución de extracción|  
|PullDP.log|Registra los detalles sobre el contenido que el punto de distribución de extracción transfiere de puntos de distribución de origen.|Equipo configurado como punto de distribución de extracción|  
|PrestageContent.log|Registra los detalles sobre el uso de la herramienta ExtractContent.exe en un punto de distribución preconfigurado remoto. Esta herramienta extrae el contenido que ha sido exportado a un archivo.|Rol de sistema de sitio|  
|SMSdpmon.log|Registra detalles sobre tareas programadas de supervisión de estado de punto de distribución configuradas en un punto de distribución.|Rol de sistema de sitio|  
|smsdpprov.log|Registra detalles acerca de la extracción de archivos comprimidos recibidos de un sitio primario. El proveedor de WMI del punto de distribución remoto genera este registro.|Equipo de punto de distribución que no comparte ubicación con el servidor de sitio|  


###  <a name="BKMK_DiscoveryLog"></a> Detección  
En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la detección.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Registra acciones de detección de grupos de seguridad de Active Directory.|Servidor de sitio|  
|adsysdis.log|Registra acciones de detección de sistema de Active Directory.|Servidor de sitio|  
|adusrdis.log|Registra acciones de detección de usuarios de Active Directory.|Servidor de sitio|  
|ADForestDisc.log|Registra acciones de detección de bosques de Active Directory.|Servidor de sitio|  
|ddm.log|Registra actividades del administrador de datos de detección.|Servidor de sitio|  
|InventoryAgent.log|Registra actividades de acciones de inventario de hardware, inventario de software y detección de latido en el cliente.|Cliente|  
|netdisc.log|Registra acciones de detección de redes.|Servidor de sitio|  

###  <a name="BKMK_EPLog"></a> Endpoint Protection  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con Endpoint Protection.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Registra detalles sobre la instalación del cliente de Endpoint Protection y la aplicación de directiva antimalware en el cliente.|Cliente|  
|EPCtrlMgr.log|Registra detalles sobre la sincronización de información de amenazas de malware del servidor de rol de Endpoint Protection con la base de datos de Configuration Manager.|Servidor de sistema de sitio|  
|EPMgr.log|Supervisa el estado del rol de sistema de sitio de Endpoint Protection.|Servidor de sistema de sitio|  
|EPSetup.log|Proporciona información sobre la instalación del rol de sistema de sitio de Endpoint Protection.|Servidor de sistema de sitio|  

###  <a name="BKMK_Extensions"></a> Extensiones  
 En la siguiente tabla se enumeran los archivos de registro que contienen información relacionada con las extensiones.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Registra información sobre la descarga de extensiones de Microsoft y la instalación y desinstalación de todas las extensiones.|Equipo que ejecuta la consola de Configuration Manager|  
|FeatureExtensionInstaller.log|Registra información sobre la instalación y desinstalación de extensiones individuales cuando están habilitadas o deshabilitadas en la consola de Configuration Manager.|Equipo que ejecuta la consola de Configuration Manager|  
|SmsAdminUI.log|Registra la actividad de consola de Configuration Manager.|Equipo que ejecuta la consola de Configuration Manager|  

###  <a name="BKMK_InventoryLog"></a> Inventario  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con los datos de inventario de procesamiento.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Registra información sobre el procesamiento de archivos MIF y el inventario de hardware en la base de datos de Configuration Manager.|Servidor de sitio|  
|invproc.log|Registra el reenvío de archivos MIF de un sitio secundario a su sitio primario.|Servidor de sitio secundario|  
|sinvproc.log|Registra información acerca del procesamiento de datos de inventario de software en la base de datos del sitio.|Servidor de sitio|  

###  <a name="BKMK_MeteringLog"></a> Medición  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la disponibilidad.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Supervisa todos los procesos de disponibilidad de software.|Servidor de sitio|  

###  <a name="BKMK_MigrationLog"></a> Migración  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la migración.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Registra información acerca de las acciones de migración que implican trabajos de migración, puntos de distribución compartidos y actualizaciones de puntos de distribución.|Sitio de nivel superior de la jerarquía de Configuration Manager y cada sitio primario secundario.<br /><br /> En una jerarquía de varios sitios primarios, utilice el archivo de registro creado en el sitio de administración central.|  

###  <a name="BKMK_MDMLog"></a> Dispositivos móviles  
 En las secciones siguientes se incluyen los archivos de registro que contienen información relacionada con la administración de dispositivos móviles.  

####  <a name="BKMK_EnrollmentLog"></a> Inscripción  
 En la tabla siguiente se incluyen los registros que contienen información relacionada con la inscripción de dispositivos móviles.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Registra la comunicación entre puntos de administración habilitados para dispositivos móviles y los extremos de punto de administración.|Servidor de sistema de sitio|  
|dmpmsi.log|Registra los datos de Windows Installer para la configuración de un punto de administración habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DMPSetup.log|Registra la configuración del punto de administración cuando está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|enrollsrvMSI.log|Registra los datos de Windows Installer para la configuración de un punto de inscripción.|Servidor de sistema de sitio|  
|enrollmentweb.log|Registra la comunicación entre dispositivos móviles y el punto de proxy de inscripción.|Servidor de sistema de sitio|  
|enrollwebMSI.log|Registra los datos de Windows Installer para la configuración de un punto de proxy de inscripción.|Servidor de sistema de sitio|  
|enrollmentservice.log|Registra la comunicación entre un punto de proxy de inscripción y un punto de inscripción.|Servidor de sistema de sitio|  
|SMS_DM.log|Registra la comunicación entre dispositivos móviles, equipos Mac y el punto de administración habilitado para dispositivos móviles y equipos Mac.|Servidor de sistema de sitio|  

####  <a name="BKMK_ExchSrvLog"></a> Conector de Exchange Server  
 Los registros siguientes contienen información relacionada con el conector de Exchange Server.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Registra las actividades y el estado del conector de Exchange Server.|Servidor de sitio|  

####  <a name="BKMK_MDLegLog"></a> Herencia de dispositivo móvil  
 En la tabla siguiente se incluyen los registros que contienen información relacionada con el cliente heredado de dispositivo móvil.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Registra detalles acerca de datos de inscripción de certificados en clientes heredados de dispositivos móviles.|Cliente|  
|DMCertResp.htm|Registra la respuesta HTML del servidor de certificados cuando el programa de inscripción de cliente heredado de dispositivos móviles solicita un certificado PKI.|Cliente|  
|DmClientHealth.log|Registra los GUID de todos los clientes heredados de dispositivos móviles que se comunican con el punto de administración que está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DmClientRegistration.log|Registra las solicitudes y respuestas de registro a y desde clientes heredados de dispositivos móviles.|Servidor de sistema de sitio|  
|DmClientSetup.log|Registra datos de instalación de cliente para clientes heredados de dispositivos móviles.|Cliente|  
|DmClientXfer.log|Registra datos de transferencia de clientes para clientes heredados de dispositivos móviles y para implementaciones de ActiveSync.|Cliente|  
|DmCommonInstaller.log|Registra la instalación de archivos de transferencia de cliente para configurar archivos de transferencia de cliente heredado de dispositivos móviles.|Cliente|  
|DmInstaller.log|Registra si DMInstaller llama correctamente a DmClientSetup, y si sale de DmClientSetup correcta o incorrectamente para clientes heredados de dispositivos móviles.|Cliente|  
|DmpDatastore.log|Registra todas las conexiones de base de datos de sitio y las consultas realizadas por el punto de administración que está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DmpDiscovery.log|Registra todos los datos de detección de los clientes heredados de dispositivos móviles en el punto de administración que está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DmpHardware.log|Registra los datos de inventario de hardware de los clientes heredados de dispositivos móviles en el punto de administración que está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DmpIsapi.log|Registra la comunicación de cliente heredado de dispositivos móviles con un punto de administración que está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|dmpmsi.log|Registra los datos de Windows Installer para la configuración de un punto de administración habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DMPSetup.log|Registra la configuración del punto de administración cuando está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DmpSoftware.log|Registra los datos de distribución de software de los clientes heredados de dispositivos móviles en el punto de administración que está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DmpStatus.log|Registra los datos de mensajes de estado de los clientes de dispositivos móviles en un punto de administración que está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DmSvc.log|Registra la comunicación de clientes heredados de dispositivos móviles con un punto de administración que está habilitado para dispositivos móviles.|Cliente|  
|FspIsapi.log|Registra detalles acerca de las comunicaciones con el punto de estado de reserva de los clientes heredados de dispositivo móvil y los equipos cliente.|Servidor de sistema de sitio|  

###  <a name="BKMK_OSDLog"></a> Implementación de sistema operativo  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la implementación de sistema operativo.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|CAS.log|Registra los detalles cuando se encuentran puntos de distribución de contenido al que se hace referencia.|Cliente|  
|ccmsetup.log|Registra tareas de ccmsetup de instalación, actualización y eliminación de cliente. Puede utilizarse para solucionar problemas de instalación de cliente.|Cliente|  
|CreateTSMedia.log|Registra los detalles de creación de medios de secuencia de tareas.|Equipo que ejecuta la consola de Configuration Manager|  
|DeployToVhd.log|Registra detalles sobre el proceso de creación y modificación de discos duros virtuales (VHD).|Equipo que ejecuta la consola de Configuration Manager|  
|Dism.log|Registra acciones de instalación del controlador o acciones de aplicación de actualizaciones para el mantenimiento sin conexión.|Servidor de sistema de sitio|  
|distmgr.log|Registra detalles sobre la configuración para habilitar un punto de distribución de Medio de ejecución anterior al inicio (PXE).|Servidor de sistema de sitio|  
|DriverCatalog.log|Registra los detalles acerca de los controladores de dispositivo que se han importado en el catálogo de controladores.|Servidor de sistema de sitio|  
|mcsisapi.log|Registra información de respuestas de solicitud de cliente y de transferencia de paquetes mediante multidifusión.|Servidor de sistema de sitio|  
|mcsexec.log|Registra acciones de comprobación de estado, espacio de nombres, creación de sesiones y comprobación de certificados.|Servidor de sistema de sitio|  
|mcsmgr.log|Registra cambios en la configuración, el modo de seguridad y la disponibilidad.|Servidor de sistema de sitio|  
|mcsprv.log|Registra la interacción del proveedor de multidifusión con los Servicios de implementación de Windows (WDS).|Servidor de sistema de sitio|  
|MCSSetup.log|Registra los detalles acerca de la instalación del rol del servidor de multidifusión.|Servidor de sistema de sitio|  
|MCSMSI.log|Registra los detalles acerca de la instalación del rol del servidor de multidifusión.|Servidor de sistema de sitio|  
|Mcsperf.log|Registra los detalles acerca de las actualizaciones de contador de rendimiento de multidifusión.|Servidor de sistema de sitio|  
|MP_ClientIDManager.log|Registra las respuestas de punto de administración a secuencias de tareas de solicitudes de identificador de cliente iniciadas desde PXE o desde medios de arranque.|Servidor de sistema de sitio|  
|MP_DriverManager.log|Registra las respuestas de puntos de administración a las solicitudes de acciones de secuencias de tareas de aplicación automática de controladores.|Servidor de sistema de sitio|  
|OfflineServicingMgr.log|Registra detalles de los planes de mantenimiento sin conexión y de las acciones de aplicación de actualizaciones en archivos Windows Imaging Format (WIM) de sistema operativo.|Servidor de sistema de sitio|  
|Setupact.log|Registra los detalles acerca de los registros de instalación y SysPrep de Windows.|Cliente|  
|Setupapi.log|Registra los detalles acerca de los registros de instalación y SysPrep de Windows.|Cliente|  
|Setuperr.log|Registra los detalles acerca de los registros de instalación y SysPrep de Windows.|Cliente|  
|smpisapi.log|Registra los detalles acerca de las acciones de restauración y captura de estado de cliente, así como información sobre umbrales.|Cliente|  
|Smpmgr.log|Registra los detalles acerca de los resultados de las comprobaciones de estado de punto de migración de estado y los cambios de configuración.|Servidor de sistema de sitio|  
|smpmsi.log|Registra los detalles de instalación y configuración acerca del punto de migración de estado.|Servidor de sistema de sitio|  
|smpperf.log|Registra las actualizaciones de contador de rendimiento de punto de migración de estado.|Servidor de sistema de sitio|  
|smspxe.log|Registra detalles sobre las respuestas a los clientes que usan arranque PXE y detalles sobre la expansión de archivos e imágenes de arranque.|Servidor de sistema de sitio|  
|smssmpsetup.log|Registra los detalles de instalación y configuración acerca del punto de migración de estado.|Servidor de sistema de sitio|  
|Smsts.log|Registra las actividades de secuencia de tareas.|Cliente|  
|TSAgent.log|Registra el resultado de las dependencias de secuencia de tareas antes de iniciar una secuencia de tareas.|Cliente|  
|TaskSequenceProvider.log|Registra los detalles acerca de las secuencias de tareas cuando se importan, exportan o editan.|Servidor de sistema de sitio|  
|loadstate.log|Registra los detalles acerca de la Herramienta de migración de estado de usuario (USMT) y la restauración de los datos de estado de usuario.|Cliente|  
|scanstate.log|Registra los detalles acerca de la Herramienta de migración de estado de usuario (USMT) y la captura de los datos de estado de usuario.|Cliente|  

###  <a name="BKMK_PowerMgmtLog"></a> Administración de energía  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la administración de energía.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|Pwrmgmt.log|Registra detalles sobre las actividades de administración de energía en el equipo cliente, que incluyen la supervisión y la aplicación de configuración por el agente cliente de administración de energía.|Cliente|  

###  <a name="BKMK_RCLog"></a> Control remoto  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el control remoto.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Registra los detalles acerca de la actividad del visor de control remoto.|En la carpeta %temp% del equipo que ejecuta el visor de control remoto|  

###  <a name="BKMK_ReportLog"></a> Generación de informes  
 En la tabla siguiente se incluyen los archivos de registro de Configuration Manager que contienen información relacionada con la generación de informes.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Registra información acerca de la actividad y el estado del punto de servicios de informes.|Servidor de sistema de sitio|  
|srsrpMSI.log|Registra resultados detallados del proceso de instalación del punto de servicios de informes desde la salida de MSI.|Servidor de sistema de sitio|  
|srsrpsetup.log|Registra los resultados del proceso de instalación del punto de servicios de informes.|Servidor de sistema de sitio|  

###  <a name="BKMK_RBALog"></a> Administración basada en roles  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la administración basada en roles.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|hman.log|Registra información sobre los cambios de configuración de sitio y la publicación de información de sitio en Servicios de dominio de Active Directory.|Servidor de sitio|  
|SMSProv.log|Registra el acceso del proveedor de WMI a la base de datos del sitio.|Equipo con el proveedor de SMS|  

###  <a name="BKMK_WITLog"></a> Punto de conexión de servicio  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el punto de conexión de servicio.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Registra información de cuenta de proxy y de certificado.|Servidor de sitio|  
|colleval.log|Registra los detalles acerca de la creación, cambio y eliminación de recopilaciones por parte del Evaluador de recopilaciones.|Sitio primario y sitio de administración central|  
|Cloudusersync.log|Registra la habilitación de licencia de usuarios.|Equipo con el punto de conexión de servicio|  
|dataldr.log|Registra información sobre el procesamiento de archivos MIF.|Servidor de sitio|  
|ddm.log|Registra actividades del administrador de datos de detección.|Servidor de sitio|  
|distmgr.log|Registra detalles acerca de las solicitudes de distribución de contenido.|Servidor de sitio de nivel superior|  
|Dmpdownloader.log|Registra detalles sobre las descargas desde Microsoft Intune.|Equipo con el punto de conexión de servicio|  
|Dmpuploader.log|Registra detalles relacionados con la carga de cambios de base de datos en Microsoft Intune.|Equipo con el punto de conexión de servicio|  
|hman.log|Registra información acerca del reenvío de mensajes.|Servidor de sitio|  
|objreplmgr.log|Registra el procesamiento de directivas y asignaciones.|Servidor de sitio primario|  
|policypv.log|Registra la generación de directivas de todas las directivas.|Servidor de sitio|  
|outgoingcontentmanager.log|Registra el contenido cargado en Microsoft Intune.|Equipo con el punto de conexión de servicio|  
|sitecomp.log|Registra los detalles de la instalación del de punto de conexión de servicio.|Servidor de sitio|  
|SmsAdminUI.log|Registra la actividad de consola de Configuration Manager.|Equipo que ejecuta la consola de Configuration Manager|  
|SMSProv.log|Registra las actividades realizadas por el proveedor de SMS. Las actividades de la consola de Configuration Manager usan el proveedor de SMS.|Equipo con el proveedor de SMS|  
|SrvBoot.log|Registra los detalles sobre el servicio de instalador de punto de conexión de servicio.|Equipo con el punto de conexión de servicio|  
|Statesys.log|Registra el procesamiento de mensajes de administración de dispositivos móviles.|Sitio primario y sitio de administración central|  

###  <a name="BKMK_SU_NAPLog"></a> Actualizaciones de software  
 En la tabla siguiente se indican los archivos de registro que contienen información relacionada con las actualizaciones de software.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|Ccmperf.log|Registra actividades relacionadas con el mantenimiento y la captura de datos relacionados con los contadores de rendimiento de cliente.|Cliente|  
|PatchDownloader.log|Registra detalles sobre el proceso de descarga de actualizaciones de software del origen de actualizaciones al destino de descarga en el servidor de sitio.|Equipo que hospeda la consola de Configuration Manager desde la que se inician las descargas|  
|PolicyEvaluator.log|Registra los detalles acerca de la evaluación de directivas en los equipos cliente, incluidas las directivas de las actualizaciones de software.|Cliente|  
|RebootCoordinator.log|Registra los detalles acerca de la coordinación de reinicios del sistema en los equipos cliente después de que se instalan las actualizaciones de software.|Cliente|  
|ScanAgent.log|Registra los detalles acerca de cómo examinar las solicitudes de actualización de software, la ubicación de WSUS y acciones relacionadas.|Cliente|  
|SdmAgent.log|Registra detalles sobre cómo realizar un seguimiento de la corrección y la compatibilidad. Pero en el archivo de registro de actualizaciones de software, Updateshandler.log, se proporcionan detalles más informativos sobre cómo instalar las actualizaciones de software necesarias a efectos de compatibilidad.<br /><br /> Este archivo de registro se comparte con la configuración de compatibilidad.|Cliente|  
|ServiceWindowManager.log|Registra los detalles acerca de la evaluación de las ventanas de mantenimiento.|Cliente|  
|SmsWusHandler.log|Registra los detalles sobre el proceso de análisis de la herramienta de inventario para Microsoft Update.|Cliente|  
|StateMessage.log|Registra detalles sobre los mensajes de estado de actualizaciones de software que se crean y envían al punto de administración.|Cliente|  
|SUPSetup.log|Registra detalles acerca de la instalación de un punto de actualización de software. Cuando se completa la instalación del punto de actualización de software, **Installation was successful** se escribe en este archivo de registro.|Servidor de sistema de sitio|  
|UpdatesDeployment.log|Registra los detalles acerca de las implementaciones en el cliente, incluidas la activación, evaluación y aplicación de las actualizaciones de software. En el registro detallado se muestra información adicional acerca de la interacción con la interfaz de usuario del cliente.|Cliente|  
|UpdatesHandler.log|Registra información sobre el análisis de compatibilidad de actualizaciones de software y la descarga e instalación de actualizaciones de software en el cliente.|Cliente|  
|UpdatesStore.log|Registra los detalles acerca del estado de compatibilidad de las actualizaciones de software evaluadas durante el ciclo de análisis de compatibilidad.|Cliente|  
|WCM.log|Registra detalles sobre la configuración del punto de actualización de software y las conexiones con el servidor WSUS para las clasificaciones, idiomas y categorías de actualizaciones suscritas.|Servidor de sitio|  
|WSUSCtrl.log|Registra los detalles acerca de la configuración, la conectividad de base de datos y el estado del servidor WSUS para el sitio.|Servidor de sistema de sitio|  
|wsyncmgr.log|Registra detalles sobre el proceso de sincronización de actualizaciones de software.|Servidor de sitio|  
|WUAHandler.log|Registra detalles acerca del agente de Windows Update en el cliente cuando busca actualizaciones de software.|Cliente|  

###  <a name="BKMK_WOLLog"></a> Wake On LAN  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el uso de Wake On LAN.  

> [!NOTE]  
>  Si complementa Wake on LAN con el uso de un proxy de reactivación, esta actividad se registra en el cliente. Por ejemplo, vea CcmExec.log y SleepAgent_<*dominio*\>@SYSTEM_0.log en la sección [Operaciones de cliente](#BKMK_ClientOpLogs) de este tema.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Registra los detalles acerca de los clientes a los que se deben enviar paquetes de reactivación, el número de paquetes de reactivación enviados y el número de paquetes de reactivación que se reintentaron.|Servidor de sitio|  
|wolmgr.log|Registra los detalles sobre los procedimientos de reactivación, como la reactivación de implementaciones configuradas para Wake on LAN.|Servidor de sitio|  

###  <a name="BKMK_WindowsServicingLog"></a>Mantenimiento de Windows 10  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el mantenimiento de Windows 10.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|Ccmperf.log|Registra actividades relacionadas con el mantenimiento y la captura de datos relacionados con los contadores de rendimiento de cliente.|Cliente|  
|CcmRepair.log|Registra las actividades de reparación del agente de cliente.|Cliente|
|PatchDownloader.log|Registra detalles sobre el proceso de descarga de actualizaciones de software del origen de actualizaciones al destino de descarga en el servidor de sitio.|Equipo que hospeda la consola de Configuration Manager desde la que se inician las descargas|  
|PolicyEvaluator.log|Registra los detalles acerca de la evaluación de directivas en los equipos cliente, incluidas las directivas de las actualizaciones de software.|Cliente|  
|RebootCoordinator.log|Registra los detalles acerca de la coordinación de reinicios del sistema en los equipos cliente después de que se instalan las actualizaciones de software.|Cliente|  
|ScanAgent.log|Registra los detalles acerca de cómo examinar las solicitudes de actualización de software, la ubicación de WSUS y acciones relacionadas.|Cliente|  
|SdmAgent.log|Registra detalles sobre cómo realizar un seguimiento de la corrección y la compatibilidad. Pero en el archivo de registro de actualizaciones de software, UpdatesHandler.log, se proporcionan detalles más informativos sobre cómo instalar las actualizaciones de software necesarias a efectos de compatibilidad.<br /><br /> Este archivo de registro se comparte con la configuración de compatibilidad.|Cliente|  
|ServiceWindowManager.log|Registra los detalles acerca de la evaluación de las ventanas de mantenimiento.|Cliente|  
|setupact.log|Archivo de registro principal para la mayoría de los errores que se producen durante el proceso de instalación de Windows. El archivo de registro se encuentra en la carpeta %windir%\$Windows.~BT\sources\panther.|Cliente|
|SmsWusHandler.log|Registra los detalles sobre el proceso de análisis de la herramienta de inventario para Microsoft Update.|Cliente|  
|StateMessage.log|Registra los detalles acerca de los mensajes de estado de actualizaciones de software que se crean y envían al punto de administración.|Cliente|  
|SUPSetup.log|Registra detalles acerca de la instalación de un punto de actualización de software. Cuando se completa la instalación del punto de actualización de software, **Installation was successful** se escribe en este archivo de registro.|Servidor de sistema de sitio|  
|UpdatesDeployment.log|Registra los detalles acerca de las implementaciones en el cliente, incluidas la activación, evaluación y aplicación de las actualizaciones de software. En el registro detallado se muestra información adicional acerca de la interacción con la interfaz de usuario del cliente.|Cliente|  
|Updateshandler.log|Registra información sobre el análisis de compatibilidad de actualizaciones de software y la descarga e instalación de actualizaciones de software en el cliente.|Cliente|  
|UpdatesStore.log|Registra los detalles acerca del estado de compatibilidad de las actualizaciones de software evaluadas durante el ciclo de análisis de compatibilidad.|Cliente|  
|WCM.log|Registra detalles sobre la configuración del punto de actualización de software y las conexiones con el servidor WSUS para las clasificaciones, idiomas y categorías de actualizaciones suscritas.|Servidor de sitio|  
|WSUSCtrl.log|Registra los detalles acerca de la configuración, la conectividad de base de datos y el estado del servidor WSUS para el sitio.|Servidor de sistema de sitio|  
|wsyncmgr.log|Registra detalles sobre el proceso de sincronización de actualizaciones de software.|Servidor de sitio|  
|WUAHandler.log|Registra detalles acerca del agente de Windows Update en el cliente cuando busca actualizaciones de software.|Cliente|  

###  <a name="BKMK_WULog"></a> Agente de Windows Update  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el agente de Windows Update.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Registra detalles sobre la conexión del agente de Windows Update con el servidor WSUS y recupera las actualizaciones de software para evaluar el cumplimiento y determinar si hay actualizaciones de los componentes del agente.|Cliente|  

###  <a name="BKMK_WSUSLog"></a> Servidor WSUS  
 En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el servidor WSUS.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|Change.log|Registra detalles sobre la información de base de datos del servidor WSUS que ha cambiado.|Servidor WSUS|  
|SoftwareDistribution.log|Registra detalles sobre las actualizaciones de software que se sincronizan del origen de actualizaciones configurado a la base de datos del servidor de WSUS.|Servidor WSUS|  

