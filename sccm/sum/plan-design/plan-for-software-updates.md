---

title: Planear las actualizaciones de software | System Center Configuration Manager
description: "Es imprescindible planear la infraestructura de punto de actualización de software antes de usar las actualizaciones de software en un entorno de producción de System Center Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 69f2c9c3c098013679e12d8578a780130adb94be


---

# <a name="plan-for-software-updates-in-system-center-configuration-manager"></a>Planear las actualizaciones de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Antes de usar las actualizaciones de software en un entorno de producción de System Center Configuration Manager, es importante que siga el proceso de planeamiento. Tener un buen plan para la infraestructura de punto de actualización de software es la clave para conseguir una correcta implementación de actualizaciones de software.

## <a name="capacity-planning-recommendations-for-software-updates"></a>Recomendaciones para la planeación de capacidad para las actualizaciones de software  
 Puede utilizar las siguientes recomendaciones como una línea de base que puede ayudarle a determinar la información para la planeación de la capacidad de las actualizaciones de software que sea adecuada para su organización. Los requisitos de capacidad reales pueden variar de las recomendaciones que se enumeran en este tema en función de los siguientes criterios: el entorno de red específico, el hardware que usa para hospedar el sistema de sitio de puntos de actualización de software, el número de clientes instalados y los roles del sistema de sitio que están instalados en el servidor.  

###  <a name="a-namebkmksumcapacitya-capacity-planning-for-the-software-update-point"></a><a name="BKMK_SUMCapacity"></a> Planeamiento de la capacidad para el punto de actualización de software  
 El número de clientes admitidos depende de la versión de Windows Server Update Services (WSUS) que se ejecuta en el punto de actualización de software, y también depende de si el rol del sistema de sitio del punto de actualización de software coexiste con otro rol del sistema de sitio:  

-   El punto de actualización de software puede admitir hasta 25 000 clientes cuando WSUS se ejecuta en el equipo del punto de actualización de software y este punto coexiste con otro rol de sistema de sitio.  

-   El punto de actualización de software puede admitir hasta 150 000 clientes cuando el equipo remoto cumple los requisitos de WSUS para admitir este número de clientes.   
    De manera predeterminada, Configuration Manager no admite la configuración de puntos de actualización de software como clústeres de NLB. En cambio, puede usar el SDK de Configuration Manager para configurar hasta cuatro puntos de actualización de software en un clúster de NLB.  

### <a name="capacity-planning-for-software-updates-objects"></a>Planeación de la capacidad para los objetos de actualizaciones de software  
 Utilice la siguiente información de capacidad para planear los objetos de actualizaciones de software.  

-   **Límite de 1.000 actualizaciones de software en una implementación**  

     Debe limitar el número de actualizaciones de software a 1.000 por cada implementación de actualización de software. Cuando crea una regla de implementación automática, especifique un criterio que limite el número de actualizaciones de software que se devuelven. Se produce un error en la regla de implementación automática cuando los criterios especificados devuelven más de 1.000 actualizaciones de software. Puede comprobar el estado de la regla de implementación automática desde el nodo **Reglas de implementación automática** de la consola de Configuration Manager. Al implementar manualmente las actualizaciones de software, no seleccione más de 1.000 actualizaciones para implementar.  

     También debe limitar el número de actualizaciones de software a 1000 en una línea base de configuración. Para obtener más información, consulte [Crear una línea base de configuración](../../compliance/deploy-use/create-configuration-baselines.md).

##  <a name="a-namebkmksupinfrastructurea-determine-the-software-update-point-infrastructure"></a><a name="BKMK_SUPInfrastructure"></a> Determinar la infraestructura del punto de actualización de software  
 El sitio de administración central y todos los sitios primarios secundarios deben tener un punto de actualización de software donde va a implementar las actualizaciones de software. Cuando planee la infraestructura del punto de actualización de software, necesitará determinar las siguientes dependencias: en dónde instalar el punto de actualización de software para el sitio; qué sitios requieren un punto de actualización de software que acepta la comunicación desde clientes basados en Internet; si se va a configurar el punto de actualización de software como un clúster del NLB, y si se necesita un punto de actualización de software en un sitio secundario. Consulte las secciones siguientes para determinar la infraestructura del punto de actualización de software.  

> [!IMPORTANT]  
>  Para obtener información sobre las dependencias internas y externas que se requieren para las actualizaciones de software, consulte [Requisitos previos para las actualizaciones de software](prerequisites-for-software-updates.md).  

 Puede agregar varios puntos de actualización de software en un sitio primario de Configuration Manager. La posibilidad de tener varios puntos de actualización de software en un sitio ofrece tolerancia a errores sin requerir la complejidad del NLB. Sin embargo, la conmutación por error que recibe con varios puntos de actualización de software no es tan sólida como el NLB para el equilibrio de carga puro, sino que está diseñada para tolerancia a errores. Además, el diseño de conmutación por error del punto de actualización de software difiere del modelo de selección aleatoria pura, que se utiliza en el diseño de los puntos de administración. A diferencia del diseño de los puntos de administración, en los puntos de actualización de software hay costes de rendimiento de red y de cliente asociados al cambio a un nuevo punto de actualización de software. Cuando el cliente cambia a un servidor de WSUS nuevo para explorar actualizaciones de software, el resultado es un aumento del tamaño del catálogo, y demandas de rendimiento de red y de cliente asociadas. Por tanto, el cliente conserva la afinidad con el último punto de actualización de software que exploró satisfactoriamente.  

 El primer punto de actualización de software que se instala en un sitio primario es el origen de sincronización para todos los puntos de actualización de software adicionales que se agregan al sitio primario. Después de haber agregado los puntos de actualización de software y de haber iniciado la sincronización de actualizaciones de software, puede ver el estado de dichos puntos y el origen de sincronización en el nodo **Estado de sincronización de punto de actualización de software** del área de trabajo **Supervisión** .  

 Cuando se produce un error en el punto de actualización de software y dicho punto está configurado como el origen de sincronización para el resto de puntos de actualización de software del sitio, es necesario quitar manualmente el punto de actualización de software que produjo el error, y seleccionar un punto nuevo para usarlo como el origen de sincronización. Para obtener más información sobre cómo quitar un punto de actualización de software, consulte [Quitar el rol del sistema de sitio del punto de actualización de software](../get-started/remove-a-software-update-point.md).  

