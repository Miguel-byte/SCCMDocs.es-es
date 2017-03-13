---
title: "Aspectos básicos de la administración de contenido | Microsoft Docs"
description: Use herramientas y opciones en System Center Configuration Manager para administrar el contenido que implemente.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
caps.latest.revision: 28
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 83020f532edd7a640f0087aad40789e026f75913
ms.openlocfilehash: 00751cd03a3dd49718994e31bc396e4e7d29ed2b
ms.lasthandoff: 02/28/2017


---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>Conceptos básicos de la administración de contenido en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

System Center Configuration Manager admite un sistema eficaz de herramientas y opciones para administrar el contenido que se implementa, como aplicaciones, paquetes, actualizaciones de software e implementaciones de sistema operativo.  

 El contenido que se implementa se almacena en los servidores de sitio y en los servidores de sistema de sitio de punto de distribución. Este contenido puede requerir una gran cantidad de ancho de banda de red cuando se transfiere entre ubicaciones. Para planear y usar eficazmente la infraestructura de administración de contenido, se recomienda que conozca las opciones y configuraciones disponibles, y que considere cómo usarlas para adaptarse mejor a su entorno de red y a sus necesidades de implementación de contenido.  

A continuación se indican los conceptos básicos de la administración de contenido. Cuando un concepto requiere información adicional o compleja, se proporcionan vínculos para dirigirle a ella.  

## <a name="accounts-used-for-content-management"></a>Cuentas usadas para la administración de contenido  
 Las cuentas siguientes pueden usarse con la administración de contenido:  

-   **Cuenta de acceso a la red**: la usan los clientes para conectarse a un punto de distribución y tener acceso al contenido. De forma predeterminada, se intenta usar en primer lugar la cuenta de equipo.  

     Esta cuenta también la usan los puntos de distribución de extracción para obtener el contenido de un punto de distribución de origen en un bosque remoto.  

-   **Cuenta de acceso de paquete**: de forma predeterminada, Configuration Manager concede acceso al contenido en un punto de distribución a los usuarios y los administradores de cuentas de acceso genéricas. Sin embargo, puede configurar permisos adicionales para restringir el acceso.   

-   **Cuenta de conexión de multidifusión**: se usa para implementaciones de sistema operativo.  

Para obtener más información sobre estas cuentas, consulte [Administración de cuentas para acceder al contenido](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).

