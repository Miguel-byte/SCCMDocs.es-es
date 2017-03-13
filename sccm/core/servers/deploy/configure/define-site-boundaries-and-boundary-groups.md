---
title: "Definir los límites del sitio | Microsoft Docs"
description: "Obtenga información sobre cómo definir ubicaciones de red de la intranet que pueden contener los dispositivos que quiere administrar."
ms.custom: na
ms.date: 2/27/2017
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
ms.sourcegitcommit: 6d83570e3210709c5ef39b50d9c483f99017664b
ms.openlocfilehash: 13b79c920a64698660ee1c041b9166646789634c
ms.lasthandoff: 02/28/2017


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


##  <a name="BKMK_Boundaries"></a> Límites  
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

### <a name="to-create-a-boundary"></a>Para crear un límite  

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

### <a name="to-configure-a-boundary"></a>Para configurar un límite  

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

##  <a name="BKMK_BoundaryGroups"></a> Boundary groups
> [!IMPORTANT]  
>  **La información incluida en esta sección sobre los grupos de límites y sus secciones secundarios se aplica a la versión 1610 o posterior.** Este contenido se ha revisado para que se refiera específicamente a los cambios de diseño que se han introducido para los grupos de límites con esta versión de actualización.
>
> **Si usa las versiones 1511, 1602 o 1606**, consulte [Boundary groups for System Center Configuration Manager versions 1511, 1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) (Grupos de límites para las versiones 1511, 1602 y 1606 de System Center Configuration Manager) para obtener información sobre cómo usar y configurar grupos de límites con esas versiones de producto.

La versión 1610 presenta cambios importantes en los grupos de límites y en su funcionamiento con los puntos de distribución. Estos cambios le ayudan a simplificar el diseño de la infraestructura de contenido y le proporcionan más control sobre cómo y cuándo los clientes usan la reserva para buscar puntos de distribución adicionales como ubicaciones de origen de contenido. Esto incluye tanto puntos de distribución locales como basados en la nube.

**Acerca de los grupos de límites:**  
 Cree grupos de límites para agrupar de forma lógica las ubicaciones de red (límites) de manera que su infraestructura de red resulte más fácil de administrar. Debe asignar límites a grupos de límites para poder utilizar el grupo de límites. Los clientes usan la configuración de grupos de límites para lo siguiente:  

