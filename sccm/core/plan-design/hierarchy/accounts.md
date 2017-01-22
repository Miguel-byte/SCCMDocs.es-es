---
title: Cuentas que se usan en Configuration Manager | Microsoft Docs
description: Identifique y administre los grupos y las cuentas de Windows en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: fe573ebce2868686dd3156f4a3661dc8b85bc948


---
# <a name="accounts-used-in-system-center-configuration-manager"></a>Cuentas que se usan en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use la información siguiente para identificar las cuentas y los grupos de Windows que se usan en System Center Configuration Manager, cómo se usan y cualquier requisito aplicable.  

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a>Grupos de Windows que crea y utiliza Configuration Manager  
 Configuration Manager crea automáticamente y, en muchos casos, mantiene automáticamente los siguientes grupos de Windows:  

> [!NOTE]  
>  Cuando Configuration Manager crea un grupo en un equipo que es miembro del dominio, el grupo es un grupo de seguridad local. Si el equipo es un controlador de dominio, el grupo es un grupo local de dominio que se comparte entre todos los controladores de dominio en el dominio.  


### <a name="configmgrcollectedfilesaccess"></a>ConfigMgr_CollectedFilesAccess  
Configuration Manager usa este grupo para conceder acceso para ver los archivos recopilados por el inventario de software.  

En la tabla siguiente se enumeran detalles adicionales para este grupo:  

|Detalle|Más información|  
|------------|----------------------|  
|Tipo y ubicación|Este grupo es un grupo de seguridad local creado en el servidor de sitio primario.<br /><br /> Cuando se desinstala un sitio, este grupo no se quita automáticamente y se debe eliminar manualmente.|  
|Pertenencia|Configuration Manager administra automáticamente la pertenencia al grupo. Entre los miembros se incluyen usuarios administrativos que tienen concedido el permiso **Ver archivos recopilados** en el objeto asegurable **Recopilación** desde un rol de seguridad asignado.|  
|Permisos|De forma predeterminada, este grupo tiene el permiso **Read** en la siguiente carpeta en el servidor de sitio: **%path%\Microsoft Configuration Manager\sinv.box\FileCol**.|  

### <a name="configmgrdviewaccess"></a>ConfigMgr_DViewAccess  
 Este grupo es un grupo de seguridad local creado por Configuration Manager en el servidor de base de datos del sitio o en el servidor de réplica de base de datos y no se usa actualmente. Este grupo está reservado para su uso futuro por parte de Configuration Manager.  

### <a name="configmgr-remote-control-users"></a>Usuarios del control remoto de ConfigMgr  
 Las herramientas remotas de Configuration Manager usan este grupo para almacenar las cuentas y los grupos que configure en la lista de visores permitidos asignados a cada cliente.  

 En la tabla siguiente se enumeran detalles adicionales para este grupo:  

|Detalle|Más información|  
|------------|----------------------|  
|Tipo y ubicación|Este grupo es un grupo de seguridad local creado en el cliente de Configuration Manager cuando el cliente recibe la directiva que habilita las herramientas remotas.<br /><br /> Después de deshabilitar herramientas remotas para un cliente, este grupo no se quita automáticamente y debe eliminarse de forma manual desde cada equipo cliente.|  
|Pertenencia|De forma predeterminada, no hay ningún miembro en este grupo. Al agregar usuarios a la lista de visores permitidos, se agregan automáticamente a este grupo.<br /><br /> Puede utilizar la lista de visores permitidos para administrar la pertenencia a este grupo en lugar de agregar usuarios o grupos directamente.<br /><br /> Además de ser un visor permitido, un usuario administrativo debe tener el permiso de **Control remoto** en el objeto **Recopilación** . Puede asignar este permiso mediante el rol de seguridad Operador de herramientas remotas.|  
|Permisos|De forma predeterminada, este grupo no tiene permisos en ninguna ubicación del equipo y solo se utiliza para albergar la lista de visores permitidos.|  

### <a name="sms-admins"></a>Administradores de SMS  
 Configuration Manager usa este grupo para conceder acceso al proveedor de SMS, a través de WMI. Se necesita acceso al proveedor de SMS para ver y modificar objetos en la consola de Configuration Manager.  

> [!NOTE]  
>  La configuración de administración basada en roles de un usuario administrativo determina qué objetos puede ver y administrar cuando usa la consola de Configuration Manager.  

 En la tabla siguiente se enumeran detalles adicionales para este grupo:  

