---
title: SQL Server Always On
titleSuffix: Configuration Manager
description: Planee el uso de un grupo de disponibilidad Always On de SQL Server con SCCM.
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: "16"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 93aec5773f56ad28950ae75db54739d04124794f
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Preparación para usar grupos de disponibilidad AlwaysOn de SQL Server con Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Prepare System Center Configuration Manager para usar grupos de disponibilidad AlwaysOn de SQL Server como una solución de alta disponibilidad y recuperación ante desastres para la base de datos de sitio.  
Configuration Manager admite el uso de grupos de disponibilidad:
-     En sitos primarios y el sitio de administración central.
-     De forma local, o en Microsoft Azure.

Al utilizar grupos de disponibilidad en Microsoft Azure, puede aumentar aún más la disponibilidad de la base de datos de sitio mediante *conjuntos de disponibilidad de Azure*. Para más información sobre los conjuntos de disponibilidad de Azure, consulte [Administrar la disponibilidad de las máquinas virtuales](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

>  [!Important]   
>  Antes de continuar, familiarícese con la configuración de SQL Server y los grupos de disponibilidad de SQL Server. La siguiente información hace referencia a la biblioteca de documentación y los procedimientos de SQL Server.

## <a name="supported-scenarios"></a>Escenarios admitidos
Los siguientes escenarios son compatibles con el uso de grupos de disponibilidad con Configuration Manager. Los detalles y los procedimientos de cada uno de ellos se pueden encontrar en [Configure availability groups for Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag) (Configuración de grupos de disponibilidad para Configuration Manager).


-      [Crear un grupo de disponibilidad para su uso con Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group).
-     [Configurar un sitio para utilizar un grupo de disponibilidad](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group).
-     [Agregar o quitar a miembros de la réplica sincrónica de un grupo de disponibilidad que hospeda una base de datos de sitio](/sccm/core/servers/deploy/configure/configure-aoag#add-and-remove-synchronous-replica-members).
-     [Configurar réplicas de confirmación asincrónica](/sccm/core/servers/deploy/configure/configure-aoag#configure-an-asynchronous-commit-repilca) (requiere la versión 1706 de Configuration Manager o una posterior).
-     [Recuperar un sitio a partir de una réplica de confirmación asincrónica](/sccm/core/servers/deploy/configure/configure-aoag#use-the-asynchronous-replica-to-recover-your-site) (requiere la versión 1706 de Configuration Manager o una posterior).
-     [Sacar una base de datos de sitio de un grupo de disponibilidad a una instancia predeterminada o con nombre de un servidor SQL Server independiente](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group).


## <a name="prerequisites"></a>Requisitos previos
Los siguientes requisitos previos se aplican a todos los escenarios. Si hubiera requisitos previos adicionales para un escenario concreto, se detallarán con ese escenario.   

### <a name="configuration-manager-accounts-and-permissions"></a>Cuentas y permisos de Configuration Manager
**Acceso del miembro del servidor de sitio a la réplica:**   
La cuenta de equipo del servidor del sitio debe formar parte del grupo de **administradores locales** de cada equipo que sea miembro del grupo de disponibilidad.

### <a name="sql-server"></a>SQL Server
**Versión:**  
Cada réplica del grupo de disponibilidad debe ejecutar una versión de SQL Server que sea compatible con su versión de Configuration Manager. Si SQL Server lo admite, distintos nodos del grupo de disponibilidad pueden ejecutar distintas versiones de SQL Server.

**Edición:**  
Debe usar una edición *Enterprise* de SQL Server.

**Cuenta:**  
Cada instancia de SQL Server puede ejecutarse en una cuenta de usuario de dominio (**cuenta de servicio**) o a una que no sea de dominio. Cada réplica de un grupo puede tener una configuración diferente. De acuerdo con los [procedimientos recomendados de SQL Server](/sql/sql-server/install/security-considerations-for-a-sql-server-installation#before-installing-includessnoversionincludesssnoversion-mdmd), use una cuenta con los mínimos permisos posibles.

-   Para configurar las cuentas de servicio y los permisos de SQL Server 2016, consulte [Configuración de los permisos y las cuentas de servicio de Windows](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions) en MSDN.
-   Para usar una cuenta que no es de dominio, debe utilizar certificados. Para obtener más información, consulte [Uso de certificados para un punto de conexión de creación de reflejo de la base de datos (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).


Para obtener más información, consulte [Crear un punto de conexión de creación de reflejo de la base de datos para grupos de disponibilidad AlwaysOn](/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).

### <a name="availability-group-configurations"></a>Configuraciones de grupo de disponibilidad
**Miembros de réplica:**  
-   El grupo de disponibilidad debe tener, al menos, una réplica principal.
-   Antes de la versión 1706, puede tener hasta dos réplicas secundarias sincrónicas.
-   A partir de la versión 1706, puede usar el mismo número y tipo de réplicas en un grupo de disponibilidad en la medida en que lo admita la versión de SQL Server que utilice.

-   A partir de la versión 1706, se puede utilizar una réplica de confirmación asincrónica para recuperar una réplica sincrónica. Vea [las opciones de recuperación de la base de datos de sitio]( /sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) en el tema Copia de seguridad y recuperación para obtener información sobre cómo realizar esta tarea.
    > [!CAUTION]  
    > Configuration Manager no admite la conmutación por error para usar la réplica de confirmación asincrónica como la base de datos de sitio.
Dado que Configuration Manager no valida el estado de la réplica de confirmación asincrónica para confirmar que está actualizada, y que [por cuestiones de diseño una réplica de este tipo puede no estar sincronizada]( https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), el uso de una réplica de confirmación asincrónica como la base de datos de sitio puede poner en peligro la integridad de los datos y del sitio.

Cada miembro de réplica debe cumplir lo siguiente:
-   Utilizar la **instancia predeterminada**  
    *A partir de la versión 1702, puede usar una*  ***instancia con nombre***.

-     Tener la opción **Conexiones del rol principal** establecida en **Sí**
-     Tener la opción **Secundaria legible** establecida en **Sí**  
-     Establecerse para la **conmutación por error manual**      

    >  [!TIP]
    >  Configuration Manager admite el uso de las réplicas sincrónicas del grupo de disponibilidad cuando se establece en **Conmutación automática por error**. Sin embargo, debe establecerse la **conmutación por error manual** en los siguientes casos:
    >  -  Cuando se ejecuta el programa de instalación para especificar el uso de la base de datos de sitio en el grupo de disponibilidad.
    >  -  Cuando se instala cualquier actualización en Configuration Manager (no solo las actualizaciones que se aplican a la base de datos de sitio).  

**Ubicación del miembro de réplica:**  
Todas las réplicas de un grupo de disponibilidad deben hospedarse en el entorno local o en Microsoft Azure. No se admite un escenario en el que un grupo incluya un miembro en el entorno local y otro en Azure.     

Si configura un grupo de disponibilidad en Azure y el grupo está detrás de un equilibrador de carga interno o externo, estos son los puertos predeterminados que debe abrir para permitir el acceso del programa de instalación a cada réplica:   

-     Asignador de puntos de conexión RPC: **TCP 135**   
-     Bloque de mensajes del servidor: **TCP 445**  
    *Puede quitar este puerto al finalizar el traslado de la base de datos. A partir de la versión 1702, este puerto ya no es necesario.*
-     SQL Server Service Broker -  **TCP 4022**
-     SQL a través de TCP: **TCP 1433**   

Una vez completada la instalación, los siguientes puertos deben permanecer accesibles:
-     SQL Server Service Broker -  **TCP 4022**
-     SQL a través de TCP: **TCP 1433**

A partir de la versión 1702, puede usar puertos personalizados para estas configuraciones. Deben utilizarse los mismos puertos por el punto de conexión y en todas las réplicas del grupo de disponibilidad.


**Agente de escucha:**   
El grupo de disponibilidad debe tener al menos un **agente de escucha de grupo de disponibilidad**. El nombre virtual de este agente de escucha se usa al configurar Configuration Manager para usar la base de datos de sitio en el grupo de disponibilidad. Aunque un grupo de disponibilidad puede contener varios agentes de escucha, Configuration Manager solo puede usar uno. Vea [Create or Configure an Availability Group Listener (SQL Server)](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server) (Creación o configuración de un agente de escucha de grupo de disponibilidad) para obtener más información.

**Rutas de acceso de archivo:**   
Al ejecutar el programa de instalación de Configuration Manager para configurar un sitio para que use la base de datos en un grupo de disponibilidad, cada servidor de réplica secundario debe tener una ruta de acceso de archivo de SQL Server idéntica a la ruta de acceso para los archivos de base de datos de sitio que se encuentran en la réplica principal actual.
-   Si no existe una ruta de acceso idéntica, se producirá un error en el programa de instalación al agregar la instancia para el grupo de disponibilidad como nueva ubicación de la base de datos de sitio.
-   Además, la cuenta de servicio de SQL Server local debe tener permiso de **Control total** para esta carpeta.

Los servidores de réplica secundaria solo requieren esta ruta de acceso de archivo mientras utilizan el programa de instalación para especificar la instancia de base de datos del grupo de disponibilidad. Una vez que el programa de instalación completa la configuración de la base de datos de sitio en el grupo de disponibilidad, puede eliminar la ruta de acceso de los servidores de réplicas secundarias sin usar.

Por ejemplo, considere el siguiente escenario:
-   Crea un grupo de disponibilidad que utiliza tres servidores SQL Server.

-   El servidor de réplica principal es una nueva instalación de SQL Server 2014. De forma predeterminada, la base de datos .MDF y los archivos .LDF se almacenan en C:\Program Files\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\DATA.

-   Dos de los servidores de réplica secundaria se actualizaron a SQL Server 2014 desde versiones anteriores y conservan la ruta del archivo original para almacenar los archivos de base de datos: C:\Program Files\Microsoft SQL Server\MSSQL10. MSSQLSERVER\MSSQL\DATA.

-   Antes de intentar mover la base de datos de sitio a este grupo de disponibilidad, en cada servidor de réplica secundaria debe crear la siguiente ruta de acceso, aunque las réplicas secundarias no utilicen esta ubicación de archivo: C:\Program Files\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\DATA (un duplicado de la ruta de acceso que se usa en la réplica principal).

-   A continuación, concede a la cuenta de servicio de SQL Server de cada réplica secundaria control total de acceso a la ubicación del archivo recién creada en el servidor.

-   Ahora puede ejecutar correctamente el programa de instalación de Configuration Manager para configurar el sitio para que use la base de datos de sitio del grupo de disponibilidad.

**Configuración de la base de datos en una nueva réplica:**   
 La base de datos de cada réplica deben configurarse con los siguientes parámetros:
-   **Integración con CLR** debe tener el valor *habilitado*
-     **Tamaño de replicación de texto máximo** debe ser *2147483647*
-     El propietario de la base de datos debe ser la *Cuenta SA*
-     **DE CONFIANZA** debe tener el valor **activado**
-     **Service Broker** debe tener el valor *habilitado*

Puede establecer estas configuraciones en solo una réplica principal. Para configurar una réplica secundaria, primero debe conmutar por error la principal en la secundaria, lo que convierte a la secundaria en la nueva réplica principal.   

Utilice la documentación de SQL Server cuando sea necesario para obtener ayuda con la configuración de estas opciones. Por ejemplo, consulte [DE CONFIANZA](/sql/relational-databases/security/trustworthy-database-property) o [Integración CLR](/sql/relational-databases/clr-integration/clr-integration-enabling) en la documentación de SQL Server.

### <a name="verification-script"></a>Script de comprobación
Puede ejecutar el script siguiente para comprobar las configuraciones de base de datos para las réplicas principal y secundaria. Para solucionar un problema en una réplica secundaria, debe cambiar esa réplica secundaria para que sea la réplica principal.

    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targetting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targetted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:

## <a name="limitations-and-known-issues"></a>Limitaciones y problemas conocidos
Las siguientes limitaciones se aplican a todos los escenarios.   

**Opciones y configuraciones de SQL Server que no son compatibles:**
- **Grupos de disponibilidad básicos**  
  Introducidos con la edición SQL Server 2016 Standard, los [grupos de disponibilidad básica](https://msdn.microsoft.com/library/mt614935.aspx) no admiten el acceso de lectura a réplicas secundarias, un requisito para su uso con Configuration Manager.
- **Instancia del clúster de conmutación por error**  
  Las [instancias del clúster de conmutación por error](/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server) no son compatibles con las réplicas usadas junto con Configuration Manager.

- **MultiSubnetFailover**    
    No se admite para usar un grupo de disponibilidad de una configuración de varias subredes o con la cadena de conexión de palabras clave [MutliSubnetFailover](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover).



**Servidores SQL Server que hospedan grupos de disponibilidad adicionales:**   
Antes de la versión 1610 de Configuration Manager, cuando un grupo de disponibilidad en un servidor SQL Server hospeda uno o varios grupos de disponibilidad además del grupo que se usa para Configuration Manager, cada réplica de esos grupos de disponibilidad adicionales debe tener las siguientes configuraciones en el momento de ejecutar el programa de instalación de Configuration Manager o instalar una actualización para Configuration Manager:
-   **conmutación por error manual**
-   **permitir cualquier conexión de solo lectura**

**Uso de la base de datos no admitido:**
-   **Configuration Manager admite solo la base de datos de sitio en un grupo de disponibilidad:** No se admiten las siguientes:
    -   Base de datos de informes
    -   Base de datos WSUS
-   **Base de datos existente:** no puede usar la nueva base de datos que creó en la réplica. En su lugar, debe restaurar una copia de una base de datos de Configuration Manager existente en la réplica principal al configurar un grupo de disponibilidad.

**Errores de instalación en ConfigMgrSetup.log:**  
Al ejecutar el programa de instalación para mover una base de datos de sitio a un grupo de disponibilidad, el programa de instalación intenta procesar los roles de la base de datos en las réplicas secundarias del grupo de disponibilidad y registra errores como el siguiente:
-   ERROR: Error de SQL Server: [25000] [3906] [Microsoft] [SQL Server Native Client 11.0] [SQL Server] No se pudo actualizar la base de datos "CM_AAA" porque es de solo lectura. Programa de instalación de Configuration Manager 1/21/2016 4:54:59 PM 7344 (0x1CB0)  

Es seguro omitir estos errores.

## <a name="changes-for-site-backup"></a>Cambios para la copia de seguridad del sitio
**Copia de seguridad de archivos de base de datos:**  
Cuando una base de datos de sitio se ejecuta en un grupo de disponibilidad, debe ejecutar la tarea de mantenimiento del **Servidor del sitio de copia de seguridad** integrada para realizar una copia de seguridad de los archivos y las configuraciones comunes de Configuration Manager. Sin embargo, no use los archivos .MDF o .LDF creados por esa copia de seguridad. Realice en su lugar realizar copias de seguridad directas de los archivos de la base de datos mediante SQL Server.

**Registro de transacciones:**  
El modelo de recuperación de la base de datos de sitio debe establecerse en **Completo** (un requisito para su uso en un grupo de disponibilidad). Con esta configuración, debe supervisar y mantener el tamaño del registro de transacciones de la base de datos de sitio. En el modelo de recuperación completa, las transacciones no están protegidas hasta que se realiza una copia de seguridad completa de la base de datos o el registro de transacciones. Consulte [Realizar copias de seguridad y restaurar bases de datos de SQL Server](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases) en la documentación de SQL Server para obtener más información.

## <a name="changes-for-site-recovery"></a>Cambios para la recuperación del sitio
Puede utilizar la opción de recuperación del sitio **Omitir recuperación de base de datos (use esta opción si la base de datos de sitio no se vio afectada)** si al menos un nodo del grupo de disponibilidad sigue funcionando.

 Para recuperar el sitio cuando se han perdido todos los nodos de un grupo de disponibilidad, debe volver a crear dicho grupo. Configuration Manager no puede volver a generar o restaurar el nodo de disponibilidad. Una vez que se haya vuelto a crear el grupo y se haya restaurado y reconfigurado una copia de seguridad, podrá usar la opción de recuperación del sitio **Omitir recuperación de base de datos (use esta opción si la base de datos de sitio no se vio afectada)**.

Para obtener más información, consulte [Copia de seguridad y recuperación de System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

## <a name="changes-for-reporting"></a>Cambios para la notificación
**Instalación del punto de servicios de informes:**  
El punto de servicios de informes no admite el uso del nombre virtual del agente de escucha del grupo de disponibilidad o el alojamiento de la base de datos de servicios de informes en un grupo de disponibilidad AlwaysOn de SQL Server:
-   De forma predeterminada, la instalación del punto de servicios de informes establece el **Nombre de servidor de base de datos de sitio** en el nombre virtual que se especifica como el agente de escucha. Cambie esta opción para especificar un nombre de equipo y una instancia de una réplica del grupo de disponibilidad.
-   Para descargar la carga de informes y para aumentar la disponibilidad cuando un nodo de la réplica está sin conexión, considere la posibilidad de instalar puntos de servicios de informes adicionales en cada nodo de réplica y configurar cada punto de servicios de informes para que señale a su propio nombre de equipo.

Cuando se instala un punto de servicios de informes en cada réplica del grupo de disponibilidad, los informes siempre pueden conectarse a un servidor de punto de informes activo.

**Cambio del punto de servicios de informes que utiliza la consola:**  
Para ejecutar informes, en la consola vaya a **Supervisión** > **Introducción** > **Generación de informes** > **Informes** y, a continuación, elija **Opciones de informes**. En el cuadro de diálogo Opciones de informes seleccione el punto de servicios de informes deseado.

## <a name="next-steps"></a>Pasos siguientes
Una vez que comprenda los requisitos previos, las limitaciones y los cambios en las tareas comunes que se requieren al usar grupos de disponibilidad, consulte [Configure availability groups for Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag) (Configuración de grupos de disponibilidad para Configuration Manager) a fin de conocer los procedimientos de instalación y configuración del sitio para usar grupos de disponibilidad.
