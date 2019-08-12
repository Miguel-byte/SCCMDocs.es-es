---
title: Transferencias de datos
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo Configuration Manager mueve datos entre sitios y cómo se puede administrar la transferencia de datos a través de la red.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cf2890f44bcb6e8e7813581de300e4544202f6ce
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536237"
---
# <a name="data-transfers-between-sites-in-configuration-manager"></a>Transferencias de datos entre sitios en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager usa la *replicación basada en archivos* y la *replicación de base de datos* para transferir distintos tipos de información entre sitios. Obtenga información sobre cómo Configuration Manager mueve datos entre sitios y cómo se puede administrar la transferencia de datos a través de la red.  


## <a name="bkmk_fileroute"></a> File-based replication

Configuration Manager usa la replicación basada en archivos para transferir datos basados en archivos entre sitios de la jerarquía. Estos datos incluyen las aplicaciones y los paquetes que quiere implementar en puntos de distribución de sitios secundarios. También incluye los registros de datos de detección no procesados que se transfieren a los sitios primarios y que posteriormente se procesan.  

La comunicación entre sitios basada en archivos usa el protocolo *Bloque de mensajes del servidor** (SMB) en el puerto TCP/IP 445. Para controlar la cantidad de datos transferidos a través de la red, especifique el límite de ancho de banda y el modo por pulsos. También puede usar programaciones para controlar cuándo enviar los datos a través de la red.  

### <a name="bkmk_routes"></a> Rutas de replicación de archivos

La información siguiente puede ayudar a configurar y usar las rutas de replicación de archivos.  

#### <a name="file-replication-route"></a>Ruta de replicación de archivos

Cada ruta de replicación de archivos identifica un sitio de destino al que se pueden transferir los datos basados en archivos. Cada sitio admite una ruta de replicación de archivos a un sitio de destino específico.  

Para administrar una ruta de replicación de archivos, en el área de trabajo **Administración**, expanda **Configuración de jerarquía** y, luego, seleccione el nodo **Replicación de archivos**.  

Puede cambiar los siguientes valores para rutas de replicación de archivos:  

##### <a name="file-replication-account"></a>Cuenta de replicación de archivos

Esta cuenta se conecta al sitio de destino y escribe datos en el recurso compartido **SMS_Site** del sitio. El sitio de destino procesa los datos escritos en este recurso compartido. De manera predeterminada, cuando agrega un sitio a la jerarquía, Configuration Manager asigna una cuenta de equipo del servidor de sitio nuevo como su cuenta de replicación de archivos. Luego agrega esta cuenta al grupo **SMS_SiteToSiteConnection_&lt;CódigoDeSitio\>** del sitio de destino. Este grupo es local en el equipo que concede acceso al recurso compartido SMS_Site. Puede cambiar esta cuenta para que sea una cuenta de usuario de Windows. Si cambia la cuenta, asegúrese de agregarla al grupo **SMS_SiteToSiteConnection_&lt;CódigoDeSitio\>** del sitio de destino.  

> [!NOTE]  
> Los sitios secundarios siempre utilizan la cuenta de equipo del servidor de sitio secundario como la **Cuenta de replicación de archivos**.  

##### <a name="schedule"></a>Programa

Para restringir el tipo de datos y la hora en que los datos se pueden transferir al sitio de destino, establezca la programación para cada ruta de replicación de archivos.

##### <a name="rate-limits"></a>Límites de frecuencia

Para controlar el ancho de banda de red que el sitio usa cuando transfiere datos al sitio de destino, especifique los límites de frecuencia para cada ruta de replicación de archivos:

- **Modo por pulsos**: especifique el tamaño de los bloques de datos que el sitio envía al sitio de destino. También puede especificar un retraso de tiempo entre el envío de cada bloque de datos. Use esta opción cuando tenga que enviar datos a través de una conexión de red con un ancho de banda bajo al sitio de destino.

    Por ejemplo, puede tener limitaciones para enviar 1 KB de datos cada cinco segundos y no 1 KB cada tres segundos, sin importar de la velocidad del vínculo o su uso en un momento dado.