|Detalle|Más información|  
|------------|----------------------|  
|Tipo y ubicación|Este grupo es un grupo de seguridad local creado en cada equipo que tenga un proveedor de SMS.<br /><br /> Cuando se desinstala un sitio, este grupo no se quita automáticamente y se debe eliminar manualmente.|  
|Pertenencia|Configuration Manager administra automáticamente la pertenencia al grupo. De forma predeterminada, cada usuario administrativo en una jerarquía y la cuenta de equipo del servidor de sitio son miembros del grupo de administradores de SMS en cada equipo de proveedor de SMS en un sitio.|  
|Permisos|Los permisos y derechos de administradores de SMS se establecen en el complemento MMC Control WMI. De forma predeterminada, se concede **Enable Account** y **Remote Enable** al grupo de administradores de SMS en el espacio de nombres Root\SMS. Los usuarios autenticados tienen los permisos **Execute Methods**, **Provider Write**y **Enable Account**.<br /><br /> Los usuarios administrativos que van a usar una consola de Configuration Manager remota necesitan permisos de DCOM de activación remota en el equipo de servidor de sitio y en el equipo de proveedor de SMS. Es recomendable conceder estos derechos a los administradores de SMS para simplificar la administración, en lugar de conceder estos derechos directamente a los usuarios o grupos. Para obtener más información, consulte la sección [Configure DCOM permissions for remote Configuration Manager consoles](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) del tema [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) .|  

### <a name="smssitesystemtositeserverconnectionmpltsitecode"></a>SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>  
 Los puntos de administración de Configuration Manager que son remotos con respecto al servidor de sitio usan este grupo para conectarse a la base de datos del sitio. Este grupo proporciona un acceso de punto de administración a las carpetas de bandeja de entrada en el servidor de sitio y la base de datos del sitio.  

 En la tabla siguiente se enumeran detalles adicionales para este grupo:  

|Detalle|Más información|  
|------------|----------------------|  
|Tipo y ubicación|Este grupo es un grupo de seguridad local creado en cada equipo que tenga un proveedor de SMS.<br /><br /> Cuando se desinstala un sitio, este grupo no se quita automáticamente y se debe eliminar manualmente.|  
|Pertenencia|Configuration Manager administra automáticamente la pertenencia al grupo. De forma predeterminada, la pertenencia incluye las cuentas de equipo de equipos remotos que tienen un punto de administración para el sitio.|  
|Permisos|De forma predeterminada, este grupo tiene los permisos **Leer**, **Leer y ejecutar** y **Mostrar el contenido de la carpeta** para la carpeta **%ruta%\Microsoft Configuration Manager\inboxes** en el servidor de sitio. Además, este grupo tiene el permiso adicional de **Write** en varias subcarpetas por debajo de **inboxes** en donde el punto de administración escribe datos de cliente.|  

### <a name="smssitesystemtositeserverconnectionsmsprovltsitecode"></a>SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>  
 Los equipos del proveedor de SMS de Configuration Manager que son remotos con respecto al servidor de sitio usan este grupo para conectarse al servidor de sitio.  

 En la tabla siguiente se enumeran detalles adicionales para este grupo:  

|Detalle|Más información|  
|------------|----------------------|  
|Tipo y ubicación|Este grupo es un grupo de seguridad local creado en el servidor de sitio.<br /><br /> Cuando se desinstala un sitio, este grupo no se quita automáticamente y se debe eliminar manualmente.|  
|Pertenencia|Configuration Manager administra automáticamente la pertenencia al grupo. De forma predeterminada, la pertenencia incluye la cuenta de equipo o la cuenta de usuario de dominio que se utiliza para conectar al servidor de sitio desde cada equipo remoto que tenga instalado un proveedor de SMS para el sitio.|  
|Permisos|De forma predeterminada, este grupo tiene los permisos **Leer**, **Leer y ejecutar** y **Mostrar el contenido de la carpeta** para la carpeta **%ruta%\Microsoft Configuration Manager\inboxes** en el servidor de sitio. Además, este grupo tiene el permiso adicional de **Write** o los permisos **Write** y **Modify** en varias subcarpetas por debajo de **inboxes** en donde el proveedor de SMS requiere acceso.<br /><br /> Este grupo también tiene los permisos **Leer**, **Leer y ejecutar**, **Mostrar el contenido de la carpeta**, **Escribir** y **Modificar** para las carpetas por debajo de **%ruta%\Microsoft Configuration Manager\OSD\boot** y permiso **Leer** para las carpetas por debajo de **%ruta%\Microsoft Configuration Manager\OSD\Bin** en el servidor de sitio.|  

