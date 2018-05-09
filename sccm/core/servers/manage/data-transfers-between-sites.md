---
title: Transferencias de datos
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo Configuration Manager mueve datos entre sitios y cómo se puede administrar la transferencia de datos a través de la red.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 45fb1bc31a7e888ca4caa21a710e74ec0fde422c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-transfers-between-sites-in-system-center-configuration-manager"></a>Transferencias de datos entre sitios en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

System Center Configuration Manager usa la **replicación basada en archivos** y la **replicación de base de datos** para transferir distintos tipos de información entre sitios. Obtenga información sobre cómo Configuration Manager mueve datos entre sitios y cómo se puede administrar la transferencia de datos a través de la red.  


## <a name="bkmk_fileroute"></a> File-based replication  
Configuration Manager usa la replicación basada en archivos para transferir datos basados en archivos entre sitios de la jerarquía. Estos datos incluyen aplicaciones y paquetes que quiere implementar en puntos de distribución de sitios secundarios, así como registros de datos de detección no procesados que se transfieren a sitios principales donde se procesan.  

La comunicación entre sitios basada en archivos usa el protocolo **Bloque de mensajes del servidor** (SMB) en el puerto TCP/IP 445. Puede especificar la limitación de ancho de banda y el modo por pulsos para controlar el volumen de datos transferidos a través de la red, y puede usar programaciones para controlar cuándo enviar datos a través de la red.  

### <a name="bkmk_routes"></a> Rutas de replicación de archivos  
La información siguiente puede ayudar a configurar y usar las rutas de replicación de archivos.  

#### <a name="file-replication-route"></a>Ruta de replicación de archivos

Cada ruta de replicación de archivos identifica un sitio de destino al que se pueden transferir los datos basados en archivos. Cada sitio admite una ruta de replicación de archivos a un sitio de destino específico.  

Puede cambiar los siguientes valores para rutas de replicación de archivos:  

-  **Cuenta de replicación de archivos**. Esta cuenta se conecta al sitio de destino y escribe datos en el recurso compartido **SMS_Site** del sitio. El sitio de destino procesa los datos escritos en este recurso compartido. De forma predeterminada, cuando se agrega un sitio a la jerarquía, Configuration Manager asigna la cuenta de equipo del nuevo servidor de sitios como la Cuenta de replicación de archivos de dichos sitios. Después, esta cuenta se agrega al grupo **SMS_SiteToSiteConnection_&lt;código de sitio\>** del sitio de destino, un grupo local en el equipo que concede acceso al recurso compartido SMS_Site. Puede cambiar esta cuenta para que sea una cuenta de usuario de Windows. Si cambia la cuenta, asegúrese de agregar la nueva cuenta al grupo **SMS_SiteToSiteConnection_&lt;código de sitio\>** del sitio de destino.  

    > [!NOTE]  
    >  Los sitios secundarios siempre utilizan la cuenta de equipo del servidor de sitio secundario como la **Cuenta de replicación de archivos**.  

