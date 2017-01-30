---
title: Requisitos previos del sitio | Microsoft Docs
description: "Obtenga información sobre cómo configurar un equipo Windows como un servidor de sistema de sitio de System Center Configuration Manager."
ms.custom: na
ms.date: 1/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 42549b98dd7f418cc3f4543198aaeb90ea8a3efd
ms.openlocfilehash: 0b1d2d619d6cdaf36cc22ef461ea1505b5cacc41

---
# <a name="site-and-site-system-prerequisites-for-system-center-configuration-manager"></a>Requisitos previos de sitio y sistema de sitio para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


 Los equipos basados en Windows requieren configuraciones específicas para poder usarse como servidores de sistema de sitio de System Center Configuration Manager.  


 Para algunos productos, como Windows Server Update Services (WSUS) para el punto de actualización de software, debe consultar la documentación del producto para identificar los requisitos previos y limitaciones adicionales de uso de ese producto. Aquí solo se incluyen las configuraciones que se aplican directamente al uso con Configuration Manager.   

> [!NOTE]  
>  En enero de 2016 caducó el soporte para .NET Framework 4.0, 4.5 y 4.5.1. Para más información, consulte [Preguntas más frecuentes de la directiva del ciclo de vida de soporte técnico de Microsoft de .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) en support.microsoft.com.  

## <a name="a-namebkmkgeneralprerewqa-general-site-server-requirements-and-limitations"></a><a name="bkmk_generalprerewq"></a> Requisitos y limitaciones generales del servidor de sitio
**Se aplican a todos los tipos de servidores de sistema de sitio:**

-   Cada servidor de sistema de sitio debe usar un sistema operativo de 64 bits. La única excepción a esta regla es el rol de sistema de sitio de punto de distribución, que puede instalar en algunos sistemas operativos de 32 bits.  

-   Los sistemas de sitio no se admiten en las instalaciones de Server Core de ningún sistema operativo. Una excepción a esta regla son las instalaciones Server Core, que se admiten para el rol de sistema de sitio de punto de distribución, sin compatibilidad con PXE o multidifusión.  

-   Después de que se instala un servidor de sistema de sitio, no se permite cambiar:  

    -   El nombre del dominio en el que se encuentra el equipo del sistema de sitio (también conocido como **cambio de nombre de dominio**).  

    -   La pertenencia del equipo al dominio.  

    -   Nombre del equipo.  

  Si necesita cambiar cualquiera de ellos, primero debe quitar el rol de sistema de sitio del equipo y luego volver a instalarlo una vez completado el cambio. Si esto afecta al equipo de servidor del sitio, debe desinstalar el sitio y, a continuación, volver a instalar el sitio una vez completado el cambio.  

-   Los roles de sistema de sitio no se admiten en una instancia de un clúster de Windows Server. La única excepción a esto es el servidor de base de datos del sitio.  

-   No se permite cambiar la configuración de tipo de inicio o de inicio de sesión de ningún servicio de Configuration Manager. Si hace esto, es posible que impida que servicios clave se ejecuten correctamente.  

##  <a name="a-namebkmk2012prereqa-prerequisites-for-windows-server-2012-and-later-operating-systems"></a><a name="bkmk_2012Prereq"></a> Requisitos previos para Windows Server 2012 y sistemas operativos posteriores  
###  <a name="a-namebkmk2012sspreqa-site-server-central-administration-site-and-primary-site"></a><a name="bkmk_2012sspreq"></a> Servidor de sitio: sitio de administración central y sitio primario  
  **Roles y características de Windows Server:**  

-   .NET framework 3.5 SP1 (o posterior)  

-   .NET Framework 4.5.2  

-   Compresión diferencial remota  

**Windows ADK:**  

-   Antes de instalar o actualizar un sitio de administración central o un sitio primario, debe instalar la versión de Windows Assessment and Deployment Kit (ADK) que requiere la versión de Configuration Manager que va a instalar o actualizar.  

    -   La versión 1511 de Configuration Manager requiere la versión Windows 10 RTM (10.0.10240) de Windows ADK.  

