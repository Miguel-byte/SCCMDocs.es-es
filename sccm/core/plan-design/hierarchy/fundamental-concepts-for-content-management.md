---
title: Conceptos básicos de administración de contenido
titleSuffix: Configuration Manager
description: Use herramientas y opciones en Configuration Manager para administrar el contenido que implemente.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a8f4d93c7bfa73b04ed2c760db17b27e8f1f6de2
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385273"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Aspectos básicos de la administración de contenido en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager admite un sólido sistema de herramientas y opciones para administrar contenido de software. Todas las implementaciones de software (como aplicaciones, paquetes, actualizaciones de software e implementaciones del sistema operativo) necesitan contenido. Configuration Manager almacena el contenido en servidores de sitio y puntos de distribución. Este contenido requiere una gran cantidad de ancho de banda de red cuando se transfiere entre ubicaciones. Para planear y usar de manera eficaz la infraestructura de administración de contenidos, primero necesita comprender las opciones y configuraciones disponibles. Después, considere la posibilidad de cómo usarlas para ajustar mejor las necesidades de implementación de contenido y el entorno de red.  

> [!TIP]    
> Para obtener más información sobre el proceso de distribución de contenido y para buscar ayuda para diagnosticar y solucionar problemas generales de distribución de contenido, vea [Descripción y solución de problemas de distribución de contenido en Microsoft Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

Los temas siguientes son conceptos clave para la administración de contenido. Cuando un concepto requiere información adicional o compleja, se proporcionan vínculos para dirigirle a ella.



## <a name="accounts-used-for-content-management"></a>Cuentas usadas para la administración de contenido  
 Las cuentas siguientes pueden usarse con la administración de contenido:  

-   **Cuenta de acceso a la red**: la usan los clientes para conectarse a un punto de distribución y tener acceso al contenido. De forma predeterminada, se intenta usar en primer lugar la cuenta de equipo.  

     Esta cuenta también la usan los puntos de distribución de extracción para descargar el contenido de un punto de distribución de origen en un bosque remoto.  

-   **Cuenta de acceso de paquete**: de forma predeterminada, Configuration Manager concede acceso al contenido en un punto de distribución a los usuarios y los administradores de cuentas de acceso genéricas. Sin embargo, puede configurar permisos adicionales para restringir el acceso.   

-   **Cuenta de conexión de multidifusión**: se usa para implementaciones de sistema operativo.  

Para obtener más información sobre estas cuentas, consulte [Administración de cuentas para acceder al contenido](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content).



## <a name="bandwidth-throttling-and-scheduling"></a>Programación y límite de ancho de banda  
 La programación y el límite son opciones que le ayudan a controlar cuándo se distribuye el contenido de un servidor de sitio en puntos de distribución. Estas funciones son similares a los controles de ancho de banda para la replicación basada en archivos de sitio a sitio, aunque no están directamente relacionadas.  

 Para obtener más información, consulte [Administración del ancho de banda de red](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="binary-differential-replication"></a>Replicación diferencial binaria  
 La replicación diferencial binaria (BDR) es un requisito previo para los puntos de distribución. También se conoce como replicación diferencial. Cuando se distribuyen actualizaciones del contenido que se ha implementado previamente en otros sitios o puntos de distribución remotos, se usa automáticamente la BDR para reducir el ancho de banda.  

 La BDR minimiza el ancho de banda de red que se usa para enviar actualizaciones de contenido distribuido. Solo se vuelve a enviar el contenido nuevo o que ha cambiado en lugar del conjunto completo de archivos de origen de contenido cada vez que se cambian esos archivos.  

 Cuando se usa la BDR, Configuration Manager identifica los cambios que se producen en los archivos de origen de cada conjunto de contenido distribuido anteriormente.  

-   Cuando cambian los archivos del contenido de origen, el sitio crea una versión incremental del contenido. Después, solamente replica los archivos que han cambiado en los sitios de destino y puntos de distribución. Se considera que un archivo ha cambiado cuando se ha cambiado el nombre, se ha movido o se ha modificado su contenido. Por ejemplo, si se sustituye un solo archivo de controlador de un paquete de controladores distribuido anteriormente a varios sitios, solo se replica el archivo de controlador cambiado.  

-   Configuration Manager admite hasta cinco versiones incrementales de un conjunto de contenido antes de volver a enviar todo el conjunto de contenido. Después de la quinta actualización, el siguiente cambio en el conjunto de contenido hace que el sitio cree una versión del conjunto de contenido. Configuration Manager distribuye la nueva versión del conjunto de contenido para reemplazar el conjunto anterior y cualquiera de sus versiones incrementales. Después de distribuir el nuevo conjunto de contenido, la BDR replicará de nuevo los cambios incrementales siguientes en los archivos de origen.  

La BDR es compatible entre cada sitio principal y secundario de una jerarquía. Dentro de un sitio, la BDR es compatible entre el servidor de sitio y sus puntos de distribución normales. Pero los puntos de distribución de extracción y los puntos de distribución de nube no son compatibles con BDR para la transferencia de contenido. Los puntos de distribución de extracción admiten deltas de nivel de archivo, transferir archivos nuevos, pero no los bloques dentro de un archivo.

Las aplicaciones siempre usan la replicación diferencial binaria. BDR es opcional para los paquetes y no está habilitada de forma predeterminada. Para usar la BDR para paquetes, habilite esta funcionalidad en cada paquete. Seleccione la opción **Habilitar replicación diferencial binaria** al crear o modificar un paquete.   



## <a name="branchcache"></a>BranchCache  
 [BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) es una tecnología de Windows. Los clientes que admiten BranchCache y que han descargado una implementación configurada para BranchCache, después actúan como un origen de contenido para otros clientes habilitados para BranchCache.  

 Por ejemplo, tiene un punto de distribución en el que se ejecuta Windows Server 2012 o una versión posterior, y está configurado como un servidor de BranchCache. Cuando el primer cliente habilitado para BranchCache solicita contenido desde este servidor, el cliente descarga el contenido y lo almacena en caché.  

- Después, ese cliente puede hacer que el contenido esté disponible para otros clientes habilitados para BranchCache en la misma subred, que también pueden almacenar en caché el contenido.  
- Otros clientes en la misma subred no tendrán que descargar el contenido desde el punto de distribución.  
- El contenido se distribuye entre varios clientes para futuras transferencias.  

Para obtener más información, vea [Compatibilidad con Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache).



## <a name="delivery-optimization"></a>Optimización de entrega
<!-- 1324696 --> Los grupos de límites de Configuration Manager se usan para definir y regular la distribución de contenido a través de la red corporativa y en las oficinas remotas. La [optimización de distribución de Windows](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) es una tecnología entre iguales basada en la nube para compartir contenido entre los dispositivos de Windows 10. A partir de la versión 1802, configure la optimización de entrega para usar los grupos de límites al compartir contenido entre iguales. La configuración de cliente aplica el identificador del grupo de límites como el identificador del grupo de optimización de entrega en el cliente. Cuando el cliente se comunica con el servicio en la nube de optimización de distribución, utiliza este identificador para buscar elementos del mismo nivel con el contenido deseado. Para obtener más información, vea la configuración de cliente de [optimización de distribución](/sccm/core/clients/deploy/about-client-settings#delivery-optimization).

La Optimización de distribución es la tecnología recomendada para [optimizar la distribución de actualizaciones de Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery) de archivos de instalación rápida para actualizaciones de calidad de Windows 10.



## <a name="windows-ledbat"></a>Windows LEDBAT
<!--1358112--> Windows Low Extra Delay Background Transport (LEDBAT) es una característica de control de congestión de la red de Windows Server que permite administrar transferencias de red en segundo plano. En los puntos de distribución que se ejecuten en versiones compatibles de Windows Server, habilite una opción para ayudar a ajustar el tráfico de red. Después, los clientes solo usarán el ancho de banda de red cuando esté disponible. 

Para obtener información general sobre Windows LEDBAT, vea la entrada de blog [Nuevos avances en transporte](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/).

Para obtener más información sobre cómo usar Windows LEDBAT con puntos de distribución de Configuration Manager, vea la opción **Ajustar la velocidad de descarga para usar el ancho de banda de red sin usar (Windows LEDBAT)** al [Configurar las opciones generales de un punto de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-general).



## <a name="peer-cache"></a>Almacenamiento en caché del mismo nivel
El almacenamiento en caché del mismo nivel de cliente ayuda a administrar la implementación de contenido en los clientes en ubicaciones remotas. El almacenamiento en caché del mismo nivel es una solución integrada de Configuration Manager que permite a los clientes compartir contenido con otros clientes directamente desde su caché local.

Primero, implemente la configuración de cliente que habilite la caché de sistemas del mismo nivel en una colección. Después, los miembros de esa colección pueden actuar como un origen de contenido del mismo nivel para otros clientes del mismo grupo de límites.

A partir de la versión 1806, los orígenes de caché de sistemas del mismo nivel de clientes pueden dividir el contenido en varias partes. Estas partes reducen al mínimo la transferencia de red para usar menos WAN. El punto de administración proporciona un seguimiento más detallado de las partes de contenido Intenta eliminar más de una descarga del mismo contenido por grupo de límites.<!--1357346-->

Para obtener más información, vea [Caché del mismo nivel para clientes de Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).



## <a name="windows-pe-peer-cache"></a>Almacenamiento en caché del mismo nivel de Windows PE
Al implementar un sistema operativo nuevo con Configuration Manager, los equipos que ejecutan la secuencia de tareas pueden usar el almacenamiento en caché del mismo nivel de Windows PE. Descargan el contenido desde un origen de almacenamiento en caché del mismo nivel en lugar de un punto de distribución. Este comportamiento minimiza el tráfico WAN en escenarios de sucursales donde no existe un punto de distribución local.

Para obtener más información, consulte [Almacenamiento en caché del mismo nivel de Windows PE](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).



## <a name="client-locations"></a>Ubicaciones del cliente  
 A continuación se indican las ubicaciones desde las que los clientes tienen acceso a contenido:  

-   **Intranet** (local):  

    -   Los puntos de distribución pueden usar HTTP o HTTPS.  

    -   Use un punto de distribución de nube como reserva solo cuando los puntos de distribución locales no estén disponibles.  

-   **Internet**:  

    -   Se necesitan puntos de distribución accesibles desde Internet para aceptar conexiones HTTPS.  

    -   Se puede usar un punto de distribución de nube.  

-   **Grupo de trabajo**:  

    -   Requiere que los puntos de distribución acepten HTTPS.  

    -   Se puede usar un punto de distribución de nube.  



## <a name="content-source-priority"></a>Prioridad de origen de contenido

Cuando un cliente necesita contenido, realiza una solicitud de ubicación de contenido al punto de administración. El punto de administración devuelve una lista de ubicaciones de origen que son válidas para el contenido solicitado. Esta lista varía según el escenario específico, las tecnologías usadas, el diseño del sitio, los grupos de límites y la configuración de implementación. La lista siguiente contiene todas las posibles ubicaciones de orígenes de contenido que un cliente puede usar en el orden en que se prioricen:  

1.  El punto de distribución en el mismo equipo que el cliente
2.  Un origen del mismo nivel en la misma subred de red
3.  Un punto de distribución en la misma subred de red
4.  Un origen del mismo nivel en el mismo sitio de Active Directory
5.  Un punto de distribución en el mismo sitio de Active Directory
6.  Un origen del mismo nivel en el mismo grupo de límites
7.  Un punto de distribución en el grupo de límites actual
8.  Un punto de distribución en un grupo de límites próximo configurado como reserva
9.  Un punto de distribución en el grupo de límites del sitio predeterminado 
10. El servicio en la nube de Windows Update
11. Un punto de distribución accesible desde Internet
12. Un punto de distribución de nube en Azure



## <a name="content-library"></a>Biblioteca de contenido  
 La biblioteca de contenido es el almacén de instancia única del contenido en Configuration Manager. Esta biblioteca reduce el tamaño total del contenido que se distribuye.  

- Obtenga más información sobre la [biblioteca de contenido](/sccm/core/plan-design/hierarchy/the-content-library).
- Utilice la herramienta [Content Library Cleanup Tool](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) para quitar contenido cuando deja de estar asociado con una aplicación.  



## <a name="distribution-points"></a>Puntos de distribución  
 Configuration Manager usa puntos de distribución para almacenar los archivos necesarios para la ejecución de software en los equipos cliente. Los clientes deben tener acceso al menos a un punto de distribución desde el cual puedan descargar los archivos del contenido que implemente.  

 El punto de distribución básico (no especializado) suele denominarse punto de distribución estándar. Hay dos variaciones en el punto de distribución estándar que reciben atención especial:  

-   **Punto de distribución de extracción**: variación de un punto de distribución donde el punto de distribución obtiene contenido de otro punto de distribución (un punto de distribución de origen). Este proceso es similar a la manera en que los clientes descargan contenido desde los puntos de distribución. Los puntos de distribución de extracción pueden ayudarle a evitar los cuellos de botella en el ancho de banda de red que se producen cuando el servidor de sitio debe distribuir directamente el contenido a cada punto de distribución. [Usar un punto de distribución de extracción](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Punto de distribución de nube**: una variación de un punto de distribución instalado en Microsoft Azure. [Obtenga información sobre cómo usar un punto de distribución de nube](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point).  


Los puntos de distribución estándar admiten una variedad de configuraciones y características:  

- Use controles como las **programaciones** o el **límite de ancho de banda** para ayudar a controlar esta transferencia.  

- Use otras opciones, incluido el **contenido preconfigurado** y los **puntos de distribución de extracción** para minimizar y controlar el consumo de red.  

- **BranchCache**, **Caché del mismo nivel** y **Optimización de distribución** son tecnologías punto a punto para reducir el ancho de banda de red que se usa al implementar contenido.  

- Existen otras configuraciones para implementaciones de sistema operativo, como **[PXE](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_PXEDistributionPoint)** y **[Multidifusión](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_DPMulticast)**.  

- Opciones para **dispositivos móviles**   
  
Los puntos de distribución de extracción y de la nube admiten muchas de estas mismas configuraciones, pero tienen limitaciones específicas de cada variación de punto de distribución.  



## <a name="distribution-point-groups"></a>Grupos de puntos de distribución  
 Los grupos de puntos de distribución son agrupaciones lógicas de puntos de distribución que pueden simplificar la distribución de contenido.  

 Para obtener más información, vea [Administrar grupos de puntos de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_manage).



## <a name="distribution-point-priority"></a>Prioridad de puntos de distribución  
 El valor de prioridad del punto de distribución se basa en cuánto tiempo se tardó en transferir las implementaciones anteriores en ese punto de distribución.  

-   Este valor es de ajuste automático. Se establece en cada punto de distribución para ayudar a Configuration Manager a transferir el contenido más rápidamente a más puntos de distribución.  

-   Cuando se distribuye contenido a varios puntos de distribución al mismo tiempo, o bien a un grupo de puntos de distribución, el sitio envía primero el contenido al servidor con la prioridad más alta. Después, envía el mismo contenido a un punto de distribución con una prioridad inferior.  

-   La prioridad del punto de distribución no reemplaza a la prioridad de distribución de los paquetes. La prioridad del paquete sigue siendo el factor decisivo de cuándo envía el sitio otro contenido.  

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



## <a name="network-bandwidth"></a>Ancho de banda de red  
 Para administrar la cantidad de ancho de banda de red usada al distribuir contenido, puede usar las opciones siguientes:  

-   **Contenido preconfigurado**: transferencia de contenido a un punto de distribución sin distribuir el contenido a través de la red.  

-   **Programación y limitación**: configuraciones que ayudan a controlar el momento y la forma en que se distribuye el contenido a los puntos de distribución.  

Para obtener más información, consulte [Administración del ancho de banda de red](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="network-connection-speed-to-content-source"></a>Velocidad de conexión de red con el origen de contenido  
 Varios aspectos han cambiado con la Rama actual de Configuration Manager relacionados con la forma en que los clientes buscan un punto de distribución que tiene contenido. Estos cambios incluyen la velocidad de red a un origen de contenido. 

Ya no se usan las velocidades de conexión de red que definen un punto de distribución como **rápido** o **lento**. En su lugar, cada sistema de sitio asociado a un grupo de límites se trata de la misma manera.

Para obtener más información, consulte [Boundary groups (Grupos de límites)](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).



## <a name="on-demand-content-distribution"></a>Distribución de contenido a petición  
 La distribución de contenido a petición es una opción para las implementaciones de aplicaciones y paquetes individuales. Esta opción permite la distribución de contenido a petición en los servidores preferidos.  

-   Para habilitar esta opción para una implementación, habilite: **Distribuir el contenido de este paquete en puntos de distribución preferidos**.  

-   Cuando se habilita esta opción para una implementación y un cliente pide ese contenido, pero el contenido no está disponible en ninguno de los puntos de distribución preferidos del cliente, Configuration Manager distribuye automáticamente ese contenido en los puntos de distribución preferidos del cliente.  

-   Aunque esto hace que Configuration Manager distribuya automáticamente el contenido a los puntos de distribución preferidos del cliente, este puede obtener el contenido desde otros puntos de distribución antes de que los puntos de distribución preferidos del cliente reciban la implementación. Cuando se produce este comportamiento, el contenido estará presente en ese punto de distribución para que lo use el próximo cliente que busque esa implementación.  

Para obtener más información, consulte [Boundary groups (Grupos de límites)](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).



## <a name="package-transfer-manager"></a>Administrador de transferencia de paquetes  
 El administrador de transferencia de paquetes es el componente de servidor de sitio que transfiere contenido a puntos de distribución de otros equipos.  

 Para obtener más información, vea [Administrador de transferencia de paquetes](/sccm/core/plan-design/hierarchy/package-transfer-manager).  



## <a name="prestage-content"></a>Preconfigurar el contenido  
 Preconfigurar el contenido es un proceso de transferencia de contenido a un punto de distribución sin distribuirlo a través de la red.  

 Para obtener más información, consulte [Administración del ancho de banda de red](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).