-  **Programación**. Puede configurar la programación de cada ruta de replicación de archivos para restringir el tipo de datos y la hora a la que se pueden transferir datos al sitio de destino.  
-  **Límites de frecuencia**. Puede especificar los límites de frecuencia para cada ruta de replicación de archivos a fin de controlar el ancho de banda de red que se usa cuando el sitio transfiere datos al sitio de destino:  

    -  Utilice el **modo por pulsos** para especificar el tamaño de los bloques de datos que se envían al sitio de destino. También puede especificar un retraso de tiempo entre el envío de cada bloque de datos. Use esta opción cuando tenga que enviar datos a través de una conexión de red con un ancho de banda muy bajo al sitio de destino. Por ejemplo, podría tener limitaciones al enviar 1 kB de datos cada cinco segundos, y no 1 kB cada tres segundos, independientemente de la velocidad del vínculo o su uso en un momento dado.
    -  Utilice **Limitado al máximo especificado de velocidades de transferencia por hora** para que un sitio envíe datos a un sitio de destino usando sólo el porcentaje de tiempo especificado. Cuando use esta opción, Configuration Manager no identifica el ancho de banda disponible de las redes, sino que divide el tiempo en que puede enviar datos en intervalos de tiempo. Después, se envían datos durante un corto periodo de tiempo, seguido de periodos de tiempo durante los cuales no se envían datos. Por ejemplo, si la velocidad máxima se establece en **50 %**, Configuration Manager transmitirá datos durante una cantidad de tiempo seguida de un periodo de tiempo igual en que no se enviarán datos. La cantidad real de datos, o el tamaño del bloque de datos, no se administra. En su lugar, solo se administra la cantidad de tiempo durante la cual se envían datos.  

        > [!CAUTION]  
        > De forma predeterminada, un sitio puede utilizar hasta tres **envíos simultáneos** para transferir datos a un sitio de destino. Cuando se habilitan los límites de frecuencia para una ruta de replicación de archivos, los **envíos simultáneos** para enviar datos a ese sitio están limitados a uno. Esto se aplica incluso cuando la opción **Limitar ancho de banda disponible (%)** se establece en **100%**. Por ejemplo, si usa la configuración predeterminada para el remitente, esto reduce la velocidad de transferencia al sitio de destino para que sea un tercio de la capacidad predeterminada.  

-  Puede configurar una ruta de replicación de archivos entre dos sitios secundarios para distribuir contenido basado en archivos entre dichos sitios.  

Para administrar una ruta de replicación de archivos, en el área de trabajo **Administración**, expanda el nodo **Configuración de jerarquía** y, después, seleccione **Replicación de archivos**.  

#### <a name="sender"></a>Remitente

Cada sitio tiene un remitente. El remitente administra la conexión de red desde un sitio a un sitio de destino y puede establecer conexiones a varios sitios al mismo tiempo. Para conectarse a un sitio, el remitente utiliza la ruta de replicación de archivos al sitio para identificar la cuenta que se va a utiliza para establecer la conexión de red. El remitente también usa esta cuenta para escribir datos en el recurso compartido SMS_Site del sitio de destino.  

De forma predeterminada, el remitente escribe datos en un sitio de destino mediante el uso de varios **envíos simultáneos**, lo que normalmente se conoce como un subproceso. Cada envío simultáneo, o subproceso, puede transferir un objeto basado en archivo diferente al sitio de destino. De forma predeterminada, cuando el remitente comienza a enviar un objeto, continúa escribiendo bloques de datos para ese objeto hasta que se envía todo el objeto. Una vez que se han enviado todos los datos para el objeto, un nuevo objeto puede empezar a enviar ese subproceso.  

Puede cambiar los siguientes valores para un remitente:  

-  **Máximo de envíos simultáneos**. De forma predeterminada, cada sitio usa cinco envíos simultáneos, con tres envíos disponibles para su uso cuando el sitio envía datos a un sitio de destino. Si aumenta este número, podrá aumentar la transmisión de datos entre sitios dado que Configuration Manager puede transferir más archivos al mismo tiempo. Si se aumenta este número, también aumenta la demanda de ancho de banda de red entre sitios.  

-  **Configuración de reintento**. De forma predeterminada, cada sitio reintenta dos veces una conexión con problemas, con un retraso de un minuto entre intentos de conexión. Puede modificar el número de intentos de conexión que realiza el sitio y el tiempo que hay que esperar entre ellos.  

Para administrar el remitente para un sitio, expanda el nodo **Configuración de sitio** del área de trabajo **Administración**, seleccione el nodo **Sitios** y, después, haga clic en **Propiedades** para el sitio que quiere administrar. Haga clic en la pestaña **Remitente** para cambiar la configuración del remitente.  

## <a name="bkmk_dbrep"></a> Database replication  
La replicación de base de datos de Configuration Manager usa SQL Server para transferir datos y combinar los cambios realizados en una base de datos de sitio con la información almacenada en la base de datos de otros sitios de la jerarquía. Tenga en cuenta lo siguiente sobre la replicación de base de datos:

-  Todos los sitios comparten la misma información.  
-  Cuando se instala un sitio en una jerarquía, la replicación de base de datos se establece automáticamente entre el nuevo sitio y su sitio primario designado.  
-  Cuando finaliza la instalación del sitio, se inicia automáticamente la replicación de base de datos.  

Si se agrega un nuevo sitio a una jerarquía, Configuration Manager crea una base de datos genérica en el nuevo sitio. Después, el sitio primario crea una instantánea de los datos relevantes en su base de datos y transfiere esa instantánea al nuevo sitio mediante replicación basada en archivos. De este modo, el nuevo sitio usa un programa de copia masiva (BCP) de SQL Server para cargar la información en su copia local de la base de datos de Configuration Manager. Después de cargar la instantánea, cada sitio lleva a cabo la replicación de base de datos con el otro sitio.  

Para replicar datos entre sitios, Configuration Manager usa su propio servicio de replicación de base de datos. El servicio de replicación de base de datos usa el seguimiento de cambios de SQL Server para supervisar los cambios de la base de datos de sitio local y luego replica los cambios en otros sitios mediante SQL Server Service Broker (SSB). De forma predeterminada, este proceso usa el puerto TCP/IP 4022.  

Configuration Manager agrupa los datos replicados mediante la replicación de base de datos en grupos de replicación diferentes. Tenga en cuenta lo siguiente sobre los grupos de replicación:

-  Cada grupo de replicación tiene una programación de replicación independiente y fija que determina la frecuencia con que los cambios en los datos del grupo se replican a otros sitios.  

     Por ejemplo, un cambio en una configuración de administración basada en roles se replica rápidamente en otros sitios para garantizar que estos cambios se apliquen lo más pronto posible. Mientras tanto, un cambio de configuración de menor prioridad, como una solicitud para instalar un nuevo sitio secundario, se replica con menos urgencia. Una solicitud de nuevo sitio puede tardar varios minutos en llegar al sitio primario de destino.  

-   Puede modificar la siguiente configuración para la replicación de base de datos:  

    -  **Vínculos de replicación de base de datos**. Controle cuándo el tráfico específico cruza la red.  
    -  **Vistas distribuidas**. Cambie la configuración para vínculos de replicación para que las solicitudes de datos de un sitio seleccionado realizadas en un sitio de administración central tengan acceso a esos datos de sitio directamente desde la base de datos en un sitio primario secundario.  
    -  **Programaciones**. Especifique cuándo se usa un vínculo de replicación y cuándo se replican distintos tipos de datos del sitio.  
    -  **Resumen**. Cambie la configuración de resumen de datos sobre el tráfico de red que cruza los vínculos de replicación. De forma predeterminada, el resumen se produce cada 15 minutos y se usa en informes para la replicación de base de datos.  
    -  **Umbrales de replicación de base de datos**. Defina cuándo se notifican los vínculos como degradados o con error. También es posible configurar en qué momento Configuration Manager genera alertas relativas a los vínculos de replicación que tienen un estado de degradado o con error.  

Configuration Manager clasifica los datos replicados mediante replicación de base de datos como **datos globales** o **datos de sitio**. Cuando se produce la replicación de base de datos, los cambios en los datos globales y los datos de sitio se transfieren a través del vínculo de replicación de base de datos. Los datos globales se pueden replicar en un sitio primario o secundario. Los datos de sitio solo se replican en un sitio primario. Existe un tercer tipo de datos, datos locales, que no se replica en otros sitios. Los datos locales incluyen información que no requieren otros sitios. Tenga en cuenta lo siguiente sobre los tipos de datos:  