### <a name="smssitesystemtositeserverconnectionstatltsitecode"></a>SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>  
 El Administrador de distribuciones de archivos en equipos de sistema de sitio remoto de Configuration Manager usa este grupo para conectarse al servidor de sitio.  

 En la tabla siguiente se enumeran detalles adicionales para este grupo:  

|Detalle|Más información|  
|------------|----------------------|  
|Tipo y ubicación|Este grupo es un grupo de seguridad local creado en el servidor de sitio.<br /><br /> Cuando se desinstala un sitio, este grupo no se quita automáticamente y se debe eliminar manualmente.|  
|Pertenencia|Configuration Manager administra automáticamente la pertenencia al grupo. De forma predeterminada, la pertenencia incluye la cuenta de equipo o la cuenta de usuario de dominio que se utiliza para conectar al servidor de sitio desde cada equipo de sistema de sitio remoto que ejecute el Administrador de distribución de archivos.|  
|Permisos|De forma predeterminada, este grupo tiene los permisos **Leer**, **Leer y ejecutar** y **Mostrar el contenido de la carpeta** para la carpeta **%ruta%\Microsoft Configuration Manager\inboxes** y varias subcarpetas por debajo de esa ubicación en el servidor de sitio. Además, este grupo tiene los permisos adicionales de **Write** y **Modify** en la carpeta **%path%\Microsoft Configuration Manager\inboxes\statmgr.box** en el servidor de sitio.|  

### <a name="smssitetositeconnectionltsitecode"></a>SMS_SiteToSiteConnection_&lt;sitecode\>  
 Configuration Manager usa este grupo para habilitar la replicación basada en archivos entre sitios de una jerarquía. Por cada sitio remoto que transfiere los archivos directamente a este sitio, este grupo contiene cuentas configuradas como una **Cuenta de replicación de archivos**.  

 En la tabla siguiente se enumeran detalles adicionales para este grupo:  

|Detalle|Más información|  
|------------|----------------------|  
|Tipo y ubicación|Este grupo es un grupo de seguridad local creado en el servidor de sitio.|  
|Pertenencia|Cuando instala un nuevo sitio como secundario de otro sitio, Configuration Manager agrega automáticamente la cuenta de equipo del nuevo sitio al grupo en el servidor de sitio primario y la cuenta de equipo de sitios primarios al grupo en el nuevo servidor de sitio. Si especifica otra cuenta para las transferencias basadas en archivos, agregue dicha cuenta a este grupo en el servidor de sitio de destino.<br /><br /> Cuando se desinstala un sitio, este grupo no se quita automáticamente y se debe eliminar manualmente.|  
|Permisos|De forma predeterminada, este grupo tiene **control total** en la carpeta **%path%\Microsoft Configuration Manager\inboxes\despoolr.box\receive** .|  

## <a name="accounts-that-configuration-manager-uses"></a>Cuentas que utiliza Configuration Manager  
 Puede configurar las cuentas siguientes para Configuration Manager:  

### <a name="active-directory-group-discovery-account"></a>Cuenta de detección de grupos de Active Directory  
 La **Cuenta de detección de grupos de Active Directory** se usa para detectar grupos de seguridad locales, globales y universales, la pertenencia a estos grupos y la pertenencia a grupos de distribución desde las ubicaciones especificadas en Servicios de dominio de Active Directory. Los grupos de distribución no se detectan como recursos de grupo.  

 Esta cuenta puede ser una cuenta de equipo del servidor de sitio que ejecute la detección o una cuenta de usuario de Windows. Debe tener permiso de acceso de **lectura** en las ubicaciones de Active Directory que se especifiquen para la detección.  

### <a name="active-directory-system-discovery-account"></a>Cuenta de detección de sistemas de Active Directory  
 La **Cuenta de detección de sistemas de Active Directory** se usa para detectar equipos desde las ubicaciones especificadas en Servicios de dominio de Active Directory.  

 Esta cuenta puede ser una cuenta de equipo del servidor de sitio que ejecute la detección o una cuenta de usuario de Windows. Debe tener permiso de acceso de **lectura** en las ubicaciones de Active Directory que se especifiquen para la detección.  

### <a name="active-directory-user-discovery-account"></a>Cuenta de detección de usuarios de Active Directory  
 La **Cuenta de detección de usuarios de Active Directory** se usa para detectar cuentas de usuario desde las ubicaciones especificadas en Servicios de dominio de Active Directory.  

 Esta cuenta puede ser una cuenta de equipo del servidor de sitio que ejecute la detección o una cuenta de usuario de Windows. Debe tener permiso de acceso de **lectura** en las ubicaciones de Active Directory que se especifiquen para la detección.  

