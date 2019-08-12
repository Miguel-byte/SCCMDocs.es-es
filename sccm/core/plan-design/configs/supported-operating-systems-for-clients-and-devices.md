---
title: Dispositivos y clientes compatibles
titleSuffix: Configuration Manager
description: Obtenga información sobre qué versiones de SO admite Configuration Manager para clientes y dispositivos.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c391b681d2be9a7ce7e1cc1a9f7c69e58f958840
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536776"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Versiones de SO admitidas para clientes y dispositivos de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager admite la instalación de software cliente en equipos Windows y macOS.  

## <a name="general-requirements-and-limitations"></a>Limitaciones y requisitos generales

Revise las siguientes limitaciones y requisitos para todos los clientes:

- No se permite cambiar el tipo de inicio ni la configuración de **Iniciar sesión como** de ningún servicio de Configuration Manager. Este cambio puede impedir que servicios importantes funcionen correctamente.


## <a name="windows-computers"></a>Equipos Windows  

Para administrar las siguientes versiones del sistema operativo Windows, use el cliente que se incluye con Configuration Manager. Para obtener más información, consulte [Cómo implementar clientes en equipos Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).  

### <a name="supported-client-os-versions"></a>Versiones compatibles del sistema operativo de cliente

- **Windows 10**  

    Para obtener información más detallada, vea [Compatibilidad con Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).  

- **Windows 8.1** (x86, x64): Professional y Enterprise

- **Windows 7 con SP1** (x86, x64): Professional, Enterprise y Ultimate

#### <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

<!--3556025-->
[Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/) es una característica en versión preliminar de Microsoft Azure y Microsoft 365. A partir de la versión 1906, use Configuration Manager para administrar estos dispositivos virtuales que ejecutan Windows en Azure.

Al igual que un servidor de terminal, estos dispositivos virtuales permiten varias sesiones de usuario activas simultáneas. Para facilitar el rendimiento del cliente, ahora en Configuration Manager se deshabilitan las directivas de usuario en todos los dispositivos que admiten estas sesiones de usuario múltiples. Aunque habilite las directivas de usuario, el cliente las deshabilita de forma predeterminada en estos dispositivos, que incluyen Windows Virtual Desktop y servidores de terminal.

El cliente solo deshabilita la directiva de usuario cuando detecta este tipo de dispositivo durante una instalación nueva. Para un cliente existente de este tipo que actualice a esta versión, se conserva el comportamiento anterior. En un dispositivo existente, establece la configuración de directiva de usuario incluso si detecta que el dispositivo permite varias sesiones de usuario.

Si en este escenario requiere la directiva de usuario y acepta un posible impacto del rendimiento, use el SDK de Configuration Manager con la [clase WMI de servidor SMS_PolicyAgentConfig](/sccm/develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class). Establezca la nueva propiedad `PolicyEnableUserPolicyOnTS` en `true`.

> [!Note]  
> No puede usar la administración conjunta con una instancia de Windows Virtual Desktop. Windows 10 Enterprise para escritorios virtuales (EVD) es, en realidad, una edición de Windows Server, que no tiene los componentes MDM.<!-- SCCMDocs-pr#3950 -->

### <a name="supported-server-os-versions"></a>Versiones compatibles del sistema operativo del servidor

- **Windows Server 2019**: Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>  
    (A partir de la versión 1806 de Configuration Manager)

- **Windows Server 2016**: Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>  

- **Windows Storage Server 2016**: Workgroup, Standard  

- **Windows Server 2012 R2** (x64): Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64): Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

- **Windows Server 2008 R2 con SP1** (x64): Standard, Enterprise, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>

- **Windows Storage Server 2008 R2** (x86, x64): Workgroup, Standard, Enterprise

- **Windows Server 2008 con SP2** (x86, x64): Standard, Enterprise, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>

#### <a name="server-core"></a>Server Core

