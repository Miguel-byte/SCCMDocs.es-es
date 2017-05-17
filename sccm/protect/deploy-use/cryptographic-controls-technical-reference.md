---
title: "Referencia técnica de controles criptográficos | Microsoft Docs"
description: "Obtenga información sobre la manera en que la firma y el cifrado pueden proteger contra ataques para leer datos de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c63dcc5-a1bd-4037-959a-2e6ba0fd1b2c
caps.latest.revision: 6
author: arob98
ms.author: angrobe
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 0f76ed3dd74a80d9e22cfa743e5aa484f6cd7d97
ms.contentlocale: es-es
ms.lasthandoff: 12/16/2016


---
# <a name="cryptographic-controls-technical-reference"></a>Referencia técnica de controles criptográficos

*Se aplica a: System Center Configuration Manager (rama actual)*


System Center Configuration Manager usa la firma y el cifrado para ayudar a proteger la administración de los dispositivos en la jerarquía de Configuration Manager. Con la firma, si los datos se han modificado en el tránsito, se descartan. El cifrado, mediante un analizador de protocolos de red, ayuda a impedir que un atacante pueda leer los datos.  

 El algoritmo hash primario que Configuration Manager usa para firmar es SHA-256. Si dos sitios de Configuration Manager se comunican entre sí, firman sus comunicaciones mediante SHA-256. El algoritmo primario de cifrado que se implementa en Configuration Manager es 3DES. Se usa para almacenar datos en la base de datos de Configuration Manager y para la comunicación HTTP de cliente. Si usa comunicación de cliente a través de HTTPS, puede configurar la infraestructura de clave pública (PKI) para que use certificados RSA con los algoritmos hash y longitudes de clave máximos documentados en [PKI certificate requirements for System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md) (Requisitos de certificados PKI para System Center Configuration Manager).  

 Para la mayoría de operaciones de cifrado de sistemas operativos basados en Windows, Configuration Manager usa los algoritmos SHA-2, 3DES y AES, y RSA en la biblioteca CryptoAPI de Windows rsaenh.dll.  

