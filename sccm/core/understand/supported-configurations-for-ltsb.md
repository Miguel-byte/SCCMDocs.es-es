---
title: 'Configuraciones compatibles con LTBS '
titleSuffix: Configuration Manager
description: Entienda qué sistemas operativos y productos dependientes funcionan con la rama de mantenimiento a largo plazo de System Center Configuration Manager.
ms.date: 05/10/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4b71530cbde931c14810ba0e0960e530b56ece04
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70891887"
---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Configuraciones admitidas de la rama de mantenimiento a largo plazo de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama de mantenimiento a largo plazo)*

Use la información de este tema para comprender qué sistemas operativos y dependencias de productos son compatibles con la rama de mantenimiento a largo plazo (LTSB) de Configuration Manager.
Si no se indica lo contrario en este tema o en los temas específicos de la LTSB, se aplican a la LTSB las mismas configuraciones y limitaciones que se aplican a la versión 1606 de la rama actual.  Cuando se produzcan conflictos, use la información que se aplica a la edición que use. Normalmente, la LTSB es más limitada que la rama actual.

## <a name="general-statement-of-support"></a>Estado general de compatibilidad
Los siguientes productos y tecnologías son compatibles con esta rama de Configuration Manager. Sin embargo, su inclusión en este contenido no expresa una extensión de la compatibilidad con cualquier producto o versión más allá del ciclo de vida de soporte individual de los productos. Los productos que están fuera de su ciclo de vida de soporte no se pueden usar con Configuration Manager. Para obtener más información, visite el sitio web [Ciclo de vida de soporte de Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270) y lea la [Directiva de ciclo de vida de soporte técnico: preguntas más frecuentes](https://go.microsoft.com/fwlink/p/?LinkId=31976).

Además, los productos y las versiones de los productos que no aparecen en los temas siguientes no se admiten a menos que se hayan anunciado en el [Blog de Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/).

**Limitaciones de compatibilidad futura:** la LTSB tiene compatibilidad limitada con futuros sistemas operativos cliente y del servidor, y dependencias del producto. La lista de plataformas de la LTSB se fija para la vida de la versión:

**Windows:**
- Solo se admiten actualizaciones de seguridad y calidad para Windows.
- No hay compatibilidad con ramas actuales (CB), ramas actuales para empresas (CBB) ni LTSB de Windows 10.
- Las nuevas versiones principales de Windows Server no son compatibles.

**SQL Server:**
- Solo son compatibles con SQL Server las actualizaciones de seguridad y calidad o las actualizaciones secundarias, como los Service Pack.
- Las nuevas versiones principales de SQL Server no son compatibles.  

## <a name="site-systems-and-servers"></a>Servidores y sistemas de sitio
La LTSB admite el uso de los siguientes sistemas operativos de equipo Windows como sistemas de sitio.  Cada sistema operativo tiene los mismos requisitos y limitaciones que la misma entrada de [Sistemas operativos compatibles para los servidores de sistema de sitio](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  Por ejemplo, la instalación Server Core de Windows 2012 R2 debe ser una versión x64, solo se admite para hospedar un punto de distribución y no es compatible con el entorno PXE o multidifusión.

**Sistemas operativos compatibles:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows Server 2008 R2 con SP1 (x64): Standard, Enterprise, Datacenter
- Windows Server 2008 con SP2 (x86, x64): Standard, Enterprise, Datacenter *(vea la nota 1)*
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional y Enterprise
- Windows 7 con SP1 (x86, x64): Professional, Enterprise y Ultimate
- La instalación Server Core de Windows Server 2012
- La instalación Server Core de Windows Server 2012 R2    

*Nota 1*: No se admite este sistema operativo para servidores de sitio o roles de sistema de sitio con la excepción del punto de distribución y el punto de distribución de extracción. Puede seguir usando este sistema operativo como un punto de distribución hasta que se anuncie que esta compatibilidad queda obsoleta o expire el período extendido de soporte técnico de este sistema operativo. Para más información, vea [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095) (La instalación de System Center Configuration Manager CB y LTBS produce un error en Windows Server 2008).

## <a name="client-management"></a>Administración de cliente
En las secciones siguientes se identifican los sistemas operativos cliente que puede administrar con la LTSB. La LTSB no admite la adición de nuevos sistemas operativos como clientes admitidos.

### <a name="windows-computers"></a>Equipos Windows
Puede usar la LTSB para administrar los siguientes sistemas operativos de equipo Windows con el software cliente de Configuration Manager que se incluye con Configuration Manager. Para más información, vea [Implementar clientes en equipos Windows con System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

**Sistemas operativos compatibles:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter (nota 1)
- Windows Server 2012 (x64): Standard, Datacenter (nota 1)
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows Server 2008 R2 con SP1 (x64): Standard, Enterprise, Datacenter (nota 1)
- Windows Storage Server 2008 R2 (x86, x64): Workgroup, Standard, Enterprise
- Windows Server 2008 con SP2 (x86, x64): Standard, Enterprise, Datacenter (nota 1)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional y Enterprise
- Windows 7 con SP1 (x86, x64): Professional, Enterprise y Ultimate
- La instalación Server Core de Windows Server 2012 R2 (x64) (Nota 2)
- La instalación Server Core de Windows Server 2012 (x64) (Nota 2)
- La instalación Server Core de Windows Server 2008 R2 SP1 (x64)
- La instalación Server Core de Windows Server 2008 SP2 (x86, x64)

**(Nota 1)** Las versiones de Datacenter son compatibles pero no están certificadas para Configuration Manager.  
**(Nota 2)** Para admitir la instalación de inserción de cliente, el equipo que ejecuta esta versión del sistema operativo debe ejecutar el servicio de rol Servidor de archivos para el rol de servidor Servicios de archivos y almacenamiento. Para obtener más información sobre cómo instalar características de Windows en un equipo Server Core, consulte [Instalar roles de servidor y características en un servidor Server Core](https://technet.microsoft.com/library/jj574158(v=ws.11).aspx) en la biblioteca de TechNet de Windows Server 2012.

### <a name="windows-embedded"></a>Windows Embedded
Puede usar la LTSB para administrar los siguientes dispositivos de Windows Embedded mediante la instalación del software cliente en el dispositivo.  Para obtener más información, consulte [Planning for client deployment to Windows Embedded devices in System Center Configuration Manager](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices) (Planeación de la implementación del cliente en dispositivos Windows Embedded en System Center Configuration Manager).

**Limitaciones y requisitos:**  

-   Todas las características de cliente se admiten en sistemas de Windows Embedded que no tengan habilitados filtros de escritura.  

-   Los clientes que usan uno de los siguientes filtros son compatibles con todas las características, excepto la administración de energía:  

    -   Filtros de escritura mejorados (EWF)    

    -   Filtros de escritura basados en archivos RAM (FBWF)    

    -   Filtros de escritura unificados (UWF)  

-   El catálogo de aplicaciones no es compatible con ningún dispositivo de Windows Embedded.  

-   Para poder supervisar malware detectado en dispositivos de Windows Embedded basados en Windows XP, debe instalar el paquete de scripting de WMI de Microsoft Windows en el dispositivo incrustado. Use Windows Embedded Target Designer para instalar este paquete. Los archivos *WBEMDISP.DLL* y *WBEMDISP.TLB* deben existir y registrarse en la carpeta %windir%\System32\WBEM del dispositivo incrustado para garantizar que se informe sobre el malware detectado.  

**Sistemas operativos compatibles:**  
-   Windows 10 Enterprise 2016 LTSB (x86, x64)  
-   Windows 10 Enterprise 2015 LTSB (x86, x64)  
-   Windows Embedded 8.1 Industry (x86, x64)    
-   Windows Thin PC (x86, x64)    
-   Windows Embedded POSReady 7 (x86, x64)    
-   Windows Embedded Standard 7 con SP1 (x86, x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 Puede administrar dispositivos de Windows CE con el cliente heredado de dispositivos móviles de Configuration Manager que se incluye con Configuration Manager.  

**Limitaciones y requisitos:**  

-   El cliente de dispositivo móvil requiere 0,78 MB de espacio de almacenamiento para instalar el cliente. Un dispositivo móvil puede requerir hasta 256 KB de espacio adicional de almacenamiento para iniciar sesión.    

-   Las características de estos dispositivos móviles varían según el tipo de cliente y la plataforma. Para más información sobre el tipo de funciones de administración que admite Configuration Manager para un cliente heredado de dispositivo móvil, vea [Elegir una solución de administración de dispositivos para System Center Configuration Manager](/sccm/core/plan-design/choose-a-device-management-solution).  

**Sistemas operativos compatibles:**  

-   Windows CE 7.0 (procesadores ARM y x86)  

**Los idiomas admitidos son:**  
-   Chino (simplificado y tradicional)    
-   Inglés (EE.UU.)    
-   Francés (Francia)    
-   Alemán    
-   Italiano    
-   Japonés  
-   Coreano  
-   Portugués (Brasil)  
-   Ruso  
-   Español (España)  

### <a name="mac-computers"></a>Equipos Mac  
 Puede usar la LTSB para administrar equipos con Mac OS X con el cliente de Configuration Manager para Mac.

El paquete de instalación del cliente Mac no se suministra con los medios de Configuration Manager. Puede descargarlo como parte de la descarga de clientes para sistemas operativos adicionales en el [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?LinkID=525184).  

La compatibilidad con sistemas operativos Mac se limita a los que aparecen en esta sección. La compatibilidad no incluye otros sistemas operativos que pudieran ser compatibles mediante una futura actualización para paquetes de instalación de cliente Mac para la rama actual.

Para obtener más información, consulte [How to deploy clients to Macs in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs) (Implementar clientes en equipos Mac en System Center Configuration Manager).

**Versiones admitidas:**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Servidores Linux y UNIX
Puede usar la LTSB para administrar servidores Linux y UNIX con el cliente de Configuration Manager para Linux y UNIX.

Los paquetes de instalación del cliente Linux y UNIX no se suministran con los medios de Configuration Manager. Puede descargarlos como parte de la descarga de clientes para sistemas operativos adicionales en el [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?LinkID=525184). Además de los paquetes de instalación de cliente, la descarga de cliente incluye el script de instalación que administra la instalación del cliente en cada equipo.

La compatibilidad con sistemas operativos Linux y UNIX se limita a los que aparecen en esta sección. La compatibilidad no incluye otros sistemas operativos que pudieran ser compatibles mediante una futura actualización para paquetes de cliente Linux y UNIX para la rama actual.

**Limitaciones y requisitos:**  

-   Para consultar las dependencias de archivo del sistema operativo para el cliente Linux y UNIX, consulte [Requisitos previos para la implementación del cliente en servidores UNIX y Linux](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#BKMK_ClientDeployPrereqforLnU).  
-   Para obtener información general de las capacidades de administración compatibles con equipos que ejecutan Linux o UNIX, consulte [Implementar clientes en servidores UNIX y Linux con System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  
-   En versiones compatibles de Linux y UNIX, la versión enumerada incluye todas las posteriores versiones secundarias. Por ejemplo, cuando se indica compatibilidad con CentOS versión 6, también se incluyen las posteriores versiones secundarias de CentOS 6, como CentOS 6.3. De forma similar, cuando se indica compatibilidad con un sistema operativo que usa Service Packs, por ejemplo, SUSE Linux Enterprise Server 11 SP1, se incluyen los posteriores Service Packs para esa versión del sistema operativo.
-   Para obtener información sobre los paquetes de instalación de cliente y el agente universal, consulte [Implementar clientes en servidores UNIX y Linux con System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).


**Versiones admitidas:**    
Las siguientes versiones se admiten mediante el archivo .tar indicado.  
### <a name="aix"></a>AIX  

|Versión|Archivo|  
|-|-|  
|Versión 5.3 (Power)|ccm-Aix53ppc.&lt;compilación\>.tar|  
|Versión 6.1 (Power)|ccm-Aix61ppc.&lt;compilación\>.tar|  
|Versión 7.1 (Power)|ccm-Aix71ppc.&lt;compilación\>.tar|  

### <a name="centos"></a>CentOS  

|Versión|Archivo|  
|-|-|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  

### <a name="debian"></a>Debian  

|Versión|Archivo|    
|-|-|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 8 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 8 x64|ccm-Universalx64.&lt;compilación\>.tar|  

### <a name="hp-ux"></a>HP-UX  

|Versión|Archivo|  
|-|-|  
|Versión 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;compilación\>.tar|  
|Versión 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;compilación\>.tar|  
|Versión 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;compilación\>.tar|  
|Versión 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;compilación\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|Versión|Archivo|    
|-|-|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Versión|Archivo|  
|-|-|  
|Versión 4 x86|ccm-RHEL4x86.&lt;compilación\>.tar|  
|Versión 4 x64|ccm-RHEL4x64.&lt;compilación\>.tar|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  

### <a name="solaris"></a>Solaris  

|Versión|Archivo|   
|-|-|  
|Versión 9 SPARC|ccm-Sol9sparc.&lt;compilación\>.tar|  
|Versión 10 x86|ccm-Sol10x86.&lt;compilación\>.tar|  
|Versión 10 SPARC|ccm-Sol10sparc.&lt;compilación\>.tar|  
|Versión 11 x86|ccm-Sol11x86.&lt;compilación\>.tar|  
|Versión 11 SPARC|ccm-Sol11sparc.&lt;compilación\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Versión|Archivo|  
|-|-|  
|Versión 9 x86|ccm-SLES9x86.&lt;compilación\>.tar|  
|Versión 10 SP1 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 10 SP1 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 11 SP1 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 11 SP1 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 12 x64|ccm-Universalx64.&lt;compilación\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|Versión|Archivo|    
|-|-|  
|Versión 10.04 LTS x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 10.04 LTS x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 12.04 LTS x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 12.04 LTS x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 14.04 LTS x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 14.04 LTS x64|ccm-Universalx64.&lt;compilación\>.tar|  

### <a name="exchange-server-connector"></a>Conector de Exchange Server
 La LTSB admite la administración limitada de dispositivos que se conectan a la instancia de Exchange Server, sin instalar software cliente. Para más información, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).

 **Limitaciones y requisitos:**  

-   Configuration Manager ofrece administración limitada para dispositivos móviles. La administración limitada está disponible cuando se usa el conector de Exchange Server para los dispositivos compatibles con Exchange Active Sync (EAS) que se conectan a un servidor que ejecuta Exchange Server o Exchange Online.  

-   Para más información sobre las funciones de administración que Configuration Manager admite para dispositivos móviles que administra el conector de Exchange Server, vea [Elegir una solución de administración de dispositivos para System Center Configuration Manager](/sccm/core/plan-design/choose-a-device-management-solution).  

**Versiones admitidas de Exchange Server:**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> La LTSB no admite la administración de dispositivos que se conectan a través de un servicio en línea, como Exchange Online (Office 365).


## <a name="configuration-manager-console"></a>Consola de Configuration Manager
La LTSB es compatible con los siguientes sistemas operativos para ejecutar la consola de Configuration Manager. Cada equipo que hospede la consola debe tener una versión mínima de .NET Framework 4.5.2, excepto Windows 10, que requiere una versión mínima de .NET Framework 4.6.

**Sistemas operativos compatibles:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows Server 2008 R2 con SP1 (x64): Standard, Enterprise, Datacenter
- Windows Server 2008 con SP2 (x86, x64): Standard, Enterprise, Datacenter
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional y Enterprise
- Windows 7 con SP1 (x86, x64): Professional, Enterprise y Ultimate


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>Versiones de SQL Server compatibles con la base de datos del sitio y el punto de notificación
La LTSB admite las siguientes versiones de SQL Server para hospedar la base de datos del sitio y el punto de notificación. Para cada una de las versiones compatibles, se aplican a la LTSB los mismos requisitos de configuración y limitaciones que aparecen en [Compatibilidad con versiones de SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions) para la rama actual.  Esto incluye el uso de un clúster de SQL Server o un grupo de disponibilidad AlwaysOn de SQL Server.  

**Versiones admitidas:**

- SQL Server 2016: Standard, Enterprise
- SQL Server 2014 SP2: Standard, Enterprise
- SQL Server 2014 SP1: Standard, Enterprise
- SQL Server 2012 SP3: Standard, Enterprise
- SQL Server 2008 R2 SP3: Standard, Enterprise, Datacenter
- SQL Server 2016 Express
- SQL Server 2014 Express SP2
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## <a name="support-for-active-directory-domains"></a>Compatibilidad con dominios de Active Directory
Todos los sistemas de sitio de la LTSB deben ser miembros de un dominio de Windows Active Directory compatible. La compatibilidad con dominios de Active Directory tiene los mismos requisitos y limitaciones que los que aparecen en [Compatibilidad con dominios de Active Directory](/sccm/core/plan-design/configs/support-for-active-directory-domains), pero se limita a los siguientes niveles funcionales de dominio:

**Niveles admitidos:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Temas de compatibilidad adicionales que se aplican a la rama de mantenimiento a largo plazo
La información de los siguientes temas de la rama actual se aplican a la LTSB:
- [Números de tamaño y escala](/sccm/core/plan-design/configs/size-and-scale-numbers)
- [Requisitos previos de sitio y sistema de sitio](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
- [Opciones de alta disponibilidad](/sccm/protect/understand/high-availability-options)
- [Hardware recomendado](/sccm/core/plan-design/configs/recommended-hardware)
- [Compatibilidad con las características de Windows y redes](/sccm/core/plan-design/configs/support-for-windows-features-and-networks)
- [Compatibilidad con entornos de virtualización](/sccm/core/plan-design/configs/support-for-virtualization-environments)