-   Para obtener más información sobre este requisito, consulte [Requisitos de infraestructura para la implementación de sistema operativo en System Center Configuration Manager](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

**Visual C++ Redistributable:**  

-   Configuration Manager instala el paquete redistribuible de Microsoft Visual C++ 2013 en cada equipo que instala un servidor de sitio.  

-   Los sitios de administración central y sitios primarios requieren las versiones x86 y x64 del archivo redistribuible aplicable.  

###  <a name="a-namebkmk2012secpreqa-site-server-secondary-site"></a><a name="bkmk_2012secpreq"></a> Servidor de sitio: sitio secundario  
**Roles y características de Windows Server:**  

-   .NET framework 3.5 SP1 (o posterior)  

-   .NET Framework 4.5.2  

-   Compresión diferencial remota  

**Visual C++ Redistributable:**  

-   Configuration Manager instala el paquete redistribuible de Microsoft Visual C++ 2013 en cada equipo que instala un servidor de sitio.  

-   Los sitios secundarios solo requieren la versión x64.  

**Roles de sistema de sitio predeterminados:**  

-   De manera predeterminada, un sitio secundario instala un **punto de administración** y un **punto de distribución**.  

-   Asegúrese de que el servidor de sitio secundario cumple los requisitos previos para estos roles de sistema de sitio.  

###  <a name="a-namebkmk2012dbpreqa-database-server"></a><a name="bkmk_2012dbpreq"></a> Servidor de bases de datos  
**Servicio de Registro remoto:**  

-   Durante la instalación del sitio de Configuration Manager, debe habilitar el servicio de Registro remoto en el equipo que hospedará la base de datos del sitio.  

**SQL Server:**  

-   Antes de instalar un sitio de administración central o un sitio primario, debe instalar una versión compatible de SQL Server para hospedar la base de datos del sitio.  

-   Antes de instalar un sitio secundario, puede instalar una versión compatible de SQL Server.  

-   Si decide que Configuration Manager instale SQL Server Express como parte de la instalación del sitio secundario, asegúrese de que el equipo cumple los requisitos para ejecutar SQL Server Express.  

###  <a name="a-namebkmk2012smsprovpreqa-sms-provider-server"></a><a name="bkmk_2012smsprovpreq"></a> Servidor de proveedor de SMS  
**Windows ADK:**  

-   El equipo en el que instale una instancia del proveedor de SMS debe tener la versión adecuada de Windows ADK que requiere la versión de Configuration Manager que va a instalar o actualizar.  

    -   La versión 1511 de Configuration Manager requiere la versión Windows 10 RTM (10.0.10240) de Windows ADK.  

-   Para obtener más información sobre este requisito, consulte [Requisitos de infraestructura para la implementación de sistema operativo en System Center Configuration Manager](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

###  <a name="a-namebkmk2012acwspreqa-application-catalog-website-point"></a><a name="bkmk_2012acwspreq"></a> Punto de sitios web del catálogo de aplicaciones  
**Roles y características de Windows Server:**  

-   .NET framework 3.5 SP1 (o posterior)  

-   .NET Framework 4.5.2:  

    -   ASP.NET 4.5  

**Configuración de IIS:**  

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

###  <a name="a-namebkmk2012acwsitepreqa-application-catalog-web-service-point"></a><a name="bkmk_2012ACwsitepreq"></a> Punto de servicio web del catálogo de aplicaciones  
**Roles y características de Windows Server:**  

-   .NET framework 3.5 SP1 (o posterior)  

-   .NET Framework 4.5.2:  

    -   ASP.NET 4.5:  

        -   Activación HTTP (y las opciones seleccionadas automáticamente)  

**Configuración de IIS:**  

-   Características HTTP comunes:  

    -   Documento predeterminado  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

-   Desarrollo de aplicaciones:  

    -   ASP.NET 3.5 (y las opciones seleccionadas automáticamente)  

    -   Extensibilidad de .NET 3.5  

    -   ASP.NET 4.5 (y las opciones seleccionadas automáticamente)  

    -   Extensibilidad de .NET 4.5  

**Memoria del equipo:**  

-   El equipo que hospeda este rol de sistema de sitio debe tener libre, como mínimo, el 5 % de la memoria disponible en el equipo para permitir que el rol de sistema de sitio procese las solicitudes.  

-   Una vez colocado el rol de sistema de sitio junto con otro rol de sistema de sitio que tiene este mismo requisito, este requisito de memoria para el equipo no aumenta, pero se mantiene en un mínimo de 5 %.  

###  <a name="a-namebkmk2012aipreqa-asset-intelligence-synchronization-point"></a><a name="bkmk_2012AIpreq"></a> Punto de sincronización de Asset Intelligence  
**Roles y características de Windows Server:**  

-   .NET Framework 4.5.2  

###  <a name="a-namebkmk2012crppreqa-certificate-registration-point"></a><a name="bkmk_2012crppreq"></a> Punto de registro de certificados  
**Roles y características de Windows Server:**  

-   .NET Framework 4.5.2:  

    -   Activación HTTP  

**Configuración de IIS:**  

-   Desarrollo de aplicaciones:  

    -   ASP.NET 3.5 (y las opciones seleccionadas automáticamente)  

    -   ASP.NET 4.5 (y las opciones seleccionadas automáticamente)  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

    -   Compatibilidad con WMI de IIS 6  

###  <a name="a-namebkmk2012dppreqa-distribution-point"></a><a name="bkmk_2012dppreq"></a> Punto de distribución  
**Roles y características de Windows Server:**  

-   Compresión diferencial remota  

**Configuración de IIS:**  

-   Desarrollo de aplicaciones:  

    -   Extensiones ISAPI  

-   Seguridad:  

    -   Autenticación de Windows  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

    -   Compatibilidad con WMI de IIS 6  

**PowerShell:**  

-   En Windows Server 2012 o posterior, se requiere PowerShell 3.0 o 4.0 antes de instalar el punto de distribución.  

**Visual C++ Redistributable:**  

-   Configuration Manager instala el paquete redistribuible de Microsoft Visual C++ 2013 en cada equipo que hospeda un punto de distribución.  

-   La versión que se instala depende de la plataforma del equipo (x86 o x64).  

**Microsoft Azure:**  

-   Puede usar un servicio en la nube de Microsoft Azure para hospedar un punto de distribución.  

**Para admitir un entorno PXE o multidifusión:**  

-   Instale y configure el rol de servidor de Windows Servicios de implementación de Windows (WDS).  

    > [!NOTE]  
    >  WDS se instala y configura de forma automática cuando se configura un punto de distribución para que admita un entorno PXE o multidifusión en un servidor que ejecuta Windows Server 2012 o una versión posterior.  

> [!NOTE]  
> El rol de sistema de sitio de punto de distribución no requiere el servicio de transferencia inteligente en segundo plano (BITS). Cuando BITS se configura en el equipo de punto de distribución, no se usa BITS en el equipo de punto de distribución para facilitar la descarga de contenido por parte de los clientes que usan BITS.  

###  <a name="a-namebkmk2012epppreqa-endpoint-protection-point"></a><a name="bkmk_2012EPPpreq"></a> Punto de Endpoint Protection  
**Roles y características de Windows Server:**  

-   .NET framework 3.5 SP1 (o posterior)  

###  <a name="a-namebkmk2012enrollpreqa-enrollment-point"></a><a name="bkmk_2012Enrollpreq"></a> Punto de inscripción  
**Roles y características de Windows Server:**  

-   .NET Framework 3.5 (or later)  

-   .NET Framework 4.5.2:  

     Cuando se instala este rol de sistema de sitio, Configuration Manager instala automáticamente .NET Framework 4.5.2. Esta instalación puede colocar el servidor en un estado de reinicio pendiente. Cuando hay un reinicio pendiente para .NET Framework, es posible que las aplicaciones .NET produzcan un error después de que se reinicia el servidor y finaliza la instalación.  

    -   Activación HTTP (y las opciones seleccionadas automáticamente)  

    -   ASP.NET 4.5  


**Configuración de IIS:**  

-   Características HTTP comunes:  

    -   Documento predeterminado  

-   Desarrollo de aplicaciones:  

    -   ASP.NET 3.5 (y las opciones seleccionadas automáticamente)  

    -   Extensibilidad de .NET 3.5  

    -   ASP.NET 4.5 (y las opciones seleccionadas automáticamente)  

    -   Extensibilidad de .NET 4.5  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

**Memoria del equipo:**  

-   El equipo que hospeda este rol de sistema de sitio debe tener libre, como mínimo, el 5 % de la memoria disponible en el equipo para permitir que el rol de sistema de sitio procese las solicitudes.  

-   Una vez colocado el rol de sistema de sitio junto con otro rol de sistema de sitio que tiene este mismo requisito, este requisito de memoria para el equipo no aumenta, pero se mantiene en un mínimo de 5 %.  

###  <a name="a-namebkmk2012enrollproxpreqa-enrollment-proxy-point"></a><a name="bkmk_2012EnrollProxpreq"></a> Punto de proxy de inscripción  
**Roles y características de Windows Server:**  

-   .NET Framework 3.5 (or later)  

-   .NET Framework 4.5.2  

     Cuando se instala este rol de sistema de sitio, Configuration Manager instala automáticamente .NET Framework 4.5.2. Esta instalación puede colocar el servidor en un estado de reinicio pendiente. Cuando hay un reinicio pendiente para .NET Framework, es posible que las aplicaciones .NET produzcan un error después de que se reinicia el servidor y se completa la instalación.  

**Configuración de IIS:**  

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

**Memoria del equipo:**  

-   El equipo que hospeda este rol de sistema de sitio debe tener libre, como mínimo, el 5 % de la memoria disponible en el equipo para permitir que el rol de sistema de sitio procese las solicitudes.  

-   Una vez colocado el rol de sistema de sitio junto con otro rol de sistema de sitio que tiene este mismo requisito, este requisito de memoria para el equipo no aumenta, pero se mantiene en un mínimo de 5 %.  

###  <a name="a-namebkmk2012fsppreqa-fallback-status-point"></a><a name="bkmk_2012FSPpreq"></a> Punto de estado de reserva  
Se requiere la configuración de IIS predeterminada con las siguientes adiciones:  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

###  <a name="a-namebkmk2012mppreqa-management-point"></a><a name="bkmk_2012MPpreq"></a> Punto de administración  
**Roles y características de Windows Server:**  

-   .NET Framework 4.5.2  

-   Las extensiones de servidor BITS (y las opciones seleccionadas automáticamente) o los servicios de transferencia inteligente en segundo plano (BITS) (y las opciones seleccionadas automáticamente)  

**Configuración de IIS:**  

-   Desarrollo de aplicaciones:  

    -   Extensiones ISAPI  

-   Seguridad:  

    -   Autenticación de Windows  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

    -   Compatibilidad con WMI de IIS 6  

###  <a name="a-namebkmk2012rspointa-reporting-services-point"></a><a name="bkmk_2012RSpoint"></a> Punto de servicios de informes  
**Roles y características de Windows Server:**  

-   .NET Framework 4.5.2  

**SQL Server Reporting Services:**  

-   Debe instalar y configurar al menos una instancia de SQL Server para que sea compatible con SQL Server Reporting Services antes de instalar el punto de servicios de informes.  

-   La instancia que se usa para SQL Server Reporting Services puede ser la misma instancia que se usa para la base de datos del sitio.  

-   Además, la instancia que se usa puede compartirse con otros productos de System Center, siempre y cuando los otros productos de System Center no tengan restricciones para el uso compartido de la instancia de SQL Server.  

###  <a name="a-namebkmkscppreqa-service-connection-point"></a><a name="bkmk_SCPpreq"></a> Punto de conexión de servicio  
**Roles y características de Windows Server:**  

-   .NET Framework 4.5.2  

     Cuando se instala este rol de sistema de sitio, Configuration Manager instala automáticamente .NET Framework 4.5.2. Esta instalación puede colocar el servidor en un estado de reinicio pendiente. Cuando hay un reinicio pendiente para .NET Framework, es posible que las aplicaciones .NET produzcan un error después de que se reinicia el servidor y finaliza la instalación.  

**Visual C++ Redistributable:**  

-   Configuration Manager instala el paquete redistribuible de Microsoft Visual C++ 2013 en cada equipo que hospeda un punto de distribución.  

-   El rol de sistema de sitio requiere la versión x64.  

###  <a name="a-namebkmk2012suppreqa-software-update-point"></a><a name="bkmk_2012SUPpreq"></a> Punto de actualización de software  
**Roles y características de Windows Server:**  

-   .NET framework 3.5 SP1 (o posterior)  

-   .NET Framework 4.5.2  

Requiere la configuración predeterminada de IIS.

**Windows Server Update Services:**  

-   Debe instalar el rol de servidor de Windows, Windows Server Update Services, en un equipo antes de instalar un punto de actualización de software.  

-   Para obtener más información, consulte [Planear las actualizaciones de software en System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

### <a name="state-migration-point"></a>Punto de migración de estado  
Requiere la configuración predeterminada de IIS.  

##  <a name="a-namebkmk2008a-prerequisites-for-windows-server-2008-r2-and-windows-server-2008"></a><a name="bkmk_2008"></a> Requisitos previos para Windows Server 2008 R2 y Windows Server 2008  
Windows Server 2008 y Windows Server 2008 R2 tienen ahora soporte extendido y ya no están dentro del soporte estándar, tal y como se detalla en el [Ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle). Para más información sobre la compatibilidad futura de estos sistemas operativos como servidores de sistema de sitio con Configuration Manager, vea [Características eliminadas y en desuso de System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

**La siguiente información es aplicable a todos los requisitos de .NET Framework:**  

-   Instale la versión completa de .NET Framework antes de instalar los roles de sistema de sitio. Por ejemplo, consulte [Microsoft .NET Framework 4 (instalador independiente)](http://go.microsoft.com/fwlink/p/?LinkId=193048). .NET Framework 4 Client Profile no es suficiente para este requisito.  

**La siguiente información es aplicable a todos los requisitos de activación de Windows Communication Foundation (WCF):**  

-   Puede configurar la activación de WCF como parte de la característica de Windows .NET Framework en el servidor de sistema de sitio. Por ejemplo, en Windows Server 2008 R2, ejecute el **Asistente para agregar características** para instalar características adicionales en el servidor. En la página **Seleccionar características**, expanda **Características de NET Framework 3.5.1**, expanda **Activación WCF** y después active las casillas **Activación HTTP** y **Activación no HTTP** para habilitar estas opciones.  

###  <a name="a-namebkmk2008sspreqa-site-server-central-administration-site-and-primary-site"></a><a name="bkmk_2008sspreq"></a> Servidor de sitio: sitio de administración central y sitio primario  
**.NET Framework:**  

-   .NET framework 3.5 SP1 (o posterior)  

-   .NET Framework 4.5.2  

**Característica de Windows:**  

-   Compresión diferencial remota  

**Windows ADK:**  

-   Antes de instalar o actualizar un sitio de administración central o un sitio primario, debe instalar la versión de Windows ADK que requiere la versión de Configuration Manager que va a instalar o actualizar.  

    -   La versión 1511 de Configuration Manager requiere la versión Windows 10 RTM (10.0.10240) de Windows ADK.  

-   Para obtener más información sobre este requisito, consulte [Requisitos de infraestructura para la implementación de sistema operativo en System Center Configuration Manager](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

**Visual C++ Redistributable:**  

-   Configuration Manager instala el paquete redistribuible de Microsoft Visual C++ 2013 en cada equipo que instala un servidor de sitio.  

-   Los sitios de administración central y sitios primarios requieren las versiones x86 y x64 del archivo redistribuible aplicable.  

###  <a name="a-namebkmk2008secpreqa-site-server-secondary-site"></a><a name="bkmk_2008secpreq"></a> Servidor de sitio: sitio secundario  
**.NET Framework:**  

-   .NET framework 3.5 SP1 (o posterior)  

-   .NET Framework 4.5.2  

**Visual C++ Redistributable:**  

-   Configuration Manager instala el paquete redistribuible de Microsoft Visual C++ 2013 en cada equipo que instala un servidor de sitio.  

-   Los sitios secundarios solo requieren la versión x64.  

**Roles de sistema de sitio predeterminados:**  

-   De manera predeterminada, un sitio secundario instala un **punto de administración** y un **punto de distribución**.  

-   Asegúrese de que el servidor de sitio secundario cumple los requisitos previos para estos roles de sistema de sitio.  

###  <a name="a-namebkmk2008dbpreqa-database-server"></a><a name="bkmk_2008dbpreq"></a> Servidor de bases de datos  
**Servicio de Registro remoto:**  

-   Durante la instalación del sitio de Configuration Manager, debe habilitar el servicio de Registro remoto en el equipo que hospedará la base de datos del sitio.  

**SQL Server:**  

-   Antes de instalar un sitio de administración central o un sitio primario, debe instalar una versión compatible de SQL Server para hospedar la base de datos del sitio.  

-   Antes de instalar un sitio secundario, puede instalar una versión compatible de SQL Server.  

-   Si decide que Configuration Manager instale SQL Server Express como parte de la instalación del sitio secundario, asegúrese de que el equipo cumple los requisitos para ejecutar SQL Server Express.  

###  <a name="a-namebkmk2008smsprovpreqa-sms-provider-server"></a><a name="bkmk_2008smsprovpreq"></a> Servidor de proveedor de SMS  
**Windows ADK:**  

-   El equipo en el que instale una instancia del proveedor de SMS debe tener la versión adecuada de Windows ADK que requiere la versión de Configuration Manager que va a instalar o actualizar.  

    -   La versión 1511 de Configuration Manager requiere la versión Windows 10 RTM (10.0.10240) de Windows ADK.  

-   Para obtener más información sobre este requisito, consulte [Requisitos de infraestructura para la implementación de sistema operativo en System Center Configuration Manager](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

###  <a name="a-namebkmk2008acwspreqa-application-catalog-website-point"></a><a name="bkmk_2008acwspreq"></a> Punto de sitios web del catálogo de aplicaciones  
**.NET Framework:**  

-   .NET Framework 4.5.2  

**Configuración de IIS:**

Se requiere la configuración de IIS predeterminada con las siguientes adiciones:  

-   Características HTTP comunes:  

    -   Contenido estático  

    -   Documento predeterminado  

-   Desarrollo de aplicaciones:  

    -   ASP.NET (y las opciones seleccionadas automáticamente)  

         En algunos escenarios, como cuando se instala IIS o se vuelve a configurar tras instalar la versión 4.5.2 de .NET Framework, debe habilitar explícitamente la versión 4.5 de ASP.NET. Por ejemplo, en un equipo de 64 bits que ejecuta la versión 4.0.30319 de .NET Framework, ejecute el siguiente comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

-   Seguridad:  

    -   Autenticación de Windows  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

###  <a name="a-namebkmk2008acwsitepreqa-application-catalog-web-service-point"></a><a name="bkmk_2008ACwsitepreq"></a> Punto de servicio web del catálogo de aplicaciones  
**.NET Framework:**  

-   .NET framework 3.5 SP1 (o posterior)  

-   .NET Framework 4.5.2  

**Activación de Windows Communication Foundation (WCF):**  

-   Activación HTTP  

-   Activación no HTTP  

**Configuración de IIS:**

Se requiere la configuración de IIS predeterminada con las siguientes adiciones:  

-   Desarrollo de aplicaciones:  

    -   ASP.NET (y las opciones seleccionadas automáticamente)  

         En algunos escenarios, como cuando se instala IIS o se vuelve a configurar tras instalar la versión 4.5.2 de .NET Framework, debe habilitar explícitamente la versión 4.5 de ASP.NET. Por ejemplo, en un equipo de 64 bits que ejecuta la versión 4.0.30319 de .NET Framework, ejecute el siguiente comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

**Memoria del equipo:**  

-   El equipo que hospeda este rol de sistema de sitio debe tener libre, como mínimo, el 5 % de la memoria disponible en el equipo para permitir que el rol de sistema de sitio procese las solicitudes.  

-   Una vez colocado el rol de sistema de sitio junto con otro rol de sistema de sitio que tiene este mismo requisito, este requisito de memoria para el equipo no aumenta, pero se mantiene en un mínimo de 5 %.  

###  <a name="a-namebkmk2008aipreqa-asset-intelligence-synchronization-point"></a><a name="bkmk_2008AIpreq"></a> Punto de sincronización de Asset Intelligence  
**.NET Framework:**  

-   .NET Framework 4.5.2  

###  <a name="a-namebkmk2008crppreqa-certificate-registration-point"></a><a name="bkmk_2008crppreq"></a> Punto de registro de certificados  
**.NET Framework:**  

-   .NET Framework 4.5.2  

-   Activación HTTP  

**Configuración de IIS:**

Se requiere la configuración de IIS predeterminada con las siguientes adiciones:  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

    -   Compatibilidad con WMI de IIS 6  

###  <a name="a-namebkmk2008dppreqa-distribution-point"></a><a name="bkmk_2008dppreq"></a> Punto de distribución  
**Configuración de IIS:**

Puede usar la configuración predeterminada de IIS o una configuración personalizada. Para usar una configuración personalizada de IIS, debe habilitar las siguientes opciones para IIS:  

-   Desarrollo de aplicaciones:  

    -   Extensiones ISAPI  

-   Seguridad:  

    -   Autenticación de Windows  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

    -   Compatibilidad con WMI de IIS 6  

Cuando se usa una configuración personalizada de IIS, puede quitar las opciones que no son necesarias, como las siguientes:  

-   Características HTTP comunes:  

    -   Redirección HTTP  

-   Scripts y herramientas de administración de IIS  

**Característica de Windows:**  

-   Compresión diferencial remota  

**Visual C++ Redistributable:**  

-   Configuration Manager instala el paquete redistribuible de Microsoft Visual C++ 2013 en cada equipo que hospeda un punto de distribución.  

-   La versión que se instala depende de la plataforma del equipo (x86 o x64).  

**Microsoft Azure:**  

-   Puede usar un servicio en la nube en Azure para hospedar un punto de distribución.  

**Para admitir un entorno PXE o multidifusión:**  

-   Instale y configure el rol de servidor de Windows Servicios de implementación de Windows (WDS).  

    > [!NOTE]  
    >  WDS se instala y configura de forma automática cuando se configura un punto de distribución para que admita un entorno PXE o multidifusión en un servidor que ejecuta Windows Server 2012 o una versión posterior.  

> [!NOTE]  
> El rol de sistema de sitio de punto de distribución no requiere el servicio de transferencia inteligente en segundo plano (BITS). Cuando BITS se configura en el equipo de punto de distribución, no se usa BITS en el equipo de punto de distribución para facilitar la descarga de contenido por parte de los clientes que usan BITS.  


###  <a name="a-namebkmk2008epppreqa-endpoint-protection-point"></a><a name="bkmk_2008EPPpreq"></a> Punto de Endpoint Protection  
**.NET Framework:**  

-   .NET framework 3.5 SP1 (o posterior)  

###  <a name="a-namebkmk2008enrollpreqa-enrollment-point"></a><a name="bkmk_2008Enrollpreq"></a> Punto de inscripción  
**.NET Framework:**  

-   .NET Framework 4.5.2  

     Cuando se instala este rol de sistema de sitio, si el servidor no tiene ya instalada una versión compatible de .NET Framework, Configuration Manager instala automáticamente .NET Framework 4.5.2. Esta instalación puede colocar el servidor en un estado de reinicio pendiente. Cuando hay un reinicio pendiente para .NET Framework, es posible que las aplicaciones .NET produzcan un error después de que se reinicia el servidor y finaliza la instalación.  

**Activación de Windows Communication Foundation (WCF):**  

-   Activación HTTP  

-   Activación no HTTP  

**Configuración de IIS:**

Se requiere la configuración de IIS predeterminada con las siguientes adiciones:  

-   Desarrollo de aplicaciones:  

    -   ASP.NET (y las opciones seleccionadas automáticamente)  

         En algunos escenarios, como cuando se instala IIS o se vuelve a configurar tras instalar la versión 4.5.2 de .NET Framework, debe habilitar explícitamente la versión 4.5 de ASP.NET. Por ejemplo, en un equipo de 64 bits que ejecuta la versión 4.0.30319 de .NET Framework, ejecute el siguiente comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

**Memoria del equipo:**  

-   El equipo que hospeda este rol de sistema de sitio debe tener libre, como mínimo, el 5 % de la memoria disponible en el equipo para permitir que el rol de sistema de sitio procese las solicitudes.  

-   Una vez colocado el rol de sistema de sitio junto con otro rol de sistema de sitio que tiene este mismo requisito, este requisito de memoria para el equipo no aumenta, pero se mantiene en un mínimo de 5 %.  

###  <a name="a-namebkmk2008enrollproxpreqa-enrollment-proxy-point"></a><a name="bkmk_2008EnrollProxpreq"></a> Punto de proxy de inscripción  
**.NET Framework:**  

-   .NET Framework 4.5.2  

     Cuando se instala este rol de sistema de sitio, si el servidor no tiene ya instalada una versión compatible de .NET Framework, Configuration Manager instala automáticamente .NET Framework 4.5.2. Esta instalación puede colocar el servidor en un estado de reinicio pendiente. Cuando hay un reinicio pendiente para .NET Framework, es posible que las aplicaciones .NET produzcan un error después de que se reinicia el servidor y finaliza la instalación.  

**Activación de Windows Communication Foundation (WCF):**  

-   Activación HTTP  

-   Activación no HTTP  

**Configuración de IIS:**

Se requiere la configuración de IIS predeterminada con las siguientes adiciones:  

-   Desarrollo de aplicaciones:  

    -   ASP.NET (y las opciones seleccionadas automáticamente)  

         En algunos escenarios, como cuando se instala IIS o se vuelve a configurar tras instalar la versión 4.5.2 de .NET Framework, debe habilitar explícitamente la versión 4.5 de ASP.NET. Por ejemplo, en un equipo de 64 bits que ejecuta la versión 4.0.30319 de .NET Framework, ejecute el siguiente comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

**Memoria del equipo:**  

-   El equipo que hospeda este rol de sistema de sitio debe tener libre, como mínimo, el 5 % de la memoria disponible en el equipo para permitir que el rol de sistema de sitio procese las solicitudes.  

-   Una vez colocado el rol de sistema de sitio junto con otro rol de sistema de sitio que tiene este mismo requisito, este requisito de memoria para el equipo no aumenta, pero se mantiene en un mínimo de 5 %.  

###  <a name="a-namebkmk2008fsppreqa-fallback-status-point"></a><a name="bkmk_2008FSPpreq"></a> Punto de estado de reserva  
**Configuración de IIS:**

Se requiere la configuración de IIS predeterminada con las siguientes adiciones:  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

###  <a name="a-namebkmk2008mppreqa-management-point"></a><a name="bkmk_2008MPpreq"></a> Punto de administración  
**.NET Framework:**  

-   .NET Framework 4.5.2  

**Configuración de IIS:**

Puede usar la configuración predeterminada de IIS o una configuración personalizada. Cada punto de administración que se habilita para admitir dispositivos móviles requiere la configuración adicional de IIS para ASP.NET (y sus opciones seleccionadas automáticamente).

En algunos escenarios, como cuando se instala IIS o se vuelve a configurar tras instalar la versión 4.5.2 de .NET Framework, debe habilitar explícitamente la versión 4.5 de ASP.NET. Por ejemplo, en un equipo de 64 bits que ejecuta la versión 4.0.30319 de .NET Framework, ejecute el siguiente comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  


Para usar una configuración personalizada de IIS, debe habilitar las siguientes opciones para IIS:  

-   Desarrollo de aplicaciones:  

    -   Extensiones ISAPI  

-   Seguridad:  

    -   Autenticación de Windows  

-   Compatibilidad con la administración de IIS 6:  

    -   Compatibilidad con la metabase de IIS 6  

    -   Compatibilidad con WMI de IIS 6  


Cuando se usa una configuración personalizada de IIS, puede quitar las opciones que no son necesarias, como las siguientes:  

-   Características HTTP comunes:  

    -   Redirección HTTP  

-   Scripts y herramientas de administración de IIS  

**Característica de Windows:**  

-   Las extensiones de servidor BITS (y las opciones seleccionadas automáticamente) o los servicios de transferencia inteligente en segundo plano (BITS) (y las opciones seleccionadas automáticamente)  

###  <a name="a-namebkmk2008rspointa-reporting-services-point"></a><a name="bkmk_2008RSpoint"></a> Punto de servicios de informes  
**.NET Framework:**  

-   .NET Framework 4.5.2  

**SQL Server Reporting Services:**  

-   Debe instalar y configurar al menos una instancia de SQL Server para que sea compatible con SQL Server Reporting Services antes de instalar el punto de servicios de informes.  

-   La instancia que se usa para SQL Server Reporting Services puede ser la misma instancia que se usa para la base de datos del sitio.  

-   Además, la instancia que se usa puede compartirse con otros productos de System Center, siempre y cuando los otros productos de System Center no tengan restricciones para el uso compartido de la instancia de SQL Server.  

###  <a name="a-namebkmk2008scppreqa-service-connection-point"></a><a name="bkmk_2008SCPpreq"></a> Punto de conexión de servicio  
**.NET Framework:**  

-   .NET Framework 4.5.2  

     Cuando se instala este rol de sistema de sitio, si el servidor no tiene ya instalada una versión compatible de .NET Framework, Configuration Manager instala automáticamente .NET Framework 4.5.2. Esta instalación puede colocar el servidor en un estado de reinicio pendiente. Cuando hay un reinicio pendiente para .NET Framework, es posible que las aplicaciones .NET produzcan un error después de que se reinicia el servidor y finaliza la instalación.  

**Visual C++ Redistributable:**  

-   Configuration Manager instala el paquete redistribuible de Microsoft Visual C++ 2013 en cada equipo que hospeda un punto de distribución.  

-   El rol de sistema de sitio requiere la versión x64.  

###  <a name="a-namebkmk2008suppreqa-software-update-point"></a><a name="bkmk_2008SUPpreq"></a> Punto de actualización de software  
**.NET Framework:**  

-   .NET framework 3.5 SP1 (o posterior)  

-   .NET Framework 4.5.2  

**Configuración de IIS:**

Requiere la configuración predeterminada de IIS.  

**Windows Server Update Services:**  

-   Debe instalar el rol de servidor de Windows, Windows Server Update Services, en un equipo antes de instalar un punto de actualización de software.  

-   Para obtener más información, consulte [Planear las actualizaciones de software en System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).

###  <a name="a-namebkmk2008smppreqa-state-migration-point"></a><a name="bkmk_2008SMPpreq"></a> Punto de migración de estado  
**Configuración de IIS:**

Requiere la configuración predeterminada de IIS.  



<!--HONumber=Jan17_HO3-->


