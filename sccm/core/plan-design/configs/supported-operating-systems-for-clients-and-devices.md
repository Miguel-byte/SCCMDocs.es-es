---
title: Dispositivos y clientes compatibles | System Center Configuration Manager
description: "Obtenga información sobre qué sistemas operativos admite System Center Configuration Manager con clientes y dispositivos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
caps.latest.revision: 5
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 862291f52d5a1bb34fb5483806972fcf70f158a8

---
# <a name="supported-operating-systems-for-clients-and-devices-for-system-center-configuration-manager"></a>Sistemas operativos compatibles con dispositivos y clientes de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*




 System Center Configuration Manager admite la instalación de software cliente en diversos equipos Windows, Mac, Linux y UNIX.  

 **Requisitos y limitaciones para todos los clientes:**  

-   No se permite cambiar la configuración de tipo de inicio o de inicio de sesión de ningún servicio de Configuration Manager. Si lo hace, servicios importantes podrían dejar de funcionar correctamente.    

-   No se permite instalar o ejecutar el cliente de Configuration Manager para Linux o UNIX, o el cliente para Mac, en equipos con una cuenta que no sea root. Si lo hace, servicios importantes podrían dejar de funcionar correctamente.  

##  <a name="a-namebkmkwinclientosa-windows-computers"></a><a name="bkmk_WinClientos"></a> Equipos Windows  
 Puede administrar equipos Windows con el cliente de Configuration Manager que se incluye con Configuration Manager. Para obtener más información, consulte [Implementar clientes en equipos Windows con System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

**Sistemas operativos compatibles:**  

-  **Windows Server 2016**: Standard, Datacenter <sup>1</sup>
  - Windows Server 2016 se admite a partir de la versión 1606 de Configuration Manager con el paquete acumulativo de revisiones de KB3186654 (o la versión de línea base de 1606 que se ha publicado en octubre de 2016).  


-   **Windows Server 2012 R2** (x64): Standard, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64): Standard, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012** (x64)    

-   **Windows Server 2008 R2 con SP1** (x64): Standard, Enterprise, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2008 R2** (x86, x64): Workgroup, Standard, Enterprise    

-   **Windows Server 2008 con SP2** (x86, x64): Standard, Enterprise, Datacenter <sup>1</sup>    

-   **Windows 10 Enterprise LTSB** (x86, x64) <sup>3</sup>    

-   **Windows 10** (x86, x64): Pro, Enterprise    

-   **Windows 8.1** (x86, x64): Professional, Enterprise    

-   **Windows 8** (x86, x64): Professional, Enterprise    

-   **Windows 7 con SP1** (x86, x64): Professional, Enterprise, Ultimate    

-   **La instalación Server Core de Windows Server 2012 R2** (x64) <sup>2</sup>    

-   **La instalación Server Core de Windows Server 2012** (x64) <sup>2</sup>    

-   **La instalación Server Core de Windows Server 2008 R2**  
    **(sin Service Pack o con SP1)** (x64)    

