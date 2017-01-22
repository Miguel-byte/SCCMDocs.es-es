---
title: "Grupos de límites para las versiones 1511, 1602 y 1606 | System Center Configuration Manager"
description: "Use grupos de límites con las versiones 1511, 1602 y 1606 de Configuration Manager."
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: b64f1f06af1ab4a255b6291b6eb5f85cff99ae63
ms.openlocfilehash: ef408041eb6d0d6716e244d34b9a2a4ebe5cb9cc


---
# <a name="boundary-groups-for-system-center-configuration-manager-version-1511-1602-and-1606"></a>Grupos de límites para las versiones 1511, 1602 y 1606 de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La información de este tema es específica para el uso de grupos de límites con las versiones 1511, 1602 y 1606 de System Center Configuration Manager.
Si usa la versión 1610 o posterior, consulte [Grupos de límites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-group/) en *Define site boundaries and bondary groups or System Center Configuration Manager (Definir límites de sitio y grupos de límites en System Center Configuration Manager)* para obtener información sobre el uso de los grupos de límites rediseñados.  


##  <a name="a-namebkmkboundarygroupsa-boundary-groups"></a><a name="BKMK_BoundaryGroups"></a> Boundary groups  
 Cree grupos de límites para agrupar de forma lógica las ubicaciones de red (límites) de manera que su infraestructura de red resulte más fácil de administrar. Debe asignar límites a grupos de límites para poder utilizar el grupo de límites. Los clientes usan la configuración de grupos de límites para lo siguiente:  

-   Asignación automática de sitio  

-   Ubicación del contenido  

-   Puntos de administración preferidos (si va a usar los puntos de administración preferidos, debe habilitar esta opción para la jerarquía y no desde la configuración del grupo de límites. Vea el siguiente procedimiento *Para habilitar el uso de puntos de administración preferidos*)  

Al configurar grupos de límites, se agregan uno o varios límites al grupo de límites y después se especifican los valores de configuración adicionales que usarán los clientes ubicados en esos límites.  

#### <a name="to-create-a-boundary-group"></a>Para crear un grupo de límites  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de jerarquía** >  **Grupos de límites**.  

2.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear grupo de límites**.  

3.  En el cuadro de diálogo **Crear grupo de límites** , seleccione la pestaña **General** y especifique un **Nombre** para este grupo de límites.  

4.  Haga clic en **Aceptar** para guardar el nuevo grupo de límites.  

#### <a name="to-configure-a-boundary-group"></a>Para configurar un grupo de límites  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de jerarquía** >  **Grupos de límites**.  

2.  Seleccione el grupo de límites que desea modificar.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades** para el grupo de límites, seleccione la pestaña **General** para modificar los límites que son miembros de este grupo de límites:  

    -   Para agregar límites, haga clic en **Agregar**, seleccione la casilla para uno o más límites y, a continuación, haga clic en **Aceptar**.  

    -   Para quitar límites, seleccione el límite y haga clic en **Quitar**.  

5.  Seleccione la pestaña **Referencias** para modificar la configuración de asignación de sitio y del servidor del sistema de sitio asociado:  

    -   Para habilitar este grupo de límites para que lo usen los clientes para asignación de sitio, seleccione la casilla correspondiente a **Usar este grupo de límites para la asignación de sitio**y, a continuación, seleccione un sitio en la lista desplegable **Sitio asignado** .  

    -   Para configurar qué servidores del sistema sitio disponibles están asociados a este grupo de límites:  

    1.  Haga clic en **Agregar**y, a continuación, seleccione la casilla para uno o más servidores. Los servidores se agregan como servidores del sistema de sitio asociados para este grupo de límites. Solo están disponibles los servidores que admitieron el rol de sistema de sitio que se instaló en ellos.  

        > [!NOTE]  
        >  Puede seleccionar cualquier combinación de sistemas de sitio disponibles en cualquier sitio de la jerarquía. Los sistemas de sitio seleccionados se muestran en la pestaña **Sistemas de sitio** en las propiedades de cada límite miembro de este grupo de límites.  

    2.  Para quitar un servidor de este grupo de límites, seleccione el servidor y, a continuación, haga clic en **Quitar**.  

        > [!NOTE]  
        >  Para que este grupo de límites deje de usarse para asociar sistemas de sitio, debe quitar todos los servidores que se enumeran como servidores de sistema de sitio asociados.  

    3.  Para cambiar la velocidad de conexión de red para un servidor de sistema de sitio para este grupo de límites, seleccione el servidor y, a continuación, haga clic en **Cambiar conexión**.  

         De forma predeterminada, la velocidad de conexión para cada sistema de sitio es **Rápida**, pero puede cambiarse a **Lenta**. La velocidad de conexión de red y la configuración de una implementación determinan si un cliente puede descargar contenido desde el servidor.  

