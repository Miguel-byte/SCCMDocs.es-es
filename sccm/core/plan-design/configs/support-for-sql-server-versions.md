---
title: Versiones de SQL Server admitidas
titleSuffix: Configuration Manager
description: Obtenga los requisitos de configuración y versión de SQL Server para hospedar una base de datos de sitio de Configuration Manager.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5f2d2b10419cec019cc3c0791c7a7aadc016c15b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133806"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Versiones de SQL Server compatibles con Configuration Manager

*Se aplica a: System Center Configuration Manager (ramificación actual)*

Cada sitio de System Center Configuration Manager requiere una versión y una configuración de SQL Server compatibles para hospedar la base de datos del sitio.  



##  <a name="bkmk_Instances"></a> Instancias y ubicaciones de SQL Server  
 
### <a name="central-administration-site-and-primary-sites"></a>Sitio de administración central y sitio primario  
 La base de datos de sitio debe usar una instalación completa de SQL Server.  

 SQL Server puede ubicarse en:  

-   El equipo de servidor de sitio.  
-   Un equipo remoto desde el servidor de sitio.  

Se admiten las siguientes instancias:  

-   La instancia con nombre o predeterminada de SQL Server.  
-   Varias configuraciones de instancias.  
-   Un clúster de SQL Server. Vea [Usar un clúster de SQL Server para hospedar la base de datos del sitio](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database).
-   Un grupo de disponibilidad AlwaysOn de SQL Server. Para obtener más información, vea [SQL Server Always On para una base de datos de sitio de alta disponibilidad](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).


### <a name="secondary-sites"></a>Sitios secundarios  
 La base de datos de sitio puede usar la instancia predeterminada de una instalación completa de SQL Server o SQL Server Express.  

 SQL Server debe ubicarse en el equipo del servidor de sitio.  


### <a name="limitations-to-support"></a>Limitaciones para la compatibilidad   
 Las configuraciones que aparecen a continuación no son compatibles:
 -   Un clúster de SQL Server en una configuración de clúster de equilibrio de carga de red (NLB)
 -   Un clúster de SQL Server en un volumen compartido de clúster (CSV)
 -   Tecnología de creación de reflejo y replicación punto a punto de la base de datos de SQL Server

