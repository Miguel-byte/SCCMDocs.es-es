---
title: Buscar recursos de sitio | System Center Configuration Manager
description: "Comprenda cómo y cuándo los clientes de System Center Configuration Manager usan la ubicación del servicio para buscar recursos de sitio."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5d718d0f9b8c6121f3124a8ade7507c61b7313f2
ms.openlocfilehash: cad4ebd3f8fa275d7d2cad9b2b87c32b971c580d


---
# <a name="understand-how-clients-find-site-resources-and-services-for-system-center-configuration-manager"></a>Comprender cómo los clientes buscan servicios y recursos de sitio para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los clientes de System Center Configuration Manager usan un proceso denominado **ubicación del servicio** para ubicar servidores de sistema de sitio con los que poder comunicarse y que ofrecen servicios a los que se dirige a los clientes para que los usen.   Comprender cómo y cuándo los clientes usan la ubicación del servicio para encontrar recursos de sitio puede ayudarle a configurar los sitios para admitir correctamente las operaciones de cliente.   Estas configuraciones pueden requerir que el sitio interactúe con las configuraciones de dominio y red, como los servicios de dominio de Active Directory (AD DS) y DNS, o que usted configure alternativas más complejas.  

 Algunos ejemplos de roles de sistema de sitio que proporcionan servicios pueden ser el servidor de sistema de sitio principal para clientes, el punto de administración y los servidores de sistema de sitio adicionales con los que el cliente puede comunicarse, como los puntos de distribución y de actualización de software.  



##  <a name="a-namebkmkfunda-fundamentals-of-service-location"></a><a name="bkmk_fund"></a> Fundamentals of service location  
 Un cliente evalúa su ubicación de red actual, la preferencia del protocolo de comunicación y el sitio asignado al usar una ubicación de servicio para encontrar un punto de administración con el que poder comunicarse.  

 **Un cliente se comunica con un punto de administración para:**  
-   Descargar información sobre otros puntos de administración para el sitio, de forma que puedan generar una lista de puntos de administración para futuros ciclos de ubicación de servicio.  
-   Cargar detalles de configuración, como el inventario y estado.  
-   Descargar la directiva que establece la configuración en el cliente e informar al cliente del software que puede o debe instalar, así como otras tareas relacionadas.  
-   Solicitar información sobre los roles de sistema de sitios adicionales que proporcionan servicios que se pueden usar con la configuración del cliente, como puntos de distribución de software para software que puede instalar o un punto de actualización de software desde el que puede obtener las actualizaciones.  

**Un cliente de Configuration Manager realiza una solicitud de ubicación del servicio:**  
-   Cada 25 horas de funcionamiento continuo  
-   Cuando el cliente detecta un cambio de su ubicación o configuración de red  
-   Cuando se inicia el servicio **ccmexec.exe** del equipo (el servicio de cliente principal)  
-   Cuando el cliente debe encontrar un rol de sistema de sitio que proporcione un servicio necesario  

**Al intentar encontrar servidores que hospedan roles de sistema de sitio**, el cliente usa la ubicación del servicio para encontrar un rol de sistema de sitio que admita el protocolo del cliente (HTTP o HTTPS). Los clientes usan de forma predeterminada el método más seguro que tengan a su disposición:  

