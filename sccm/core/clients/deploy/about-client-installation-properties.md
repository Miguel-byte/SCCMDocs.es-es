---
title: "Propiedades de instalación del cliente | System Center Configuration Manager"
description: "Obtenga información sobre las propiedades de instalación de clientes en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: 15
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 3987e6a66f9c0f52da8ce9a8c29e35836d2a2bcb

---
# <a name="about-client-installation-properties-in-system-center-configuration-manager"></a>Acerca de las propiedades de instalación de clientes en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use el comando CCMSetup.exe de System Center Configuration Manager para instalar manualmente el software de cliente de Configuration Manager en los equipos de su empresa.  

##  <a name="a-nameaboutccmsetupa-about-ccmsetupexe"></a><a name="aboutCCMSetup"></a> Acerca de CCMSetup.exe  
 El comando CCMSetup.exe descarga todos los archivos necesarios para completar la instalación del cliente desde un punto de administración especificado o desde una ubicación de origen especificada. Estos archivos podrían incluir lo siguiente:  

-   El paquete de Windows Installer Client.msi que instala el software cliente de Configuration Manager.  

-   Archivos de instalación del Servicio de transferencia inteligente en segundo plano (BITS), en caso necesario.  

-   Archivos de instalación de Windows Installer, en caso necesario.  

-   Actualizaciones y correcciones para el cliente de Configuration Manager, en caso necesario.  

> [!NOTE]  
>  En Configuration Manager no se puede ejecutar el archivo Client.msi directamente.  

 CCMSetup.exe proporciona varias propiedades de línea de comandos para personalizar el comportamiento de la instalación. Además, también puede especificar propiedades para modificar el comportamiento de Client.msi en la línea de comandos de CCMSetup.exe.  

> [!IMPORTANT]  
>  Debe especificar todas las propiedades necesarias de CCMSetup antes de especificar propiedades para Client.msi.  

 CCMSetup.exe y sus archivos auxiliares se encuentran en el servidor de sitio de Configuration Manager en la carpeta **Client** de la carpeta de instalación de Configuration Manager. Esta carpeta se comparte en la red como **&lt;Nombre del servidor de sitio\>\SMS_&lt;Código de sitio\>\Cliente**.  

 En el símbolo del sistema, el comando CCMSetup.exe utiliza el formato siguiente:  

 **CCMSetup.exe [&lt;propiedades de Ccmsetup\>] [&lt;propiedades de instalación de client.msi>]**  

 Ejemplo:  

 **CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01**  

 Este comando de ejemplo realiza las siguientes acciones:  

-   Especifica al punto de administración denominado SMSMP01 que solicite una lista de puntos de distribución para descargar los archivos fuente de instalación de cliente.  

-   Especifica que la instalación debe detenerse si ya existe una versión del cliente de Configuration Manager en el equipo.  

-   Indica a client.msi que asigne el cliente al código del sitio S01.  

-   Indica a client.msi que use el punto de estado de reserva denominado SMSFP01.  

> [!NOTE]  
>  Si una propiedad contiene espacios, ponga comillas ("").  

 Las propiedades descritas en la tabla siguiente están disponibles para modificar el comportamiento de la instalación de CCMSetup.exe.  

> [!IMPORTANT]  
>  Si amplió el esquema de Active Directory para Configuration Manager, muchas propiedades de instalación de cliente se publican en Servicios de dominio de Active Directory y el cliente de Configuration Manager las lee automáticamente. Para obtener una lista de las propiedades de instalación de cliente publicada en Servicios de dominio de Active Directory, consulte [Acerca de las propiedades de instalación de cliente publicadas en Servicios de dominio de Active Directory en System Center Configuration Manager](about-client-installation-properties-published-to-active-directory-domain-services.md).  

##  <a name="a-namebkmkccmsetupcommandlinea-ccmsetupexe-command-line-properties"></a><a name="BKMK_CCMSetupCommandLine"></a> Propiedades de la línea de comandos de CCMSetup.exe  

-   **/?**  

     Abre el cuadro de diálogo **CCMSetup** que muestra las propiedades de la línea de comandos para ccmsetup.exe.  

     Ejemplo: **ccmsetup.exe /?**  

-   **/source:&lt;ruta de acceso\>**  

     Especifica la ubicación desde la que se van a descargar archivos de instalación. Puede utilizar una ruta de instalación local o UNC. Los archivos se descargan mediante el protocolo Bloque de mensajes del servidor (SMB).  

    > [!NOTE]  
    >  Puede utilizar la propiedad **/source** varias veces en la línea de comandos para especificar ubicaciones alternativas desde donde descargar archivos de instalación.  

    > [!IMPORTANT]  
    >  Para usar la propiedad de la línea de comandos **/source** , la cuenta de usuario de Windows usada para la instalación del cliente debe tener permisos de lectura en la ubicación de instalación.  

     Ejemplo: **ccmsetup.exe /source:"\\\computer\folder"**  