### <a name="active-directory-forest-account"></a>Cuenta de bosque de Active Directory  
 La **Cuenta de bosque de Active Directory** se usa para detectar infraestructura de red desde bosques de Active Directory. También la usan sitios de administración central y sitios primarios para publicar datos del sitio en los Servicios de dominio de Active Directory de un bosque.  

> [!NOTE]  
>  Los sitios secundarios siempre utilizan la cuenta de equipo del servidor de sitio secundario para publicar en Active Directory.  

> [!NOTE]  
>  La Cuenta de bosque de Active Directory debe ser una cuenta global para detectar y publicar en bosques que no son de confianza. Si no utiliza la cuenta de equipo del servidor de sitio, solo se puede seleccionar una cuenta global.  

 Esta cuenta debe tener permisos de **lectura** en cada bosque de Active Directory donde desee detectar infraestructura de red.  

 Esta cuenta debe tener permisos de **control total** en el contenedor System Management y todos sus objetos secundarios en cada bosque de Active Directory donde desee publicar datos del sitio.  

### <a name="asset-intelligence-synchronization-point-proxy-server-account"></a>Cuenta de servidor proxy de punto de sincronización de Asset Intelligence  
 El punto de sincronización de Asset Intelligence usa la **Cuenta de servidor proxy de punto de sincronización de Asset Intelligence** para acceder a Internet a través de un servidor proxy o firewall que requiera acceso autenticado.  

> [!IMPORTANT]  
>  Especifique una cuenta que tenga los mínimos permisos posibles en el servidor proxy o firewall correspondiente.  

### <a name="certificate-registration-point-account"></a>Cuenta de punto de registro de certificado  
 La **cuenta del punto de registro de certificados** conecta dicho punto de registro de certificados con la base de datos de Configuration Manager. De forma predeterminada, se utiliza la cuenta de equipo del punto de registro del certificado, pero puede configurar una cuenta de usuario en su lugar. Debe especificar una cuenta de usuario cada vez que el punto de registro del certificado esté en un dominio que no sea de confianza en el servidor del sitio. Esta cuenta solo requiere acceso de lectura a la base de datos del sitio, ya que las operaciones de escritura se controlan mediante el sistema de mensajes de estado.  

### <a name="capture-operating-system-image-account"></a>Cuenta de captura de imagen de sistema operativo  
 Configuration Manager usa la **cuenta de captura de imagen de sistema operativo** para acceder a la carpeta en la que se almacenan las imágenes capturadas cuando se implementan sistemas operativos. Esta cuenta es necesaria si agrega el paso **Capturar imagen de sistema operativo** a una secuencia de tareas.  

 La cuenta debe tener permisos de **Lectura** y **Escritura** en el recurso compartido de red donde se almacena la imagen capturada.  

 Si se cambia la contraseña de la cuenta en Windows, debe actualizar la secuencia de tareas con la nueva contraseña. El cliente de Configuration Manager recibirá la nueva contraseña la siguiente vez que descargue la directiva de cliente.  

 Si utiliza esta cuenta, puede crear una cuenta de usuario de dominio con unos permisos mínimos para el acceso a los recursos de red requeridos, y usarla para todas las cuentas de la secuencia de tareas.  

> [!IMPORTANT]  
>  No asigne a esta cuenta permisos de inicio de sesión interactivo.  
>   
>  No utilice la cuenta de acceso de red para esta cuenta.  

### <a name="client-push-installation-account"></a>Cuenta de instalación de inserción de cliente  
 La **cuenta de instalación de inserción de cliente** se usa para conectarse a equipos e instalar el software de cliente de Configuration Manager si implementa clientes mediante la instalación de inserción de cliente. Si no se especifica esta cuenta, se utiliza la cuenta del servidor del sitio para intentar instalar el software de cliente.  

 Esta cuenta debe ser miembro del grupo **Administradores** local en los equipos en los que se va a instalar el software de cliente de Configuration Manager. Esta cuenta no requiere derechos de administrador de dominio.  

 Puede especificar una o más cuentas de instalación de inserción de cliente que Configuration Manager prueba por turnos hasta que se establece la conexión.  

