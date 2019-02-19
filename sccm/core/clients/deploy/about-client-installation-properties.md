---
title: Parámetros y propiedades de instalación de cliente
titleSuffix: Configuration Manager
description: Obtenga información sobre los parámetros y propiedades de la línea de comandos de ccmsetup para instalar el cliente de Configuration Manager.
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ebfcde2be230c9c5e04031210cb6e137ed81668c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126497"
---
# <a name="about-client-installation-parameters-and-properties-in-system-center-configuration-manager"></a>Acerca de los parámetros y propiedades de instalación de cliente en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use el comando CCMSetup.exe para instalar el cliente de Configuration Manager. Si proporciona parámetros de instalación de cliente en la línea de comandos, modificarán el comportamiento de la instalación. Si proporciona propiedades de instalación de cliente en la línea de comandos, modificarán la configuración inicial del agente cliente instalado.



##  <a name="aboutCCMSetup"></a> Acerca de CCMSetup.exe  
 El comando CCMSetup.exe descarga los archivos necesarios para instalar el cliente desde un punto de administración o una ubicación de origen. Es posible que estos archivos incluyan:  

-   El paquete de Windows Installer client.msi que instala el software cliente.  

-   Archivos de instalación del Servicio de transferencia inteligente en segundo plano (BITS).  

-   Archivos de instalación de Windows Installer.  

-   Actualizaciones y correcciones para el cliente de Configuration Manager.  