-   **La instalación Server Core de Windows Server 2008 SP2** (x86, x64)  

 <sup>1</sup> Las versiones de Datacenter son compatibles pero no están certificadas para Configuration Manager. No ofrece soporte de revisiones para problemas específicos a Windows Server Datacenter Edition.  

 <sup>2</sup> Para admitir la instalación de inserción de cliente, el equipo que ejecuta esta versión del sistema operativo debe ejecutar el servicio de rol Servidor de archivos para el rol de servidor Servicios de archivos y almacenamiento. Para obtener más información sobre cómo instalar características de Windows en un equipo Server Core, consulte [Instalar roles de servidor y características en un servidor Server Core](http://go.microsoft.com/fwlink/p/?LinkId=299359) en la biblioteca de TechNet de Windows Server 2012.  

 <sup>3</sup> El uso de este sistema operativo requiere la versión 1602 u otra posterior.  

##  <a name="a-namebkmkembeddedosa-windows-embedded"></a><a name="bkmk_EmbeddedOS"></a> Windows Embedded  
 Puede administrar dispositivos de Windows Embedded mediante la instalación del software cliente de Configuration Manager en el dispositivo.  Para obtener más información, consulte [Planning for client deployment to Windows Embedded devices in System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md) (Planeación de la implementación del cliente en dispositivos Windows Embedded en System Center Configuration Manager).  

**Limitaciones y requisitos:**  

-   Todas las características de cliente se admiten en sistemas de Windows Embedded que no tengan habilitados filtros de escritura.  

-   Los clientes que usan uno de los siguientes filtros son compatibles con todas las características, excepto la administración de energía:  

    -   Filtros de escritura mejorados (EWF)    

    -   Filtros de escritura basados en archivos RAM (FBWF)    

    -   Filtros de escritura unificados (UWF)  

-   El catálogo de aplicaciones no es compatible con ningún dispositivo de Windows Embedded.  

-   Para poder supervisar malware detectado en dispositivos de Windows Embedded basados en Windows XP, debe instalar el paquete de scripting de WMI de Microsoft Windows en el dispositivo incrustado. Use Windows Embedded Target Designer para instalar este paquete. Los archivos **WBEMDISP.DLL** y **WBEMDISP.TLB** deben existir y registrarse en la carpeta **%windir%\System32\WBEM** del dispositivo incrustado para garantizar que se informa sobre el malware detectado.  

**Sistemas operativos compatibles:**  

-   **Windows 10 Enterprise** (x86, x64)  

-   **Windows 10 IoT Enterprise** (x86, x64)  

-   **Windows Embedded 8.1 Industry** (x86, x64)    

-   **Windows Embedded 8 Industry** (x86, x64)    

-   **Windows Embedded 8 Standard** (x86, x64)    

-   **Windows Embedded 8 Pro** (x86, x64)    

-   **Windows Thin PC** (x86, x64)    

-   **Windows Embedded POSReady 7** (x86, x64)    

-   **Windows Embedded Standard 7 con SP1** (x86, x64)    

-   **WEPOS 1.1 con SP3** (x86)    

-   **Windows Embedded POSReady 2009** (x86)    

-   **Windows Fundamentals para equipos heredados (WinFLP)** (x86)    

-   **Windows XP Embedded SP3** (x86)    

-   **Windows Embedded Standard 2009** (x86)  

## <a name="windows-ce"></a>Windows CE  
 Puede administrar dispositivos de Windows CE con el cliente heredado de dispositivos móviles de Configuration Manager que se incluye con Configuration Manager.  

**Limitaciones y requisitos**  

-   El cliente de dispositivo móvil requiere 0,78 MB de espacio de almacenamiento para instalar el cliente. El registro en el dispositivo móvil puede requerir hasta 256 KB de espacio adicional de almacenamiento.    

-   Las características de estos dispositivos móviles varían según el tipo de cliente y la plataforma. Para obtener información sobre qué funciones de administración de Configuration Manager son compatibles con el cliente heredado de dispositivos móviles, consulte [Elegir una solución de administración de dispositivos para System Center Configuration Manager](../../../core/plan-design/choose-a-device-management-solution.md).  

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

## <a name="mac-computers"></a>Equipos Mac  
 Puede administrar equipos con Mac OS X con el cliente de Configuration Manager para Mac.  

 El paquete de instalación del cliente Mac no se suministra con los medios de Configuration Manager. Puede descargarlo como parte de la descarga de los clientes para sistemas operativos adicionales en el [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

**Limitaciones y requisitos:**  

 Debe usar el cliente de Configuration Manager para Mac (versión 5.0.8333.1 o posterior), que debe descargarse por separado. A diferencia del cliente Windows, el cliente Mac no está incluido en el software de Configuration Manager que se instala. Para descargar el cliente Mac, vaya a [Microsoft System Center Configuration Manager: clientes para sistemas operativos adicionales](http://go.microsoft.com/fwlink/?LinkID=525184).  

 Para obtener más información, consulte [How to deploy clients to Macs in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-macs.md) (Implementar clientes en equipos Mac en System Center Configuration Manager).  

**Versiones admitidas:**  

-   **Mac OS X 10.9** (Mavericks)  

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

##  <a name="a-namebkmklinuxosa-linux-and-unix-servers"></a><a name="bkmk_LinuxOS"></a> Servidores Linux y UNIX  
 Puede administrar servidores Linux y UNIX con el cliente de Configuration Manager para Linux y UNIX.  

 Los paquetes de instalación del cliente Linux y UNIX no se suministran con los medios de Configuration Manager. Puede descargarlos como parte de la descarga de los clientes para sistemas operativos adicionales en el [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). Además de los paquetes de instalación de cliente, la descarga de cliente incluye el script de instalación que administra la instalación del cliente en cada equipo.  

**Limitaciones y requisitos:**  

-   Para consultar las dependencias de archivo del sistema operativo para el cliente Linux y UNIX, consulte [Requisitos previos para la implementación del cliente en servidores UNIX y Linux](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  

-   Para obtener información general de las capacidades de administración compatibles con equipos que ejecutan Linux o UNIX, consulte [Implementar clientes en servidores UNIX y Linux con System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

-   En versiones compatibles de Linux y UNIX, la versión enumerada incluye todas las posteriores versiones secundarias. Por ejemplo, cuando se indica compatibilidad con CentOS versión 6, también se incluyen las posteriores versiones secundarias de CentOS 6, como CentOS 6.3. De forma similar, cuando se indica compatibilidad con un sistema operativo que usa Service Packs, por ejemplo, SUSE Linux Enterprise Server 11 SP1, se incluyen los posteriores Service Packs para esa versión del sistema operativo.  

-   Para obtener información sobre los paquetes de instalación de cliente y el agente universal, consulte [Implementar clientes en servidores UNIX y Linux con System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

**Versiones compatibles:** las siguientes versiones se admiten mediante el archivo .tar indicado.  

### <a name="aix"></a>AIX  

|||  
|-|-|  
|Versión 5.3 (Power)|ccm-Aix53ppc.&lt;compilación\>.tar|  
|Versión 6.1 (Power)|ccm-Aix61ppc.&lt;compilación\>.tar|  
|Versión 7.1 (Power)|ccm-Aix71ppc.&lt;compilación\>.tar|  

### <a name="centos"></a>CentOS  

|||  
|-|-|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  

### <a name="debian"></a>Debian  

|||  
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

|||  
|-|-|  
|Versión 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;compilación\>.tar|  
|Versión 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;compilación\>.tar|  
|Versión 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;compilación\>.tar|  
|Versión 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;compilación\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|||  
|-|-|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|||  
|-|-|  
|Versión 4 x86|ccm-RHEL4x86.&lt;compilación\>.tar|  
|Versión 4 x64|ccm-RHEL4x64.&lt;compilación\>.tar|  
|Versión 5 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 5 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 6 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 6 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 7 x64|ccm-Universalx64.&lt;compilación\>.tar|  

### <a name="solaris"></a>Solaris  

|||  
|-|-|  
|Versión 9 SPARC|ccm-Sol9sparc.&lt;compilación\>.tar|  
|Versión 10 x86|ccm-Sol10x86.&lt;compilación\>.tar|  
|Versión 10 SPARC|ccm-Sol10sparc.&lt;compilación\>.tar|  
|Versión 11 x86|ccm-Sol11x86.&lt;compilación\>.tar|  
|Versión 11 SPARC|ccm-Sol11sparc.&lt;compilación\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|||  
|-|-|  
|Versión 9 x86|ccm-SLES9x86.&lt;compilación\>.tar|  
|Versión 10 SP1 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 10 SP1 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 11 SP1 x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 11 SP1 x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 12 x64|ccm-Universalx64.&lt;compilación\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|||  
|-|-|  
|Versión 10.04 LTS x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 10.04 LTS x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 12.04 LTS x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 12.04 LTS x64|ccm-Universalx64.&lt;compilación\>.tar|  
|Versión 14.04 LTS x86|ccm-Universalx86.&lt;compilación\>.tar|  
|Versión 14.04 LTS x64|ccm-Universalx64.&lt;compilación\>.tar|  

##  <a name="a-namebkmkintuneosa-mobile-devices-enrolled-by-microsoft-intune"></a><a name="bkmk_IntuneOS"></a> Dispositivos móviles inscritos por Microsoft Intune  
 Para obtener más información sobre los equipos y dispositivos que puede administrar al integrar Microsoft Intune con Configuration Manager, consulte los dos temas siguientes en la biblioteca de documentación de Microsoft Intune:  

-   [Capacidades de administración de dispositivos móviles en Microsoft Intune](https://docs.microsoft.com/intune/get-started/choose-how-to-manage-devices)  
-   [Funciones de administración de equipos Windows en Microsoft Intune](https://docs.microsoft.com/intune/get-started/windows-pc-management-capabilities-in-microsoft-intune)  

##  <a name="a-namebkmkonpremosa-on-premises-mobile-device-management"></a><a name="bkmk_OnpremOS"></a> Administración local de dispositivos móviles  
 Configuration Manager incorpora funcionalidades para administrar dispositivos locales sin necesidad de instalar software cliente.  Para obtener más información, consulte [Administrar dispositivos móviles con la infraestructura local en System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Limitaciones y requisitos:**  

-   Debe configurar el **punto de conexión de servicio** en el sitio de nivel superior de la jerarquía  

 **Sistemas operativos compatibles:**  

-   **Windows 10 Pro** (x86, x64)  

-   **Windows 10 Pro Enterprise** (x86, x64)  

-   **Windows 10 IoT Enterprise** (x86, x64)

-   **Windows 10 Mobile**  

-   **Windows 10 Mobile Enterprise**  

-  **Windows 10 IoT Mobile Enterprise**

##  <a name="a-namebkmkexsrvconosa-exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a> Conector de Exchange Server  
 Configuration Manager admite la administración limitada de dispositivos que se conectan a Exchange Server, sin instalar software cliente.  Para obtener más información, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

 **Limitaciones y requisitos:**  

-   Configuration Manager ofrece administración limitada para dispositivos móviles cuando se usa el conector de Exchange Server para los dispositivos compatibles con Exchange Active Sync (EAS) que se conectan a un servidor que ejecuta Exchange Server o Exchange Online.  

-   Para obtener más información sobre las funciones de administración que admite Configuration Manager para los dispositivos móviles que administra el conector de Exchange Server, consulte Determinar cómo administrar dispositivos móviles en Configuration Manager.  

**Versiones admitidas de Exchange Server:**  

-   **Exchange Server 2010 SP1**  

-   **Exchange Server 2010 SP2**  

-   **Exchange Server 2013**  

-   **Exchange Online (Office 365):** incluye Business Productivity Online Standard Suite  



<!--HONumber=Nov16_HO1-->