- **Limitado al máximo de velocidades de transferencia por hora**: el sitio envía datos a un sitio de destino únicamente mediante el porcentaje de tiempo que especifica. Al usar esta opción, Configuration Manager no identifica el ancho de banda disponible de la red. En su lugar, divide el tiempo en que puede enviar datos en intervalos de tiempo. Después, envía datos durante un período de tiempo corto, seguido de bloques de tiempo durante los cuales no envía ningún dato.

    Por ejemplo, puede establecer la velocidad máxima en **50 %** . Configuration Manager transmite los datos durante un período de tiempo, seguido de un período de tiempo equivalente durante el cual no envía ningún dato. No administra la cantidad real de datos ni el tamaño del bloque de datos. Solo se administra la cantidad de tiempo durante el que se envían datos.  

    > [!CAUTION]  
    > De forma predeterminada, un sitio puede utilizar hasta tres **envíos simultáneos** para transferir datos a un sitio de destino. Cuando habilita los límites de frecuencia para una ruta de replicación de archivos, los **envíos simultáneos** a ese sitio se limitan a uno. Este comportamiento se aplica incluso cuando la opción **Limitar ancho de banda disponible (%)** se establece en **100 %** . Por ejemplo, si usa la configuración predeterminada para el remitente, esto reduce la velocidad de transferencia al sitio de destino para que sea un tercio de la capacidad predeterminada.  

##### <a name="secondary-sites"></a>Sitios secundarios

Puede configurar una ruta de replicación de archivos entre dos sitios secundarios para distribuir contenido basado en archivos entre dichos sitios.  


#### <a name="sender"></a>Remitente

Cada sitio tiene un remitente. El remitente administra la conexión de red desde un sitio a un sitio de destino y puede establecer conexiones a varios sitios al mismo tiempo. Para conectarse a un sitio, el remitente utiliza la ruta de replicación de archivos al sitio para identificar la cuenta que se va a utiliza para establecer la conexión de red. El remitente también usa esta cuenta para escribir datos en el recurso compartido SMS_Site del sitio de destino.  

De forma predeterminada, el remitente escribe datos en un sitio de destino mediante el uso de varios **envíos simultáneos**, lo que normalmente se conoce como un subproceso. Cada envío simultáneo, o subproceso, puede transferir un objeto basado en archivo diferente al sitio de destino. De forma predeterminada, cuando el remitente comienza a enviar un objeto, continúa escribiendo bloques de datos para ese objeto hasta que se envía todo el objeto. Una vez que se han enviado todos los datos para el objeto, un nuevo objeto puede empezar a enviar ese subproceso.  

Para limitar el remitente para un sitio, vaya al área de trabajo **Administración** y expanda el nodo **Configuración del sitio**. Seleccione el nodo **Sitios** y, luego, **Propiedades** para el sitio que quiere administrar. Haga clic en la pestaña **Remitente** para cambiar la configuración del remitente.  

Puede cambiar los siguientes valores para un remitente:  

##### <a name="maximum-concurrent-sendings"></a>Máximo de envíos simultáneos

De manera predeterminada, cada sitio usa cinco envíos simultáneos. Hay tres subprocesos disponibles para usarlos cuando se envían datos a cualquier sitio de destino. Si aumenta este número, podrá aumentar la transmisión de datos entre sitios dado que Configuration Manager puede transferir más archivos al mismo tiempo. Si se aumenta este número, también aumenta la demanda de ancho de banda de red entre sitios.  

##### <a name="retry-settings"></a>Configuración de reintento

De forma predeterminada, cada sitio reintenta dos veces una conexión con problemas, con un retraso de un minuto entre intentos de conexión. Puede modificar el número de intentos de conexión que realiza el sitio y el tiempo que hay que esperar entre ellos.  


