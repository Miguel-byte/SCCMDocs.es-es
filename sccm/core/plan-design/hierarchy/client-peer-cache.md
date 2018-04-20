---
title: Caché del mismo nivel de cliente
titleSuffix: Configuration Manager
description: Use la caché del mismo nivel de cliente para las ubicaciones de origen de contenido cuando se distribuya contenido con System Center Configuration Manager.
ms.custom: na
ms.date: 04/10/2018
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 99eef9faf6ac66f65d16020b703e3a64d9beb9d0
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Caché del mismo nivel para clientes de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

<!--1101436-->
Use **Caché del mismo nivel** para ayudar a administrar la implementación de contenido en los clientes en ubicaciones remotas. La caché del mismo nivel es una solución integrada de Configuration Manager que permite que los clientes compartan contenido con otros clientes directamente desde su caché local.   

> [!TIP]  
> Esta característica se introdujo por primera vez en la versión 1610 como un [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). A partir de la versión 1710, ya no es una característica de versión preliminar.  


> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para más información, vea [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


## <a name="overview"></a>Información general
Un cliente de la caché del mismo nivel es un cliente de Configuration Manager que está habilitado para usar el almacenamiento en la caché del mismo nivel. Un cliente de la caché del mismo nivel que tenga contenido que puede compartir con otros clientes es un origen de la caché del mismo nivel.
 -  Use la configuración de cliente para configurar los clientes y usar la caché del mismo nivel.
 -  Para compartir el contenido como origen de la caché del mismo nivel, un cliente de la caché del mismo nivel debe cumplir los requisitos siguientes:
    -  Debe estar unido a un dominio. Sin embargo, un cliente que no esté unido a un dominio podrá obtener contenido de un origen de la caché del mismo nivel unido a dominio.
    -  Debe ser miembro del grupo de límites actual del cliente que está buscando el contenido. Cuando un cliente usa la reserva para buscar contenido de un grupo de límites vecino, la lista de ubicaciones de origen de contenido no incluye un cliente de la caché del mismo nivel en un grupo de límites vecino. Para más información acerca de los grupos de límites actuales y vecinos, vea [Grupos de límites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - El cliente de Configuration Manager proporciona todos los tipos de contenido en la caché a otros clientes mediante la caché del mismo nivel. Este contenido incluye archivos de Office 365 y de instalación rápida.<!--SMS.500850-->
 -  La caché del mismo nivel no reemplaza el uso de otras soluciones como BranchCache. La caché del mismo nivel funciona junto con otras soluciones para ofrecer más opciones para extender las soluciones tradicionales de implementación de contenido (como puntos de distribución). La caché del mismo nivel es una solución personalizada que no depende de BranchCache. Si no habilita o usa Windows BranchCache, la caché del mismo nivel sigue funcionando.

### <a name="operations"></a>Operaciones

Para habilitar la caché del mismo nivel, implemente la configuración de cliente en una colección. Después, los miembros de esa colección actúan como un origen de contenido del mismo nivel para otros clientes en el mismo grupo de límites.
 -  El cliente que actúa como origen de contenido del mismo nivel envía una lista de contenido almacenado en caché disponible a su punto de administración.
 -  Cuando el cliente siguiente en ese grupo de límites solicita ese contenido, cada origen de caché del mismo nivel, que tiene el contenido y está en línea, se devuelve en la lista de posibles orígenes de contenido. En esta lista también se incluyen puntos de distribución y otras ubicaciones de origen de contenido de ese grupo de límites.
 -  En el proceso normal, el cliente que busca el contenido selecciona un origen de la lista proporcionada. Después, el cliente intenta obtener el contenido.

> [!NOTE]
> Si el cliente reserva el contenido en un grupo de límites vecino, no agrega las ubicaciones de origen de contenido de la caché del mismo nivel del grupo de límites vecino a la lista de ubicaciones de origen de contenido potenciales.  


El procedimiento recomendado es elegir solo los clientes más adecuados como orígenes de caché del mismo nivel. Evalúe la idoneidad del cliente en función de atributos como el tipo de chasis, el espacio en disco y la conectividad de red. Para obtener más información que pueda ayudarle a seleccionar los mejores clientes para la caché del mismo nivel, vea [este blog de un consultor de Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Acceso limitado al origen de almacenamiento en caché del mismo nivel**  
A partir de la versión 1702, un equipo de origen de almacenamiento en caché del mismo nivel rechaza una solicitud de contenido cuando el equipo de origen de almacenamiento en caché del mismo nivel cumple alguna de las condiciones siguientes:  
  -  Está en modo de batería baja.
  -  La carga de CPU supera el 80 % en el momento en que se solicita el contenido.
  -  E/S de disco tiene un valor *AvgDiskQueueLength* superior a 10.
  -  No hay más conexiones disponibles para el equipo.   

Configure estas opciones mediante la clase WMI del servidor de configuración de cliente para la característica de origen del mismo nivel (*SMS_WinPEPeerCacheConfig*) en el SDK de Configuration Manager.

Cuando el equipo rechaza una solicitud del contenido, el equipo solicitante continúa buscando el contenido en la lista de ubicaciones de origen de contenido disponibles.   



### <a name="monitoring"></a>monitoring   
Para ayudarle a entender el uso de la caché del mismo nivel, puede ver el panel Orígenes de datos de cliente. Vea [Panel de orígenes de datos de cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

A partir de la versión 1702, puede usar tres informes para ver el uso de la caché del mismo nivel. En la consola, vaya a **Supervisión** > **Crear informes** > **Informes**. Todos los informes tienen un tipo de **contenido de distribución de software**:
1.  **Rechazo del contenido de origen de la caché del mismo nivel**:  
Use este informe para conocer la frecuencia con que los orígenes de la caché del mismo nivel de un grupo de límites rechazan una solicitud de contenido.
 - **Problema conocido:** al desglosar resultados como *MaxCPULoad* o *MaxDiskIO*, es posible que reciba un error que sugiere que no se puede encontrar el informe o los detalles. Como solución alternativa, use los dos informes siguientes que muestran los resultados directamente.

2. **Rechazo del contenido de origen de la caché del mismo nivel según la condición**:  
Utilice este informe para conocer los detalles de rechazo de un tipo de rechazo o grupo de límites específico. Puede especificar

  - **Problema conocido:** no puede seleccionar de entre los parámetros disponibles y, en su lugar, debe escribirlos manualmente. Escriba los valores de *Nombre del grupo de límites* y *Tipo de rechazo* tal como se muestra en el primer informe. Por ejemplo, para *Tipo de rechazo* puede escribir *MaxCPULoad* o *MaxDiskIO*.

3. **Detalles del rechazo del contenido de origen de la caché del mismo nivel**:   
  Use este informe para conocer el contenido que el cliente solicitaba cuando se rechazó.

 - **Problema conocido:** no puede seleccionar de entre los parámetros disponibles y, en su lugar, debe escribirlos manualmente. Escriba el valor para *Tipo de rechazo* como se muestra en el informe **Rechazo del contenido de origen de la caché del mismo nivel**. Después, escriba el *Id. del recurso* para el origen de contenido sobre el que quiera obtener más información. Para buscar el identificador de recurso del origen de contenido:  

    1. Busque el nombre de equipo que se muestra como *Origen de caché del mismo nivel* en los resultados del informe **Rechazo del contenido de origen de la caché del mismo nivel por condición**.  
    2. A continuación, vaya a **Activos y compatibilidad** > **Dispositivos** y después busque ese nombre de equipos. Utilice el valor de la columna de identificador de recurso.  


## <a name="requirements-and-considerations-for-peer-cache"></a>Requisitos y consideraciones de la caché del mismo nivel
-   El almacenamiento en caché del mismo nivel es compatible con cualquier sistema operativo de Windows admitido como cliente de Configuration Manager. No se admiten sistemas operativos que no son Windows para el almacenamiento en caché del mismo nivel.

-   Los clientes solo pueden transferir contenido desde los clientes de la caché del mismo nivel que están en su actual grupo de límites.

-   Antes de la versión 1706, los sitios en los que los clientes usen la caché del mismo nivel deben estar configurados con una [cuenta de acceso de red](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account). A partir de la versión 1706, que cuenta ya no es necesaria con una excepción. El escenario de excepción es cuando un cliente que admite la caché del mismo nivel ejecuta una secuencia de tareas desde el Centro de software, y la secuencia de tareas reinicia el cliente en una imagen de arranque. En este escenario, el cliente sigue necesitando la cuenta de acceso a la red. Cuando el cliente está en Windows PE, usa la cuenta de acceso a la red para obtener contenido desde el origen de caché del mismo nivel.

    Cuando es necesario, el equipo de origen de memoria caché del mismo nivel usa la cuenta de acceso a la red para autenticar las solicitudes de descarga de elementos del mismo nivel. Esta cuenta solo requiere permisos de usuario de dominio para este propósito.

-   El último envío de inventario de hardware del cliente determina el límite actual de un origen de contenido de la caché del mismo nivel. Es posible que un cliente que se desplaza a un grupo de límites diferente siga siendo miembro de su grupo de límites anterior a efectos de la caché del mismo nivel. Este comportamiento da lugar a que un cliente ofrezca un origen de contenido de la caché del mismo nivel que no está en su ubicación de red inmediata. Se recomienda excluir del origen de la caché del mismo nivel a los clientes que son propensos a esta configuración.
-    A partir de la versión 1706, el cliente de caché del mismo nivel valida en primer lugar si el origen de contenido de la caché del mismo nivel está en línea antes de intentar descargar el contenido. <!--sms.498675-->

## <a name="to-configure-client-peer-cache-client-settings"></a>Para configurar las opciones de cliente de la caché del mismo nivel de cliente
Para obtener información sobre cómo configurar las opciones de cliente, vea [Configuración de la memoria caché del cliente](/sccm/core/clients/deploy/about-client-settings#client-cache-settings). Para obtener más información, vea [Cómo configurar el cliente](/sccm/core/clients/deploy/configure-client-settings).

En los clientes que admiten la caché del mismo nivel que usan el Firewall de Windows, Configuration Manager configura los puertos de firewall que se especifiquen en la configuración de cliente.