> [!TIP]  
>  Para coordinar de un modo más eficaz las actualizaciones de cuentas en las implementaciones de Active Directory grandes, cree una nueva cuenta con un nombre distinto y agréguela a la lista de cuentas de instalación de inserción de cliente en Configuration Manager. Deje el tiempo necesario para que Active Directory Domain Services pueda replicar la nueva cuenta y luego elimine la cuenta anterior de Configuration Manager y de Active Directory Domain Services.  

> [!IMPORTANT]  
>  No conceda a esta cuenta derechos para iniciar sesión localmente.  

### <a name="enrollment-point-connection-account"></a>Cuenta de conexión de punto de inscripción  
 La **cuenta de conexión de punto de inscripción** conecta el punto de inscripción a la base de datos de sitio de Configuration Manager. De forma predeterminada, se utiliza la cuenta de equipo del punto de inscripción, pero puede configurar una cuenta de usuario en su lugar. Debe especificar una cuenta de usuario cada vez que el punto de inscripción esté en un dominio que no sea de confianza en el servidor del sitio. Esta cuenta requiere acceso de lectura y escritura a la base de datos del sitio.  

### <a name="exchange-server-connection-account"></a>Cuenta de conexión de Exchange Server  
 La **Cuenta de conexión de Exchange Server** conecta el servidor de sitio con el equipo de Exchange Server especificado para buscar y administrar los dispositivos móviles que se conectan a Exchange Server. Esta cuenta requiere los cmdlets de PowerShell de Exchange que proporcionan los permisos necesarios para el equipo de Exchange Server. Para más información sobre esta solución, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="exchange-server-connector-proxy-server-account"></a>Cuenta de servidor proxy del conector de Exchange Server  
 El conector de Exchange Server usa la **Cuenta de servidor proxy del conector de Exchange Server** para acceder a Internet a través de un servidor proxy o firewall que requiera acceso autenticado.  

> [!IMPORTANT]  
>  Especifique una cuenta que tenga los mínimos permisos posibles en el servidor proxy o firewall correspondiente.  

### <a name="management-point-connection-account"></a>Cuenta de conexión del punto de administración  
 La **cuenta de conexión del punto de administración** se usa para conectar el punto de administración a la base de datos de sitio de Configuration Manager de modo que pueda enviar y recuperar información para clientes. De forma predeterminada, se utiliza la cuenta de equipo del punto de administración pero puede configurar una cuenta de usuario en su lugar. Debe especificar una cuenta de usuario cada vez que el punto de administración esté en un dominio que no sea de confianza en el servidor del sitio.  

 Cree la cuenta como una cuenta local con derechos reducidos en el equipo que ejecuta Microsoft SQL Server.  

> [!IMPORTANT]  
>  No conceda a esta cuenta derechos de inicio de sesión interactivo.  

### <a name="multicast-connection-account"></a>Cuenta de conexión de multidifusión  
 Los puntos de distribución, que están configurados para multidifusión, usan la **Cuenta de conexión de multidifusión** para leer información de la base de datos del sitio. De forma predeterminada, se utiliza la cuenta de equipo del punto de distribución pero puede configurar una cuenta de usuario en su lugar. Debe especificar una cuenta de usuario cada vez que la base de datos del sitio esté en un bosque que no sea de confianza. Por ejemplo, si el centro de datos tiene una red perimetral en un bosque que no sea ni el servidor del sitio ni la base de datos del sitio, puede utilizar esta cuenta para leer información de multidifusión desde la base de datos del sitio.  

 Si crea esta cuenta, créela como una cuenta local con derechos reducidos en el equipo que ejecuta Microsoft SQL Server.  

> [!IMPORTANT]  
>  No conceda a esta cuenta derechos de inicio de sesión interactivo.  

### <a name="network-access-account"></a>Cuenta de acceso a la red  
 Los equipos cliente usan la **Cuenta de acceso a la red** cuando no pueden usar su cuenta de equipo local para acceder a contenido en los puntos de distribución. Por ejemplo, esto se aplica a los equipos y clientes del grupo de trabajo de dominios que no son de confianza. Esta cuenta también se puede utilizar durante la implementación de un sistema operativo cuando el equipo que instala el sistema operativo no tiene aún una cuenta de equipo en el dominio.  

> [!NOTE]  
>  La cuenta de acceso a la red nunca se utiliza como contexto de seguridad para ejecutar programas, instalar actualizaciones de software ni ejecutar secuencias de tareas, sino únicamente para tener acceso a recursos de la red.  

 Conceda a esta cuenta los permisos adecuados mínimos en el contenido que el cliente necesita para tener acceso al software. La cuenta debe tener el derecho **Tener acceso a este equipo desde la red** en el punto de distribución u otro servidor que hospeda el contenido del paquete.  Puede configurar hasta 10 cuentas de acceso a la red por cada sitio.  