6.  Haga clic en **Aceptar** para cerrar las propiedades del grupo de límites y guardar la configuración.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Para asociar un servidor de implementación de contenido o un grupo de administración a un grupo de límites  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de jerarquía** >  **Grupos de límites**.  

2.  Seleccione el grupo de límites que desea modificar.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades** correspondiente al grupo de límites, seleccione la pestaña **Referencias** .  

5.  En **Seleccionar servidores de sistema de sitio**, haga clic en **Agregar**, seleccione la casilla correspondiente a los servidores de sistema de sitio que desea asociar con este grupo de límites y después haga clic en **Aceptar**.  

6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo y guardar la configuración del grupo de límites.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Para habilitar el uso de puntos de administración preferidos  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de sitio** > **Sitios** y, después, en la pestaña **Inicio**, seleccione **Configuración de jerarquía**.  

2.  En la pestaña **General** de la Configuración de jerarquía, seleccione **Los clientes prefieren usar puntos de administración especificados en grupos de límites**.  

3.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo y guardar la configuración.  

#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>Para configurar un sitio de reserva para asignación de sitio automática  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración del sitio** >  **Sitios**.  

2.  En la pestaña **Inicio** , en el grupo **Sitios** , haga clic en **Configuración de jerarquía**.  

3.  En la pestaña **General** , seleccione la casilla de verificación para **Usar un sitio de reserva**y, a continuación, seleccione un sitio en la lista desplegable **Sitio de reserva** .  

4.  Haga clic en **Aceptar** para guardar la configuración.  

 Las secciones siguientes proporcionan detalles adicionales sobre las configuraciones de grupos de límites.  

###  <a name="a-namebkmkboundarysiteassignmenta-about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> Información sobre la asignación de sitio  
 Puede configurar cada grupo de límites con un sitio asignado para los clientes.  

-   Un cliente recién instalado que usa la asignación automática de sitio se unirá al sitio asignado de un grupo de límites que contiene la ubicación de red actual del cliente.  

-   Una vez recibida la asignación a un sitio, el cliente no la modifica al cambiar la ubicación de red. Por ejemplo, si el cliente se mueve a una nueva ubicación de red representada por un límite en un grupo de límites con una asignación de sitio diferente, el sitio asignado del cliente no se modificará.  

-   Cuando la detección de sistemas de Active Directory detecta un nuevo recurso, la información de red para el recurso detectado se evalúa en relación con los límites en los grupos de límites. Este proceso asocia el nuevo recurso con un sitio asignado para que use el método de instalación de inserción de cliente.  

-   Cuando un límite es miembro de varios grupos de límites que tienen diferentes sitios asignados, los clientes seleccionarán uno de los sitios de forma aleatoria.  

-   Los cambios que se realicen a un sitio de grupo de límites asignado solo se aplicarán a las nuevas acciones de asignación de sitio. Los clientes previamente asignados a un sitio no vuelven a evaluar su asignación de sitio según los cambios en la configuración de un grupo de límites (o en su propia ubicación de red).  

Para obtener más información sobre la asignación de sitio de cliente, consulte [Using Automatic Site Assignment for Computers](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) (Uso de la asignación de sitio automática para los equipos) en [How to assign clients to a site in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md) (Cómo asignar clientes a un sitio en System Center Configuration Manager).  