-  **Datos globales**. Los datos globales hacen referencia a objetos creados por el administrador que se replican en todos los sitios a lo largo de la jerarquía, aunque los sitios secundarios reciben sólo un subconjunto de datos globales, como los datos de proxy globales. Los datos globales incluyen implementaciones de software, actualizaciones de software, definiciones de colecciones y ámbitos de seguridad de administración basada en roles. Los administradores pueden crear datos globales en sitios de administración central y en sitios primarios.  
-  **Datos de sitio**. Los datos de sitio hacen referencia a información operativa creada por sitios primarios de Configuration Manager y los clientes que se comunican con los sitios primarios. Los datos de sitio se replican en el sitio de administración central pero no en otros sitios primarios. Los datos de sitio incluyen datos de inventario de hardware, mensajes de estado, alertas y resultados de recopilaciones basadas en consultas. Los datos de sitio solo son visibles en el sitio de administración central y en el sitio primario donde se originan los datos. Los datos de sitio pueden modificarse únicamente en el sitio primario donde se crearon.  

     Todos los datos de sitio se replican en el sitio de administración central. El sitio de administración central realiza la administración y la creación de informes para toda la jerarquía de sitios.  

En las secciones siguientes, se detallan las configuraciones que puede cambiar para administrar la replicación de base de datos.  

### <a name="bkmk_Dblinks"></a> Vínculos de replicación de base de datos  
Cuando se instala un nuevo sitio en una jerarquía, Configuration Manager crea automáticamente un vínculo de replicación de base de datos entre el sitio primario y el nuevo sitio. Para conectar los dos sitios, se crea un único vínculo.  

Puede cambiar la configuración de cada vínculo de replicación de base de datos para controlar la transferencia de datos a través del vínculo de replicación. Cada vínculo de replicación es compatible con configuraciones independientes. Los controles para los vínculos de replicación de base de datos incluyen los siguientes:  

-  Detener la replicación de datos de sitio seleccionados desde un sitio primario al sitio de administración central, para que el sitio de administración central pueda tener acceso directamente a estos datos desde la base de datos del sitio primario.  
-  Programar los datos de sitio seleccionados para transferirlos desde un sitio primario secundario al sitio de administración central.
-  Definir la configuración que determina cuándo un vínculo de replicación de base de datos tiene un estado degradado o con errores.
-  Especificar cuándo se generan alertas para un vínculo de replicación con errores.
-  Especificar la frecuencia con que Configuration Manager resume los datos sobre el tráfico de replicación que usa el vínculo de replicación. Estos datos se utilizan en los informes.

Para configurar un vínculo de replicación de base de datos, edite las propiedades del vínculo en la consola de Configuration Manager, en el nodo **Replicación de base de datos**. Este nodo aparece en el área de trabajo **Supervisión** y en el nodo **Configuración de jerarquía** del área de trabajo **Administración**. Es posible editar un vínculo de replicación desde el sitio primario o el sitio secundario del vínculo de replicación.  

> [!TIP]  
> Es posible editar los vínculos de replicación de base de datos desde el nodo **Replicación de base de datos** en cualquier área de trabajo. En cambio, cuando se usa el nodo **Replicación de base de datos** en el área de trabajo **Supervisión**, también se puede ver el estado de la replicación de base de datos para los vínculos de replicación y tener acceso a la herramienta Replication Link Analyzer para investigar problemas con la replicación de base de datos.  