> [!WARNING]  
>  Cuando Configuration Manager intenta usar la cuenta nombreDeEquipo$ para descargar el contenido y se produce un error, lo intenta de nuevo automáticamente con la cuenta de acceso a la red, incluso si ya lo intentó antes y se produjo un error.  

 Cree la cuenta en cualquier dominio que proporcione el acceso necesario a los recursos. La cuenta de acceso de red debe incluir siempre un nombre de dominio. No se admite la seguridad de paso a través para esta cuenta. Si tiene puntos de distribución en varios dominios, cree la cuenta en un dominio de confianza.  

> [!TIP]  
>  Para evitar bloqueos de cuentas, no cambie la contraseña de una cuenta de acceso de red existente. En su lugar, cree una cuenta nueva y configúrela en Configuration Manager. Cuando transcurra el tiempo suficiente para que todos los clientes reciban los detalles de la cuenta nueva, quite la cuenta antigua de las carpetas compartidas de red y elimine la cuenta.  

> [!IMPORTANT]  
>  No conceda a esta cuenta derechos de inicio de sesión interactivo.  
>   
>  No conceda a esta cuenta el derecho de unir equipos al dominio. Si debe unir equipos al dominio durante una secuencia de tareas, utilice la cuenta de unión al dominio del editor de secuencia de tareas.  

### <a name="package-access-account"></a>Cuenta de acceso de paquetes  
 La **Cuenta de acceso de paquetes** permite establecer permisos NTFS para especificar los usuarios y grupos de usuarios que pueden acceder a una carpeta de paquetes en los puntos de distribución. De forma predeterminada, Configuration Manager solo concede acceso a las cuentas genéricas **Usuarios** y **Administradores**, aunque puede controlar el acceso de los equipos cliente mediante el empleo de otras cuentas o grupos de Windows. Los dispositivos móviles siempre recuperan contenido de paquete de forma anónima, por lo que estos dispositivos no utilizan cuentas de acceso de paquetes.  

 De forma predeterminada, cuando Configuration Manager crea el recurso compartido de paquete en un punto de distribución, concede acceso **Leer** al grupo **Usuarios** local y **Control total** al grupo **Administradores** local. Los permisos reales necesarios dependen del paquete. Si tiene clientes en grupos de trabajo o en bosques que no son de confianza, estos clientes utilizan la cuenta de acceso de red para acceder al contenido del paquete. Asegúrese de que la cuenta de acceso a la red tenga permisos para el paquete, y utilice las cuentas de acceso de paquetes definidas.  

 Utilice las cuentas en un dominio que pueda acceder a los puntos de distribución. Si crea o modifica la cuenta después de que se cree el paquete, deberá redistribuirlo. La actualización del paquete no cambia los permisos NTFS del paquete.  

 No es necesario que agregue la cuenta de acceso a la red como una cuenta de acceso de paquetes, porque la pertenencia al grupo Usuarios la agrega automáticamente. Restringir la cuenta de acceso de paquetes a solo la cuenta de acceso a la red no impide que los clientes accedan al paquete.  

### <a name="reporting-services-point-account"></a>Cuenta de punto de Reporting Services  
 SQL Server Reporting Services usa la **cuenta de punto de servicios de informes** para recuperar los datos de informes de Configuration Manager de la base de datos del sitio. La cuenta de usuario y la contraseña de Windows especificadas se cifran y almacenan en la base de datos de SQL Server Reporting Services.  

### <a name="remote-tools-permitted-viewer-accounts"></a>Cuentas de visores permitidos de herramientas remotas  
 Las cuentas que especifique como **Visores permitidos** para el control remoto son una lista de usuarios a los que se permite el uso de funcionalidades de herramientas remotas en los clientes.  

### <a name="site-system-installation-account"></a>Cuenta de instalación del sistema de sitio  
 El servidor de sitio usa la **Cuenta de instalación del sistema de sitio** para instalar, reinstalar, desinstalar y configurar sistemas de sitio. Si configura el sistema de sitio de modo que exija al servidor de sitio iniciar conexiones con dicho sistema de sitio, Configuration Manager también usa esta cuenta para extraer datos del equipo de sistema de sitio después de la instalación del sistema de sitio y los roles de sistema de sitio. Cada sistema de sitio puede tener una cuenta de instalación del sistema de sitio distinta, pero solo se puede configurar una cuenta de instalación del sistema de sitio para administrar los roles de sistema de sitio en el sistema de sitio.  

 Esta cuenta requiere permisos administrativos locales en los sistemas de sitio que se van a instalar y configurar. Además, esta cuenta debe **Tener acceso a este equipo desde la red** en la directiva de seguridad en los sistemas de sitio que se van a instalar y configurar.  

