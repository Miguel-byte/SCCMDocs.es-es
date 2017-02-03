---
title: Versiones de SQL Server admitidas | Microsoft Docs
description: "Obtenga los requisitos de configuración y versión de SQL Server para hospedar una base de datos de sitio de System Center Configuration Manager."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
caps.latest.revision: 21
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 25aa013896ca118f0689b71e5cddcb8baf049c66
ms.openlocfilehash: 9bf4c1d9ee12da6801470165d33df50b2d08a810


---
# <a name="supported-sql-server-versions-for-system-center-configuration-manager"></a>Versiones de SQL Server compatibles con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Cada sitio de System Center Configuration Manager requiere una versión y una configuración de SQL Server compatibles para hospedar la base de datos del sitio.  

##  <a name="a-namebkmkinstancesa-sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> Instancias y ubicaciones de SQL Server  
 **Sitios primarios y sitio de administración central:**  
La base de datos de sitio debe usar una instalación completa de SQL Server.  

 SQL Server puede ubicarse en:  

-   El equipo de servidor de sitio.  
-   Un equipo remoto desde el servidor de sitio.  

Se admiten las siguientes instancias:  

-   La instancia con nombre o predeterminada de SQL Server.  
-   Varias configuraciones de instancias.  
-   Un clúster de SQL Server. Vea [Usar un clúster de SQL Server para hospedar la base de datos del sitio](../../../core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
-   Un grupo de disponibilidad AlwaysOn de SQL Server. Esta opción requiere la versión 1602 o posterior de Configuration Manager. Para obtener más información, vea [SQL Server AlwaysOn para una base de datos de sitio de alta disponibilidad para System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

> [!NOTE]  
>  No se admite un clúster de SQL Server en una configuración de clúster de equilibrio de carga de red (NLB). Además, no se admiten la tecnología de creación de reflejo ni la replicación punto a punto de la base de datos de SQL Server. La replicación transaccional estándar de SQL Server solo se admite para replicar objetos a los puntos de administración que están configurados para usar [réplicas de base de datos](https://technet.microsoft.com/library/mt608546.aspx).  


 **Sitios secundarios:**  
 La base de datos de sitio puede usar la instancia predeterminada de una instalación completa de SQL Server o SQL Server Express.  

 SQL Server debe ubicarse en el equipo del servidor de sitio.  

##  <a name="a-namebkmksqlversionsa-supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> Versiones de SQL Server admitidas  
 En una jerarquía con varios sitios, cada sitio puede usar una versión diferente de SQL Server para hospedar la base de datos del sitio, siempre que Configuration Manager admita las versiones de SQL Server que usa.  

 A menos que se especifique lo contrario, con System Center Configuration Manager versión 1511 y versiones posteriores se admiten las siguientes versiones de SQL Server.  

> [!IMPORTANT]  
>  Cuando usa SQL Server Standard para la base de datos en el sitio de administración central, limita el número total de clientes que una jerarquía puede admitir. Consulte [Números de tamaño y escala](../../../core/plan-design/configs/size-and-scale-numbers.md).

### <a name="sql-server-2016-sp1-standard-enterprise"></a>SQL Server 2016 SP1: Standard, Enterprise  
Puede utilizar esta versión de SQL Server sin una versión de actualización acumulativa mínima para lo siguiente:  

-   Un sitio de administración central  
-   Un sitio primario  
-   Un sitio secundario  

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard, Enterprise  
Puede utilizar esta versión de SQL Server sin una versión de actualización acumulativa mínima para lo siguiente:  

-   Un sitio de administración central  
-   Un sitio primario  
-   Un sitio secundario  


### <a name="sql-server-2014-sp2-standard-enterprise"></a>SQL Server 2014 SP2: Standard, Enterprise  
Puede utilizar esta versión de SQL Server sin una versión de actualización acumulativa mínima para lo siguiente:  

-   Un sitio de administración central  
-   Un sitio primario  
-   Un sitio secundario



### <a name="sql-server-2014-sp1-standard-enterprise"></a>SQL Server 2014 SP1: Standard, Enterprise  
 Puede utilizar esta versión de SQL Server sin una versión de actualización acumulativa mínima para lo siguiente:  

-   Un sitio de administración central  
-   Un sitio primario  
-   Un sitio secundario


### <a name="sql-server-2012-sp3-standard-enterprise"></a>SQL Server 2012 SP3: Standard, Enterprise  
 Puede utilizar esta versión de SQL Server sin una versión de actualización acumulativa mínima para lo siguiente:  

-   Un sitio de administración central  
-   Un sitio primario  
-   Un sitio secundario  


### <a name="sql-server-2012-sp2-standard-enterprise"></a>SQL Server 2012 SP2: Standard, Enterprise   
 Puede utilizar esta versión de SQL Server sin una versión de actualización acumulativa mínima para lo siguiente:  

-   Un sitio de administración central  
-   Un sitio primario  
-   Un sitio secundario  


### <a name="sql-server-2008-r2-sp3-standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3: Standard, Enterprise, Datacenter     
Puede utilizar esta versión de SQL Server sin una versión de actualización acumulativa mínima para lo siguiente:  

-   Un sitio de administración central  
-   Un sitio primario
-   Un sitio secundario



### <a name="sql-server-2016-express-sp1"></a>SQL Server 2016 Express SP1  
Puede utilizar esta versión de SQL Server sin una versión de actualización acumulativa mínima para lo siguiente:
-   Un sitio secundario

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
Puede utilizar esta versión de SQL Server sin una versión de actualización acumulativa mínima para lo siguiente:
-   Un sitio secundario


### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2   
Puede utilizar esta versión de SQL Server sin una versión de actualización acumulativa mínima para lo siguiente:  

-   Un sitio secundario  


### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1   
 Puede utilizar esta versión de SQL Server sin una versión de actualización acumulativa mínima para lo siguiente:  

-   Un sitio secundario  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
Puede utilizar esta versión de SQL Server sin una versión de actualización acumulativa mínima para lo siguiente:  

-   Un sitio secundario  

### <a name="sql-server-2012-express-sp2"></a>SQL Server 2012 Express SP2   
 Puede utilizar esta versión de SQL Server sin una versión de actualización acumulativa mínima para lo siguiente:  

-   Un sitio secundario  

##  <a name="a-namebkmksqlconfiga-required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> Configuraciones necesarias para SQL Server  
 Los siguientes elementos son necesarios para todas las instalaciones de SQL Server que use para una base de datos de sitio (incluido SQL Server Express). Si Configuration Manager instala SQL Server Express como parte de una instalación de sitio secundario, estas configuraciones se crean automáticamente.  

 **Versión de arquitectura de SQL Server:**  
 Configuration Manager requiere una versión de 64 bits de SQL Server para hospedar la base de datos del sitio.  

 **Intercalación de base de datos:**  
 En cada sitio, la instancia de SQL Server que se usa para el sitio y la base de datos del sitio deben usar la intercalación siguiente: **SQL_Latin1_General_CP1_CI_AS**.  

 Configuration Manager admite dos excepciones a esta intercalación para cumplir los estándares definidos en GB18030 para su uso en China. Para obtener más información, consulte [Compatibilidad internacional en System Center Configuration Manager](../../../core/plan-design/hierarchy/international-support.md).  

 **Características de SQL Server:**  
 Solo la característica **Servicios de motor de base de datos** es necesaria para cada servidor de sitio.  

 La replicación de base de datos de Configuration Manager no requiere la característica **Replicación de SQL Server**. En cambio, esta configuración de SQL Server es necesaria si usa [réplicas de bases de datos para puntos de administración de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Autenticación de Windows:**  
 Configuration Manager requiere la **autenticación de Windows** para validar las conexiones con la base de datos.  

 **Instancia de SQL Server:**  
 Debe usar una instancia dedicada de SQL Server para cada sitio. Esto puede ser una **instancia con nombre** o una **instancia predeterminada**.  

 **Memoria de SQL Server:**  
 Reserve memoria para SQL Server con SQL Server Management Studio y configure el valor **Memoria mínima del servidor** en **Opciones de memoria del servidor**. Para más información sobre cómo establecer una cantidad fija de memoria, vea [Cómo establecer una cantidad fija de memoria (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

-   **Para un servidor de base de datos que está instalado en el mismo equipo que el servidor de sitio:** limite la memoria para SQL Server a entre un 50 y 80 % de la memoria de sistema direccionable disponible.  

-   **Para un servidor de base de datos dedicado (ubicación remota con respecto al servidor de sitio):** limite la memoria para SQL Server a entre un 80 y 90 % de la memoria de sistema direccionable disponible.  

-   **Para una reserva de memoria para el grupo de búferes de cada instancia de SQL Server en uso:**  

    -   Para un sitio de administración central: establezca 8 GB como mínimo.  
    -   Para un sitio primario: establezca 8 GB como mínimo.  
    -   Para un sitio secundario: establezca 4 GB como mínimo.  

**Desencadenadores anidados de SQL:**  
Los [desencadenadores anidados de SQL](http://go.microsoft.com/fwlink/?LinkId=528802) deben estar habilitados.  

 **Integración de CLR de SQL Server**  
  La base de datos de sitio requiere Common Language Runtime (CLR) para habilitarse. Se habilita de forma automática cuando se instala Configuration Manager. Para obtener más información sobre CLR, consulte [Introducción a la integración CLR de SQL Server](https://msdn.microsoft.com/library/ms254498\(v=vs.110\).aspx).  

##  <a name="a-namebkmkoptionala-optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> Configuraciones opcionales para SQL Server  
 Las siguientes configuraciones son opcionales para cada base de datos que use una instalación completa de SQL Server.  

 **Servicio de SQL Server:**  
 Puede configurar el servicio SQL Server para que se ejecute mediante:  

-   La cuenta de **usuario local de dominio**:  

    -   Se trata de un procedimiento recomendado y puede requerir que registre manualmente el nombre de entidad de seguridad de servicio (SPN) de la cuenta.  

-   La cuenta de **sistema local** del equipo que ejecuta SQL Server:  

    -   Use la cuenta de sistema local para simplificar el proceso de configuración.  
    -   Cuando se usa la cuenta de sistema local, Configuration Manager registra automáticamente el SPN para el servicio SQL Server.  
    -   Tenga en cuenta que el uso de la cuenta de sistema local para el servicio SQL Server no es un procedimiento recomendado de SQL Server.  

Cuando el equipo que ejecuta SQL Server no usa su cuenta de sistema local para ejecutar el servicio de SQL Server, debe configurar el SPN de la cuenta que ejecuta el servicio de SQL Server en Active Directory Domain Services. (Cuando se usa la cuenta del sistema, el SPN se registra automáticamente).

Para obtener más información sobre los SPN de la base de datos del sitio, vea [Administrar el SPN para el servidor de base de datos del sitio](../../../core/servers/manage/modify-your-infrastructure.md#bkmk_SPN) en el tema [Modificar la infraestructura de System Center Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md).  

Para obtener información sobre cómo cambiar la cuenta que usa el servicio de SQL Server, vea [Cambiar la cuenta de inicio del servicio para SQL Server (Administrador de configuración de SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=237661).  

**SQL Server Reporting Services:**  
SQL Server Reporting Services se necesita para instalar un punto de servicios de informes que le permita ejecutar informes.  

> [!IMPORTANT]  
> Después de actualizar SQL Server desde una versión anterior, podría ver el siguiente error: *Report Builder Does Not Exist* (El generador de informes no existe).    
> Para resolver este error, debe reinstalar el rol de sistema de sitio de punto de servicios de informes.

**Puertos de SQL Server:**  
Para la comunicación con el motor de base de datos de SQL Server y para la replicación entre sitios, puede usar las configuraciones del puerto de SQL Server predeterminadas o especificar puertos personalizados:  

-   Las **comunicaciones entre sitios** usan SQL Server Service Broker, que usa de manera predeterminada el puerto TCP 4022.  
-   La **comunicación entre sitios** entre el motor de base de datos de SQL Server y varios roles de sistema de sitio de Configuration Manager tienen el puerto TCP 1433 como predeterminado. Los siguientes roles de sistema de sitio se comunican directamente con la base de datos de SQL Server:  

    -   Punto de administración  
    -   Equipo de proveedor de SMS  
    -   Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.  
    -   Servidor de sitio  

Si un equipo que ejecuta SQL Server hospeda una base de datos de más de un sitio, cada base de datos debe usar una instancia independiente de SQL Server. Además, cada instancia debe estar configurada para usar un conjunto de puertos único.  

> [!WARNING]  
>  Configuration Manager no admite los puertos dinámicos. Ya que las instancias con nombre de SQL Server usan de manera predeterminada puertos dinámicos para las conexiones con el motor de base de datos, cuando usa una instancia con nombre deberá configurar manualmente el puerto estático que desea usar para la comunicación entre sitios.  

Si tiene un firewall habilitado en el equipo que ejecuta SQL Server, asegúrese de que está configurado para permitir los puertos utilizados por su implementación en todas las ubicaciones en la red entre los equipos que se comunican con SQL Server.  

Para obtener un ejemplo de cómo configurar SQL Server para usar un puerto específico, vea [Configurar un servidor para que escuche en un puerto TCP específico (Administrador de configuración de SQL Server)](http://go.microsoft.com/fwlink/p/?LinkID=226349) en la biblioteca de TechNet de SQL Server.  



<!--HONumber=Jan17_HO1-->