> [!NOTE]  
>  En Configuration Manager no se puede ejecutar el archivo client.msi directamente.  

 CCMSetup.exe proporciona [parámetros de línea de comandos](#ccmsetup-exe-command-line-parameters) para personalizar la instalación (a los parámetros se les agrega como prefijo una barra diagonal inversa y, por convención, van en minúsculas). Puede especificar el valor de un parámetro en caso necesario mediante el uso de dos puntos inmediatamente seguidos del valor deseado. También puede proporcionar propiedades para modificar el comportamiento de client.msi en la línea de comandos de CCMSetup.exe (las propiedades, por convención, van todas en mayúsculas). Puede especificar un valor para una propiedad mediante el uso de un signo igual inmediatamente seguido del valor deseado.  

> [!IMPORTANT]  
>  Especifique los parámetros de CCMSetup antes de especificar propiedades para client.msi.  

 CCMSetup.exe y los archivos auxiliares se encuentran en el servidor de sitio en la carpeta **Client** de la carpeta de instalación de Configuration Manager. Esta carpeta se comparte en la red como **&lt;Nombre del servidor de sitio\>\SMS_&lt;Código de sitio\>\Cliente**.  

 En el símbolo del sistema, el comando CCMSetup.exe utiliza el formato siguiente:  

 `CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

 Por ejemplo:  

   `CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

 Este ejemplo hace lo siguiente:  

-   Especifica al punto de administración denominado SMSMP01 que solicite una lista de puntos de distribución para descargar los archivos de instalación de cliente.  

-   Especifica que la instalación debe detenerse si ya existe una versión del cliente en el equipo.  

-   Indica a client.msi que asigne el cliente al código del sitio S01.  

-   Indica a client.msi que use el punto de estado de reserva denominado SMSFP01.  

> [!NOTE]  
>  Si un valor de parámetro tiene espacios, póngalo entre comillas.  


> [!IMPORTANT]  
>  Si ha ampliado el esquema de Active Directory para Configuration Manager, el sitio publica muchas propiedades de instalación de cliente en Active Directory Domain Services. El cliente de Configuration Manager lee dichas propiedades automáticamente. Para obtener más información, vea [Acerca de las propiedades de instalación de cliente publicadas en Active Directory Domain Services](about-client-installation-properties-published-to-active-directory-domain-services.md).  



##  <a name="ccmsetupexe-command-line-parameters"></a>Parámetros de línea de comandos de CCMSetup.exe  

### <a name=""></a>/?  

Abre el cuadro de diálogo **CCMSetup** que muestra los parámetros de línea de comandos para ccmsetup.exe.  

Ejemplo: **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;Ruta de acceso\>  

 Especifica la ubicación de descarga de archivos. Use una ruta de acceso local o UNC. Los archivos se descargan mediante el protocolo de bloque de mensajes del servidor (SMB). Para usar **/source**, la cuenta de usuario de Windows para la instalación de cliente debe tener permisos de lectura para la ubicación.

> [!NOTE]  
>  Puede usar el parámetro **/source** más de una vez en una línea de comandos para especificar ubicaciones de descarga alternativas.  

 Ejemplo: **ccmsetup.exe /source:"\\\computer\folder"**  

### <a name="mpltserver"></a>/mp:&lt;Server\>

 Especifica un punto de administración de origen al que se van a conectar los equipos. Los equipos usan dicho punto de administración para encontrar el punto de distribución más cercano para los archivos de instalación. Si no hay ningún punto de distribución o los equipos no pueden descargar los archivos desde los puntos de distribución después de cuatro horas, descargan los archivos desde el punto de administración especificado.  

> [!IMPORTANT]  
>  Este parámetro se usa para especificar un punto de administración inicial para que los equipos busquen un origen de descarga, y puede ser cualquier punto de administración en cualquier sitio. No *asigna* el cliente a un punto de administración.   

 Los equipos descargan los archivos a través de una conexión HTTP o HTTPS, dependiendo de la configuración del rol de sistema de sitio para las conexiones de cliente. La descarga usa limitación de BITS, si está configurada. Si todos los puntos de distribución y puntos de administración están configurados solo para conexiones cliente HTTPS, compruebe que el equipo cliente tenga un certificado de cliente válido.  

Puede usar el parámetro de línea de comandos **/mp** para especificar más de un punto de administración. Si el equipo no puede conectarse al primero, prueba con el siguiente de la lista especificada. Cuando especifique varios puntos de administración, separe los valores con puntos y comas.

Si el cliente se conecta a un punto de administración mediante HTTPS, por lo general, debe especificar el FQDN, no el nombre del equipo. El valor debe coincidir con el nombre del firmante o el nombre alternativo del firmante del certificado PKI del punto de administración. Aunque Configuration Manager admita el uso de un nombre de equipo en el certificado para conexiones en la intranet, se recomienda el uso de un FQDN.

Ejemplo con el nombre de equipo: `ccmsetup.exe /mp:SMSMP01`  

Ejemplo con el nombre de dominio completo (FQDN): `ccmsetup.exe /mp:smsmp01.contoso.com`  

Este parámetro puede especificar la dirección URL de una instancia de Cloud Management Gateway. Use esta dirección URL para instalar el cliente en un dispositivo basado en Internet. Para obtener el valor de este parámetro, siga los pasos siguientes:
- Cree una instancia de Cloud Management Gateway.
- En un cliente activo, abra un símbolo del sistema de Windows PowerShell como administrador. 
- Ejecute el comando siguiente: `(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`.
- Anexe el prefijo "https://" para usarlo con el parámetro **/mp**.

Ejemplo para cuando use la dirección URL de la instancia de Cloud Management Gateway: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`.

 > [!Important]
 > Cuando especifique la dirección URL de una instancia de Cloud Management Gateway para el parámetro **/mp**, debe comenzar con **https://**.


### <a name="retryltminutes"></a>/retry:&lt;Minutos\>

El intervalo de reintentos si CCMSetup.exe no puede descargar los archivos de instalación. CCMSetup continúa intentándolo hasta que alcanza el límite especificado en el parámetro **downloadtimeout**.  

Ejemplo: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Impide que CCMSetup se ejecute como un servicio, que es el valor predeterminado. Cuando CCMSetup se ejecuta como un servicio, se ejecuta en el contexto de la cuenta de sistema local del equipo. Esta cuenta podría no disponer de los derechos suficientes para tener acceso a los recursos de red necesarios para la instalación. Con **/noservice**, CCMSetup.exe se ejecuta en el contexto de la cuenta de usuario usada para iniciar la instalación. Además, si usa un script para ejecutar CCMSetup.exe con el parámetro **/service**, CCMSetup.exe se cierra después del inicio del servicio y es posible que no proporcione los detalles de la instalación correctamente.   

Ejemplo: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Especifica que CCMSetup debe ejecutarse como un servicio que utiliza la cuenta de sistema local.  

Ejemplo: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Especifica que el software cliente se debe desinstalar. Para obtener más información, vea [Cómo administrar clientes](../manage/manage-clients.md).  

Ejemplo: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Si ya hay instalada una versión del cliente, este parámetro especifica que la instalación del cliente debe detenerse.  

Ejemplo: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

 Especifica que CCMSetup debe exigir que el equipo cliente se reinicie si es necesario para completar la instalación. Si no se especifica este parámetro, CCMSetup se cierra cuando es necesario reiniciar. Después, continúa tras el siguiente reinicio manual.  

 Ejemplo: `CCMSetup.exe /forcereboot`  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;Prioridad\>

 Especifica la prioridad de descarga cuando se descargan los archivos de instalación del cliente mediante una conexión HTTP. Los valores posibles son:  

- FOREGROUND  

- HIGH  

- NORMAL  

- LOW  

  El valor predeterminado es NORMAL.  

  Ejemplo: `ccmsetup.exe /BITSPriority:HIGH`  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;Minutos\>

Tiempo en minutos que CCMSetup intenta descargar los archivos de instalación del cliente antes de detenerse. El valor predeterminado es **1440** minutos (un día).  

Ejemplo: `ccmsetup.exe /downloadtimeout:100`  

### <a name="usepkicert"></a>/UsePKICert

Cuando se especifica, el cliente usa un certificado PKI que incluye autenticación de cliente, si está disponible. Si el cliente no encuentra un certificado válido, usa una conexión HTTP con un certificado autofirmado. Este comportamiento es el mismo si no se usa este parámetro.

> [!NOTE]  
>  En algunos escenarios no es necesario especificar este parámetro cuando se va a instalar un cliente y se sigue usando un certificado de cliente. Estos escenarios incluyen la instalación de un cliente mediante la instalación de cliente basada en punto de actualización de software y la instalación de inserción de cliente. No obstante, debe especificar este parámetro siempre que instale manualmente un cliente y use el parámetro **/mp** para especificar un punto de administración configurado para aceptar únicamente conexiones cliente HTTPS. También debe especificar este parámetro cuando se instala un cliente para comunicarse solo a través de Internet. Use la propiedad CCMALWAYSINF=1 junto con las propiedades para el punto de administración basado en Internet (CCMHOSTNAME) y el código de sitio (SMSSITECODE). Para obtener más información sobre la administración de clientes basada en Internet, vea [Consideraciones sobre las comunicaciones de cliente desde Internet o desde un bosque que no es de confianza](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

 Ejemplo: `CCMSetup.exe /UsePKICert`  

### <a name="nocrlcheck"></a>/NoCRLCheck

 Especifica que un cliente no debe comprobar la lista de revocación de certificados (CRL) cuando se comunica a través de HTTPS con un certificado PKI.  

 Cuando no se especifica, el cliente comprueba la CRL antes de establecer una conexión HTTPS.  

 Para obtener más información sobre la comprobación de CRL de cliente, vea [Planear la revocación de certificados PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).  

 Ejemplo: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="configltconfiguration-file"></a>/config:&lt;archivo de configuración\>

Especifica el nombre de un archivo de texto que enumera las propiedades de la instalación de cliente.

- Si no especifica el parámetro **/noservice** de CCMSetup, este archivo debe encontrarse en la carpeta de CCMSetup, que es %Windir%\\Ccmsetup en sistemas operativos de 32 y 64 bits.
- Si se especifica el parámetro **/noservice**, este archivo debe estar en la misma carpeta desde la que se ejecuta CCMSetup.exe.  

Ejemplo: `CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

Para proporcionar el formato de archivo correcto, use el archivo mobileclienttemplate.tcf de la carpeta &lt;directorio de Configuration Manager\>\\bin\\&lt;plataforma\> del servidor de sitio. Este archivo también tiene comentarios sobre las secciones y cómo se usan. Especifique las propiedades de la instalación del cliente en la sección [Instalación de cliente], después del texto siguiente: **Install=INSTALL=ALL**.  

Entrada de la sección [Instalación de cliente] de ejemplo: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;nombre de archivo\>

 Especifica que CCMSetup.exe no debe instalar el programa de requisito previo especificado cuando se instala el cliente de Configuration Manager. Este parámetro admite la entrada de más de un valor. Utilice el carácter de punto y coma (;) para separar cada valor.  


 Ejemplos: `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe` o `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`  

### <a name="forceinstall"></a>/forceinstall

 Especifica que CCMSetup.exe desinstala los clientes existentes e instala un cliente nuevo.  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;característica\>

Especifica que CCMSetup.exe no instala la característica especificada cuando instala el cliente.  

Ejemplo: `CCMSetup.exe /ExcludeFeatures:ClientUI` no instala el Centro de software en el cliente.  

> [!NOTE]  
>  **ClientUI** es el único valor compatible con el parámetro **/ExcludeFeatures**.  



##  <a name="ccmsetupReturnCodes"></a> Códigos de retorno de CCMSetup.exe  
 El comando CCMSetup.exe proporciona los siguientes códigos de retorno cuando se completa. Para solucionar problemas, revise el archivo ccmsetup.log en el equipo cliente para determinar el contexto y los detalles adicionales sobre los códigos de retorno.  

|Código de retorno|Significado|  
|-----------------|-------------|  
|0|Correcto|  
|6|Error|  
|7|Es necesario reiniciar|  
|8|El programa de instalación se está ejecutando|  
|9|Error de evaluación de requisitos previos|  
|10|Error de validación de hash del manifiesto de la instalación|  



## <a name="ccmsetupMsiProps"></a> Propiedades de Ccmsetup.msi  
 Las siguientes propiedades pueden modificar el comportamiento de la instalación de ccmsetup.msi.

### <a name="ccmsetupcmd"></a>CCMSETUPCMD 

Especifica los parámetros y propiedades de línea de comandos que se pasan a ccmsetup.exe después de instalarlo ccmsetup.msi. Incluye otras propiedades entre comillas. Use esta propiedad cuando arranque el cliente de Configuration Manager mediante el método de instalación de MDM de Intune. 

Ejemplo: `ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

 > [!Tip]
 > Microsoft Intune limita la línea de comandos a 1024 caracteres. 



##  <a name="clientMsiProps"></a> Propiedades de Client.msi  
 Las siguientes propiedades pueden modificar el comportamiento de la instalación de client.msi. Si usa el método de instalación de inserción de cliente, también puede especificar las propiedades en la pestaña **Cliente** del cuadro de diálogo **Propiedades de instalación de inserción de cliente** .  


### <a name="aadclientappid"></a>AADCLIENTAPPID

Especifica el identificador de aplicación cliente de Azure Active Directory (Azure AD). La aplicación cliente se crea o importa al [configurar servicios de Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para la administración en la nube. Un administrador de Azure puede obtener el valor de esta propiedad desde Azure Portal. Para obtener más información, vea [Obtención del id. y la clave de autenticación de la aplicación](/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key). Para la propiedad **AADCLIENTAPPID**, este identificador de aplicación es para el tipo de aplicación "Native".

Ejemplo: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`


### <a name="aadresourceuri"></a>AADRESOURCEURI

Especifica el identificador de aplicación de servidor de Azure AD. La aplicación de servidor se crea o importa al [configurar servicios de Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para la administración en la nube. Al crear la aplicación de servidor, en el cuadro de diálogo Crear aplicación de servidor, esta propiedad es el **URI de id. de aplicación**.

Un administrador de Azure puede obtener el valor de esta propiedad desde Azure Portal. En la hoja **Azure Active Directory**, busque la aplicación de servidor en **Registros de aplicaciones**. Esta aplicación es de tipo "aplicación web/API". Abra la aplicación, haga clic en **Configuración** y en **Propiedades**. Use el valor del **URI de id. de aplicación** para esta propiedad de instalación de cliente AADRESOURCEURI.

Ejemplo: `ccmsetup.exe AADRESOURCEURI=https://contososerver`


### <a name="aadtenantid"></a>AADTENANTID

Especifica el identificador de inquilino de Azure AD. Este inquilino se vincula a Configuration Manager al [configurar servicios de Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para la administración en la nube. Para obtener el valor de esta propiedad, siga los pasos siguientes:
- En un dispositivo Windows 10 unido al mismo inquilino de Azure AD, abra un símbolo del sistema.
- Ejecute el comando siguiente: `dsregcmd.exe /status`.
- En la sección Estado del dispositivo, busque el valor **TenantId**. Por ejemplo, `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`.

  > [!Note]
  > Un administrador de Azure también puede obtener este valor en Azure Portal. Para obtener más información, vea [Obtención del identificador de inquilino](/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-tenant-id).

Ejemplo: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

Especifica la concesión del acceso de una o más cuentas o grupos de usuarios de Windows a directivas y configuraciones de cliente. Esta propiedad es especialmente útil si el administrador de Configuration Manager no tiene credenciales administrativas locales en el equipo cliente. Especifique una lista de cuentas separadas por punto y coma.  

Ejemplo: `CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Especifica que el equipo puede reiniciarse después de la instalación del cliente si es necesario.  

> [!IMPORTANT]  
>  El equipo se reinicia sin previo aviso, incluso si un usuario ha iniciado sesión.  

Ejemplo: **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 Se establece en **1** para especificar que el cliente siempre está basado en Internet y nunca se conecta a la intranet. El tipo de conexión del cliente muestra **Siempre Internet**.  

 Use esta propiedad junto con CCMHOSTNAME, que especifica el FQDN del punto de administración basado en Internet. Úselo también con el parámetro de CCMSetup /UsePKICert y con el código de sitio.  

 Para obtener más información sobre la administración de clientes basada en Internet, vea [Consideraciones sobre las comunicaciones de cliente desde Internet o desde un bosque que no es de confianza](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

 Ejemplo: `CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 Especifica la lista de emisores de certificados, que es una lista de certificados de entidad de certificación raíz de confianza (CA) en los que confía el sitio de Configuration Manager.  

 Para obtener más información sobre la lista de emisores de certificados y cómo los clientes la usan durante el proceso de selección de certificados, vea [Planear la selección de certificados de cliente PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

 Este valor es una coincidencia de mayúsculas y minúsculas de los atributos del firmante que se encuentran en el certificado de entidad de certificación raíz. Los atributos se pueden separar con una coma (,) o un punto y coma (;). Para especificar más de un certificado de entidad de certificación raíz, use una barra de separación. Ejemplo:  

 `CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &#124; CN=Litware Corporate Root CA; O=Litware, Inc.”`  

> [!TIP]  
>  Para copiar el valor **CertificateIssuers=&lt;string\>** para el sitio, haga referencia al archivo mobileclient.tcf de la carpeta &lt;directorio de Configuration Manager\>\bin\\&lt;plataforma\> del servidor de sitio.  

### <a name="ccmcertsel"></a>CCMCERTSEL

 Especifica los criterios de selección de certificado si el cliente tiene más de un certificado para la comunicación HTTPS. Este certificado es un certificado válido que incluye la capacidad de autenticación de cliente.  

 Puede buscar una coincidencia exacta (use **Subject:**) o una coincidencia parcial (use **SubjectStr:)** en el nombre del firmante o el nombre alternativo del firmante. Ejemplo:  

 `CCMCERTSEL="Subject:computer1.contoso.com"` busca un certificado con una coincidencia exacta con el nombre de equipo "computer1.contoso.com" en el nombre del firmante o en el nombre alternativo del firmante.  

 `CCMCERTSEL="SubjectStr:contoso.com"` busca un certificado que contenga "contoso.com" en el nombre del firmante o en el nombre alternativo del firmante.  

 También puede utilizar los atributos de nombre distintivo (DN) o de identificador de objeto (OID) en los atributos de nombre del firmante o de nombre alternativo del firmante, por ejemplo:  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` busca el atributo de unidad organizativa expresado como un identificador de objeto y con el nombre de Equipos.  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` busca el atributo de unidad organizativa expresado como un nombre distintivo (DN) y con el nombre de Equipos.  

> [!IMPORTANT]
>  Si usa el cuadro Nombre del firmante, **Subject:** distingue mayúsculas de minúsculas y **SubjectStr:** no distingue mayúsculas de minúsculas.  
> 
>  Si usa el cuadro Nombre alternativo del firmante, <strong>Subject:</strong> y **SubjectStr:** no distinguen mayúsculas de minúsculas.  

 La lista completa de atributos que puede usar para la selección de certificados está en [Valores de atributos admitidos para los criterios de selección de certificado PKI](#BKMK_attributevalues).  

 Si más de un certificado coincide con la búsqueda y la propiedad CCMFIRSTCERT está establecida en 1, se selecciona el certificado con el período de validez más largo.  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 Especifica un nombre de almacén de certificados alternativo si el certificado de cliente para HTTPS no se encuentra en el almacén de certificados predeterminado de **Personal** en almacén del equipo.  

 Ejemplo: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  Habilita el registro de depuración. Los valores pueden ser 0 (desactivado, predeterminado) o 1 (activado). Esta propiedad hace que el cliente registre información de bajo nivel para la solución de problemas. Como procedimiento recomendado, evite usar esta propiedad en sitios de producción. Puede producirse un registro excesivo, lo que podría hacer que resultase difícil encontrar información relevante en los archivos de registro. Además, establezca CCMENABLELOGGING en TRUE para habilitar el registro de depuración.  

  Ejemplo: `CCMSetup.exe CCMDEBUGLOGGING=1`  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  De forma predeterminada, esta propiedad está establecida en TRUE para habilitar el registro. Los archivos de registro se almacenan en la carpeta **Logs** de la carpeta de instalación del cliente de Configuration Manager. De forma predeterminada, esta carpeta es % Windir%\CCM\Logs.  

  Ejemplo: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 La frecuencia a la que se ejecuta la herramienta de evaluación de estado de cliente (ccmeval.exe). Puede ser **1** a **1440** minutos. De forma predeterminada, se ejecuta una vez al día.  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 La hora a la que se ejecuta la herramienta de evaluación de estado de cliente (ccmeval.exe), entre **0** (medianoche) y **23** (11 p.m.). Se ejecuta de forma predeterminada a medianoche.  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 Si está establecida en 1, esta propiedad especifica que el cliente debe seleccionar el certificado PKI con el período de validez más largo. Esta configuración puede ser necesaria si usa Protección de acceso a redes con cumplimiento de IPsec.  

 Ejemplo: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  


### <a name="ccmhostname"></a>CCMHOSTNAME

 Si el cliente se administra a través de Internet, esta propiedad especifica el FQDN del punto de administración basado en Internet.  

 No especifique esta opción con la propiedad de instalación SMSSITECODE=AUTO. Los clientes basados en Internet deben asignarse directamente a su sitio basado en Internet.  

 Ejemplo: `CCMSetup.exe  /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

Esta propiedad puede especificar la dirección URL de una instancia de Cloud Management Gateway. Para obtener el valor de esta propiedad, siga los pasos siguientes:
- Cree una instancia de Cloud Management Gateway.
- En un cliente activo, abra un símbolo del sistema de Windows PowerShell como administrador. 
- Ejecute el comando siguiente: `(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`.
- Use el valor devuelto tal cual con la propiedad **CCMHOSTNAME**.

Por ejemplo: `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > Al especificar la dirección de una instancia de Cloud Management Gateway para la propiedad **CCMHOSTNAME**, *no* anexe un prefijo como **https://**. Este prefijo se usa únicamente con la dirección URL **/mp** de una instancia de Cloud Management Gateway.



### <a name="ccmhttpport"></a>CCMHTTPPORT

 Especifica el puerto que el cliente debe usar al comunicarse a través de HTTP con los servidores de sistema de sitio. Se establece en el puerto 80 de forma predeterminada.  

 Ejemplo: `CCMSetup.exe CCMHTTPPORT=80`  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Especifica el puerto que el cliente debe usar al comunicarse a través de HTTPS con los servidores de sistema de sitio. Se establece en el puerto 443 de forma predeterminada.  

Ejemplo: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 Identifica la carpeta en la que se instalan los archivos de cliente de Configuration Manager, de forma predeterminada *%Windir%* \CCM. Independientemente de la ubicación de instalación de estos archivos, el archivo Ccmcore.dll siempre se instala en la carpeta *%Windir%\System32*. Además, en un sistema operativo de 64 bits, siempre se instala una copia del archivo Ccmcore.dll en la carpeta *%Windir%* \SysWOW64. Este archivo es compatible con aplicaciones de 32 bits que usan la versión de 32 bits de las API de cliente del SDK de Configuration Manager.  

 Ejemplo: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Especifica el nivel de detalle que se va a escribir en los archivos de registro de Configuration Manager. Especifique un entero entre 0 y 3, donde 0 es el registro más detallado y 3 solo registra errores. El valor predeterminado es 1.  

Ejemplo: `CCMSetup.exe CCMLOGLEVEL=3`  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Cuando un archivo de registro de Configuration Manager alcanza el tamaño máximo, el cliente le cambia el nombre como si fuera una copia de seguridad y crea un archivo de registro. El tamaño máximo es 250 000 bytes de forma predeterminada, o bien el valor especificado por la propiedad CCMLOGMAXSIZE.

Esta propiedad especifica el número de versiones anteriores del archivo de registro que se van a conservar. El valor predeterminado es 1. Si el valor se establece en 0, no se mantiene ningún archivo de registro antiguo.  

Ejemplo: `CCMSetup.exe CCMLOGMAXHISTORY=0`  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

El tamaño máximo del archivo de registro en bytes. Cuando un registro crece hasta el tamaño especificado, el cliente le cambia el nombre como si fuera un archivo de historial y crea un archivo. Esta propiedad debe establecerse en al menos 10 000 bytes. El valor predeterminado es 250 000 bytes.  

Ejemplo: `CCMSetup.exe CCMLOGMAXSIZE=300000`  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 Si se establece en TRUE, esta propiedad deshabilita la posibilidad de que los usuarios administrativos cambien el sitio asignado en el panel de control de **Configuration Manager**.  

 Ejemplo: **CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Si se establece en TRUE, esta propiedad deshabilita la posibilidad de que los usuarios administrativos cambien la configuración de la carpeta de caché de cliente en el panel de control de **Configuration Manager**.  

Ejemplo: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

 Especifica un dominio DNS para que los clientes localicen puntos de administración que se publican en DNS. Cuando se encuentra un punto de administración, informa al cliente sobre otros puntos de administración en la jerarquía. Este comportamiento significa que el punto de administración que se encuentra mediante la publicación de DNS no tiene que ser del sitio del cliente, sino que puede ser cualquier punto de administración de la jerarquía.  

> [!NOTE]  
>  No es necesario especificar esta propiedad si el cliente está en el mismo dominio que un punto de administración publicado. En este caso, el dominio del cliente se usa automáticamente para buscar los puntos de administración en DNS.  

 Para obtener más información sobre la publicación de DNS como método de ubicación del servicio para clientes de Configuration Manager, vea [Ubicación del servicio y cómo los clientes averiguan su punto de administración asignado](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).  

> [!NOTE]  
>  De forma predeterminada, la publicación en DNS no está habilitada en Configuration Manager.  

 Ejemplo: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### <a name="fsp"></a>FSP

Especifica el punto de estado de reserva que recibe y procesa los mensajes de estado enviados por los equipos cliente de Configuration Manager.  

Para más información sobre el punto de estado de reserva, vea [Determine if you need a fallback status point](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point) (Determinar si necesita un punto de estado de reserva).  

Ejemplo: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 Especifica que no se compruebe la presencia de la versión mínima necesaria de Microsoft Application Virtualization (App-V) antes de instalar el cliente.  

> [!IMPORTANT]  
>  Si se instala el cliente de Configuration Manager sin instalar App-V, no se pueden implementar aplicaciones virtuales.  

 Ejemplo: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### <a name="notifyonly"></a>NOTIFYONLY

Especifica que el cliente informa del estado, pero no soluciona los problemas que encuentre.  

Ejemplo: `CCMSetup.exe NOTIFYONLY=TRUE`  

Para obtener más información, vea [Cómo configurar el estado de cliente](configure-client-status.md).  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 Si un cliente tiene la clave raíz confiable de Configuration Manager errónea y no puede contactar con un punto de administración confiable para recibir la nueva clave raíz confiable, use esta propiedad para quitar manualmente la antigua clave raíz confiable. Esta situación se puede producir cuando se mueve un cliente de una jerarquía de sitio a otra. Esta propiedad se aplica a los clientes que utilizan la comunicación de cliente HTTP y HTTPS.  

 Ejemplo: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Habilita la reasignación de sitio automática para las actualizaciones de cliente cuando se usa con [SMSSITECODE](#smssitecode)=AUTO.

Ejemplo: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Especifica la ubicación de la carpeta de caché de cliente en el equipo cliente, que almacena los archivos temporales. De forma predeterminada, la ubicación es *%Windir%\ccmcache*.  

Ejemplo: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Esta propiedad puede usarse junto con la propiedad SMSCACHEFLAGS para controlar la ubicación de la carpeta de caché de cliente.  

Ejemplo: `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` instala la carpeta de caché de cliente en la unidad de disco de cliente más grande disponible.  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Especifica otros detalles de la instalación de la carpeta de caché de cliente. Puede utilizar las propiedades SMSCACHEFLAGS individualmente o en combinación, separadas por punto y coma. Si no se especifica esta propiedad, la carpeta de caché de cliente se instala según la propiedad SMSCACHEDIR, la carpeta no se comprime y se usa el valor SMSCACHESIZE como el tamaño en MB de la carpeta.  

Este valor se omite cuando se actualiza un cliente existente.  

Propiedades:  

-   PERCENTDISKSPACE: especifica el tamaño de la carpeta como un porcentaje del espacio total en disco. Si se especifica esta propiedad, también debe especificar la propiedad SMSCACHESIZE como el valor de porcentaje para usar.  

-   PERCENTFREEDISKSPACE: especifica el tamaño de la carpeta como un porcentaje del espacio libre en disco. Si se especifica esta propiedad, también debe especificar la propiedad SMSCACHESIZE como el valor de porcentaje para usar. Por ejemplo, si el disco tiene 10 MB de espacio libre y SMSCACHESIZE se especifica como 50, el tamaño de la carpeta se establece en 5 MB. No puede utilizar esta propiedad con la propiedad PERCENTDISKSPACE.  

-   MAXDRIVE: especifica que la carpeta debe instalarse en el disco disponible más grande. Este valor se omite si se ha especificado una ruta de acceso con la propiedad SMSCACHEDIR.  

-   MAXDRIVESPACE: especifica que la carpeta debe instalarse en el disco duro que tenga más espacio libre. Este valor se omite si se ha especificado una ruta de acceso con la propiedad SMSCACHEDIR.  

-   NTFSONLY: especifica que la carpeta puede instalarse solamente en unidades de disco NTFS. Este valor se omite si se ha especificado una ruta de acceso con la propiedad SMSCACHEDIR.  

-   COMPRESS: especifica que la carpeta debe almacenarse en un formato comprimido.  

-   FAILIFNOSPACE: especifica que se debe quitar el software cliente si no hay espacio suficiente para instalar la carpeta.  

Ejemplo: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> Hay opciones de cliente disponibles para especificar el tamaño de la carpeta de caché del cliente. La adición de dichas opciones reemplaza efectivamente el uso de SMSCACHESIZE como propiedad de client.msi para especificar el tamaño de la caché del cliente. Para más información, consulte la [configuración del cliente del tamaño de la caché](about-client-settings.md#client-cache-settings).  

<!-- For 1602 and earlier, SMSCACHESIZE specifies the size of the client cache folder in megabyte (MB) or as a percentage when used with the PERCENTDISKSPACE or PERCENTFREEDISKSPACE property. If this property isn't set, the folder defaults to a maximum size of 5120 MB. The lowest value that you can specify is 1 MB.  -->

> [!NOTE]  
>  Si un nuevo paquete que debe descargarse va a causar que la carpeta supere el tamaño máximo y si la carpeta no se puede purgar para obtener suficiente espacio disponible, se produce un error en la descarga del paquete y el programa o aplicación no se ejecuta.  

Este valor se omite cuando se actualiza un cliente existente y cuando el cliente descarga las actualizaciones de software.  

Ejemplo: `CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  Si vuelve a instalar un cliente, no puede usar las propiedades de instalación SMSCACHESIZE o SMSCACHEFLAGS para establecer el tamaño de caché en un valor inferior al anterior. Si intenta hacerlo, se omitirá el valor. El tamaño de caché se establece automáticamente en el tamaño anterior.  

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Especifica la ubicación y el orden en que el instalador de Configuration Manager comprueba si hay valores de configuración. La propiedad es una cadena de uno o más caracteres, cada uno de los cuales define un origen de configuración específico. Use lo valores de caracteres R, P, M y U, solos o en combinación:  

- R: comprueba los valores de configuración en el Registro.  

  Para obtener más información, vea la [información sobre el almacenamiento de las propiedades de instalación de cliente en el Registro](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

- P: comprueba los valores de configuración de las propiedades de instalación proporcionados en el símbolo del sistema.  

- M: comprueba la configuración existente al actualizar un cliente anterior con el software cliente de Configuration Manager.  

- U: actualiza el cliente instalado a una versión más reciente (y utiliza el código de sitio asignado).  

  De forma predeterminada, la instalación del cliente usa `PU` para comprobar, en primer lugar, las propiedades de instalación y, a continuación, la configuración existente.  

  Ejemplo: `CCMSetup.exe SMSCONFIGSOURCE=RP`  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 Especifica si el cliente puede utilizar el Servicio de nombres Internet de Windows (WINS) para buscar un punto de administración que acepte conexiones HTTP. Los clientes usan este método cuando no encuentran un punto de administración en Active Directory Domain Services o en DNS.  

 Esta propiedad no afecta a si el cliente usa WINS para la resolución de nombres.  

 Puede configurar dos modos diferentes para esta propiedad:  

-   NOWINS: este valor es la configuración más segura para esta propiedad e impide que los clientes puedan encontrar un punto de administración en WINS. Cuando use esta opción, los clientes deben tener un método alternativo para buscar un punto de administración en la intranet, como Servicios de dominio de Active Directory o el uso de la publicación en DNS.  

-   WINSSECURE (valor predeterminado): en este modo, un cliente que utiliza la comunicación HTTP puede utilizar WINS para buscar un punto de administración. Sin embargo, el cliente debe tener una copia de la clave raíz confiable antes de que pueda conectarse correctamente al punto de administración. Para obtener más información, consulte [Planeación de la clave raíz confiable](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  


 Ejemplo: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Especifica un punto de administración inicial para que lo use el cliente de Configuration Manager.  

> [!IMPORTANT]  
>  Si el punto de administración solo acepta conexiones de cliente a través de HTTPS, se debe anteponer https:// al nombre del punto de administración.  

Ejemplo: `CCMSetup.exe SMSMP=smsmp01.contoso.com`

Ejemplo: `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  


### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 Especifica la clave raíz confiable de Configuration Manager cuando no se puede recuperar desde Active Directory Domain Services. Esta propiedad se aplica a los clientes que utilizan la comunicación de cliente HTTP y HTTPS. Para obtener más información, consulte [Planeación de la clave raíz confiable](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 Ejemplo: `CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 Se utiliza para volver a instalar la clave raíz confiable de Configuration Manager. Especifica el nombre y la ruta de acceso completa en un archivo que contiene la clave raíz confiable. Esta propiedad se aplica a los clientes que utilizan la comunicación de cliente HTTP y HTTPS. Para obtener más información, consulte [Planeación de la clave raíz confiable](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 Ejemplo: 'CCMSetup.exe SMSROOTKEYPATH=&lt;Ruta completa y nombre de archivo\>`  

### <a name="smssigncert"></a>SMSSIGNCERT

 Especifica el nombre de archivo .cer y la ruta de acceso completa del certificado autofirmado exportado en el servidor del sitio.  

 Este certificado se almacena en el almacén de certificados **SMS** ; su nombre de sujeto es **Servidor del sitio** y su nombre descriptivo es **Certificado de firma de servidor de sitio**.  

 Ejemplo: **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;ruta completa y nombre de archivo\>**  

### <a name="smssitecode"></a>SMSSITECODE

 Especifica el sitio de Configuration Manager al que se va a asignar el cliente. Este valor puede ser un código de sitio de tres caracteres o la palabra AUTO. Si se especifica AUTO, o si no se especifica esta propiedad, el cliente intenta determinar su asignación de sitio desde Active Directory Domain Services o desde un punto de administración especificado. Para habilitar AUTO para las actualizaciones de cliente, también debe establecer [SITEREASSIGN](#sitereassign) en TRUE.    

> [!NOTE]  
>  No use AUTO si también especifica el punto de administración basado en Internet (CCMHOSTNAME). En ese caso, debe asignar directamente el cliente a su sitio.  

 Ejemplo: `CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> Valores de atributos admitidos para los criterios de selección de certificado PKI  
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
