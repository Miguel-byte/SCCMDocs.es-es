---
title: Planificar la seguridad en System Center Configuration Manager
description: "Obtenga las recomendaciones de seguridad y otra información sobre seguridad en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
caps.latest.revision: 6
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f38d7275a39d16f9e6cf90334a46668fcc860bc1


---
# <a name="plan-for-security-in-system-center-configuration-manager"></a>Planificar la seguridad en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use la información de este tema para ayudarle a planear la seguridad en System Center Configuration Manager.  

   Para obtener información adicional sobre Cómo Configuration Manager usa los certificados y los controles criptográficos, consulte [Referencia técnica de controles criptográficos de System Center Configuration Manager](../../../protect/deploy-use/cryptographic-controls-technical-reference.md).  


##  <a name="a-namebkmkplanningforcertificatesa-planning-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a> Planeamiento de certificados (autofirmados y PKI)  
 Configuration Manager usa una combinación de certificados autofirmados y certificados de infraestructura de clave pública (PKI).  

 Por motivos de seguridad, se recomienda utilizar certificados PKI siempre que sea posible. Para obtener más información sobre los requisitos de certificados PKI, consulte [Requisitos de certificados PKI para System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md). Cuando Configuration Manager solicita los certificados PKI, como por ejemplo durante la inscripción de dispositivos móviles y el aprovisionamiento de AMT, debe usar Servicios de dominio de Active Directory y una entidad de certificación empresarial. En todos los demás casos, los certificados PKI se deben implementar y administrar independientemente de Configuration Manager.  

 Los certificados PKI también se necesitan cuando los equipos cliente se conectan a sistemas de sitio basados en Internet, y se recomienda su uso cuando los clientes se conectan a sistemas de sitio que ejecutan Internet Information Services (IIS). Para obtener más información sobre la comunicación de cliente, consulte [Configurar puertos de comunicación de cliente en System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

 Cuando utiliza PKI, también puede utilizar IPsec para proteger la comunicación de servidor a servidor entre sistemas de sitio en un sitio y entre sitios, y para cualquier otro escenario cuando transfiere datos entre equipos. Debe configurar e implementar IPsec independientemente de Configuration Manager.  

 Configuration Manager puede generar automáticamente certificados autofirmados cuando no hay certificados PKI disponibles, y algunos certificados de Configuration Manager siempre son autofirmados. En la mayoría de los casos, Configuration Manager administra automáticamente los certificados autofirmados y no es necesario tomar medidas adicionales. El certificado de firma de servidor de sitio constituye una posible excepción. El certificado de firma de servidor de sitio siempre es autofirmado, y garantiza que las directivas de cliente que los clientes descargan del punto de administración se enviaron desde el servidor de sitio y no fueron alteradas.  

### <a name="planning-for-the-site-server-signing-certificate-self-signed"></a>Planificación del certificado de firma de servidor de sitio (autofirmado)  
 Los clientes pueden obtener de forma segura una copia del certificado de firma de servidor de sitio a través de Servicios de dominio de Active Directory y de la instalación de inserción de cliente. Si los clientes no pueden obtener una copia del certificado de firma de servidor de sitio mediante uno de estos mecanismos, por motivos de seguridad se recomienda instalar una copia del certificado de firma de servidor de sitio al instalar el cliente. Esto resulta de especial importancia si la primera comunicación del cliente con el sitio se realiza desde Internet, ya que el punto de administración está conectado a una red que no es de confianza y, por tanto, es vulnerable a los ataques. Si no se realiza este paso adicional, los clientes descargan automáticamente una copia del certificado de firma de servidor de sitio desde el punto de administración.  

 Los posibles escenarios de clientes que no pueden obtener de forma segura una copia del certificado de firma de servidor de sitio son los siguiente:  

-   No se instala el cliente mediante la inserción de cliente, y se cumple cualquiera de las siguientes condiciones:  

    -   El esquema de Active Directory no se extiende para Configuration Manager.  

    -   El sitio del cliente no está publicado en Servicios de dominio de Active Directory.  

    -   El cliente pertenece a un grupo de trabajo o un bosque que no es de confianza.  

-   El cliente se instala cuando está en Internet.  

Utilice el siguiente procedimiento para instalar clientes junto con una copia del certificado de firma de servidor de sitio.  

##### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Para instalar clientes con una copia del certificado de firma de servidor de sitio  

1.  Busque el certificado de firma de servidor de sitio en el servidor de sitio primario del cliente. El certificado se almacena en el almacén de certificados **SMS** ; su nombre de sujeto es **Servidor del sitio** y su nombre descriptivo es **Certificado de firma de servidor de sitio**.  

2.  Exporte el certificado sin la clave privada, almacene el archivo de forma segura y acceda al mismo sólo desde un canal seguro (por ejemplo, mediante la firma de SMB o IPsec).  

3.  Instale el cliente mediante el uso de la propiedad de Client.msi **SMSSIGNCERT=***&lt;ruta completa y nombre de archivo\>* con CCMSetup.exe.  

###  <a name="a-namebkmkplanningforcrlsa-planning-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a> Planeamiento de la revocación de certificados PKI  
Cuando use certificados PKI con Configuration Manager, planifique si y cómo los clientes y servidores usarán una lista de revocación de certificados (CRL) para comprobar el certificado en el equipo que se conecta. La lista de revocación de certificados (CRL) es un archivo creado y firmado por una entidad de certificación (CA) que contiene una lista de certificados emitidos y revocados. Los certificados pueden ser revocados por un administrador de CA, por ejemplo, si se sabe o se sospecha que un certificado emitido está comprometido.  

> [!IMPORTANT]  
>  Como la ubicación de la CRL se agrega al certificado cuando lo emite la CA, asegúrese de tener en cuenta la CRL antes de implementar los certificados PKI que va a usar Configuration Manager.  

De forma predeterminada, IIS comprueba siempre la CRL de los certificados de cliente, y no se puede cambiar esta configuración en Configuration Manager. De forma predeterminada, los clientes de Configuration Manager comprueban siempre la CRL de los sistemas de sitio; pero esta opción se puede deshabilitar si se especifica una propiedad de sitio y una propiedad de CCMSetup. Si administra equipos basados en Intel AMT fuera de banda, puede habilitar también la comprobación de CRL para el punto de servicio fuera de banda y para equipos que ejecutan la consola de administración fuera de banda.  

Si los equipos utilizan la comprobación de revocación de certificados pero no pueden encontrar la CRL, se comportan como si todos los certificados de la cadena de certificación estuvieran revocados, ya que no se puede comprobar su ausencia de la lista. En este escenario, se produce un error en todas las conexiones que requieren certificados y utilizan una CRL.  

La comprobación de la CRL cada vez que se usa un certificado proporciona una mayor seguridad contra certificados que han sido revocados pero incorpora un retraso en la conexión e implica un procesamiento adicional en el cliente. Es más probable que se requiera esta comprobación de seguridad adicional cuando los clientes están en Internet o en una red que no es de confianza.  

Consulte con los administradores de PKI antes de decidir si los clientes de Configuration Manager deben comprobar la CRL y, después, considere la posibilidad de mantener esta opción habilitada en Configuration Manager cuando se cumplen las condiciones siguientes:  

-   La infraestructura PKI es compatible con una CRL, y está publicada donde todos los clientes de Configuration Manager puedan encontrarla. Recuerde que podrían estar incluidos los clientes de Internet, si utiliza la administración de cliente basada en Internet, así como los clientes de bosques que no son de confianza.  

-   La necesidad de comprobar la CRL para cada conexión a un sistema de sitio configurado para el uso de un certificado PKI tiene mayor importancia que la necesidad de conexiones más rápidas y un procesamiento eficaz en el cliente, y tiene asimismo mayor importancia que el riesgo de que los clientes no se puedan conectar a los servidores si no pueden encontrar la CRL.  

###  <a name="a-namebkmkplanningforrootcasa-planning-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a> Planeamiento de los certificados raíz de confianza PKI y la lista de emisores de certificados  
Si los sistemas de sitio de IIS utilizan certificados de cliente PKI para la autenticación de cliente a través de HTTP o para la autenticación de cliente y el cifrado a través de HTTPS, podría ser necesario importar los certificados CA raíz como una propiedad de sitio. Los dos escenarios son los siguientes:  

-   Se implementan los sistemas operativos mediante el uso de Configuration Manager y los puntos de administración solo aceptan conexiones de cliente HTTPS.  

-   Se utilizan certificados de cliente PKI que no están vinculados a un certificado de entidad de certificación (CA) raíz que es confiable para los puntos de administración.  

    > [!NOTE]  
    >  Cuando se emiten certificados PKI de cliente de la misma jerarquía de CA que emite los certificados de servidor utilizados para los puntos de administración, no es necesario especificar este certificado de CA raíz. Pero si usa varias jerarquías de CA y no está seguro de si tienen confianza mutua, importe la CA raíz de la jerarquía de la CA de los clientes.  

Si debe importar los certificados de CA raíz para Configuration Manager, expórtelos desde la CA emisora o desde el equipo cliente. Si exporta el certificado desde la CA emisora que también es la CA raíz, asegúrese de que no se exporta la clave privada. Almacene el archivo de certificado exportado en una ubicación segura para evitar que sea alterado. Debe poder acceder al archivo al configurar el sitio, de modo que si accede al archivo a través de la red, asegúrese de que la comunicación está protegida contra alteraciones mediante la firma de SMB o IPsec.  

Si cualquiera de los certificados de CA raíz que importa se renuevan, debe importar los certificados renovados.  

Estos certificados de CA raíz importados y el certificado de CA raíz de cada punto de administración forman la lista de emisores de certificados que los equipos de Configuration Manager usan de las siguientes maneras:  

-   Cuando los clientes se conectan a puntos de administración, el punto de administración comprueba que el certificado de cliente esté vinculado a un certificado raíz de confianza de la lista de emisores de certificados del sitio. Si no es así, se rechaza el certificado y se produce un error en la conexión de PKI.  

-   Cuando los clientes seleccionan un certificado PKI, si tienen una lista de emisores de certificados, seleccionan un certificado vinculado a un certificado raíz de confianza de la lista de emisores de certificados. Si no hay ninguna coincidencia, el cliente no selecciona un certificado PKI. Para más información sobre el proceso de certificado de cliente, consulte la sección [Planning for PKI client certificate selection](#BKMK_PlanningForClientCertificateSelection) en este tema.  

Independientemente de la configuración del sitio, también podría tener que importar un certificado de CA raíz al inscribir dispositivos móviles o equipos Mac y al realizar el aprovisionamiento de equipos basados en Intel AMT para redes inalámbricas.  

###  <a name="a-namebkmkplanningforclientcertificateselectiona-planning-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a> Planeamiento de la selección de certificados de cliente PKI  
 Si los sistemas de sitio de IIS usan certificados de cliente PKI para la autenticación de cliente a través de HTTP o para la autenticación de cliente y el cifrado a través de HTTPS, planifique cómo seleccionarán los clientes basados en Windows el certificado que se debe usar para Configuration Manager.  

> [!NOTE]  
>  No todos los dispositivos admiten un método de selección de certificado y en su lugar, seleccionan automáticamente el primer certificado que cumple los requisitos del certificado. Por ejemplo, los clientes de equipos Mac y dispositivos móviles no admiten un método de selección de certificado.  

En muchos casos, la configuración y el comportamiento predeterminados serán suficientes. El cliente de Configuration Manager en equipos basados en Windows filtra varios certificados mediante los siguientes criterios:  

1.  La lista de emisores de certificados: el certificado está vinculado a una CA raíz que es de confianza para el punto de administración.  

2.  El certificado se encuentra en el almacén de certificados predeterminado **Personal**.  

3.  El certificado es válido, no se revocó y no expiró. La comprobación de validez incluye comprobar que la clave privada es accesible y que el certificado no se creó con la versión 3 de la plantilla de certificado, que no es compatible con Configuration Manager.  

4.  El certificado tiene capacidad de autenticación de cliente, o se emitió con el nombre del equipo.  

5.  El certificado tiene el periodo de validez más largo.  

Los clientes se pueden configurar para utilizar la lista de emisores de certificados mediante los siguientes mecanismos:  

-   Se publica como información de sitio de Configuration Manager en Servicios de dominio de Active Directory.  

-   Los clientes se instalan mediante la inserción de cliente.  

-   Los clientes lo descargan desde el punto de administración después de ser asignados correctamente a su sitio.  

-   Se especifica durante la instalación del cliente, como una propiedad CCMCERTISSUERS de CCMSetup Client.msi.  

Si los clientes no tienen la lista de emisores de certificados cuando se instalan por primera vez y todavía no están asignados al sitio, omiten esta comprobación. Cuando tienen la lista de emisores de certificados pero no tienen un certificado PKI vinculado a un certificado raíz de confianza de la lista de emisores de certificados, se produce un error en la selección de certificados y los clientes no continúan con los demás criterios de selección de certificados.  

En la mayoría de los casos, el cliente de Configuration Manager identifica correctamente un certificado PKI exclusivo y adecuado para usarlo. Sin embargo, si no es así, en lugar de seleccionar el certificado en función de la capacidad de autenticación de cliente, puede configurar dos métodos de selección alternativos:  

-   Una coincidencia de cadena parcial del nombre de sujeto del certificado de cliente. Esta coincidencia, que no distingue mayúsculas de minúsculas, resulta adecuada si se usa el nombre de dominio completo (FQDN) de un equipo en el campo del firmante y se desea basar la selección de certificados en el sufijo del dominio, por ejemplo **contoso.com**. Sin embargo, se puede utilizar este método de selección para identificar cualquier cadena de caracteres secuenciales del nombre de sujeto del certificado que permita distinguir este último de los demás certificados del almacén de certificados de cliente.  

    > [!NOTE]  
    >  No se puede utilizar la coincidencia de cadena parcial con el nombre alternativo del sujeto (SAN) como configuración de sitio. Aunque se puede especificar una coincidencia de cadena parcial para el SAN mediante el uso de CCMSetup, las propiedades de sitio la sobrescribirán en los siguientes escenarios:  
    >   
    >  -   Los clientes recuperan información del sitio que está publicada en Servicios de dominio de Active Directory.  
    > -   Los clientes se instalan mediante la instalación de inserción de cliente.  
    >   
    >  Utilice una coincidencia de cadena parcial del SAN solo cuando instala los clientes manualmente, y cuando estos no recuperan información del sitio desde Servicios de dominio de Active Directory. Por ejemplo, estas condiciones se aplican a los clientes solo de Internet.  

-   Una coincidencia de los valores de atributo del nombre de sujeto del certificado de cliente o de los valores de atributo del nombre alternativo del sujeto (SAN). Esta coincidencia, que distingue mayúsculas de minúsculas, resulta adecuada si se utiliza un nombre distintivo X500 u OID (identificadores de objetos) equivalentes conforme a RFC 3280 y se desea basar la selección de certificados en los valores de atributo. Puede especificar sólo los atributos, con sus valores, que necesita para identificar de manera exclusiva o validar el certificado y distinguirlo de los demás certificados del almacén de certificados de cliente.  

En la siguiente tabla aparecen los valores de atributo que Configuration Manager admite para los criterios de selección de certificados de cliente.  

|Atributo OID|Atributo de nombre distintivo|Definición de atributo|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Componente de dominio|  
|1.2.840.113549.1.9.1|E o E-mail|Dirección de correo electrónico|  
|2.5.4.3|CN|Nombre común|  
|2.5.4.4|SN|Nombre de sujeto|  
|2.5.4.5|SERIALNUMBER|Número de serie|  
|2.5.4.6|C|Código de país|  
|2.5.4.7|L|Localidad|  
|2.5.4.8|S o ST|Nombre de estado o provincia|  
|2.5.4.9|STREET|Dirección|  
|2.5.4.10|O|Nombre de la organización|  
|2.5.4.11|OU|Unidad organizativa|  
|2.5.4.12|T o Title|Título|  
|2.5.4.42|G o GN o GivenName|Nombre dado|  
|2.5.4.43|I o Initials|Iniciales|  
|2.5.29.17|(ningún valor)|Nombre alternativo del sujeto|  

Si se encuentra más de un certificado adecuado después de aplicar los criterios de selección, se puede invalidar la configuración predeterminada que establece la selección del certificado que tenga el periodo de validez más largo y en su lugar especificar que no se debe seleccionar ningún certificado. En este escenario, el cliente no podrá comunicarse con los sistemas de sitio de IIS mediante un certificado PKI. El cliente envía un mensaje de error al punto de estado de reserva asignado para alertar acerca del error de selección de certificados de manera que se puedan modificar o refinar los criterios de selección de certificados. El comportamiento del cliente luego dependerá de si la conexión con errores era HTTPS o HTTP:  

-   Si la conexión con errores era a través de HTTPS: el cliente intenta establecer una conexión a través de HTTP y usa el certificado autofirmado del cliente.  

-   Si la conexión con errores era a través de HTTP: el cliente intenta establecer otra conexión a través de HTTP con el certificado autofirmado del cliente.  

Para facilitar la identificación de un certificado de cliente PKI exclusivo, también puede especificar un almacén personalizado distinto al almacén predeterminado **Personal** del almacén del **Equipo** . Pero debe crear este almacén independientemente de Configuration Manager y debe poder implementar certificados en este almacén personalizado así como renovarlos antes de que expire el periodo de validez.  

Para obtener más información sobre cómo configurar las opciones de los certificados de cliente, consulte la sección [Configurar certificados PKI de cliente](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) en el tema [Configurar la seguridad en System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

###  <a name="a-namebkmkplanningforpkitransitiona-planning-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a> Planeamiento de una estrategia de transición para certificados PKI y administración de cliente basada en Internet  
Las opciones de configuración flexible de Configuration Manager permiten llevar a cabo una transición gradual en los clientes y el sitio hacia el uso de los certificados PKI para proteger los extremos de cliente. Los certificados PKI proporcionan mayor seguridad y permiten administrar los clientes cuando están en Internet.  

Debido al número de opciones de configuración de Configuration Manager, no existe una única manera de llevar a cabo la transición de un sitio para que todos los clientes usen conexiones HTTPS. Sin embargo, puede seguir estos pasos como guía:  

1.  Instale el sitio de Configuration Manager y configúrelo para que los sistemas de sitio acepten conexiones de cliente a través de HTTPS y HTTP.  

2.  Configure la pestaña **Comunicación de equipo cliente** de las propiedades del sitio de modo que la **Configuración de sistema de sitio** sea **HTTP o HTTPS**, y active la casilla **Usar un certificado de cliente PKI (capacidad de autenticación de cliente) cuando esté disponible** . Configure las demás opciones de esta pestaña que desee. Para obtener más información, consulte la sección [Configurar certificados PKI de cliente](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) del tema [Configurar la seguridad en System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

3.  Lleve a cabo una implementación de PKI para certificados de cliente. Para ver una implementación de ejemplo, consulte la sección *Implementación del certificado de cliente para equipos Windows* en el tema [Ejemplo paso a paso de implementación de los certificados PKI para Configuration Manager: Entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

4.  Instale los clientes mediante el método de instalación de inserción de cliente. Para obtener más información, consulte la sección [Instalación de clientes de Configuration Manager mediante la inserción de cliente](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush) en el tema [How to deploy clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md) (Implementar clientes en equipos Windows en System Center Configuration Manager).  

5.  Supervise la implementación y el estado de los clientes mediante los informes y la información de la consola de Configuration Manager.  

6.  Para realizar el seguimiento del número de clientes que utilizan un certificado PKI de cliente, consulte la columna **Certificado de cliente** del área de trabajo **Activos y compatibilidad** , nodo **Dispositivos** .  

     También puede implementar la herramienta de evaluación de preparación de HTTPS (**cmHttpsReadiness.exe**) en los equipos y usar los informes para ver cuántos equipos pueden utilizar un certificado PKI de cliente con Configuration Manager.  

    > [!NOTE]  
    >  Cuando el cliente de Configuration Manager se instala en equipos cliente, la herramienta **cmHttpsReadiness.exe** se instala en la carpeta *%windir%***\CCM**. Cuando ejecuta esta herramienta en los clientes, puede especificar las siguientes opciones:  
    >   
    >  -   /Store:&lt;nombre\>  
    > -   /Issuers:&lt;lista\>  
    > -   /Criteria:&lt;criterios\>  
    > -   /SelectFirstCert  
    >   
    >  Estas opciones se asignan a las propiedades de Client.msi **CCMCERTSTORE**, **CCMCERTISSUERS**, **CCMCERTSEL**y **CCMFIRSTCERT** , respectivamente. Para más información sobre estas opciones, consulte [Acerca de las propiedades de instalación de clientes en System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

7.  Cuando esté seguro de que un número suficiente de los clientes está utilizando correctamente su certificado PKI de cliente para la autenticación a través de HTTP, haga lo siguiente:  

    1.  Implemente un certificado de servidor web PKI en un servidor miembro que vaya a ejecutar un punto de administración adicional para el sitio, y configure ese certificado en IIS. Para obtener más información, consulte la sección *Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS* del tema [Ejemplo paso a paso de implementación de los certificados PKI para Configuration Manager: Entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

    2.  Instale el rol de punto de administración en este servidor y configure la opción **Conexiones de cliente** de las propiedades del punto de administración para **HTTPS**.  

8.  Compruebe que los clientes que tienen un certificado PKI utilizan el nuevo punto de administración mediante HTTPS. Puede utilizar el registro de IIS o los contadores de rendimiento para comprobarlo.  

9. Vuelva a configurar otros roles de sistema de sitio para utilizar conexiones de cliente HTTPS. Si desea administrar clientes en Internet, asegúrese de que los sistemas de sitio tienen un FQDN de Internet y configure puntos de administración y puntos de distribución individuales para que acepten conexiones de cliente de Internet.  

    > [!IMPORTANT]  
    >  Antes de configurar los roles de sistema de sitio para que acepten conexiones de Internet, revise la información de planeación y los requisitos previos de la administración de cliente basada en Internet. Para obtener más información, vea [Communications between endpoints in System Center Configuration Manager (Comunicaciones entre puntos de conexión en System Center Configuration Manager)](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

10. Amplíe la implementación de certificados PKI a clientes y sistemas de sitio que ejecutan IIS, y configure los roles de sistema de sitio para las conexiones de cliente HTTPS y las conexiones de Internet, según sea necesario.  

11. Para obtener la máxima seguridad: cuando esté seguro de que todos los clientes usan un certificado PKI de cliente para la autenticación y el cifrado, cambie las propiedades del sitio para que se use HTTPS solamente.  

 Si sigue este plan para introducir gradualmente los certificados PKI, primero para la autenticación solo a través de HTTP y luego para la autenticación y el cifrado a través de HTTPS, se reducirá el riesgo de que los clientes dejen de estar administrados. Además, se beneficiará de la máxima seguridad que Configuration Manager admite.  

##  <a name="a-namebkmkplanningforrtka-planning-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a> Planeamiento de la clave raíz confiable  
La clave raíz confiable de Configuration Manager permite que los clientes de Configuration Manager comprueben que los sistemas de sitio pertenecen a su jerarquía. Cada servidor de sitio genera una clave de intercambio de sitio para comunicarse con otros sitios. La clave de intercambio de sitio del sitio de nivel superior de la jerarquía se denomina clave raíz confiable.  

La función de la clave raíz confiable en Configuration Manager es similar a la de un certificado raíz en una infraestructura de clave pública, ya que cualquier elemento firmado por la clave privada de la clave raíz confiable se considerará confiable en los niveles inferiores de la jerarquía. Por ejemplo, al firmar el certificado de punto de administración con la clave privada del par de claves raíz confiables, y al poner a disposición de los clientes una copia de la clave pública del par de claves raíz confiables, los clientes pueden distinguir entre los puntos de administración que están en su jerarquía y los puntos de administración que no están en su jerarquía. Los clientes utilizan WMI para almacenar una copia de la clave raíz confiable en el espacio de nombres **root\ccm\locationservices**.  

Los clientes pueden recuperar automáticamente la copia pública de la clave raíz confiable mediante dos mecanismos:  

-   El esquema de Active Directory se extiende para Configuration Manager, el sitio está publicado en Servicios de dominio de Active Directory y los clientes pueden recuperar la información del sitio desde un servidor de catálogo global.  

-   Los clientes se instalan mediante la inserción de cliente.  

Si los clientes no pueden recuperar la clave raíz confiable mediante uno de estos mecanismos, confiarán en la clave raíz confiable que proporcione el primer punto de administración con el que se comuniquen En este escenario, un cliente podría ser dirigido erróneamente al punto de administración de un atacante, donde recibiría una directiva del punto de administración no autorizado. Tal cosa, que sería obra de un atacante sofisticado, podría suceder solo en un plazo de tiempo limitado antes de que el cliente recupere la clave raíz confiable de un punto de administración válido. Sin embargo, para reducir el riesgo de que un atacante dirija erróneamente los clientes a un punto de administración no autorizado, puede aprovisionar los clientes previamente con la clave raíz confiable.  

Use los siguientes procedimientos para aprovisionar previamente un cliente de Configuration Manager y comprobar su clave raíz confiable:  

-   Aprovisione previamente un cliente con la clave raíz confiable mediante un archivo.  

-   Aprovisione previamente un cliente con la clave raíz confiable sin utilizar un archivo.  

-   Compruebe la clave raíz confiable de un cliente.  

> [!NOTE]  
>  No es necesario aprovisionar previamente los clientes con la clave raíz confiable si la pueden obtener en Servicios de dominio de Active Directory o se instalan mediante la instalación de inserción de cliente. Asimismo, no es necesario aprovisionar previamente los clientes cuando utilizan la comunicación HTTPS con los puntos de administración, ya que la confianza se establece mediante los certificados PKI.  

Puede quitar la clave raíz confiable de un cliente mediante la propiedad de Client.msi **RESETKEYINFORMATION = TRUE** con CCMSetup.exe Para reemplazar la clave raíz confiable, vuelva a instalar el cliente junto con la nueva clave raíz confiable, por ejemplo, mediante la inserción de cliente, o mediante la propiedad de Client.msi **SMSPublicRootKey** con CCMSetup.exe.  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a>Para aprovisionar previamente un cliente con la clave raíz confiable mediante un archivo  

1.  En un editor de texto, abra el archivo *&lt;Directorio de Configuration Manager\>***\bin\mobileclient.tcf**.  

2.  Busque la entrada **SMSPublicRootKey=**, copie la clave de esa línea y cierre el archivo sin realizar ningún cambio.  

3.  Cree un nuevo archivo de texto y pegue la información de la clave copiada del archivo mobileclient.tcf.  

4.  Guarde el archivo y colóquelo en un lugar donde todos los equipos tengan acceso al mismo y donde esté protegido para evitar alteraciones.  

5.  Instale el cliente mediante cualquier método de instalación que acepte las propiedades de Client.msi, y especifique la propiedad de Client.msi **SMSROOTKEYPATH=***&lt;ruta completa y nombre de archivo\>*.  

    > [!IMPORTANT]  
    >  Cuando especifique la clave raíz confiable para incrementar la seguridad durante la instalación de clientes, también debe especificar el código de sitio mediante la propiedad de Client.msi **SMSSITECODE=&lt;código de sitio\>**.  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a>Para aprovisionar previamente un cliente con la clave raíz confiable sin utilizar un archivo  

1.  En un editor de texto, abra el archivo *&lt;Directorio de Configuration Manager\>***\bin\mobileclient.tcf**.  

2.  Busque la entrada SMSPublicRootKey=, anote la clave de esa línea o cópiela en el Portapapeles y, a continuación, cierre el archivo sin realizar ningún cambio.  

3.  Instale el cliente mediante cualquier método de instalación que acepte las propiedades de Client.msi, y especifique la propiedad de Client.msi **SMSPublicRootKey=***&lt;clave\>*, donde *&lt;clave\>* es la cadena copiada de mobileclient.tcf.  

    > [!IMPORTANT]  
    >  Cuando especifique la clave raíz confiable para incrementar la seguridad durante la instalación de clientes, también debe especificar el código de sitio mediante la propiedad de Client.msi **SMSSITECODE=&lt;código de sitio\>**.  

#### <a name="to-verify-the-trusted-root-key-on-a-client"></a>Para comprobar la clave raíz confiable de un cliente  

1.  En el menú **Inicio** , haga clic en **Ejecutar**y, a continuación, escriba **Wbemtest**.  

2.  En el cuadro de diálogo **Herramienta de comprobación del instrumental de administración de Windows** , haga clic en **Conectar**.  

3.  En el cuadro de diálogo **Conectar** , en la casilla **Espacio de nombres** , escriba **root\ccm\locationservices**y, a continuación, haga clic en **Conectar**.  

4.  En el cuadro de diálogo **Herramienta de comprobación del instrumental de administración de Windows** , en la sección **IWbemServices** , haga clic en **Clases enumeradoras**.  

5.  En el cuadro de diálogo **Información de la superclase** , seleccione **Recurrente**y, a continuación, haga clic en **Aceptar**.  

6.  En la ventana **Resultado de la consulta** , desplácese hasta el final de la lista y, a continuación, haga doble clic en **TrustedRootKey ()**.  

7.  En el cuadro de diálogo **Editor de objetos de TrustedRootKey** , haga clic en **Instancias**.  

8.  En la nueva ventana **Resultado de la consulta** donde se muestran las instancias de **TrustedRootKey**, haga doble clic en **TrustedRootKey=@**  

9. En el cuadro de diálogo **Editor de objetos de TrustedRootKey=@**, en la sección **Propiedades**, desplácese hacia abajo hasta **TrustedRootKey CIM_STRING**. La cadena de la columna de la derecha es la clave raíz confiable. Compruebe que coincide con el valor de **SMSPublicRootKey** del archivo *&lt;directorio de Configuration Manager\>***\bin\mobileclient.tcf**.  

##  <a name="a-namebkmkplanningforsigningencryptiona-planning-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a> Planeamiento de la firma y el cifrado  
 Cuando se utilizan certificados PKI para todas las comunicaciones de cliente, no es necesario planear la firma y el cifrado para proteger la comunicación de datos de cliente. Sin embargo, si configura sistemas de sitio que ejecutan IIS para permitir las conexiones de cliente HTTP, debe decidir cómo proteger la comunicación de cliente del sitio.  

 Para proteger los datos que los clientes envían a los puntos de administración, puede requerir la firma de los datos. Además, puede requerir que todos los datos firmados de los clientes que utilizan HTTP se firmen mediante el algoritmo SHA-256. Aunque se trata de una configuración más segura, no habilite esta opción a menos que todos los clientes admitan SHA-256. Muchos sistemas operativos admiten de forma nativa SHA-256, pero los sistemas operativos anteriores pueden necesitar una actualización o revisión. Por ejemplo, los equipos que ejecutan Windows Server 2003 SP2 deben instalar una revisión a la que se hace referencia en el [artículo de Knowledge Base 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666).  

 La firma permite proteger los datos contra la manipulación, y el cifrado permite proteger los datos contra la divulgación de información. Puede habilitar el cifrado 3DES para los mensajes de estado y datos de inventario que los clientes envían a los puntos de administración del sitio. No es necesario que instale actualizaciones en los clientes para admitir esta opción, pero tenga en cuenta el uso adicional de CPU que será necesario en los clientes y en el punto de administración para cifrar y descifrar datos.  

 Para obtener más información sobre cómo configurar las opciones de firma y cifrado, consulte la sección [Configurar la firma y el cifrado](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption) en el tema [Configurar la seguridad en System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

##  <a name="a-namebkmkplanningforrbaa-planning-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a> Planeamiento de la administración basada en roles  
 Para obtener esta información, consulte [Fundamentals of role-based administration for System Center Configuration Manager (Aspectos básicos de la administración basada en roles para System Center Configuration Manager)](../../../core/understand/fundamentals-of-role-based-administration.md).  



<!--HONumber=Nov16_HO1-->


