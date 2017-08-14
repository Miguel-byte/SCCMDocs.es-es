---
title: "Definición de grupos de límites| Microsoft Docs"
description: "Obtenga información sobre los grupos de límites que vinculan a los clientes con sistemas de sitio en System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: 5debc6559f4b1c213e8ca513d685941c9e669063
ms.contentlocale: es-es
ms.lasthandoff: 07/29/2017

---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>Configuración de grupos de límites para System Center Configuration Manager


*Se aplica a: System Center Configuration Manager (rama actual)*

Los grupos de límites se usan en System Center Configuration Manager para agrupar de forma lógica las ubicaciones de red ([límites](/sccm/core/servers/deploy/configure/boundaries)) de manera que su infraestructura de red resulte más fácil de administrar. Los límites deben asignarse a los grupos de límites para poder utilizar el grupo de límites.

De forma predeterminada, Configuration Manager crea un grupo de límites de sitio de forma predeterminada en cada sitio.

> [!IMPORTANT]  
>  **La información incluida en esta sección sobre los grupos de límites y sus secciones secundarios se aplica a la versión 1610 o posterior.** Este contenido se ha revisado para que se refiera específicamente a los cambios de diseño que se han introducido para los grupos de límites con esta versión de actualización.
>
> **Si usa las versiones previas a la 1610**, vea [Grupos de límites para las versiones 1511, 1602 y 1606 de System Center Configuration Manager](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) para obtener información sobre cómo usar y configurar grupos de límites con esas versiones de producto.

Para configurar grupos de límites, se asocian límites (ubicaciones de red) y roles de sistema de sitio, como los puntos de distribución, al grupo de límites. Esto ayuda a asociar clientes a servidores de sistema de sitio como puntos de distribución ubicados cerca de los clientes en la red.

Al asignar el mismo límite a varios grupos de límites y los mismos servidores de sistema de sitio, como los puntos de distribución, a varios grupos de límites, aumenta la disponibilidad de los sistemas de sitio a una variedad más amplia de ubicaciones de red.

Los clientes usan un grupo de límites para:  