-   **/mp:&lt;equipo\>**  

     Especifica un punto de administración de origen para que los equipos se conecten de forma que puedan buscar el punto de distribución más cercano para descargar los archivos de instalación del cliente. Si no hay ningún punto de distribución o los equipos no pueden descargar los archivos desde los puntos de distribución después de 4 horas, los clientes descargan los archivos desde el punto de administración especificado.  

     Los equipos descargan los archivos a través de una conexión HTTP o HTTPS, dependiendo de la configuración del rol de sistema de sitio para las conexiones de cliente. La descarga utiliza límite de BITS si este está configurado. Si todos los puntos de distribución y puntos de administración se configuran solo para conexiones cliente HTTPS, debe comprobar que el equipo cliente tenga un certificado de cliente de infraestructura de clave pública (PKI) válido.  

    > [!NOTE]  
    >  Puede usar la propiedad de la línea de comandos **/mp** para especificar varios puntos de administración de forma que si el equipo no se puede conectar al primero, lo intentará con el segundo y así sucesivamente. Cuando especifique varios puntos de administración, separe los valores con puntos y comas.  

    > [!IMPORTANT]  
    >  Esta propiedad se utiliza solo para especificar un punto de administración inicial para que los equipos busquen el origen más cercano para descargar los archivos de instalación del cliente. No especifica el punto de administración al que se asignará el cliente después de la instalación. Puede especificar cualquier punto de administración de Configuration Manager en cualquier sitio para proporcionar a los equipos una lista de puntos de distribución desde la que podrán descargar los archivos de instalación del cliente.  

     Ejemplo con el nombre de equipo: **ccmsetup.exe /mp:SMSMP01**  

     Ejemplo con el nombre de dominio completo (FQDN): **ccmsetup.exe /mp:smsmp01.contoso.com**  

    > [!TIP]  
    >  Si el cliente se conecta a un punto de administración mediante HTTPS, por lo general, debe especificar el FQDN de esta opción en lugar del nombre del equipo. El valor que especifique debe estar incluido en el nombre del firmante o nombre alternativo del firmante del certificado PKI del punto de administración. Aunque Configuration Manager admita un nombre de equipo solo en este certificado PKI para conexiones en la intranet, se recomienda el uso de un FQDN como medida de seguridad.  

-   **/retry:&lt;minutos\>**  

     Especifica el intervalo de reintentos si CCMSetup.exe no puede descargar los archivos de instalación. El valor predeterminado es **10** minutos. CCMSetup continúa intentándolo hasta que alcanza el límite especificado en la propiedad de la instalación **downloadtimeout** .  

     Ejemplo: **ccmsetup.exe /retry:20**  

-   **/noservice**  

     Impide que CCMSetup se ejecute como un servicio. Cuando CCMSetup se ejecuta como un servicio, se ejecuta en el contexto de la cuenta de sistema local del equipo, que puede que no tenga derechos suficientes para acceder a los recursos de red necesarios para el proceso de instalación. Cuando se especifica la opción **/noservice** , CCMSetup.exe se ejecuta en el contexto de la cuenta de usuario utilizada para iniciar el proceso de instalación. De forma adicional, si usa un script para ejecutar CCMSetup.exe con la propiedad **/service** , CCMSetup.exe se cierra después del inicio del servicio y puede que no proporcione detalles de la instalación correctamente porque el servicio CCMSetup realiza la instalación del cliente. Si no se especifica esta propiedad de la línea de comandos, de forma predeterminada, se usará **/service** .  

     Ejemplo: **ccmsetup.exe /noservice**  

-   **/service**  

     Especifica que CCMSetup debe ejecutarse como un servicio que utiliza la cuenta de sistema local.  

     Ejemplo: **ccmsetup.exe /service**  

-   **/uninstall**  

     Especifica que el software cliente de Configuration Manager se debe desinstalar. Para más información, vea [How to manage clients in System Center Configuration Manager](../manage/manage-clients.md).  

     Ejemplo: **ccmsetup.exe /uninstall**  

-   **/logon**  

     Especifica que la instalación del cliente debe detenerse si ya hay instalada una versión de Configuration Manager o del cliente de Configuration Manager.  

     Ejemplo: **ccmsetup.exe /logon**  

-   **/forcereboot**  

     Especifica que CCMSetup debe exigir que el equipo cliente se reinicie si es necesario para completar la instalación del cliente. Si no se especifica esta opción, CCMSetup termina cuando es necesario reiniciar el equipo y, a continuación, continúa después del siguiente reinicio manual.  

     Ejemplo: **CCMSetup.exe /forcereboot**  

-   **/BITSPriority:&lt;prioridad\>**  

     Especifica la prioridad de descarga cuando se descargan los archivos de instalación del cliente mediante una conexión HTTP. Los valores posibles son:  

    -   FOREGROUND  

    -   HIGH  

    -   NORMAL  

    -   LOW  

     El valor predeterminado es NORMAL.  

     Ejemplo: **ccmsetup.exe /BITSPriority:HIGH**  

-   **/downloadtimeout:&lt;minutos\>**  

     Especifica el tiempo en minutos que CCMSetup intenta descargar los archivos de instalación del cliente antes de desistir. El valor predeterminado es **1440** minutos (1 día).  

     Ejemplo: **ccmsetup.exe /downloadtimeout:100**  

