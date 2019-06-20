---
title: Habilitación de TLS 1.2
titleSuffix: Configuration Manager
description: Información sobre cómo habilitar TLS 1.2 para Configuration Manager.
ms.date: 06/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3d97ee2e68f9f4606ad46c8566467fad459ffa9
ms.sourcegitcommit: 725e1bf7d3250c2b7b7be9da01135517428be7a1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822076"
---
# <a name="how-to-enable-tls-12"></a>Habilitación de TLS 1.2

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se describe cómo habilitar TLS 1.2 para Configuration Manager, incluso para los componentes individuales. En este artículo también se describen los requisitos de actualización de las características más usadas y la solución de algunos problemas comunes.

Configuration Manager se basa en muchos componentes distintos para garantizar una comunicación segura. El protocolo que se usa para una conexión determinada depende de las funcionalidades de todos los componentes requeridos. Si un componente no está actualizado, es posible que la comunicación use un protocolo más antiguo y menos seguro.

Para habilitar correctamente Configuration Manager a fin de admitir TLS 1.2, habilite primero TLS 1.2 para todos los componentes necesarios. Los componentes necesarios dependen del entorno y de las características de Configuration Manager que use.

Inicie este proceso con los clientes, especialmente las versiones anteriores de Windows. Antes de habilitar TLS 1.2 en los servidores de Configuration Manager, asegúrese de que todos los clientes admiten TLS 1.2. En caso contrario, los clientes no podrán comunicarse con los servidores y podrían quedar huérfanos.


## <a name="tasks-for-features-and-scenarios"></a>Tareas para características y escenarios

Para habilitar TLS 1.2 para los componentes de los que depende Configuration Manager para tener una comunicación segura, debe hacer lo siguiente:

- [Habilite el protocolo TLS 1.2 como proveedor de seguridad](#enable-tls-12-protocol-as-a-security-provider)
- [Actualización de .NET Framework para admitir TLS 1.2](#update-net-framework-to-support-tls-12)
- [Actualización de SQL Server y componentes cliente](#update-sql-server-and-client-components)
- [Habilitación de Windows y WinHTTP en Windows 8.0, Windows Server 2012 R2 y versiones anteriores](#update-windows-and-winhttp)
- [Actualización de Windows Server Update Services (WSUS)](#update-windows-server-update-services-wsus)

En esta sección se describen las dependencias para características y escenarios específicos de Configuration Manager. Para determinar los pasos siguientes, busque los elementos que son de aplicación para su entorno.

|Característica o un escenario|Tareas de actualización|
|--- |--- |
|Servidores de sitio (central, principal o secundario)| - [Actualice .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Compruebe la configuración de la criptografía segura.|
|Servidor de base de datos del sitio|[Actualice SQL Server y sus componentes cliente](#update-sql-server-and-client-components).|
|Servidores de sitio secundario|[Actualice SQL Server y sus componentes cliente](#update-sql-server-and-client-components) a una versión compatible de SQL Express.|
|Roles de sistema de sitio| - [Actualice .NET Framework](#update-net-framework-to-support-tls-12) y compruebe la configuración de la criptografía segura. <br/> - [Actualice SQL Server y sus componentes cliente](#update-sql-server-and-client-components) en roles que lo necesitan, como [SQL Server Native Client](#sql-server-native-client).|
|Punto de servicios de informes|- [Actualice .NET Framework](#update-net-framework-to-support-tls-12) en el servidor de sitio, los servidores de SQL Reporting Services y cualquier equipo que tenga la consola.<br/> - Reinicie el servicio SMS_Executive según sea necesario.|
|Punto de actualización de software|[Actualice WSUS](#update-windows-server-update-services-wsus).|
|Consola de Configuration Manager| - [Actualice .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Compruebe la configuración de la criptografía segura.|
|Cliente de Configuration Manager con roles de sistema de sitio HTTPS|[Actualice Windows para admitir TLS 1.2 para las comunicaciones cliente-servidor mediante WinHTTP](#update-windows-and-winhttp).|
|Centro de software| - [Actualice .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Compruebe la configuración de la criptografía segura.|
|Clientes de Windows 7| *Antes* de habilitar TLS 1.2 en cualquier componente del servidor, [actualice Windows para admitir TLS 1.2 para las comunicaciones cliente-servidor mediante WinHTTP](#update-windows-and-winhttp). Si habilita TLS 1.2 en componentes de servidor en primer lugar, puede dejar huérfanas las versiones anteriores de los clientes.|


## <a name="enable-tls-12-protocol-as-a-security-provider"></a>Habilitación del protocolo TLS 1.2 como proveedor de seguridad

Compruebe la configuración de la subclave del Registro `\SecurityProviders\SCHANNEL\Protocols`, tal como se muestra en [Procedimientos recomendados sobre la seguridad de la capa de transporte (TLS) con .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).

> [!NOTE]
> TLS 1.2 está habilitado de manera predeterminada. Por lo tanto, no se requiere modificar estas claves para habilitarlo. Puede realizar cambios en Protocolos para deshabilitar TLS 1.0 y TLS 1.1 después de seguir el resto de las instrucciones de este artículo y de haber comprobado que el entorno funciona sin problemas solo con TLS 1.2 habilitado.


## <a name="update-net-framework-to-support-tls-12"></a>Actualización de .NET Framework para admitir TLS 1.2

### <a name="determine-net-version"></a>Determinación de la versión de .NET

En primer lugar, determine el número de versión de .NET. Para obtener más información, consulte el artículo sobre [cómo determinar qué versiones y niveles de Service Pack de Microsoft .NET Framework están instalados](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

### <a name="install-net-updates"></a>Instalación de actualizaciones de .NET

Algunas versiones de .NET Framework pueden requerir actualizaciones para habilitar la criptografía segura. Use estas instrucciones:

- .NET Framework 4.6.2 y versiones posteriores admite TLS 1.1 y TLS 1.2. Confirme la configuración del Registro, pero no se requiere ningún cambio adicional.

- Actualice .NET Framework 4.6 y versiones anteriores para admitir TLS 1.1 y TLS 1.2. Para obtener más información, vea [Versiones y dependencias de .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- Si usa .NET Framework 4.5.1 o 4.5.2 en Windows 8.1 o Windows Server 2012, las actualizaciones importantes y otros detalles también están disponibles en el [Centro de descarga](https://www.microsoft.com/download/details.aspx?id=42883).

### <a name="configure-for-strong-cryptography"></a>Configuración de la criptografía segura

Configure .NET Framework para admitir criptografía segura. Establezca la configuración `SchUseStrongCrypto` del registro en `DWORD:00000001`. Este valor deshabilita el cifrado de flujo RC4 y requiere reiniciar. Para más información sobre esta configuración, consulte el [aviso de seguridad de Microsoft 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358).

Asegúrese de establecer las siguientes claves del Registro en cualquier equipo que se comunique a través de la red con un sistema habilitado para TLS 1.2. Por ejemplo, los clientes de Configuration Manager, o cualquier rol de sistema de sitio remoto que no esté instalado en el servidor de sitio.

Para las aplicaciones de 32 bits que se ejecutan en sistemas de 32 bits o aplicaciones de 64 bits que se ejecutan en sistemas de 64 bits, actualice el valor de subclave siguiente:

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

En el caso de las aplicaciones de 32 bits que se ejecutan en sistemas de 64 bits, actualice el valor de subclave siguiente:

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> El valor `SchUseStrongCrypto` permite a .NET usar TLS 1.1 y TLS 1.2. El valor `SystemDefaultTlsVersions` permite a .NET usar la configuración del sistema operativo. Para obtener más información, consulte [Procedimientos recomendados sobre la seguridad de la capa de transporte (TLS) con .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls).


## <a name="update-sql-server-and-client-components"></a>Actualización de SQL Server y componentes cliente

Microsoft SQL Server 2016 y versiones posteriores admiten TLS 1.1 y TLS 1.2. Las versiones anteriores y las bibliotecas dependientes pueden requerir actualizaciones. Para más información, consulte [KB 3135244: Compatibilidad con TLS 1.2 para Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

Los servidores de sitio secundario deben usar al menos SQL Server 2016 Express con Service Pack 2 (13.2.50.26) o posterior.

### <a name="sql-server-native-client"></a>SQL Server Native Client

> [!NOTE]
> [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) también describe los requisitos de los componentes cliente de SQL Server.

No olvide actualizar también SQL Server Native Client al menos a la versión SQL 2012 SP4 (11.*.7001.0). A partir de la versión 1810, este requisito es una [comprobación de requisitos previos (advertencia)](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-server-native-client).

Configuration Manager usa SQL Server Native Client en los siguientes roles de sistema de sitio:

- Servidor de base de datos del sitio
- Servidor de sitio: sitio de administración central, sitio primario o sitio secundario
- Punto de administración
- Punto de administración de dispositivos
- Punto de migración de estado
- Proveedor de SMS
- Punto de actualización de software
- Punto de distribución habilitado con multidifusión
- Punto de servicio de actualización de Asset Intelligence
- Punto de servicios de informes
- Servicio web del catálogo de aplicaciones
- Punto de inscripción
- Punto de Endpoint Protection
- Punto de conexión de servicio
- Punto de registro de certificados
- Punto de servicio de almacenamiento de datos


## <a name="update-windows-and-winhttp"></a>Actualización de Windows y WinHTTP

Windows 8.1, Windows Server 2012 R2, Windows 10, Windows Server 2016 y las versiones posteriores de Windows admiten de forma nativa TLS 1.2 para las comunicaciones cliente-servidor a través de WinHTTP.

Las versiones anteriores de Windows, como Windows 7 o Windows Server 2012, no habilitan TLS 1.1 ni 1.2 de manera predeterminada para las comunicaciones cliente-servidor a través de HTTPS. Para estas versiones anteriores de Windows, instale la [actualización 3140245](https://support.microsoft.com/help/3140245) para habilitar TLS 1.1 y TLS 1.2 como los protocolos seguros predeterminados para WinHTTP en Windows. Luego, establezca los siguientes valores del Registro:

> [!IMPORTANT]
> Habilite esta configuración en todos los clientes *antes* de habilitar TLS 1.2 en los servidores de Configuration Manager. En caso contrario, puede dejarlos huérfanos sin darse cuenta.

Compruebe el valor de la configuración del Registro `DefaultSecureProtocols`, por ejemplo:

```Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

Si cambia este valor, reinicie el equipo.

> [!Note]  
> El ejemplo anterior muestra el valor de `0xAA0` para el parámetro `DefaultSecureProtocols` de WinHTTP. [KB 3140245: Actualización para habilitar TLS 1.1 y 1.2 como protocolos seguros predeterminados de WinHTTP en Windows](https://support.microsoft.com/help/3140245) muestra el valor hexadecimal de cada protocolo. De forma predeterminada en Windows, este valor es `0x0A0` para habilitar SSL 3.0 y TLS 1.0 para WinHTTP. En el ejemplo anterior se mantienen estos valores predeterminados, y se habilitan también TLS 1.1 y TLS 1.2 para WinHTTP. Esta configuración garantiza que el cambio no interrumpe ninguna otra aplicación que todavía podría depender de SSL 3.0 o TLS 1.0. Puede usar el valor de `0xA00` para habilitar solo TLS 1.1 y TLS 1.2. Configuration Manager admite el protocolo más seguro que Windows negocia entre ambos dispositivos.
>
> Si desea deshabilitar SSL 3.0 y TLS 1.0 por completo, use el parámetro de los protocolos deshabilitados de SChannel en Windows. Para obtener más información, consulte el artículo sobre [cómo restringir el uso de ciertos algoritmos criptográficos y protocolos en Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).


## <a name="update-windows-server-update-services-wsus"></a>Actualización de Windows Server Update Services (WSUS)

A fin de admitir TLS 1.2 para la comunicación cliente-servidor en WSUS en Windows Server 2012 y Windows Server 2012 R2, instale la actualización siguiente en el servidor WSUS:

- En el servidor WSUS que ejecuta Windows Server 2012, instale la [actualización 4022721](https://support.microsoft.com/help/4022721) o una posterior.
- En el servidor WSUS que ejecuta Windows Server 2012 R2, instale la [actualización 4022720](https://support.microsoft.com/help/4022720) o una posterior.


## <a name="known-issues"></a>Problemas conocidos

En esta sección de proporcionan consejos para solucionar los problemas comunes que se producen al habilitar la compatibilidad con TLS 1.2.

### <a name="unsupported-platforms"></a>Plataformas no compatibles

Las siguientes plataformas de cliente son compatibles con Configuration Manager, pero no se admiten en un entorno de TLS 1.2:

- Windows Server 2008
- Windows CE
- Apple OS X
- Dispositivos Windows 10 administrados con MDM local

### <a name="reports-dont-show-in-the-console"></a>Los informes no se muestran en la consola

Si los informes no se muestran en la consola de Configuration Manager, asegúrese de actualizar el equipo en el que está ejecutando la consola. Deberá [actualizar .NET Framework](#update-net-framework-to-support-tls-12) y habilitar la criptografía segura.

### <a name="fips-security-policy-enabled"></a>Directiva de seguridad FIPS habilitada

Si habilita la configuración de directiva de seguridad FIPS para el cliente o un servidor, la negociación de Secure Channel (Schannel) puede provocar que utilicen TLS 1.0. Este comportamiento se produce incluso si deshabilita el protocolo en el Registro.

Para investigar esto, habilite el registro de eventos del canal seguro y, luego, revise los eventos de Schannel en el registro del sistema. Para obtener más información, consulte el artículo sobre [cómo restringir el uso de ciertos algoritmos criptográficos y protocolos en Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

### <a name="sql-server-communication-failure"></a>Error de comunicación de SQL Server

Si se produce algún error de comunicación de SQL Server y se devuelve un error **SslSecurityError**, compruebe la siguiente configuración:

- [Actualice .NET Framework](#update-net-framework-to-support-tls-12) y habilite la criptografía segura en cada equipo
- [Actualice SQL Server](#update-sql-server-and-client-components) en el servidor host
- [Actualice los componentes del cliente SQL](#update-sql-server-and-client-components) en todos los sistemas que se comunican con SQL. Por ejemplo, los servidores de sitio, el proveedor de SMS y los servidores del rol de sitio.

### <a name="configuration-manager-client-communication-failures"></a>Errores de comunicación del cliente de Configuration Manager

Si el cliente de Configuration Manager no se comunica con los roles de sitio, compruebe que [actualizó Windows](#update-windows-and-winhttp) para admitir TLS 1.2 para la comunicación cliente/servidor mediante el uso de WinHTTP. Los roles de sitio comunes incluyen puntos de distribución, puntos de administración y puntos de migración de estado.

### <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>El punto de servicios de informes devuelve un error inesperado

Si el punto de servicios de informes no configura los informes, revise el registro **SRSRP.log** para ver la entrada de error siguiente:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Para solucionar este problema, siga estos pasos:

1. [Actualice .NET Framework](#update-net-framework-to-support-tls-12) y habilite la criptografía segura en todos los equipos pertinentes.

1. Después de instalar las actualizaciones, reinicie el servicio SMS_Executive.

### <a name="application-catalog-doesnt-initialize"></a>El catálogo de aplicaciones no se inicializa

> [!Important]  
> El catálogo de aplicaciones está en desuso. Para más información, consulte [Características en desuso y eliminadas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

Si el catálogo de aplicaciones no se inicializa, revise el archivo **ServicePortalWebSite.svclog** para ver la entrada de error siguiente:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Para solucionar este problema, siga estos pasos:

1. [Actualice .NET Framework](#update-net-framework-to-support-tls-12) y habilite la criptografía segura en todos los equipos pertinentes.

1. En la carpeta `%WinDir%\System32\InetSrv` del servidor del catálogo de aplicaciones, cree un archivo **W2SP.exe.config** con el contenido siguiente:

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > Este es el archivo predeterminado que se crea si la aplicación se compiló con .NET Framework 4.6.3.

1. Use la seguridad de transporte HTTPS para los roles del catálogo de aplicaciones.

    > [!Important]
    > Cuando se usa la seguridad de mensajes HTTP para los roles del catálogo de aplicaciones, WCF se codifica de forma rígida para que solo use SSL 3.0 y TLS 1.0. Esto evita el uso de TLS 1.2.

1. Si hizo alguna modificación, reinicie el equipo.

### <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>El Centro de software o el explorador no se puede comunicar con el catálogo de aplicaciones

> [!Important]  
> El catálogo de aplicaciones está en desuso. Para más información, consulte [Características en desuso y eliminadas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

El mejor método para que el Centro de Software funcione con las aplicaciones disponibles para el usuario en un sitio habilitado para TLS 1.2 es quitar la función del catálogo de aplicaciones. A continuación, deje que el Centro de software se comunique directamente con un punto de administración. Para más información, consulte [Eliminación del catálogo de aplicaciones](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).

Si tiene que resolver errores de comunicación entre el catálogo de aplicaciones y el Centro de software, compruebe las condiciones siguientes:

- [Actualice .NET Framework](#update-net-framework-to-support-tls-12) y habilite la criptografía segura en cada equipo.

- Después de realizar los cambios, reinicie todos los equipos afectados.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

### <a name="service-connection-point-upload-failures"></a>Errores de carga del punto de conexión del servicio

Si el punto de conexión del servicio no carga datos a SCCMConnectedService, [actualice .NET Framework](#update-net-framework-to-support-tls-12) y habilite la criptografía segura en cada equipo. No olvide reiniciar los equipos una vez hechos los cambios.

### <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>La consola de Configuration Manager muestra el cuadro de diálogo de incorporación a Intune

Si el cuadro de diálogo de incorporación a Intune aparece cuando la consola intenta conectarse al portal de Intune, [actualice .NET Framework](#update-net-framework-to-support-tls-12) y habilite la criptografía segura en cada equipo. No olvide reiniciar los equipos una vez hechos los cambios.

### <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>La consola de Configuration Manager muestra un error al iniciar sesión en Azure

Al intentar crear aplicaciones en Azure Active Directory (Azure AD), si el cuadro de diálogo de incorporación a los servicios de Azure presenta un error inmediatamente después de que se selecciona **Iniciar sesión**, [actualice .NET Framework](#update-net-framework-to-support-tls-12) y habilite la criptografía segura. No olvide reiniciar los equipos una vez hechos los cambios.

### <a name="configuration-manager-cloud-services-and-tls-12"></a>Servicios en la nube de Configuration Manager y TLS 1.2

A partir de la versión 1802, las máquinas virtuales de Azure utilizadas por la puerta de enlace de administración en la nube y los puntos de distribución en la nube admiten TLS 1.2. Los clientes compatibles en la versión 1802 o posterior utilizan automáticamente TLS 1.2.

El registro **SMSAdminui.log** puede contener un error similar al ejemplo siguiente:

```
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

En el registro de eventos del sistema, el identificador de evento 36874 de SChannel podría registrarse con la descripción siguiente: `An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->


## <a name="see-also"></a>Consulte también

- Para obtener más información, consulte [Procedimientos recomendados sobre la seguridad de la capa de transporte (TLS) con .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).

- [KB 3135244: Compatibilidad con TLS 1.2 para Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

- [Referencia técnica de controles criptográficos](cryptographic-controls-technical-reference.md)