Las siguientes versiones se refieren específicamente a la instalación Server Core del sistema operativo. <sup>[Nota 3](#bkmk_note3)</sup>  

Las versiones de canal semestrales de Windows Server son instalaciones Server Core, por ejemplo, Windows Server, versión 1809. Como un cliente de Configuration Manager, se admiten de la misma forma que la versión de canal semestral de Windows 10 asociada. Para más información, vea [Compatibilidad con Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).

- **Windows Server 2019** (x64) <sup>[Nota 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup>[Nota 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup>[Nota 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup>[Nota 2](#bkmk_note2)</sup>

- **Windows Server 2008 R2** sin ningún Service Pack o con SP1 (x64)

- **Windows Server 2008 SP2** (x86, x64)

#### <a name="bkmk_note1"></a> Nota 1

Configuration Manager prueba y admite las ediciones de Windows Server Datacenter, pero está certificado oficialmente para Windows Server. No se ofrece soporte técnico de revisiones de Configuration Manager para problemas específicos de Windows Server Datacenter Edition. Para más información sobre el programa de certificación de Windows Server, vea [Windows Server Catalog](https://www.windowsservercatalog.com/).

#### <a name="bkmk_note2"></a> Nota 2

Para admitir la [instalación de inserción de cliente](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation), agregue el servicio del servidor de archivos del rol del servidor de Servicios de archivos y almacenamiento. Para más información sobre cómo instalar características de Windows en Server Core, vea [Install roles, role services, and features by using Windows PowerShell cmdlets](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets) (Instalar roles, servicios de roles y características mediante los cmdlets de Windows PowerShell).  

#### <a name="bkmk_note3"></a> Nota 3

No se admite la nueva aplicación de Centro de Software en ninguna versión de Windows Server Core.<!--SCCMDocs issue 683-->


## <a name="windows-embedded-computers"></a>Equipos de Windows Embedded  

Administre dispositivos de Windows Embedded mediante la instalación del cliente de Configuration Manager en el dispositivo. Para obtener más información, vea [Planeación de la implementación del cliente en dispositivos Windows Embedded](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices).  

### <a name="requirements-and-limitations"></a>Limitaciones y requisitos

- Todas las características de cliente se admiten en sistemas de Windows Embedded que no tengan habilitados filtros de escritura.  

- Los clientes que usan uno de los siguientes filtros son compatibles con todas las características, excepto la administración de energía:  

    - Filtros de escritura mejorados (EWF)

    - Filtros de escritura basados en archivos RAM (FBWF)

    - Filtros de escritura unificados (UWF)  

- El catálogo de aplicaciones no es compatible con ningún dispositivo de Windows Embedded.  

### <a name="supported-os-versions"></a>Versiones de SO admitidas  

- **Windows 10 Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Esta versión incluye el canal de servicio a largo plazo (LTSC). Para más información, vea [Información general de Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows Embedded 8.1 Industry** (x86, x64)

- **Windows Embedded 8 Standard** (x86, x64)

- **Windows Thin PC** (x86, x64)

- **Windows Embedded POSReady 7** (x86, x64)

- **Windows Embedded Standard 7 con SP1** (x86, x64)


## <a name="windows-ce-computers"></a>Equipos de Windows CE

Administre dispositivos de Windows CE con el cliente heredado de dispositivos móviles de Configuration Manager que se incluye con Configuration Manager.  

### <a name="requirements-and-limitations"></a>Limitaciones y requisitos

- El cliente de dispositivo móvil necesita 0,78 MB de espacio de almacenamiento para la instalación. El inicio de sesión puede requerir hasta 256 KB de espacio adicional de almacenamiento.

- Las características de estos dispositivos móviles varían según el tipo de cliente y la plataforma. Para obtener información sobre qué funciones de administración son compatibles, vea [Elegir una solución de administración de dispositivos](/sccm/core/plan-design/choose-a-device-management-solution).  

### <a name="supported-os-versions"></a>Versiones de SO admitidas

- Windows CE 7.0 (procesadores ARM y x86)  

    > [!Note]
    > El soporte técnico está en desuso para Windows CE 7.0 en Configuration Manager. Para obtener más información, consulte [Elementos eliminados y en desuso para clientes de Configuration Manager](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client).

#### <a name="supported-languages-include"></a>Los idiomas admitidos son

- Chino (simplificado y tradicional)

- Inglés (EE.UU.)

- Francés (Francia)

- Alemán

- Italiano

- Japonés  

- Coreano  

- Portugués (Brasil)  

- Ruso  

- Español (España)  


## <a name="mac-computers"></a>Equipos Mac  

Administre equipos Apple Mac con el cliente de Configuration Manager para macOS.  

El paquete de instalación del cliente macOS no se suministra con los medios de Configuration Manager. Descargue los **clientes para sistemas operativos adicionales** en el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=47719).  

Para obtener más información, consulte [How to deploy clients to Macs](/sccm/core/clients/deploy/deploy-clients-to-macs) (Implementación de clientes en equipos Mac).  

### <a name="requirements-and-limitations"></a>Limitaciones y requisitos

- No se permite instalar o ejecutar el cliente de Configuration Manager para macOS en equipos con una cuenta que no sea la cuenta raíz. Si lo hace, servicios importantes podrían dejar de funcionar correctamente.  

### <a name="supported-versions"></a>Versiones admitidas

- **macOS Mojave (10.14)**

- **macOS High Sierra (10.13)**

- **macOS Sierra (10.12)**

- **macOS 10.11** (El Capitan)  

- **macOS 10.10** (Yosemite)  

- **macOS 10.9** (Mavericks)

- **macOS 10.8** (Mountain Lion)

- **macOS 10.7** (Lion)

- **macOS 10.6** (Snow Leopard)


## <a name="linux-and-unix-servers"></a>Servidores Linux y UNIX  

> [!Important]  
> La versión 1902 de Configuration Manager anula la compatibilidad de Linux y UNIX como cliente. El anuncio del desuso se realizó con la [versión 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802#deprecation-announcement-for-linux-and-unix-client-support). Para administrar servidores Linux, considere la posibilidad de usar la administración de Microsoft Azure. Las soluciones de Azure tienen una amplia compatibilidad con Linux que, en la mayoría de los casos, supera la funcionalidad de Configuration Manager, incluida la administración de revisiones de un extremo a otro para Linux.

Los paquetes de instalación del cliente Linux y UNIX no se suministran con los medios de Configuration Manager. Descargue los **clientes para sistemas operativos adicionales** en el [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). Además de los paquetes de instalación de cliente, la descarga de cliente incluye el script que administra la instalación del cliente en cada equipo.  

### <a name="requirements-and-limitations"></a>Limitaciones y requisitos

- Para consultar las dependencias de archivo del sistema operativo para el cliente Linux y UNIX, consulte [Requisitos previos para la implementación del cliente en servidores UNIX y Linux](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#BKMK_ClientDeployPrereqforLnU).  

- Para obtener información general de las funciones de administración compatibles con Linux o UNIX, vea [Implementar clientes en servidores UNIX y Linux](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  

- En versiones compatibles de Linux y UNIX, la versión enumerada incluye todas las posteriores versiones secundarias. Por ejemplo, CentOS versión 6 incluye CentOS 6.3. De manera similar, la compatibilidad con un sistema operativo que usa Service Packs (como SUSE Linux Enterprise Server 11 SP1), incluye los Service Packs posteriores para esa versión del sistema operativo.  

- Para obtener información sobre los paquetes de instalación de cliente y el agente universal, consulte [Implementar clientes en servidores UNIX y Linux](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  

### <a name="supported-versions"></a>Versiones admitidas

Las siguientes versiones se admiten mediante el archivo .tar indicado.  

#### <a name="aix"></a>AIX  

|Versión|Archivo TAR|  
|-|-|  
|Versión 6.1 (Power)|ccm-Aix61ppc.&lt;compilación\>.tar|  
|Versión 7.1 (Power)|ccm-Aix71ppc.&lt;compilación\>.tar|  

#### <a name="centos"></a>CentOS  

|Versión|Archivo TAR|  
|-|-|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  

#### <a name="debian"></a>Debian  

|Versión|Archivo TAR|  
|-|-|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 8 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 8 x64|ccm-Universalx64.&lt;compilación\>.tar|  

#### <a name="hp-ux"></a>HP-UX  

|Versión|Archivo TAR|  
|-|-|  
|Versión 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;compilación\>.tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|Versión|Archivo TAR|  
|-|-|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Versión|Archivo TAR|  
|-|-|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  

#### <a name="solaris"></a>Solaris  

|Versión|Archivo TAR|  
|-|-|  
|Versión 10 x86|ccm-Sol10x86.&lt;compilación\>.tar|  
|Versión 10 SPARC|ccm-Sol10sparc.&lt;compilación\>.tar|  
|Versión 11 x86|ccm-Sol11x86.&lt;compilación\>.tar|  
|Versión 11 SPARC|ccm-Sol11sparc.&lt;compilación\>.tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Versión|Archivo TAR|  
|-|-|  
|Versión 10 SP1 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 10 SP1 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 11 SP1 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 11 SP1 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 12 x64|ccm-Universalx64.&lt;compilación\>.tar|  

#### <a name="ubuntu"></a>Ubuntu  

|Versión|Archivo TAR|  
|-|-|  
|Versión 10.04 LTS x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 10.04 LTS x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 12.04 LTS x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 12.04 LTS x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 14.04 LTS x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 14.04 LTS x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 16.04 LTS x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 16.04 LTS x64|ccm-Universalx64.&lt;compilación\>.tar|  


## <a name="bkmk_OnpremOS"></a> MDM local

Configuration Manager tiene características integradas para administrar dispositivos móviles locales sin instalar el software cliente. Para obtener más información, consulte [Administrar dispositivos móviles con la infraestructura local](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  

### <a name="requirements-and-limitations"></a>Limitaciones y requisitos

- Configure el **punto de conexión de servicio** en el sitio de nivel superior de la jerarquía.  

### <a name="supported-operating-systems"></a>Sistemas operativos compatibles

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Esta versión incluye el canal de servicio a largo plazo (LTSC). Para más información, vea [Información general de Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows 10 IoT Mobile Enterprise**  

- **Windows 10 Team para Surface Hub**  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

    > [!Note]
    > El soporte técnico está en desuso para Windows 10 Mobile y Windows 10 Mobile Enterprise en Configuration Manager. Para obtener más información, consulte [Elementos eliminados y en desuso para clientes de Configuration Manager](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client).


## <a name="bkmk_ExSrvConOS"></a> Conector de Exchange Server  

Configuration Manager admite la administración limitada de dispositivos que se conectan a Exchange Server sin instalar el cliente de Configuration Manager. Para obtener más información, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  

### <a name="supported-versions-of-exchange-server"></a>Versiones admitidas de Exchange Server

- **Exchange Online (Office 365)** : esta versión incluye Business Productivity Online Standard Suite.  

- **Exchange Server 2016**  

- **Exchange Server 2013**  

- **Exchange Server 2010 SP1** o **Exchange Server 2010 SP2**
