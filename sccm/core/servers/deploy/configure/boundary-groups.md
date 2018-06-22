---
title: Configurar grupos de límites
titleSuffix: Configuration Manager
description: Ayude a los clientes a encontrar sistemas de sitio mediante grupos de límites para organizar de manera lógica las ubicaciones de red relacionadas denominadas límites.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79c6796c116fbe4d182827e24f41ae4d1e5242fe
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342705"
---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>Configuración de grupos de límites para System Center Configuration Manager


*Se aplica a: System Center Configuration Manager (Rama actual)*

Use los grupos de límites en Configuration Manager para organizar de forma lógica las ubicaciones de red relacionadas ([límites](/sccm/core/servers/deploy/configure/boundaries)) para que sea más fácil administrar la infraestructura. Asigne límites a grupos de límites para poder usar el grupo de límites.

De forma predeterminada, Configuration Manager crea un grupo de límites de sitio de forma predeterminada en cada sitio.

Para configurar grupos de límites, asocie límites (ubicaciones de red) y roles de sistema de sitio, como los puntos de distribución, al grupo de límites. Esta configuración ayuda a asociar clientes a servidores de sistema de sitio como puntos de distribución ubicados cerca de los clientes en la red.

Para aumentar la disponibilidad de los servidores de sistema de sitio, como los puntos de distribución, a una variedad más amplia de ubicaciones de red, asigne el mismo límite y el mismo servidor a varios grupos de límites.

Los clientes usan un grupo de límites para:  

