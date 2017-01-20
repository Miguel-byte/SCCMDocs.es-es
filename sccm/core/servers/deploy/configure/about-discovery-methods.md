---
title: "Métodos de detección | System Center Configuration Manager"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8bb71e477bb9a265b3485bd3ef8232f6e9933a37

---
# <a name="about-discovery-methods-for-system-center-configuration-manager"></a>Acerca de los métodos de detección para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los métodos de detección de System Center Configuration Manager pueden encontrar diferentes dispositivos en la red o dispositivos y usuarios de Active Directory. Para usar correctamente un método de detección, debe comprender las configuraciones disponibles y las limitaciones.  

##  <a name="a-namebkmkaboutforesta-active-directory-forest-discovery"></a><a name="bkmk_aboutForest"></a> Detección de bosques de Active Directory  
 **Configurable:** Sí  

 **Habilitado de forma predeterminada:** No  

 **Cuentas** que se pueden usar para ejecutar este método:  

-   **Cuenta de detección de bosques de Active Directory** (definida por el usuario)  

-   **Cuenta de equipo** del servidor de sitio  

A diferencia de otros métodos de detección de Active Directory, la detección de bosques de Active Directory no detecta recursos que se puedan administrar. En su lugar, este método detecta ubicaciones de red configuradas en Active Directory y puede convertir esas ubicaciones en límites que se usan en toda la jerarquía.  

Cuando se ejecuta este método, busca el bosque de Active Directory local, cada bosque de confianza y cada bosque adicional que configure en el nodo **Bosques de Active Directory** de la consola de Configuration Manager.  

Use la detección de bosques de Active Directory para:  

-   Detectar sitios y subredes de Active Directory y luego crear límites de Configuration Manager basados en esas ubicaciones de red  

-   Identificar superredes asignadas a un sitio de Active Directory y convertirlas en límites de intervalo de direcciones IP  

-   Publicar en Active Directory Domain Services de un bosque cuando está habilitada la publicación en ese bosque y la cuenta de bosque de Active Directory especificada tiene permisos en dicho bosque  

Puede administrar la detección de bosques de Active Directory en la consola de Configuration Manager desde los nodos siguientes en **Configuración de jerarquía** en el área de trabajo **Administración**:  

-   **Métodos de detección**: aquí puede habilitar la detección de bosques de Active Directory para que se ejecute en el sitio de nivel superior de la jerarquía. También puede especificar un plan sencillo para ejecutar la detección, y configurarlo para crear automáticamente los límites de las subredes IP y los sitios de Active Directory que detecte. No se puede ejecutar la detección de bosques de Active Directory en un sitio primario secundario ni en un sitio secundario.  

-   **Bosques de Active Directory**: aquí puede configurar los bosques de Active Directory adicionales que desea detectar, especificar la cuenta que va a utilizar como cuenta de bosque de Active Directory en cada bosque, y configurar la publicación para cada bosque. Además puede supervisar el proceso de detección y agregar subredes IP y sitios de Active Directory a Configuration Manager como límites y miembros de grupos de límites.  

Para configurar la publicación de bosques de Active Directory para cada sitio de la jerarquía, conecte la consola de Configuration Manager al sitio de nivel superior de la jerarquía. La pestaña **Publicación** del cuadro de diálogo **Propiedades** del sitio de Active Directory solo puede mostrar el sitio actual y sus sitios secundarios. Cuando la publicación está habilitada para un bosque y el esquema de ese bosque se extiende para Configuration Manager, se publica la siguiente información de cada sitio que está habilitado para publicar en ese bosque de Active Directory:  

-    **SMS-Site-&lt;código de sitio>**

-   **SMS-MP-&lt;código de sitio>-&lt;nombre de servidor de sistema de sitio>**  

-   **SMS-SLP-&lt;código de sitio>-&lt;nombre de servidor de sistema de sitio>**  

-   **SMS-&lt;código de sitio>-&lt;subred o nombre de sitio de Active Directory>**  

> [!NOTE]  
>  Los sitios secundarios siempre utilizan la cuenta de equipo del servidor de sitio secundario para publicar en Active Directory. Si desea que los sitios secundarios publiquen en Active Directory, asegúrese de que la cuenta del equipo del servidor de sitio secundario tenga permisos para publicar en Active Directory. Un sitio secundario no puede publicar datos en un bosque que no sea de confianza.  

> [!CAUTION]  
>  Al desactivar la opción para publicar un sitio en un bosque de Active Directory, toda la información anteriormente publicada para ese sitio, incluidos los roles de sistema de sitio disponibles, se elimina del Active Directory de ese bosque.  

Las acciones de detección de bosques de Active Directory se registran en los registros siguientes:  

-   Todas las acciones, con excepción de las relativas a la publicación, se registran en el archivo **ADForestDisc.Log** de la carpeta **&lt;Ruta de instalación>\Logs** del servidor de sitio.  