## <a name="bkmk_dbrep"></a> Database replication

La replicación de base de datos de Configuration Manager usa SQL Server para transferir datos y combinar los cambios realizados en una base de datos de sitio con la información almacenada en la base de datos de otros sitios de la jerarquía.

En una jerarquía:

- Todos los sitios comparten la misma información.  
- Cuando instala un sitio en una jerarquía, Configuration Manager establece automáticamente la replicación de base de datos entre el sitio nuevo y su sitio primario.  
- Cuando finaliza la instalación del sitio, se inicia automáticamente la replicación de base de datos.  

Si se agrega un nuevo sitio a una jerarquía, Configuration Manager crea una base de datos genérica en el nuevo sitio. Después, el sitio primario crea una instantánea de los datos relevantes en su base de datos y transfiere esa instantánea al nuevo sitio mediante replicación basada en archivos. De este modo, el nuevo sitio usa un programa de copia masiva (BCP) de SQL Server para cargar la información en su copia local de la base de datos de Configuration Manager. Después de cargar la instantánea, cada sitio lleva a cabo la replicación de base de datos con el otro sitio.  

Para replicar datos entre sitios, Configuration Manager usa su propio servicio de replicación de base de datos. El servicio de replicación de base de datos usa el seguimiento de cambios de SQL Server para supervisar los cambios en la base de datos del sitio local. Luego, replica los cambios en los demás sitios mediante SQL Server Service Broker (SSB). De forma predeterminada, este proceso usa el puerto TCP/IP 4022.  

### <a name="replication-groups"></a>Grupos de replicación

Configuration Manager agrupa los datos replicados mediante la replicación de base de datos en grupos de replicación diferentes. Cada grupo de replicación tiene una programación de replicación independiente y fija. El sitio usa esta programación para determinar la frecuencia con que replica los cambios en otros sitios.  

Por ejemplo, un cambio en una configuración de administración basada en roles se replica rápidamente en otros sitios. Con este comportamiento se garantiza que otros sitios pueden aplicar rápidamente estos cambios. Un cambio de configuración de menor prioridad, como una solicitud para instalar un sitio secundario nuevo, se replica con menos urgencia. Una solicitud de nuevo sitio puede tardar varios minutos en llegar al sitio primario de destino.  

### <a name="settings-for-database-replication"></a>Configuración de la replicación de base de datos

Puede modificar la siguiente configuración para la replicación de base de datos:  

- **Vínculos de replicación de base de datos**: Controle cuándo el tráfico específico cruza la red.  

- **Vistas distribuidas**: cuando un sitio de administración central (CAS) solicita los datos del sitio seleccionados, puede acceder directamente a los datos desde la base de datos en un sitio primario secundario.  

- **Programaciones**: especifique cuándo se usa un vínculo de replicación y cuándo se replican distintos tipos de datos del sitio.  

- **Resumen**: resumen de la configuración de datos sobre el tráfico de red que cruza los vínculos de replicación. De forma predeterminada, el resumen se produce cada 15 minutos. Se usa en informes para la replicación de base de datos.  

- **Umbrales de replicación de base de datos**: defina cuándo Configuration Manager informa vínculos como degradados o erróneos. También puede configurar en qué momento genera alertas relativas a los vínculos de replicación que tienen un estado de degradado o erróneo.  

### <a name="types-of-data"></a>Tipos de datos

Configuration Manager clasifica principalmente los datos que replica como *datos globales* o *datos del sitio*. Cuando se produce la replicación de base de datos, el sitio transfiere los cambios en los datos globales y en los datos del sitio a través del vínculo de replicación de base de datos. Los datos globales se replican a un sitio primario o secundario. Los datos de sitio solo se replican en un sitio primario. Un tercer tipo de datos, los *datos locales*, no se replica a otros sitios. Los datos locales son información que los demás sitios no necesitan.

#### <a name="global-data"></a>Datos globales