-   Asignación automática de sitio  
-   Para buscar un servidor de sistema de sitio que puede proporcionar un servicio, que incluya:
    - Puntos de distribución para la ubicación del contenido
    -   Puntos de actualización de software
    - Puntos de migración de estado
    - Puntos de administración preferidos (si va a usar los puntos de administración preferidos, debe habilitar esta opción para la jerarquía y no desde la configuración del grupo de límites. Vea [Para habilitar el uso de puntos de administración preferidos](#to-enable-use-of-preferred-management-points) en este tema).

##  <a name="boundary-groups-and-relationships"></a>Grupos de límites y relaciones
Para cada grupo de límites de la jerarquía, puede asignar:

-  Uno o varios límites. El grupo de límites **actual** de un cliente es una ubicación de red que se define como un límite asignado a un grupo de límites específico. Un cliente puede tener más de un grupo de límites actual.
- Uno o varios roles de sistema de sitio. Los clientes siempre pueden usar los roles de sistema de sitio asociados con su grupo de límites actual. Dependiendo de las configuraciones adicionales, pueden ser capaces de usar los roles de sistema de sitio en grupos de límites adicionales.  

Para cada grupo de límites creados, puede configurar un vínculo de un solo uso a otro grupo de límites. Al vínculo se le denomina **relación**. Los grupos de límites vinculados se denominan grupos de límites **vecinos**. Un grupo de límites puede tener varias relaciones, cada una con un grupo de límites vecino específico.

Cuando un cliente no encuentra un servidor de sistema de sitio disponible en su grupo de límites actual, la configuración de cada relación determina cuándo empieza a buscar un grupo de límites vecino. Esta búsqueda de grupos adicionales se denomina **reserva**.

## <a name="fallback"></a>Reserva
Para evitar problemas cuando los clientes no pueden encontrar un sistema de sitio disponible en su grupo de límites actual, se definen relaciones entre los grupos de límites para el comportamiento de reserva. La reserva permite a un cliente expandir la búsqueda a grupos de límites adicionales para encontrar un sistema de sitio disponible.

Las relaciones se configuran en la pestaña **Relaciones** de las propiedades de un grupo de límites. Cuando se configura una relación, se define un vínculo a un grupo de límites vecino. Para cada tipo de rol de sistema de sitio admitido, configure opciones independientes para la reserva en el grupo de límites vecino. Por ejemplo, cuando se configura una relación con un grupo de límites concreto, se puede establecer que la reserva para los puntos de distribución se produzca después de 20 minutos, en lugar del tiempo predeterminado de 120 minutos. Para obtener un ejemplo más extenso, vea [Ejemplo de uso de grupos de límites](#example-of-using-boundary-groups).

Si un cliente no puede encontrar un rol de sistema de sitio disponible en su grupo de límites actual, el cliente usa el tiempo de reserva en minutos. Este tiempo de reserva determina cuándo comienza el cliente a buscar un sistema de sitio disponible asociado con el grupo de límites vecino.  

Cuando un cliente no encuentra un sistema de sitio disponible y empieza a buscar en ubicaciones de los grupos de límites vecinos, se incrementa el grupo de sistemas de sitio disponibles. La configuración de los grupos de límites y sus relaciones define el uso del cliente de este grupo de sistemas de sitio disponibles.

- Un grupo de límites puede tener más de una relación. Con varias relaciones, se puede configurar la reserva de cada tipo de sistema de sitio en los distintos vecinos para que se produzca después de otros períodos.    
- Los clientes solo usarán como reserva un grupo de límites que sea vecino directo de su actual grupo de límites.
- Cuando un cliente es miembro de varios grupos de límites, el grupo de límites actual se define como una unión de todos los grupos de límites del cliente. El cliente puede usar como reserva vecinos de cualquiera de esos grupos de límites originales.

### <a name="the-default-site-boundary-group"></a>El grupo de límites de sitio predeterminado
Además de los grupos de límites creados, cada sitio tiene un grupo de límites de sitio predeterminado creado por Configuration Manager. Este grupo se denomina ***Grupo-Límites-Sitio-Predeterminado&lt;códigodesitio>***. Por ejemplo, el grupo del sitio ABC se denominaría *Grupo-Límites-Sitio-Predeterminado&lt;ABC>.*

Para cada grupo de límites creado, Configuration Manager crea automáticamente un vínculo implícito a cada grupo de límites de sitio predeterminado de la jerarquía.
-   El vínculo implícito es una opción de reserva predeterminada de un grupo de límites actual al grupo de límites de sitio predeterminado que tiene un tiempo de reserva predeterminado de 120 minutos.
-   Para los clientes que no se encuentran en un límite asociado con ningún grupo de límites: para identificar roles de sistema de sitio válidos, use el grupo de límites de sitio predeterminado de su sitio asignado.

Para administrar la reserva para el grupo de límites de sitio predeterminado:
- Abra las propiedades del grupo de límites de sitio predeterminado y cambie los valores en la pestaña **Comportamiento predeterminado**. Los cambios que realice aquí se aplican a *todos* vínculos implícitos a este grupo de límites. Esta configuración puede invalidarse cuando configura el vínculo explícito a este grupo de límites de sitio predeterminado desde otro grupo de límites.
- Abra las propiedades de un grupo de límites personalizado. Cambie los valores del vínculo explícito a un grupo de límites de sitio predeterminado. Cuando se establece un nuevo tiempo en minutos para la reserva o reserva en bloque, ese cambio afecta únicamente al vínculo que se va a configurar. La configuración del vínculo explícito invalida la que se establece en la pestaña **Comportamiento predeterminado** de un grupo de límites de sitio predeterminado.


## <a name="site-assignment"></a>Asignación de sitio  
 Puede configurar cada grupo de límites con un sitio asignado para los clientes.  

-   Un cliente recién instalado que usa la asignación automática de sitio se unirá al sitio asignado de un grupo de límites que contiene la ubicación de red actual del cliente.  
-   Una vez recibida la asignación a un sitio, el cliente no la modifica al cambiar la ubicación de red. Por ejemplo, si el cliente se mueve a una nueva ubicación de red representada por un límite de un grupo de límites con una asignación de sitio diferente, el sitio asignado del cliente no se modifica.  
-   Cuando la detección de sistemas de Active Directory detecta un nuevo recurso, la información de red para el recurso detectado se evalúa en relación con los límites en los grupos de límites. Este proceso asocia el nuevo recurso con un sitio asignado para que use el método de instalación de inserción de cliente.  
-   Cuando un límite es miembro de varios grupos de límites que tienen diferentes sitios asignados, los clientes seleccionan uno de los sitios de forma aleatoria.  
-   Los cambios que se realicen a un sitio de grupo de límites asignado solo se aplicarán a las nuevas acciones de asignación de sitio. Los clientes previamente asignados a un sitio no vuelven a evaluar su asignación de sitio según los cambios en la configuración de un grupo de límites (o en su propia ubicación de red).  

Para obtener más información sobre la asignación de sitio de cliente, consulte [Using Automatic Site Assignment for Computers](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) (Uso de la asignación de sitio automática para los equipos) en [How to assign clients to a site in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md) (Cómo asignar clientes a un sitio en System Center Configuration Manager).  

## <a name="distribution-points"></a>Puntos de distribución

Cuando un cliente solicita la ubicación de un punto de distribución, Configuration Manager envía al cliente una lista de sistemas de sitio. Estos sistemas de sitio son del tipo adecuado asociado a cada grupo de límites que incluye la ubicación de red actual de los clientes:

-   **Durante la distribución de software**, los clientes solicitan una ubicación para el contenido de implementación que está disponible desde un punto de distribución, u otro origen de contenido válido (por ejemplo, un cliente configurado para el almacenamiento en caché del mismo nivel).

-   **Durante la implementación de sistema operativo**, los clientes solicitan una ubicación para enviar o recibir su información de estado de la migración.  

Durante la implementación de contenido, si un cliente solicita contenido que no está disponible desde un origen de su grupo de límites actual, el cliente continúa con la solicitud de ese contenido. El cliente prueba otros orígenes de contenido en su grupo de límites actual hasta que alcanza el período de reserva para un grupo de límites vecino o el grupo de límites de sitio predeterminado. Si el cliente aún no encuentra contenido, expande la búsqueda de los orígenes de contenido para incluir los grupos de límites vecinos.

Si el contenido se distribuye a petición y no está disponible cuando lo solicita un cliente en un punto de distribución, se inicia el proceso de transferir el contenido a ese punto de distribución. Es posible que el cliente encuentre ese servidor como un origen de contenido antes de recurrir a un grupo de límites vecino.

## <a name="software-update-points"></a>Puntos de actualización de software
Los clientes usan grupos de límites para buscar un punto de actualización de software nuevo. Para controlar qué servidores puede buscar un cliente, agregue puntos de actualización de software individuales a otros grupos de límites.

Cuando se actualiza desde una versión anterior a la 1702, todos sitios agregan todos los puntos de actualización de software existentes al grupo de límites de sitio predeterminado. Este comportamiento de actualización de sitio mantiene el comportamiento de cliente anterior para seleccionar un punto de actualización de software del grupo de servidores disponibles. Este comportamiento se mantiene hasta que decida agregar puntos de actualización de software individuales a grupos de límites diferentes para un comportamiento controlado de selección y reserva.

Si se instala un sitio nuevo, no se agregan puntos de actualización de software al grupo de límites de sitio predeterminado. Asigne los puntos de actualización de software a un grupo de límites para que los clientes pueden buscarlos y usarlos.

### <a name="fallback-for-software-update-points"></a>Reserva de los puntos de actualización de software
La reserva de puntos de actualización de software se configura como otros roles de sistema de sitio, pero tiene las siguientes observaciones:
- **Los nuevos clientes utilizan grupos de límites para seleccionar puntos de actualización de software.** Los clientes nuevos que se instalen seleccionan un punto de actualización de software de los servidores asociados a los grupos de límites que se configuren. Este comportamiento sustituye al anterior, en el que los clientes seleccionan un punto de actualización de software aleatoriamente de una lista de servidores que comparten el bosque del cliente.

- **Los clientes seguirán usando el último punto de actualización de software válido conocido hasta que recurran a la reserva para buscar uno nuevo.** Los clientes que ya tienen un punto de actualización de software lo siguen usando hasta que no se puede alcanzar. Este comportamiento incluye el uso continuado de un punto de actualización de software que no está asociado al grupo de límites actual del cliente.

  El uso continuado de un punto de actualización de software existente incluso cuando ese servidor no está en el grupo de límites actual del cliente es intencionado. Cuando se cambia el punto de actualización de software, el cliente sincroniza los datos con el nuevo servidor, lo que supone un uso de red significativo. Si todos los clientes cambian a un servidor nuevo al mismo tiempo, el retraso en la transición ayuda a evitar la saturación de la red.

- **Antes de iniciar la reserva, un cliente siempre trata de acceder al último punto de actualización de software válido conocido durante 120 minutos.** Después de ese tiempo, si el cliente no ha establecido contacto, se inicia la reserva. Cuando se inicia la reserva, el cliente recibe una lista de todos los puntos de actualización de software del grupo de límites actual. En función de las configuraciones de reserva, hay más puntos de actualización de software disponibles en los grupos de límites vecinos y de sitio predeterminados.

### <a name="fallback-configurations-for-software-update-points"></a>Configuraciones de reserva de los puntos de actualización de software
#### <a name="beginning-with-version-1706"></a>A partir dela versión 1706   
Puede configurar **Tiempos de reserva (en minutos)** para que los puntos de actualización de software sean inferiores a 120 minutos. Pero el cliente continúa realizando intentos para alcanzar su punto de actualización de software original durante 120 minutos. Después, amplía su búsqueda a otros servidores. Los tiempos de reserva del grupo de límites se inician la primera vez que el cliente no puede alcanzar su servidor original. Cuando el cliente amplía la búsqueda, el sitio proporciona los grupos de límites configurados para menos de 120 minutos.

Para bloquear la reserva de un punto de actualización de software en un grupo de límites vecino, establezca la opción en **No usar reserva nunca**.

Transcurridas dos horas sin conseguir acceder al servidor original, el cliente utiliza un ciclo más corto para establecer conexión con un nuevo punto de actualización de software. Este comportamiento permite al cliente buscar de forma rápida por la lista expandida de posibles puntos de actualización de software.

 -  **Ejemplo de reserva:**  
    El grupo de límites actual de un cliente tiene una reserva con los puntos de actualización de software configurada en *10* minutos para el grupo de límites *A* y en *130* minutos para el *B*. Cuando el cliente no puede acceder al último punto de actualización de software válido conocida, ocurre lo siguiente:
    -   El cliente trata de acceder solo al servidor original durante los siguientes 120 minutos. Después de 10 minutos, los puntos de actualización de software del grupo de límites A se agregan al grupo de servidores disponibles. Sin embargo, el cliente no puede tratar de conectarse a ellos o a cualquier otro servidor hasta que no haya transcurrido el período inicial de 120 minutos para volver a acceder al servidor original.
    -   Después de tratar de encontrar ese punto de actualización de software original durante 120 minutos, el cliente puede ampliar la búsqueda. En ese momento, el cliente agrega servidores al grupo disponible de puntos de actualización de software del grupo de límites actual del cliente y todos los grupos de límites vecinos configurados para 120 minutos o menos. Este grupo incluye los servidores del grupo de límites A que se agregaron anteriormente al grupo de servidores disponibles.
    -       Cuando transcurren 10 minutos más (un tiempo total de 130 minutos después de que el cliente no pudiera acceder al último punto de actualización de software válido conocido), el cliente amplía la búsqueda para incluir los puntos de actualización de software del grupo de límites B.  

#### <a name="prior-to-version-1706"></a>Antes de la versión 1706
Antes de la versión 1706, las configuraciones de reserva de los puntos de actualización de software no son compatibles con un tiempo configurable en minutos. En su lugar, el comportamiento de reserva se limita a lo siguiente:

  - **Tiempos de reserva (en minutos):** esta opción está atenuada para los puntos de actualización de software y no se puede configurar. Se establece en 120 minutos.
  -     **Never fallback** (Nunca reserva): puede bloquear la reserva para un punto de actualización de software en un grupo de límites vecino cuando se utiliza esta configuración.

Cuando un cliente que ya tiene un punto de actualización de software no puede alcanzarlo, recurre a la reserva para encontrar otro. Cuando se usa la reserva, el cliente recibe una lista de todos los puntos de actualización de software del grupo de límites actual. Si se produce un error al buscar un servidor disponible durante 120 minutos, recurre a la reserva de sus grupos de límites vecinos y del grupo de límites de sitio predeterminado. La reserva en ambos grupos de límites se produce al mismo tiempo. El tiempo de reserva del punto de actualización de software para los grupos vecinos se establece en 120 minutos. Este tiempo de reserva no se puede cambiar. 120 minutos también es el período predeterminado que se utiliza para la reserva del grupo de límites de sitio predeterminado. Cuando un cliente recurre a la reserva de un grupo de límites vecino y de un grupo de límites de sitio predeterminado, este trata de establecer contacto con los puntos de actualización de software del grupo de límites vecino antes de tratar de usar alguno del grupo de límites de sitio predeterminado.

### <a name="manually-switch-to-a-new-software-update-point"></a>Cambio manual a un nuevo punto de actualización de software
Además de utilizar la reserva, puede usar *Notificación de cliente* para forzar manualmente a que un dispositivo cambie a un nuevo punto de actualización de software.

Cuando se cambia a un nuevo servidor, los dispositivos utilizan la reserva para buscar ese servidor nuevo. Revise las configuraciones de los grupos de límites. Asegúrese de que los puntos de actualización de software se encuentran en los grupos de límites correctos antes de iniciar este cambio.

Para obtener más información, consulte [Cambio manual de clientes a un nuevo punto de actualización de software](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).



## <a name="management-points"></a>Puntos de administración
<!-- 1324594 -->
A partir de la versión 1802, se configuran relaciones de reserva para los puntos de administración entre grupos de límites. Este comportamiento proporciona mayor control para los puntos de administración que utilizan los clientes. En la pestaña **Relaciones** de las propiedades del grupo de límites, hay una columna para el punto de administración. Cuando se agrega un nuevo grupo de límites de reserva, el tiempo de reserva para el punto de administración actualmente siempre es cero (0). Este comportamiento es el mismo para el **comportamiento predeterminado** en el grupo de límites predeterminado del sitio.

Anteriormente se producía un problema con frecuencia cuando tenía un punto de administración protegido en una red segura. Los clientes de la red corporativa principal reciben una directiva que incluye este punto de administración protegido, incluso aunque no se puedan comunicar con él a través de un firewall. Para solucionar este problema, utilice la opción **No usar reserva nunca** para asegurarse de que los clientes solo reservan para los puntos de administración con los que pueden comunicarse.

Al actualizar el sitio a la versión 1802, Configuration Manager agrega todos los puntos de administración que no son accesibles desde Internet al grupo de límites predeterminado del sitio. Con este comportamiento de actualización se garantiza que las versiones de cliente anteriores seguirán comunicándose con puntos de administración. Para aprovechar plenamente esta característica, mueva los puntos de administración a los grupos de límites deseados.

La reserva del grupo de límites del punto de administración no cambia el comportamiento durante la instalación de cliente (ccmsetup.exe). Si la línea de comandos no especifica el punto de administración inicial mediante el parámetro/MP, el cliente nuevo recibe la lista completa de puntos de administración disponibles. Para su proceso de arranque inicial, el cliente utiliza el primer punto de administración al que pueda tener acceso. Una vez que el cliente se registre en el sitio, recibirá la lista de puntos de administración ordenada correctamente de acuerdo con este nuevo comportamiento. 

Para que los clientes usen esta función, habilite la opción siguiente: **Los clientes prefieren usar puntos de administración especificados en grupos de límites** en **Configuración de jerarquía**. 

> [!Note]
> Los procesos de implementación de sistema operativo no operan de acuerdo con los grupos de límites.

### <a name="troubleshooting"></a>Solución de problemas
Las nuevas entradas aparecen en **LocationServices.log**. El atributo **Localidad** identifica uno de los siguientes estados:
- 0: desconocido
- 1: el punto de administración especificado solo está en el grupo de límites predeterminado del sitio para la reserva.
- 2: el punto de administración especificado está en un grupo de límites remoto o vecino. Cuando el punto de administración está simultáneamente en un grupo vecino y en un grupo de límites predeterminado del sitio, la localidad es 2.
- 3: el punto de administración especificado está en el grupo de límites local o actual. Cuando el punto de administración está en el grupo de límites actual, así como en un grupo vecino o de límites predeterminado del sitio, la localidad es 3. Si no habilita la configuración de los puntos de administración preferidos en la configuración de jerarquía, la localidad siempre es 3, con independencia de en qué grupo de límites se encuentre el punto de administración.

Los clientes utilizan puntos de administración locales primero (localidad 3), luego remotos (localidad 2) y por último reserva (localidad 1). 

Cuando un cliente recibe cinco errores en 10 minutos y no puede comunicarse con un punto de administración de su grupo de límites actual, trata de contactar con un punto de administración en un grupo vecino o el grupo de límites predeterminado del sitio. Si el punto de administración del grupo de límites actual más adelante vuelve a estar conectado, el cliente volverá al punto de administración local en el siguiente ciclo de actualización. El ciclo de actualización es de 24 horas, o cuando se reinicia el servicio del agente de Configuration Manager.




## <a name="preferred-management-points"></a>Puntos de administración preferidos

 > [!Note]
 > El comportamiento de esta configuración de jerarquía, **Los clientes prefieren usar puntos de administración especificados en grupos de límites**, cambia a partir de la versión 1802. Si habilita esta opción, Configuration Manager usa la funcionalidad de grupo de límites para el punto de administración asignado. Para obtener más información, vea [Puntos de administración](#management-points). 

 Los puntos de administración preferidos permiten que un cliente identifique un punto de administración asociado con su ubicación de red (límite) actual.  

-   Un cliente intenta usar un punto de administración preferido de su sitio asignado antes de usar otro que no está configurado como el preferido.  
-   Para usar esta opción, habilite **Los clientes prefieren usar puntos de administración especificados en grupos de límites** en **Configuración de jerarquía**. Después, configure los grupos de límites en sitios primarios individuales. Incluya los puntos de administración que se deben asociar con los límites asociados de ese grupo de límites.
-   Al configurar puntos de administración preferidos, y cuando un cliente organiza su lista de puntos de administración, el cliente coloca los puntos de administración preferidos en la parte superior de la lista. En esta lista se incluyen todos los puntos de administración del sitio asignado del cliente.  

> [!NOTE]  
>  La movilidad del cliente significa que cambia sus ubicaciones de red. Por ejemplo, cuando un equipo portátil viaja a una ubicación de oficina remota. Cuando un cliente usa la movilidad, es posible que use un punto de administración o un punto de administración proxy del sitio local como su ubicación nueva, antes de intentar usar un servidor de su sitio asignado. En esta lista de servidores de su sitio asignado se incluyen los puntos de administración preferidos. Para obtener más información, vea [Más información sobre cómo los clientes buscan servicios y recursos de sitio](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="overlapping-boundaries"></a>Superposición de los límites  
 Configuration Manager admite configuraciones de límites que se superponen para la ubicación del contenido. Cuando la ubicación de red del cliente pertenece a varios grupos de límites:

-   Cuando un cliente solicita contenido, Configuration Manager envía al cliente una lista de todos los puntos de distribución que lo tienen.  
-   Cuando un cliente solicita a un servidor que envíe o reciba información de migración de su estado, Configuration Manager envía al cliente una lista de todos los puntos de migración de estado asociados a un grupo de límites que incluye la ubicación de red actual del cliente.  

Este comportamiento permite al cliente seleccionar el servidor más cercano desde el que se va a transferir el contenido o información de migración de estado.  



## <a name="example-of-using-boundary-groups"></a>Ejemplo de uso de grupos de límites
En el ejemplo siguiente se usa un cliente que busca contenido desde un punto de distribución. Este ejemplo se puede aplicar a otros roles de sistema de sitio que utilizan grupos de límites. Tenga en cuenta que los puntos de actualización de software no admiten la configuración de reserva en un grupo vecino, por lo que siempre se debe usar un período de 120 minutos.

Cree tres grupos de límites que no compartan los límites ni los servidores de sistema de sitio:
-   Grupo BG_A con puntos de distribución DP_A1 y DP_A2 asociados al grupo
-   Grupo BG_B con puntos de distribución DP_B1 y DP_B2 asociados al grupo
-   Grupo BG_C con puntos de distribución DP_C1 y DP_C2 asociados al grupo

Agregue las ubicaciones de red de los clientes como límites solo al grupo de límites BG_A. Después, configure las relaciones de ese grupo de límites a los otros dos:
-   Configure los puntos de distribución para usar el primer grupo *vecino* (BG_B) después de 10 minutos. Este grupo contiene los puntos de distribución DP_B1 y DP_B2. Ambos están bien conectados a las primeras ubicaciones de límite de grupos.
-   Configure el segundo grupo *vecino* (BG_C) para usarse después de 20 minutos. Este grupo contiene los puntos de distribución DP_C1 y DP_C2. Ambos están separados por WAN de los otros dos grupos de límites.
-   Agregue también al grupo de límites de sitio predeterminado de los sitios otro punto de distribución que se encuentre en el servidor de sitio. Este servidor se encuentra en la ubicación de origen de contenido menos preferida, pero tiene una ubicación central con respecto a todos los grupos de límites.

    Ejemplo de grupos de límites y tiempos de reserva:

     ![Ejemplo de grupos de límites y tiempos de reserva](media/BG_Fallback.png)


Con esta configuración:
-   El cliente comienza a buscar contenido de los puntos de distribución en su grupo de límites *actual* (BG_A). Busca durante dos minutos en cada punto de distribución y, después, cambia al siguiente punto de distribución del grupo de límites. El grupo de clientes de ubicaciones de origen de contenido válidas incluye DP_A1 y DP_A2.
-   Si el cliente no puede encontrar contenido en su grupo de límites *actual* después de buscar durante 10 minutos, agrega los puntos de distribución del grupo de límites BG_B a su búsqueda. Después, continúa la búsqueda de contenido de un punto de distribución en su grupo combinado de servidores. En este grupo ahora se incluyen los servidores de los grupos de límites BG_A y BG_B. El cliente sigue poniéndose en contacto con cada punto de distribución durante dos minutos y después cambia al servidor siguiente de su grupo. El grupo de clientes de ubicaciones de origen de contenido válidas incluye DP_A1, DP_A2, DP_B1 y DP_B2.
-   Después de otros 10 minutos (un total de 20), si el cliente todavía no ha encontrado un punto de distribución con contenido, amplía su grupo para incluir los servidores del segundo grupo de límites *vecino*, BG_C. Ahora el cliente tiene seis puntos de distribución para buscar (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 y DP_C2). Continúa cambiando a un punto de distribución nuevo cada dos minutos hasta que encuentra el contenido.
-   Si el cliente no ha encontrado contenido después de un total de 120 minutos, usa la reserva para incluir el *grupo de límites de sitio predeterminado* como parte de su búsqueda continuada. Ahora el grupo incluye todos los puntos de distribución de los tres grupos de límites configurados y el punto de distribución final ubicado en el servidor de sitio. El cliente sigue buscando contenido, cambiando de punto de distribución cada dos minutos hasta que encuentra contenido.

Mediante la configuración de otros grupos vecinos como disponibles en momentos diferentes, se puede controlar cuándo se agregan puntos de distribución específicos como una ubicación de origen de contenido. El cliente usa la reserva para el grupo de límites de sitio predeterminado como una red de seguridad para el contenido que no está disponible desde ninguna otra ubicación.





<!--
### Update existing boundary groups to the new model
When you update to version prior to 1610, the following configurations are automatically made. This behavior ensures your current fallback behavior remains available until you configure new boundary groups and relationships.

-   Each primary site creates a default site boundary group named ***Default-Site-Boundary-Group&lt;sitecode>***.
  - The primary site adds to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group any state migration points and distribution points configured to **Allow fallback source location for content**.
  - The site adds software update points to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group.
-   The site makes a copy of each existing boundary group that includes a site server configured with a slow connection. The name of the new group is ***&lt;original boundary group name>-&lt;original boundary group ID>***:  
    -   Site systems that have a fast connection are left in the original boundary group.
    -   A copy of site systems (distribution points, management points) that have a slow connection are added to the copy of the boundary group. The original site systems configured as slow remain in their original boundary groups for backward compatibility, but are not used from those boundary groups.
    - This boundary group copy does not have boundaries associated with it. However, A fallback link is created between the original group and the new boundary group copy that has the fallback time set to zero.  


- **Specific to secondary sites:**
  - If a secondary site has at least one state migration point or distribution point enabled to **Allow fallback source location for content**, Configuration Manager creates a boundary group named ***Secondary-Site-Neighbor--Tmp&lt;Sitecode>***. 
  - All distribution points enabled to **Allow fallback source location for content** and state migration points are added to this secondary site boundary group.
  - A fallback link is created between the original boundary group and the newly created neighbor boundary group. The fallback time is set to zero.


 The following table identifies the new fallback behavior you can expect from the combination the original deployment settings and distribution point configurations:

Original deployment configuration for “Do not run program” in slow network  |Original distribution point configuration for “Allow client to use a fallback source location for content”  |New fallback behavior  
---------|---------|---------
Selected     |  Selected    |  **No fallback** - Only use the distribution points in current boundary group       
Selected     |  Not selected|  **No fallback** - Only use the distribution points in current boundary group       
Not selected |  Not selected|  **Fallback to neighbor** - Use the distribution points in current boundary group, and then add the distribution points from the neighbor boundary group. Unless an explicit link to the default site boundary group is configured, clients do not fallback to that group.    
Not selected | Selected     |   **Normal fallback** - Use distribution points in current boundary group, then servers from the neighbor and site default boundary groups

 All other deployment configurations result in **Normal fallback**.  
-->



## <a name="changes-from-prior-versions"></a>Cambios con respecto a las versiones anteriores
Estos son los cambios principales en los grupos de límites y en la forma en que los clientes buscan contenido en Configuration Manager (Rama actual). Muchos de estos conceptos y cambios funcionan conjuntamente.


-   Se quitan las configuraciones de rápido o lento: ya no se configuran los puntos de distribución individuales para que sean rápidos o lentos. En su lugar, se trata igual cada sistema de sitio asociado a un grupo de límites. Debido a este cambio, la pestaña **Referencias** de las propiedades del grupo de límites ya no admite la configuración de Rápido o Lento.
- Nuevo grupo de límites predeterminado en cada sitio: cada sitio primario tiene un grupo de límites predeterminado denominado nuevo ***Grupo-De-Límites-De-Sitio-Predeterminado&lt;código_de_sitio>***. Cuando un cliente no está en una ubicación de red asignada a un grupo de límites, usa los sistemas de sitio asociados con el grupo predeterminado de su sitio asignado. Este grupo de límites se puede considerar un sustituto del concepto de ubicación de contenido de reserva.   
 -  **Permitir a los clientes usar una ubicación de origen de reserva para el contenido** se ha quitado: ya no se configuran puntos de distribución de forma explícita para usarse como reserva. Las opciones para configurar esta opción se han quitado de la consola.

    Además, el resultado de establecer **Permitir a los clientes usar una ubicación de origen de reserva para el contenido** en un tipo de implementación para aplicaciones ha cambiado. Esta opción en un tipo de implementación ahora permite a un cliente usar el grupo de límites de sitio predeterminado como una ubicación de origen de contenido.

 -  Relaciones de grupos de límites: cada grupo de límites se puede vincular a uno o más grupos de límites adicionales. Estos vínculos forman relaciones que se configuran en la nueva pestaña de propiedades de grupos de límites denominada **Relaciones**:
    -   Cada grupo de límites asociado directamente a un cliente se denomina grupo de límites **actual**.  
    -   Cualquier grupo de límites que un cliente pueda usar debido a una asociación entre el grupo de límites *actual* de ese cliente y otro grupo se denomina grupo de límites **vecino**.
    -  Es en la pestaña **Relaciones**, agregue los grupos de límites que se van a usar como grupos de límites *vecinos*. Configure también un tiempo en minutos para la reserva. Cuando un cliente no puede encontrar contenido de un punto de distribución del grupo *actual*, este es el tiempo cuando empieza a buscar ubicaciones de contenido de los grupos de límites *vecinos*.

        Al agregar o cambiar la configuración de un grupo de límites, tiene la opción de bloquear la reserva de ese grupo de límites concreto desde el grupo actual que está configurando.

    Para usar la nueva configuración, defina asociaciones explícitas (vínculos) de un grupo de límites a otro. Configure todos los puntos de distribución de ese grupo asociado con el mismo tiempo en minutos. Cuando un cliente no encuentra un origen de contenido de su grupo de límites *actual*, el tiempo que se configure determina cuándo empieza a buscar orígenes de contenido en su grupo de límites vecino.

    Además de los grupos de límites que se configuran explícitamente, cada grupo de límites tiene un vínculo implícito al grupo de límites de sitio predeterminado. Este vínculo se activa después de 120 minutos. Luego, el grupo de límites de sitio predeterminado se convierte en un grupo de límites vecino. Este comportamiento permite a los clientes usar como ubicaciones de origen de contenido los puntos de distribución asociados a ese grupo de límites.

    Este comportamiento reemplaza a lo que anteriormente se conocía como reserva de contenido. Para invalidar este comportamiento predeterminado de 120 minutos, asocie de forma explícita el grupo de límites de sitio predeterminado a un grupo *actual*. Establezca un tiempo específico en minutos, o bien bloquee completamente la reserva para impedir su uso.


-   Los clientes intentan obtener contenido de cada punto de distribución hasta un máximo de dos minutos: cuando un cliente busca una ubicación de origen de contenido, intenta tener acceso a cada punto de distribución durante dos minutos antes de intentarlo con otro. Este comportamiento supone un cambio con respecto a las versiones anteriores, donde los clientes intentaban conectarse a un punto de distribución hasta un máximo de dos horas.

    - El cliente selecciona aleatoriamente el primer punto de distribución del grupo de servidores disponibles del grupo (o grupos) de límites *actual* del cliente.

    - Después de dos minutos, si el cliente no ha encontrado el contenido, cambia a un nuevo punto de distribución e intenta obtener contenido de ese servidor. Este proceso se repite cada dos minutos hasta que el cliente encuentra el contenido o alcanza el último servidor de su grupo.

    - Si un cliente no puede encontrar una ubicación de origen de contenido válida de su grupo *actual* antes de que se alcance el periodo de reserva para un grupo de límites *vecino*, el cliente agrega los puntos de distribución de ese grupo *vecino* al final de su lista actual. Después, busca en el grupo ampliado de ubicaciones de origen en el que se incluyen los puntos de distribución de ambos grupos de límites.

        > [!TIP]  
        > Al crear un vínculo explícito entre el grupo de límites actual y el grupo de límites de sitio predeterminado, y definir un tiempo de reserva menor que el tiempo de reserva de un vínculo a un grupo de límites vecino, los clientes empiezan a buscar en las ubicaciones de origen del grupo de límites de sitio predeterminado antes de incluir el grupo vecino.

    - Cuando el cliente no puede obtener contenido del último servidor del grupo, el proceso comienza de nuevo.


## <a name="procedures-for-boundary-groups"></a>Procedimientos de los grupos de límites

### <a name="to-create-a-boundary-group"></a>Para crear un grupo de límites  
1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de jerarquía** >  **Grupos de límites**.  

2.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear grupo de límites**.  

3.  En el cuadro de diálogo **Crear grupo de límites**, haga clic en la pestaña **General** y especifique un **Nombre** para este grupo de límites.  

4.  Haga clic en **Aceptar** para guardar el nuevo grupo de límites.  


### <a name="to-configure-a-boundary-group"></a>Para configurar un grupo de límites  
 1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de jerarquía** >  **Grupos de límites**.  

 2.  Seleccione el grupo de límites que desea modificar.  

 3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

 4.  En el cuadro de diálogo **Propiedades** para el grupo de límites, seleccione la pestaña **General** para modificar los límites que son miembros de este grupo de límites:  

     -   Para agregar límites, haga clic en **Agregar**, seleccione la casilla para uno o más límites y, a continuación, haga clic en **Aceptar**.  

     -   Para quitar límites, seleccione el límite y haga clic en **Quitar**.  

 5.  Seleccione la pestaña **Referencias** para modificar la configuración de asignación de sitio y del servidor del sistema de sitio asociado:  

     -   Para habilitar este grupo de límites para que los clientes lo usen para la asignación de sitio, seleccione **Usar este grupo de límites para la asignación de sitio**. Después, seleccione un sitio en la lista desplegable **Sitio asignado**.  

     -   Para configurar qué servidores del sistema sitio disponibles están asociados a este grupo de límites:  

     1.  Haga clic en **Agregar**y, a continuación, seleccione la casilla para uno o más servidores. Los servidores se agregan como servidores del sistema de sitio asociados para este grupo de límites. Solo están disponibles los servidores que admitieron el rol de sistema de sitio que se instaló en ellos.  

         > [!NOTE]  
         >  Puede seleccionar cualquier combinación de sistemas de sitio disponibles en cualquier sitio de la jerarquía. Los sistemas de sitio seleccionados se muestran en la pestaña **Sistemas de sitio** en las propiedades de cada límite miembro de este grupo de límites.  

     2.  Para quitar un servidor de este grupo de límites, seleccione el servidor y, a continuación, haga clic en **Quitar**.  

         > [!NOTE]  
         >  Para que este grupo de límites deje de usarse para asociar sistemas de sitio, quite todos los servidores que se enumeran como servidores de sistema de sitio asociados.  

 6.  Para configurar el comportamiento de reserva, haga clic en la pestaña **Relaciones**:  

     - Haga clic en **Agregar** y, después, seleccione el grupo de límites que quiere configurar.

     - Establezca un tiempo de reserva para los puntos de distribución. Después de este período de tiempo, los clientes del grupo de límites para el que está configurando relaciones podrán empezar a buscar contenido en los puntos de distribución del grupo de límites que está agregando.

     - Para impedir la reserva en un grupo de límites específico, incluido el *grupo de límites de sitio predeterminado* que está configurado de forma predeterminada, seleccione el grupo de límites y, después, active la casilla **No usar reserva nunca**.   

 7.  Haga clic en **Aceptar** para cerrar las propiedades del grupo de límites y guardar la configuración.  

#### <a name="to-associate-a-site-system-server-with-a-boundary-group"></a>Para asociar un servidor de sistema de sitio a un grupo de límites  
 1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de jerarquía** >  **Grupos de límites**.  

 2.  Seleccione el grupo de límites que desea modificar.  

 3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

 4.  En el cuadro de diálogo **Propiedades** correspondiente al grupo de límites, seleccione la pestaña **Referencias** .  

 5.  En **Seleccionar servidores de sistema de sitio**, haga clic en **Agregar**. Seleccione los servidores de sistema de sitio que se van a asociar a este grupo de límites y después haga clic en **Aceptar**.  

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