###  <a name="a-namebkmksuplista-software-update-point-list"></a><a name="BKMK_SUPList"></a> Lista de puntos de actualización de software  
 Configuration Manager proporciona el cliente con una lista de punto de actualización de software en los siguientes escenarios: si un cliente nuevo recibe la directiva para habilitar actualizaciones de software, o si un cliente no puede ponerse en contacto con su punto de actualización de software y necesita cambiar a otro punto. El cliente selecciona aleatoriamente un punto de actualización de software de la lista, y da prioridad a los puntos de actualización de software que se encuentran en el mismo bosque. Configuration Manager proporciona clientes de otra lista según el tipo de cliente.  

-   **Clientes basados en intranet**: recibe una lista de puntos de actualización de software que puede configurar para permitir conexiones solo desde la intranet, o una lista de puntos de actualización de software que permiten las conexiones de cliente de Internet o intranet.  

-   **Clientes basados en Internet**: reciben una lista de puntos de actualización de software que se configuran para permitir conexiones provenientes de Internet solamente o una lista de puntos de actualización de software que permiten conexiones de cliente a Internet e intranet.  

###  <a name="a-namebkmksupswitchinga-software-update-point-switching"></a><a name="BKMK_SUPSwitching"></a> Cambio de punto de actualización de software  
 Si tiene varios puntos de actualización de software en un sitio y uno deja de estar disponible o genera errores, los clientes se conectarán a otro punto de actualización de software, y continuarán con la exploración para detectar las actualizaciones de software más recientes. Cuando a un cliente se le asigna por primera vez un punto de actualización de software, permanecerá asignado a dicho punto de actualización de software a no ser que no pueda explorar para detectar las actualizaciones de software en dicho punto de actualización.  

 La exploración para la detección de actualizaciones de software puede producir un error con un número diferente de códigos de error de reintentos y de no reintentos. Cuando la exploración produce un código de error de reintento, el cliente inicia un proceso de reintento para explorar las actualizaciones de software en el punto de actualización de software. Las condiciones de alto nivel que dan como resultado un código de error de reintento suelen producirse porque el servidor de WSUS no está disponible o porque está temporalmente sobrecargado. El cliente utiliza el siguiente proceso cuando se produce un error al explorar para detectar actualizaciones de software:  

1.  El cliente explora para detectar actualizaciones de software a la hora programada, o cuando se inicia a través del panel de control en el cliente, o mediante el SDK. Si se produce un error en la exploración, el cliente espera 30 minutos para reintentarla, y utiliza el mismo punto de actualización de software.  

2.  El cliente lo reintenta un mínimo de cuatro veces en intervalos de 30 minutos. Después del cuarto error, y tras esperar otros dos minutos, el cliente pasará al siguiente punto de actualización de software de la lista de puntos de actualización de software.  

3.  Después de una exploración correcta, el cliente se conectará con el punto de actualización de software.  

 En la lista siguiente se ofrece información adicional que puede tener en cuenta en los escenarios de cambio y reintento de puntos de actualización de software:  

-   Si un cliente se desconecta de la intranet corporativa y no puede explorar para detectar actualizaciones de software, no se cambiará a otro punto de actualización de software. Es un error esperado, dado que el cliente no puede conectarse a la red corporativa ni al punto de actualización de software que permite la conexión desde la intranet. El cliente de Configuration Manager determina la disponibilidad del punto de actualización de software de la intranet.  

-   Si está habilitada la administración del cliente basada en Internet, y hay varios puntos de actualización de software que están configurados para aceptar la comunicación de clientes en Internet, el proceso de cambio seguirá el proceso de reintento estándar descrito en el escenario anterior.  

-   Si se inició el proceso de exploración pero el cliente se desconectó antes de completarse la exploración, no se considera un error, y no cuenta como uno de los cuatro reintentos.  

###  <a name="a-namebkmkmanuallyswitchsupsamanually-switch-clients-to-a-new-software-update-point"></a><a name="BKMK_ManuallySwitchSUPs"></a> Cambio manual de clientes a un nuevo punto de actualización de software
A partir de la versión 1606 de Configuración Manager, puede habilitar la opción para que los clientes de Configuration Manager cambien a un nuevo punto de actualización de software cuando hay problemas con el punto de actualización de software activo. Esta opción genera cambios solo cuando un cliente recibe varios puntos de actualización de software desde un punto de administración.  

Habilite esta opción en una recopilación de dispositivos o en un conjunto de dispositivos seleccionados. Una vez habilitada, los clientes buscarán otro punto de actualización de software en el siguiente examen. En función de las opciones de configuración de WSUS (clasificaciones de actualizaciones, productos, si los puntos de actualización de software comparten una base de datos WSUS, etc.), el cambio a un nuevo punto de actualización de software generará tráfico de red adicional. Por lo tanto, solo se debe utilizar esta opción cuando sea necesario.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Para habilitar la opción de cambiar los puntos de actualización de software  

1.  En la consola de Configuration Manager, vaya a **Activos y compatibilidad > Información general > Recopilaciones de dispositivos**.  

2.  En la pestaña **Inicio** del grupo **Recopilación** , haga clic en **Notificación de cliente**y luego en **Cambiar al siguiente punto de actualización de software**.  


