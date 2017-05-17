---
title: "Configurar puerta de enlace de administración en la nube | Microsoft Docs"
description: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 05/01/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.translationtype: Human Translation
ms.sourcegitcommit: d5a6fdc9a526c4fc3a9027dcedf1dd66a6fff5a7
ms.openlocfilehash: 97e1bc6585cee0ff433da0ec0b60b9604cb7348f
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017

---

# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurar puerta de enlace de administración en la nube para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

A partir de la versión 1610, el proceso para configurar la puerta de enlace de administración en la nube en Configuration Manager incluye los pasos siguientes:

## <a name="step-1-configure-required-certificates"></a>Paso 1: Configurar los certificados necesarios

## <a name="option-1-preferred---use-the-server-authentication-certificate-from-a-public-and-globally-trusted-certificate-provider-like-verisign"></a>Opción 1 (preferida): Usar el certificado de autenticación de servidor de un proveedor de certificados público y de confianza global (como VeriSign)

Cuando use este método, los clientes confiarán automáticamente en el certificado y no tendrá que crear un certificado SSL personalizado usted mismo.

1. Cree un registro de nombre canónico (CNAME) en el servicio de nombres de dominio (DNS) público de su organización para crear un alias del servicio Cloud Management Gateway con un nombre descriptivo que se usará en el certificado público.
Por ejemplo, Contoso denomina su servicio Cloud Management Gateway **GraniteFalls** que, en Azure, será **GraniteFalls.CloudApp.Net**. En el DNS espacio de nombres público de Contoso, contoso.com, el administrador de DNS crea un registro CNAME para **GraniteFalls.Contoso.com** con el nombre del host real, **GraniteFalls.CloudApp.net**.
2. Luego, con el nombre común (CN) del alias de CNAME, solicite un certificado de autenticación de servidor de un proveedor público.
Por ejemplo, Contoso usa **GraniteFalls.Contoso.com** como CN del certificado.
3. Cree el servicio Cloud Management Gateway en la consola de Configuration Manager con este certificado.
    - En la página **Configuración** del Asistente para crear una instancia de Cloud Management Gateway, cuando agregue el certificado de servidor de este servicio en la nube (en **Archivo de certificado**), el asistente extraerá el nombre de host del CN de certificado como nombre del servicio y lo agregará a **cloudapp.net** (o a **usgovcloudapp.net** en el caso de la nube Azure Gobierno de EE.UU.) como FQDN de servicio para crear el servicio en Azure.
Por ejemplo, al crear el servicio Cloud Management Gateway en Contoso, se extrae el nombre de host, **GraniteFalls**, del CN de certificado, por lo que el servicio real de Azure se crea como **GraniteFalls.CloudApp.net**.

### <a name="option-2---create-a-custom-ssl-certificate-for-cloud-management-gateway-in-the-same-way-as-for-a-cloud-based-distribution-point"></a>Opción 2: Crear un certificado SSL personalizado para Cloud Management Gateway de la misma manera que se crea para un punto de distribución basado en la nube

Puede crear un certificado SSL personalizado para la puerta de enlace de administración en la nube de la misma manera que si fuera para un punto de distribución basado en la nube. Siga las instrucciones de [Deploying the Service Certificate for Cloud-Based Distribution Points (Implementación del certificado de servicio para puntos de distribución basados en la nube)](/sccm/core/plan-design/network/example-deployment-of-pki-certificates), pero con las siguientes diferencias:

- Al configurar la plantilla del nuevo certificado, otórguele permisos de **lectura** e **inscripción** en el grupo de seguridad que establezca para los servidores de Configuration Manager.
- Cuando se le solicite el certificado de servidor web personalizado, proporcione un nombre de dominio completo para el nombre común del certificado que finalice en**cloudapp.net** para usar la puerta de enlace de administración en la nube en la nube pública de Azure o **usgovcloudapp.net** para la nube de administración pública de Azure.


## <a name="step-2-export-the-client-certificates-root"></a>Paso 2: Exportar la raíz del certificado de cliente

La manera más sencilla de exportar la raíz de los certificados de cliente usados en la red es abrir un certificado de cliente en uno de los equipos unidos a dominio que tenga uno y copiarlo.