La replicación transaccional de SQL Server solo se admite para replicar objetos a los puntos de administración que están configurados para usar [réplicas de base de datos](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  



##  <a name="bkmk_SQLVersions"></a> Versiones de SQL Server admitidas  
 En una jerarquía con varios sitios, cada sitio puede usar una versión diferente de SQL Server para hospedar la base de datos del sitio. Pero siempre que se cumplan las condiciones siguientes:
 -  Configuration Manager admite las versiones de SQL Server que se usan.
 -  Las versiones de SQL Server que se usan siguen teniendo soporte técnico de Microsoft.
 -  SQL Server admite replicación entre las dos versiones de SQL Server. Por ejemplo, SQL Server no admite replicación entre SQL Server 2008 R2 y SQL Server 2016. Para más información, vea [Características que ya no se utilizan en la replicación de SQL Server](https://docs.microsoft.com/sql/relational-databases/replication/deprecated-features-in-sql-server-replication).



 A menos que se especifique lo contrario, las versiones siguientes de SQL Server son compatibles con todas las versiones activas de Configuration Manager. Si se agrega soporte para una nueva versión de SQL Server o Service Pack, se notifica la versión de Configuration Manager que agrega dicha compatibilidad. De forma similar, si la compatibilidad está en desuso, busque detalles sobre las versiones afectadas de Configuration Manager.   

La compatibilidad para un Service Pack de SQL Server específico incluye actualizaciones acumulativas a menos que interrumpan la compatibilidad con versiones anteriores para la versión del Service Pack base. Cuando no se indica ninguna versión del Service Pack, la compatibilidad es para la versión de SQL Server sin Service Pack. En el futuro, si se publica algún Service Pack para una versión de SQL Server, se declara una instrucción independiente de compatibilidad antes de que se admita la versión nueva del Service Pack.


> [!IMPORTANT]  
>  Cuando usa SQL Server Standard para la base de datos en el sitio de administración central, limita el número total de clientes que una jerarquía puede admitir. Consulte [Números de tamaño y escala](/sccm/core/plan-design/configs/size-and-scale-numbers).

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: Standard, Enterprise  
Puede usar esta versión de SQL Server, con una [versión 2 de actualización acumulativa](https://support.microsoft.com/help/4052574) mínima, empezando por [Configuration Manager versión 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710) para los sitios siguientes: 

- Un sitio de administración central  
- Un sitio primario  
- Un sitio secundario  
  <!--SMS.498506-->

### <a name="sql-server-2016-sp2-standard-enterprise"></a>SQL Server 2016 SP2: Standard, Enterprise  
<!--514985--> Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:  

-   Un sitio de administración central  
-   Un sitio primario  
-   Un sitio secundario  

### <a name="sql-server-2016-sp1-standard-enterprise"></a>SQL Server 2016 SP1: Standard, Enterprise  
Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:  

-   Un sitio de administración central  
-   Un sitio primario  
-   Un sitio secundario  

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard, Enterprise  
Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:  

-   Un sitio de administración central  
-   Un sitio primario  
-   Un sitio secundario  

### <a name="sql-server-2014-sp3-standard-enterprise"></a>SQL Server 2014 SP3: Standard, Enterprise  
Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:  

-   Un sitio de administración central  
-   Un sitio primario  
-   Un sitio secundario

### <a name="sql-server-2014-sp2-standard-enterprise"></a>SQL Server 2014 SP2: Standard, Enterprise  
Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:  

-   Un sitio de administración central  
-   Un sitio primario  
-   Un sitio secundario

### <a name="sql-server-2014-sp1-standard-enterprise"></a>SQL Server 2014 SP1: Standard, Enterprise  
 Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:  

-   Un sitio de administración central  
-   Un sitio primario  
-   Un sitio secundario

### <a name="sql-server-2012-sp4-standard-enterprise"></a>SQL Server 2012 SP4: Standard, Enterprise  
 Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:  

-   Un sitio de administración central  
-   Un sitio primario  
-   Un sitio secundario  

### <a name="sql-server-2012-sp3-standard-enterprise"></a>SQL Server 2012 SP3: Standard, Enterprise  
 Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:  

-   Un sitio de administración central  
-   Un sitio primario  
-   Un sitio secundario  

### <a name="sql-server-2008-r2-sp3-standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3: Standard, Enterprise, Datacenter     
  Esta versión de SQL Server no es compatible. Para obtener más información, consulte [Compatibilidad en desuso con versiones de SQL Server como base de datos de sitio](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-support-for-sql-server-versions-as-a-site-database).  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express   
Puede usar esta versión de SQL Server, con una [versión 2 de actualización acumulativa](https://support.microsoft.com/help/4052574) mínima, empezando por [Configuration Manager versión 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710) para los sitios siguientes:
-   Un sitio secundario <!--SMS.498506-->

### <a name="sql-server-2016-express-sp2"></a>SQL Server 2016 Express SP2  
Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:
-   Un sitio secundario

### <a name="sql-server-2016-express-sp1"></a>SQL Server 2016 Express SP1  
Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:
-   Un sitio secundario

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:
-   Un sitio secundario

### <a name="sql-server-2014-express-sp3"></a>SQL Server 2014 Express SP3   
Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:  

-   Un sitio secundario  

### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2   
Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:  

-   Un sitio secundario  

### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1   
 Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:  

-   Un sitio secundario  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
Puede usar esta versión de SQL Server sin una versión de actualización acumulativa mínima para los sitios siguientes:  

-   Un sitio secundario  



##  <a name="bkmk_SQLConfig"></a> Configuraciones necesarias para SQL Server  
 Los siguientes elementos son necesarios para todas las instalaciones de SQL Server que use para una base de datos de sitio (incluido SQL Server Express). Si Configuration Manager instala SQL Server Express como parte de una instalación de sitio secundario, estas configuraciones se crean automáticamente.  

### <a name="sql-server-architecture-version"></a>Versión de arquitectura de SQL Server  
 Configuration Manager requiere una versión de 64 bits de SQL Server para hospedar la base de datos del sitio.  

### <a name="database-collation"></a>Intercalación de base de datos  
 En cada sitio, la instancia de SQL Server que se usa para el sitio y la base de datos del sitio deben usar la intercalación siguiente: **SQL_Latin1_General_CP1_CI_AS**.  

 Configuration Manager admite dos excepciones a esta intercalación para cumplir los estándares definidos en GB18030 para su uso en China. Para más información, vea [Compatibilidad internacional](/sccm/core/plan-design/hierarchy/international-support).  

### <a name="database-compatibility-level"></a>Nivel de compatibilidad de la base de datos   
 Configuration Manager requiere que el nivel de compatibilidad para la base de datos del sitio no sea inferior a la versión mínima compatible de SQL Server para su versión de Configuration Manager. Por ejemplo, a partir de la versión 1702, debe tener un [nivel de compatibilidad de la base de datos](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) mayor o igual a 110. <!-- SMS.506266--> 

### <a name="sql-server-features"></a>Características de SQL Server  
 Solo la característica **Servicios de motor de base de datos** es necesaria para cada servidor de sitio.  

 La replicación de base de datos de Configuration Manager no requiere la característica **Replicación de SQL Server**. En cambio, esta configuración de SQL Server es necesaria si usa [réplicas de bases de datos para puntos de administración](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  

### <a name="windows-authentication"></a>Autenticación de Windows  
 Configuration Manager requiere la **autenticación de Windows** para validar las conexiones con la base de datos.  

### <a name="sql-server-instance"></a>Instancia de SQL Server  
 Use una instancia dedicada de SQL Server para cada sitio. La instancia puede ser una **instancia con nombre** o la **instancia predeterminada**.  

### <a name="sql-server-memory"></a>Memoria de SQL Server  
 Reserve memoria para SQL Server con SQL Server Management Studio y configure el valor **Memoria mínima del servidor** en **Opciones de memoria del servidor**. Para obtener más información acerca de cómo configurar esta opción, consulte [Opciones de configuración de memoria del servidor](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options).  

-   **Para un servidor de bases de datos que está instalado en el mismo equipo que el servidor de sitio**: Limite la memoria para SQL Server al 50-80 % de la memoria de sistema direccionable disponible.  

-   **Para un servidor de bases de datos dedicado (ubicación remota con respecto al servidor de sitio)**: Limite la memoria para SQL Server al 80-90 % de la memoria de sistema direccionable disponible.  

-   **Para una reserva de memoria para el grupo de búferes de cada instancia de SQL Server en uso**:  

    -   Para un sitio de administración central: establezca un mínimo de 8 gigabytes (GB).  
    -   Para un sitio primario: establezca un mínimo de 8 gigabytes (GB).  
    -   Para un sitio secundario: establezca un mínimo de 4 gigabytes (GB).  

### <a name="sql-nested-triggers"></a>Desencadenadores anidados de SQL  
 Los desencadenadores anidados de SQL deben estar habilitados. Para obtener más información, consulte [Establecer la opción de configuración del servidor Desencadenadores anidados](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option). 

### <a name="sql-server-clr-integration"></a>Integración de CLR de SQL Server  
  La base de datos de sitio requiere Common Language Runtime (CLR) para habilitarse. Esta opción se habilita de forma automática cuando se instala Configuration Manager. Para obtener más información sobre CLR, consulte [Introducción a la integración CLR de SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).  



##  <a name="bkmk_optional"></a> Configuraciones opcionales para SQL Server  
 Las siguientes configuraciones son opcionales para cada base de datos que use una instalación completa de SQL Server.  

### <a name="sql-server-service"></a>Servicio de SQL Server  
 Puede configurar el servicio SQL Server para que se ejecute mediante:  

-   Una cuenta de *usuario de dominio con derechos reducidos*:  

    -   Esta configuración es un procedimiento recomendado y puede requerir que registre manualmente el nombre de entidad de seguridad de servicio (SPN) de la cuenta.  

-   La cuenta de **sistema local** del equipo que ejecuta SQL Server:  

    -   Use la cuenta de sistema local para simplificar el proceso de configuración.  
    -   Cuando se usa la cuenta de sistema local, Configuration Manager registra automáticamente el SPN para el servicio SQL Server.  
    -   El uso de la cuenta de sistema local para el servicio SQL Server no es un procedimiento recomendado de SQL Server.  

Cuando el equipo que ejecuta SQL Server no usa su cuenta de sistema local para ejecutar el servicio de SQL Server, configure el SPN de la cuenta que ejecuta el servicio de SQL Server en Active Directory Domain Services. (Cuando se usa la cuenta del sistema, el SPN se registra automáticamente).

Para obtener información acerca de los SPN para la base de datos de sitio, consulte [Administrar el SPN para el servidor de base de datos del sitio](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_SPN).  

Para obtener información sobre cómo cambiar la cuenta que usa el servicio SQL Server, consulte [Servicios SCM: cambiar la cuenta de inicio de servicio](https://docs.microsoft.com/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account).  

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  
SQL Server Reporting Services se necesita para instalar un punto de servicios de informes que le permita ejecutar informes.  

> [!IMPORTANT]  
> Después de actualizar SQL Server desde una versión anterior, podría ver el siguiente error:  *Report Builder Does Not Exist* (El generador de informes no existe).  
> Para resolver este error, debe reinstalar el rol de sistema de sitio de punto de servicios de informes.  

### <a name="sql-server-ports"></a>Puertos de SQL Server  
Para la comunicación con el motor de base de datos de SQL Server y para la replicación entre sitios, puede usar las configuraciones del puerto de SQL Server predeterminadas o especificar puertos personalizados:  

-   Las **comunicaciones entre sitios** usan SQL Server Service Broker, que usa de manera predeterminada el puerto TCP 4022.  
-   Las **comunicaciones entre sitios** entre el motor de base de datos de SQL Server y varios roles de sistema de sitio de Configuration Manager usan el puerto TCP 1433 de forma predeterminada. Los siguientes roles de sistema de sitio se comunican directamente con la base de datos de SQL Server:  

    -   Punto de administración  
    -   Equipo de proveedor de SMS  
    -   Punto de servicios de informes  
    -   Servidor de sitio  

Si un equipo que ejecuta SQL Server hospeda una base de datos de más de un sitio, cada base de datos debe usar una instancia independiente de SQL Server. Además, cada instancia debe estar configurada para usar un conjunto de puertos único.  

> [!WARNING]  
>  Configuration Manager no admite los puertos dinámicos. Ya que las instancias con nombre de SQL Server usan de manera predeterminada puertos dinámicos para las conexiones con el motor de base de datos, cuando usa una instancia con nombre deberá configurar manualmente el puerto estático que desea usar para la comunicación entre sitios.  

Si tiene un firewall habilitado en el equipo que ejecuta SQL Server, asegúrese de que está configurado para permitir los puertos utilizados por su implementación en todas las ubicaciones en la red entre los equipos que se comunican con SQL Server.  

Para obtener un ejemplo de cómo configurar SQL Server para usar un determinado puerto, consulte [Configurar un servidor para que escuche en un puerto TCP específico](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  



## <a name="upgrade-options-for-sql-server"></a>Opciones de actualización de SQL Server

Si tiene que actualizar la versión de SQL Server, use uno de los métodos siguientes, del más sencillo al más complicado:  

- [Realice una actualización local de SQL Server](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recomendado)  

- Instale una nueva versión de SQL Server en un equipo nuevo y después [use la opción para mover datos](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) del programa de instalación de Configuration Manager para transfiera el servidor de sitio a la nueva instancia de SQL Server  

- Use [Copia de seguridad y recuperación](/sccm/protect/understand/backup-and-recovery). Se admite el uso de copias de seguridad y recuperación para un escenario de actualización de SQL. Puede omitir el requisito de control de versiones SQL al revisar las [consideraciones antes de recuperar un sitio](/sccm/protect/understand/recover-sites#considerations-before-recovering-a-site). 