Los datos globales son objetos creados por el administrador que se replican a todos los sitios de la jerarquía. Los sitios secundarios solo reciben un subconjunto de los datos globales, como los datos de proxy globales. Puede crear datos globales en el sitio CAS y el sitio primario. Este tipo incluye los datos siguientes:

- Implementaciones de software
- Actualizaciones de software
- Definiciones de colección
- Ámbitos de seguridad de administración basada en roles

#### <a name="site-data"></a>Datos del sitio

Los datos del sitio son información operativa creada por los sitios primarios de Configuration Manager y sus clientes asignados. Los datos del sitio se replican al sitio CAS, pero no a otros sitios primarios. Los datos del sitio solo son visibles en el sitio CAS y en el sitio primario donde se originan los datos. Solo puede modificar los datos del sitio en el sitio primario donde los creó. Este tipo incluye los datos siguientes:

- Inventario de hardware
- Mensajes de estado
- Alertas
- Los resultados de las colecciones basadas en consultas

Todos los datos del sitio se replican en el sitio CAS. El sitio CAS realiza la administración y la generación de informes para toda la jerarquía de sitios.  

### <a name="bkmk_Dblinks"></a> Vínculos de replicación de base de datos

Cuando se instala un nuevo sitio en una jerarquía, Configuration Manager crea automáticamente un vínculo de replicación de base de datos entre el sitio primario y el nuevo sitio. Crea un vínculo único para conectar ambos sitios.  

Para ayudarlo a controlar la transferencia de datos a través del vínculo de replicación de base de datos, cambie la configuración de cada vínculo. Cada vínculo de replicación es compatible con configuraciones independientes. Cada vínculo de replicación de base de datos incluye estos controles:  

- Detener la replicación de los datos del sitio seleccionados desde un sitio primario al sitio CAS. Después, el sitio CAS puede acceder directamente a estos datos desde la base de datos del sitio primario.  
- Programar la transferencia de los datos del sitio seleccionados desde un sitio primario secundario al sitio CAS.
- Definir la configuración que determina cuándo un vínculo de replicación de base de datos tiene un estado degradado o erróneo.
- Especificar cuándo se generan alertas para un vínculo de replicación con errores.
- Especificar la frecuencia con que Configuration Manager resume los datos sobre el tráfico de replicación que usa el vínculo de replicación. Estos datos se utilizan en los informes.

Para configurar un vínculo de replicación de base de datos, abra las **Propiedades** del vínculo en la consola de Configuration Manager, en el nodo **Replicación de base de datos**. Este nodo aparece en el área de trabajo **Supervisión** y en el nodo **Configuración de jerarquía** del área de trabajo **Administración**. Es posible editar un vínculo de replicación desde el sitio primario o el sitio secundario.

> [!TIP]  
> Es posible editar los vínculos de replicación de base de datos desde el nodo **Replicación de base de datos** en cualquier área de trabajo. Sin embargo, cuando usa el nodo **Replicación de base de datos** en el área de trabajo **Supervisión**, también puede ver el estado de la replicación de base de datos. También proporciona acceso a la herramienta [Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA). Use esta herramienta para ayudar a investigar los problemas con la replicación de base de datos.  