Para más información sobre cómo configurar vínculos de replicación, consulte [Controles de replicación de base de datos de sitio](#BKMK_DBRepControls). Para obtener más información sobre cómo supervisar la replicación, consulte [Cómo supervisar los vínculos de replicación de bases de datos y el estado de replicación](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) en el tema [Supervisar la infraestructura de la jerarquía y replicación de System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

Use la información de las secciones siguientes para planear los vínculos de replicación de base de datos.  

### <a name="bkmk_distviews"></a> Vistas distribuidas  
Mediante las vistas distribuidas, las solicitudes realizadas en un sitio de administración central para datos de sitio seleccionados obtienen acceso a esos datos de sitio directamente desde la base de datos en un sitio primario secundario. El acceso directo reemplaza la necesidad de replicar esos datos de sitios desde el sitio primario al sitio de administración central. Dado que cada vínculo de replicación es independiente de otros vínculos de replicación, solo se pueden usar las vistas distribuidas en los vínculos de replicación elegidos. No se pueden usar vistas distribuidas entre un sitio primario y un sitio secundario.  

Las vistas distribuidas pueden proporcionar las siguientes ventajas:  

-  Reducir la carga de CPU para procesar los cambios de la base de datos en el sitio de administración central y los sitios primarios
-  Reducir la cantidad de datos que se transfieren a través de la red al sitio de administración central
-  Mejorar el rendimiento del servidor SQL Server que hospeda la base de datos del sitio de administración central
-  Reducir el espacio en disco usado por la base de datos en el sitio de administración central

Considere la posibilidad de usar vistas distribuidas cuando un sitio primario esté cerca del sitio de administración central en la red, y los dos sitios estén siempre activados y siempre conectados. Se debe a que las vistas distribuidas reemplazan la replicación de los datos seleccionados entre los sitios con conexiones directas entre los servidores SQL Server en cada sitio. Se crea una conexión directa cada vez que se realiza una solicitud de estos datos en el sitio de administración central. Normalmente, las solicitudes de datos que se puedan habilitar para vistas distribuidas se realizan al ejecutar informes o consultas, cuando se ve información en el Explorador de recursos o mediante la evaluación de colecciones que incluyen reglas basadas en los datos del sitio.  

De forma predeterminada, las vistas distribuidas están desactivadas para cada vínculo de replicación. Al activar las vistas distribuidas para un vínculo de replicación, se seleccionan datos de sitio que no se replicarán en el sitio de administración central a través de ese vínculo. El sitio de administración central tiene acceso a estos datos directamente desde la base de datos del sitio primario secundario que comparte el vínculo. Puede configurar los siguientes tipos de datos de sitio para las vistas distribuidas:  

-  Datos de inventario de hardware de clientes
-  Datos de inventario y de disponibilidad de software de clientes
-  Mensajes de estado de clientes, el sitio primario y todos los sitios secundarios

Desde el punto de vista operativo, las vistas distribuidas son invisibles para los usuarios administrativos que visualizan datos en la consola de Configuration Manager o en los informes. Cuando se realiza una solicitud de datos que están habilitados para vistas distribuidas, el servidor SQL Server que hospeda la base de datos para el sitio de administración central obtiene acceso directamente al servidor SQL Server del sito primario secundario para recuperar la información. Un ejemplo sería cuando se usa una consola de Configuration Manager en el sitio de administración central para solicitar información sobre inventario de hardware de dos sitios, y solamente un sitio tiene el inventario de hardware habilitado para una vista distribuida. La información de inventario para los clientes del sitio que no está configurada para vistas distribuidas se recupera de la base de datos en el sitio de administración central. A la información de inventario para los clientes del sitio que está configurado para vistas distribuidas se tiene acceso desde la base de datos del sitio primario secundario. Esta información aparece en la consola de Configuration Manager o en un informe sin que se identifique el origen.  

Siempre que un vínculo de replicación tenga un tipo de datos habilitado para vistas distribuidas, el sitio primario secundario no replica los datos en el sitio de administración central. Tan pronto como se desactiven las vistas distribuidas para un tipo de datos, el sitio primario secundario reanuda la replicación de los datos en el sitio de administración central como parte de la replicación de datos normal. En cambio, antes de que estos datos estén disponibles en el sitio de administración central, los grupos de replicación que tienen estos datos se deben reinicializar entre el sitio primario y el sitio de administración central. Igualmente, una vez que se desinstale un sitio primario que tenga activadas las vistas distribuidas, el sitio de administración central deberá completar la reinicialización de sus datos antes de que se pueda obtener acceso a los datos que se han habilitado para las vistas distribuidas en el sitio de administración central.  

> [!IMPORTANT]  
> Cuando se usan vistas distribuidas en cualquier vínculo de replicación en la jerarquía de sitios, se deben desactivar las vistas distribuidas para todos los vínculos de replicación antes de desinstalar cualquier sitio primario. Para obtener más información, consulte [Uninstall a primary site that is configured with distributed views](../../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#BKMK_UninstallPrimaryDistViews) (Desinstalar un sitio primario configurado con vistas distribuidas).  

#### <a name="prerequisites-and-limitations-for-distributed-views"></a>Requisitos previos y limitaciones para las vistas distribuidas  

-  Solo se pueden usar vistas distribuidas en vínculos de replicación entre un sitio de administración central y un sitio primario.
- El sitio de administración central debe usar una edición Enterprise de SQL Server. El sitio primario no tiene este requisito.
-  El sitio de administración central sólo puede tener una instancia del proveedor de SMS instalada, y esa instancia debe estar instalada en el servidor de base de datos del sitio. Esto es necesario para admitir la autenticación Kerberos requerida para que el servidor SQL Server en el sitio de administración central pueda tener acceso al servidor SQL Server en el sitio primario secundario. No hay limitaciones en el proveedor de SMS del sitio primario secundario.
-  El sitio de administración central puede sólo puede tener un punto de SQL Server Reporting Services instalado, y debe estar ubicado en el servidor de base de datos del sitio. Esto es necesario para admitir la autenticación Kerberos requerida para habilitar el servidor SQL Server en el sitio de administración central para tener acceso al servidor SQL Server en el sitio primario secundario.
-  La base de datos del sitio no puede hospedarse en un clúster de SQL Server.
-  La base de datos del sitio no se puede hospedar en un grupo de disponibilidad AlwaysOn de SQL Server.
-  La cuenta de equipo del servidor de base de datos del sitio de administración central requiere permisos de lectura para la base de datos del sitio primario.

> [!IMPORTANT]  
>  Las vistas distribuidas y las programaciones de replicación de datos son configuraciones mutuamente exclusivas para un vínculo de replicación de base de datos.  

### <a name="BKMK_schedules"></a> Programar transferencias de datos de sitio en vínculos de replicación de base de datos  
Para poder controlar el ancho de banda de red que se utiliza para replicar datos de un sitio primario secundario en su sitio de administración central, es posible programar cuándo se va a utilizar un vínculo de replicación y especificar cuándo se van a replicar los distintos tipos de datos de sitio. Es posible controlar cuándo el sitio primario va a replicar los mensajes de estado, el inventario y los datos de disponibilidad. Los vínculos de replicación de base de datos de sitios secundarios no son compatibles con programaciones para datos de sitio. No se puede programar la transferencia de datos globales.  

Cuando se configura una programación de vínculos de replicación de base de datos, es posible restringir la transferencia de datos de sitio seleccionados desde el sitio primario al sitio de administración central, además de configurar momentos diferentes para replicar distintos tipos de datos de sitio.  

> [!IMPORTANT]  
> Las vistas distribuidas y las programaciones de replicación de datos son configuraciones mutuamente exclusivas para un vínculo de replicación de base de datos.  

### <a name="BKMK_SummarizeDBReplication"></a> Resumen de tráfico de replicación de base de datos  
Cada sitio resume regularmente los datos relativos al tráfico de red que cruza los vínculos de replicación de base de datos para el sitio. Los datos resumidos se usan en informes para la replicación de base de datos. Ambos sitios de un vínculo de replicación resumen el tráfico de red que recorre el vínculo de replicación. El resumen de los datos lo realiza el servidor SQL Server que hospeda la base de datos del sitio. Después de resumirse los datos, la información se replica en otros sitios como datos globales.  

De forma predeterminada, el resumen se produce cada 15 minutos. Para modificar la frecuencia de resumen del tráfico de red, edite el **Intervalo de resumen** en las propiedades del vínculo de replicación de base de datos. La frecuencia de resumen afecta a la información que se ve en los informes sobre la replicación de base de datos. Puede elegir un intervalo de entre 5 y 60 minutos. Al aumentar la frecuencia de resumen, aumenta la carga de procesamiento en el servidor SQL Server de cada sitio del vínculo de replicación.  

### <a name="BKMK_DBRepThresholds"></a> Umbrales de replicación de base de datos  
Los umbrales de replicación de base de datos definen cuándo el estado de un vínculo de replicación de base de datos se establece como degradado o con errores. De forma predeterminada, un vínculo se establece en estado degradado cuando un grupo de replicación no puede completar la replicación durante 12 intentos consecutivos. El vínculo se establece en estado de error cuando un grupo de replicación no puede replicar durante 24 intentos consecutivos.  

Se pueden especificar valores personalizados para ajustar cuándo Configuration Manager va a notificar el estado de un vínculo de replicación como degradado o con error. La posibilidad de ajustar cuándo Configuration Manager va a notificar cada uno de los estados de los vínculos de replicación de base de datos puede ayudarle a supervisar de forma precisa el estado de la replicación de base de datos en todos los vínculos de replicación.  

Ya que es posible que uno o varios grupos de replicación no puedan replicar mientras que otros grupos de replicación continúan replicando correctamente, se debe planear la revisión del estado de replicación de un vínculo de replicación cuando notifique por primera vez un estado degradado. Si algunos grupos de replicación específicos presentan retrasos periódicos, pero ese retraso no representa un problema, o si el vínculo de red entre los sitios dispone de poco ancho de banda, considere la posibilidad de modificar los valores de reintento para el estado degradado o con errores del vínculo. Si aumenta el número de reintentos antes de que el estado del vínculo se establezca en degradado o con errores, se pueden eliminar los avisos falsos de problemas conocidos y realizar un seguimiento más preciso del estado del vínculo.  

También se debe tener en cuenta el intervalo de sincronización de replicación para cada grupo de replicación para comprender la frecuencia con la que se produce la replicación de ese grupo. Para ver el **Estado de sincronización** de los grupos de replicación, haga clic en la pestaña **Detalle de la replicación** de un vínculo de replicación del nodo **Replicación de base de datos** en el área de trabajo **Supervisión**.  

Para obtener más información sobre cómo supervisar la replicación de base de datos, incluida la forma de ver el estado de la replicación, consulte [Cómo supervisar los vínculos de replicación de bases de datos y el estado de replicación](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) en el tema [Supervisar la infraestructura de la jerarquía y replicación de System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

Para obtener más información sobre cómo configurar los umbrales de replicación de base de datos, consulte [Controles de replicación de base de datos de sitio](#BKMK_DBRepControls).  

## <a name="BKMK_DBRepControls"></a> Controles de replicación de base de datos de sitio  
Se puede cambiar la configuración de cada base de datos de sitio para controlar el ancho de banda de red usado para la replicación de base de datos. Las opciones solo se aplican a la base de datos de sitio en la que se configuran las opciones. Las opciones siempre se usan cuando el sitio replica cualquier dato mediante replicación de base de datos en otro sitio.  

Estos son los controles de replicación que puede modificar para cada base de datos de sitio:  

-  Cambiar el puerto SSB.  
-  Configurar el tiempo de espera antes de que los errores de replicación provoquen que el sitio reinicialice su copia de la base de datos de sitio.  
-  Configurar una base de datos de sitio para comprimir los datos que se replican mediante replicación de base de datos. Los datos se comprimen solo para transferirse entre sitios y no para almacenarse en la base de datos de cada sitio.  

Para cambiar la configuración de los controles de replicación de una base de datos de sitio, edite las propiedades de la base de datos en la consola de Configuration Manager, en el nodo **Replicación de base de datos**. Este nodo aparece en el nodo **Configuración de jerarquía** del área de trabajo **Administración** y también aparece en el área de trabajo **Supervisión**. Para editar las propiedades de la base de datos de sitio, seleccione el vínculo de replicación entre los sitios y, después, abra las **Propiedades de base de datos primaria** o las **Propiedades de base de datos secundaria**.  

> [!TIP]  
> Es posible configurar los controles de replicación de base de datos desde el nodo **Replicación de base de datos** en cualquier área de trabajo. En cambio, cuando se usa el nodo **Replicación de base de datos** en el área de trabajo **Supervisión**, también se puede ver el estado de la replicación de base de datos para un vínculo de replicación y tener acceso a la herramienta Replication Link Analyzer para investigar problemas de replicación.  
