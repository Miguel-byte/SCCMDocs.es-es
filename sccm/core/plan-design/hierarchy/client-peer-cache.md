---
title: "Caché del mismo nivel de cliente | System Center Configuration Manager"
description: "Use la caché del mismo nivel de cliente para las ubicaciones de origen de contenido cuando se distribuya contenido con System Center Configuration Manager."
ms.custom: na
ms.date: 12/05/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3329c3180899a4de96f5d9fed46f97744cf5e7da
ms.openlocfilehash: e983358e32502a130f95647a11cd73ff4bbef05f

---
# <a name="peer-cache-for-configuration-manager-clients"></a>Caché del mismo nivel para clientes de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Comenzando por la versión 1610 de System Center Configuration Manager, puede usar la **Caché del mismo nivel** para ayudar a administrar la implementación de contenido a los clientes en ubicaciones remotas. Caché del mismo nivel es una solución integrada de Configuration Manager para que los clientes compartan contenido con otros clientes directamente desde su caché local.   

> [!TIP]  
> Con la versión 1610, el panel de orígenes de datos de cliente y la caché del mismo nivel son funciones de la versión preliminar. Para habilitarlos, vea [Uso de características de la versión preliminar a partir de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

 -  Use la configuración de cliente para configurar los clientes y usar la caché del mismo nivel.
 -  Para compartir el contenido, los clientes de la caché del mismo nivel deben ser miembros del grupo de límite actual del cliente que busca el contenido. Los clientes de la caché del mismo nivel en grupos de límites vecino no están incluidos con el grupo de ubicaciones de origen de contenido disponibles cuando un cliente usa la reserva para buscar contenido de un grupo de límites vecino. Para más información acerca de los grupos de límites actuales y vecinos, vea [Grupos de límites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 -  Cada tipo de contenido que se mantiene en la caché del cliente de Configuration Manager puede proporcionarse a otros clientes mediante la caché del mismo nivel.
 -  La Caché del mismo nivel no reemplaza el uso de otras soluciones como BranchCache, sino que funciona en paralelo para ofrecerle más opciones que amplíen las tradicionales soluciones de implementación de contenido (como los puntos de distribución). Como una solución personalizada sin ninguna dependencia en BranchCache, si no habilita o usa Windows BranchCache, esta solución sigue funcionando.

Después de implementar la configuración de cliente que habilita la caché del mismo nivel en una colección, los miembros de esa colección pueden actuar como origen de contenido del mismo nivel para otros clientes en el mismo grupo de límites:
 -  El cliente que actúa como origen de contenido del mismo nivel enviará una lista de contenido disponible que ha almacenado en caché a su punto de administración.
 -  A continuación, cuando el siguiente cliente en ese grupo de límites solicita contenido, cada origen de la caché del mismo nivel que tiene el contenido se devuelve como un origen de contenido posible junto con los puntos de distribución y otras ubicaciones de origen de contenido en ese grupo de límites.
 -  Según el proceso de funcionamiento normal, el cliente que busca el contenido selecciona un origen de contenido del conjunto de orígenes que se proporciona y continúa intentando obtener el contenido.
 -  Si se produce una reserva para un grupo de límites vecino para el contenido, las ubicaciones de origen del contenido de la caché del mismo nivel del grupo de límites vecino no se agregan al grupo de clientes de ubicaciones de origen de contenido potenciales.  

Aunque podría hacer que todos los clientes participaran en la caché del mismo nivel, es recomendable elegir solo los clientes que mejor se adapten a ser orígenes de la caché del mismo nivel.  Puede evaluar la idoneidad de los clientes basándose en el tipo de chasis de un cliente, el espacio en disco, la conectividad de red y mucho más. Para obtener más información que pueda ayudarle a seleccionar los mejores clientes para la caché del mismo nivel, vea [este blog con un consultor de Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

Para ayudarle a entender el uso de la caché del mismo nivel, puede ver el panel Orígenes de datos de cliente. Vea [Panel de orígenes de datos de cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## <a name="requirements-and-considerations-for-peer-cache"></a>Requisitos y consideraciones de la caché del mismo nivel:
- Debe configurar el sitio con una **Cuenta de acceso a la red** que tenga **Control total** sobre la carpeta de caché en cada cliente. De forma predeterminada, es ***%windir%\ccmcache***.

- Los clientes solo pueden transferir contenido desde los clientes de la caché del mismo nivel que están en su actual grupo de límites.

-   Dado que el límite actual de un origen de contenido de la caché del mismo nivel viene determinado por que esos clientes conserven el envío del inventario de hardware, un cliente que se mueve a una ubicación de red e un grupo de límites diferente podría considerarse un miembro de su grupo de límites anterior para la caché del mismo nivel. Esto puede dar lugar a que un cliente ofrezca un origen de contenido de la caché del mismo nivel que no está en su ubicación de red inmediata. Se recomienda excluir los clientes que son propensos a esta configuración de la caché del mismo nivel.

## <a name="to-configure-client-peer-cache-client-settings"></a>Para configurar las opciones de cliente de la caché del mismo nivel de cliente
1.  En la consola de Configuration Manager, vaya a **Administración** > **Configuración de cliente** y luego abra el objeto de configuración de cliente de dispositivo que quiera usar. También puede modificar el objeto Configuración de cliente predeterminada.
2.  En la lista de configuraciones disponibles, seleccione **Configuración de caché de cliente**.
3.  **Habilite el cliente de Configuration Manager en el SO completo para compartir contenido** en **Sí**.
4.  Configure las siguientes opciones para definir los puertos que desea utilizar para la caché del mismo nivel:  
  -  **Puerto para difusión de red inicial**
  -  **Habilitar HTTPS para la comunicación del mismo nivel del cliente**
  -  **Puerto para descarga de contenido desde nivel (HTTP/HTTPS)**

En cada equipo habilitado para la caché del mismo nivel, si el Firewall de Windows está en uso, Configuration Manager se configura para permitir el uso de los puertos que configure.



<!--HONumber=Dec16_HO3-->