###  <a name="a-namebkmksupcrossforesta-software-update-points-in-an-untrusted-forest"></a><a name="BKMK_SUP_CrossForest"></a> Puntos de actualización de software en un bosque que no es de confianza  
 Puede crear uno o varios puntos de actualización de software en un sitio para admitir a clientes de un bosque que no es de confianza. Para agregar un punto de actualización de software en otro bosque, primero debe instalar y configurar un servidor de WSUS en el bosque. Después, inicie el asistente para agregar un servidor de sitio de Configuration Manager con el rol de sistema de sitio del punto de actualización de software. En el asistente, configure las siguientes opciones para conectarse correctamente a WSUS en el bosque que no es de confianza:  

-   Especifique una cuenta de instalación del sistema de sitio que pueda acceder al servidor WSUS en el bosque.  

-   Especifique la cuenta de conexión del servidor WSUS que se va a utilizar para conectarse al servidor WSUS.  

 Por ejemplo, tiene un sitio primario en el bosque A con dos puntos de actualización de software (SUP01 y SUP02). Además, para el mismo sitio primario tiene dos puntos de actualización de software (SUP03 y SUP04) en el bosque B. Cuando se produce el cambio en este ejemplo, tienen prioridad los puntos de actualización de software del mismo bosque que el cliente.  

###  <a name="a-namebkmkwsussyncsourcea-use-an-existing-wsus-server-as-the-synchronization-source-at-the-top-level-site"></a><a name="BKMK_WSUSSyncSource"></a> Usar servidor WSUS existente como origen de la sincronización en el sitio de nivel superior  
 Normalmente, el sitio de nivel superior de la jerarquía está configurado para sincronizar los metadatos de las actualizaciones de software con Microsoft Update. Si su directiva de seguridad corporativa no permite acceder a Internet desde el sitio de nivel superior, puede configurar el origen de la sincronización del sitio de nivel superior para usar un servidor WSUS existente que no esté en su jerarquía de Configuration Manager. Por ejemplo, podría tener un servidor WSUS instalado en su red perimetral que tiene acceso a Internet, a diferencia del sitio de nivel superior. Puede configurar el servidor WSUS de la red perimetral como origen de la sincronización para los metadatos de las actualizaciones de software. Debe asegurarse de que el servidor WSUS de la red perimetral sincroniza las actualizaciones de software que cumplen los criterios necesarios de la jerarquía de Configuration Manager. De lo contrario, es posible que el sitio de nivel superior no sincronice las actualizaciones de software previstas. Al instalar el punto de actualización de software, configure una cuenta de conexión de WSUS que tenga acceso al servidor WSUS de la red perimetral y asegúrese de que el firewall permite el tráfico en los puertos correspondientes. Para obtener más información, consulte [los puertos que usa el punto de actualización de software para el origen de la sincronización](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS).  