> [!IMPORTANT]  
>  Consulte la información sobre los cambios recomendados en respuesta a las vulnerabilidades SSL en [About SSL Vulnerabilities](#about-ssl-vulnerabilities) (Acerca de las vulnerabilidades SSL).  

##  <a name="cryptographic-controls-for-configuration-manager-operations"></a>Controles criptográficos para operaciones de Configuration Manager  
 La información de Configuration Manager se puede firmar y cifrar, independientemente de si se usan certificados PKI con Configuration Manager.  

### <a name="policy-signing-and-encryption"></a>Firma y cifrado de directiva  
 Las asignaciones de directiva de cliente están siempre firmadas por el certificado de firma de servidor de sitio autofirmado para impedir que un punto de administración comprometido envíe directivas alteradas. Esto es importante si usa administración de cliente basada en Internet, ya que este entorno requiere que un punto de administración esté expuesto a la comunicación de Internet.  

 La directiva se cifra con 3DES cuando contiene información confidencial. La directiva que contiene información confidencial se envía a clientes autorizados únicamente. La directiva que no tiene información confidencial no se cifra.  

 Cuando la directiva se almacena en los clientes, se cifra con la interfaz de programación de aplicaciones de protección de datos (DPAPI).  

### <a name="policy-hashing"></a>Hash de la directiva  
 Cuando los clientes de Configuration Manager solicitan una directiva, primero obtienen una asignación de directiva para que sepan qué directivas les son aplicables y, después, solicitan solo estos cuerpos de directiva. Cada asignación de directiva contiene el hash calculado para el cuerpo de directiva correspondiente. El cliente recupera los cuerpos de directiva aplicables y, a continuación, calcula el hash en relación a dicho cuerpo. Si el hash del cuerpo de directiva descargado no coincide con el hash de la asignación de directiva, el cliente descarta el cuerpo de directiva.  

 El algoritmo hash para la directiva es SHA-1 y SHA-256.  

### <a name="content-hashing"></a>Hash de contenido  
 El servicio de administrador de distribución del servidor del sitio aplica el hash a los archivos de contenido de todos los paquetes. El proveedor de directivas incluye el hash en la directiva de distribución de software. Cuando descarga el contenido, el cliente de Configuration Manager regenera el hash localmente y lo compara con el suministrado en la directiva. Si sus valores coinciden, significa que el contenido no se modificó, y el cliente lo instala. La modificación de un solo byte del contenido hará que los valores hash no coincidan y, por lo tanto, no se instale el software. Esta comprobación permite garantizar que sólo el software correcto se instala porque su contenido sólo se valida si coincide con el de la directiva.  

 El algoritmo hash predeterminado para el contenido es SHA-256. Para cambiar este valor predeterminado, consulte la documentación del kit de desarrollo de software (SDK) de Configuration Manager.  

 No todos los dispositivos admiten la aplicación del hash al contenido. Entre estas excepciones se incluyen las siguientes:  

-   Clientes de Windows cuando transmiten en secuencia contenido de App-V.  

-   Clientes de Windows Phone, aunque estos clientes sí comprueban la firma de una aplicación si está firmada por un origen de confianza.  

-   Clientes de Windows RT, aunque estos clientes comprueban la firma de una aplicación si está firmada por un origen de confianza y, además, usan la validación de nombre completo del paquete (PFN, por sus siglas en inglés).  

-   iOS, aunque estos dispositivos comprueban la firma de una aplicación que esté firmada por cualquier certificado de desarrollador que proceda de un origen de confianza.  

-   Clientes de Nokia, aunque estos clientes comprueban la firma de una aplicación que use un certificado autofirmado. También, la firma de un certificado que proceda de un origen de confianza y el certificado pueden firmar las aplicaciones del origen de instalación de Nokia Symbian (SIS, por sus siglas en inglés).  

-   Android. Además, estos dispositivos no utilizan la validación de firma para la instalación de aplicaciones.  

-   Los clientes que se ejecutan en versiones de Linux y UNIX no admiten SHA-256. Para obtener más información, consulte [Planning for client deployment to Linux and UNIX computers in System Center Configuration Manager](../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md) (Planificación de la implementación del cliente en equipos Linux y UNIX con System Center Configuration Manager).  

### <a name="inventory-signing-and-encryption"></a>Cifrado y firma de inventario  
 El inventario que los clientes envían a los puntos de administración está siempre firmado por dispositivos, independientemente de si se comunican con los puntos de administración a través de HTTP o HTTPS. Si utilizan HTTP, tendrá la opción de cifrar estos datos, lo cual es una práctica recomendada de seguridad.  

### <a name="state-migration-encryption"></a>Cifrado de migración de estado  
 El cifrado de los datos almacenados en los puntos de administración de estado para la implementación de sistema operativo siempre se realiza con la Herramienta de migración de estado de usuario (USMT, por sus siglas en inglés) y 3DES.  

### <a name="encryption-for-multicast-packages-to-deploy-operating-systems"></a>Cifrado de paquetes de multidifusión para implementar sistemas operativos  
 Para cada paquete de implementación de sistema operativo, puede habilitar el cifrado cuando el paquete se transfiere a los equipos mediante multidifusión. El cifrado usa el Estándar de cifrado avanzado (AES, por sus siglas en inglés). Si se habilita el cifrado, no se requiere ninguna configuración de certificado adicional. El punto de distribución habilitado para multidifusión genera automáticamente claves simétricas para cifrar el paquete. Cada paquete tiene su propia clave de cifrado. La clave se almacena en el punto de distribución habilitado para multidifusión mediante el uso de API de Windows estándar. Cuando el cliente se conecta con la sesión de multidifusión, el intercambio de claves se realiza a través de un canal cifrado con el certificado de autenticación de cliente emitido por PKI, si el cliente utiliza HTTPS, o con el certificado autofirmado, si el cliente utiliza HTTP. El cliente almacena la clave en la memoria sólo durante la sesión de multidifusión.  

### <a name="encryption-for-media-to-deploy-operating-systems"></a>Cifrado de los medios usados para implementar sistemas operativos  
 Si se utilizan medios para implementar sistemas operativos, y se especifica una contraseña para protegerlos, las variables de entorno se cifran mediante el Estándar de cifrado avanzado (AES, por sus siglas en inglés). El resto de datos de los medios, incluidos los paquetes y contenido para las aplicaciones, no se cifra.  

### <a name="encryption-for-content-that-is-hosted-on-cloud-based-distribution-points"></a>Cifrado para el contenido hospedado en puntos de distribución basados en la nube  
 A partir de System Center 2012 Configuration Manager SP1, si se usan puntos de distribución basados en la nube, el contenido que se carga en estos puntos de distribución se cifra mediante el Estándar de cifrado avanzado (AES) con un tamaño de clave de 256 bits. El contenido se cifrará de nuevo cada vez que lo actualice. Cuando los clientes descargan el contenido, la conexión HTTPS lo cifra y protege.  

### <a name="signing-in-software-updates"></a>Firma en actualizaciones de software  
 Todas las actualizaciones de software deben estar firmadas por un editor de confianza como medida de protección ante la manipulación. En los equipos cliente, el Agente de Windows Update (WUA, por sus siglas en inglés) examina las actualizaciones en el catálogo, pero no instalará la actualización si no encuentra el certificado digital en el almacén de editores de confianza del equipo local. Si se utilizó un certificado autofirmado para publicar el catálogo de actualizaciones, como Editores WSUS autofirmados, el certificado también debe estar en el almacén de certificados Entidades de certificación raíz de confianza del equipo local para, así, comprobar la validez del certificado. El Agente de Windows Update también comprueba si la opción de directiva de grupo **Permitir el contenido firmado procedente de la ubicación del servicio Microsoft Update de la intranet** está habilitada en el equipo local. Esta opción de directiva debe estar habilitada para que el Agente de Windows Update pueda examinar las actualizaciones que se crearon y publicaron con Updates Publisher.  

 Cuando se publican actualizaciones de software en System Center Updates Publisher, un certificado digital las firma cuando se publican en un servidor de actualizaciones. Puede firmar la actualización de software con un certificado PKI, o con un certificado autofirmado generado con Updates Publisher.  

### <a name="signed-configuration-data-for-compliance-settings"></a>Datos de configuración firmados para configuración de cumplimiento  
 Cuando se importan datos de configuración, Configuration Manager comprueba la firma digital de los archivos. Si los archivos no están firmados, o si la comprobación de firma digital no se completa correctamente, el sistema emitirá una advertencia, y se solicitará al usuario confirmación para continuar con la importación. Continúe con la importación de datos de configuración sólo si confía totalmente en el editor y la integridad de los archivos.  

### <a name="encryption-and-hashing-for-client-notification"></a>Cifrado y hash para notificación de cliente  
 Si utiliza la notificación de cliente, todas las comunicaciones utilizarán TLS y el nivel de cifrado más alto que puedan negociar los sistemas operativos del servidor y del cliente. Por ejemplo, un equipo cliente que ejecuta Windows 7 y un punto de administración que ejecuta Windows Server 2008 R2 pueden admitir un cifrado de AES de 128 bits; sin embargo, este mismo punto de administración con un equipo cliente que ejecuta Vista sólo podrán optar a cifrados interiores a 3DES. La misma negociación se produce para la aplicación del hash en los paquetes que se transfieren durante la notificación de cliente, que utiliza SHA-1 o SHA-2.  

##  <a name="certificates-used-by-configuration-manager"></a>Certificados que usa Configuration Manager  
 Para obtener una lista de los certificados PKI (infraestructura de clave pública) que puede usar Configuration Manager, sus requisitos y limitaciones específicos y cómo se usan los certificados, consulte [PKI certificate requirements for System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md) (Requisitos de certificados PKI para System Center Configuration Manager). Esta lista incluye las longitudes de clave y los algoritmos hash admitidos. La mayoría de los certificados admiten una longitud de clave de 2048 bits y SHA-256.  

> [!NOTE]  
>  Todos los certificados que usa Configuration Manager deben contener caracteres de byte único en el nombre del sujeto o el nombre alternativo del sujeto.  

 Se requieren certificados PKI para los siguientes escenarios:  

-   Cuando se administran clientes de Configuration Manager en Internet.  

-   Cuando se administran clientes de Configuration Manager en dispositivos móviles.  

-   Cuando se administran equipos Mac.  

-   Cuando se utilizan puntos de distribución basados en nube.  

-   Cuando se administran equipos basados en Intel AMT fuera de banda.  

 Para el resto de comunicaciones de Configuration Manager que requieren certificados para la autenticación, firma y cifrado, Configuration Manager usa automáticamente certificados PKI, si están disponibles. Si no están disponibles, Configuration Manager genera certificados autofirmados.  

 Configuration Manager no usa certificados PKI cuando administra dispositivos móviles mediante el conector de Exchange Server.  

### <a name="mobile-device-management-and-pki-certificates"></a>Certificados PKI y administración de dispositivos móviles  
 Si el dispositivo móvil no está bloqueado por el operador de telefonía móvil, puede usar Configuration Manager o Microsoft Intune para solicitar e instalar un certificado de cliente. Este certificado permite la autenticación mutua entre el cliente del dispositivo móvil y los sistemas de sitio de Configuration Manager o los servicios de Microsoft Intune. Si el dispositivo móvil está bloqueado, no podrá usar Configuration Manager ni Intune para implementar certificados.  

 Si habilita el inventario de hardware para dispositivos móviles, Configuration Manager o Intune también hará un inventario de los certificados que están instalados en el dispositivo móvil.  

### <a name="out-of-band-management-and-pki-certificates"></a>Certificados PKI y administración fuera de banda  
 La administración fuera de banda para equipos basados en Intel AMT usa, como mínimo, dos tipos de certificados emitidos por PKI: un certificado de aprovisionamiento de AMT y un certificado de servidor web.  

 El punto de servicio fuera de banda utiliza un certificado de aprovisionamiento de AMT para preparar los equipos para la administración fuera de banda. Los equipos basados en AMT objeto de aprovisionamiento deben confiar en el certificado que presenta el punto de administración fuera de banda. De forma predeterminada, los fabricantes de equipos configuran los equipos basados en AMT para que utilicen entidades de certificación externas, como VeriSign, Go Daddy, Comodo o Starfield. Si adquiere un certificado de aprovisionamiento de una de las entidades de certificación externas y configura Configuration Manager para que lo use, los equipos basados en AMT confiarán en la entidad de certificación del certificado de aprovisionamiento y el proceso se completará correctamente. Sin embargo, se recomienda utilizar la entidad de certificación interna propia para emitir el certificado de aprovisionamiento de AMT.  

 Los equipos basados en AMT ejecutan un componente de servidor web en su firmware. Este componente de servidor web cifra el canal de comunicación con el punto de servicio fuera de banda mediante Seguridad de la capa de transporte (TLS, por sus siglas en inglés). El BIOS de AMT no tiene interfaz de usuario para configurar manualmente un certificado; por lo tanto, debe tener una entidad de certificación de Microsoft que apruebe automáticamente las solicitudes de certificado procedentes de equipos basados en AMT. La solicitud utiliza PKCS #10 para el formato de solicitud, y a su vez, utiliza PKCS#7 para transmitir la información del certificado al equipo basado en AMT.  

 Aunque el equipo basado en AMT esté autenticado en el equipo que lo administra, no hay ningún certificado PKI de cliente correspondiente en el equipo que lo administra. En su lugar, estas comunicaciones utilizan la autenticación de Kerberos de HTTP implícita. Si se utiliza HTTP implícita, el cifrado se realiza con TLS.  

 Se podría requerir otro tipo de certificado para la administración de equipos basados en AMT fuera de banda: un certificado de cliente opcional para redes inalámbricas y cableadas 802.1X autenticadas. El equipo basado en AMT podría requerir el certificado de cliente para la autenticación en el servidor RADIUS. Cuando el servidor RADIUS está configurado para la autenticación EAP-TLS, siempre se requiere un certificado de cliente. Cuando el servidor RADIUS está configurado para EAP-TTLS/MSCHAPv2 o PEAPv0/EAP-MSCHAPv2, la configuración de RADIUS especifica si se requiere un certificado de cliente o no. Para solicitar este certificado, el equipo basado en AMT utiliza el mismo proceso que para solicitar el certificado de servidor web.  

### <a name="operating-system-deployment-and-pki-certificates"></a>Implementación de sistema operativo y certificados PKI  
 Cuando usa Configuration Manager para implementar sistemas operativos y un punto de administración requiere conexiones de cliente HTTPS, el equipo cliente debe tener también un certificado para comunicarse con el punto de administración, aunque se encuentre en una fase de transición como el arranque desde medios de secuencia de tareas o un punto de administración habilitado con entorno PXE. Para que este escenario sea compatible, debe crear un certificado de autenticación del cliente PKI, exportarlo con la clave privada e importarlo en las propiedades del servidor de sitio, así como agregar el certificado de CA raíz de confianza del punto de administración.  

 Si se crea un medio de arranque, se importa el certificado de autenticación del cliente al crear el medio de arranque. Configure una contraseña en el medio de arranque para proteger la clave privada y demás información confidencial configurada en la secuencia de tareas. Todos los equipos que se arranquen desde el medio de arranque presentarán el mismo certificado al punto de administración según sea necesario para las funciones de cliente tales como la solicitud de una directiva de cliente.  

 Si se utiliza el arranque PXE, se importa el certificado de autenticación del cliente en el punto de distribución habilitado con PXE; se utiliza el mismo certificado para todos los clientes que se arranquen desde ese punto de distribución habilitado con PXE. Por motivos de seguridad, se recomienda solicitar a los usuarios que conectan sus equipos a un servicio PXE que faciliten una contraseña para proteger la clave privada y demás información confidencial de la secuencia de tareas.  

 Si cualquiera de estos certificados de autenticación del cliente se ve comprometido, bloquee los certificados en el nodo **Certificados** del área de trabajo **Administración** , nodo **Seguridad** . Para administrar estos certificados, debe tener el derecho **Administrar certificado de implementación de sistema operativo** .  

 Una vez que el sistema operativo está implementado y Configuration Manager está instalado, el cliente necesitará su propio certificado de autenticación del cliente PKI para la comunicación de cliente HTTPS.  

### <a name="isv-proxy-solutions-and-pki-certificates"></a>Soluciones de proxy de ISV y certificados PKI  
 Los fabricantes de software independientes (ISV) pueden crear aplicaciones que extienden Configuration Manager. Por ejemplo, un ISV puede crear extensiones compatibles con plataformas de cliente que no sean de Windows, como los equipos Macintosh o UNIX. Sin embargo, si los sistemas de sitio requieren conexiones de cliente HTTPS, estos clientes también deben usar certificados PKI para comunicarse con el sitio. Configuration Manager incluye la capacidad para asignar un certificado al proxy de ISV que permite la comunicación entre los clientes de proxy de ISV y el punto de administración. Si utiliza extensiones que requieren certificados de proxy de ISV, consulte la documentación del producto correspondiente. Para obtener más información sobre cómo crear certificados de proxy de ISV, consulte el kit de desarrollador de software (SDK) de Configuration Manager.  

 Si el certificado de ISV se ve comprometido, bloquéelo en el nodo **Certificados** del área de trabajo **Administración** , nodo **Seguridad** .  

### <a name="asset-intelligence-and-certificates"></a>Asset Intelligence y certificados  
 Configuration Manager se instala con un certificado X.509 que el punto de sincronización de Asset Intelligence usa para conectarse a Microsoft. Configuration Manager usa este certificado para solicitar un certificado de autenticación del cliente del servicio de certificados de Microsoft. El certificado de autenticación del cliente se instala en el servidor de sistema de sitio del punto de sincronización de Asset Intelligence y se utiliza para autenticar el servidor en Microsoft. Configuration Manager utiliza el certificado de autenticación del cliente para descargar el catálogo Asset Intelligence y cargar títulos de software.  

 Este certificado tiene una longitud de clave de 1024 bits.  

### <a name="cloud-based-distribution-points-and-certificates"></a>Puntos de distribución basados en la nube y certificados  
 A partir de System Center 2012 Configuration Manager SP1, los puntos de distribución basados en la nube requieren un certificado de administración (autofirmado o PKI) que se carga en Microsoft Azure. Este certificado de administración requiere capacidad de autenticación de servidor y una longitud de clave de certificado de 2048 bits. Además, se debe configurar un certificado de servicio para cada punto de distribución basado en la nube, que no debe ser autofirmado y que debe tener capacidad de autenticación de servidor y una longitud mínima de clave de certificado de 2048 bits.  

> [!NOTE]  
>  El certificado de administración autofirmado solo se debe utilizar para realizar pruebas y no en redes de producción.  

 Los clientes no requieren un certificado PKI de cliente para utilizar los puntos de distribución basados en la nube; se autentican en la administración mediante el uso de un certificado autofirmado o de un certificado PKI de cliente. Después, el punto de administración emite un token de acceso de Configuration Manager para el cliente, que el cliente presenta al punto de distribución basado en la nube. El token es válido durante 8 horas.  

### <a name="the-microsoft-intune-connector-and-certificates"></a>Conector de Microsoft Intune y certificados  
 Cuando Microsoft Intune inscribe dispositivos móviles, puede administrarlos en Configuration Manager mediante la creación de un conector de Microsoft Intune. El conector usa un certificado PKI con capacidad de autenticación de cliente para autenticar Configuration Manager en Microsoft Intune y transferir toda la información entre ambos mediante SSL. El tamaño de clave de certificado es de 2048 bits y se utiliza el algoritmo hash SHA-1.  

 Cuando instala el conector, se crea un certificado de firma que se almacena en el servidor de sitio para las claves de instalación de prueba, y se crea un certificado de cifrado que se almacena en el punto de registro de certificados para cifrar el desafío del Protocolo de inscripción de certificados simple (SCEP). Estos certificados también tienen un tamaño de clave de 2048 bits y usan el algoritmo hash SHA-1.  

 Cuando Intune inscribe dispositivos móviles, instala un certificado PKI en el dispositivo móvil. Este certificado tiene capacidad de autenticación de cliente, utiliza un tamaño de clave de 2048 bits y utiliza el algoritmo hash SHA-1.  

 Microsoft Intune solicita, genera e instala estos certificados PKI automáticamente.  

### <a name="crl-checking-for-pki-certificates"></a>Comprobación de CRL para certificados PKI  
 Una lista de revocación de certificados (CRL) PKI aumenta la sobrecarga administrativa y de procesamiento, pero resulta más segura. Sin embargo, si la comprobación de CRL está habilitada pero no se puede acceder a la CRL, se produce un error en la conexión de PKI. Para obtener más información, consulte [Security and privacy for System Center Configuration Manager](../../core/plan-design/security/security-and-privacy.md) (Seguridad y privacidad en System Center Configuration Manager).  

 La comprobación de lista de revocación de certificados (CRL) está habilitada de forma predeterminada en IIS, por lo que si usa una CRL con la implementación de PKI, no es necesario configurar nada más en la mayoría de los sistemas de sitio de Configuration Manager que ejecutan IIS. Las actualizaciones de software constituyen una excepción, ya que se requiere un paso manual para habilitar la comprobación de CRL para comprobar las firmas en los archivos de actualización de software.  

 La comprobación de CRL está habilitada de forma predeterminada en los equipos cliente cuando utilizan conexiones de cliente HTTPS. La comprobación de CRL no está habilitada de forma predeterminada cuando se ejecuta la consola de administración fuera de banda para conectarse a un equipo basado en AMT, pero se puede habilitar esta opción. No se puede deshabilitar la comprobación de CRL en los clientes de equipos Mac en Configuration Manager SP1 o versiones posteriores.  

 La comprobación de CRL no es compatible con las siguientes conexiones en Configuration Manager:  

-   Conexiones entre servidores.  

-   Dispositivos móviles inscritos por Configuration Manager.  

-   Dispositivos móviles inscritos por Microsoft Intune.  

##  <a name="cryptographic-controls-for-server-communication"></a>Controles criptográficos para la comunicación de servidor  
 Configuration Manager usa los siguientes controles criptográficos para la comunicación de servidor.  

### <a name="server-communication-within-a-site"></a>Comunicación de servidor dentro de un sitio  
 Cada servidor de sistema de sitio usa un certificado para transferir datos a otros sistemas de sitio en el mismo sitio de Configuration Manager. Algunos roles de sistema de sitio también utilizan certificados para la autenticación. Por ejemplo, si instala el punto de proxy de inscripción en un servidor y el punto de inscripción en otro servidor, pueden autenticarse entre sí mediante el uso de este certificado de identidad. Cuando Configuration Manager usa un certificado para esta comunicación, si hay un certificado PKI disponible que tenga capacidad de autenticación de servidor, Configuration Manager lo usa automáticamente. En caso contrario, genera un certificado autofirmado. Este certificado autofirmado tiene capacidad de autenticación de servidor, usa SHA-256 y tiene una longitud de clave de 2048 bits. Configuration Manager copia el certificado en el almacén de usuarios de confianza de otros servidores de sistema de sitio que podrían necesitar confiar en el sistema de sitio. Los sistemas de sitio, a continuación, pueden confiar unos en otros mediante el uso de estos certificados y confianza de mismo nivel.  

 Además de este certificado para cada servidor de sistema del sitio, Configuration Manager genera un certificado autofirmado para la mayoría de los roles de sistema de sitio. Si hay más de un rol de sistema de sitio en el mismo sitio, comparten el mismo certificado. Por ejemplo, podría tener varios puntos de administración o varios puntos de inscripción en el mismo sitio. Este certificado autofirmado también utiliza SHA-256 y tiene una longitud de clave de 2048 bits. Asimismo se copia en el almacén de usuarios de confianza de los servidores de sistema de sitio que podrían necesitar confiar en él. Los siguientes roles de sistema de sitio generan este certificado:  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de sincronización de Asset Intelligence  

-   Punto de registro de certificados  

-   Punto de Endpoint Protection  

-   Punto de inscripción  

-   Punto de estado de reserva  

-   Punto de administración  

-   Punto de distribución habilitado con multidifusión  

-   Servidor que ejecuta Internet Information Services (IIS)  

-   Punto de servicios de informes  

-   Punto de actualización de software  

-   Punto de migración de estado  

-   Punto de Validador de mantenimiento del sistema  

-   Conector de Microsoft Intune  

 Estos certificados se administran automáticamente mediante Configuration Manager y, en caso necesario, se generan automáticamente.  

 Configuration Manager también usa un certificado de autenticación del cliente para enviar mensajes de estado desde el punto de distribución hasta el punto de administración. Cuando el punto de administración está configurado solamente para conexiones de cliente HTTPS, se debe utilizar un certificado PKI. Si el punto de administración acepta las conexiones HTTP, se puede utilizar un certificado PKI o seleccionar la opción de uso de un certificado autofirmado que tiene capacidad de autenticación de servidor, utiliza SHA-256 y tiene una longitud de clave de 2048 bits.  

### <a name="server-communication-between-sites"></a>Comunicación de servidor entre sitios  
 Configuration Manager transfiere datos entre sitios mediante el uso de replicación de base de datos y replicación basada en archivos. Para obtener más información, consulte [Communications between endpoints in System Center Configuration Manager](../../core/plan-design/hierarchy/communications-between-endpoints.md) (Comunicaciones entre puntos de conexión en System Center Configuration Manager).  

 Configuration Manager configura automáticamente la replicación de base de datos entre sitios y usa certificados PKI que tienen capacidad de autenticación de servidor si están disponibles; en caso contrario, crea certificados autofirmados para la autenticación de servidor. En ambos casos, la autenticación entre sitios se establece mediante el uso de certificados del almacén de usuarios de confianza que utiliza confianza de mismo nivel. Este almacén de certificados se usa para garantizar que solo los equipos con SQL Server que usa la jerarquía de Configuration Manager participan en la replicación de sitio a sitio. Mientras que los sitios primarios y el sitio de administración central pueden replicar los cambios de configuración en todos los sitios de la jerarquía, los sitios secundarios solo pueden replicar los cambios de configuración en su sitio primario.  

 Los servidores de sitio establecen la comunicación de sitio a sitio mediante un intercambio de claves seguro que se realiza automáticamente. El servidor de sitio emisor genera un hash y lo firma con su clave privada. El servidor de sitio receptor comprueba la firma con la clave pública y compara el hash con un valor generado localmente. Si coinciden, el sitio receptor acepta los datos replicados. Si los valores no coinciden, Configuration Manager rechaza los datos de replicación.  

 La replicación de base de datos en Configuration Manager usa SQL Server Service Broker para transferir datos entre sitios mediante los siguientes mecanismos:  

-   Conexión de SQL Server a SQL Server: utiliza credenciales de Windows para autenticación de servidor y certificados autofirmados de 1024 bits para firmar y cifrar los datos mediante el Estándar de cifrado avanzado (AES). Se utilizarán certificados PKI con capacidad de autenticación de servidor si están disponibles. El certificado debe estar ubicado en el almacén personal del almacén de certificados del equipo.  

-   SQL Service Broker: utiliza certificados autofirmados de 2048 bits para autenticación y para firmar y cifrar los datos mediante el Estándar de cifrado avanzado (AES). El certificado debe estar ubicado en la base de datos maestra de SQL Server.  

 La replicación basada en archivos utiliza el protocolo de Bloque de mensajes del servidor (SMB) y utiliza SHA-256 para firmar los datos que no están cifrados pero no contienen información confidencial. Si quiere cifrar los datos, puede usar IPsec y debe implementarlo independientemente de Configuration Manager.  

##  <a name="cryptographic-controls-for-clients-that-use-https-communication-to-site-systems"></a>Controles criptográficos para los clientes que usan la comunicación HTTPS con los sistemas de sitio  
 Cuando los roles de sistema de sitio aceptan conexiones de cliente, se pueden configurar para que acepten conexiones HTTPS y HTTP, o solo conexiones HTTPS. Los roles de sistema de sitio que aceptan conexiones de Internet solo aceptan conexiones de cliente a través de HTTPS.  

 Las conexiones de cliente a través de HTTPS ofrecen un mayor nivel de seguridad gracias a la integración con una infraestructura de clave pública (PKI) para proteger la comunicación entre cliente y servidor. Sin embargo, podría seguir existiendo vulnerabilidad si se configuran las conexiones de cliente HTTPS sin un conocimiento profundo de la planeación, la implementación y las operaciones de PKI. Por ejemplo, si no protege la CA raíz, la confianza de toda la infraestructura PKI podría verse comprometida a través de la acción de atacantes. Si no se implementan y administran los certificados PKI mediante procesos controlados y seguros, se obtendrán como resultado clientes no administrados que no pueden recibir paquetes ni actualizaciones de software imprescindibles.  

> [!IMPORTANT]  
>  Los certificados PKI que se utilizan para la comunicación del cliente protegen la comunicación solo entre el cliente y algunos sistemas de sitio. No protegen el canal de comunicación entre el servidor de sitio y los sistemas de sitio o entre servidores de sitio.  

### <a name="communication-that-is-unencrypted-when-clients-use-https-communication"></a>Comunicación sin cifrar cuando los clientes usan la comunicación HTTPS  
 Cuando los clientes se comunican con los sistemas de sitio mediante HTTPS, las comunicaciones se suelen cifrar mediante SSL. Sin embargo, en las siguientes situaciones, los clientes se comunican con los sistemas de sitio sin utilizar cifrado:  

-   El cliente no puede realizar una conexión HTTPS en la intranet y recurre al uso de HTTP cuando los sistemas de sitio permiten esta configuración  

-   Comunicación con los siguientes roles de sistema de sitio:  

    -   El cliente envía mensajes de estado al punto de estado de reserva  

    -   El cliente envía solicitudes PXE a un punto de distribución habilitado con PXE  

    -   El cliente envía datos de notificación a un punto de administración  

 Los puntos de servicios de informes están configurados para utilizar HTTP o HTTPS independientemente del modo de comunicación del cliente.  

##  <a name="cryptographic-controls-for-clients-chat-use-http-communication-to-site-systems"></a>Controles criptográficos para los clientes que usan la comunicación HTTP con los sistemas de sitio  
 Cuando los clientes usan la comunicación HTTP con los roles de sistema de sitio, pueden usar los certificados PKI para la autenticación del cliente, o los certificados autofirmados que genera Configuration Manager. Cuando Configuration Manager genera certificados autofirmados, cuentan con un identificador personalizado de objetos para la firma y el cifrado. Estos certificados se usan para identificar al cliente de forma única. Para todos los sistemas operativos admitidos excepto Windows Server 2003, estos certificados autofirmados usan SHA-256 y tienen una longitud de clave de 2048 bits. Para Windows Server 2003, se utiliza SHA1 con una longitud de clave de 1024 bits.  

### <a name="operating-system-deployment-and-self-signed-certificates"></a>Implementación de sistema operativo y certificados autofirmados  
 Cuando usa Configuration Manager para implementar sistemas operativos con certificados autofirmados, el equipo cliente debe tener también un certificado para comunicarse con el punto de administración, aunque se encuentre en una fase de transición como el arranque desde medios de secuencia de tareas o un punto de administración habilitado con entorno PXE. Para que este escenario sea compatible con conexiones de cliente HTTP, Configuration Manager genera certificados autofirmados que cuentan con un identificador personalizado de objetos para la firma y el cifrado, y que se usan para identificar al cliente de forma única. Para todos los sistemas operativos admitidos excepto Windows Server 2003, estos certificados autofirmados usan SHA-256 y tienen una longitud de clave de 2048 bits. Para Windows Server 2003, se utiliza SHA1 con una longitud de clave de 1024 bits. Si los certificados autofirmados se ven comprometidos, para evitar que se utilicen para suplantar a clientes de confianza, bloquee los certificados en el nodo **Certificados** del área de trabajo **Administración** , nodo **Seguridad** .  

### <a name="client-and-server-authentication"></a>Autenticación de servidor y cliente  
 Cuando los clientes se conectan a través de HTTP, autentican los puntos de administración mediante Active Directory Domain Services o la clave raíz confiable de Configuration Manager. Los clientes no autentican otros roles de sistema de sitio como puntos de migración de estado o puntos de actualización de software.  

 Cuando un punto de administración autentica primero un cliente mediante el certificado de cliente autofirmado, este mecanismo proporciona una seguridad mínima, ya que cualquier equipo puede generar un certificado autofirmado. En esta situación, se debe aumentar el proceso de identidad del cliente por aprobación. Solo los equipos de confianza deben aprobarse, ya sea automáticamente mediante Configuration Manager o a través de un usuario administrativo de forma manual. Para obtener más información, consulte la sección relativa a la aprobación en [Communications between endpoints in System Center Configuration Manager](../../core/plan-design/hierarchy/communications-between-endpoints.md) (Comunicaciones entre puntos de conexión en System Center Configuration Manager).  

##  <a name="about-ssl-vulnerabilities"></a>Acerca de las vulnerabilidades SSL  
 Se recomienda deshabilitar SSL 3.0, habilitar TLS 1.1 y 1.2 y reordenar los conjuntos de cifrado relacionados con TLS para mejorar la seguridad de los servidores de Configuration Manager. Puede obtener información sobre cómo realizar estas acciones en [este artículo de Knowledge Base](https://support.microsoft.com/en-us/kb/245030/). Esta acción no afectará a la funcionalidad de Configuration Manager.  