## <a name="bandwidth-throttling-and-scheduling"></a>Programación y límite de ancho de banda  
 La programación y el límite son opciones que le ayudan a controlar cuándo se distribuye el contenido de un servidor de sitio en puntos de distribución. Esto es similar a los controles de ancho de banda para la replicación basada en archivos de sitio a sitio, aunque no está directamente relacionado.  

 Para obtener más información, consulte [Administración del ancho de banda de red](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

## <a name="binary-differential-replication"></a>Replicación diferencial binaria  
 La replicación diferencial binaria (BDR) es un requisito previo de los puntos de distribución y se usa automáticamente para reducir el uso de ancho de banda cuando se distribuyen las actualizaciones de contenido que se han implementado previamente en otros sitios o en un punto de distribución remoto.  

 La BDR minimiza el ancho de banda de red que se usa para enviar actualizaciones de contenido distribuido, ya que solo reenvía el contenido nuevo o cambiado, en lugar de enviar todo el conjunto de archivos de origen de contenido cada vez que se produce un cambio en dichos archivos.  

 Cuando se usa la replicación diferencial binaria, Configuration Manager identifica los cambios que ocurren en los archivos de origen de cada conjunto de contenido que se ha distribuido anteriormente.  

-   Cuando los archivos del contenido de origen cambian, Configuration Manager crea una nueva versión incremental del conjunto de contenido y replica solamente los archivos cambiados en sitios de destino y puntos de distribución. Se considera que un archivo ha cambiado cuando se ha cambiado su nombre, se ha movido o su contenido ha cambiado. Por ejemplo, si sustituye un solo archivo de controlador del paquete de implementación de un sistema operativo distribuido anteriormente a varios sitios, solo se replica el archivo de controlador cambiado a esos sitios de destino.  

-   Configuration Manager admite hasta cinco versiones incrementales de un conjunto de contenido antes de volver a enviar todo el conjunto de contenido. Después de la quinta actualización, el siguiente cambio en el conjunto de contenido hace que Configuration Manager cree una nueva versión del conjunto de contenido. Configuration Manager distribuye la nueva versión del conjunto de contenido para reemplazar el conjunto anterior y cualquiera de sus versiones incrementales. Después de que el nuevo conjunto de contenido se distribuya, la replicación diferencial binaria replicará de nuevo los cambios incrementales subsiguientes en los archivos de origen.  


La BDR es compatible entre cada sitio principal y secundario de una jerarquía. Dentro de un sitio, la BDR es compatible entre el servidor de sitio y sus puntos de distribución. Esta compatibilidad incluye puntos de distribución de extracción, pero no incluye puntos de distribución basados en la nube. Los puntos de distribución basados en la nube no admiten la replicación diferencial binaria para transferir contenido.  

Las aplicaciones siempre usan la replicación diferencial binaria. En el caso de los paquetes, la replicación diferencial binaria es opcional y no está habilitada de forma predeterminada. Para utilizar la replicación diferencial binaria para paquetes, debe habilitar esta funcionalidad en cada paquete. Para ello, seleccione la opción **Habilitar replicación diferencial binaria** cuando cree un paquete nuevo o cuando edite la pestaña **Origen de datos** de las propiedades del paquete.  

## <a name="branchcache"></a>BranchCache  
 Tecnología de Windows que habilita a los clientes que admiten BranchCache y que han descargado una implementación configurada para BranchCache, de modo que después puedan actuar como un origen de contenido para otros clientes habilitados para BranchCache.  

 Por ejemplo, cuando el primer equipo cliente habilitado para BranchCache solicita contenido desde un punto de distribución que ejecuta Windows Server 2012 y que se configuró como un servidor de BranchCache, el equipo cliente descarga el contenido y lo almacena en la memoria caché.  

-   Dicho equipo cliente puede hacer que el contenido esté disponible para otros clientes habilitados para BranchCache en la misma subred, que también pueden almacenar en caché el contenido.  

-   De esta forma, los siguientes clientes de la misma subred no tienen que descargar contenido desde el punto de distribución, y el contenido se distribuye por varios clientes en las siguientes transferencias.  

## <a name="peer-cache"></a>Almacenamiento en caché del mismo nivel
A partir de la versión 1610, el almacenamiento en caché del mismo nivel de cliente le ayuda a administrar la implementación de contenido en los clientes en ubicaciones remotas. La caché del mismo nivel es una solución integrada de Configuration Manager que permite que los clientes compartan contenido con otros clientes directamente desde su caché local.

Después de implementar la configuración de cliente que habilita el almacenamiento en caché del mismo nivel en una colección, los miembros de esa colección pueden actuar como origen de contenido del mismo nivel para otros clientes en el mismo grupo de límites.

Para obtener más información, vea [Caché del mismo nivel para clientes de Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).


## <a name="windows-pe-peer-cache"></a>Almacenamiento en caché del mismo nivel de Windows PE
Al implementar un nuevo sistema operativo en System Center Configuration Manager, los equipos que ejecutan la secuencia de tareas pueden usar Almacenamiento en caché del mismo nivel de Windows PE para obtener contenido de un elemento local del mismo nivel (un origen de almacenamiento en caché del mismo nivel), en lugar de descargar el contenido de un punto de distribución. Esto ayuda a minimizar el tráfico de red de área extensa (WAN) en escenarios de sucursales donde no hay ningún punto de distribución local.

Para obtener más información, consulte [Almacenamiento en caché del mismo nivel de Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).


## <a name="client-locations"></a>Ubicaciones del cliente  
 A continuación se indican las ubicaciones desde las que los clientes tienen acceso a contenido:  

-   **Intranet** (local):  

    -   Los puntos de distribución pueden usar HTTP o HTTPS.  

    -   Use solo un punto de distribución basado en la nube para la reserva si no están disponibles los puntos de distribución locales.  

-   **Internet**:  

    -   Requiere que los puntos de distribución acepten HTTPS.  

    -   Es posible usar un punto de distribución basado en la nube para la reserva.  

-   **Grupo de trabajo**:  

    -   Requiere que los puntos de distribución acepten HTTPS.  

    -   Es posible usar un punto de distribución basado en la nube para la reserva.  



## <a name="content-library"></a>Biblioteca de contenido  
 La biblioteca de contenido es un almacén de instancia única del contenido que Configuration Manager usa para reducir el tamaño total del cuerpo combinado del contenido que distribuya.  

Obtenga más información sobre la [biblioteca de contenido](../../../core/plan-design/hierarchy/the-content-library.md).


## <a name="distribution-points"></a>Puntos de distribución  
 Configuration Manager usa puntos de distribución para almacenar los archivos necesarios para la ejecución de software en los equipos cliente. Los clientes deben tener acceso al menos a un punto de distribución desde el cual puedan descargar los archivos del contenido que implemente.  

 El punto de distribución básico (no especializado) suele denominarse punto de distribución estándar. Hay dos variaciones en el punto de distribución estándar que reciben atención especial:  

-   **Punto de distribución de extracción**: variación de un punto de distribución donde el punto de distribución obtiene contenido de otro punto de distribución (un punto de distribución de origen). Este proceso es similar a la manera en que los clientes descargan contenido desde los puntos de distribución. Los puntos de distribución de extracción pueden ayudarle a evitar los cuellos de botella en el ancho de banda de red que se producen cuando el servidor de sitio debe distribuir directamente el contenido a cada punto de distribución.  Consulte [Usar un punto de distribución de extracción con System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Punto de distribución basado en la nube**: variación de un punto de distribución instalado en Microsoft Azure. [Obtenga información sobre cómo usar un punto de distribución basado en la nube con System Center Configuration Manager](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md).  


Los puntos de distribución estándar admiten diversas configuraciones y características, como la limitación y la programación, el entorno PXE y la multidifusión, o el contenido preconfigurado.  

-   Puede usar controles como las **programaciones** o el **límite de ancho de banda** para ayudar a controlar esta transferencia.  

-   También puede usar otras opciones, incluido el **contenido preconfigurado** y los **puntos de distribución de extracción**. Además, puede aprovechar **BranchCache** para reducir el ancho de banda de red que se usa al implementar el contenido.  

-   Los puntos de distribución admiten distintas configuraciones, como el entorno **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** y la **[multidifusión](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)** para las implementaciones del sistema operativo o configuraciones que admiten **dispositivos móviles**.  

 Los puntos de distribución de extracción y basados en la nube admiten muchas de estas configuraciones, pero tienen limitaciones específicas de cada variación del punto de distribución.  

## <a name="distribution-point-groups"></a>Grupos de puntos de distribución  
 Los grupos de puntos de distribución son agrupaciones lógicas de puntos de distribución que pueden simplificar la distribución de contenido.  

 Para obtener más información, vea [Administrar grupos de puntos de distribución](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).

## <a name="distribution-point-priority"></a>Prioridad de puntos de distribución  
 El valor de prioridad del punto de distribución se basa en cuánto tiempo se tardó en transferir las implementaciones anteriores en ese punto de distribución.  

-   Se trata de un valor autoajustable asignado a un punto de distribución que ayuda a Configuration Manager a transferir contenido a más puntos de distribución en un período de tiempo más corto.  

-   Cuando distribuye contenido a varios puntos de distribución al mismo tiempo o a un grupo de puntos de distribución, Configuration Manager envía el contenido al punto de distribución con la prioridad más alta antes de enviar el mismo contenido a otro punto de distribución con una prioridad inferior.  

-   Esto no sustituye la prioridad de distribución de los paquetes, que sigue siendo el factor decisivo en la secuencia de transferencia de las distribuciones.  


Por ejemplo, si distribuye contenido con una prioridad de distribución alta en un punto de distribución con una prioridad de punto de distribución baja, este paquete de prioridad de distribución siempre se transferirá antes que un paquete con una prioridad inferior. La prioridad de la distribución se aplica incluso si los paquetes que tienen una prioridad de distribución inferior se distribuyen a puntos de distribución con prioridades de punto de distribución mayores.

Una prioridad de distribución alta del paquete garantiza que Configuration Manager distribuirá el contenido a los puntos de distribución aplicables antes de que se envíen paquetes con una prioridad de distribución inferior.  

> [!NOTE]  
>  Los puntos de distribución de extracción también usan el concepto de prioridad para ordenar la secuencia de los puntos de distribución de origen.  
>   
>  -   La prioridad de los puntos de distribución para las transferencias de contenido al punto de distribución es distinta de la prioridad que los puntos de distribución de extracción usan cuando buscan contenido en un punto de distribución de origen.  
>  -   Para obtener más información, vea [Usar un punto de distribución de extracción con System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  


## <a name="fallback"></a>Reserva  
 A partir de la versión 1610, han cambiado algunas cuestiones relacionadas con la forma en que los clientes buscan un punto de distribución que tenga contenido, incluida la reserva. Use la información siguiente aplicada a su versión:

**Versión 1610 y posteriores**   
Los clientes que no encuentran contenido en un punto de distribución asociado a su grupo de límites actual pueden usar como reserva ubicaciones de origen de contenido asociadas a grupos de límites vecinos. Para que se use como reserva, un grupo de límites vecino debe tener una relación definida con el grupo de límites actual del cliente. Esta relación incluye un tiempo configurado que debe transcurrir para que un cliente que no encuentra contenido localmente pueda incluir orígenes de contenido del grupo de límites vecino como parte de su búsqueda.

Ya no se usa el concepto de puntos de distribución preferidos, y la opción para **permitir el uso de ubicaciones de origen de reserva para el contenido** ya no está disponible ni se aplica.

Para obtener más información, consulte [Boundary groups (Grupos de límites)](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


**Versiones 1511, 1602 y 1606**   
La configuración de reserva está relacionada con el uso de los **puntos de distribución preferidos** y con las ubicaciones de origen de contenido que usan los clientes.

-   De manera predeterminada, los clientes solo descargan contenido desde un punto de distribución preferido (uno que esté asociado a los grupos de límites del cliente).  

-   Sin embargo, cuando se configura un punto de distribución con **Allow clients to use this site system as a fallback source location for content** (Permitir a los clientes usar este sistema de sitio como ubicación de origen de reserva para contenido), dicho punto solo se ofrece como origen de contenido válido a todos los clientes que no puedan obtener una implementación desde uno de sus puntos de distribución preferidos.  


Para obtener información sobre los diferentes escenarios de reserva y ubicación de contenido, vea [Escenarios de ubicación de orígenes de contenido](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). Para obtener información sobre los grupos de límites, vea [Grupos de límites para las versiones 1511, 1602 y 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).

## <a name="network-bandwidth"></a>Ancho de banda de red  
 Para administrar la cantidad de ancho de banda de red usada al distribuir contenido, puede usar las opciones siguientes:  

-   **Contenido preconfigurado**: proceso de transferencia de contenido a un punto de distribución sin depender de Configuration Manager para distribuir el contenido a través de la red.  

-   **Programación y limitación**: configuraciones que ayudan a controlar el momento y la forma en que se distribuye el contenido a los puntos de distribución.  

Para obtener más información, consulte [Administración del ancho de banda de red](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

## <a name="network-connection-speed-to-content-source"></a>Velocidad de conexión de red con el origen de contenido  
A partir de la versión 1610, han cambiado algunas cuestiones relacionadas con la forma en que los clientes buscan un punto de distribución que tenga contenido, incluida la velocidad de conexión de red con un origen de contenido. Use la información siguiente aplicada a su versión:

**Versión 1610 y posteriores**   
Ya no se usan las velocidades de conexión de red que definen un punto de distribución como **rápido** o **lento**. En su lugar, cada sistema de sitio asociado a un grupo de límites se trata de la misma manera.

Para obtener más información, consulte [Boundary groups (Grupos de límites)](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


**Versiones 1511, 1602 y 1606**   
 Puede configurar la velocidad de conexión de red de cada punto de distribución en un grupo de límites:  

-   Los clientes usan este valor al conectarse al punto de distribución.

-   De forma predeterminada, la velocidad de conexión de red se configura como **Rápida**, pero también se puede establecer como **Lenta**.  

-   La **velocidad de conexión de red** y la configuración de una implementación determinan si un cliente puede descargar contenido desde un punto de distribución cuando el cliente está en un grupo de límites asociado.  

Para obtener información sobre los diferentes escenarios de reserva y ubicación de contenido, vea [Escenarios de ubicación de orígenes de contenido](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). Para obtener información sobre los grupos de límites, vea [Grupos de límites para las versiones 1511, 1602 y 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).

## <a name="on-demand-content-distribution"></a>Distribución de contenido a petición  
 La distribución de contenido a petición es una opción que puede establecer para aplicaciones y paquetes individuales (implementaciones) con el fin de habilitar la distribución de contenido a petición a puntos de distribución preferidos.  

-   Para habilitar esta opción para una implementación, habilite **Distribuir el contenido de este paquete en puntos de distribución preferidos**.  

-   Cuando esta opción está habilitada para una implementación y un cliente intenta solicitar ese contenido pero dicho contenido no está disponible en ninguno de los puntos de distribución preferidos del cliente, Configuration Manager distribuye automáticamente el contenido a los puntos de distribución preferidos del cliente.  

-   Aunque esto hace que Configuration Manager distribuya automáticamente el contenido a los puntos de distribución preferidos del cliente, este puede obtener el contenido desde otros puntos de distribución antes de que los puntos de distribución preferidos del cliente reciban la implementación. Cuando esto suceda, el contenido estará presente en ese punto de distribución para que lo use el próximo cliente que busque esa implementación.  

Si usa la versión 1610 o una versión posterior, consulte [Grupos de límites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
Si usa las versiones 1511, 1602 o 1606, vea [Escenarios de ubicación de orígenes de contenido](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) para obtener información sobre los diferentes escenarios de reserva y ubicación de contenido.  



## <a name="package-transfer-manager"></a>Administrador de transferencia de paquetes  
 El administrador de transferencia de paquetes es el componente del servidor de sitio que transfiere contenido a puntos de distribución de otros equipos.  

 Obtenga más información sobre el [administrador de transferencia de paquetes](../../../core/plan-design/hierarchy/package-transfer-manager.md).  

## <a name="preferred-distribution-point"></a>Punto de distribución preferido  
 Un punto de distribución preferido incluye todos los puntos de distribución que están asociados a los grupos de límites actuales de un cliente.  

 Tiene la opción de asociar cada punto de distribución a uno o más grupos de límites:  

-   Esta asociación ayuda al cliente a identificar puntos de distribución desde los que puede descargar contenido.  
-   De forma predeterminada, los clientes solo pueden descargar contenido desde un punto de distribución preferido.  


Para obtener más información:
 - Si usa la versión 1610 o una versión posterior, consulte [Grupos de límites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
 - Si usa las versiones 1511, 1602 o 1606, vea [Escenarios de ubicación de orígenes de contenido](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).

## <a name="prestage-content"></a>Preconfigurar el contenido  
 La preconfiguración de contenido es un proceso de transferencia de contenido a un punto de distribución sin depender de Configuration Manager para distribuir el contenido a través de la red.  

 Para obtener más información, consulte [Administración del ancho de banda de red](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