> [!NOTE] 
>
> Los certificados de cliente son necesarios en cualquier equipo que desee administrar con la puerta de enlace de administración en la nube y en el servidor de sistema de sitio que hospeda el punto de conexión de la puerta de enlace de administración en la nube. Si necesita agregar un certificado de cliente a cualquiera de estas máquinas, vea [Deploying the Client Certificate for Windows Computers (Implementación del certificado de cliente para equipos Windows)](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).

1.  En la ventana Ejecutar, escriba **mmc** y presione ENTRAR.

2.  En el menú Archivo, elija **Agrear o quitar complemento...**.

3.  En el cuadro de diálogo Agregar o quitar complemento, elija **Certificados** > **Agregar &gt;** > **Cuenta de equipo** > **Siguiente** > **Equipo local** > **Finalizar**. 

4.  Vaya a **Certificados** &gt; **Personal** &gt; **Certificados**.

5.  Haga doble clic en el certificado para la autenticación de cliente en el equipo, elija la pestaña Ruta de certificación y haga doble clic en la entidad de certificación raíz (al principio de la ruta de acceso).

6.  En la pestaña Detalles, elija **Copiar en archivo...**.

7.  Complete el Asistente para exportar certificados con el formato de certificado predeterminado. Anote el nombre y la ubicación del certificado raíz que ha creado, ya que lo necesitará para configurar la puerta de enlace de administración en la nube en un [paso posterior](#step-4-set-up-cloud-management-gateway).

## <a name="step-3-upload-the-management-certificate-to-azure"></a>Paso 3: Cargar el certificado de administración en Azure

Se necesita un certificado de administración de Azure para que Configuration Manager tenga acceso a la API de Azure y para configurar la puerta de enlace de administración en la nube. Para obtener más información e instrucciones sobre cómo cargar un certificado de administración, vea los artículos siguientes de la documentación de Azure:

- [Introducción a los certificados para los servicios en la nube de Azure](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)

- [Carga de un certificado de administración de API de administración de Azure](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)

>[!IMPORTANT]
>Asegúrese de copiar el identificador de suscripción asociado al certificado de administración, ya que lo necesitará para configurar la puerta de enlace de administración en la nube en la consola de Configuration Manager en el [paso siguiente](#step-4-set-up-cloud-management-gateway).

### <a name="subordinate-ca-certificates-and-azure"></a>Certificados de entidad de certificación subordinada y Azure

Si el certificado lo emite una entidad de certificación subordinada y la infraestructura de clave pública de la organización no está en Internet, use este procedimiento para cargar el certificado en Azure. 

1. En el portal de Azure, después de configurar una puerta de enlace de administración en la nube, ubique el servicio de puerta de enlace de administración en la nube y vaya a la pestaña **Certificado**. Suba aquí sus certificados de entidad de certificación subordinada. Si tiene más de un certificado de entidad de certificación subordinada, debe cargarlos todos. 
2. Una vez que se cargue el certificado, registre su huella digital. 
3. Agregue la huella digital a la base de datos del sitio con este script:
    
```

    DIM serviceCName
    DIM subCAThumbprints

    ' Verify arguments
    IF WScript.Arguments.Count <> 2 THEN
    WScript.StdOut.WriteLine "Usage: CScript UpdateSubCAThumbprints.vbs <ServiceCName> <SubCA cert thumbprints, separated by ;>"
    WScript.Quit 1
    END IF

    'Get arguments
    serviceCName = WScript.Arguments.Item(0)
    subCAThumbprints = WScript.Arguments.Item(1)

    'Find SMS Provider
    WScript.StdOut.WriteLine "Searching for SMS Provider for local site..."
    SET objSMSNamespace = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms")
    SET results = objSMSNamespace.ExecQuery("SELECT * From SMS_ProviderLocation WHERE ProviderForLocalSite = true")

    'Process the results
    FOR EACH var in results
    siteCode = var.SiteCode
    NEXT

    IF siteCode = "" THEN
    WScript.StdOut.WriteLine "Failed to locate SMS provider."
    WScript.Quit 1
    END IF

    WScript.StdOut.WriteLine "SiteCode = " & siteCode 

    ' Connect to the SMS namespace
    SET objWMIService = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms\site_" & siteCode)

    'Get instance of SMS_AzureService
    DIM query
    query = "SELECT * From SMS_AzureService WHERE ServiceType = 'CloudProxyService' AND ServiceCName = '" & serviceCName & "'"
    WScript.StdOut.WriteLine "Run WQL query: " &  query
    SET objInstances = objWMIService.ExecQuery(query)

    IF IsNull(objInstances) OR (objInstances.Count = 0) THEN
    WScript.StdOut.WriteLine "Failed to get Azure_Service instance."
    WScript.Quit 1
    END IF

    FOR EACH var IN objInstances
    SET azService = var
    NEXT

    WScript.StdOut.WriteLine "Update [SubCACertThumbprint] to " & subCAThumbprints

    'Update SubCA cert thumbprints
    azService.Properties_.item("SubCACertThumbprint") = subCAThumbprints

    'Save data back to provider
    azService.Put_

    WScript.StdOut.WriteLine "[SubCACertThumbprint] is updated successfully."
```


## <a name="step-4-set-up-cloud-management-gateway"></a>Paso 4: Configurar puerta de enlace de administración en la nube

>[!NOTE]
>En la versión 1610, la puerta de enlace de administración en la nube es una característica de versión preliminar. Para habilitarla, consulte [Use pre-release features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease) (Uso de características de la versión preliminar a partir de las actualizaciones).

1. En la consola de Configuration Manager, vaya a **Administración** > **Servicios en la nube** > **Puerta de enlace de administración en la nube**.
2. Elija **Crear puerta de enlace de administración en la nube**.

3. En el Asistente para crear puerta de enlace de administración en la nube, escriba el identificador de suscripción de Azure (copiado desde el portal de administración de Azure) y busque el archivo de certificado que usó para cargarlo como un certificado de administración de Azure. Elija **Siguiente** y, luego, espere unos instantes mientras que la consola se conecta a Azure.

4. Rellene los detalles adicionales en el asistente:

    - Especifique el nombre del servicio que se ejecutará en Azure. El nombre del servicio solo puede incluir caracteres alfanuméricos y debe tener entre 3 y 24 caracteres.

    - Elija la región de Azure en la que desea que se ejecute el servicio.

    - Especifique el número de máquinas virtuales que desee usar para el servicio. El valor predeterminado es 1, pero puede ejecutar hasta 16 máquinas virtuales para el servicio.

    >[!NOTE]
    >Si usa un proxy de Internet para el punto de conexión de puerta de enlace de administración en la nube, necesita aumentar el número de puertos en el proxy en función del número de máquinas virtuales que usa, a partir del puerto 10124.

    - Especifique la clave privada (archivo .pfx) que ha exportado desde el certificado SSL personalizado.

    - Especifique el certificado raíz exportado desde el certificado de cliente.

    -   Especifique el mismo FQDN de servicio que usó cuando creó la nueva plantilla de certificado. Debe especificar uno de los siguientes sufijos para el nombre de servicio de nombre de dominio completo en función de la nube de Azure que usa:

    Nube de Azure | Prefijo de nombre de dominio completo
    --------------|-------------
    Nube pública (comercial) | .cloudapp.net    
    Nube de administración pública | .usgovcloudapp.net

  - Desactive la casilla situada junto a **Comprobar revocación de certificado de cliente** (a menos que vaya a publicar la información de CRL públicamente).

  - Elija **Siguiente** cuando termine.

5. Si desea administrar el tráfico de la puerta de enlace de administración en la nube con un umbral de 14 días, elija la casilla para activar la alerta de umbral. Luego, especifique el umbral y el porcentaje en que desea elevar los distintos niveles de alerta. Elija **Siguiente** cuando termine.

6. Revise la configuración y elija **Siguiente**. Configuration Manager comienza a configurar el servicio. Cuando cierre el asistente, llevará entre 5 y 15 minutos aprovisionar por completo el servicio en Azure. Compruebe la columna **Estado** de la puerta de enlace de administración en la nube recién configurada para determinar si el servicio está listo.

## <a name="step-5-configure-primary-site-for-client-certification-authentication"></a>Paso 5: Configurar un sitio primario para la autenticación de certificados de cliente

1. En la consola de Configuration Manager, vaya a **Administración** > **Configuración de sitio** > **Sitios**.

2. Seleccione el sitio primario de los clientes que desea administrar mediante la puerta de enlace de administración en la nube y elija **Propiedades**.

3. En la pestaña Comunicaciones de equipo cliente de la hoja de propiedades del sitio primario, active la casilla **Usar un certificado de cliente PKI (capacidad de autenticación de cliente) cuando esté disponible**.

4. Asegúrese de desactivar la opción **Los clientes comprueban la lista de revocación de certificados (CRL) para sistemas de sitio**. Esta opción solo sería necesaria si fuera a publicar la CRL públicamente.


## <a name="step-6-add-the-cloud-management-gateway-connector-point"></a>Paso 6: Agregar el punto de conexión de puerta de enlace de administración en la nube

El punto de conexión de puerta de enlace de administración en la nube es un rol de sistema de sitio nuevo para comunicarse con la puerta de enlace de administración en la nube. Para agregar el punto de conexión de puerta de enlace de administración en la nube, siga las instrucciones de [Agregar roles de sistema de sitio para System Center Configuration Manager](/sccm/core/servers/deploy/configure/add-site-system-roles).

## <a name="step-7-configure-roles-for-cloud-management-gateway-traffic"></a>Paso 7: Configurar roles para el tráfico de puerta de enlace de administración en la nube

El último paso de la configuración de la puerta de enlace de administración en la nube es configurar los roles de sistema de sitio para que acepten tráfico de la puerta de enlace de administración en la nube. En Tech Preview 1606, solo son compatibles con la puerta de enlace de administración en la nube los roles de punto de administración, punto de distribución y punto de actualización de software. Debe configurar cada rol por separado.

1. En la consola de Configuration Manager, vaya a **Administración** > **Configuración de sitio** > **Servidores y roles del sistema de sitios**.

2. Elija el servidor de sistema de sitio del rol que desea configurar para el tráfico de la puerta de enlace de administración en la nube.

3. Elija el rol y, luego, elija **Propiedades**.

4. En la hoja Propiedades del rol, en Conexiones de cliente, elija **HTTPS**, active la casilla situada junto a **Permitir el tráfico de puerta de enlace de administración en la nube de Configuration Manager** y, luego, elija **Aceptar**. Repita estos pasos para los roles restantes.

## <a name="step-8-configure-clients-for-cloud-management-gateway"></a>Paso 8: Configurar clientes para la puerta de enlace de administración en la nube

Una vez que los roles de sistema de sitio y puerta de enlace de administración en la nube están completamente configurados y en ejecución, los clientes obtendrán automáticamente la ubicación del servicio de puerta de enlace de administración en la nube en la siguiente solicitud de ubicación. Los clientes deben encontrarse en la red corporativa para recibir la ubicación del servicio de puerta de enlace de administración en la nube. El ciclo de sondeo de las solicitudes de ubicación es cada 24 horas. Si no quiere esperar a la solicitud de ubicación normalmente programada, puede forzar la solicitud si reinicia el servicio Host de agente de SMS (ccmexec.exe) en el equipo.

Con la ubicación del servicio de puerta de enlace de administración en la nube configurada en el cliente, puede determinar automáticamente si se encuentra en la intranet o en Internet. Si el cliente puede ponerse en contacto con el controlador de dominio o con el punto de administración local, lo usará para comunicarse con Configuration Manager. De lo contrario, considerará que se encuentra en Internet y usará la ubicación del servicio de puerta de enlace de administración en la nube para comunicarse.

>[!NOTE]
> Puede forzar a un cliente para que siempre use la puerta de enlace de administración en la nube independientemente de si se encuentra en la intranet o en Internet. Para ello, debe establecer la siguiente clave de registro en el equipo cliente:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`

Para comprobar que los clientes se pueden poner en contacto con Configuration Manager, puede ejecutar el comando de PowerShell siguiente en el equipo cliente:

`gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate`

Este comando muestra los puntos de administración con los que puede ponerse en contacto el cliente, incluido el servicio de puerta de enlace de administración en la nube.

## <a name="next-steps"></a>Pasos siguientes

[Supervisar clientes para la puerta de enlace de administración en la nube](monitor-clients-cloud-management-gateway.md)

