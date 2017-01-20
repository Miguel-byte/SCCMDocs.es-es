---
title: "Definir los límites del sitio | System Center Configuration Manager"
description: "Obtenga información sobre cómo definir ubicaciones de red de la intranet que pueden contener los dispositivos que quiere administrar."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9df8b5d5fd67a5ced5860771295d05dfb56a3982


---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>Definir los límites del sitio y los grupos de límites para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los límites de System Center Configuration Manager definen ubicaciones de red de la intranet que pueden contener los dispositivos que quiere administrar. Los grupos de límites son grupos lógicos de límites que puede configurar. Tanto los grupos de límites como los límites están disponibles en toda una jerarquía y no se pueden configurar para sitios independientes.  

 Una jerarquía puede contener cualquier número de grupos de límites, y cada uno de los grupos de límites puede contener cualquier combinación de los siguientes tipos de límites:  

-   Subred de IP,  

-   Nombre de sitio de Active Directory  

-   Prefijo IPv6  

-   Intervalo de direcciones IP  

Los clientes de la intranet evalúan su ubicación de red actual y después usan esa información para identificar los grupos de límites a los que pertenecen.  

 Los clientes usan grupos de límites para lo siguiente:  

-   **Encontrar un sitio asignado:** los grupos de límites permiten a los clientes buscar un sitio principal para la asignación de cliente (asignación automática de sitio).  

-   **Encontrar determinados roles de sistema de sitio que puedan usar:**  al asociar un grupo de límites con determinados roles de sistema de sitio, el grupo de límites proporciona esa lista de sistemas de sitio a los clientes para que la usen durante la ubicación de contenido y como puntos de administración preferidos.  

Los clientes que están en Internet o están configurados como clientes de Internet únicamente no usan la información de límites. Estos clientes no pueden usar la asignación automática de sitio y siempre pueden descargar contenido de cualquier punto de distribución desde su sitio asignado, si el punto de distribución se configura para permitir conexiones de cliente desde Internet.  


##  <a name="a-namebkmkboundariesa-boundaries"></a><a name="BKMK_Boundaries"></a> Límites  
 Puede crear límites independientes manualmente. Además, puede configurar la [Detección de bosques de Active Directory](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) para que detecte automáticamente y cree límites para las subredes IP y el sitio de Active Directory que detecte.  

-   Cada límite representa una ubicación de red y puede usarse en todos los sitios de la jerarquía.  

-   Configuration Manager no es compatible con la entrada directa de una superred como un límite. En su lugar, utilice el tipo de límite de intervalo de direcciones IP.  

-   Cuando la detección de bosques de Active Directory identifica una superred asignada a un sitio de Active Directory, Configuration Manager convierte la superred en un límite de intervalo de direcciones IP.  

-   El límite en el que se encuentra un cliente equivale al sitio de Active Directory, o a la dirección IP de red que el cliente identifica. (No es raro que un cliente use una dirección IP de la que el administrador de Configuration Manager no tiene constancia. Si tiene dudas sobre la ubicación de red de los clientes, confirme la ubicación que el cliente notifica mediante el comando **IPCONFIG** en el cliente.)  

Al crear un límite, este recibe automáticamente un nombre basado en el tipo y ámbito del límite. No se puede modificar este nombre. Pero, al configurar el límite, sí puede especificar una descripción que ayude a identificar el límite en la consola de Configuration Manager.  

 Después de crear un límite, puede modificar sus propiedades para hacer lo siguiente:  

-   Agregar el límite a uno o varios grupos de límites.  

-   Cambiar el tipo o el ámbito del límite.  

-   Ver la pestaña **Sistemas de sitio** del límite para ver qué servidores de sistema de sitio (puntos de distribución, puntos de migración de estado y puntos de administración) están asociados con el límite.  

#### <a name="to-create-a-boundary"></a>Para crear un límite  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de jerarquía** > **Límites**.  

2.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear Boundary.**.  

3.  En la pestaña **General** del cuadro de diálogo Crear límite, puede especificar una **Descripción** para identificar el límite con un nombre o referencia fácil de reconocer.  