> [!TIP]  
>  Si tiene muchos controladores de dominio y estas cuentas se utilizarán en varios dominios, compruebe que las cuentas se han replicado antes de configurar el sistema de sitio.  
>   
>  La especificación de una cuenta local en cada sistema de sitio que se va a administrar es una configuración más segura que la utilización de cuentas de dominio, ya que se limitan los daños que los atacantes pueden producir si la seguridad de la cuenta se ve comprometida. Sin embargo, las cuentas de dominio son más fáciles de administrar: tenga en cuenta que debe conseguir un equilibrio entre la seguridad y una administración eficaz.  

### <a name="smtp-server-connection-account"></a>Cuenta de conexión del servidor SMTP  
 El servidor de sitio usa la **Cuenta de conexión del servidor SMTP** para enviar alertas por correo electrónico cuando el servidor SMTP requiera acceso autenticado.  

> [!IMPORTANT]  
>  Especifique una cuenta que tenga los mínimos permisos posibles para enviar mensajes de correo electrónico.  

### <a name="software-update-point-connection-account"></a>Cuenta de conexión de punto de actualización de software  
 El servidor de sitio usa la **Cuenta de conexión de punto de actualización de software** para los dos servicios de actualizaciones de software siguientes:  

-   Configuration Manager de WSUS, que configura opciones como las definiciones de producto, las clasificaciones y la configuración ascendente.  

-   Administrador de sincronización de WSUS, que solicita la sincronización a un servidor WSUS ascendente o a Microsoft Update.  

La cuenta de instalación del sistema de sitio puede instalar componentes para las actualizaciones de software, pero no puede realizar funciones específicas de actualizaciones de software en el punto de actualización de software. Si no puede usar la cuenta de equipo del servidor de sitio para esta funcionalidad porque el punto de actualización de software está en un bosque que no es de confianza, debe especificar esta cuenta además de la cuenta de instalación del sistema de sitio.  

Esta cuenta debe ser un administrador local en el equipo en el que está instalado WSUS y formar parte del grupo local Administradores de WSUS.  

### <a name="software-update-point-proxy-server-account"></a>Cuenta del servidor proxy del punto de actualización de software  
 El punto de actualización de software usa la **Cuenta del servidor proxy del punto de actualización de software** para acceder a Internet a través de un servidor proxy o firewall que requiera acceso autenticado.  

> [!IMPORTANT]  
>  Especifique una cuenta que tenga los mínimos permisos posibles en el servidor proxy o firewall correspondiente.  

### <a name="source-site-account"></a>Cuenta de sitio de origen  
 El proceso de migración usa la **Cuenta de sitio de origen** para acceder al proveedor de SMS del sitio de origen. Esta cuenta requiere permisos de **Leer** en objetos de sitio en el sitio de origen para obtener datos de trabajos de migración.  

 Si actualiza sitios secundarios o puntos de distribución de Configuration Manager 2007 que tienen puntos de distribución que comparten ubicación con puntos de distribución de System Center Configuration Manager, la cuenta también tiene que tener permisos **Eliminar** en la clase **Sitio** para eliminar correctamente el punto de distribución del sitio de Configuration Manager 2007 durante la actualización.  

> [!NOTE]  
>  La cuenta de sitio de origen y la cuenta de base de datos del sitio de origen se identifican como **Administrador de migraciones** en el nodo **Cuentas** del área de trabajo **Administración** en la consola de Configuration Manager.  

### <a name="source-site-database-account"></a>Cuenta de base de datos del sitio de origen  
 El proceso de migración usa la **Cuenta de base de datos del sitio de origen** para acceder a la base de datos de SQL Server del sitio de origen. Para obtener datos de la base de datos de SQL Server del sitio de origen, la cuenta de base de datos del sitio de origen debe tener los permisos **Leer** y **Ejecutar** en la base de datos de SQL Server del sitio de origen.  