-   Las acciones de publicación de detección de bosques de Active Directory se registran en **hman.log** y **sitecomp.log** en la carpeta **&lt;Ruta de instalación>\Logs** del servidor de sitio.  

Para más información sobre cómo configurar este método de detección, vea [Configurar métodos de detección para System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="a-namebkmkaboutgroupa-active-directory-group-discovery"></a><a name="bkmk_aboutGroup"></a> Detección de grupos de Active Directory  
**Configurable:** Sí  

**Habilitado de forma predeterminada:** No  

**Cuentas** que se pueden usar para ejecutar este método:  

-   **Cuenta de detección de grupos de Active Directory** (definida por el usuario)  

-   **Cuenta de equipo** del servidor de sitio  

> [!TIP]  
>  Además de la información de esta sección, vea [Características comunes de la detección de grupos, sistemas y usuarios de Active Directory](#bkmk_shared).  

Use este método para buscar en Active Directory Domain Services (AD DS) a fin de identificar:  

-   Grupos de seguridad locales, globales y universales  

-   Pertenencia a grupos  

-   Información limitada acerca de equipos y usuarios de miembros de grupos, incluso si esos equipos y usuarios no se detectaron anteriormente por otro método de detección  

Este método de detección está pensado para identificar grupos y las relaciones de grupo de miembros de grupos. De forma predeterminada, solo se detectan grupos de seguridad. Si además quiere detectar la pertenencia a grupos de distribución, tiene que activar la casilla de verificación de la opción **Detectar la pertenencia de los grupos de distribución** en la pestaña **Opción** del cuadro de diálogo Propiedades de detección de grupos de Active Directory.  

La detección de grupos de Active Directory no es compatible con los atributos extendidos de Active Directory que pueden identificarse mediante la detección de sistemas de Active Directory o la detección de usuarios de Active Directory. Como este método de detección no está optimizado para detectar recursos de equipos y usuarios, tenga en cuenta la posibilidad de ejecutar este método de detección una vez ejecutadas la detección de sistemas de Active Directory y la detección de usuarios de Active Directory. Esto se debe a que este método crea un DDR completo para grupos, pero solo un DDR limitado para equipos y usuarios que son miembros de grupos.  

Puede configurar los siguientes ámbitos de detección que controlan cómo busca información este método:  

-   **Ubicación**: utilice una ubicación si desea buscar en uno o varios contenedores de Active Directory. Esta opción de ámbito es compatible con una búsqueda recurrente de los contenedores de Active Directory especificados que también busca en cada contenedor secundario del contenedor que especifique. Este proceso continúa hasta que no se encuentren más contenedores secundarios.  

-   **Grupos**: utilice grupos si desea buscar en uno o varios grupos específicos de Active Directory. Puede configurar el **Dominio de Active Directory** para que utilice el dominio y el bosque predeterminados o limitar la búsqueda a un controlador de dominio determinado. Además, puede especificar uno o más grupos en los que realizar la búsqueda. Si no especifica al menos un grupo, la búsqueda se realizará en todos los grupos que se encuentren en el **Dominio de Active Directory** especificado.  

> [!CAUTION]  
>  Cuando se configura un ámbito de detección, seleccione solo los grupos que debe detectar. Esto se debe a que la detección de grupos de Active Directory intenta detectar cada miembro de cada grupo del ámbito de detección. La detección de grupos grandes puede requerir un uso considerable de ancho de banda y de recursos de Active Directory.  

> [!NOTE]  
>  Para crear colecciones basadas en atributos extendidos de Active Directory (y para garantizar unos resultados de detección precisos para equipos y usuarios), ejecute la detección de sistemas o de usuarios de Active Directory, según lo que quiera detectar.  

Las acciones de detección de grupos de Active Directory se registran en el archivo **adsgdis.log** de la carpeta **&lt;Ruta de instalación\>\LOGS** del servidor de sitio.  

Para más información sobre cómo configurar este método de detección, vea [Configurar métodos de detección para System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="a-namebkmkaboutsystema-active-directory-system-discovery"></a><a name="bkmk_aboutSystem"></a> Detección de sistemas de Active Directory  
**Configurable:** Sí  

**Habilitado de forma predeterminada:** No  

**Cuentas** que se pueden usar para ejecutar este método:  

-   **Cuenta de detección de sistemas de Active Directory** (definida por el usuario)  

-   **Cuenta de equipo** del servidor de sitio  

> [!TIP]  
>  Además de la información de esta sección, vea [Características comunes de la detección de grupos, sistemas y usuarios de Active Directory](#bkmk_shared).  

Use este método de detección para buscar en las ubicaciones especificadas de Active Directory Domain Services (AD DS) recursos informáticos que se puedan usar para crear colecciones y consultas. También puede instalar el cliente de Configuration Manager en un dispositivo detectado mediante la instalación de inserción de cliente.  

De forma predeterminada, este método detecta información básica sobre el equipo, incluido lo siguiente:  

-   Nombre del equipo  

-   Sistema operativo y versión  

-   Nombre de contenedor de Active Directory  

-   Dirección IP  

-   Sitio de Active Directory  

-   Marca de tiempo de último inicio de sesión  

Para crear correctamente un registro de datos de detección (DDR) para un equipo, la detección de sistemas de Active Directory debe poder identificar la cuenta de equipo y resolver el nombre del equipo en una dirección IP.  

Puede ver la lista completa de atributos predeterminados de objetos devueltos por la detección de sistemas de Active Directory y configurar el método para detectar atributos adicionales (extendidos) en el cuadro de diálogo **Propiedades de detección de sistemas de Active Directory** de la pestaña **Atributos de Active Directory**.  

Las acciones de detección de sistemas de Active Directory se registran en el archivo **adsysdis.log** de la carpeta **&lt;Ruta de instalación\>\LOGS** del servidor de sitio.  

Para más información sobre cómo configurar este método de detección, vea [Configurar métodos de detección para System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="a-namebkmkaboutusera-active-directory-user-discovery"></a><a name="bkmk_aboutUser"></a> Detección de usuario de Active Directory  
**Configurable:** Sí  

**Habilitado de forma predeterminada:** No  

**Cuentas** que se pueden usar para ejecutar este método:  

-   **Cuenta de detección de usuarios de Active Directory** (definida por el usuario)  

-   **Cuenta de equipo** del servidor de sitio  

> [!TIP]  
>  Además de la información de esta sección, vea [Características comunes de la detección de grupos, sistemas y usuarios de Active Directory](#bkmk_shared).  

Use este método de detección para buscar en Active Directory Domain Services (AD DS) e identificar cuentas de usuario y atributos asociados.  De forma predeterminada, este método detecta información básica sobre la cuenta de usuario, incluido lo siguiente:  

-   Nombre de usuario  

-   Nombre de usuario único (incluye el nombre de dominio)  

-   Dominio  

-   Nombres de contenedor de Active Directory  

Puede ver la lista completa predeterminada de atributos de objetos devueltos por la detección de usuarios de Active Directory y configurar el método para detectar atributos adicionales (extendidos) en el cuadro de diálogo **Propiedades de detección de usuarios de Active Directory** de la pestaña **Atributos de Active Directory**.  

Las acciones de detección de usuarios de Active Directory se registran en el archivo **adusrdis.log** de la carpeta **&lt;Ruta de instalación\>\LOGS** del servidor de sitio.  

Para más información sobre cómo configurar este método de detección, vea [Configurar métodos de detección para System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="a-namebkmkaboutheartbeata-heartbeat-discovery"></a><a name="bkmk_aboutHeartbeat"></a> Detección de latidos  
**Configurable:** Sí  

**Habilitado de forma predeterminada:** Sí  

**Cuentas** que se pueden usar para ejecutar este método:  

-   **Cuenta de equipo** del servidor de sitio  

La detección de latidos difiere de otros métodos de detección de Configuration Manager. Está habilitada de forma predeterminada y se ejecuta en cada equipo cliente (en lugar de en un servidor de sitio) para crear un registro de datos de detección (DDR). Para los clientes de dispositivos móviles, el punto de administración, que el cliente del dispositivo móvil utiliza, crea este DDR.  Para mantener el registro de base de datos de los clientes de Configuration Manager, no deshabilite la detección de latidos.  Además de mantener el registro de base de datos, este método puede forzar la detección de un equipo como un nuevo registro de recursos o puede volver a llenar el registro de base de datos de un equipo que se eliminó de la base de datos.  

La detección de latidos se ejecuta en una programación configurada para todos los clientes de la jerarquía o, si se invoca manualmente, en un cliente específico mediante la ejecución de **Ciclo de recopilación de datos de descubrimiento** de la pestaña **Acción** del programa Configuration Manager de un cliente. El plan predeterminado para la detección de latidos está establecido en cada 7 días. Si modifica el intervalo de detección de latidos, asegúrese de que se ejecuta con mayor frecuencia que la tarea de mantenimiento del sitio **Eliminar datos de detección antiguos**, que elimina registros de clientes inactivos en la base de datos del sitio. Puede configurar la tarea **Eliminar datos de detección antiguos** solo para sitios primarios.  

Cuando se ejecuta la detección de latidos, crea un DDR que contiene la información actual del cliente. Después, el cliente copia este pequeño archivo (aproximadamente 1 KB) en un punto de administración para que pueda ser procesado por un sitio primario.  El archivo contiene la siguiente información:  

-   Ubicación de red  

-   Nombre de NetBIOS  

-   Versión del agente cliente  

-   Detalles del estado operativo  

La detección de latidos es el único método de detección que proporciona detalles sobre el estado de instalación del cliente. Para ello, actualiza el atributo de cliente de un recurso del sistema para establecer un valor igual a **Sí**.  

> [!NOTE]  
>  Incluso cuando se deshabilita la detección de latidos, todavía se crean y se envían DDR a clientes de dispositivos móviles activos. Esto garantiza que la tarea **Eliminar datos de detección antiguos** no afecte a los dispositivos móviles activos. Esto se hace porque cuando la tarea **Eliminar datos de detección antiguos** elimina un registro de base de datos de un dispositivo móvil, también revoca el certificado del dispositivo y evita que este se conecte con los puntos de administración.  

Las acciones de detección de latidos se registran en las siguientes ubicaciones:  

-   En los clientes de equipos, las acciones de detección de latidos se registran en el cliente de **InventoryAgent.log** de la carpeta *%Windir%\CCM\Logs*.  

-   Para clientes de dispositivos móviles, las acciones de detección de latidos se registran en el **DMPRP.log** de la carpeta *%Program Files%\CCM\Logs* del punto de administración que el cliente del dispositivo móvil utiliza.  

Para más información sobre cómo configurar este método de detección, vea [Configurar métodos de detección para System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="a-namebkmkaboutnetworka-network-discovery"></a><a name="bkmk_aboutNetwork"></a> Detección de redes  
**Configurable:** Sí  

**Habilitado de forma predeterminada:** No  

**Cuentas** que se pueden usar para ejecutar este método:  

-   **Cuenta de equipo** del servidor de sitio  

Use este método para detectar la topología de la red y para detectar dispositivos de la red que tengan una dirección IP. Detección de redes busca en la red recursos habilitados para IP mediante la consulta de servidores que ejecutan una implementación de Microsoft de DHCP, memorias caché del Protocolo de resolución de direcciones (ARP) en enrutadores, dispositivos habilitados para SNMP y dominios de Active Directory.  

Para usar la detección de redes, debe especificar el **nivel** de detección que se va a ejecutar. También puede configurar uno o más mecanismos de detección que permiten a Detección de redes consultar segmentos o dispositivos de red. Puede configurar asimismo las opciones que ayudan a controlar las acciones de detección en la red. Por último, puede definir una o más programaciones para la ejecución de Detección de redes.  

Para que este método detecte correctamente un recurso, la detección de redes debe identificar la dirección IP y la máscara de subred del recurso. Se usan los siguientes métodos para identificar la máscara de subred de un objeto:  

-   **Caché ARP del enrutador:** la detección de redes consulta a la caché ARP de un enrutador para buscar información de subred. Normalmente, los datos de una caché ARP del enrutador tienen un corto período de vida. Por tanto, cuando la detección de redes consulta a la caché ARP, es posible que esta ya no contenga información sobre el objeto solicitado.  

-   **DHCP:** la detección de redes consulta a cada servidor DHCP especificado para detectar los dispositivos para los que el servidor DHCP ha proporcionado una concesión. La detección de redes sólo admite servidores DHCP en que se ejecuta la implementación de DHCP de Microsoft.  

-   **Dispositivo SNMP:** la detección de redes puede consultar directamente a un dispositivo SNMP. Para que la detección de redes consulte un dispositivo, este último debe tener instalado un agente SNMP local. También se debe configurar la detección de redes para utilizar el nombre de comunidad utilizado por el agente SNMP.  

Cuando la detección identifica un objeto IP direccionable y puede determinar la máscara de subred de objetos, crea un registro de datos de detección (DDR) para ese objeto. Debido a que pueden conectarse a la red diferentes tipos de dispositivos, la detección de redes puede detectar recursos que no son compatibles con el software cliente de Configuration Manager. Por ejemplo, entre los dispositivos que se pueden detectar, pero no administrar, se incluyen impresoras y enrutadores.  

Detección de redes puede devolver varios atributos como parte del registro de detección que se crea. Entre ellos, se incluye:  

-   Nombre de NetBIOS  

-   Direcciones IP  

-   Dominio de recursos  

-   Roles del sistema  

-   Nombre de comunidad SNMP  

-   Direcciones MAC  

La actividad de la detección de redes se registra en **Netdisc.log** de **&lt;Ruta de instalación\>\Logs** del servidor de sitio que ejecuta la detección.  

 Para más información sobre cómo configurar este método de detección, vea [Configurar métodos de detección para System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

> [!NOTE]  
>  Las redes complejas y las conexiones de ancho de banda reducido pueden provocar que Detección de redes se ejecute lentamente y genere mucho tráfico de red. Como práctica recomendada, ejecute Detección de redes solo cuando los otros métodos de detección no puedan encontrar los recursos que debe detectar. Por ejemplo, puede utilizar Detección de redes si debe detectar equipos de grupos de trabajo. Los equipos de grupos de trabajo no se detectan mediante otros métodos de detección.  

###  <a name="a-namebkmknetdisclevelsa-levels-of-network-discovery"></a><a name="BKMK_NetDiscLevels"></a> Niveles de detección de redes  
Al configurar Detección de redes, se puede especificar uno de los tres niveles de detección:  

|Nivel de detección|Detalles|  
|------------------------|-------------|  
|Topología|Este nivel detecta los enrutadores y subredes, pero no identifica una máscara de subred para los objetos.|  
|Topología y cliente|Además de la topología, este nivel detecta posibles clientes como equipos y recursos, tales como impresoras y enrutadores. Este nivel de detección intenta identificar la máscara de subred de los objetos que encuentra.|  
|Topología, cliente y sistema operativo de cliente|Además de la topología y posibles clientes, este nivel intenta detectar el nombre y la versión del sistema operativo del equipo. Este nivel utiliza el Explorador de Windows y las llamadas a redes de Windows.|  

 Con cada nivel de incremento, Detección de redes aumenta su actividad y el uso de ancho de banda de red. Tenga en cuenta el tráfico de red que puede generarse antes de habilitar todos los aspectos de Detección de redes.  

 Por ejemplo, cuando se utiliza Detección de redes por primera vez, puede comenzar únicamente por el nivel de topología para identificar la infraestructura de red. A continuación, puede volver a configurar Detección de redes para que se detecten objetos y sus sistemas operativos de dispositivos. También puede configurar opciones que limiten Detección de redes a un intervalo específico de segmentos de red para detectar objetos en ubicaciones de red que necesite, y evitar un tráfico de red innecesario y la detección de objetos desde enrutadores perimetrales o desde fuera de la red.  

###  <a name="a-namebkmknetdiscoptionsa-network-discovery-options"></a><a name="BKMK_NetDiscOptions"></a> Opciones de detección de redes  
Para que la detección de redes pueda buscar dispositivos IP direccionables, debe configurar una o varias de las siguientes opciones que especifican cómo buscar dispositivos.  

> [!NOTE]  
>  Detección de redes se ejecuta en el contexto de la cuenta de equipo del servidor de sitio que ejecuta la detección. Si la cuenta de equipo no tiene permisos para un dominio que no es de confianza, es posible que las configuraciones de dominio y de servidor DHCP no consigan detectar recursos.  

**DHCP:**  

Especifique cada servidor DHCP que desea que consulte Detección de redes. (La detección de redes solo admite servidores DHCP que ejecutan la implementación de DHCP de Microsoft)  

-   Detección de redes recupera información mediante llamadas a procedimiento remoto en la base de datos del servidor DHCP.  

-   Detección de redes puede consultar servidores DHCP de 32 y 64 bits para obtener una lista de los dispositivos que están registrados en cada servidor.  

-   Para que Detección de redes consulte correctamente un servidor DHCP, la cuenta de equipo del servidor que ejecuta la detección debe ser miembro del grupo Usuarios de DHCP del servidor DHCP. Por ejemplo, este nivel de acceso existe cuando se cumple una de las siguientes acciones:  

    -   El servidor DHCP especificado es el servidor DHCP del servidor que ejecuta la detección.  

    -   El equipo que ejecuta la detección y el servidor DHCP están en el mismo dominio.  

    -   Existe una confianza bidireccional entre el equipo que ejecuta la detección y el servidor DHCP.  

    -   El servidor de sitio es miembro del grupo de usuarios de DHCP.  

-   Cuando Detección de redes enumera un servidor DHCP, no siempre detecta direcciones IP estáticas. Detección de redes no encuentra direcciones IP que forman parte de un intervalo de direcciones IP excluido en el servidor DHCP y no detecta direcciones IP que están reservadas para su asignación manual.  

**Dominios:**  

Especifique cada dominio que desea que consulte Detección de redes.  

-   La cuenta de equipo del servidor de sitio que ejecute la detección debe tener permisos para leer los controladores de dominio en cada dominio especificado.  

-   Para detectar equipos del dominio local, debe habilitar el servicio Explorador de equipos en al menos un equipo que se encuentre en la misma subred que el servidor de sitio que ejecuta la detección de redes.  

-   La detección de redes puede detectar cualquier equipo que se pueda ver desde el servidor de sitio al examinar la red,  

-   Detección de redes recupera la dirección IP y utiliza una solicitud de eco del Protocolo de mensajes de control de Internet para hacer ping a cada dispositivo que encuentre. El comando **ping** ayuda a determinar qué equipos están activos actualmente.  

**Dispositivos SNMP:**  

Especifique cada dispositivo SNMP que desea que consulte Detección de redes.  

-   La detección de redes recupera el valor ipNetToMediaTable desde cualquier dispositivo SNMP que responda a la consulta. Este valor devuelve matrices de direcciones IP que son equipos cliente u otros recursos como impresoras, enrutadores u otros dispositivos IP direccionables.  

-   Para consultar un dispositivo, debe especificar la dirección IP o el nombre de NetBIOS del mismo.  

-   Debe configurar Detección de redes para que utilice el nombre de comunidad del dispositivo o el dispositivo rechazará la consulta basada en SNMP.  

###  <a name="a-namebkmklimitnetdisca-limiting-network-discovery"></a><a name="BKMK_LimitNetDisc"></a> Limitación de la detección de redes  
Cuando Detección de redes consulta un dispositivo SNMP en el perímetro de la red, puede identificar información acerca de las subredes y los dispositivos SNMP que se encuentran fuera de la red inmediata. Use la siguiente información para limitar la detección de redes mediante la configuración de los dispositivos SNMP con los que se puede comunicar la detección y mediante la especificación de los segmentos de red que se van a consultar.  

**Subredes:**  

Configure las subredes en que la detección de redes realiza consultas cuando utiliza las opciones DHCP y SNMP. Estas dos opciones sólo buscan en las subredes habilitadas.  

Por ejemplo, una solicitud DHCP puede devolver los dispositivos desde ubicaciones de toda la red. Si desea que solo se detecten los dispositivos de una subred concreta, especifique y habilite dicha subred en la pestaña **Subredes** del cuadro de diálogo **Propiedades de Detección de redes** . Al especificar y habilitar las subredes, se limitan futuras operaciones de detección DHCP y SNMP en esas subredes.  

> [!NOTE]  
>  La configuración de las subredes no limita los objetos detectados con la opción de detección de dominios.  

**Nombres de comunidades SNMP:**  

Para habilitar la detección de redes para consultar correctamente un dispositivo SNMP, configure la detección de redes con el nombre de comunidad del dispositivo. Si la detección de redes no está configurada con el nombre de comunidad del dispositivo SNMP, este último rechaza la consulta.  

**Número máximo de saltos:**  

Cuando se configura el número máximo de saltos de enrutador, se limita el número de segmentos de red y enrutadores que puede consultar la detección de redes con SNMP.  

-   El número de saltos configurado limita el número de segmentos de red y dispositivos adicionales que puede consultar la detección de red.  

 Por ejemplo, una detección solo de topología con **0** (cero) saltos de enrutador detecta la subred en que reside el servidor de origen e incluye todos los enrutados de dicha subred.  

En el diagrama siguiente se muestra qué encuentra la detección de redes de solo topología cuando se ejecuta en el servidor 1 con 0 saltos de enrutador definidos: subred D y enrutador 1.  

 ![Imagen de detección con cero saltos de enrutador](media/Disc-0.gif)  

 En el diagrama siguiente se muestra qué encuentra una detección de redes de clientes y topologías cuando se ejecuta en el servidor 1 con 0 saltos de enrutador definidos: subred D y enrutador 1, así como todos los clientes posibles en la subred D.  

 ![Imagen de detección con un salto de enrutador](media/Disc-1.gif)  

 Para hacerse una idea más clara de cómo los saltos de enrutador adicionales pueden aumentar la cantidad de recursos de red detectados, tenga en cuenta la siguiente red:  

 ![Imagen de detección con dos saltos de enrutador](media/Disc-2.gif)  

 Al ejecutar una detección de redes de solo topología desde el servidor 1 con un salto de enrutador, se detecta lo siguiente:  

-   Enrutador 1 y subred 10.1.10.0 (encontrados con cero saltos).  

-   Subredes 10.1.20.0 y 10.1.30.0, subred A y enrutador 2 (encontrados en el primer salto).  

> [!WARNING]  
>  Cada incremento del número de saltos de enrutador puede aumentar significativamente el número de recursos detectables y el ancho de banda de red que consume la detección de redes.  

##  <a name="a-namebkmkaboutservera-server-discovery"></a><a name="bkmk_aboutServer"></a> Detección de servidores  
**Configurable:** No  

Además de los métodos de detección configurables por el usuario, Configuration Manager también emplea un proceso denominado **detección de servidores** (SMS_WINNT_SERVER_DISCOVERY_AGENT). Este método de detección crea registros de recursos para los equipos que son sistemas de sitio, por ejemplo, un equipo que esté configurado como un punto de administración.  

##  <a name="a-namebkmkshareda-common-features-of-active-directory-group-system-and-user-discovery"></a><a name="bkmk_shared"></a> Características comunes de la detección de grupos, sistemas y usuarios de Active Directory  
En esta sección se proporciona información sobre las características que son comunes a los siguientes métodos de detección:  

-   Detección de grupos de Active Directory  

-   Detección de sistemas de Active Directory  

-   Detección de usuario de Active Directory  

> [!NOTE]  
>  La información de esta sección no se aplica a la detección de bosques de Active Directory.  

Estos tres métodos de detección son similares en configuración y funcionamiento, y pueden detectar equipos, usuarios e información acerca de pertenencia a grupos de los recursos almacenados en Servicios de dominio de Active Directory. El proceso de la detección lo administra un agente de detección que se ejecuta en el servidor de sitio en cada sitio donde se configura la ejecución de la detección. Puede configurar cada uno de estos métodos de detección para buscar una o más ubicaciones de Active Directory como instancias de ubicación en el bosque local o los bosques remotos.  

Cuando la detección busca recursos en un bosque que no es de confianza, el agente de detección debe ser capaz de resolver lo siguiente para tener éxito:  

-   Para detectar un recurso de equipo con la detección de sistemas de Active Directory, el agente de detección debe ser capaz de resolver el FQDN del recurso. Si no puede resolver el FQDN, a continuación, intentará resolver el recurso por su nombre NetBIOS.  

-   Para detectar un recurso de usuario o grupo con la detección de usuarios de Active Directory o la detección de grupos de Active Directory, el agente de detección debe ser capaz de resolver el FQDN del nombre de controlador de dominio que especifique para la ubicación de Active Directory.  

Para cada ubicación que especifique, puede configurar opciones de búsqueda individuales, como habilitar una búsqueda recursiva de los contenedores secundarios de Active Directory de las ubicaciones. También puede configurar una cuenta única para usarla cuando realice una búsqueda en esa ubicación. Esto proporciona flexibilidad a la hora de configurar un método de detección en un sitio para buscar varias ubicaciones de Active Directory en varios bosques, sin tener que configurar una cuenta única que tenga permisos para todas las ubicaciones.  

Cuando estos tres métodos de detección se ejecutan en un sitio específico, el servidor de sitio de Configuration Manager de dicho sitio se pone en contacto con el controlador de dominio más próximo del bosque de Active Directory especificado para buscar los recursos de Active Directory. El dominio y el bosque pueden estar en cualquier modo de Active Directory admitido, y la cuenta que asigne a cada instancia de ubicación debe tener permiso de acceso de **Lectura** en las ubicaciones de Active Directory especificadas. La detección busca objetos en las ubicaciones definidas, e intenta recopilar información acerca de ellos. Cuando se puede identificar suficiente información sobre un recurso, se crea un registro de datos de detección (DDR). La información necesaria varía en función del método de detección que se utilice.  

Si configura el mismo método de detección para que se ejecute en diferentes sitios de Configuration Manager a fin de sacar partido de la consulta de servidores locales de Active Directory, puede configurar cada sitio con un único conjunto de opciones de detección. Dado que los datos de detección se comparten con cada sitio de la jerarquía, evite la superposición entre estas configuraciones para detectar de forma eficaz una sola vez cada recurso. En entornos más pequeños, puede tener en cuenta la posibilidad de ejecutar cada método de detección en un único sitio de la jerarquía para reducir la sobrecarga administrativa y el potencial para que varias acciones de detección detecten de nuevo los mismos recursos. Al minimizar el número de sitios que ejecutan la detección, puede reducir el ancho de banda de red total empleado por la detección y disminuir el número total de DDR que se crean y que los servidores de sitio deben procesar.  

Muchas de las configuraciones del método de detección se explican por sí mismas. Utilice las siguientes secciones para obtener más información acerca de las opciones de detección que pueden requerir información adicional antes de configurarlas.  

Las siguientes opciones están disponibles con varios métodos de detección de Active Directory:  

-   [Detección de diferencias](#bkmk_delta)  

-   [Filtrar registros informáticos obsoletos por inicio de sesión de dominio](#bkmk_stalelogon)  

-   [Filtrar registros obsoletos por contraseña de equipo](#bkmk_stalepassword)  

-   [Buscar atributos personalizados de Active Directory](#bkmk_customAD)  

###  <a name="a-namebkmkdeltaa-delta-discovery"></a><a name="bkmk_delta"></a> Detección de diferencias  
Disponible para:  

-   Detección de grupos de Active Directory  

-   Detección de sistemas de Active Directory  

-   Detección de usuario de Active Directory  

La detección de diferencias no es un método de detección independiente, sino una opción disponible para los métodos de detección aplicables. La detección de diferencias busca cambios realizados desde el último ciclo de detección completo del método de detección aplicable en atributos específicos de Active Directory.  Esta búsqueda usa menos recursos que un ciclo de detección completo y los cambios de los atributos se envían a la base de datos de Configuration Manager para actualizar el registro de detección del recurso.  

De forma predeterminada, la detección de diferencias se ejecuta en un ciclo de cinco minutos. Esta frecuencia es superior a la programación típica de un ciclo de detección completo.  Esta frecuencia es posible porque la detección de diferencias usa menos recursos de servidor de sitio y red que un ciclo de detección completo. Cuando use la detección de diferencias, puede reducir la frecuencia del ciclo de detección completo de ese método de detección.  

Los cambios siguientes son los cambios más comunes que encuentra la detección de diferencias:  

-   Nuevos equipos o usuarios agregados a Active Directory  

-   Cambios en la información básica de equipos y usuarios  

-   Nuevos equipos o usuarios que se agregan a un grupo  

-   Equipos o usuarios que se quitan de un grupo  

-   Cambios en los objetos de grupo del sistema  

Aunque la detección de diferencias puede detectar nuevos recursos y cambios en la pertenencia a grupos, no puede detectar si se ha eliminado un recurso de Active Directory. Los DDR creados por la detección de diferencias se procesan de forma similar a los DDR que se crean mediante un ciclo de detección completo.  

La detección de diferencias se configura en la pestaña **Programación de sondeo** de las propiedades para cada método de detección.  

###  <a name="a-namebkmkstalelogona-filter-stale-computer-records-by-domain-logon"></a><a name="bkmk_stalelogon"></a> Filtrar registros informáticos obsoletos por inicio de sesión de dominio  
Disponible para:  

-   Detección de grupos de Active Directory  

-   Detección de sistemas de Active Directory  

Puede configurar la detección para que excluya a los equipos con un registro informático obsoleto en función del último inicio de sesión de dominio del equipo. Cuando esta opción está habilitada, la detección de sistemas de Active Directory evalúa cada equipo que identifica. La detección de grupos de Active Directory evalúa cada equipo que es miembro de un grupo que se detecta.  

Para usar esta opción:  

-   Los equipos deben estar configurados para actualizar el atributo **lastLogonTimeStamp** en Active Directory Domain Services.  

-   El nivel funcional de dominio de Active Directory debe estar establecido en Windows Server 2003 o posterior.  

Al configurar el tiempo después del último inicio de sesión que quiere usar para esta configuración, tenga en cuenta el intervalo para la replicación entre controladores de dominio.  

El filtrado se configura en la pestaña **Opción** de los cuadros de diálogo **Propiedades de detección de sistemas de Active Directory** y **Propiedades de detección de grupos de Active Directory** mediante la selección de la opción **Detectar solo los equipos que iniciaron sesión en un dominio en un determinado período de tiempo**.  

> [!WARNING]  
>  Al configurar este filtro y **Filtrar registros obsoletos por contraseña de equipo**, los equipos que cumplen los criterios de cada filtro se excluyen de la detección.  

###  <a name="a-namebkmkstalepassworda-filter-stale-records-by-computer-password"></a><a name="bkmk_stalepassword"></a> Filtrar registros obsoletos por contraseña de equipo  
Disponible para:  

-   Detección de grupos de Active Directory  

-   Detección de sistemas de Active Directory  

Puede configurar la detección para que excluya a los equipos con un registro informático obsoleto en función de la última actualización de contraseña de la cuenta de equipo realizada por el equipo. Cuando esta opción está habilitada, la detección de sistemas de Active Directory evalúa cada equipo que identifica. La detección de grupos de Active Directory evalúa cada equipo que es miembro de un grupo que se detecta.  

Para usar esta opción:  

-   Los equipos deben estar configurados para actualizar el atributo **pwdLastSet** en Active Directory Domain Services.  

Al configurar esta opción, tenga en cuenta el intervalo de las actualizaciones para este atributo, además del intervalo de replicación entre controladores de dominio.  

El filtrado se configura en la pestaña **Opción** de los cuadros de diálogo **Propiedades de detección de sistemas de Active Directory** y **Propiedades de detección de grupos de Active Directory** mediante la selección de la opción **Detectar solo los equipos que actualizaron su contraseña de cuenta de equipo en un determinado período de tiempo**.  

> [!WARNING]  
>  Al configurar este filtro y **Filtrar registros obsoletos por inicio de sesión de dominio**, los equipos que cumplen los criterios de cada filtro se excluyen de la detección.  

###  <a name="a-namebkmkcustomada-search-customized-active-directory-attributes"></a><a name="bkmk_customAD"></a> Buscar atributos personalizados de Active Directory  
 Disponible para:  

-   Detección de sistemas de Active Directory  

-   Detección de usuario de Active Directory  

Cada método de detección es compatible con una lista única de atributos de Active Directory que se pueden detectar.  

Puede ver y configurar la lista de atributos personalizados en la pestaña **Atributos de Active Directory** de los cuadros de diálogo **Propiedades de detección de sistemas de Active Directory** y **Propiedades de detección de usuarios de Active Directory**.  



<!--HONumber=Nov16_HO1-->