4.  Seleccione un **Tipo** para este límite:  

    -   Si selecciona **Subred de IP**, debe especificar un **Id. de subred** para este límite.  

        > [!TIP]  
        >  Puede especificar la **Red** y la **Máscara de subred** para que el **Id. de subred** se especifique automáticamente. Cuando se guarda el límite, se guarda solo el valor de Id. de subred.  

    -   Si selecciona **Sitio de Active Directory**, debe especificarlo o **Examinar** para buscar un sitio de Active Directory en el bosque local del servidor de sitio.  

        > [!IMPORTANT]  
        >  Cuando se especifica un sitio de Active Directory para un límite, el límite incluye cada subred de IP que sea miembro de ese sitio de Active Directory. Si cambia la configuración del sitio de Active Directory en Active Directory, también cambiarán las ubicaciones de red incluidas en este límite.  

    -   Si selecciona **Prefijo IPv6**, debe especificar un **Prefijo** en el formato de prefijo IPv6.  

    -   Si selecciona **Intervalo de direcciones IP**, debe especificar una **Dirección IP inicial** y una **Dirección IP final** que incluya parte de una subred de IP o que incluya múltiples subredes de IP.  

5.  Haga clic en **Aceptar** para guardar el nuevo límite.  

#### <a name="to-configure-a-boundary"></a>Para configurar un límite  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de jerarquía** > **Límites**.  

2.  Seleccione el límite que desea modificar.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades** para el límite, seleccione la pestaña **General** para editar la **Descripción** o el **Tipo** para el límite. También puede cambiar el ámbito de un límite mediante la edición de las ubicaciones de red para el límite. Por ejemplo, para un límite de sitio de Active Directory, puede especificar un nuevo nombre de sitio de Active Directory.  

5.  Seleccione la pestaña **Sistemas de sitio** para ver los sistemas de sitio que están asociados con este límite. No puede cambiar esta configuración desde las propiedades de un límite.  

    > [!TIP]  
    >  Para que un servidor de sistema de sitio se muestre como sistema de sitio para un límite, el servidor de sistema de sitio debe estar asociado como servidor de sistema de sitio para, al menos, un grupo de límites que incluya este límite. Esto se configura en la pestaña **Referencias** de un grupo de límites.  

6.  Seleccione la pestaña **Grupos de límites** para modificar la pertenencia al grupo de límites de este límite:  

    -   Para agregar este límite a uno o más grupos de límites, haga clic en **Agregar**, seleccione la casilla para uno o más grupos de límites y, a continuación, haga clic en **Aceptar**.  

    -   Para quitar este límite de un grupo de límites, seleccione el grupo de límites y haga clic en **Quitar**.  

7.  Haga clic en **Aceptar** para cerrar las propiedades de límite y guardar la configuración.  

##  <a name="a-namebkmkboundarygroupsa-boundary-groups"></a><a name="BKMK_BoundaryGroups"></a> Grupos de límites  
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

##  <a name="a-namebkmkboundarybestpracticesa-best-practices-for-boundaries"></a><a name="BKMK_BoundaryBestPractices"></a> Procedimientos recomendados para los límites  

-   **Plantéese usar el tipo de límite de intervalo de direcciones IP solo cuando no se pueden usar otros tipos de límites:**  

     Al diseñar la estrategia de límite, se recomienda utilizar límites que se basan en sitios de Active Directory antes de utilizar otros tipos de límites. Cuando los límites basados en sitios de Active Directory no son una opción, utilice la subred IP o límites de IPv6. Si ninguna de estas opciones está disponible para usted, aproveche los límites del intervalo de direcciones IP. Esto se debe a que el sitio evalúa miembros de límites periódicamente y la consulta que se necesita para evaluar miembros de un intervalo de direcciones IP requiere un uso sustancialmente mayor de recursos de SQL Server que las consultas que evalúan miembros de otros tipos de límites.  

-   **Evite la superposición de límites en la asignación automática de sitio:**  

     Aunque los grupos de límites admiten tanto configuraciones de asignación de sitio como configuraciones de ubicación de contenido, se recomienda crear un conjunto de grupos de límites independiente que se vaya a usar solo para la asignación de sitio. Es decir, asegúrese de que cada uno de los límites de un grupo de límites, no forme parte de otro grupo de límites con una asignación de sitio diferente. El motivo es el siguiente:  

    -   Un único límite puede incluirse en varios grupos de límites  

    -   Los grupos de límites pueden asociarse con un sitio principal diferente para la asignación de sitio  

    -   Un cliente en un límite que es miembro de dos grupos de límites diferentes con asignaciones de sitio diferentes, seleccionará un sitio al que unirse al azar, que puede no ser el sitio que determinó para el cliente.  Esta configuración se denomina superposición de límites.  

     La superposición de límites no es un problema para la ubicación de contenido, sino que a menudo es una configuración deseada que proporciona recursos o ubicaciones de contenido adicionales a los clientes.  



<!--HONumber=Nov16_HO1-->