> [!NOTE]  
>  Si usa la cuenta de equipo de System Center Configuration Manager, asegúrese de que se cumpla lo siguiente para esta cuenta:  
>   
>  -   Es un miembro del grupo de seguridad **Usuarios COM distribuidos** en el dominio en el que reside el sitio de Configuration Manager 2007.  
> -   Es un miembro del grupo de seguridad **Administradores de SMS** .  
> -   Tiene el permiso **Leer** para todos los objetos de Configuration Manager 2007.  

> [!NOTE]  
>  La cuenta de sitio de origen y la cuenta de base de datos del sitio de origen se identifican como **Administrador de migraciones** en el nodo **Cuentas** del área de trabajo **Administración** en la consola de Configuration Manager.  

### <a name="task-sequence-editor-domain-joining-account"></a>Cuenta de unión de dominio de editor de secuencia de tareas  
 La **Cuenta de unión de dominio de editor de secuencia de tareas** se usa en una secuencia de tareas para unir un equipo creado recientemente con una imagen a un dominio. La cuenta se necesita si agrega el paso **Unirse a dominio o grupo de trabajo** a una secuencia de tareas y, a continuación, selecciona **Unirse a un dominio**. También se puede configurar esta cuenta si agrega el paso **Aplicar configuración de red** a una secuencia de tareas, pero no es obligatorio.  

 Esta cuenta requiere el derecho **Unirse al dominio** en el dominio al que el equipo se va a unir.  

> [!TIP]  
>  Si requiere esta cuenta para su secuencia de tareas, puede crear una cuenta de usuario de dominio con los permisos mínimos para acceder a los recursos de red requeridos y usarla para todas las cuentas de secuencia de tareas.  

> [!IMPORTANT]  
>  No asigne a esta cuenta permisos de inicio de sesión interactivo.  
>   
>  No utilice la cuenta de acceso de red para esta cuenta.  

### <a name="task-sequence-editor-network-folder-connection-account"></a>Cuenta de conexión de carpeta de red de editor de secuencias de tareas  
 Una secuencia de tareas usa la **Cuenta de conexión de carpeta de red de editor de secuencias de tareas** para conectarse a una carpeta compartida en la red. Esta cuenta es necesaria si agrega el paso **Conectar a carpeta de red** a una secuencia de tareas.  

 Esta cuenta requiere permisos de acceso a la carpeta compartida especificada y debe ser una cuenta de dominio de usuario.  

> [!TIP]  
>  Si requiere esta cuenta para su secuencia de tareas, puede crear una cuenta de usuario de dominio con los permisos mínimos para acceder a los recursos de red requeridos y usarla para todas las cuentas de secuencia de tareas.  

> [!IMPORTANT]  
>  No asigne a esta cuenta permisos de inicio de sesión interactivo.  
>   
>  No utilice la cuenta de acceso de red para esta cuenta.  

### <a name="task-sequence-run-as-account"></a>Cuenta de ejecución de secuencia de tareas  
 La **Cuenta de ejecución de secuencia de tareas** se usa para ejecutar líneas de comandos en secuencias de tareas y emplear credenciales distintas a las de la cuenta de sistema local. Esta cuenta es necesaria si desea agregar el paso **Ejecutar línea de comandos** a una secuencia de tareas pero no quiere que la secuencia de tareas se ejecute con permisos de cuenta de sistema local en el equipo administrado.  

 Configure la cuenta para que tenga los permisos mínimos necesarios para ejecutar la línea de comandos especificada en la secuencia de tareas. La cuenta requiere permisos de inicio de sesión interactivo y normalmente requiere la capacidad de instalar software y tener acceso a recursos de red.  

> [!IMPORTANT]  
>  No utilice la cuenta de acceso de red para esta cuenta.  
>   
>  Nunca convierta la cuenta en administrador de dominio.  
>   
>  No configure nunca perfiles móviles para esta cuenta. Cuando se ejecuta la secuencia de tareas, descargará el perfil móvil de la cuenta y se podrá acceder al perfil en el equipo local.  
>   
>  Limite el ámbito de la cuenta. Por ejemplo, cree varias cuentas de ejecución de secuencia de tareas para cada secuencia de tareas de manera que si una cuenta se ve comprometida, solo se exponen los equipos cliente a los que la cuenta tiene acceso.  
>   
>  Si la línea de comandos requiere acceso administrativo en el equipo, considere la posibilidad de crear una cuenta de administrador local solo para la cuenta de ejecución de secuencia de tareas en todos los equipos que ejecutarán la secuencia de tareas y elimine la cuenta cuando ya no sea necesaria.  



<!--HONumber=Dec16_HO3-->


