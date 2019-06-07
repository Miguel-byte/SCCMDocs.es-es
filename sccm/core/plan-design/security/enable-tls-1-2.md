---
title: Habilitación de TLS 1.2
titleSuffix: Configuration Manager
description: Información sobre cómo habilitar TLS 1.2 para Microsoft Configuration Manager.
ms.date: 05/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3641c3a9adce23f24a80135d996da03e12e78907
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/29/2019
ms.locfileid: "66355612"
---
# <a name="how-to-enable-tls-12-for-configuration-manager"></a>Habilitación de TLS 1.2 para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se describe cómo habilitar TLS 1.2 para Configuration Manager, incluso para los componentes individuales. En este artículo también se describen los requisitos de actualización de las características más usadas y la solución de algunos problemas comunes.

Configuration Manager se basa en muchos componentes distintos para garantizar una comunicación segura. El protocolo que se usa para una conexión determinada depende de las funcionalidades de todos los componentes requeridos. Si un componente no está actualizado, es posible que la comunicación use un protocolo más antiguo y menos seguro.

Para habilitar correctamente Configuration Manager a fin de admitir TLS 1.2, debe habilitar TLS 1.2 para todos los componentes necesarios. Los componentes necesarios dependen del entorno y de las características de Configuration Manager que use.


## <a name="to-enable-tls-12"></a>Para habilitar TLS 1.2

Para habilitar TLS 1.2, primero debe habilitar TLS 1.2 como proveedor de seguridad para cada equipo que ejecute o interactúe con Configuration Manager. Luego, habilite TLS 1.2 para los componentes de los que depende Configuration Manager para tener una comunicación segura.

### <a name="enable-the-tls-12-protocol-as-a-security-provider"></a>Habilitación del protocolo TLS 1.2 como proveedor de seguridad

Compruebe la configuración de la subclave "\SecurityProviders\SCHANNEL\Protocols" del registro, tal como se muestra en [Procedimientos recomendados sobre la seguridad de la capa de transporte (TLS) con .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry?).

> [!NOTE]
> TLS 1.2 está habilitado de manera predeterminada. Por lo tanto, no se requiere modificar estas claves para habilitarlo. Puede realizar cambios en Protocolos para deshabilitar TLS 1.0 y TLS 1.1 después de seguir el resto de las instrucciones de este artículo y de haber comprobado que el entorno funciona sin problemas solo con TLS 1.2 habilitado.

### <a name="enable-tls-12-for-dependent-components"></a>Habilitación de TLS 1.2 para componentes dependientes
Para habilitar TLS 1.2 para los componentes dependientes de los que depende Configuration Manager para tener una comunicación segura, debe completar los siguientes pasos:

