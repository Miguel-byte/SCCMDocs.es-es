---
title: Conceptos básicos de administración de contenido
titleSuffix: Configuration Manager
description: Use herramientas y opciones en Configuration Manager para administrar el contenido que implemente.
ms.custom: na
ms.date: 03/22/2018
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
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0595e34d096b2d7f6450b3255bae03ae3aa57862
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2018
---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>Conceptos básicos de la administración de contenido en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager admite un sistema eficaz de herramientas y opciones para administrar el contenido que se implementa como aplicaciones, paquetes, actualizaciones de software e implementaciones de sistema operativo. Configuration Manager almacena el contenido en servidores de sitio y puntos de distribución. Este contenido requiere una gran cantidad de ancho de banda de red cuando se transfiere entre ubicaciones. Para planear y usar eficazmente la infraestructura de administración de contenido, se recomienda comprender las opciones y configuraciones disponibles. Después, considere la posibilidad de cómo usarlas para ajustar mejor las necesidades de implementación de contenido y el entorno de red.  

> [!TIP]    
> Para obtener más información sobre el proceso de distribución de contenido y para buscar ayuda para diagnosticar y solucionar problemas generales de distribución de contenido, vea [Descripción y solución de problemas de distribución de contenido en Microsoft Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

Los temas siguientes son conceptos clave para la administración de contenido. Cuando un concepto requiere información adicional o compleja, se proporcionan vínculos para dirigirle a ella.



## <a name="accounts-used-for-content-management"></a>Cuentas usadas para la administración de contenido  
 Las cuentas siguientes pueden usarse con la administración de contenido:  

-   **Cuenta de acceso a la red**: la usan los clientes para conectarse a un punto de distribución y tener acceso al contenido. De forma predeterminada, se intenta usar en primer lugar la cuenta de equipo.  

     Esta cuenta también la usan los puntos de distribución de extracción para descargar el contenido de un punto de distribución de origen en un bosque remoto.  

-   **Cuenta de acceso de paquete**: de forma predeterminada, Configuration Manager concede acceso al contenido en un punto de distribución a los usuarios y los administradores de cuentas de acceso genéricas. Sin embargo, puede configurar permisos adicionales para restringir el acceso.   

-   **Cuenta de conexión de multidifusión**: se usa para implementaciones de sistema operativo.  

Para obtener más información sobre estas cuentas, consulte [Administración de cuentas para acceder al contenido](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).



## <a name="bandwidth-throttling-and-scheduling"></a>Programación y límite de ancho de banda  
 La programación y el límite son opciones que le ayudan a controlar cuándo se distribuye el contenido de un servidor de sitio en puntos de distribución. Estas funciones son similares a los controles de ancho de banda para la replicación basada en archivos de sitio a sitio, aunque no están directamente relacionadas.  

 Para obtener más información, consulte [Administración del ancho de banda de red](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="binary-differential-replication"></a>Replicación diferencial binaria  
 La replicación diferencial binaria (BDR) es un requisito previo para los puntos de distribución. A veces se denomina replicación diferencial. Cuando se distribuyen actualizaciones del contenido que se ha implementado previamente en otros sitios o puntos de distribución remotos, se usa automáticamente la BDR para reducir el ancho de banda.  

 La BDR minimiza el ancho de banda de red que se usa para enviar actualizaciones de contenido distribuido. Solo se vuelve a enviar el contenido nuevo o que ha cambiado en lugar del conjunto completo de archivos de origen de contenido cada vez que se cambian esos archivos.  

 Cuando se usa la BDR, Configuration Manager identifica los cambios que se producen en los archivos de origen de cada conjunto de contenido distribuido anteriormente.  

-   Cuando cambian los archivos en el contenido de origen, el sitio crea una versión incremental del conjunto de contenido. Después, solamente replica los archivos que han cambiado en los sitios de destino y puntos de distribución. Se considera que un archivo ha cambiado cuando se ha cambiado el nombre, se ha movido o se ha modificado su contenido. Por ejemplo, si se sustituye un solo archivo de controlador de un paquete de controladores distribuido anteriormente a varios sitios, solo se replica el archivo de controlador cambiado.  

-   Configuration Manager admite hasta cinco versiones incrementales de un conjunto de contenido antes de volver a enviar todo el conjunto de contenido. Después de la quinta actualización, el siguiente cambio en el conjunto de contenido hace que el sitio cree una versión del conjunto de contenido. Configuration Manager distribuye la nueva versión del conjunto de contenido para reemplazar el conjunto anterior y cualquiera de sus versiones incrementales. Después de distribuir el nuevo conjunto de contenido, la BDR replicará de nuevo los cambios incrementales siguientes en los archivos de origen.  

La BDR es compatible entre cada sitio principal y secundario de una jerarquía. Dentro de un sitio, la BDR es compatible entre el servidor de sitio y sus puntos de distribución normales. Pero los puntos de distribución de extracción y basados en la nube no admiten la BDR para transferir contenido. Los puntos de distribución de extracción admiten deltas de nivel de archivo, transferir archivos nuevos, pero no los bloques dentro de un archivo.

Las aplicaciones siempre usan la replicación diferencial binaria. La BDR es opcional para los paquetes y no está habilitada de forma predeterminada. Para usar la BDR para paquetes, habilite esta funcionalidad en cada paquete. Seleccione la opción **Habilitar replicación diferencial binaria** al crear o modificar un paquete.   



## <a name="branchcache"></a>BranchCache  
 [BranchCache](/windows-server/networking/branchcache/branchcache) es una tecnología de Windows. Los clientes que admiten BranchCache y que han descargado una implementación configurada para BranchCache, después actúan como un origen de contenido para otros clientes habilitados para BranchCache.  

 Por ejemplo, tiene un punto de distribución en el que se ejecuta Windows Server 2012 o una versión posterior, y está configurado como un servidor de BranchCache. Cuando el primer cliente habilitado para BranchCache solicita contenido desde este servidor, el cliente descarga el contenido y lo almacena en caché.  

- Después, ese cliente puede hacer que el contenido esté disponible para otros clientes habilitados para BranchCache en la misma subred, que también pueden almacenar en caché el contenido.  
- Otros clientes en la misma subred no tendrán que descargar el contenido desde el punto de distribución.  
- El contenido se distribuye entre varios clientes para futuras transferencias.  



## <a name="delivery-optimization"></a>Optimización de entrega
<!-- 1324696 -->
Los grupos de límites de Configuration Manager se usan para definir y regular la distribución de contenido a través de la red corporativa y en las oficinas remotas. La [optimización de distribución de Windows](/windows/deployment/update/waas-delivery-optimization) es una tecnología entre iguales basada en la nube para compartir contenido entre los dispositivos de Windows 10. A partir de la versión 1802, configure la optimización de entrega para usar los grupos de límites al compartir contenido entre iguales. La configuración de cliente aplica el identificador del grupo de límites como el identificador del grupo de optimización de entrega en el cliente. Cuando el cliente se comunica con el servicio en la nube de optimización de distribución, utiliza este identificador para buscar elementos del mismo nivel con el contenido deseado. Para obtener más información, vea la configuración de cliente de [optimización de distribución](/sccm/core/clients/deploy/about-client-settings#delivery-optimization).



## <a name="peer-cache"></a>Almacenamiento en caché del mismo nivel
El almacenamiento en caché del mismo nivel de cliente ayuda a administrar la implementación de contenido en los clientes en ubicaciones remotas. El almacenamiento en caché del mismo nivel es una solución integrada de Configuration Manager que permite a los clientes compartir contenido con otros clientes directamente desde su caché local.

Después de implementar la configuración de cliente que habilita el almacenamiento en caché del mismo nivel en una colección, los miembros de esa colección pueden actuar como origen de contenido del mismo nivel para otros clientes en el mismo grupo de límites.

Para obtener más información, vea [Caché del mismo nivel para clientes de Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).



## <a name="windows-pe-peer-cache"></a>Almacenamiento en caché del mismo nivel de Windows PE
Al implementar un sistema operativo nuevo con Configuration Manager, los equipos que ejecutan la secuencia de tareas pueden usar el almacenamiento en caché del mismo nivel de Windows PE. Descargan el contenido desde un origen de almacenamiento en caché del mismo nivel en lugar de un punto de distribución. Este comportamiento ayuda a minimizar el tráfico de WAN en escenarios de sucursales donde no hay ningún punto de distribución local.

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
 La biblioteca de contenido es el almacén de instancia única del contenido en Configuration Manager. Esta biblioteca reduce el tamaño total del contenido que se distribuye.  

- Obtenga más información sobre la [biblioteca de contenido](../../../core/plan-design/hierarchy/the-content-library.md).
- Utilice la herramienta [Content Library Cleanup Tool](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) para quitar contenido cuando deja de estar asociado con una aplicación.  



## <a name="distribution-points"></a>Puntos de distribución  
 Configuration Manager usa puntos de distribución para almacenar los archivos necesarios para la ejecución de software en los equipos cliente. Los clientes deben tener acceso al menos a un punto de distribución desde el cual puedan descargar los archivos del contenido que implemente.  

 El punto de distribución básico (no especializado) suele denominarse punto de distribución estándar. Hay dos variaciones en el punto de distribución estándar que reciben atención especial:  

-   **Punto de distribución de extracción**: variación de un punto de distribución donde el punto de distribución obtiene contenido de otro punto de distribución (un punto de distribución de origen). Este proceso es similar a la manera en que los clientes descargan contenido desde los puntos de distribución. Los puntos de distribución de extracción pueden ayudarle a evitar los cuellos de botella en el ancho de banda de red que se producen cuando el servidor de sitio debe distribuir directamente el contenido a cada punto de distribución. [Usar un punto de distribución de extracción](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Punto de distribución basado en la nube**: variación de un punto de distribución instalado en Microsoft Azure. [Obtenga información sobre cómo usar un punto de distribución basado en la nube](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md).  


Los puntos de distribución estándar admiten una variedad de configuraciones y características:  

- Use controles como las **programaciones** o el **límite de ancho de banda** para ayudar a controlar esta transferencia.  
- Use otras opciones, incluido el **contenido preconfigurado** y los **puntos de distribución de extracción** para minimizar y controlar el consumo de red. 
- **BranchCache**, **Caché del mismo nivel** y **Optimización de distribución** son tecnologías punto a punto para reducir el ancho de banda de red que se usa al implementar contenido.  
- Existen otras configuraciones para implementaciones de sistema operativo, como **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** y **[Multidifusión](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**.
- Opciones para **dispositivos móviles**   
  
  
Los puntos de distribución de extracción y basados en la nube admiten muchas de estas configuraciones, pero tienen limitaciones específicas de cada variación del punto de distribución.  



## <a name="distribution-point-groups"></a>Grupos de puntos de distribución  
 Los grupos de puntos de distribución son agrupaciones lógicas de puntos de distribución que pueden simplificar la distribución de contenido.  

 Para obtener más información, vea [Administrar grupos de puntos de distribución](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).



## <a name="distribution-point-priority"></a>Prioridad de puntos de distribución  
 El valor de prioridad del punto de distribución se basa en cuánto tiempo se tardó en transferir las implementaciones anteriores en ese punto de distribución.  

-   Este valor es de ajuste automático. Se establece en cada punto de distribución para ayudar a Configuration Manager a transferir el contenido más rápidamente a más puntos de distribución.  

-   Cuando se distribuye contenido a varios puntos de distribución al mismo tiempo, o bien a un grupo de puntos de distribución, el sitio envía primero el contenido al servidor con la prioridad más alta. Después, envía el mismo contenido a un punto de distribución con una prioridad inferior.  

-   La prioridad de los puntos de distribución no sustituye a la prioridad de distribución de los paquetes. La prioridad del paquete sigue siendo el factor decisivo de cuándo envía el sitio otro contenido.  

Por ejemplo, tiene un paquete con una prioridad de paquete alta. Lo distribuye a un servidor con una prioridad de punto de distribución baja. Este paquete de prioridad alta siempre se transferirá antes que un paquete con una prioridad más baja. La prioridad de paquete se aplica incluso si el sitio distribuye paquetes de prioridad más baja a servidores con prioridades de punto de distribución más altas.

La prioridad alta del paquete garantiza que Configuration Manager distribuye el contenido a los puntos de distribución antes de que envíe paquetes con una prioridad de distribución inferior.  

> [!NOTE]  
>  Los puntos de distribución de extracción también usan el concepto de prioridad para ordenar la secuencia de los puntos de distribución de origen.  
>   
>  -   La prioridad de punto de distribución de las transferencias de contenido al servidor es distinta de la prioridad que usan los puntos de distribución de extracción. Los puntos de distribución de extracción usan su prioridad cuando buscan contenido de un punto de distribución de origen.  
>  -   Para más información, vea [Usar un punto de distribución de extracción con System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  



## <a name="fallback"></a>Reserva  
 Varios aspectos han cambiado con la Rama actual de Configuration Manager relacionados con la forma en que los clientes buscan un punto de distribución que tiene contenido, incluida la reserva. 

Los clientes que no encuentran contenido en un punto de distribución asociado a su grupo de límites actual usan como reserva ubicaciones de origen de contenido asociadas a grupos de límites vecinos. Para que se use como reserva, un grupo de límites vecino debe tener una relación definida con el grupo de límites actual del cliente. Esta relación incluye un tiempo configurado que debe transcurrir para que un cliente que no encuentra contenido localmente incluya los orígenes de contenido del grupo de límites vecino como parte de su búsqueda.

Ya no se usa el concepto de puntos de distribución preferidos, y la opción para **permitir el uso de ubicaciones de origen de reserva para el contenido** ya no está disponible ni se aplica.

Para obtener más información, consulte [Boundary groups (Grupos de límites)](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
**Version 1511, 1602, and 1606**   
Fallback settings are related to the use of **preferred distribution points** and to content source locations that are used by clients.

-   By default, clients only download content from a preferred distribution point (one that is associated with the client's boundary groups).  

-   However, when a distribution point is configured with **Allow clients to use this site system as a fallback source location for content**, that distribution point is only offered as a valid content source to any client that can't get a deployment from one of its preferred distribution points.  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="network-bandwidth"></a>Ancho de banda de red  
 Para administrar la cantidad de ancho de banda de red usada al distribuir contenido, puede usar las opciones siguientes:  

-   **Contenido preconfigurado**: transferencia de contenido a un punto de distribución sin distribuir el contenido a través de la red.  

-   **Programación y limitación**: configuraciones que ayudan a controlar el momento y la forma en que se distribuye el contenido a los puntos de distribución.  

Para obtener más información, consulte [Administración del ancho de banda de red](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="network-connection-speed-to-content-source"></a>Velocidad de conexión de red con el origen de contenido  
 Varios aspectos han cambiado con la Rama actual de Configuration Manager relacionados con la forma en que los clientes buscan un punto de distribución que tiene contenido. Estos cambios incluyen la velocidad de red a un origen de contenido. 

Ya no se usan las velocidades de conexión de red que definen un punto de distribución como **rápido** o **lento**. En su lugar, cada sistema de sitio asociado a un grupo de límites se trata de la misma manera.

Para obtener más información, consulte [Boundary groups (Grupos de límites)](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
**Version 1511, 1602, and 1606**   
 You can configure the network connection speed of each distribution point in a boundary group:  

-   Clients use this value when they connect to the distribution point.

-   By default, the network connection speed is configured as **Fast**, but it can also be set as **Slow**.  

-   The **network connection speed**, along with the configuration of a deployment, determine if a client can download content from a distribution point when the client is in an associated boundary group  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="on-demand-content-distribution"></a>Distribución de contenido a petición  
 La distribución de contenido a petición es una opción para las implementaciones de aplicaciones y paquetes individuales. Esta opción permite la distribución de contenido a petición en los servidores preferidos.  

-   Para habilitar esta opción para una implementación, habilite: **Distribuir el contenido de este paquete en puntos de distribución preferidos**.  

-   Cuando esta opción está habilitada para una implementación y un cliente intenta solicitar ese contenido pero dicho contenido no está disponible en ninguno de los puntos de distribución preferidos del cliente, Configuration Manager distribuye automáticamente el contenido a los puntos de distribución preferidos del cliente.  

-   Aunque esto hace que Configuration Manager distribuya automáticamente el contenido a los puntos de distribución preferidos del cliente, este puede obtener el contenido desde otros puntos de distribución antes de que los puntos de distribución preferidos del cliente reciban la implementación. Cuando se produce este comportamiento, el contenido estará presente en ese punto de distribución para que lo use el próximo cliente que busque esa implementación.  

Para obtener más información, consulte [Boundary groups (Grupos de límites)](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
If you use version 1511, 1602, or 1606, see  [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) for information about the different content location and fallback scenarios.
-->



## <a name="package-transfer-manager"></a>Administrador de transferencia de paquetes  
 El administrador de transferencia de paquetes es el componente de servidor de sitio que transfiere contenido a puntos de distribución de otros equipos.  

 Para obtener más información, vea [Administrador de transferencia de paquetes](../../../core/plan-design/hierarchy/package-transfer-manager.md).  



<!--
## Preferred distribution point  
 A preferred distribution point includes any distribution points that are associated with a client's current boundary groups.  

 You have the option to associate each distribution point with one or more boundary groups:  

-   This association helps the client identify distribution points from which it can download content.  
-   By default, clients can only download content from a preferred distribution point.  


For more information:
 - If you use version 1610 or later, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
 - If you use version 1511, 1602, or 1606, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).
-->



## <a name="prestage-content"></a>Preconfigurar el contenido  
 Preconfigurar el contenido es un proceso de transferencia de contenido a un punto de distribución sin distribuirlo a través de la red.  

 Para obtener más información, consulte [Administración del ancho de banda de red](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).