-   Para usar HTTPS, es necesario disponer de una infraestructura de clave pública (PKI) e instalar certificados PKI en los clientes y servidores. Para más información sobre el uso de certificados, consulte [Requisitos de certificados PKI para System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

-   Cuando se implementa un rol de sistema de sitio que usa Internet Information Services (IIS) y que admite la comunicación desde clientes, es necesario especificar si los clientes se conectan al sistema de sitio mediante HTTP o HTTPS. Si utiliza HTTP, también debe tener en cuenta las opciones de firma y cifrado. Para obtener más información, consulte [Planeación de la firma y el cifrado](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) en el tema [Planear la seguridad en System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md).  

##  <a name="a-namebkmkplanservicelocationa-service-location-and-how-clients-determine-their-assigned-management-point"></a><a name="BKMK_Plan_Service_Location"></a> Ubicación del servicio y cómo los clientes averiguan su punto de administración asignado  
Cuando un cliente se asigna primero a un sitio primario, este selecciona un punto de administración predeterminado para ese sitio. (Los sitios principales admiten varios puntos de administración, y cada uno de los clientes identifica un punto de administración de forma independiente como su punto de administración predeterminado).  Este punto de administración predeterminado luego se convierte en el punto de administración asignado a ese cliente. (También puede usar comandos de instalación de cliente para establecer el punto de administración asignado para un cliente en el momento en que se instala).  

-   Los clientes seleccionan un punto de administración con el cual comunicarse, en función de las configuraciones de ubicación de red actual y de grupo de límites. Aunque tenga un punto de administración asignado, puede que este no sea el punto de administración que el cliente usa.  

    > [!NOTE]  
    >  Un cliente siempre usa el punto de administración asignado para los mensajes de registro y para determinados mensajes de la directiva, aun cuando se envíen otras comunicaciones a un punto de administración proxy o local.  

-   Puede usar puntos de administración preferidos. Un punto de administración preferido es un punto de administración que está asociado a un grupo de límites como servidor de sistema de sitio, de manera similar a cómo los puntos de distribución o puntos de migración de estado están asociados a un grupo de límites. Si habilita puntos de administración preferidos para la jerarquía, cuando un cliente usa un punto de administración desde su sitio asignado intentará usar un punto de administración preferido antes de usar otros puntos de administración desde su sitio asignado.  

-   También puede usar la información del siguiente blog de TechNet.com para configurar la afinidad del punto de administración. La afinidad del punto de administración invalida el comportamiento predeterminado de los puntos de administración asignados y permite al cliente usar uno o varios puntos de administración determinados: [afinidad de punto de administración](http://blogs.technet.com/b/jchalfant/archive/2014/09/22/management-point-affinity-added-in-configmgr-2012-r2-cu3.aspx).  

Cada vez que un cliente necesita contactar con un punto de administración, consulta una lista de puntos de administración conocidos (denominada **lista de puntos de administración**) que se almacena localmente en WMI. El cliente crea una lista de puntos de administración inicial cuando se instala y la actualiza periódicamente con detalles sobre cada punto de administración en la jerarquía.  

Cuando el cliente no puede encontrar un punto de administración válido en la lista de puntos de administración, busca en los siguientes orígenes de ubicación del servicio (en el orden dispuesto) hasta que encuentra uno que pueda usar:  

1.  Punto de administración  
2.  Servicios de dominio de Active Directory  
3.  DNS  
4.  WINS  

Después de que un cliente ubique un punto de administración correctamente desde uno de esos orígenes y se comunique con él, descargará la lista actual de los puntos de administración que hay disponibles en la jerarquía y actualizará su lista local de puntos de administración. Esto es válido para los clientes que están unidos a un dominio y los que no, indistintamente.  

Por ejemplo, cuando un cliente de Configuration Manager que está en Internet se conecta a un punto de administración basado en Internet, el punto de administración envía a ese cliente una lista de puntos de administración basados en Internet disponibles en el sitio. De forma similar, los clientes que están unidos a un dominio o en grupos de trabajo también reciben la lista de puntos de administración que pueden usar.  
-   Un cliente que no esté configurado para Internet no recibirá puntos de administración con conexión a Internet.  
-   Los clientes de grupo de trabajo configurados para Internet se comunicarán únicamente con puntos de administración con conexión a Internet.  

##  <a name="a-namebkmkmplista-the-mp-list"></a><a name="BKMK_MPList"></a> La lista de puntos de administración  
La lista de puntos de administración es el origen de ubicación del servicio preferido de un cliente, puesto que es una lista de prioridades de los puntos de administración que el cliente identificó anteriormente. Cada cliente ordena esta lista en función de su ubicación de red cuando el cliente la actualiza y, luego, la almacena localmente en el cliente en WMI.  

### <a name="building-the-initial-mp-list"></a>Creación de la lista de puntos de administración inicial  
Durante la instalación del cliente, se emplean las siguientes reglas para generar la **lista de puntos de administración**inicial del cliente:  

-   La lista inicial contiene los puntos de administración especificados durante la instalación del cliente (usando las opciones **SMSMP**= o **/MP** ).  
-   El cliente consulta a Servicios de dominio de Active Directory (AD DS) para conocer los puntos de administración publicados. Para identificarse en AD DS, el punto de administración debe proceder del sitio asignado del cliente y tener la misma versión de producto que el cliente.  
-   Si no se ha especificado ningún punto de administración durante la instalación del cliente y el esquema de Active Directory no es extendido, el cliente consulta a DNS y WINS para conocer los puntos de administración publicados.  
-   Al generar la lista inicial, puede que la información sobre algunos puntos de administración en la jerarquía no sea conocida.  

### <a name="organizing-the-management-point-list"></a>Organización de la lista de puntos de administración  
Los clientes organizan su lista de puntos de administración mediante las siguientes clasificaciones:  

-   **Proxy**: un punto de administración proxy es un punto de administración en un sitio secundario.  
-   **Local**: cualquier punto de administración asociado a la ubicación de red actual del cliente, según definen los límites del sitio.  
    -   Cuando un cliente pertenece a más de un grupo de límites, la lista de puntos de administración local se determina a partir de la unión de todos los límites que incluyen la ubicación de red actual del cliente.  
    -   Normalmente, los puntos de administración **locales** son un subconjunto de puntos de administración **asignados** de un cliente, a menos que el cliente esté en una ubicación de red asociada a otro sitio con puntos de administración que mantienen sus grupos de límites.   


-   **Asignado**: cualquier punto de administración que sea un sistema de sitio del sitio asignado del cliente.  

     Puede usar puntos de administración preferidos. Los puntos de administración preferidos son los puntos de administración de un sitio asignado del cliente que están asociados con un grupo de límites que el cliente usa para buscar servidores de sistema de sitio.  

     Los puntos de administración en un sitio que no están asociados con un grupo de límites, o que no están en un grupo de límites asociado con la ubicación de red actual del cliente, no se consideran preferidos y se usarán cuando el cliente no pueda identificar un punto de administración preferido disponible.  

### <a name="selecting-a-management-point-to-use"></a>Selección de un punto de administración para usarlo  
En una comunicación típica, un cliente intenta usar un punto de administración de las clasificaciones en el siguiente orden, según cuál sea la ubicación de red del cliente:  

1.  Proxy  
2.  Local  
3.  asignados  

Sin embargo, el cliente siempre usa el punto de administración asignado para los mensajes de registro y para determinados mensajes de la directiva, aun cuando se envíen otras comunicaciones a un punto de administración proxy o local.  

Dentro de cada clasificación (proxy, local o asignado), los clientes intentan usar un punto de administración según las preferencias, en el orden siguiente:  

1.  Con capacidad para HTTPS en un bosque de confianza o local (cuando el cliente está configurado para la comunicación HTTPS)  
2.  Con capacidad para HTTPS pero no en un bosque de confianza o local (cuando el cliente está configurado para la comunicación HTTPS)  
3.  Con capacidad para HTTPS en un bosque de confianza o local  
4.  Con capacidad para HTTPS pero no en un bosque de confianza o local  

Desde el conjunto de puntos de administración ordenado por preferencias, los clientes intentan usar el primer punto de administración de la lista:  

-   Esta lista ordenada de puntos de administración es aleatoria y no se puede ordenar.  
-   El orden de la lista puede cambiar cada vez que el cliente actualice su lista de puntos de administración.  

Cuando un cliente no puede establecer contacto con el primer punto de administración, lo intenta con cada punto de administración sucesivo de su lista, y trata de usar cada punto de administración preferido de la clasificación antes de pasar a probar con los puntos de administración no preferidos. Si un cliente no se puede comunicar correctamente con un punto de administración en la clasificación, intenta ponerse en contacto con un punto de administración preferido de la siguiente clasificación, y así sucesivamente hasta que el cliente encuentra un punto de administración que pueda usar.  

Después de establecer la comunicación con un punto de administración, el cliente seguirá usándolo hasta que tenga lugar una de las siguientes situaciones:  

-   Transcurridas 25 horas, el cliente selecciona aleatoriamente un nuevo punto de administración que usar.  
-   Tras 5 intentos durante un período de 10 minutos, el cliente no puede comunicarse con el punto de administración, momento en el que selecciona un nuevo punto de administración que usar.  

##  <a name="a-namebkmkada-active-directory"></a><a name="bkmk_ad"></a> Active Directory  
Los clientes que están unidos a un dominio pueden usar Servicios de dominio de Active Directory (AD DS) para la ubicación del servicio. Para ello, es necesario que los sitios [publiquen datos en Active Directory](http://technet.microsoft.com/library/hh696543.aspx).  

Los clientes pueden usar Servicios de dominio de Active Directory para la ubicación del servicio cuando se cumplen todas estas condiciones:  

-   El [esquema de Active Directory se ha extendido](https://technet.microsoft.com/library/mt345589.aspx) para System Center 2012 Configuration Manager.  
-   El [bosque de Active Directory está configurado para publicación](http://technet.microsoft.com/library/hh696542.aspx)y los sitios de Configuration Manager están configurados para publicar.  
-   El equipo cliente forma parte de un dominio de Active Directory y puede tener acceso a un servidor de catálogo global.  

Si un cliente no puede encontrar un punto de administración para usarlo en la ubicación del servicio desde AD DS, lo intenta recurriendo a DNS. Los clientes que están unidos a un dominio pueden usar AD DS para la ubicación del servicio. Para ello, es necesario que los sitios [publiquen datos en Active Directory](http://technet.microsoft.com/library/hh696543.aspx).  

##  <a name="a-namebkmkdnsa-dns"></a><a name="bkmk_dns"></a> DNS  
Los clientes de la intranet pueden usar DNS para la ubicación del servicio. Esto requiere al menos un sitio en una jerarquía para publicar información sobre los puntos de administración en DNS.  

Considere la posibilidad de usar DNS para la ubicación del servicio cuando se cumpla alguna de las siguientes condiciones:
-   No se extiende el esquema de Active Directory Domain Services para admitir Configuration Manager.
-   Los clientes de la intranet se encuentran en un bosque que no está habilitado para la publicación de Configuration Manager.  
-   Hay clientes en equipos de grupo de trabajo que no están configurados para la administración de clientes de solo Internet (un cliente de grupo de trabajo configurado para Internet se comunicará únicamente con puntos de administración con conexión a Internet y no usará DNS para la ubicación del servicio).  
-   Puede [configurar clientes para que busquen puntos de administración desde DNS](http://technet.microsoft.com/library/gg682055).  

Cuando un sitio publica registros de ubicación del servicio de los puntos de administración en DNS:  

-   La publicación solo será factible en los puntos de administración que acepten conexiones de clientes desde la intranet.  
-   La publicación agrega un registro de recursos de ubicación del servicio (SRV RR) en la zona DNS del equipo del punto de administración. Debe haber una entrada de host correspondiente en DNS para ese equipo.  

Los clientes unidos a un dominio buscan de manera predeterminada en DNS para hallar los registros de punto de administración desde el dominio del cliente local. Puede configurar una propiedad del cliente que especifique un sufijo de dominio relativo a un dominio que tenga información de puntos de administración publicada en DNS.  

Para obtener más información sobre cómo configurar la propiedad del cliente del sufijo DNS, consulte [Configurar los equipos cliente para buscar los puntos de administración mediante el uso de la publicación en DNS en System Center Configuration Manager](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

Si un cliente no puede encontrar un punto de administración para usarlo para la ubicación del servicio desde DNS, intentará usar WINS.  

### <a name="publish-management-points-to-dns"></a>Publicar puntos de administración en DNS  
Para publicar puntos de administración en DNS, deben cumplirse las dos condiciones siguientes:  

-   Los servidores DNS admiten registros de recursos de ubicación de servicio mediante el uso de una versión de BIND que es al menos 8.1.2.  
-   Los FQDN de intranet especificados para los puntos de administración en Configuration Manager tienen entradas de host (por ejemplo, registros A) en DNS.  

> [!IMPORTANT]  
>  La publicación en DNS de Configuration Manager no es compatible con un espacio de nombres no contiguo. Si tiene un espacio de nombres discontinuo, puede publicar manualmente puntos de administración en DNS o puede usar uno de los otros métodos de ubicación de servicio alternativos que están documentados en esta sección.  

**Cuando los servidores DNS admiten actualizaciones automáticas**, puede configurar Configuration Manager para publicar de forma automática puntos de administración en la intranet en DNS, o bien puede publicar de forma manual estos registros en DNS. Cuando los puntos de administración se publican en DNS, el número de puerto y FQDN de la intranet se publican en el registro de ubicación de servicio (SRV). La publicación en DNS en un sitio se configura en las propiedades de componente de punto de administración del sitio en cuestión. Para obtener más información, consulte [Componentes de sitio para System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

**Cuando Zona DNS se establece en "Sólo seguras" para Actualizaciones dinámicas**, solo el primer punto de administración para publicar en DNS puede hacerlo correctamente con los permisos predeterminados.
- Puede agregar cada servidor que hospeda un punto de administración al grupo DnsAdmins para garantizar que aquellos puntos de administración tienen permisos para modificar sus registros.  
- Si solo un punto de administración puede publicar y modificar correctamente su registro DNS, siempre y cuando ese servidor de puntos de administración permanezca en buen estado, los clientes pueden obtener la lista completa de MP desde ese punto de administración y luego encontrar su punto de administración preferido.


**Cuando los servidores DNS no admiten actualizaciones automáticas, pero son compatibles con los registros de ubicación del servicio**, puede publicar manualmente los puntos de administración en DNS. Para ello, debe especificar manualmente el registro de recurso de ubicación de servicio (SRV RR) en DNS.  

Configuration Manager es compatible con RFC 2782 para registros de ubicación del servicio, que tiene el siguiente formato: *_Servicio._Protocolo.Nombre TTL Clase SRV Prioridad Peso Puerto Destino*  

Para publicar un punto de administración en Configuration Manager, especifique los valores siguientes:  

-   **_Servicio**: escriba **_mssms_mp***_&lt;código de sitio\>*, donde *&lt;código de sitio\>* es el código del sitio del punto de administración.  
-   **._Proto**: especifique **._tcp**.  
-   **.Nombre**: escriba el sufijo DNS del punto de administración, por ejemplo **contoso.com**.  
-   **TTL**: escriba **14400**, que es cuatro horas.  
-   **Clase**: especifique **IN** (de acuerdo con RFC 1035).  
-   **Prioridad**: Configuration Manager no usa este campo.
-   **Peso**: Configuration Manager no usa este campo.  
-   **Puerto**: escriba el número de puerto que el punto de administración usa, por ejemplo, **80** para HTTP y **443** para HTTPS.  

    > [!NOTE]  
    >  El puerto del registro SRV debe coincidir con el puerto de comunicación que el punto de administración usa. De forma predeterminada, es **80** para la comunicación HTTP y **443** para la comunicación HTTPS.  

-   **Destino**: escriba el FQDN de la intranet especificado para el sistema de sitio que está configurado con el rol de sitio de punto de administración.  

Si utiliza DNS de Windows Server, puede utilizar el siguiente procedimiento para especificar este registro de DNS para los puntos de administración de la intranet. Si utiliza una implementación distinta para DNS, utilice la información de esta sección acerca de los valores de campo y consulte la documentación de ese DNS para adaptar este procedimiento.  

##### <a name="to-configure-automatic-publishing"></a>Para configurar la publicación automática:  

1.  En la consola de Configuration Manager, expanda **Administración** > **Configuración del sitio** > **Sitios**.  

2.  Seleccione el sitio y, después, haga clic en **Configurar componentes de sitio**.  

3.  Seleccione **Punto de administración**.  

4.  Seleccione los puntos de administración que quiera publicar (esta selección es válida para la publicación tanto en AD DS como en DNS).  

5.  Active la casilla para publicar en DNS:  

    -   Este cuadro de diálogo permite seleccionar qué puntos de administración se van a publicar y publicar en DNS.  

    -   En este cuadro de diálogo no se configura la publicación en AD DS.  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>Para publicar manualmente puntos de administración en DNS en Windows Server  

1.  En la consola de Configuration Manager, especifique los FQDN de intranet de los sistemas de sitio.  

2.  En la consola de administración de DNS, seleccione la zona DNS para el equipo de punto de administración.  

3.  Compruebe que existe un registro de host (A o AAAA) para el FQDN de intranet del sistema de sitio. Si este registro no existe, créelo.  

4.  Con la opción **Otros registros nuevos** , haga clic en **Ubicación de servicio (SRV)** en el cuadro de diálogo **Tipo de registro del recurso** , haga clic en **Crear registro**, escriba la información siguiente y, a continuación, haga clic en **Listo**:  

    -   **Dominio**: si es necesario, escriba el sufijo DNS del punto de administración, por ejemplo **contoso.com**.  
    -   **Servicio**: escriba **_mssms_mp***_&lt;código de sitio\>*, donde *&lt;código de sitio\>* es el código del sitio del punto de administración.  
    -   **Protocolo**: escriba **_tcp**.  
    -   **Prioridad**: Configuration Manager no usa este campo.  
    -   **Peso**: Configuration Manager no usa este campo.  
    -   **Puerto**: escriba el número de puerto que el punto de administración usa, por ejemplo, **80** para HTTP y **443** para HTTPS.  

        > [!NOTE]  
        >  El puerto del registro SRV debe coincidir con el puerto de comunicación que el punto de administración usa. De forma predeterminada, es **80** para la comunicación HTTP y **443** para la comunicación HTTPS.  

    -   **Host que ofrece este servicio**: escriba el nombre de dominio completo de la intranet especificado para el sistema de sitio que está configurado con el rol de sitio de punto de administración.  

Repita estos pasos por cada punto de administración de la intranet que desee publicar en DNS.  

##  <a name="a-namebkmkwinsa-wins"></a><a name="bkmk_wins"></a> WINS  
Cuando se produce un error en otros mecanismos de ubicación de servicio, los clientes pueden buscar un punto de administración inicial mediante la comprobación de WINS.  

De forma predeterminada, un sitio primario publica en WINS el primer punto de administración en el sitio que está configurado para HTTP y el primer punto de administración configurado para HTTPS.  

Si no desea que los clientes encuentren un punto de administración HTTP en WINS, configure los clientes con la propiedad Client.msi de CCMSetup.exe **SMSDIRECTORYLOOKUP=NOWINS**.  



<!--HONumber=Nov16_HO1-->