- [Actualización de .NET Framework para admitir TLS 1.2](#update-net-framework-to-support-tls-12)
- [Actualización de SQL Server y componentes cliente](#update-sql-server-and-client-components)
- [Habilitación de Windows y WinHTTP en Windows 8.0, Windows Server 2012 R2 y versiones anteriores](#update-windows-and-winhttp)
- [Actualización de Windows Server Update Services (WSUS)](#update-windows-server-update-services)

#### <a name="update-net-framework-to-support-tls-12"></a>Actualización de .NET Framework para admitir TLS 1.2
Para actualizar .NET Framework a fin de admitir TLS 1.2, primero determine el número de versión de .NET. Para obtener ayuda, consulte el artículo sobre [cómo determinar qué versiones y niveles de Service Pack de Microsoft .NET Framework están instalados](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

Las versiones anteriores de .NET Framework pueden requerir actualizaciones o cambios en el registro para habilitar la criptografía segura. Use estas instrucciones:

- .NET Framework 4.6.2 admite TLS 1.1 y TLS 1.2.  No se requiere ningún cambio adicional.
- .NET Framework 4.6 y versiones anteriores [se deben actualizar](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies) para admitir TLS 1.1 y TLS 1.2.

Si usa .NET Framework 4.5.1 o 4.5.2 en Windows 8.1, Windows RT 8.1 o Windows Server 2012, las actualizaciones importantes y otros detalles también están disponibles en el [Centro de descarga](https://www.microsoft.com/download/details.aspx?id=42883).
-  .NET Framework debe estar configurado para admitir criptografía segura. Establezca la configuración `SchUseStrongCrypto` del registro en `DWORD:00000001`. Esto deshabilita el cifrado de flujo RC4 y requiere reiniciar. Para más información sobre esta configuración, consulte el [aviso de seguridad de Microsoft 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358).

Para las aplicaciones de 32 bits que se ejecutan en sistemas de 32 bits o aplicaciones de 64 bits que se ejecutan en sistemas de 64 bits, actualice el valor de subclave siguiente:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto" = (DWORD): 00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto"=dword:00000001
```
En el caso de las aplicaciones de 32 bits que se ejecutan en sistemas de 64 bits, actualice el valor de subclave siguiente:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Wow6432Node\Microsoft\.NETFramework\\v2.0.50727]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto" = (DWORD): 00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\
   WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto"=dword:00000001
```
#### <a name="update-sql-server-and-client-components"></a>Actualización de SQL Server y componentes cliente

Microsoft SQL Server 2016 admite TLS 1.1 y TLS 1.2.
Las versiones anteriores y las bibliotecas dependientes pueden requerir actualizaciones. Para más información, consulte [KB 3135244: Compatibilidad con TLS 1.2 para Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

> [!NOTE]
> KB 3135244 también describe los requisitos de los componentes cliente de SQL Server. Actualice cada componente que se usa en su entorno.

#### <a name="update-windows-and-winhttp"></a>Actualización de Windows y WinHTTP

Windows 10, Windows 8.1, Windows Server 2016 y Windows Server 2012 R2 admiten de fábrica TLS 1.2 para las comunicaciones cliente-servidor a través de WinHTTP.

Windows 8.0, Windows Server 2012 y las versiones anteriores de Windows no habilitan TLS 1.1 ni 1.2 de manera predeterminada para las comunicaciones cliente-servidor a través de HTTPS. Para estas versiones anteriores de Windows, debe instalar la [actualización 3140245](https://support.microsoft.com/help/3140245) para habilitar TLS 1.1 y TLS 1.2 como los protocolos seguros predeterminados en WinHTTP en Windows y establezca los valores del registro siguientes.

> [!IMPORTANT]
> Se debe ejecutar primero en todos los clientes de bajo nivel **antes** de habilitar TLS 1.2 o pueden quedar huérfanos de manera inadvertida.

Compruebe que la configuración `DefaultSecureProtocols` del registro es `0xAA0`, tal como se muestra a continuación:

```
HKEY_LOCAL_MACHINE\SOFTWARE\
   \Microsoft\Windows\CurrentVersion\
      Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\
   Wow6432Node\Microsoft\Windows\CurrentVersion\
      Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```
> [!NOTE]
> Este cambio requiere un reinicio.

#### <a name="update-windows-server-update-services"></a>Actualización de Windows Server Update Services (WSUS)

A fin de admitir TLS 1.2 para la comunicación cliente-servidor en WSUS en Windows Server 2012 y Windows Server 2012 R2, debe aplicar la actualización siguiente en el servidor WSUS:
- En el servidor WSUS que ejecutar Windows Server 2012, aplique la [actualización 4022721](https://support.microsoft.com/help/4022721) o una actualización posterior.
- En el servidor WSUS que ejecutar Windows Server 2012 R2, aplique la [actualización 4022720](https://support.microsoft.com/help/4022720) o una actualización posterior.

## <a name="tasks-required-for-configuration-manager-features-and-scenarios"></a>Tareas necesarias para escenarios y características de Configuration Manager
En esta sección se describen las dependencias para características y escenarios específicos de Configuration Manager. Para determinar los pasos siguientes, busque los elementos que se aplican al entorno y, luego, compruebe las dependencias con los pasos ya entregados en [Habilitación de TLS 1.2 para componentes dependientes](#enable-tls-12-for-dependent-components).

|Característica o un escenario|Tareas de actualización|
|--- |--- |
|Servidores de sitio (central, principal o secundario)|[Actualice .NET Framework](#update-net-framework-to-support-tls-12) y compruebe la configuración de la criptografía segura.|
|Proveedor de SMS|[Actualice SQL Server y sus componentes cliente](#update-sql-server-and-client-components) según corresponda para cada proveedor de SMS.|
|Roles de sistema de sitio|[Actualice .NET Framework](#update-net-framework-to-support-tls-12) y compruebe la configuración de la criptografía segura. [Actualice SQL Server y sus componentes cliente](#update-sql-server-and-client-components).|
|Catálogo de aplicaciones de punto de conexión de servicio|[Actualice .NET Framework](#update-net-framework-to-support-tls-12) y compruebe la configuración de la criptografía segura.|
|Punto de notificación de SRS|[Actualice .NET Framework](#update-net-framework-to-support-tls-12) en el servidor de sitio y los servidores de SRS. Reinicie el servicio SMS_Executive según sea necesario.|
|Consola de Configuration Manager|[Actualice .NET Framework](#update-net-framework-to-support-tls-12) y compruebe la configuración de la criptografía segura.|
|Cliente de SCCM con roles de sistema de sitio HTTPS|[Actualice Windows para admitir TLS 1.2 para las comunicaciones cliente-servidor mediante WinHTTP](#update-windows-and-winhttp).|
|Centro de software|[Actualice .NET Framework](#update-net-framework-to-support-tls-12) y compruebe la configuración de la criptografía segura.|
|Punto de actualización de software|[Actualice WSUS](#update-windows-server-update-services).|
|Puntos de administración|Actualice al cliente nativo de SQL Server más reciente para habilitar Configuration Manager para comunicarse con los componentes de SQL Server habilitados para TLS 1.2 más recientes. Consulte la tabla "Descargas de componentes cliente" en [Compatibilidad con TLS 1.2 para Microsoft SQL Server](https://support.microsoft.com/help/3135244).|

## <a name="known-issues"></a>Problemas conocidos

En esta sección de proporcionan consejos para solucionar los problemas comunes que se producen al habilitar la compatibilidad con TLS 1.2.

### <a name="fips-security-policy-enabled"></a>Directiva de seguridad FIPS habilitada

Si la configuración de la directiva de seguridad FIPS está habilitada para el cliente o para un servidor, la negociación de canal seguro (Schannel) puede provocar que se use TLS 1.0 incluso si el protocolo se deshabilita mediante el registro.

Para investigar esto, habilite el registro de eventos del canal seguro y, luego, revise los eventos de Schannel en el registro del sistema. Para información relacionada, consulte el artículo sobre [cómo restringir el uso de ciertos algoritmos criptográficos y protocolos en Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

### <a name="sql-server-communication-failure"></a>Error de comunicación de SQL Server

Si se produce algún error de comunicación de SQL Server y se devuelve un error **SslSecurityError**, compruebe que se cumple lo siguiente:
- .NET Framework está actualizado y tiene habilitada la criptografía segura en cada máquina.
- SQL Server está actualizado en el servidor host.
- Los componentes cliente de SQL están actualizados en los servidores de sitio, el proveedor de SMS, los servidores de rol de sitio y todos los demás sistemas que se comunican con SQL Server.

### <a name="configuration-manager-client-communication-failures"></a>Errores de comunicación del cliente de Configuration Manager

Si el cliente de Configuration Manager no se comunica con los puntos de conexión del rol de sitio, como los puntos de distribución, los puntos de administración y los puntos de migración de estado, compruebe que Windows se actualizó para admitir TLS 1.2 para la comunicación cliente-servidor mediante WinHTTP.

### <a name="srs-reporting-point-fails-and-returns-an-expected-error"></a>Error del punto de notificación de SRS y se devuelve un error inesperado

Si el punto de notificación de SRS no configura los informes, revise el *SRSRP.log* para ver la entrada de error siguiente:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Para solucionar este problema, siga estos pasos:

1. Compruebe que .NET Framework está actualizado y tiene habilitada la criptografía segura en todos los equipos pertinentes.
1. Compruebe que el servicio SMS_Executive se reinició después de instaladas las actualizaciones.

### <a name="application-catalog-doesnt-initialize"></a>El catálogo de aplicaciones no se inicializa

Si el catálogo de aplicaciones no se inicializa, revise el archivo *ServicePortalWebSite.svclog* para ver la entrada de error siguiente:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Para solucionar este problema, siga estos pasos:
1. Compruebe que .NET Framework está actualizado y tiene habilitada la criptografía segura en todos los equipos pertinentes.
1. En la carpeta C:\Windows\System32\InetSrv del servidor del catálogo de aplicaciones, cree un archivo *W2SP.exe.config* mediante la ejecución del script siguiente: 

   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
   <configuration>
     <runtime>
     <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
     </runtime>
   </configuration>
   ```
   > [!NOTE]
   > Este es el archivo predeterminado que se crearía si la aplicación se compiló con .NET Framework 4.6.3.
1. Use la seguridad de transporte HTTPS para los roles del catálogo de aplicaciones.

   > [!NOTE]
   > Cuando se usa la seguridad de mensajes HTTP para los roles del catálogo de aplicaciones, WCF se codifica de forma rígida para que solo use SSL 3.0 y TLS 1.0. Esto evita el uso de TLS 1.2.
1. Si se hizo alguna modificación, reinicie el equipo.


### <a name="software-center-or-browser-doesnt-communicate-with-application-catalog"></a>El Centro de software o el explorador no se puede comunicar con el catálogo de aplicaciones

Para resolver errores de comunicación entre el catálogo de aplicaciones y el Centro de software o el explorador, compruebe las condiciones siguientes:

- .NET Framework está actualizado y tiene habilitada la criptografía segura en cada equipo.
- El explorador está configurado para admitir TLS 1. Antes de Windows 10, esta opción estaba deshabilitada de manera predeterminada.
- Todos los equipos se reiniciaron una vez hechos los cambios.

   > [!NOTE]
   > Para que el Centro de software funcione con el servidor con TLS 1.2 forzado para las aplicaciones disponibles para el usuario, se recomienda quitar los roles del catálogo de aplicaciones y dejar que el Centro de software se comunique con el punto de administración. Para más información, consulte [Eliminación del catálogo de aplicaciones](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).

### <a name="service-connection-point-upload-failures"></a>Errores de carga del punto de conexión del servicio

Si el punto de conexión del servicio no carga datos a SCCMConnectedService, compruebe que .NET Framework está actualizado y tiene habilita la criptografía segura en cada equipo. No olvide reiniciar los equipos una vez hechos los cambios.

### <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>La consola de Configuration Manager muestra el cuadro de diálogo de incorporación a Intune

Si el cuadro de diálogo de incorporación a Intune aparece cuando la consola intenta conectarse al portal de Intune, compruebe que .NET Framework está actualizado y tiene habilitada la criptografía segura en cada equipo.  No olvide reiniciar los equipos una vez hechos los cambios.

### <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>La consola de Configuration Manager muestra un error al iniciar sesión en Azure

Si el cuadro de diálogo de incorporación a los servicios de Azure presenta un error inmediatamente después de que se selecciona **Iniciar sesión** al intentar crear aplicaciones de Azure AD, compruebe que .NET Framework esté actualizado y que la criptografía segura esté habilitada. Es necesario reiniciar para que estos cambios surtan efecto.

## <a name="see-also"></a>Consulte también

[Referencia técnica de controles criptográficos](cryptographic-controls-technical-reference.md)