-   Asignación automática de sitio  
-   Para buscar un servidor de sistema de sitio que puede proporcionar un servicio, que incluya:
    - Puntos de distribución para la ubicación del contenido
    -   Puntos de actualización de software (a partir de la versión 1702)
    - Puntos de migración de estado
    - Puntos de administración preferidos (si va a usar los puntos de administración preferidos, debe habilitar esta opción para la jerarquía y no desde la configuración del grupo de límites. Vea [Para habilitar el uso de puntos de administración preferidos](#to-enable-use-of-preferred-management-points) en este tema).

##  <a name="boundary-groups-and-relationships"></a>Grupos de límites y relaciones
Para cada grupo de límites de la jerarquía, puede asignar:

-  Uno o varios límites. Cuando un cliente está en una ubicación de red que se define como un límite asignado a un grupo de límites específico, que se denomina el grupo de límites **actual**. Un cliente puede tener más de un grupo de límites actual.
- Uno o varios roles de sistema de sitio.  Los clientes siempre pueden usar los roles de sistema de sitio asociados con su grupo de límites actual. Dependiendo de las configuraciones adicionales, pueden ser capaces de usar los roles de sistema de sitio en grupos de límites adicionales.  

Para cada grupo de límites creados, puede configurar un vínculo de un solo uso a otro grupo de límites. Al vínculo se le denomina **relación**. Los grupos de límites vinculados se denominan grupos de límites **vecinos**. Un grupo de límites puede tener varias relaciones, cada una con un grupo de límites vecino específico.

La configuración de cada relación determina si un cliente que no encuentra un servidor de sistema de sitio disponible en su actual grupo de límites puede empezar a buscar un grupo de límites vecino para encontrar un sistema de sitio disponible. Esta búsqueda de grupos adicionales se denomina **reserva**.

## <a name="fallback"></a>Reserva
Para evitar problemas a los clientes que no pueden encontrar un sistema de sitio disponible en su actual grupo de límites, se definen relaciones entre los grupos de límites que determinan el comportamiento de reserva. La reserva permite a un cliente expandir la búsqueda a grupos de límites adicionales para encontrar un sistema de sitio disponible.

Las relaciones se configuran en la pestaña **Relaciones** de las propiedades de un grupo de límites. Cuando se configura una relación, se define un vínculo a un grupo de límites vecino. Para cada tipo de rol de sistema de sitio admitido, puede configurar un ajuste independiente para la reserva en ese grupo de límites vecino. Por ejemplo, cuando se configura una relación con un grupo de límites concreto, puede establecer que la reserva para puntos de distribución se produzca después de 20 minutos, y no en el tiempo predeterminado de 120 minutos. Vea [Ejemplo de uso de grupos de límites](#example-of-using-boundary-groups) para obtener un ejemplo más extenso.

Si un cliente no puede encontrar un rol de sistema de sitio disponible en su actual grupo de límites, el cliente utiliza el tiempo de reserva en minutos para determinar después de cuánto tiempo puede empezar a buscar un sistema de sitio disponible que está asociado a ese grupo de límites vecino.  

Cuando un cliente no puede encontrar un sistema de sitio disponible y empieza a buscar ubicaciones de grupos de límites vecinos, aumenta el grupo de sistemas de sitio disponibles que puede usar según se define en la configuración de los grupos de límites y de sus relaciones.

- Un grupo de límites puede tener más de una relación. Con varias relaciones se puede configurar la reserva de cada tipo de sistema de sitio en los distintos vecinos para que se produzca después de períodos diferentes.    
- Los clientes solo usarán como reserva un grupo de límites que sea vecino directo de su actual grupo de límites.
- Cuando un cliente es miembro de varios grupos de límites, el grupo de límites actual se define como una unión de todos los grupos de límites de ese cliente. Ese cliente puede usar como reserva vecinos de cualquiera de esos grupos de límites originales.

### <a name="the-default-site-boundary-group"></a>El grupo de límites de sitio predeterminado
Además de los grupos de límites creados, cada sitio tiene un grupo de límites de sitio predeterminado creado por Configuration Manager. Este grupo se denomina ***Grupo-Límites-Sitio-Predeterminado&lt;códigodesitio>***. Por ejemplo, el grupo del sitio ABC se denominaría *Grupo-Límites-Sitio-Predeterminado&lt;ABC>.*

Para cada grupo de límites creado, Configuration Manager crea automáticamente un vínculo implícito a cada grupo de límites de sitio predeterminado de la jerarquía.
-   El vínculo implícito es una opción de reserva predeterminada de un grupo de límites actual al grupo de límites de sitio predeterminado que tiene un tiempo de reserva predeterminado de 120 minutos.
-   Los clientes que no se encuentran en un límite asociado con algún grupo de límites de la jerarquía usan el grupo de límites de sitio predeterminado de su sitio asignado para identificar roles de sistema de sitio válidos que pueden usar.

Para administrar la reserva para el grupo de límites de sitio predeterminado:
- Puede ir a las propiedades del grupo de límites de sitio predeterminado y cambiar los valores en la pestaña **Comportamiento predeterminado**. Los cambios que realice aquí se aplican a *todos* vínculos implícitos a este grupo de límites. Esta configuración puede invalidarse cuando configura el vínculo explícito a este grupo de límites de sitio predeterminado desde otro grupo de límites.
- Puede ir a las propiedades de un grupo de límites que haya creado y cambiar los valores del vínculo explícito que remite a un grupo de límites de sitio predeterminado. Cuando se establece un nuevo tiempo en minutos para la reserva o reserva en bloque, ese cambio afecta únicamente al vínculo que se va a configurar. Las configuraciones del vínculo explícito invalidan aquellas establecidas en la pestaña **Comportamiento predeterminado** de un grupo de límites de sitio predeterminado.


## <a name="site-assignment"></a>Asignación de sitio  
 Puede configurar cada grupo de límites con un sitio asignado para los clientes.  

-   Un cliente recién instalado que usa la asignación automática de sitio se unirá al sitio asignado de un grupo de límites que contiene la ubicación de red actual del cliente.  
-   Una vez recibida la asignación a un sitio, el cliente no la modifica al cambiar la ubicación de red. Por ejemplo, si el cliente se mueve a una nueva ubicación de red representada por un límite en un grupo de límites con una asignación de sitio diferente, el sitio asignado del cliente no se modificará.  
-   Cuando la detección de sistemas de Active Directory detecta un nuevo recurso, la información de red para el recurso detectado se evalúa en relación con los límites en los grupos de límites. Este proceso asocia el nuevo recurso con un sitio asignado para que use el método de instalación de inserción de cliente.  
-   Cuando un límite es miembro de varios grupos de límites que tienen diferentes sitios asignados, los clientes seleccionan uno de los sitios de forma aleatoria.  
-   Los cambios que se realicen a un sitio de grupo de límites asignado solo se aplicarán a las nuevas acciones de asignación de sitio. Los clientes previamente asignados a un sitio no vuelven a evaluar su asignación de sitio según los cambios en la configuración de un grupo de límites (o en su propia ubicación de red).  

Para obtener más información sobre la asignación de sitio de cliente, consulte [Using Automatic Site Assignment for Computers](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) (Uso de la asignación de sitio automática para los equipos) en [How to assign clients to a site in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md) (Cómo asignar clientes a un sitio en System Center Configuration Manager).  

## <a name="distribution-points"></a>Puntos de distribución

Cuando un cliente solicita la ubicación de un punto de distribución, Configuration Manager envía al cliente una lista que incluye los sistemas de sitio del tipo adecuado que están asociados a cada grupo de límites que incluye la ubicación de red actual del cliente:

-   **Durante la distribución de software**, los clientes solicitan una ubicación para el contenido de implementación que está disponible desde un punto de distribución, u otro origen de contenido válido (por ejemplo, un cliente configurado para el almacenamiento en caché del mismo nivel).

-   **Durante la implementación de sistema operativo**, los clientes solicitan una ubicación para enviar o recibir su información de estado de la migración.  

Durante la implementación de contenido, si un cliente solicita contenido que no está disponible desde un origen de su actual grupo de límites, el cliente continúa solicitando dicho contenido probando con diferentes orígenes de contenido en su grupo de límites actual, hasta que se alcanza el período de reserva de un grupo de límites vecino o del grupo de límites de sitio predeterminado. Si el cliente aún no encuentra contenido, expande la búsqueda de los orígenes de contenido para incluir los grupos de límites vecinos.

Sin embargo, si se distribuye el contenido a petición y no está disponible en un punto de distribución cuando un cliente lo solicita, comienza el proceso para transferir el contenido a dicho punto de distribución, y es posible que el cliente encuentre el servidor como un origen de contenido antes de volver a utilizar un grupo de límites vecino.

## <a name="software-update-points"></a>Puntos de actualización de software
A partir de la versión 1702, los clientes utilizan grupos de límites para encontrar un nuevo punto de actualización de software. Puede agregar puntos de actualización de software individuales a grupos de límites diferentes para controlar qué servidores puede encontrar un cliente.

Cuando se actualiza desde una versión anterior a la 1702, todos los puntos de actualización de software existentes se agregan al grupo de límites de sitio predeterminado en cada sitio. Esto mantiene el comportamiento anterior a la actualización donde los clientes seleccionan un punto de actualización de software del grupo de puntos de actualización de software disponibles que haya configurado para la jerarquía.  Este comportamiento se mantiene hasta que decida agregar puntos de actualización de software individuales a grupos de límites diferentes para un comportamiento controlado de selección y reserva.

Si instala un nuevo sitio que ejecuta la versión 1702 o una posterior, los puntos de actualización de software no se agregarán al grupo de límites de sitio predeterminado. Asigne los puntos de actualización de software a un grupo de límites para que los clientes pueden buscarlos y usarlos.

### <a name="fallback-for-software-update-points"></a>Reserva de los puntos de actualización de software
La reserva de puntos de actualización de software se configura como otros roles de sistema de sitio, pero tiene las siguientes observaciones:
- **Los nuevos clientes utilizan grupos de límites para seleccionar puntos de actualización de software.** Después de instalar la versión 1702, los clientes nuevos que instale seleccionan un punto de actualización de software de los asociados a los grupos de límites que ha configurado. Esto sustituye el comportamiento anterior, según el cual los clientes seleccionan un punto de actualización de software aleatoriamente de una lista de puntos que comparten el bosque del cliente.

- **Los clientes seguirán usando el último punto de actualización de software válido conocido hasta que recurran a la reserva para buscar uno nuevo.** Los clientes que ya tienen un punto de actualización de software seguirán usándolo hasta que no se pueda acceder al servidor.  Esto incluye el uso continuado de un punto de actualización de software que no está asociados al grupo de límites actual del cliente.

  El uso continuado de un punto de actualización de software existente aun cuando ese servidor no está en el grupo de límites actual del cliente es intencionado. Se debe a que un cambio en el punto de actualización de software puede producir un gran uso del ancho de banda de red cuando el cliente sincroniza los datos con el nuevo punto de actualización de software. El retraso en la transición puede ayudar a evitar que se sature la red en caso de que todos los clientes cambien a un punto de actualización de software nuevo al mismo tiempo.

- **Antes de iniciar la reserva, un cliente siempre trata de acceder al último punto de actualización de software válido conocido durante 120 minutos.** Después de ese tiempo, si el cliente no ha establecido contacto, se inicia la reserva. Cuando se inicia la reserva, el cliente recibe una lista de todos los puntos de actualización de software del grupo de límites actual. En función de las configuraciones de reserva, habrá disponibles más puntos de actualización de software en los grupos de límites vecinos y en el grupo de límites de sitio predeterminado.

### <a name="fallback-configurations-for-software-update-points"></a>Configuraciones de reserva de los puntos de actualización de software
#### <a name="beginning-with-version-1706"></a>A partir dela versión 1706   
Puede configurar **Tiempos de reserva (en minutos)** para que los puntos de actualización de software sean inferiores a 120 minutos. Sin embargo, el cliente todavía debe tratar de acceder al punto de actualización de software original durante 120 minutos antes de ampliar la búsqueda a los servidores adicionales. Como los tiempos de reserva del grupo de límites empiezan cuando el cliente primero no consigue acceder al servidor original, se proporcionan al cliente todos los grupos de límites configurados con menos de 120 minutos cuando este amplía la búsqueda después de que haber podido acceder al servidor original durante el período de 120 minutos.

Puede configurar la opción **No usar reserva nunca** para bloquear la reserva de un punto de actualización de software en un grupo de límites vecino.

Transcurridas dos horas sin conseguir acceder al servidor original, el cliente utiliza un ciclo más corto para establecer conexión con un nuevo punto de actualización de software. De esta forma, el cliente puede buscar rápido por la lista expandida de posibles puntos de actualización de software.

 -  **Ejemplo de reserva:**  
    El grupo de límites actual de un cliente tiene una reserva con los puntos de actualización de software configurados como *10* minutos para el grupo de límites *A*, y como *130* minutos para el *B*. Cuando el cliente no puede acceder al último punto de actualización de software válido conocida, ocurre lo siguiente:
    -   El cliente trata de acceder solo al servidor original durante los siguientes 120 minutos.  Después de 10 minutos, los puntos de actualización de software del grupo de límites A se agregan al grupo de servidores disponibles. Sin embargo, el cliente no puede tratar de conectarse a ellos o a cualquier otro servidor hasta que no haya transcurrido el período inicial de 120 minutos para volver a acceder al servidor original.
    -   Después de tratar de encontrar ese punto de actualización de software original durante 120 minutos, el cliente puede ampliar la búsqueda. En ese momento, los servidores del grupo de límites actual del cliente y todos los grupos de límites vecinos configurados para 120 minutos o menos se agregan al grupo disponible de puntos de actualización de software. Entre ellos se encuentran los servidores del grupo de límites A que se agregaron anteriormente al grupo de servidores disponibles.
    -       Cuando transcurren 10 minutos más (un tiempo total de 130 minutos después de que el cliente no pudiera acceder al último punto de actualización de software válido conocido), el cliente amplía la búsqueda para incluir los puntos de actualización de software del grupo de límites B.  

#### <a name="prior-to-version-1706"></a>Antes de la versión 1706
Antes de la versión 1706, las configuraciones de reserva de los puntos de actualización de software no son compatibles con un tiempo configurable en minutos. En su lugar, el comportamiento de reserva se limita a lo siguiente:

  - **Tiempos de reserva (en minutos):** esta opción está atenuada para puntos de actualización de software y no se puede configurar. Se establece en 120 minutos.
  -     **Never fallback** (Nunca reserva): puede bloquear la reserva para un punto de actualización de software en un grupo de límites vecino cuando se utiliza esta configuración.

Cuando un cliente que ya tiene un punto de actualización de software no puede acceder a él, este puede recurrir a la reserva para encontrar otro. Cuando se usa la reserva, el cliente recibe una lista de todos los puntos de actualización de software del grupo de límites actual. Si se produce un error al buscar un servidor disponible durante 120 minutos, recurrirá a la reserva de sus grupos de límites vecinos y del grupo de límites de sitio predeterminado. La reserva de ambos grupos de límites se produce al mismo tiempo porque el tiempo de reserva de los puntos de actualización de software de los grupos vecinos está establecido en 120 minutos y no se puede modificar. 120 minutos también es el período predeterminado que se utiliza para la reserva del grupo de límites de sitio predeterminado. Cuando un cliente recurre a la reserva de un grupo de límites vecino y de un grupo de límites de sitio predeterminado, este trata de establecer contacto con los puntos de actualización de software del grupo de límites vecino antes de tratar de usar alguno del grupo de límites de sitio predeterminado.

### <a name="manually-switch-to-a-new-software-update-point"></a>Cambio manual a un nuevo punto de actualización de software
Además de utilizar la reserva, puede usar *Notificación de cliente* para forzar manualmente a que un dispositivo cambie a un nuevo punto de actualización de software.

Cuando se cambia a un nuevo servidor, los dispositivos utilizan la reserva para buscar ese servidor nuevo. Por lo tanto, revise las configuraciones de los grupos de límites y asegúrese de que los puntos de actualización de software se encuentran en los grupos de límites correctos antes de iniciar este cambio.

Para obtener más información, consulte [Cambio manual de clientes a un nuevo punto de actualización de software](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).


## <a name="preferred-management-points"></a>Puntos de administración preferidos

 Los puntos de administración preferidos permiten que un cliente identifique un punto de administración asociado con su ubicación de red (límite) actual.  

-   Un cliente intenta usar un punto de administración preferido de su sitio asignado antes de usar un punto de administración de su sitio asignado que no está configurado como el preferido.  
-   Para usar esta opción, debe habilitarla para la jerarquía y después configurar grupos de límites en los sitios primarios individuales para que incluyan los puntos de administración que se deben asociar con esos límites asociados del grupo de límites.  
-   Cuando se configuran los puntos de administración preferidos y un cliente organiza su lista de puntos de administración, este coloca los puntos de administración preferidos en la parte superior de su lista de puntos de administración asignados (que incluye todos los puntos de administración del sitio asignado del cliente).  

> [!NOTE]  
>  Cuando un cliente activa la itinerancia (que significa cambiar sus ubicaciones de red, como por ejemplo, cuando se viaja con un equipo portátil a una ubicación de oficina remota), podría usar un punto de administración (o punto de administración proxy) desde el sitio local de su nueva ubicación, antes de intentar usar un punto de administración desde su sitio asignado (que incluye los puntos de administración preferidos).  Consulte [Understand how clients find site resources and services for System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) (Comprender cómo los clientes buscan servicios y recursos de sitio para System Center Configuration Manager) para obtener más información.  

### <a name="overlapping-boundaries"></a>Superposición de los límites  
 Configuration Manager admite configuraciones de límites que se superponen para la ubicación del contenido:  

-   **Cuando un cliente solicita contenido** y la ubicación de red del cliente pertenece a varios grupos de límites, Configuration Manager envía al cliente una lista de todos los puntos de distribución que tienen el contenido.  
-   **Cuando un cliente solicita a un servidor que envíe o reciba información de su migración de estado** y la ubicación de red del cliente pertenece a varios grupos de límites, Configuration Manager envía al cliente una lista de todos los puntos de migración de estado asociados a un grupo de límites que incluye la ubicación de red actual del cliente.  

Este comportamiento permite al cliente seleccionar el servidor más cercano desde el que se va a transferir el contenido o información de migración de estado.  



## <a name="example-of-using-boundary-groups"></a>Ejemplo de uso de grupos de límites
En el ejemplo siguiente se usa un cliente que busca contenido desde un punto de distribución. Este ejemplo se puede aplicar a otros roles de sistema de sitio que utilizan grupos de límites. Sin embargo, como se aplica a los puntos de actualización de software, tenga en cuenta que los puntos de actualización de software no admiten la configuración de un tiempo en minutos para la reserva en un grupo vecino, por lo que siempre debe usar un período de 120 minutos.

Cree tres grupos de límites que no compartan los límites ni los servidores de sistema de sitio:
-   Grupo BG_A con puntos de distribución DP_A1 y DP_A2 asociados al grupo
-   Grupo BG_B con puntos de distribución DP_B1 y DP_B2 asociados al grupo
-   Grupo BG_C con puntos de distribución DP_C1 y DP_C2 asociados al grupo

Agregue las ubicaciones de red de los clientes como límites para el grupo de límites BG_A y luego configure relaciones desde ese grupo de límites con los otros dos grupos de límites:
-   Configure los puntos de distribución para usar el primer grupo *vecino* (BG_B) después de 10 minutos. Este grupo contiene los puntos de distribución DP_B1 y DP_B2. Ambos están bien conectados a las primeras ubicaciones de límite de grupos.
-   Configure el segundo grupo *vecino* (BG_C) para usarse después de 20 minutos. Este grupo contiene los puntos de distribución DP_C1 y DP_C2. Ambos están separados por WAN de los otros dos grupos de límites.
-   Agregue también un punto de distribución adicional que se encuentre en el servidor de sitio al grupo de límites de sitio predeterminado de los sitios. Se trata de la ubicación de origen de contenido menos preferida, pero tiene una ubicación central con respecto a todos los grupos de límites.

    Ejemplo de grupos de límites y tiempos de reserva:

     ![BG_Fallack](media/BG_Fallback.png)


Con esta configuración:
-   El cliente empieza a buscar contenido en los puntos de distribución de su grupo de límites *actual* (BG_A), buscando en cada punto de distribución durante dos minutos antes de pasar al siguiente punto de distribución del grupo de límites. El grupo de clientes de ubicaciones de origen de contenido válidas incluye DP_A1 y DP_A2.
-   Si el cliente no puede encontrar contenido en su grupo de límites *actual* después de buscar durante 10 minutos, agrega los puntos de distribución del grupo de límites BG_B a su búsqueda. Luego continúa buscando contenido en un punto de distribución de su grupo combinado de puntos de distribución que ahora incluye los de los grupos de límites BG_A y BG_B. El cliente sigue poniéndose en contacto con cada punto de distribución durante dos minutos antes de pasar al siguiente punto de distribución de su grupo. El grupo de clientes de ubicaciones de origen de contenido válidas incluye DP_A1, DP_A2, DP_B1 y DP_B2.
-   Después de otros 10 minutos (un total de 20 minutos), si el cliente aún no ha encontrado un punto de distribución con contenido, amplía su grupo de puntos de distribución disponibles para incluir los del segundo grupo *vecino*, el grupo de límites BG_C. El cliente ahora tiene seis puntos de distribución para la búsqueda (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 y DP_C2) y sigue pasando a un nuevo punto de distribución cada dos minutos hasta que encuentra contenido.
-   Si el cliente no ha encontrado contenido después de un total de 120 minutos, usa la reserva para incluir el *grupo de límites de sitio predeterminado* como parte de su búsqueda continuada. Ahora el grupo de puntos de distribución incluye todos los puntos de distribución de los tres grupos de límites configurados y el punto de distribución final ubicado en el equipo de servidor de sitio.  El cliente sigue buscando contenido, cambiando de punto de distribución cada dos minutos hasta que encuentra contenido.

Mediante la configuración de los distintos grupos vecinos para que estén disponibles en momentos diferentes, se controla cuándo se agregan puntos de distribución concretos como ubicación de origen de contenido y cuándo, o si, el cliente usa la reserva del grupo de límites de sitio predeterminado como una red de seguridad para el contenido que no está disponible desde cualquier otra ubicación.






### <a name="update-existing-boundary-groups-to-the-new-model"></a>Actualizar grupos de límites existentes al nuevo modelo
Al actualizar a la versión anterior a la 1610, se realizan automáticamente las siguientes configuraciones. Su objetivo es garantizar que el comportamiento de reserva actual siga estando disponible hasta que configure nuevos grupos de límites y relaciones.

-   Se crea un grupo de límites del sitio predeterminado para cada sitio primario, con el nombre ***Default-Site-Boundary-Group&lt;CódigoDeSitio>.***
  - Los puntos de distribución con la opción *Permitir ubicación de origen de reserva para contenido* activada y puntos de migración de estado en los sitios primarios se agregan al grupo de límites *Default-Site-Boundary-Group&lt;CódigoDeSitio >* de ese sitio.
  - A partir de la versión 1702, los puntos de actualización de software se agregan a cada sitio *Grupo-Límites-Sitio-Predeterminado&lt;códigodesitio>*.
-   Se realiza una copia de cada grupo de límites existente que incluye un servidor de sitio configurado con una conexión lenta. El nombre del nuevo grupo es ***&lt;nombre del grupo de límites original>-&lt;Id. del grupo de límites original>***:  
    -   Los sistemas de sitio con una conexión rápida se dejan en el grupo de límites original.
    -   Se agrega a la copia del grupo de límites una copia de los sistemas de sitio (puntos de distribución y puntos de administración) que tienen una conexión lenta. Los sistemas de sitio originales configurados como lentos permanecen en sus grupos de límites originales por razones de compatibilidad con versiones anteriores, pero no se usan desde esos grupo de límites.
    - Esta copia del grupo de límites no tiene límites asociados, pero se crea un vínculo de reserva entre el grupo original y la nueva copia del grupo de límites con un tiempo de reserva establecido en cero.  


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
No seleccionado | Seleccionado     |   **Reserva normal**: se usan los puntos de distribución del grupo de límites actual y luego los de los grupos de límites vecinos y predeterminados de sitios

 Todas las demás configuraciones de implementación darán lugar a una **reserva normal**.  




## <a name="changes-from-prior-versions-for-ui-and-behavior-for-content-locations"></a>Cambios respecto a versiones anteriores en la interfaz de usuario y el comportamiento relacionado con las ubicaciones de contenido
Estos son los principales cambios realizados en los grupos de límites y en la forma en que los clientes buscan contenido. Estos cambios se introdujeron con la versión 1610. Muchos de estos conceptos y cambios funcionan conjuntamente.


-   **Se quitan las configuraciones de rápido o lento:** ya no se configuran los puntos de distribución individuales para que sean rápidos o lentos.  En su lugar, se trata igual cada sistema de sitio asociado a un grupo de límites. Debido a este cambio, la pestaña **Referencias** de las propiedades del grupo de límites ya no admite la configuración de Rápido o Lento.
-   **Nuevo grupo de límites predeterminado en cada sitio:** cada sitio primario tiene un nuevo grupo de límites predeterminado denominado ***Default-Site-Boundary-Group&lt;sitecode>***.  Cuando un cliente no esté en una ubicación de red asignada a un grupo de límites, ese cliente usará los sistemas de sitio asociados con el grupo predeterminado de su sitio asignado. Este grupo de límites se puede considerar un sustituto del concepto de ubicación de contenido de reserva.      
 -  **Permitir a los clientes usar una ubicación de origen de reserva para el contenido** se ha quitado: ya no se configuran puntos de distribución de forma explícita para usarse como reserva y las opciones para hacerlo se han quitado de la interfaz de usuario.

    Además, el resultado de establecer **Permitir a los clientes usar una ubicación de origen de reserva para el contenido** en un tipo de implementación para aplicaciones ha cambiado. Esta opción en un tipo de implementación ahora permite a un cliente usar el grupo de límites de sitio predeterminado como una ubicación de origen de contenido.

 -  **Relaciones de grupos de límites:** cada grupo de límites se puede vincular a uno o más grupos de límites adicionales. Estos vínculos forman relaciones que se configuran en la nueva pestaña de propiedades de grupos de límites denominada **Relaciones**:
    -   Cada grupo de límites asociado directamente a un cliente se denomina grupo de límites **actual**.  
    -   Cualquier grupo de límites que un cliente pueda usar debido a una asociación entre ese grupo de límites *actual* de cliente y otro grupo se denomina grupo de límites **vecino**.
    -  Es en la pestaña **Relaciones** donde se agregan los grupos de límites que se pueden usar como grupos de límites *vecinos*. También puede configurar un tiempo en minutos que determine cuándo empezará un cliente que no pueda encontrar contenido de un punto de distribución del grupo *actual* a buscar ubicaciones de contenido de esos grupos de límites *vecinos*.

        Al agregar o cambiar la configuración de un grupo de límites, tendrá la opción de bloquear la reserva de ese grupo de límites concreto desde el grupo actual que está configurando.

    Para usar la nueva configuración, defina asociaciones explícitas (vínculos) de un grupo de límites con otro y configure todos los puntos de distribución de ese grupo asociado con el mismo tiempo en minutos. El tiempo que configure determina si un cliente que no encuentra un origen de contenido de su grupo de límites *actual* puede empezar a buscar orígenes de contenido en ese grupo de límites vecino.

    Además de los grupos de límites que se configuran explícitamente, cada grupo de límites tiene un vínculo implícito al grupo de límites de sitio predeterminado. Este vínculo se activa después de 120 minutos, momento en que el grupo de límites de sitio predeterminado se convierte en un grupo de límites vecino que permite a los clientes usar los puntos de distribución asociados a ese grupo de límites como ubicaciones de origen de contenido.

    Este comportamiento reemplaza a lo que anteriormente se conocía como reserva de contenido.  Puede anular este comportamiento predeterminado de 120 minutos si asocia explícitamente el grupo de límites de sitio predeterminado a un grupo *actual* y establece un tiempo concreto en minutos o bloquea la reserva completamente para evitar su uso.


-   **Los clientes intentan obtener contenido de cada punto de distribución hasta un máximo de dos minutos:** cuando un cliente busca una ubicación de origen de contenido, intenta acceder a cada punto de distribución durante dos minutos antes de intentarlo con otro punto de distribución. Esto supone un cambio con respecto a las versiones anteriores, donde los clientes intentaban conectarse a un punto de distribución hasta un máximo de dos horas.

    - El primer punto de distribución que un cliente intenta usar se selecciona aleatoriamente en el grupo de puntos de distribución disponibles del grupo (o grupos) de límites *actual* del cliente.

    - Después de dos minutos, si el cliente no ha encontrado el contenido, cambia a un nuevo punto de distribución e intenta obtener contenido de ese servidor. Este proceso se repite cada dos minutos hasta que el cliente encuentra el contenido o alcanza el último servidor de su grupo.

    - Si un cliente no puede encontrar una ubicación de origen de contenido válida de su grupo *actual* antes de que se alcance la reserva de un grupo de límites *vecino*, el cliente agrega los puntos de distribución de ese grupo *vecino* al final de su lista actual y luego busca en el grupo ampliado de ubicaciones de origen que incluye los puntos de distribución de ambos grupos de límites.

        > [!TIP]  
        > Al crear un vínculo explícito entre el grupo de límites actual y el grupo de límites de sitio predeterminado y definir un tiempo de reserva menor que el tiempo de reserva de un vínculo a un grupo de límites vecino, los clientes empiezan a buscar ubicaciones de origen en el grupo de límites de sitio predeterminado antes de incluir el grupo vecino.

    - Cuando el cliente no puede obtener contenido del último servidor del grupo, el proceso comienza de nuevo.


## <a name="procedures-for-boundary-groups"></a>Procedimientos de los grupos de límites
Los procedimientos siguientes se aplican a la versión 1610 o posterior. Si usa la versión previa a la 1610, vea los procedimientos indicados en [Grupos de límites para las versiones 1511, 1602 y 1606 de System Center Configuration Manager](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).


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

#### <a name="to-associate-a-site-systme-server-with-a-boundary-group"></a>Para asociar un servidor de sistema de sitio a un grupo de límites  
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

