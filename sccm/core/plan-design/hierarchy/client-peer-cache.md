---
title: "Caché del mismo nivel de cliente"
titleSuffix: Configuration Manager
description: "Use la caché del mismo nivel de cliente para las ubicaciones de origen de contenido cuando se distribuya contenido con System Center Configuration Manager."
ms.custom: na
ms.date: 12/07/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: "3"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: cadc62ab21ac8cd43120a5baa79dd635a12b4069
ms.sourcegitcommit: 2dc9c83e57e9734ffc4a93f79cd71285036eeb8b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/07/2017
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Caché del mismo nivel para clientes de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Comenzando por la versión 1610 de System Center Configuration Manager, puede usar la **Caché del mismo nivel** para ayudar a administrar la implementación de contenido a los clientes en ubicaciones remotas. La caché del mismo nivel es una solución integrada de Configuration Manager que permite que los clientes compartan contenido con otros clientes directamente desde su caché local.   

> [!TIP]  
> Esta característica se introdujo por primera vez en la versión 1610 como un [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). A partir de la versión 1710, ya no es una característica de versión preliminar.

## <a name="overview"></a>Información general
Un cliente de la caché del mismo nivel es un cliente de Configuration Manager que está habilitado para usar el almacenamiento en la caché del mismo nivel. Un cliente de la caché del mismo nivel que tenga contenido que puede compartir con otros clientes es un origen de la caché del mismo nivel.
 -  Use la configuración de cliente para configurar los clientes y usar la caché del mismo nivel.
 -  Para compartir el contenido como origen de la caché del mismo nivel, un cliente de la caché del mismo nivel debe cumplir los requisitos siguientes:
    -  Debe estar unido a un dominio. Sin embargo, un cliente que no esté unido a un dominio podrá obtener contenido de un origen de la caché del mismo nivel unido a dominio.
    -  Debe ser miembro del grupo de límites actual del cliente que está buscando el contenido. Un cliente de la caché del mismo nivel en grupos de límites vecino no está incluido con el grupo de ubicaciones de origen de contenido disponibles cuando un cliente usa la reserva para buscar contenido de un grupo de límites vecino. Para más información acerca de los grupos de límites actuales y vecinos, vea [Grupos de límites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - Todos los tipos de contenido que se conservan en la memoria caché del cliente de Configuration Manager pueden proporcionarse a otros clientes mediante la caché del mismo nivel, incluidos archivos de Office 365 y archivos de instalación rápida.<!--SMS.500850-->
 -  La caché del mismo nivel no reemplaza el uso de otras soluciones como BranchCache, sino que funciona en paralelo para ofrecerle más opciones que amplíen las tradicionales soluciones de implementación de contenido, como los puntos de distribución. Se trata de una solución personalizada sin ninguna dependencia de BranchCache, por lo que seguirá funcionando aunque no habilite o use Windows BranchCache.

### <a name="operations"></a>Operaciones

Después de implementar la configuración de cliente que habilita la caché del mismo nivel en una colección, los miembros de esa colección pueden actuar como origen de contenido del mismo nivel para otros clientes en el mismo grupo de límites:
 -  El cliente que actúa como origen de contenido del mismo nivel envía una lista de contenido almacenado en caché disponible a su punto de administración.
 -  A continuación, cuando el siguiente cliente en ese grupo de límites solicita contenido, cada origen de la caché del mismo nivel que tiene el contenido se devuelve como un origen de contenido posible junto con los puntos de distribución y otras ubicaciones de origen de contenido en ese grupo de límites.
 -  Según el proceso de funcionamiento normal, el cliente que busca el contenido selecciona un origen de contenido del conjunto de orígenes que se proporciona y, después, intenta obtener el contenido.

> [!NOTE]
> Si se produce una reserva para un grupo de límites vecino para el contenido, las ubicaciones de origen de contenido de la caché del mismo nivel del grupo de límites vecino no se agregan al grupo del cliente de ubicaciones de origen de contenido potenciales.  


Aunque puede hacer que todos los clientes participen como un origen de la caché del mismo nivel, es recomendable elegir solo los clientes que mejor se adapten a ser orígenes de la caché del mismo nivel.  Puede evaluar la idoneidad de los clientes en función del tipo de chasis de un cliente, el espacio en disco, la conectividad de red y mucho más. Para obtener más información que pueda ayudarle a seleccionar los mejores clientes para la caché del mismo nivel, vea [este blog de un consultor de Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Acceso limitado al origen de almacenamiento en caché del mismo nivel**  
A partir de la versión 1702, un equipo de origen de almacenamiento en caché del mismo nivel rechazará una solicitud de contenido cuando el equipo de origen de almacenamiento en caché del mismo nivel cumpla alguna de las condiciones siguientes:  
  -  Está en modo de batería baja.
  -  La carga de CPU supera el 80 % en el momento en que se solicita el contenido.
  -  E/S de disco tiene un valor *AvgDiskQueueLength* superior a 10.
  -  No hay más conexiones disponibles para el equipo.   

Puede configurar estas opciones mediante la clase WMI del servidor de configuración de cliente para la característica de origen del mismo nivel (*SMS_WinPEPeerCacheConfig*) cuando se usa el SDK de System Center Configuration Manager.

Cuando el equipo rechaza una solicitud del contenido, el equipo solicitante continuará buscando el contenido en orígenes alternativos en su grupo de ubicaciones de origen de contenido disponibles.   



### <a name="monitoring"></a>monitoring   
Para ayudarle a entender el uso de la caché del mismo nivel, puede ver el panel Orígenes de datos de cliente. Vea [Panel de orígenes de datos de cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

A partir de la versión 1702, puede usar tres informes para ver el uso de la caché del mismo nivel. En la consola, vaya a **Supervisión** > **Crear informes** > **Informes**. Todos los informes tienen un tipo de **contenido de distribución de software**:
1.  **Rechazo del contenido de origen de la caché del mismo nivel**:  
Utilice este informe para conocer la frecuencia con que los orígenes de la caché del mismo nivel de un grupo de límites rechazan una solicitud de contenido.
 - **Problema conocido:** al desglosar resultados como *MaxCPULoad* o *MaxDiskIO*, es posible que reciba un error que sugiere que no se puede encontrar el informe o los detalles. Como solución alternativa, use los dos informes siguientes, donde se muestran los resultados directamente.

2. **Rechazo del contenido de origen de la caché del mismo nivel según la condición**:  
Utilice este informe para conocer los detalles de rechazo de un tipo de rechazo o grupo de límites específico. Puede especificar

  - **Problema conocido:** no puede seleccionar de entre los parámetros disponibles y, en su lugar, debe escribirlos manualmente. Escriba los valores de *Nombre del grupo de límites* y *Tipo de rechazo* tal como se muestra en el primer informe. Por ejemplo, para *Tipo de rechazo* puede escribir *MaxCPULoad* o *MaxDiskIO*.

3. **Detalles del rechazo del contenido de origen de la caché del mismo nivel**:   
  Utilice este informe para conocer el contenido que se solicitaba cuando se rechazó.

 - **Problema conocido:** no puede seleccionar de entre los parámetros disponibles y, en su lugar, debe escribirlos manualmente. Escriba el valor de *Tipo de rechazo* como se muestra en el primer informe (Rechazo del contenido de origen de la caché del mismo nivel) y después escriba el *Id. de recurso* del origen de contenido sobre el que desea obtener más información.  Para buscar el identificador de recurso del origen de contenido:  

    1. Busque el nombre del equipo que se muestra como el *Origen de caché del mismo nivel* en los resultados del segundo informe (Rechazo del contenido de origen de la caché del mismo nivel según la condición).  
    2. A continuación, vaya a **Activos y compatibilidad** > **Dispositivos** y después busque ese nombre de equipos. Utilice el valor de la columna de identificador de recurso.  


## <a name="requirements-and-considerations-for-peer-cache"></a>Requisitos y consideraciones de la caché del mismo nivel
-   El almacenamiento en caché del mismo nivel es compatible con cualquier sistema operativo de Windows admitido como cliente de Configuration Manager. No se admiten sistemas operativos que no son Windows para el almacenamiento en caché del mismo nivel.

-   Los clientes solo pueden transferir contenido desde los clientes de la caché del mismo nivel que están en su actual grupo de límites.

-   Antes de la versión 1706, los sitios en los que los clientes usen la caché del mismo nivel deben estar configurados con una [cuenta de acceso de red](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account). A partir de la versión 1706, que cuenta ya no es necesaria con una excepción.  La excepción es cuando un cliente usa la caché del mismo nivel para obtener y ejecutar una secuencia de tareas desde el Centro de software, y la secuencia de tareas reinicia el cliente en WinPE.  En este escenario, el cliente seguirá necesitando la cuenta de acceso de red cuando se encuentra en WinPE para poder acceder al origen de la caché del mismo nivel y obtener el contenido.

    Cuando se requiere, el equipo de origen de la caché del mismo nivel usa dicha cuenta para autenticar las solicitudes de elementos del mismo nivel, acción para la que solo se necesitan permisos de usuario de dominio.

-   Dado que el límite actual de un origen de contenido de la caché del mismo nivel viene determinado por el último envío de inventario de hardware del cliente, si un cliente se mueve a una ubicación de red y se encuentra en un grupo de límites diferente, podría seguir considerándose miembro de su grupo de límites anterior para la caché del mismo nivel. Esto puede dar lugar a que un cliente ofrezca un origen de contenido de la caché del mismo nivel que no está en su ubicación de red inmediata. Se recomienda excluir del origen de la caché del mismo nivel a los clientes que son propensos a esta configuración.

## <a name="to-configure-client-peer-cache-client-settings"></a>Para configurar las opciones de cliente de la caché del mismo nivel de cliente
1.  En la consola de Configuration Manager, vaya a **Administración** > **Configuración de cliente** y, luego, abra el objeto de configuración de cliente de dispositivo que quiera usar. También puede modificar el objeto Configuración de cliente predeterminada.
2.  En la lista de configuraciones disponibles, seleccione **Configuración de caché de cliente**.
3.  **Habilite el cliente de Configuration Manager en el SO completo para compartir contenido** en **Sí**.
4.  Configure las siguientes opciones para definir los puertos que desea utilizar para la caché del mismo nivel:  
  -  **Puerto para difusión de red inicial**
  -  **Habilitar HTTPS para la comunicación del mismo nivel del cliente**
  -  **Puerto para descarga de contenido desde nivel (HTTP/HTTPS)**

En cada equipo habilitado para la caché del mismo nivel, si el Firewall de Windows está en uso, Configuration Manager lo configura para que permita el uso de los puertos que se establezcan.