###  <a name="a-namebkmknlbsupsp1a-software-update-point-configured-to-use-an-nlb"></a><a name="BKMK_NLBSUPSP1"></a> Punto de actualización de software configurado para usar NLB  
 El cambio del punto de actualización de software satisfará probablemente sus necesidades de tolerancia a errores. Sin embargo, el NLB es más estable que la conmutación por error de punto de actualización de software en cuanto al equilibrio de carga puro, y además puede aumentar la confiabilidad y el rendimiento de una red. Aunque la consola de Configuration Manager no incluye ninguna opción para configurar el punto de actualización de software para usar NLB, existe la opción de configurar NLB mediante el cmdlet Set-CMSoftwareUpdatePoint de PowerShell. Para obtener más información sobre el cmdlet Set-CMSoftwareUpdatePoint de PowerShell, consulte [Set-CMSoftwareUpdatePoint](http://go.microsoft.com/fwlink/?LinkId=276834).

###  <a name="a-namebkmksupsecsitea-software-update-point-on-a-secondary-site"></a><a name="BKMK_SUPSecSite"></a> Punto de actualización de software en un sitio secundario  
 El punto de actualización de software es opcional en un sitio secundario. Cuando se instala un punto de actualización de software en un sitio secundario, la base de datos de WSUS se configura como una réplica del punto de actualización de software predeterminado del sitio primario principal. Solo se puede instalar un punto de actualización de software en un sitio secundario. Los dispositivos asignados a un sitio secundario se configuran para utilizar un punto de actualización de software del sitio primario cuando no hay un punto de actualización de software instalado en el sitio secundario. Se suele instalar un punto de actualización de software en un sitio secundario cuando el ancho de banda de red es limitado entre los dispositivos asignados al sitio secundario y los puntos de actualización de software del sitio primario principal, o cuando el punto de actualización de software se acerca al límite de su capacidad. Una vez que un punto de actualización de software está correctamente instalado y configurado en el sitio secundario, se actualiza una directiva para todo el sitio para los equipos cliente asignados al sitio, que empezarán a utilizar el nuevo punto de actualización de software.  

##  <a name="a-namebkmksupinstallationa-plan-for-software-update-point-installation"></a><a name="BKMK_SUPInstallation"></a> Planeamiento de la instalación de puntos de actualización de software  
 Antes de crear un rol de sistema de sitio de punto de actualización de software en Configuration Manager, se deben tener en cuenta varios requisitos en función de la infraestructura de Configuration Manager. Cuando configure el punto de actualización de software para la comunicación mediante SSL, es especialmente importante que consulte esta sección, ya que debe seguir unos pasos adicionales para que los puntos de actualización de software de la jerarquía funcionen correctamente. Esta sección proporciona información acerca de los pasos que debe seguir para planear y preparar correctamente la instalación de los puntos de actualización de software.  

###  <a name="a-namebkmksupsystemrequirementsa-requirements-for-the-software-update-point"></a><a name="BKMK_SUPSystemRequirements"></a> Requisitos del punto de actualización de software  
 El rol de sistema de sitio de punto de actualización de software se debe instalar en un sistema de sitio que cumpla los requisitos mínimos de WSUS y las configuraciones compatibles con Configuration Manager.  

-   Para obtener más información sobre los requisitos mínimos para el rol de servidor WSUS en Windows Server 2012, consulte [Revisar consideraciones iniciales y requisitos del sistema](https://technet.microsoft.com/library/hh852344.aspx#BKMK_1.1) en la biblioteca de documentación de Windows Server 2012.  

-   Para más información sobre las configuraciones admitidas para los sistemas de sitio de Configuration Manager, consulte [Requisitos previos del sitio y el sistema de sitio](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

###  <a name="a-namebkmkplanningforwsusa-plan-for-wsus-installation"></a><a name="BKMK_PlanningForWSUS"></a> Planear la instalación de WSUS  
 Las actualizaciones de software requieren que haya una versión compatible de WSUS instalada en todos los servidores de sistema de sitio configurados para el rol de sistema de sitio de punto de actualización de software. Además, si no instala el punto de actualización de software en el servidor de sitio, debe instalar la consola de administración de WSUS en el equipo del servidor de sitio, si no está instalada ya. Esto permite que el servidor de sitio se comunique con el WSUS que se ejecuta en el punto de actualización de software.  

 Cuando se usa WSUS en Windows Server 2012, se deben configurar permisos adicionales para permitir que el **administrador de configuración de WSUS** de Configuration Manager se conecte a WSUS para realizar comprobaciones de estado periódicas. Elija una de las siguientes opciones para configurar los permisos:  

-   Agregar la cuenta **SYSTEM** al grupo **Administradores de WSUS**  

-   Agregar la cuenta **NT AUTHORITY\SYSTEM** como usuario de la base de datos de WSUS (SUSDB) y configurar un valor mínimo de la pertenencia al rol de base de datos de servicio web  

 Para obtener más información acerca de cómo instalar WSUS en Windows Server 2012, consulte [Paso 2: instalar el rol de servidor de WSUS](http://go.microsoft.com/fwlink/p/?LinkId=272355) en la biblioteca de documentación de Windows Server 2012.  

 Cuando instale más de un punto de actualización de software en un sitio primario, utilice la misma base de datos de WSUS para cada punto de actualización de software del mismo bosque de Active Directory. Si se comparte la misma base de datos, se mitiga significativamente (aunque no se elimina por completo) el impacto sobre el rendimiento de la red y el cliente que podría experimentarse cuando los clientes cambian a un nuevo punto de actualización de software. Cuando un cliente cambia a un nuevo punto de actualización de software que comparte una base de datos con el punto de actualización de software anterior, se sigue produciendo un examen de diferencias, pero es mucho menor que si el servidor WSUS tuviera su propia base de datos.  

####  <a name="a-namebkmkcustomwebsitea-configure-wsus-to-use-a-custom-web-site"></a><a name="BKMK_CustomWebSite"></a> Configurar WSUS para usar un sitio web personalizado  
 Al instalar WSUS, tiene la opción de utilizar el sitio web de IIS predeterminado existente o crear un sitio web de WSUS personalizado. Cree un sitio web personalizado para WSUS para que IIS hospede los servicios WSUS en un sitio web virtual dedicado en vez de compartir el sitio web que también usan otros sistemas de sitio de Configuration Manager u otras aplicaciones. Esto se recomienda especialmente cuando se instala el rol de sistema de sitio de punto de actualización de software en el servidor de sitio. Cuando se ejecuta WSUS en Windows Server 2012, WSUS se configura de forma predeterminada para usar el puerto 8530 para HTTP y el puerto 8531 para HTTPS. Se debe especificar esta configuración de puertos al crear el punto de actualización de software en un sitio.  

####  <a name="a-namebkmkwsusinfrastructurea-use-an-existing-wsus-infrastructure"></a><a name="BKMK_WSUSInfrastructure"></a> Usar una infraestructura de WSUS existente  
 Puede utilizar un servidor WSUS que estuviera activo en su entorno antes de instalar Configuration Manager. Cuando se configura el punto de actualización de software, debe especificar la configuración de sincronización. Configuration Manager se conecta con el WSUS que se ejecuta en el punto de actualización de software y configura el servidor WSUS con la misma configuración. Si el servidor WSUS se sincronizó anteriormente con productos o clasificaciones que no se configuraron como parte de la configuración de sincronización del punto de actualización de software, los metadatos de las actualizaciones de software de los productos y clasificaciones se sincronizan para todos los metadatos de las actualizaciones de software de la base de datos de WSUS independientemente de la configuración de sincronización del punto de actualización de software. Esto podría tener como consecuencia unos metadatos de las actualizaciones de software inesperados en la base de datos del sitio. Experimentará el mismo comportamiento si agrega productos o clasificaciones directamente en la consola de administración de WSUS y, a continuación, inicia inmediatamente la sincronización. Cada hora, de forma predeterminada, Configuration Manager se conecta al WSUS que se ejecuta en el punto de actualización de software y restablece las opciones que se modificaron fuera de Configuration Manager.  

 Las actualizaciones de software que no cumplan con los productos y las clasificaciones especificados en la configuración de sincronización se establecen como expiradas y, luego, se quitan de la base de datos del sitio.  

####  <a name="a-namebkmkwsusasreplicaa-configure-wsus-as-a-replica-server"></a><a name="BKMK_WSUSAsReplica"></a> Configurar WSUS como un servidor de réplica  
 Cuando se crea un rol de sistema de sitio de punto de actualización de software en un servidor de sitio primario, no se puede utilizar un servidor WSUS que esté configurado como una réplica. Cuando el servidor WSUS está configurado como una réplica, Configuration Manager no puede configurar el servidor WSUS, y la sincronización de WSUS tampoco se puede llevar a cabo. Cuando se crea un punto de actualización de software en un sitio secundario, Configuration Manager configura WSUS para que sea un servidor de réplica del WSUS que se ejecuta en el punto de actualización de software del sitio primario principal. El primer punto de actualización de software que se instala en un sitio primario es el punto de actualización de software predeterminado. Los puntos de actualización de software adicionales del sitio se configuran como réplicas del punto de actualización de software predeterminado.  

####  <a name="a-namebkmkwsusandssla-decide-whether-to-configure-wsus-to-use-ssl"></a><a name="BKMK_WSUSandSSL"></a> Decidir si se va a configurar WSUS para usar SSL  
 Puede utilizar el protocolo SSL para proteger el WSUS que se ejecuta en el punto de actualización de software. WSUS utiliza SSL para autenticar en el servidor WSUS los equipos cliente y los servidores WSUS que siguen en la cadena. WSUS también utiliza SSL para cifrar los metadatos de las actualizaciones de software. Si decide proteger WSUS con SSL, debe preparar el servidor WSUS antes de instalar el punto de actualización de software.  

 Cuando instala y configura el punto de actualización de software, debe seleccionar la opción **Habilitar las comunicaciones SSL para el servidor WSUS** . De lo contrario, Configuration Manager configurará WSUS para que no use SSL. Cuando habilita SSL para un WSUS que se ejecuta en un punto de actualización de software, el WSUS que se ejecute en el punto de actualización de software de cualquier sitio secundario también se debe configurar para utilizar SSL.  

###  <a name="a-namebkmkconfigurefirewallsa-configure-firewalls"></a><a name="BKMK_ConfigureFirewalls"></a> Configurar firewalls  
 Las actualizaciones de software de un sitio de administración central de Configuration Manager se comunican con el WSUS que se ejecuta en el punto de actualización de software, que a su vez se comunica con el origen de la sincronización para sincronizar los metadatos de las actualizaciones de software. Los puntos de actualización de software de un sitio secundario se comunican con el punto de actualización de software del sitio primario. Cuando hay más de un punto de actualización de software en un sitio primario, los puntos de actualización de software adicionales se deben comunicar con el primer punto de actualización de software instalado en el sitio, que es el punto de actualización de software predeterminado.  

 Puede que el firewall deba configurarse para aceptar los puertos HTTP o HTTPS que usa WSUS en los siguientes escenarios: cuando hay un firewall corporativo entre el punto de actualización de software de Configuration Manager e Internet; cuando hay un punto de actualización de software y su origen de sincronización ascendente; o cuando hay puntos de actualización de software adicionales. La conexión a Microsoft Update siempre está configurada para utilizar el puerto 80 para HTTP y el puerto 443 para HTTPS. Se puede utilizar un puerto personalizado para la conexión del WSUS que se ejecuta en el punto de actualización de software de un sitio secundario al WSUS que se ejecuta en el punto de actualización de software del sitio primario. Si la directiva de seguridad no permite la conexión, se debe usar el método de sincronización de exportación e importación. Para más información, consulte la sección [Origen de la sincronización](#BKMK_SyncSource) en este tema. Para obtener más información sobre los puertos usados por WSUS, consulte [Cómo determinar la configuración del puerto usada por WSUS](../get-started/install-a-software-update-point.md#wsus-settings).  

#### <a name="restrict-access-to-specific-domains"></a>Restringir el acceso a dominios específicos  
 Si su organización no permite que los puertos y protocolos estén abiertos a todas las direcciones del firewall entre el punto de actualización de software activo e Internet, puede restringir el acceso a los siguientes dominios para que WSUS y Actualizaciones automáticas se puedan comunicar con Microsoft Update:  

-   http://windowsupdate.microsoft.com

-   http://*.windowsupdate.microsoft.com  

-   https://*.windowsupdate.microsoft.com  

-   http://*.update.microsoft.com  

-   https://*.update.microsoft.com  

-   http://*.windowsupdate.com  

-   http://download.windowsupdate.com  

-   http://download.microsoft.com  

-   http://*.download.windowsupdate.com  

-   http://test.stats.update.microsoft.com  

-   http://ntservicepack.microsoft.com  

 Tendrá que agregar las siguientes direcciones al firewall que se encuentra entre los dos sistemas de sitio en los siguientes casos: si los sitios secundarios tienen un punto de actualización de software de punto o si hay un punto de actualización de software basado en Internet activo remoto en un sitio:  

 **Punto de actualización de software del sitio secundario**  

-   http://<*FQDN del punto de actualización de software del sitio secundario*>  

-   https://<*FQDN del punto de actualización de software del sitio secundario*>  

-   http://<*FQDN del punto de actualización de software del sitio primario*>  

-   https://<*FQDN del punto de actualización de software del sitio primario*>  

##  <a name="a-namebkmksyncsettingsa-plan-for-synchronization-settings"></a><a name="BKMK_SyncSettings"></a> Planear la configuración de sincronización  
 La sincronización de las actualizaciones de software de Configuration Manager es el proceso de recuperación de los metadatos de las actualizaciones de software en función de los criterios que se configuren. El sitio de nivel superior de la jerarquía, el sitio de administración central o un sitio primario independiente sincroniza las actualizaciones de software de Microsoft Update. Tiene la opción de configurar el punto de actualización de software en el sitio de nivel superior para la sincronización con un servidor WSUS existente, no en la jerarquía de Configuration Manager. Los sitios primarios secundarios sincronizan los metadatos de las actualizaciones de software desde el punto de actualización de software del sitio de administración central. Antes de instalar y configurar un punto de actualización de software, utilice esta sección para planear la configuración de sincronización.  

###  <a name="a-namebkmksyncsourcea-synchronization-source"></a><a name="BKMK_SyncSource"></a> Origen de la sincronización  
 En la configuración del origen de la sincronización del punto de actualización de software se especifica la ubicación desde la cual el punto de actualización de software recupera los metadatos de las actualizaciones de software; asimismo, se especifica si se crean eventos de informe de WSUS durante el proceso de sincronización.  

-   **Origen de sincronización** : el punto de actualización de software del sitio de nivel superior configura el origen de sincronización como Microsoft Update de forma predeterminada. Tiene la opción de sincronizar el sitio de nivel superior con un servidor WSUS existente. El punto de actualización de software de un sitio primario secundario configura el origen de la sincronización como el punto de actualización de software del sitio de administración central de forma predeterminada.  

    > [!NOTE]  
    >  El primer punto de actualización de software que se instala en un sitio primario, que es el punto de actualización de software predeterminado, se sincroniza con el sitio de administración central. Los puntos de actualización de software adicionales del sitio primario se sincronizan con el punto de actualización de software predeterminado del sitio primario.  

     Cuando un punto de actualización de software se desconecta de Microsoft Update o del servidor de actualización que precede en la cadena, se puede configurar el origen de la sincronización de manera que no se realice la sincronización con un origen de la sincronización configurado, sino que en su lugar se utilice la función de exportación e importación de la herramienta WSUSUtil para sincronizar las actualizaciones de software. Para obtener más información, consulte [Sincronizar actualizaciones de software desde un punto de actualización de software desconectado](../get-started/synchronize-software-updates-disconnected.md).  

-   **Eventos de informe de WSUS:** El Agente de Windows Update de los equipos cliente puede crear mensajes de evento que se utilizan para la generación de informes de WSUS. La actualización de software de Configuration Manager no usa estos eventos y, por tanto, la opción **No crear eventos de informe de WSUS** se selecciona de forma predeterminada. Cuando no se crean estos eventos, el único momento en que el equipo cliente se debe conectar al servidor WSUS es durante los exámenes de cumplimiento y de evaluación de las actualizaciones de software. Si se necesitan estos eventos para la generación de informes fuera de las actualizaciones de software de Configuration Manager, será necesario modificar esta configuración para crear eventos de informe de WSUS.  

###  <a name="a-namebkmksyncschedulea-synchronization-schedule"></a><a name="BKMK_SyncSchedule"></a> Programación de la sincronización  
 Solo se puede configurar la programación de sincronización en el punto de actualización de software del sitio de nivel superior de la jerarquía de Configuration Manager. Cuando se configura la programación de sincronización, el punto de actualización de software se sincroniza con el origen de la sincronización en la fecha y a la hora especificadas. La programación personalizada permite sincronizar las actualizaciones de software en un momento en que la demanda del servidor WSUS, el servidor de sitio y la red sea baja, como por ejemplo a las 02:00 una vez a la semana. Como alternativa, se puede iniciar la sincronización en el sitio de nivel superior mediante la acción **Sincronizar actualizaciones de software** del nodo **Todas las actualizaciones de software** o **Grupos de actualizaciones de software** de la consola de Configuration Manager.  

> [!TIP]  
>  Programe la sincronización de las actualizaciones de software para que se ejecuten en un intervalo de tiempo adecuado para su entorno. Un escenario habitual es configurar la programación de la sincronización de las actualizaciones de software para que se ejecute poco tiempo después del lanzamiento de las actualizaciones de seguridad periódicas de Microsoft los segundos martes de cada mes, lo que normalmente se conoce como "Patch Tuesday". Otro escenario típico es configurar la programación de la sincronización de las actualizaciones de software para que se ejecute diariamente cuando se usen actualizaciones de software para suministrar actualizaciones de motor y de definiciones de Endpoint Protection.  

 Una vez que el punto de actualización de software finaliza la sincronización correctamente, se envía una solicitud de sincronización a los sitios secundarios. Si tiene puntos de actualización de software adicionales en un sitio primario, se envía una solicitud de sincronización a cada punto de actualización de software. El proceso se repite en cada sitio de la jerarquía.  

###  <a name="a-namebkmkupdateclassificationsa-update-classifications"></a><a name="BKMK_UpdateClassifications"></a> Clasificaciones de actualizaciones  
 Cada actualización de software se define con una clasificación de actualización que facilita la organización de los distintos tipos de actualizaciones. Durante el proceso de sincronización, se sincronizarán los metadatos de las actualizaciones de software para las clasificaciones especificadas. Configuration Manager permite sincronizar las actualizaciones de software con las siguientes clasificaciones de actualización:  

-   **Actualizaciones críticas:** Especifica una actualización de amplia distribución para un problema específico que resuelve un error crítico no relacionado con la seguridad.  

-   **Actualizaciones de definiciones:** Especifica una actualización para un archivo de definición de virus u otros archivos de definición.  

-   **Paquetes de características:** Especifica las nuevas características del producto que se distribuyen fuera de un lanzamiento de producto y las características que normalmente se incluyen en el siguiente lanzamiento de producto completo.  

-   **Actualizaciones de seguridad** Especifica una actualización de amplia distribución para un problema específico del producto, relacionado con la seguridad.  

-   **Service Packs:** Especifica un conjunto acumulativo de revisiones correspondientes a una aplicación. Estas revisiones pueden incluir actualizaciones de seguridad, actualizaciones críticas, actualizaciones de software, etc.  

-   **Herramientas:** Especifica una utilidad o característica que ayuda a realizar una o más tareas.  

-   **Paquetes acumulativos de revisiones:** Especifica un conjunto acumulativo de revisiones que se recopilan para facilitar la implementación. Estas revisiones pueden incluir actualizaciones de seguridad, actualizaciones críticas, actualizaciones, etc. Un paquete acumulativo de revisiones suele relacionarse, por lo general, con un área específica; por ejemplo, un componente del producto o de la seguridad.  

-   **Actualizaciones:** Especifica una actualización para una aplicación o un archivo actualmente instalado.  

 Las clasificaciones de actualizaciones se configuran solo en el sitio de nivel superior. Las clasificaciones de actualizaciones no se configuran en el punto de actualización de software de los sitios secundarios, porque los metadatos de las actualizaciones de software se replican desde el sitio de nivel superior en los sitios primarios secundarios. Al seleccionar las clasificaciones de actualizaciones, tenga en cuenta que cuantas más clasificaciones seleccione, más tiempo tardará la sincronización de los metadatos de las actualizaciones de software.  

> [!WARNING]  
>  Como práctica recomendada, desactive todas las clasificaciones antes de sincronizar las actualizaciones de software por primera vez. Después de la sincronización inicial, seleccione las clasificaciones en Propiedades de componente de punto de actualización de software y, a continuación, vuelva a iniciar la sincronización.  

###  <a name="a-namebkmkupdateproductsa-products"></a><a name="BKMK_UpdateProducts"></a> Productos  
 Los metadatos de cada actualización de software definen uno o varios productos a los que corresponde la actualización. Un producto es una edición específica de una aplicación o un sistema operativo. Un ejemplo de un producto es Microsoft Windows Server 2008. Una familia de productos es el sistema operativo o la aplicación de base de los cuales se derivan los productos individuales. Un ejemplo de una familia de productos es Microsoft Windows, de la que Microsoft Windows Server 2008 es miembro. Puede especificar una familia de productos o productos individuales dentro de una familia de productos.  

 Cuando se aplican las actualizaciones de software a varios productos y, al menos, uno de ellos se selecciona para sincronización, todos los productos aparecerán en la consola de Configuration Manager aunque no se seleccionen algunos productos. Por ejemplo, si Windows Server 2012 es el único sistema operativo al que está suscrito y se aplica una actualización de software a Windows Server 2012 y a Windows Server 2012 Datacenter Edition, ambos productos se encontrarán en la base de datos del sitio.  

 Las opciones del producto solo se configuran en el sitio de nivel superior. Las opciones del producto no se configuran en el punto de actualización de software para los sitios secundarios, porque los metadatos de las actualizaciones de software se replican desde el sitio de nivel superior en los sitios primarios secundarios. Al seleccionar los productos, tenga en cuenta que cuanto más productos seleccione, más tiempo tardarán en sincronizarse los metadatos de las actualizaciones de software.  

> [!IMPORTANT]  
>  Configuration Manager almacena una lista de productos y familias de productos entre los que puede elegir cuando instala por primera vez el punto de actualización de software. Es posible que los productos y las familias de productos lanzados después del lanzamiento de Configuration Manager no estén disponibles para seleccionar hasta que se complete la sincronización de las actualizaciones de software, lo cual actualiza la lista de productos y familias de productos disponibles para seleccionar. Como práctica recomendada, desactive todos los productos antes de sincronizar por primera vez las actualizaciones de software. Después de la sincronización inicial, seleccione los productos en Propiedades de componente de punto de actualización de software y, a continuación, vuelva a iniciar la sincronización.  

###  <a name="a-namebkmksupersedencerulesasupersedence-rules"></a><a name="BKMK_SupersedenceRules"></a> Reglas de sustitución  
 Por lo general, una actualización de software que sustituye a otra actualización de software realiza una o varias de las siguientes acciones:  

-   Mejora o actualiza la revisión proporcionada por una o varias de las actualizaciones publicadas anteriormente.  

-   Mejora la eficacia del paquete de archivos de actualización sustituidos, que se instala en los equipos cliente si se aprueba la actualización para la instalación. Por ejemplo, la actualización sustituida podría contener archivos que ya no son relevantes para la revisión o para los sistemas operativos que se admiten en la nueva actualización; por tanto, esos archivos ya no se incluyen en el paquete de archivos de sustitución de la actualización.  

-   Actualiza las versiones más recientes de un producto. En otras palabras, actualiza las versiones que ya no se aplican a las versiones o configuraciones más antiguas de un producto. Las actualizaciones también pueden sustituir a otras actualizaciones si se han realizado modificaciones para ampliar la compatibilidad de idioma. Por ejemplo, una revisión posterior de una actualización de un producto para Microsoft Office puede quitar la compatibilidad para un sistema operativo más antiguo, pero podría agregar compatibilidad adicional para nuevos idiomas en la versión de actualización inicial.  

 En las propiedades del punto de actualización de software, es posible especificar que las actualizaciones de software reemplazadas expiren inmediatamente, lo que evita que se incluyan en implementaciones nuevas, además de marcar las implementaciones existentes para que indiquen que contienen una o varias actualizaciones de software expiradas. Igualmente, es posible especificar un período de tiempo antes de que las actualizaciones de software sustituidas expiren, lo que le permite continuar con las implementaciones. Tenga en cuenta los siguientes escenarios en los que puede que necesite implementar una actualización de software sustituida:  

-   Si una actualización de un software de sustitución solo es compatible con las versiones más recientes de un sistema operativo y algunos de los equipos cliente ejecutan versiones anteriores del sistema operativo.  

-   Si una actualización de software de sustitución tiene una aplicabilidad más restringida que la actualización de software que reemplaza. Esto la haría inapropiada para algunos equipos cliente.  

-   Si una actualización de software de sustitución no se aprobó para su implementación en el entorno de producción.  

###  <a name="a-namebkmkupdatelanguagesa-languages"></a><a name="BKMK_UpdateLanguages"></a> Idiomas  
 La configuración de idioma para el punto de actualización de software permite configurar los idiomas en los que se sincronizan los detalles de resumen (metadatos de actualizaciones de software) para las actualizaciones de software, así como los idiomas de los archivos de actualización de software que se descargarán para las actualizaciones de software.  

#### <a name="software-update-file"></a>Archivo de actualización de software  
 Los idiomas que configura para la opción **Archivo de actualización de software** en las propiedades del punto de actualización de software proporcionan el conjunto predeterminado de los idiomas disponibles cuando carga las actualizaciones de software en un sitio. Puede modificar los idiomas seleccionados de manera predeterminada cada vez que se van a descargar o implementar las actualizaciones de software. Durante el proceso de descarga, los archivos de actualización de software para los idiomas configurados se descargan en la ubicación de origen del paquete de implementación, si los archivos de actualización de software están disponibles en el idioma seleccionado. Después se copian en la biblioteca de contenido del servidor del sitio y, a continuación, se copian en los puntos de distribución que están configurados para el paquete.  

 La opción de idioma del archivo de configuración de software debe configurarse con los idiomas que se utilizan con más frecuencia en el entorno. Por ejemplo, si los equipos cliente que están asignados al sitio utilizan con más frecuencia los idiomas inglés y japonés para el sistema operativo o para las aplicaciones, y apenas se utilizan otros idiomas en el sitio, seleccione, en este caso, los idiomas inglés y japonés en la columna **Archivo de actualización de software** cuando descargue o implemente la actualización de software, y desactive el resto de idiomas. Esto le permite utilizar la configuración predeterminada en la página **Selección de idioma** de la implementación y descargar asistentes. De esta forma también se impide la descarga de archivos de actualización no necesarios. Esta opción se configura en cada punto de actualización de software de la jerarquía de Configuration Manager.  

#### <a name="summary-details"></a>Detalles de resumen  
 Durante el proceso de sincronización, se actualiza la información de detalles de resumen (metadatos de las actualizaciones de software) para buscar actualizaciones de software en los idiomas especificados. Los metadatos ofrecen información sobre la actualización de software, como nombre, descripción, productos compatibles con la actualización, clasificación de actualizaciones, identificador de artículo, dirección URL de descarga y reglas de aplicación, entre otras.  

 Las opciones de los detalles de resumen solo se configuran en el sitio de nivel superior. Los detalles de resumen no se configuran en el punto de actualización de software en los sitios secundarios porque los metadatos de actualizaciones de software se replican desde el sitio de administración central a estos sitios mediante una replicación basada en archivos. Al seleccionar los idiomas de los detalles de resumen, seleccione solo los idiomas que necesita en el entorno. Cuantos más idiomas seleccione, más tiempo tomará sincronizar los metadatos de las actualizaciones de software. Configuration Manager muestra los metadatos de las actualizaciones de software en la configuración regional del sistema operativo en el que se ejecuta la consola de Configuration Manager. Si las propiedades localizadas de las actualizaciones de software no están disponibles en la configuración regional del sistema operativo, la información de las actualizaciones de software se muestra en inglés.  

> [!IMPORTANT]  
>  Es importante que seleccione todos los idiomas de los detalles de resumen que necesita en la jerarquía de Configuration Manager. Cuando el punto de actualización de software del sitio de nivel superior se sincroniza con el origen de la sincronización, los idiomas de los detalles de resumen seleccionados determinan los metadatos de las actualizaciones de software recuperados. Si modifica los idiomas de los detalles de resumen después de que la sincronización se haya ejecutado al menos una vez, los metadatos de las actualizaciones de software se recuperan para los idiomas de los detalles de resumen modificados solo para las actualizaciones de software nuevas o actualizadas. Las actualizaciones de software ya sincronizadas no se actualizan con los nuevos metadatos en los idiomas modificados, salvo que se produzca un cambio en la actualización de software en el origen de la sincronización.  

##  <a name="a-namebkmkmaintenancewindowa-plan-for-a-software-updates-maintenance-window"></a><a name="BKMK_MaintenanceWindow"></a> Planear una ventana de mantenimiento de actualizaciones de software  
 Puede agregar una ventana de mantenimiento dedicada para la instalación de actualizaciones de software. Esto le permite configurar una ventana de mantenimiento general y una ventana de mantenimiento diferente para las actualizaciones de software. Cuando se configuran una ventana de mantenimiento general y una ventana de mantenimiento de actualizaciones de software, los clientes solo instalan las actualizaciones de software durante la ventana de mantenimiento de actualizaciones de software. Para obtener más información sobre las ventanas de mantenimiento, vea [Cómo usar las ventanas de mantenimiento](../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="a-namebkmkrestartoptionsa-restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> Opciones de reinicio para clientes de Windows 10 después de la instalación de las actualizaciones de software
Cuando se implementa y se instala en un equipo una actualización de software que requiere un reinicio con Configuration Manager, se programa un reinicio pendiente y se muestra un cuadro de diálogo de reinicio.

A partir de la versión 1606 de Configuration Manager, la opción para **Actualizar y reiniciar**, y **Actualizar y apagar** está disponible en los equipos de Windows 10 en las opciones de energía de Windows siempre que haya un reinicio pendiente para una actualización de software de Configuration Manager. Después de utilizar una de estas opciones, tras reiniciar el equipo, no se mostrará el cuadro de diálogo de reinicio.

En versiones anteriores de Configuration Manager, cuando había un reinicio pendiente para equipos Windows 8 y posteriores, y al apagar o reiniciar el equipo con las opciones de energía de Windows (en lugar de desde el cuadro de diálogo de reinicio), este cuadro de diálogo seguía apareciendo después de reiniciar el equipo que tenía que reiniciarse en la fecha límite configurada.

## <a name="next-steps"></a>Pasos siguientes
Cuando haya planificado las actualizaciones de software, consulte [Preparación para la administración de actualizaciones de software](../get-started/prepare-for-software-updates-management.md).



<!--HONumber=Nov16_HO1-->