###  <a name="a-namebkmkboundarycontentlocationa-about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> Información sobre la ubicación del contenido  
 Puede configurar cada uno de los grupos de límites con uno o varios puntos de distribución y puntos de migración de estado, y puede asociar los mismos puntos de distribución y puntos de migración de estado con varios grupos de límites.  

-   **Durante la distribución de software**, los clientes solicitan una ubicación para el contenido de la implementación. Configuration Manager envía al cliente una lista de puntos de distribución asociados a cada grupo de límites que incluye la ubicación de red actual del cliente.  

-   **Durante la implementación de sistema operativo, los clientes** solicitan una ubicación para enviar o recibir su información de estado de la migración. Configuration Manager envía al cliente una lista de puntos de migración de estado asociados a cada grupo de límites que incluye la ubicación de red actual del cliente.  

Este comportamiento permite al cliente seleccionar el servidor más cercano desde el que se va a transferir el contenido o información de migración de estado.  

###  <a name="a-namebkmkpreferredmpa-about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> Información sobre los puntos de administración preferidos  
 Los puntos de administración preferidos permiten que un cliente identifique un punto de administración asociado con su ubicación de red (límite) actual.  

-   Un cliente intenta usar un punto de administración preferido de su sitio asignado antes de usar un punto de administración de su sitio asignado que no está configurado como el preferido.  

-   Para usar esta opción, debe habilitarla para la jerarquía y configurar grupos de límites en los sitios primarios individuales para que incluyan los puntos de administración que se deben asociar con esos límites asociados del grupo de límites.  

-   Cuando se configuran los puntos de administración preferidos y un cliente organiza su lista de puntos de administración, el cliente coloca los puntos de administración preferidos en la parte superior de su lista de puntos de administración asignados (que incluye todos los puntos de administración del sitio asignado del cliente).  

> [!NOTE]  
>  Cuando un cliente activa la itinerancia (que significa cambiar sus ubicaciones de red, como por ejemplo, cuando se viaja con un equipo portátil a una ubicación de oficina remota), podría usar un punto de administración (o punto de administración proxy) desde el sitio local de su nueva ubicación, antes de intentar usar un punto de administración desde su sitio asignado (que incluye los puntos de administración preferidos).  Consulte [Understand how clients find site resources and services for System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) (Comprender cómo los clientes buscan servicios y recursos de sitio para System Center Configuration Manager) para obtener más información.  

###  <a name="a-namebkmkboundaryoverlapa-about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> Información sobre la superposición de límites  
 Configuration Manager admite configuraciones de límites que se superponen para la ubicación del contenido:  

-   **Cuando un cliente solicita contenido** y la ubicación de red del cliente pertenece a varios grupos de límites, Configuration Manager envía al cliente una lista de todos los puntos de distribución que tienen el contenido.  

-   **Cuando un cliente solicita a un servidor que envíe o reciba información de su migración de estado** y la ubicación de red del cliente pertenece a varios grupos de límites, Configuration Manager envía al cliente una lista de todos los puntos de migración de estado asociados a un grupo de límites que incluye la ubicación de red actual del cliente.  

Este comportamiento permite al cliente seleccionar el servidor más cercano desde el que se va a transferir el contenido o información de migración de estado.  

###  <a name="a-namebkmkboudnarynetworkspeeda-about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a> Información sobre la velocidad de conexión de red  
 Puede establecer la velocidad de conexión de red para cada servidor de sistema de sitio en un grupo de límites. Esta configuración se aplica a los clientes que se conectan a un sistema de sitio basado en esta configuración de grupos de límites. El mismo servidor de sistema de sitio puede tener diferentes velocidades de conexión establecidas para distintos grupos de límites.  

 De forma predeterminada, la velocidad de conexión de red se configura como **Rápida**, pero también se puede configurar como **Lenta**. La velocidad de conexión de red y la configuración de implementación determinan si un cliente puede descargar contenido desde un punto de distribución cuando el cliente está en un grupo de límites asociado.  

 Para obtener más información sobre cómo la configuración de velocidad de conexión de red afecta a la forma en que los clientes obtienen el contenido, consulte [Content source location scenarios](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md) (Escenarios de ubicación de origen de contenido).  



<!--HONumber=Dec16_HO3-->