Para más información sobre cómo configurar vínculos de replicación, consulte [Controles de replicación de base de datos del sitio](#BKMK_DBRepControls). Para más información sobre cómo supervisar la replicación, consulte [Cómo supervisar los vínculos de replicación de bases de datos y el estado de replicación](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_MonitorRepLinksAndStatuss).

### <a name="bkmk_distviews"></a> Vistas distribuidas

A través de las vistas distribuidas, cuando hace una solicitud al sitio CAS para los datos del sitio seleccionados, accede directamente a la base de datos del sitio primario secundario. El acceso directo reemplaza la necesidad de replicar esos datos del sitio desde el sitio primario al sitio CAS. Dado que cada vínculo de replicación es independiente de otros vínculos de replicación, solo se pueden usar las vistas distribuidas en los vínculos de replicación elegidos. No se pueden usar vistas distribuidas entre un sitio primario y un sitio secundario.  

Las vistas distribuidas proporcionan las ventajas siguientes:  

- Reducir la carga de la CPU para procesar los cambios de base de datos en el sitio CAS y el sitio primario.
- Reducir la cantidad de datos que se transfieren a través de la red al sitio CAS.
- Mejorar el rendimiento de la instancia de SQL Server que hospeda la base de datos del sitio CAS.
- Reducir el espacio en disco que usa la base de datos del sitio CAS.

Considere la posibilidad de las vistas distribuidas cuando haya un sitio primario ubicado cerca del sitio CAS en la red, con los dos sitios siempre encendidos y siempre conectados. Las vistas distribuidas reemplazan la replicación de los datos seleccionados entre los sitios con conexiones directas entre los servidores SQL Server en cada sitio. Los sitios CAS establecen una conexión directa cada vez que se solicitan estos datos.

El sitio solicita los datos de las vistas distribuidas en estos escenarios de ejemplo:

- Cuando ejecuta informes o consultas.
- Cuando ve información en el Explorador de recursos.
- Cuando se realiza la evaluación de recopilación de las recopilaciones que incluyen reglas basadas en los datos del sitio.

De forma predeterminada, las vistas distribuidas están desactivadas para cada vínculo de replicación. Cuando activa las vistas distribuidas, puede seleccionar los datos del sitio que no se replican en el sitio CAS a través de ese vínculo. El sitio CAS accede directamente a estos datos desde la base de datos del sitio primario secundario que comparte el vínculo. Puede configurar los siguientes tipos de datos de sitio para las vistas distribuidas:  

- Datos de **inventario de hardware** de clientes.
- Datos de **inventario y de disponibilidad de software** de clientes.
- **Mensajes de estado** de clientes, el sitio primario y todos los sitios secundarios.

Cuando ve datos en la consola de Configuration Manager o en informes, las operaciones de las vistas distribuidas son invisibles para el usuario. Cuando se solicitan datos que están habilitados para las vistas distribuidas, el servidor de base de datos del sitio CAS accede directamente la base de datos del sitio primario secundario para recuperar la información.

Por ejemplo, puede usar una consola de Configuration Manager en el sitio CAS para solicitar la información del inventario de hardware del sitio primario ABC y del sitio primario XYZ. Habilita el hardware de inventario para una vista distribuida en el sitio ABC. El sitio recupera la información del inventario de cliente XYZ desde la base de datos del sitio CAS. Recupera la información del inventario de cliente ABC desde la base de datos del sitio ABC. Esta información aparece en la consola de Configuration Manager o en un informe sin que se identifique el origen.  

Siempre que un vínculo de replicación tenga un tipo de datos habilitado para las vistas distribuidas, el sitio primario secundario no replica los datos en el sitio CAS. Cuando se desactivan las vistas distribuidas para un tipo de datos, el sitio primario secundario reanuda la replicación de los datos en el sitio CAS como parte de la replicación de datos normal. Antes de que estos datos estén disponibles en el sitio CAS, los grupos de replicación que tienen estos datos se deben reinicializar entre el sitio primario y el sitio CAS. De manera similar, después de desinstalar un sitio primario que tiene activadas las vistas distribuidas, antes de que pueda acceder a estos datos en el sitio CAS, se debe completar la reinicialización de sus datos.  

> [!IMPORTANT]  
> Cuando se usan las vistas distribuidas en cualquier vínculo de replicación en la jerarquía de sitios, antes de desinstalar cualquier sitio primario, desactive las vistas distribuidas de todos los vínculos de replicación. Para obtener más información, consulte [Desinstalar un sitio primario configurado con vistas distribuidas](/sccm/core/servers/deploy/install/uninstall-sites-and-hierarchies#BKMK_UninstallPrimaryDistViews).  

#### <a name="prerequisites-and-limitations-for-distributed-views"></a>Requisitos previos y limitaciones para las vistas distribuidas  

- Solo puede usar las vistas distribuidas en los vínculos de replicación entre un sitio CAS y un sitio primario.

- El sitio CAS debe usar una edición *Enterprise* de SQL Server. El sitio primario no tiene este requisito.

- El sitio CAS solo tiene instalada una instancia del proveedor de SMS. Instale esa instancia única en el servidor de base de datos del sitio. Este requisito admite la autenticación de Kerberos. La instancia de SQL Server en el sitio CAS necesita Kerberos para acceder a la instancia de SQL Server en el sitio primario secundario. No hay limitaciones en el proveedor de SMS del sitio primario secundario.

- El sitio CAS solo tiene una instancia de SQL Server Reporting Services. Instale el punto de servicios de informes en el servidor de base de datos del sitio. Este requisito admite la autenticación de Kerberos. La instancia de SQL Server en el sitio CAS necesita Kerberos para acceder a la instancia de SQL Server en el sitio primario secundario.

- No puede hospedar la base de datos del sitio en un [clúster de SQL Server](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database).

- En la versión 1902 y versiones anteriores, no puede hospedar la base de datos del sitio en un [grupo de disponibilidad AlwaysOn de SQL Server](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database). Para admitir esta configuración, actualice a la versión 1906 o una versión posterior.<!-- SCCMDocs-pr#3792 -->

- La cuenta de equipo del servidor de bases de datos del sitio CAS requiere permisos de **lectura** en la base de datos del sitio primario.

> [!IMPORTANT]  
> Las vistas distribuidas y las [programaciones](#BKMK_schedules) de replicación de datos son configuraciones mutuamente exclusivas para un vínculo de replicación de base de datos.  

### <a name="BKMK_schedules"></a> Programar transferencias de datos de sitio en vínculos de replicación de base de datos

Para ayudarlo a controlar el ancho de banda de red que se usa para replicar los datos del sitio desde un sitio primario secundario a su sitio CAS, programe cuándo se usará un vínculo de replicación. También puede especificar cuándo se replican los distintos tipos de los datos del sitio. Es posible controlar cuándo el sitio primario va a replicar los mensajes de estado, el inventario y los datos de disponibilidad. Los vínculos de replicación de base de datos del sitio secundarios no son compatibles con programaciones para datos del sitio. No es posible programar la transferencia de los datos globales.  

Cuando se configura una programación del vínculo de replicación de base de datos, puede restringir la transferencia de los datos del sitio seleccionados desde el sitio primario al sitio CAS. También puede configurar distintas horas para replicar distintos tipos de datos del sitio.  

> [!IMPORTANT]  
> Las [vistas distribuidas](#bkmk_distviews) y las programaciones para los momentos en que se pueden replicar los datos son configuraciones mutuamente exclusivas para un vínculo de replicación de base de datos.  

### <a name="BKMK_SummarizeDBReplication"></a> Resumen de tráfico de replicación de base de datos

Cada sitio resume regularmente los datos relativos al tráfico de red que cruza los vínculos de replicación de base de datos para el sitio. El sitio usa datos resumidos en los informes para la replicación de base de datos. Ambos sitios de un vínculo de replicación resumen el tráfico de red que recorre el vínculo de replicación. El servidor de base de datos del sitio resume los datos. Una vez que se resumen los datos, la información se replica a los otros sitios como datos globales.  

De forma predeterminada, el resumen se produce cada 15 minutos. Para modificar la frecuencia de resumen del tráfico de red, edite el **intervalo de resumen** en las propiedades del vínculo de replicación de base de datos. La frecuencia de resumen afecta a la información que se ve en los informes sobre la replicación de base de datos. Puede elegir un intervalo de entre 5 a 60 minutos. Al aumentar la frecuencia de resumen, aumenta la carga de procesamiento en el servidor SQL Server de cada sitio del vínculo de replicación.  

### <a name="BKMK_DBRepThresholds"></a> Umbrales de replicación de base de datos

Los umbrales de replicación de base de datos definen cuando el sitio informa el estado de un vínculo de replicación de base de datos como degradado o erróneo. De manera predeterminada, establece un vínculo al estado *degradado* cuando un grupo de replicación no puede completar la replicación durante 12 intentos consecutivos. Establece el vínculo al estado *erróneo* cuando cualquier grupo de replicación no se puede replicar durante 24 intentos consecutivos.  

Puede especificar valores predeterminados para el estado degradado o erróneo. Si ajusta estos valores, puede supervisar de manera más segura el estado de la replicación de base de datos a través de los vínculos.  

Es posible que uno o varios grupos de replicación no se puedan replicar mientras que otros grupos de replicación se siguen replicando de manera correcta. Planee revisar el estado de replicación de un vínculo cuando notifique por primera vez un estado degradado. Si algunos grupos de replicación específicos presentan retrasos periódicos, pero ese retraso no representa un problema, o si el vínculo de red entre los sitios dispone de poco ancho de banda, considere la posibilidad de modificar los valores de reintento para el estado degradado o con errores del vínculo. Si aumenta el número de reintentos antes de que el estado del vínculo se establezca en degradado o con errores, se pueden eliminar los avisos falsos de problemas conocidos y realizar un seguimiento más preciso del estado del vínculo.  

También se debe tener en cuenta el intervalo de sincronización de cada grupo de replicación para cada grupo de replicación para comprender la frecuencia con la que se produce la replicación de ese grupo. Para ver el **Estado de sincronización** de los grupos de replicación, haga clic en la pestaña **Detalle de la replicación** de un vínculo de replicación del nodo **Replicación de base de datos** en el área de trabajo **Supervisión**.  

Para más información sobre cómo supervisar la replicación de base de datos, incluso cómo ver el estado de replicación, consulte [Cómo supervisar los vínculos de replicación de bases de datos y el estado de replicación](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_MonitorRepLinksAndStatuss).  

Para más información sobre cómo configurar los umbrales de replicación de base de datos, consulte [Controles de replicación de base de datos de sitio](#BKMK_DBRepControls).  


## <a name="BKMK_DBRepControls"></a> Controles de replicación de base de datos de sitio

Para ayudarlo a controlar el ancho de banda de red que se usa para la replicación de base de datos, cambie la configuración de cada base de datos de sitio. Las opciones solo se aplican a la base de datos de sitio donde las configuró. Las opciones siempre se usan cuando el sitio replica cualquier dato mediante replicación de base de datos en otro sitio.  

Puede modificar estos controles de replicación para cada base de datos de sitio:  

- El puerto SSB.
- El período de tiempo de espera antes de que los errores de replicación provoquen que el sitio reinicialice su copia de la base de datos de sitio.
- Comprima los datos que se replican por replicación de base de datos. Los datos se comprimen solo para transferirse entre sitios y no para almacenarse en la base de datos de cada sitio.  

Para cambiar la configuración de los controles de replicación de una base de datos de sitio, edite las propiedades de la base de datos en la consola de Configuration Manager, en el nodo **Replicación de base de datos**. Este nodo aparece en el nodo **Configuración de jerarquía** del área de trabajo **Administración** y también aparece en el área de trabajo **Supervisión**. Para editar las propiedades de la base de datos de sitio, seleccione el vínculo de replicación entre los sitios y, después, abra las **Propiedades de base de datos primaria** o las **Propiedades de base de datos secundaria**.  

> [!TIP]  
> Es posible configurar los controles de replicación de base de datos desde el nodo **Replicación de base de datos** en cualquier área de trabajo. Sin embargo, cuando usa el nodo **Replicación de base de datos** en el área de trabajo **Supervisión**, también puede ver el estado de la replicación de base de datos. También proporciona acceso a la herramienta [Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA). Use esta herramienta para ayudar a investigar los problemas con la replicación de base de datos.  
