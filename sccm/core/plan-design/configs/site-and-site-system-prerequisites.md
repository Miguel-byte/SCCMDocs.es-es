---
title: Requisitos previos del sitio
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo configurar un equipo Windows como un servidor de sistema de sitio de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e8f575fc609dea662688ed10a76733467784a5b9
ms.sourcegitcommit: d5c013a29f53b975fe3a6cb0a41f1e817bd7b235
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/16/2019
ms.locfileid: "54342812"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Sitio y requisitos previos de sistema de sitio para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los equipos basados en Windows requieren configuraciones específicas para poder usarse como servidores de sistema de sitio de Configuration Manager. 

Este artículo se centra principalmente en [Windows Server 2012 y versiones posteriores](#bkmk_2012Prereq). [Windows Server 2008 R2 y Windows Server 2008](#bkmk_2008) son compatibles con el rol de sistema de sitio de punto de distribución. Para obtener más información, vea [Sistemas operativos compatibles con servidores de sistema de sitio](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers). 

Para algunos productos, como Windows Server Update Services (WSUS) para el punto de actualización de software, debe consultar la documentación del producto para identificar los requisitos previos y limitaciones adicionales de uso. Aquí solo se incluyen las configuraciones que se aplican directamente al uso con Configuration Manager.   

> [!NOTE]  
>  En enero de 2016 caducó el soporte para .NET Framework 4.0, 4.5 y 4.5.1. Para obtener más información, vea [Preguntas frecuentes del ciclo de vida: .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update).  



## <a name="bkmk_generalprerewq"></a> Limitaciones y requisitos generales

Se aplican a todos los requisitos a todos los servidores de sistema de sitio:

- Cada servidor de sistema de sitio debe usar un sistema operativo de 64 bits. La única excepción es el rol de sistema de sitio de punto de distribución, que puede instalar en algunos sistemas operativos de 32 bits.  

- Los sistemas de sitio no se admiten en las instalaciones de Server Core de ningún sistema operativo. Una excepción son las instalaciones Server Core, que se admiten para el rol de sistema de sitio de punto de distribución. Para obtener más información, vea [Sistemas operativos compatibles con servidores de sistema de sitio de Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  

- Después de que se instala un servidor de sistema de sitio, no se permite cambiar:  

    - El nombre del dominio en el que se encuentra el equipo del sistema de sitio (también conocido como **cambio de nombre de dominio**).  

    - La pertenencia del equipo al dominio.  

    - Nombre del equipo.  

  Si necesita cambiar cualquiera de estos elementos, primero quite el rol de sistema de sitio del equipo. Después vuelva a instalar el rol una vez se haya completado el cambio. Para los cambios que afectan al servidor del sitio, primero debe desinstalar el sitio. Después vuelva a instalar el sitio una vez se haya completado el cambio.  

- Los roles de sistema de sitio no se admiten en una instancia de un clúster de Windows Server. La única excepción a esto es el servidor de base de datos del sitio. Para obtener más información, vea [Usar un clúster de SQL Server para la base de datos de sitio de Configuration Manager](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database).  

- No se permite cambiar la configuración de tipo de inicio o de inicio de sesión de ningún servicio de Configuration Manager. Si hace esto, es posible que impida que servicios clave se ejecuten correctamente.  


###  <a name="bkmk_2012Prereq"></a> Requisitos previos para Windows Server 2012 y sistemas operativos posteriores  

Vea las secciones principales de este artículo para obtener información sobre los requisitos previos específicos para los servidores de sistema de sitio y roles en Windows Server 2012 y versiones posteriores:

- [Servidores de sitio de administración central y sitio primario](#bkmk_2012sspreq)
- [Servidor de sitio secundario](#bkmk_2012secpreq)
- [Servidor de bases de datos](#bkmk_2012dbpreq)
- [Servidor de proveedor de SMS](#bkmk_2012smsprovpreq)
- [Punto de sitios web del catálogo de aplicaciones](#bkmk_2012acwspreq)
- [Punto de servicio web del catálogo de aplicaciones](#bkmk_2012ACwsitepreq)
- [Punto de sincronización de Asset Intelligence](#bkmk_2012AIpreq)
- [Punto de registro de certificados](#bkmk_2012crppreq)
- [Punto de distribución](#bkmk_2012dppreq)
- [Punto de Endpoint Protection](#bkmk_2012EPPpreq)
- [Punto de inscripción](#bkmk_2012Enrollpreq)
- [Punto de proxy de inscripción](#bkmk_2012EnrollProxpreq)
- [Punto de estado de reserva](#bkmk_2012FSPpreq)
- [Punto de administración](#bkmk_2012MPpreq)
- [Punto de servicios de informes](#bkmk_2012RSpoint)
- [Punto de conexión de servicio](#bkmk_SCPpreq)
- [Punto de actualización de software](#bkmk_2012SUPpreq)
- [Punto de migración de estado](#bkmk_2012SMPpreq)

##  <a name="bkmk_2012sspreq"></a> Servidores de sitio de administración central y sitio primario 

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

- .NET framework 3.5 SP1 (o posterior)  

- .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2  

    - Para obtener más información sobre las versiones de .NET Framework, vea [Versiones y dependencias de .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- Compresión diferencial remota  

#### <a name="windows-adk"></a>Windows ADK  

- Antes de instalar o actualizar un sitio de administración central o un sitio primario, instale la versión de Windows Assessment and Deployment Kit (ADK) que requiere la versión de Configuration Manager que va a instalar o actualizar. Para obtener más información, vea [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).  

- Para obtener más información sobre este requisito, consulte [Requisitos de infraestructura para la implementación de sistema operativo en System Center Configuration Manager](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

#### <a name="visual-c-redistributable"></a>Visual C++ Redistributable  

- Configuration Manager instala el paquete redistribuible de Microsoft Visual C++ 2013 en cada equipo que instala un servidor de sitio.  

- Los sitios de administración central y sitios primarios requieren las versiones x86 y x64 del archivo redistribuible aplicable.  



##  <a name="bkmk_2012secpreq"></a> Servidor de sitio secundario   

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

- .NET framework 3.5 SP1 (o posterior)  

- .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2  

    - Para obtener más información sobre las versiones de .NET Framework, vea [Versiones y dependencias de .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).  

- Compresión diferencial remota  

#### <a name="visual-c-redistributable"></a>Visual C++ Redistributable  

- Configuration Manager instala el paquete redistribuible de Microsoft Visual C++ 2013 en cada equipo que instala un servidor de sitio.  

- Los sitios secundarios solo requieren la versión x64.  

#### <a name="default-site-system-roles"></a>Roles de sistema de sitio predeterminados  

- De manera predeterminada, un sitio secundario instala un **punto de administración** y un **punto de distribución**.  

- Asegúrese de que el servidor de sitio secundario cumple los requisitos previos para estos roles de sistema de sitio.  



##  <a name="bkmk_2012dbpreq"></a> Servidor de bases de datos  

#### <a name="remote-registry-service"></a>Servicio de Registro remoto  

- Durante la instalación del sitio de Configuration Manager, habilite el servicio de **Registro remoto** en el equipo que hospeda la base de datos del sitio.  

#### <a name="sql-server"></a>SQL Server  

- Antes de instalar un sitio de administración central o un sitio primario, instale una versión compatible de SQL Server para hospedar la base de datos del sitio. Para obtener más información, vea [Versiones de SQL Server compatibles](/sccm/core/plan-design/configs/support-for-sql-server-versions).  

- Antes de instalar un sitio secundario, puede instalar una versión compatible de SQL Server.  

- Si decide que Configuration Manager instale SQL Server Express como parte de la instalación del sitio secundario, asegúrese de que el equipo cumple los requisitos para ejecutar SQL Server Express.  



##  <a name="bkmk_2012smsprovpreq"></a> Servidor de proveedor de SMS  

#### <a name="windows-adk"></a>Windows ADK  

- El equipo en el que instale una instancia del proveedor de SMS debe tener la versión adecuada de Windows ADK que requiere la versión de Configuration Manager que va a instalar o actualizar. Para obtener más información, vea [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).  

- Para obtener más información sobre este requisito, consulte [Requisitos de infraestructura para la implementación de sistema operativo en System Center Configuration Manager](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  



##  <a name="bkmk_2012acwspreq"></a> Punto de sitios web del catálogo de aplicaciones  

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

- .NET framework 3.5 SP1 (o posterior)  

- .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2  

    - ASP.NET 4.5  

    - Para obtener más información sobre las versiones de .NET Framework, vea [Versiones y dependencias de .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).  


#### <a name="iis-configuration"></a>Configuración de IIS  

-   Características HTTP comunes:  

    -   Documento predeterminado  

    -   Contenido estático  

-   Desarrollo de aplicaciones:  

    -   ASP.NET 3.5 (y las opciones seleccionadas automáticamente)  

    -   ASP.NET 4.5 (y las opciones seleccionadas automáticamente)  

    -   Extensibilidad de .NET 3.5  

    -   Extensibilidad de .NET 4.5  

-   Seguridad:  

    -   Autenticación de Windows  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  



##  <a name="bkmk_2012ACwsitepreq"></a> Punto de servicio web del catálogo de aplicaciones  

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

-   .NET framework 3.5 SP1 (o posterior)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2:  

    -   ASP.NET 4.5:  

        -   Activación HTTP (y las opciones seleccionadas automáticamente)  

#### <a name="iis-configuration"></a>Configuración de IIS  

-   Características HTTP comunes:  

    -   Documento predeterminado  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

-   Desarrollo de aplicaciones:  

    -   ASP.NET 3.5 (y las opciones seleccionadas automáticamente)  

    -   Extensibilidad de .NET 3.5  

    -   ASP.NET 4.5 (y las opciones seleccionadas automáticamente)  

    -   Extensibilidad de .NET 4.5  

#### <a name="computer-memory"></a>Memoria del equipo  

-   El equipo que hospeda este rol de sistema de sitio debe tener libre, como mínimo, el 5 % de la memoria disponible en el equipo para permitir que el rol de sistema de sitio procese las solicitudes.  

-   Una vez colocado el rol de sistema de sitio junto con otro rol de sistema de sitio que tiene este mismo requisito, este requisito de memoria para el equipo no aumenta, pero se mantiene en un mínimo de 5 %.  



##  <a name="bkmk_2012AIpreq"></a> Punto de sincronización de Asset Intelligence  

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2 



##  <a name="bkmk_2012crppreq"></a> Punto de registro de certificados  

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2:  

    -   Activación HTTP  

#### <a name="iis-configuration"></a>Configuración de IIS  

-   Desarrollo de aplicaciones:  

    -   ASP.NET 3.5 (y las opciones seleccionadas automáticamente)  

    -   ASP.NET 4.5 (y las opciones seleccionadas automáticamente)  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

    -   Compatibilidad con WMI de IIS 6  



##  <a name="bkmk_2012dppreq"></a> Punto de distribución  

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

-   Compresión diferencial remota  

#### <a name="iis-configuration"></a>Configuración de IIS  

-   Desarrollo de aplicaciones:  

    -   Extensiones ISAPI  

-   Seguridad:  

    -   Autenticación de Windows  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

    -   Compatibilidad con WMI de IIS 6  

#### <a name="powershell"></a>PowerShell  

-   En Windows Server 2012 o posterior, se requiere PowerShell 3.0 o 4.0 antes de instalar el punto de distribución.  

#### <a name="visual-c-redistributable"></a>Visual C++ Redistributable  

-   Configuration Manager instala el paquete redistribuible de Microsoft Visual C++ 2013 en cada equipo que hospeda un punto de distribución.  

-   La versión que se instala depende de la plataforma del equipo (x86 o x64).  

#### <a name="microsoft-azure"></a>Microsoft Azure  

-   Puede usar un servicio en la nube de Microsoft Azure para hospedar un punto de distribución.  

#### <a name="to-support-pxe-or-multicast"></a>Para admitir un entorno PXE o multidifusión  

-   Instale y configure el rol de servidor de Windows Servicios de implementación de Windows (WDS).  

    > [!NOTE]  
    >  WDS se instala y configura de forma automática cuando se configura un punto de distribución para que admita un entorno PXE o multidifusión en un servidor que ejecuta Windows Server 2012 o una versión posterior.  

-   A partir de la versión 1806, un respondedor PXE se habilita en un punto de distribución sin Servicios de implementación de Windows.  

Para obtener más información, vea [Instalación y configuración de puntos de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Cuando el punto de distribución transfiere contenido, realiza la transferencia mediante el **Servicio de transferencia inteligente en segundo plano** (BITS) integrado en Windows. El rol de punto de distribución no requiere que la característica Extensión de servidor IIS de BITS opcional esté instalada porque el cliente no carga la información en ella.  



##  <a name="bkmk_2012EPPpreq"></a> Punto de Endpoint Protection  

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

-   .NET framework 3.5 SP1 (o posterior)  

-   Características de Windows Defender (Windows Server 2016 o posterior)  



##  <a name="bkmk_2012Enrollpreq"></a> Punto de inscripción  

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

-   .NET Framework 3.5 (or later)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2:  

     Cuando se instala este rol de sistema de sitio, Configuration Manager instala automáticamente .NET Framework 4.5.2. Esta instalación puede colocar el servidor en un estado de reinicio pendiente. Si hay un reinicio pendiente para .NET Framework, es posible que las aplicaciones .NET produzcan un error después de que se reinicia el servidor y finaliza la instalación.  

    -   Activación HTTP (y las opciones seleccionadas automáticamente)  

    -   ASP.NET 4.5  

#### <a name="iis-configuration"></a>Configuración de IIS  

-   Características HTTP comunes:  

    -   Documento predeterminado  

-   Desarrollo de aplicaciones:  

    -   ASP.NET 3.5 (y las opciones seleccionadas automáticamente)  

    -   Extensibilidad de .NET 3.5  

    -   ASP.NET 4.5 (y las opciones seleccionadas automáticamente)  

    -   Extensibilidad de .NET 4.5  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

#### <a name="computer-memory"></a>Memoria del equipo  

-   El equipo que hospeda este rol de sistema de sitio debe tener libre, como mínimo, el 5 % de la memoria disponible en el equipo para permitir que el rol de sistema de sitio procese las solicitudes.  

-   Una vez colocado el rol de sistema de sitio junto con otro rol de sistema de sitio que tiene este mismo requisito, este requisito de memoria para el equipo no aumenta, pero se mantiene en un mínimo de 5 %.  



##  <a name="bkmk_2012EnrollProxpreq"></a> Punto de proxy de inscripción  

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

-   .NET Framework 3.5 (or later)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2 

     Cuando se instala este rol de sistema de sitio, Configuration Manager instala automáticamente .NET Framework 4.5.2. Esta instalación puede colocar el servidor en un estado de reinicio pendiente. Si hay un reinicio pendiente para .NET Framework, es posible que las aplicaciones .NET produzcan un error después de que se reinicia el servidor y se completa la instalación.  

#### <a name="iis-configuration"></a>Configuración de IIS  

-   Características HTTP comunes:  

    -   Documento predeterminado  

    -   Contenido estático  

-   Desarrollo de aplicaciones:  

    -   ASP.NET 3.5 (y las opciones seleccionadas automáticamente)  

    -   ASP.NET 4.5 (y las opciones seleccionadas automáticamente)  

    -   Extensibilidad de .NET 3.5  

    -   Extensibilidad de .NET 4.5  

-   Seguridad:  

    -   Autenticación de Windows  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

#### <a name="computer-memory"></a>Memoria del equipo  

-   El equipo que hospeda este rol de sistema de sitio debe tener libre, como mínimo, el 5 % de la memoria disponible en el equipo para permitir que el rol de sistema de sitio procese las solicitudes.  

-   Una vez colocado el rol de sistema de sitio junto con otro rol de sistema de sitio que tiene este mismo requisito, este requisito de memoria para el equipo no aumenta, pero se mantiene en un mínimo de 5 %.  



##  <a name="bkmk_2012FSPpreq"></a> Punto de estado de reserva 

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server 

-   Las extensiones de servidor BITS (y las opciones seleccionadas automáticamente) o los servicios de transferencia inteligente en segundo plano (BITS) (y las opciones seleccionadas automáticamente) 

#### <a name="iis-configuration"></a>Configuración de IIS 

Se requiere la configuración de IIS predeterminada con las siguientes adiciones:  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  



##  <a name="bkmk_2012MPpreq"></a> Punto de administración  

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2 

-   Las extensiones de servidor BITS (y las opciones seleccionadas automáticamente) o los servicios de transferencia inteligente en segundo plano (BITS) (y las opciones seleccionadas automáticamente)  

#### <a name="iis-configuration"></a>Configuración de IIS  

-   Desarrollo de aplicaciones:  

    -   Extensiones ISAPI  

-   Seguridad:  

    -   Autenticación de Windows  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

    -   Compatibilidad con WMI de IIS 6  



##  <a name="bkmk_2012RSpoint"></a> Punto de servicios de informes  

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2 

#### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  

-   Instale y configure al menos una instancia de SQL Server para que sea compatible con SQL Server Reporting Services antes de instalar el punto de notificación.  

-   La instancia que se usa para SQL Server Reporting Services puede ser la misma instancia que se usa para la base de datos del sitio.  

-   Además, la instancia que se usa puede compartirse con otros productos de System Center, siempre y cuando los otros productos de System Center no tengan restricciones para el uso compartido de la instancia de SQL Server.  



##  <a name="bkmk_SCPpreq"></a> Punto de conexión de servicio  

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2 

     Cuando se instala este rol de sistema de sitio, Configuration Manager instala automáticamente .NET Framework 4.5.2. Esta instalación puede colocar el servidor en un estado de reinicio pendiente. Si hay un reinicio pendiente para .NET Framework, es posible que las aplicaciones .NET produzcan un error después de que se reinicia el servidor y finaliza la instalación.  

#### <a name="visual-c-redistributable"></a>Visual C++ Redistributable  

-   Configuration Manager instala el paquete redistribuible de Microsoft Visual C++ 2013 en cada equipo que hospeda un punto de distribución.  

-   El rol de sistema de sitio requiere la versión x64.  



##  <a name="bkmk_2012SUPpreq"></a> Punto de actualización de software  

#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

-   .NET framework 3.5 SP1 (o posterior)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2 

Requiere la configuración predeterminada de IIS.

#### <a name="windows-server-update-services"></a>Windows Server Update Services  

-   Instale el rol de servidor de Windows, Windows Server Update Services, en un equipo antes de instalar un punto de actualización de software.  

-   Para obtener más información, vea [Planear actualizaciones de software](/sccm/sum/plan-design/plan-for-software-updates).  



##  <a name="bkmk_2012SMPpreq"></a> Punto de migración de estado  
<!--SCCMDocs issue 645-->
#### <a name="windows-server-roles-and-features"></a>Roles y características de Windows Server  

-   .NET Framework 3.5 (or later)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2:  

     Cuando se instala este rol de sistema de sitio, Configuration Manager instala automáticamente .NET Framework 4.5.2. Esta instalación puede colocar el servidor en un estado de reinicio pendiente. Si hay un reinicio pendiente para .NET Framework, es posible que las aplicaciones .NET produzcan un error después de que se reinicia el servidor y finaliza la instalación.  

    -   Activación HTTP (y las opciones seleccionadas automáticamente)  

    -   ASP.NET 4.5  

#### <a name="iis-configuration"></a>Configuración de IIS  

-   Características HTTP comunes:  

    -   Documento predeterminado  

-   Desarrollo de aplicaciones:  

    -   ASP.NET 3.5 (y las opciones seleccionadas automáticamente)  

    -   Extensibilidad de .NET 3.5  

    -   ASP.NET 4.5 (y las opciones seleccionadas automáticamente)  

    -   Extensibilidad de .NET 4.5  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  



##  <a name="bkmk_2008"></a> Requisitos previos para Windows Server 2008 R2 y Windows Server 2008  

Windows Server 2008 y Windows Server 2008 R2 tienen ahora soporte extendido y ya no están dentro del soporte estándar, tal y como se detalla en el [Ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle). Para obtener más información sobre la compatibilidad futura de estos sistemas operativos como servidores de sistema de sitio con Configuration Manager, consulte [Removed and deprecated server operating systems](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems) (Sistemas operativos de servidor eliminados y en desuso).  

Estas versiones de sistema operativo no son compatibles con servidores de sitio o la mayoría de los roles del sistema de sitio. Todavía se admiten para el rol de sistema de sitio del punto de distribución, incluidos los puntos de distribución de extracción y para el entorno PXE y la multidifusión.


###  <a name="bkmk_2008dppreq"></a> Punto de distribución  

#### <a name="iis-configuration"></a>Configuración de IIS

Puede usar la configuración predeterminada de IIS o una configuración personalizada. Para usar una configuración personalizada de IIS, debe habilitar las siguientes opciones para IIS:  

-   Desarrollo de aplicaciones:  

    -   Extensiones ISAPI  

-   Seguridad:  

    -   Autenticación de Windows  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

    -   Compatibilidad con WMI de IIS 6  

Cuando se usa una configuración personalizada de IIS, puede quitar las opciones que no son necesarias, como los siguientes elementos:  

-   Características HTTP comunes:  

    -   Redirección HTTP  

-   Scripts y herramientas de administración de IIS  

#### <a name="windows-feature"></a>Característica de Windows  

-   Compresión diferencial remota  

#### <a name="visual-c-redistributable"></a>Visual C++ Redistributable  

-   Configuration Manager instala el paquete redistribuible de Microsoft Visual C++ 2013 en cada equipo que hospeda un punto de distribución.  

-   La versión que se instala depende de la plataforma del equipo (x86 o x64).  

#### <a name="microsoft-azure"></a>Microsoft Azure  

-   Puede usar un servicio en la nube en Azure para hospedar un punto de distribución.  

#### <a name="to-support-pxe-or-multicast"></a>Para admitir un entorno PXE o multidifusión  

-   Instale y configure el rol de servidor de Windows Servicios de implementación de Windows (WDS).  

    > [!NOTE]  
    >  WDS se instala y configura de forma automática cuando se configura un punto de distribución para que admita un entorno PXE o multidifusión en un servidor que ejecuta Windows Server 2012 o una versión posterior.  

-   A partir de la versión 1806, un respondedor PXE se habilita en un punto de distribución sin Servicios de implementación de Windows.  

Para obtener más información, vea [Instalación y configuración de puntos de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Cuando el punto de distribución transfiere contenido, realiza la transferencia mediante el **Servicio de transferencia inteligente en segundo plano** (BITS) integrado en el sistema operativo Windows. El rol de punto de distribución no requiere que la característica Extensión de servidor IIS de BITS opcional esté instalada porque el cliente no carga la información en ella.   