-   Asignación automática de sitio  
-   Ubicación del contenido  
-   Puntos de administración preferidos (si va a usar los puntos de administración preferidos, debe habilitar esta opción para la jerarquía y no desde la configuración del grupo de límites. Consulte el procedimiento [Para habilitar el uso de puntos de administración preferidos](#to-enable-use-of-preferred-management-points) incluido en este tema).  

Al configurar grupos de límites, se agregan uno o varios límites al grupo de límites y después se especifican los valores de configuración adicionales que usarán los clientes ubicados en esos límites.  

Puede encontrar [procedimientos para administrar grupos de límites](#procedures-for-boundary-groups) más adelante en este tema.


###  <a name="BKMK_BoundarySiteAssignment"></a> Información sobre la asignación de sitio  
 Puede configurar cada grupo de límites con un sitio asignado para los clientes.  

-   Un cliente recién instalado que usa la asignación automática de sitio se unirá al sitio asignado de un grupo de límites que contiene la ubicación de red actual del cliente.  
-   Una vez recibida la asignación a un sitio, el cliente no la modifica al cambiar la ubicación de red. Por ejemplo, si el cliente se mueve a una nueva ubicación de red representada por un límite en un grupo de límites con una asignación de sitio diferente, el sitio asignado del cliente no se modificará.  
-   Cuando la detección de sistemas de Active Directory detecta un nuevo recurso, la información de red para el recurso detectado se evalúa en relación con los límites en los grupos de límites. Este proceso asocia el nuevo recurso con un sitio asignado para que use el método de instalación de inserción de cliente.  
-   Cuando un límite es miembro de varios grupos de límites que tienen diferentes sitios asignados, los clientes seleccionarán uno de los sitios de forma aleatoria.  
-   Los cambios que se realicen a un sitio de grupo de límites asignado solo se aplicarán a las nuevas acciones de asignación de sitio. Los clientes previamente asignados a un sitio no vuelven a evaluar su asignación de sitio según los cambios en la configuración de un grupo de límites (o en su propia ubicación de red).  

Para obtener más información sobre la asignación de sitio de cliente, consulte [Using Automatic Site Assignment for Computers](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) (Uso de la asignación de sitio automática para los equipos) en [How to assign clients to a site in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md) (Cómo asignar clientes a un sitio en System Center Configuration Manager).  

###  <a name="BKMK_BoundaryContentLocation"></a> Información sobre la ubicación del contenido  
Al configurar grupos de límites, se asocian límites (ubicaciones de red) y roles de sistema de sitio, como los puntos de distribución, al grupo de límites. Esto ayuda a vincular clientes a servidores de sistema de sitio como puntos de distribución ubicados cerca de los clientes en la red.

Puede asignar el mismo límite a varios grupos de límites, y puede asociar servidores de sistema de sitio, como los puntos de distribución, a varios grupos de límites. Esto los pone a disposición de una gama más amplia de ubicaciones de red.

-   **Durante la distribución de software**, los clientes solicitan una ubicación para el contenido de la implementación. Configuration Manager envía al cliente una lista de puntos de distribución asociados a cada grupo de límites que incluye la ubicación de red actual del cliente.  
-   **Durante la implementación de sistema operativo**, los clientes solicitan una ubicación para enviar o recibir su información de estado de la migración. Configuration Manager envía al cliente una lista de puntos de migración de estado asociados a cada grupo de límites que incluye la ubicación de red actual del cliente.  

Puede definir relaciones entre grupos de límites para configurar el comportamiento de reserva de las ubicaciones de origen de contenido. En la versión 1610, se introdujo por primera vez la posibilidad de configurar relaciones en la nueva pestaña **Relaciones** de las propiedades del grupo de límites. Las relaciones reemplazan la necesidad de configurar los sistemas de sitio para que sean lentos o rápidos, o de configurar un grupo de límites para que permita la ubicación de origen de reserva para el contenido.

Al configurar un grupo de límites, que se denomina el grupo de límites **actual**, debe agregar otros grupos de límites para crear un vínculo unidireccional del grupo de límites actual a cada grupo de límites que agregue. Los grupos de límites que agregue se denominan grupos de límites **vecinos**. Después, para cada vínculo que cree a un grupo vecino, puede configurar puntos de distribución con un tiempo de reserva en minutos. Este tiempo se usa para determinar después de cuánto tiempo los clientes del grupo de límites actual pueden empezar a usar puntos de distribución del grupo de límites vecino si los clientes no pueden encontrar una ubicación de origen de contenido válida en su actual grupo de límites.

Cuando un cliente no encuentra el contenido y empieza a buscar en ubicaciones de grupos de límites vecinos, se incrementa el grupo de puntos de distribución disponibles para ese cliente de una manera controlada.

-    Un grupo de límites puede tener más de una relación. Esto permite configurar la reserva de los distintos vecinos para que se produzca después de períodos de tiempo diferentes.
-     Los clientes solo usarán como reserva un grupo de límites que sea vecino directo de su actual grupo de límites.
-    Cuando un cliente es miembro de varios grupos de límites, el grupo de límites actual se define como una unión de todos los grupos de límites de ese cliente. Ese cliente puede usar como reserva un vecino de cualquiera de esos grupos de límites originales.

Además de los vínculos que se definen, hay un vínculo implícito que se crea automáticamente entre los grupos de límites que se crean y el grupo de límites predeterminado que se crea automáticamente para cada sitio. Este vínculo automático:
-     Lo usan los clientes que no están en un límite asociado a los grupos de límites de la jerarquía. Los clientes usan automáticamente el grupo de límites predeterminados de su sitio asignado para identificar las ubicaciones de origen de contenido válidas.
-     es una opción de reserva predeterminada del grupo de límites actual al grupo de límites de sitio predeterminado que se usa después de 120 minutos.

**Cuando el contenido no está disponible en un grupo de límites actual:**  
Cuando el contenido pedido por un cliente no está disponible en un origen de contenido válido del grupo de límites actual, el cliente espera hasta que se alcance el período de reserva de un grupo de límites vecino o del grupo de límites predeterminado del sitio para que el cliente pueda buscar otros orígenes de contenido.

Si el contenido se distribuye a petición pero no está disponible cuando lo solicita un cliente, se inicia el proceso de transferir el contenido a un punto de distribución del límite actual.  



**Ejemplo de uso del nuevo modelo:**   
Cree tres grupos de límites que no compartan los límites ni los servidores de sistema de sitio:
-    Grupo BG_A con puntos de distribución DP_A1 y DP_A2 asociados al grupo
-    Grupo BG_B con puntos de distribución DP_B1 y DP_B2 asociados al grupo
-    Grupo BG_C con puntos de distribución DP_C1 y DP_C2 asociados al grupo

Agregue las ubicaciones de red de los clientes como límites para el grupo de límites BG_A y luego configure relaciones desde ese grupo de límites con los otros dos grupos de límites:
-    Configure los puntos de distribución para usar el primer grupo *vecino* (BG_B) después de 10 minutos. Este grupo contiene los puntos de distribución DP_B1 y DP_B2. Ambos están bien conectados a las primeras ubicaciones de límite de grupos.
-    Configure el segundo grupo *vecino* (BG_C) para usarse después de 20 minutos. Este grupo contiene los puntos de distribución DP_C1 y DP_C2. Ambos están separados por WAN de los otros dos grupos de límites.
-    Agregue también un punto de distribución adicional que se encuentre en el servidor de sitio al grupo de límites de sitio predeterminado de los sitios. Se trata de la ubicación de origen de contenido menos preferida, pero tiene una ubicación central con respecto a todos los grupos de límites.

    Ejemplo de grupos de límites y tiempos de reserva:

     ![BG_Fallack](media/BG_Fallback.png)


Con esta configuración:
-    El cliente empieza a buscar contenido en los puntos de distribución de su grupo de límites *actual* (BG_A), buscando en cada punto de distribución durante dos minutos antes de pasar al siguiente punto de distribución del grupo de límites. El grupo de clientes de ubicaciones de origen de contenido válidas incluye DP_A1 y DP_A2.
-    Si el cliente no puede encontrar contenido en su grupo de límites *actual* después de buscar durante 10 minutos, agrega los puntos de distribución del grupo de límites BG_B a su búsqueda. Luego continúa buscando contenido en un punto de distribución de su grupo combinado de puntos de distribución que ahora incluye los de los grupos de límites BG_A y BG_B. El cliente sigue poniéndose en contacto con cada punto de distribución durante dos minutos antes de pasar al siguiente punto de distribución de su grupo. El grupo de clientes de ubicaciones de origen de contenido válidas incluye DP_A1, DP_A2, DP_B1 y DP_B2.
-    Después de otros 10 minutos (un total de 20 minutos), si el cliente aún no ha encontrado un punto de distribución con contenido, amplía su grupo de puntos de distribución disponibles para incluir los del segundo grupo *vecino*, el grupo de límites BG_C. El cliente ahora tiene seis puntos de distribución para la búsqueda (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 y DP_C2) y sigue pasando a un nuevo punto de distribución cada dos minutos hasta que encuentra contenido.
-    Si el cliente no ha encontrado contenido después de un total de 120 minutos, usa la reserva para incluir el *grupo de límites de sitio predeterminado* como parte de su búsqueda continuada. Ahora el grupo de puntos de distribución incluye todos los puntos de distribución de los tres grupos de límites configurados y el punto de distribución final ubicado en el equipo de servidor de sitio.  El cliente sigue buscando contenido, cambiando de punto de distribución cada dos minutos hasta que encuentra contenido.

Mediante la configuración de los distintos grupos vecinos para que estén disponibles en momentos diferentes, se controla cuándo se agregan puntos de distribución concretos como ubicación de origen de contenido y cuándo, o si, el cliente usa la reserva del grupo de límites de sitio predeterminado como una red de seguridad para el contenido que no está disponible desde cualquier otra ubicación.




### <a name="update-existing-boundary-groups-to-the-new-model"></a>Actualizar grupos de límites existentes al nuevo modelo
Al actualizar a la versión 1610, se realizan automáticamente las siguientes configuraciones. Su objetivo es garantizar que el comportamiento de reserva actual siga estando disponible hasta que configure nuevos grupos de límites y relaciones.
-    Se crea un grupo de límites del sitio predeterminado para cada sitio primario, con el nombre ***Default-Site-Boundary-Group&lt;CódigoDeSitio>.***
-    Los puntos de distribución con la opción *Permitir ubicación de origen de reserva para contenido* activada y puntos de migración de estado en los sitios primarios se agregan al grupo de límites *Default-Site-Boundary-Group&lt;CódigoDeSitio >* de ese sitio.
-    Se realiza una copia de cada grupo de límites existente que incluye un servidor de sitio configurado con una conexión lenta. El nombre del nuevo grupo es ***&lt;nombre del grupo de límites original>-&lt;Id. del grupo de límites original>***:  
    -    Los sistemas de sitio con una conexión rápida se dejan en el grupo de límites original.
    -    Se agrega a la copia del grupo de límites una copia de los sistemas de sitio (puntos de distribución, puntos de administración y puntos de migración de estado) que tienen una conexión lenta. Los sistemas de sitio originales configurados como lentos permanecen en sus grupos de límites originales por razones de compatibilidad con versiones anteriores, pero no se usan desde esos grupo de límites.
    -     Esta copia del grupo de límites no tiene límites asociados, pero se crea un vínculo de reserva entre el grupo original y la nueva copia del grupo de límites con un tiempo de reserva establecido en cero.  


- **Específico de los sitios secundarios:**
  - Se crea un grupo de límites si un sitio secundario tiene al menos un punto de distribución con la opción *Permitir ubicación de origen de reserva para contenido* activada o un punto de migración de estado. El nombre del grupo de límites es ***Secondary-Site-Neighbor--Tmp&lt;CódigoDeSitio>.***
  - Todos los puntos de distribución con la opción *Permitir ubicación de origen de reserva para contenido* activada y puntos de migración de estado se agregan a este grupo de límites del sitio secundario recién creado.
  - Se crea un vínculo de reserva entre el grupo de límites original y el grupo de límites vecino recién creado con un tiempo de reserva establecido en cero.


 En la siguiente tabla se identifica el nuevo comportamiento de reserva que se puede esperar de la combinación de las configuraciones de implementación originales y las configuraciones de los puntos de distribución:

Configuración de implementación original “No ejecutar programa” de la red lenta  |Configuración de punto de distribución original “Permitir a los clientes usar una ubicación de origen de reserva para el contenido”  |Nuevo comportamiento de reserva  
---------|---------|---------
Seleccionado     |  Seleccionado    |  **Sin reserva**: se usan solo los puntos de distribución del grupo de límites actual       
Seleccionado     |  No seleccionado|  **Sin reserva**: se usan solo los puntos de distribución del grupo de límites actual       
No seleccionado |  No seleccionado|  **Reserva a vecino**: se usan los puntos de distribución del grupo de límites actual y luego se agregan los puntos de distribución del grupo de límites vecino. A menos que se configure un vínculo explícito al grupo de límites de sitio predeterminado, los clientes no usarán la reserva a ese grupo.    
No seleccionado | Seleccionado        |   **Reserva normal**: se usan los puntos de distribución del grupo de límites actual y luego los de los grupos de límites vecinos y predeterminados de sitios

 Todas las demás configuraciones de implementación darán lugar a una **reserva normal**.  



### <a name="changes-from-prior-versions-for-ui-and-behavior-for-content-locations"></a>Cambios respecto a versiones anteriores en la interfaz de usuario y el comportamiento relacionado con las ubicaciones de contenido
Estos son los principales cambios en los grupos de límites y en la forma en que los clientes buscan contenido que se han introducido en la versión 1610. Muchos de estos conceptos y cambios funcionan conjuntamente.


-    **Se quitan las configuraciones de rápido o lento:** ya no se configuran los puntos de distribución individuales para que sean rápidos o lentos.  En su lugar, se trata igual cada sistema de sitio asociado a un grupo de límites. Debido a este cambio, la pestaña **Referencias** de las propiedades del grupo de límites ya no admite la configuración de Rápido o Lento.
-     **Nuevo grupo de límites predeterminado en cada sitio:** cada sitio primario tiene un nuevo grupo de límites predeterminado denominado ***Default-Site-Boundary-Group&lt;sitecode>***.  Cuando un cliente no esté en una ubicación de red asignada a un grupo de límites, ese cliente usará los sistemas de sitio asociados con el grupo predeterminado de su sitio asignado. Este grupo de límites se puede considerar un sustituto del concepto de ubicación de contenido de reserva.      
 -    **Permitir a los clientes usar una ubicación de origen de reserva para el contenido** se ha quitado: ya no se configuran puntos de distribución de forma explícita para usarse como reserva y las opciones para hacerlo se han quitado de la interfaz de usuario.

    Además, el resultado de establecer **Permitir a los clientes usar una ubicación de origen de reserva para el contenido** en un tipo de implementación para aplicaciones ha cambiado. Esta opción en un tipo de implementación ahora permite a un cliente usar el grupo de límites de sitio predeterminado como una ubicación de origen de contenido.

 -    **Relaciones de grupos de límites:** cada grupo de límites se puede vincular a uno o más grupos de límites adicionales. Estos vínculos forman relaciones que se configuran en la nueva pestaña de propiedades de grupos de límites denominada **Relaciones**:
     -    Cada grupo de límites asociado directamente a un cliente se denomina grupo de límites **actual**.  
    -     Cualquier grupo de límites que un cliente pueda usar debido a una asociación entre ese grupo de límites *actual* de cliente y otro grupo se denomina grupo de límites **vecino**.
    -  Es en la pestaña **Relaciones** donde se agregan los grupos de límites que se pueden usar como grupos de límites *vecinos*. También puede configurar un tiempo en minutos que determine cuándo empezará un cliente que no pueda encontrar contenido de un punto de distribución del grupo *actual* a buscar ubicaciones de contenido de esos grupos de límites *vecinos*.

        Al agregar o cambiar la configuración de un grupo de límites, tendrá la opción de bloquear la reserva de ese grupo de límites concreto desde el grupo actual que está configurando.

    Para usar la nueva configuración, defina asociaciones explícitas (vínculos) de un grupo de límites con otro y configure todos los puntos de distribución de ese grupo asociado con el mismo tiempo en minutos. El tiempo que configure determina si un cliente que no encuentra un origen de contenido de su grupo de límites *actual* puede empezar a buscar orígenes de contenido en ese grupo de límites vecino.

    Además de los grupos de límites que se configuran explícitamente, cada grupo de límites tiene un vínculo implícito al grupo de límites de sitio predeterminado. Este vínculo se activa después de 120 minutos, momento en que el grupo de límites de sitio predeterminado se convierte en un grupo de límites vecino que permite a los clientes usar los puntos de distribución asociados a ese grupo de límites como ubicaciones de origen de contenido.

    Este comportamiento reemplaza a lo que anteriormente se conocía como reserva de contenido.  Puede anular este comportamiento predeterminado de 120 minutos si asocia explícitamente el grupo de límites de sitio predeterminado a un grupo *actual* y establece un tiempo concreto en minutos o bloquea la reserva completamente para evitar su uso.


-     **Los clientes intentan obtener contenido de cada punto de distribución hasta un máximo de dos minutos:** cuando un cliente busca una ubicación de origen de contenido, intenta acceder a cada punto de distribución durante dos minutos antes de intentarlo con otro punto de distribución. Esto supone un cambio con respecto a las versiones anteriores, donde los clientes intentaban conectarse a un punto de distribución hasta un máximo de dos horas.

    - El primer punto de distribución que un cliente intenta usar se selecciona aleatoriamente en el grupo de puntos de distribución disponibles del grupo (o grupos) de límites *actual* del cliente.

    - Después de dos minutos, si el cliente no ha encontrado el contenido, cambia a un nuevo punto de distribución e intenta obtener contenido de ese servidor. Este proceso se repite cada dos minutos hasta que el cliente encuentra el contenido o alcanza el último servidor de su grupo.

    - Si un cliente no puede encontrar una ubicación de origen de contenido válida de su grupo *actual* antes de que se alcance la reserva de un grupo de límites *vecino*, el cliente agrega los puntos de distribución de ese grupo *vecino* al final de su lista actual y luego busca en el grupo ampliado de ubicaciones de origen que incluye los puntos de distribución de ambos grupos de límites.

        > [!TIP]  
        > Al crear un vínculo explícito entre el grupo de límites actual y el grupo de límites de sitio predeterminado y definir un tiempo de reserva menor que el tiempo de reserva de un vínculo a un grupo de límites vecino, los clientes empiezan a buscar ubicaciones de origen en el grupo de límites de sitio predeterminado antes de incluir el grupo vecino.

    - Cuando el cliente no puede obtener contenido del último servidor del grupo, el proceso comienza de nuevo.





###  <a name="BKMK_PreferredMP"></a> Información sobre los puntos de administración preferidos  
 Los puntos de administración preferidos permiten que un cliente identifique un punto de administración asociado con su ubicación de red (límite) actual.  

-   Un cliente intenta usar un punto de administración preferido de su sitio asignado antes de usar un punto de administración de su sitio asignado que no está configurado como el preferido.  
-   Para usar esta opción, debe habilitarla para la jerarquía y configurar grupos de límites en los sitios primarios individuales para que incluyan los puntos de administración que se deben asociar con esos límites asociados del grupo de límites.  
-   Cuando se configuran los puntos de administración preferidos y un cliente organiza su lista de puntos de administración, el cliente coloca los puntos de administración preferidos en la parte superior de su lista de puntos de administración asignados (que incluye todos los puntos de administración del sitio asignado del cliente).  

> [!NOTE]  
>  Cuando un cliente activa la itinerancia (que significa cambiar sus ubicaciones de red, como por ejemplo, cuando se viaja con un equipo portátil a una ubicación de oficina remota), podría usar un punto de administración (o punto de administración proxy) desde el sitio local de su nueva ubicación, antes de intentar usar un punto de administración desde su sitio asignado (que incluye los puntos de administración preferidos).  Consulte [Understand how clients find site resources and services for System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) (Comprender cómo los clientes buscan servicios y recursos de sitio para System Center Configuration Manager) para obtener más información.  

###   <a name="BKMK_BoundaryOverlap"></a> Información sobre la superposición de límites  
 Configuration Manager admite configuraciones de límites que se superponen para la ubicación del contenido:  

-   **Cuando un cliente solicita contenido** y la ubicación de red del cliente pertenece a varios grupos de límites, Configuration Manager envía al cliente una lista de todos los puntos de distribución que tienen el contenido.  
-   **Cuando un cliente solicita a un servidor que envíe o reciba información de su migración de estado** y la ubicación de red del cliente pertenece a varios grupos de límites, Configuration Manager envía al cliente una lista de todos los puntos de migración de estado asociados a un grupo de límites que incluye la ubicación de red actual del cliente.  

Este comportamiento permite al cliente seleccionar el servidor más cercano desde el que se va a transferir el contenido o información de migración de estado.  






## <a name="procedures-for-boundary-groups"></a>Procedimientos de los grupos de límites
Los procedimientos siguientes se aplican a la versión 1610 o posterior. Si usa la versión 1511, 1602 o 1606, consulte los procedimientos indicados en [Boundary groups for System Center Configuration Manager versions 1511, 1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) (Grupos de límites para las versiones 1511, 1602 y 1606 de System Center Configuration Manager).


### <a name="to-create-a-boundary-group"></a>Para crear un grupo de límites  
1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de jerarquía** >  **Grupos de límites**.  

2.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear grupo de límites**.  

3.  En el cuadro de diálogo **Crear grupo de límites** , seleccione la pestaña **General** y especifique un **Nombre** para este grupo de límites.  

4.  Haga clic en **Aceptar** para guardar el nuevo grupo de límites.  


### <a name="to-configure-a-boundary-group"></a>Para configurar un grupo de límites  
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

 6.  Seleccione la pestaña **Relaciones** para configurar el comportamiento de reserva:  

     - Haga clic en **Agregar** y, después, seleccione el grupo de límites que quiere configurar.

     - Establezca un tiempo de reserva para los puntos de distribución. Después de este período de tiempo, los clientes del grupo de límites para el que está configurando relaciones podrán empezar a buscar contenido en los puntos de distribución del grupo de límites que está agregando.

     - Para impedir la reserva en un grupo de límites específico, incluido el *grupo de límites del sitio predeterminado* que está configurado de forma predeterminada, seleccione el grupo de límites y, después, active la casilla **Never fallback** (Nunca reserva).   

 7.  Haga clic en **Aceptar** para cerrar las propiedades del grupo de límites y guardar la configuración.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Para asociar un servidor de implementación de contenido o un grupo de administración a un grupo de límites  
 1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de jerarquía** >  **Grupos de límites**.  

 2.  Seleccione el grupo de límites que desea modificar.  

 3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

 4.  En el cuadro de diálogo **Propiedades** correspondiente al grupo de límites, seleccione la pestaña **Referencias** .  

 5.  En **Seleccionar servidores de sistema de sitio**, haga clic en **Agregar**, seleccione la casilla correspondiente a los servidores de sistema de sitio que desea asociar con este grupo de límites y después haga clic en **Aceptar**.  

 6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo y guardar la configuración del grupo de límites.  


#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>Para configurar un sitio de reserva para asignación de sitio automática  

  1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración del sitio** >  **Sitios**.  

  2.  En la pestaña **Inicio** , en el grupo **Sitios** , haga clic en **Configuración de jerarquía**.  

  3.  En la pestaña **General** , seleccione la casilla de verificación para **Usar un sitio de reserva**y, a continuación, seleccione un sitio en la lista desplegable **Sitio de reserva** .  

  4.  Haga clic en **Aceptar** para guardar la configuración.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Para habilitar el uso de puntos de administración preferidos  

 1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de sitio** > **Sitios** y, después, en la pestaña **Inicio**, seleccione **Configuración de jerarquía**.  

 2.  En la pestaña **General** de la Configuración de jerarquía, seleccione **Los clientes prefieren usar puntos de administración especificados en grupos de límites**.  

 3.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo y guardar la configuración.  


### <a name="to-enable-use-of-pre-release-features"></a>Para habilitar el uso de características de la versión preliminar
1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de sitio** > **Sitios** y, después, en la pestaña **Inicio**, seleccione **Configuración de jerarquía**.  

2.  En la pestaña **General** de la configuración de la jerarquía, seleccione **Consent to use Pre-Release features** (Consentimiento para usar características de versiones preliminares).  

3.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo y guardar la configuración.  



##  <a name="BKMK_BoundaryBestPractices"></a> Procedimientos recomendados para los límites  

-   **Use una combinación del mínimo de límites que satisfagan sus necesidades:**  
   Antes, se recomendaba usar ciertos tipos de límites en lugar de otros. Con los cambios introducidos para mejorar el rendimiento, ahora se recomienda usar cualquier tipo de límites que funcionen para el entorno y que permitan usar el menor número posible de límites para simplificar las tareas de administración.      

-   **Evite la superposición de límites en la asignación automática de sitio:**  
     Aunque los grupos de límites admiten tanto configuraciones de asignación de sitio como configuraciones de ubicación de contenido, se recomienda crear un conjunto de grupos de límites independiente que se vaya a usar solo para la asignación de sitio. Es decir, asegúrese de que cada uno de los límites de un grupo de límites, no forme parte de otro grupo de límites con una asignación de sitio diferente. El motivo es el siguiente:  

    -   Un único límite puede incluirse en varios grupos de límites  

    -   Los grupos de límites pueden asociarse con un sitio principal diferente para la asignación de sitio  

    -   Un cliente en un límite que es miembro de dos grupos de límites diferentes con asignaciones de sitio diferentes, seleccionará un sitio al que unirse al azar, que puede no ser el sitio que determinó para el cliente.  Esta configuración se denomina superposición de límites.  

     La superposición de límites no es un problema para la ubicación de contenido, sino que a menudo es una configuración deseada que proporciona recursos o ubicaciones de contenido adicionales a los clientes.  