-   **/UsePKICert**  

     Cuando se especifica, el cliente utiliza un certificado PKI que incluye autenticación de cliente si está disponible. Si no se encuentra un certificado válido, el cliente recurre al uso de una conexión HTTP y un certificado autofirmado. Cuando no se especifica esta opción, el cliente utiliza un certificado autofirmado y todas las comunicaciones con sistemas de sitio se realizan mediante HTTP.  

    > [!NOTE]  
    >  Existen algunos escenarios donde no es necesario especificar esta propiedad cuando se va a instalar un cliente para que use un certificado de cliente PKI. Estos escenarios incluyen la instalación de un cliente mediante la instalación de cliente basada en punto de actualización de software y la instalación de inserción de cliente. No obstante, debe especificar esta propiedad siempre que instale manualmente un cliente y use la propiedad **/mp** para especificar un punto de administración configurado para aceptar únicamente conexiones cliente HTTPS. También debe especificar esta propiedad cuando instale un cliente para la comunicación de Internet mediante la propiedad CCMALWAYSINF=1 (junto con las propiedades del punto de administración basado en Internet y el código de sitio). Para más información acerca de la administración de clientes basada en Internet, consulte [Consideraciones sobre las comunicaciones de cliente desde Internet o desde un bosque que no es de confianza](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) en [Comunicaciones entre puntos de conexión en System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

     Ejemplo: **CCMSetup.exe /UsePKICert**  

-   **/NoCRLCheck**  

     Especifica que un cliente no debe comprobar la lista de revocación de certificados (CRL) cuando se comunica a través de HTTPS mediante un certificado PKI.  

     Cuando no se especifica esta opción, el cliente comprueba la CRL antes de establecer una conexión HTTPS con certificados PKI.  

     Para más información sobre la comprobación de CRL de cliente, consulte [Planning for PKI certificate revocation](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs) en[Plan for security en System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

     Ejemplo: **CCMSetup.exe /UsePKICert /NoCRLCheck**  

-   **/config:&lt;archivo de configuración\>**  

     Especifica el nombre de un archivo de texto que contiene propiedades de la instalación de cliente. Salvo que se especifique también la propiedad **/noservice** de CCMSetup, este archivo debe encontrarse en la carpeta de CCMSetup, que es %Windir%\\Ccmsetup en sistemas operativos de 32 y 64 bits. Si se especifica la propiedad **/noservice** , este archivo debe estar en la misma carpeta desde la que se ejecuta CCMSetup.exe.  

     Ejemplo: **CCMSetup.exe /config:&lt;Nombre de archivo de configuración.txt\>**  

     Use el archivo mobileclienttemplate.tcf de la carpeta &lt;directorio de Configuration Manager\>\\bin\\&lt;plataforma\> del equipo del servidor de sitio para proporcionar el formato correcto del archivo. Este archivo también contiene información en forma de comentario acerca de las secciones y cómo se utilizan. Especifique las propiedades de la instalación del cliente en la sección [Instalación de cliente], después del texto siguiente: **Install=INSTALL=ALL**.  

     Entrada de la sección [Instalación de cliente] de ejemplo: **Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100**  

-   **/skipprereq:&lt;nombre de archivo\>**

     Especifica que CCMSetup.exe no debe instalar el programa de requisito previo especificado cuando el cliente de Configuration Manager está instalado.  

     Ejemplos: **CCMSetup.exe /skipprereq:silverlight.exe** o **CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;Silverlight.exe**  

    > [!NOTE]  
    >  Esta propiedad admite la entrada de varios valores. Utilice el carácter de punto y coma (;) para separar cada valor.  

-   **/forceinstall**  

     Especifica que cualquier cliente existente se va a desinstalar y, a continuación, se instalará un nuevo cliente.  

-   **/Excludefeatures:&lt;característica\>**  

     Especifica que CCMSetup.exe no se instalará la característica especificada cuando el cliente de Configuration Manager está instalado.  

     Ejemplo: **CCMSetup.exe /ExcludeFeatures:ClientUI** no se instalará el Centro de software en el cliente.  

    > [!NOTE]  
    >  Para esta versión, **ClientUI** es el único valor compatible con la propiedad **/ExcludeFeatures** .  

##  <a name="a-nameccmsetupreturncodesa-ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a> Códigos de retorno de CCMSetup.exe  
 El comando CCMSetup.exe proporciona los siguientes códigos de retorno cuando se completa el comando. Para solucionar problemas al ejecutar el comando, revise el archivo ccmsetup.log en el equipo cliente para determinar el contexto y los detalles adicionales sobre los problemas de código de retorno.  

|Código de retorno|Significado|  
|-----------------|-------------|  
|0|Correcto|  
|6|Error|  
|7|Es necesario reiniciar|  
|8|El programa de instalación se está ejecutando|  
|9|Error de evaluación de requisitos previos|  
|10|Error de validación de hash del manifiesto de la instalación|  

##  <a name="a-nameclientmsipropsa-clientmsi-properties"></a><a name="clientMsiProps"></a> Propiedades de Client.msi  
 Las siguientes propiedades pueden modificar el comportamiento de la instalación de client.msi. Si usa el método de instalación de inserción de cliente, también puede especificar las propiedades en la pestaña **Cliente** del cuadro de diálogo **Propiedades de instalación de inserción de cliente** .  

-   **CCMALWAYSINF**  

     Se establece en 1 para especificar que el cliente siempre estará basado en Internet y nunca se conectará a la intranet. El tipo de conexión del cliente muestra **Siempre Internet**.  

     Esta propiedad debe utilizarse junto con CCMHOSTNAME, que especifica el FQDN del punto de administración basado en Internet. También debe utilizarse junto con la propiedad de CCMSetup /UsePKICert y con el código del sitio.  

     Para más información acerca de la administración de clientes basada en Internet, consulte [Consideraciones sobre las comunicaciones de cliente desde Internet o desde un bosque que no es de confianza](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) en [Comunicaciones entre puntos de conexión en System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

     Ejemplo: **CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC**  

-   **CCMCERTISSUERS**  

     Especifica la lista de emisores de certificados, que es una lista de certificados de entidad de certificación raíz de confianza (CA) en los que confía el sitio de Configuration Manager.  

     Para más información sobre la lista de emisores de certificados y cómo los clientes la usan durante el proceso de selección de certificados, consulte [Planning for PKI client certificate selection](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection) en [Plan for security en System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

     Se trata de una coincidencia de mayúsculas y minúsculas de los atributos del firmante que se encuentran en el certificado de entidad de certificación raíz. Los atributos se pueden separar con una coma (,) o un punto y coma (;). Se pueden especificar varios certificados de entidad de certificación raíz mediante el uso de una barra separadora. Ejemplo:  

     **CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &amp;#124; CN=Litware Corporate Root CA; O=Litware, Inc.”**  

    > [!TIP]  
    >  Use el archivo mobileclient.tcf de la carpeta &lt;directorio de Configuration Manager\>\bin\\&lt;plataforma\> del equipo del servidor del sitio para copiar el valor **CertificateIssuers=&lt;cadena\>** configurado para el sitio.  

-   **CCMCERTSEL**  

     Especifica los criterios de selección de certificado si el cliente tiene más de un certificado que se puede utilizar para la comunicación HTTPS (un certificado válido que incluye la capacidad de autenticación de cliente).  

     Puede buscar una coincidencia exacta (use **Subject:**) o una coincidencia parcial (use **SubjectStr:)**en el nombre del firmante o el nombre alternativo del firmante. Ejemplos:  

     **CCMCERTSEL="Subject:computer1.contoso.com"** busca un certificado con una coincidencia exacta con el nombre de equipo "computer1.contoso.com" en el nombre del firmante o nombre alternativo del firmante.  

     **CCMCERTSEL="SubjectStr:contoso.com"** busca un certificado que contenga "contoso.com" en el nombre del firmante o nombre alternativo del firmante.  

     También puede utilizar los atributos de nombre distintivo (DN) o de identificador de objeto (OID) en los atributos de nombre del firmante o de nombre alternativo del firmante, por ejemplo:  

     **CCMCERTSEL="SubjectAttr:2.5.4.11 = Equipos"** busca el atributo de unidad organizativa expresado como un identificador de objeto y con el nombre de Equipos.  

     **CCMCERTSEL="SubjectAttr:OU = Computers"** busca el atributo de unidad organizativa expresado como un nombre distintivo (DN) y con el nombre de Equipos.  

    > [!IMPORTANT]  
    >  Si usa el cuadro Nombre del firmante, el proceso de búsqueda de coincidencias para el valor del criterio de selección **Subject:** distingue entre mayúsculas y minúsculas, pero el proceso de búsqueda de coincidencias para el valor del criterio de selección **SubjectStr:** no distingue entre mayúsculas y minúsculas.  
    >   
    >  Si usa el cuadro Nombre alternativo del firmante, los procesos de búsqueda de coincidencias para los valores de los criterios de selección **Subject:** y **SubjectStr:** no distinguen entre mayúsculas y minúsculas.  

     La lista completa de atributos que puede usar para la selección de certificados está en [Valores de atributos admitidos para los criterios de selección de certificado PKI](#BKMK_attributevalues).  

     Si más de un certificado coincide con la búsqueda y la propiedad CCMFIRSTCERT está establecida en 1, se selecciona el certificado con el período de validez más largo.  

-   **CCMCERTSTORE**  

     Especifica un almacén de certificados alternativo si el certificado de cliente para usar con la comunicación HTTPS no se encuentra en el almacén de certificados predeterminado de **Personal** del equipo.  

     Ejemplo: **CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"**  

-   **CCMFIRSTCERT**  

     Si está establecida en 1, esta propiedad especifica que el cliente debe seleccionar el certificado PKI con el período de validez más largo. Esta configuración puede ser necesaria si utiliza Protección de acceso a redes con cumplimiento de IPsec.  

     Ejemplo: **CCMSetup.exe /UsePKICert CCMFIRSTCERT=1**  

-   **CCMHOSTNAME**  

     Especifica el FQDN del punto de administración basado en Internet si el cliente se administra a través de Internet.  

     No especifique esta opción con la propiedad de instalación SMSSITECODE = AUTO. Los clientes basados en Internet deben asignarse directamente a su sitio basado en Internet.  

     Ejemplo: **CCMSetup.exe  /UsePKICert/ CCMHOSTNAME="SMSMP01.corp.contoso.com"**  

-   **CCMHTTPPORT**  

     Especifica el puerto que el cliente debe usar al comunicarse a través de HTTP con los servidores de sistema de sitio.  

     Si no se especifica el puerto, se utilizará el valor predeterminado de 80.  

     Ejemplo: **CCMSetup.exe CCMHTTPPORT=80**  

-   **CCMHTTPSPORT**  

     Especifica el puerto que el cliente debe usar al comunicarse a través de HTTPS con los servidores de sistema de sitio. Si no se especifica el puerto, se usará el valor predeterminado de 443.  

     Ejemplo: **CCMSetup.exe /UsePKICert CCMHTTPSPORT=443**  

-   **SMSPUBLICROOTKEY**  

     Especifica la clave raíz confiable de Configuration Manager donde no se puede recuperar desde Servicios de dominio de Active Directory. Esta propiedad se aplica a los clientes que utilizan la comunicación de cliente HTTP y HTTPS. Para más enformación, vea [Planneng for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) en [Plan for security en System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

     Ejemplo: **CCMSetup.exe SMSPUBLICROOTKEY=&lt;clave\>**  

-   **SMSROOTKEYPATH**  

     Se utiliza para volver a instalar la clave raíz confiable de Configuration Manager. Especifica el nombre y la ruta de acceso completa en un archivo que contiene la clave raíz confiable. Esta propiedad se aplica a los clientes que utilizan la comunicación de cliente HTTP y HTTPS. Para más enformación, vea [Planneng for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) en [Plan for security en System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

     Ejemplo: CCMSetup.exe **SMSROOTKEYPATH=&lt;Ruta de acceso completa y nombre de archivo\>**  

-   **RESETKEYINFORMATION**  

     Si un cliente de Configuration Manager tiene una clave raíz confiable de Configuration Manager errónea y no puede contactar con un punto de administración confiable para recibir una copia válida de la clave raíz confiable nueva, debe quitar manualmente la clave raíz confiable antigua mediante esta propiedad. Esta situación se suele producir cuando se mueve un cliente de una jerarquía de sitio a otra. Esta propiedad se aplica a los clientes que utilizan la comunicación de cliente HTTP y HTTPS.  

     Ejemplo: **CCMSetup.exe RESETKEYINFORMATION=TRUE**  

-   **CCMDEBUGLOGGING**  

     Habilita el registro de depuración. Los valores pueden ser 0 (desactivado) o 1 (activado). El valor predeterminado es 0. Esto hace que el cliente registre información de bajo nivel que podría ser útil para solucionar problemas. Como práctica recomendada, evite utilizar esta propiedad en sitios de producción porque puede producirse un registro excesivo, lo que podría dificultar la búsqueda de información relevante en los archivos de registro. CCMENABLELOGGING debe establecerse en TRUE para habilitar el registro de depuración.  

     Ejemplo: **CCMSetup.exe CCMDEBUGLOGGING=1**  

-   **CCMENABLELOGGING**  

     Habilita el registro si esta propiedad se establece en TRUE. De forma predeterminada, el registro está habilitado. Los archivos de registro se almacenan en la carpeta **Logs** de la carpeta de instalación del cliente de Configuration Manager. De forma predeterminada, esta carpeta es % Windir%\CCM\Logs.  

     Ejemplo: **CCMSetup.exe CCMENABLELOGGING=TRUE**  

-   **CCMLOGLEVEL**  

     Especifica la cantidad de detalle que se va a escribir en los archivos de registro de Configuration Manager. Especifique un número entero entre 0 y 3, donde 0 es el registro más detallado y 3 solo registra errores. El valor predeterminado es 1.  

     Ejemplo: **CCMSetup.exe CCMLOGLEVEL=3**  

-   **CCMLOGMAXHISTORY**  

     Cuando un archivo de registro de Configuration Manager alcanza los 250 000 bytes de tamaño (o el valor especificado por la propiedad CCMLOGMAXSIZE), cambia su nombre como una copia de seguridad y se crea un nuevo archivo de registro.  

     Esta propiedad especifica el número de versiones anteriores del archivo de registro que se van a conservar. El valor predeterminado es 1. Si el valor se establece en 0, no se mantiene ningún archivo de registro antiguo.  

     Ejemplo: **CCMSetup.exe CCMLOGMAXHISTORY=0**  

-   **CCMLOGMAXSIZE**  

     Especifica el tamaño máximo del archivo de registro en bytes. Cuando un registro crece hasta el tamaño que se especifica, se cambia de nombre como un archivo de historial y se crea un nuevo archivo. Esta propiedad debe establecerse en al menos 10.000 bytes. El valor predeterminado es 250.000 bytes.  

     Ejemplo: **CCMSetup.exe CCMLOGMAXSIZE=300000**  

-   **CCMALLOWSILENTREBOOT**  

     Especifica que el equipo puede reiniciarse después de la instalación del cliente si es necesario.  

    > [!IMPORTANT]  
    >  El equipo se reiniciará sin previo aviso, incluso si un usuario inició sesión.  

     Ejemplo: **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

-   **DISABLESITEOPT**  

     Si se establece en TRUE, deshabilita la capacidad de los usuarios finales con credenciales administrativas en el equipo cliente de cambiar el sitio asignado del cliente de Configuration Manager mediante el uso de Configuration Manager en el Panel de control del equipo cliente.  

     Ejemplo: **CCMSetup.exe DISABLESITEOPT=TRUE**  

-   **DISABLECACHEOPT**  

     Si se establece en TRUE, deshabilita la capacidad de los usuarios finales con credenciales administrativas en el equipo cliente de cambiar la configuración de la carpeta de caché de cliente para el cliente de Configuration Manager mediante el uso de Configuration Manager en el Panel de control del equipo cliente.  

     Ejemplo: **CCMSetup.exe DISABLECACHEOPT=TRUE**  

-   **SMSCACHEDIR**  

     Especifica la ubicación de la carpeta de caché de cliente en el equipo cliente, que almacena los archivos temporales. De forma predeterminada, la ubicación es *%Windir \ccmcache*.  

     Ejemplo: **CCMSetup.exe SMSCACHEDIR="C:\Temp"**  

     Esta propiedad puede utilizarse junto con la propiedad SMSCACHEFLAGS para controlar aún más la ubicación de la carpeta de caché de cliente.  

     Ejemplo: **CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE** instala la carpeta de caché de cliente en la unidad de disco más grande disponible en el cliente.  

-   **SMSCACHEFLAGS**  

     Configura la carpeta de caché de Configuration Manager, que almacena los archivos temporales. Puede utilizar las propiedades SMSCACHEFLAGS individualmente o en combinación, separadas por punto y coma. Si no se especifica esta propiedad, la carpeta de caché de cliente se instala según la propiedad SMSCACHEDIR, la carpeta no se comprime y se usa el valor SMSCACHESIZE como el tamaño en MB de la carpeta.  

     Especifica otros detalles de la instalación de la carpeta de caché de cliente. Se pueden especificar las siguientes propiedades:  

    -   PERCENTDISKSPACE: especifica el tamaño de la carpeta como un porcentaje del espacio total en disco. Si se especifica esta propiedad, también debe especificar la propiedad SMSCACHESIZE como el valor de porcentaje para usar.  

    -   PERCENTFREEDISKSPACE: especifica el tamaño de la carpeta como un porcentaje del espacio libre en disco. Si se especifica esta propiedad, también debe especificar la propiedad SMSCACHESIZE como el valor de porcentaje para usar. Por ejemplo, si el disco tiene 10 MB de espacio libre y SMSCACHESIZE se especifica como 50, el tamaño de la carpeta se establece en 5 MB. No puede utilizar esta propiedad con la propiedad PERCENTDISKSPACE.  

    -   MAXDRIVE: especifica que la carpeta debe instalarse en el disco disponible más grande. Este valor se omitirá si se especificó una ruta de acceso con la propiedad SMSCACHEDIR.  

    -   MAXDRIVESPACE: especifica que la carpeta debe instalarse en el disco duro que tenga más espacio libre. Este valor se omitirá si se especificó una ruta de acceso con la propiedad SMSCACHEDIR.  

    -   NTFSONLY: especifica que la carpeta puede instalarse solamente en unidades de disco formateadas con el sistema de archivos NTFS. Este valor se omitirá si se especificó una ruta de acceso con la propiedad SMSCACHEDIR.  

    -   COMPRESS: especifica que la carpeta debe mantenerse en un formato comprimido.  

    -   FAILIFNOSPACE: especifica que se debe quitar el software cliente si no hay espacio suficiente para instalar la carpeta.  

    > [!NOTE]  
    >  Se pueden especificar varios valores para esta propiedad mediante la separación de cada uno con punto y coma.  

     Si no se especifica esta propiedad, se creará la carpeta de caché de cliente según la propiedad SMSCACHEDIR, no se comprimirá y tendrá el tamaño especificado en la propiedad SMSCACHESIZE.  

     Ejemplo: **CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS**  

    > [!NOTE]  
    >  Este valor se omite cuando se actualiza un cliente existente.  

-   **SMSCACHESIZE**  

     > [!IMPORTANT]
     > En la versión 1606 de Configuration Manager, hay nuevas opciones de cliente disponibles para especificar el tamaño de la carpeta de caché del cliente. La adición de dichas opciones reemplaza efectivamente el uso de SMSCACHESIZE como propiedad de client.msi para especificar el tamaño de la caché del cliente. Para más información, consulte la [configuración del cliente del tamaño de la caché](about-client-settings.md#client-cache-settings).  

     Para la versión 1602, y las anteriores, SMSCACHESIZE especifica el tamaño de la carpeta de caché de cliente en megabytes (MB) o como un porcentaje cuando se utiliza con la propiedad PERCENTDISKSPACE o PERCENTFREEDISKSPACE. Si no se establece esta propiedad, el tamaño máximo predeterminado de la carpeta será de 5120 MB. El valor más bajo que puede especificar es 1 MB.  

    > [!NOTE]  
    >  Si un nuevo paquete que debe descargarse va a causar que la carpeta supere el tamaño máximo y si la carpeta no se puede purgar para obtener suficiente espacio disponible, se producirá un error en la descarga del paquete y el programa o aplicación no se ejecutará.  

     Este valor se omite cuando se actualiza un cliente existente y cuando el cliente descarga las actualizaciones de software.  

     Ejemplo: **CCMSetup.exe SMSCACHESIZE=100**  

    > [!NOTE]  
    >  Si se vuelve a instalar un cliente, no puede utilizar las propiedades de instalación SMSCACHESIZE o SMSCACHEFLAGS para establecer el tamaño de caché más pequeño de lo que era anteriormente. Si intenta hacerlo, se omite el valor y el tamaño de caché se establece automáticamente en el último tamaño que tenía anteriormente.  
    >   
    >  Por ejemplo, si instala el cliente con el tamaño de caché predeterminado de 5120 MB y, luego, vuelve a instalar el cliente con un tamaño de caché de 100 MB, el tamaño de la carpeta de caché en el cliente reinstalado se establece en 5120 MB.  


-   **SMSCONFIGSOURCE**  

     Especifica la ubicación y el orden en que el instalador de Configuration Manager comprueba si hay valores de configuración. La propiedad es una cadena que contiene uno o más caracteres y que define un origen de configuración específico. Utilice los valores de caracteres R, P, M y U, solos o en combinación, como se muestra en los ejemplos siguientes:  

    -   R: comprueba los valores de configuración en el Registro.  

         Haga clic aquí para obtener [información acerca del almacenamiento de las propiedades de instalación de cliente en el Registro](https://technet.microsoft.com/library/gg712298.aspx#BKMK_Provision).  

    -   P: comprueba los valores de configuración de las propiedades de instalación proporcionados en el símbolo del sistema.  

    -   M: comprueba la configuración existente al actualizar un cliente anterior con el software cliente de Configuration Manager.  

    -   U: actualiza el cliente instalado a una versión más reciente (y utiliza el código de sitio asignado).  

     De forma predeterminada, la instalación del cliente usa `PU` para comprobar, en primer lugar, las propiedades de instalación y, a continuación, la configuración existente.  

     Ejemplo: **CCMSetup.exe SMSCONFIGSOURCE=RP**  

-   **SMSDIRECTORYLOOKUP**  

     Especifica si el cliente puede utilizar el Servicio de nombres Internet de Windows (WINS) para buscar un punto de administración que acepte conexiones HTTP. Los clientes usan este método cuando no encuentran un punto de administración en Servicios de dominio de Active Directory o en DNS.  

     Esta propiedad es independiente de si el cliente utiliza WINS para la resolución de nombres.  

     Puede configurar dos modos diferentes para esta propiedad:  

    -   NOWINS: es la configuración más segura para esta propiedad e impide que los clientes puedan encontrar un punto de administración en WINS.  Cuando use esta opción, los clientes deben tener un método alternativo para buscar un punto de administración en la intranet, como Servicios de dominio de Active Directory o el uso de la publicación en DNS.  

    -   WINSSECURE: en este modo, un cliente que utiliza la comunicación HTTP puede utilizar WINS para buscar un punto de administración. Sin embargo, el cliente debe tener una copia de la clave raíz confiable antes de que pueda conectarse correctamente al punto de administración. Para más enformación, vea [Planneng for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) en [Plan for security en System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

     Si no se especifica esta propiedad, se utiliza el valor predeterminado de WINSSECURE.  

     Ejemplo: **CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS**  

-   **SMSSIGNCERT**  

     Especifica el nombre de archivo .cer y la ruta de acceso completa del certificado autofirmado exportado en el servidor del sitio.  

     Este certificado se almacena en el almacén de certificados **SMS** ; su nombre de sujeto es **Servidor del sitio** y su nombre descriptivo es **Certificado de firma de servidor de sitio**.  

     Ejemplo: **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;Ruta de acceso completa y nombre de archivo\>**  

-   **SMSMP**  

     Especifica un punto de administración inicial para que lo use el cliente de Configuration Manager.  

    > [!IMPORTANT]  
    >  Si el punto de administración solo acepta conexiones de cliente a través de HTTPS (no permite conexiones de cliente HTTP), se debe anteponer al nombre del punto de administración el valor https://.  

     Ejemplo: **CCMSetup.exe SMSMP=smsmp01.contoso.com**  

     Ejemplo: **CCMSetup.exe SMSMP=smsmp01.contoso.com**  

     Ejemplo: **CCMSetup.exe SMSMP=https://smsmp01.contoso.com**  

-   **SMSSITECODE**  

     Especifica el sitio de Configuration Manager al que se va a asignar el cliente de Configuration Manager. Este puede ser un código de sitio de tres caracteres o la palabra AUTO. Si esta propiedad no se especifica o se especifica AUTO, el cliente intenta determinar su asignación de sitio de Configuration Manager desde Servicios de dominio de Active Directory o desde un punto de administración especificado.  

    > [!NOTE]  
    >  No utilice AUTO si también se especifica el punto de administración basado en Internet (CCMHOSTNAME). En este caso, debe asignar directamente el cliente a su sitio.  

     Ejemplo: **CCMSetup.exe SMSSITECODE=XZY**  

-   **CCMINSTALLDIR**  

     Identifica la carpeta en la que se instalan los archivos de cliente de Configuration Manager. Si no se establece esta propiedad, el software cliente se instala en la carpeta *%Windir%*\CCM. Independientemente de la ubicación de instalación de estos archivos, el archivo Ccmcore.dll siempre se instala en la carpeta *%Windir%\System32* . Además, en sistemas operativos de 64 bits, siempre se instala una copia del archivo Ccmcore.dll en la carpeta *%Windir%*\SysWOW64 para admitir aplicaciones de 32 bits que usan la versión de 32 bits de las API de cliente de Configuration Manager del kit de desarrollo de software (SDK) de Configuration Manager.  

     Ejemplo: **CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"**  

-   CCMADMINS  

     Especifica la concesión del acceso de una o más cuentas o grupos de usuarios de Windows a directivas y configuraciones de cliente. Es especialmente útil si el administrador de Configuration Manager no tiene credenciales administrativas locales en el equipo cliente. Puede especificar una lista de cuentas separadas por punto y coma.  

     Ejemplo: **CCMSetup.exe CCMADMINS="Dominio\Cuenta1;Dominio\Grupo1"**  

-   **FSP**  

     Especifica el punto de estado de reserva que recibe y procesa los mensajes de estado enviados por los equipos cliente de Configuration Manager.  

     Para más información acerca del punto de estado de reserva, consulte la sección [Determinar si necesita un punto de estado de reserva](plan/determine-the-site-system-roles-for-clients.md#BKMK_Determine_FSP) de [Determinar los roles de sistema de sitio para System Center Configuration Manager](plan/determine-the-site-system-roles-for-clients.md).  

     Ejemplo: **CCMSetup.exe FSP=SMSFP01**  

-   **DNSSUFFIX**  

     Especifica un dominio DNS para que los clientes localicen puntos de administración que se publican en DNS. Cuando se encuentra un punto de administración, informa al cliente sobre otros puntos de administración en la jerarquía. Esto significa que el punto de administración que se encuentra mediante la publicación de DNS no tiene que ser del sitio del cliente, pero puede ser cualquier punto de administración de la jerarquía.  

    > [!NOTE]  
    >  No es necesario especificar esta propiedad si el cliente está en el mismo dominio que un punto de administración publicado. En este escenario, el dominio del cliente se utiliza automáticamente para buscar los puntos de administración en DNS.  

     Para obtener más información sobre la publicación de DNS como método de ubicación del servicio de clientes de Configuration Manager, consulte la sección [Service Location and how clients determine their assigned management point](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location) (Ubicación del servicio y cómo los clientes averiguan su punto de administración asignado) del tema [Understand how clients find site resources and services for System Center Configuration Manager](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) (Comprender cómo los clientes buscan servicios y recursos de sitio para System Center Configuration Manager).  

    > [!NOTE]  
    >  De forma predeterminada, la publicación en DNS no está habilitada en Configuration Manager.  

     Ejemplo: **CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com**  

-   **CCMEVALINTERVAL**  

     Especifica la frecuencia con la que se ejecuta la herramienta de evaluación de estado de cliente (ccmeval.exe). Puede especificar un valor de entre **1** y **1440** minutos. Si no se especifica esta propiedad o si especifica un valor incorrecto, la evaluación se ejecutará una vez al día.  

-   **CCMEVALHOUR**  

     Especifica la hora a la que se ejecuta la herramienta de evaluación de estado de cliente (ccmeval.exe). Puede especificar un valor comprendido entre **0** (medianoche) y **23** (11 p.m.). Si no se especifica esta propiedad o si especifica un valor incorrecto, la evaluación se ejecutará a las doce de la noche.  

-   **IGNOREAPPVVERSIONCHECK**  

     Especifica que no se comprueba la existencia de la versión mínima necesaria de Microsoft Application Virtualization (App-V) antes de instalar el cliente.  

    > [!IMPORTANT]  
    >  Si se instala el cliente de Configuration Manager sin instalar App-V, no se pueden implementar aplicaciones virtuales.  

     Ejemplo: **CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE**  

-   **NOTIFYONLY**  

     Especifica que no se solucionarán los problemas del cliente de Configuration Manager, pero se notificará el estado del mismo.  

     Ejemplo: **CCMSetup.exe NOTIFYONLY=TRUE**  

     Para más información, vea [Cómo configurar el estado de cliente en System Center Configuration Manager](configure-client-status.md).  

##  <a name="a-namebkmkattributevaluesa-supported-attribute-values-for-the-pki-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a> Valores de atributos admitidos para los criterios de selección de certificado PKI  
 Configuration Manager admite los siguientes valores de atributos para los criterios de selección de certificado PKI:  

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



<!--HONumber=Nov16_HO1-->


