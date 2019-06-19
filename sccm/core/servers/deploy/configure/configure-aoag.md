---
title: Configuración de grupos de disponibilidad
titleSuffix: Configuration Manager
description: Configure y administre los grupos de disponibilidad Always On de SQL Server con SCCM.
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c1e01d423df30e36bcf5e7613aee22962077787b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499264"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Configuración de grupos de disponibilidad AlwaysOn de SQL Server para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use la información de este tema para configurar y administrar los grupos de disponibilidad que use con Configuration Manager.

Antes de empezar:  
-   Familiarícese con la información de [Preparación para usar grupos de disponibilidad AlwaysOn de SQL Server con Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).
-   Familiarícese con la documentación de SQL Server que explica el uso de grupos de disponibilidad y los procedimientos relacionados. Esta información es necesaria para completar los siguientes escenarios.

> [!TIP]  
>  Los vínculos de este tema para SQL Server hacen referencia al contenido para SQL Server 2016. Si no usa esa versión de SQL Server, consulte la documentación de la versión que utilice.

## <a name="create-and-configure-an-availability-group"></a>Creación y configuración de grupo de disponibilidad
Utilice el procedimiento siguiente para crear un grupo de disponibilidad y, a continuación, mover una copia de la base de datos de sitio a ese grupo de disponibilidad.

Para completar este procedimiento, la cuenta que utilice debe cumplir los requisitos siguientes:
-   Debe ser miembro del grupo de **administradores locales** en cada equipo que vaya a estar en el grupo de disponibilidad.
-   Debe ser **Administrador del sistema** en cada instancia de SQL Server que hospeda la base de datos de sitio.

### <a name="to-create-and-configure-an-availability-group-for-configuration-manager"></a>Para crear y configurar un grupo de disponibilidad para Configuration Manager  
1. Use el siguiente comando para detener el sitio de Configuration Manager: **Preinst.exe /stopsite**. Para obtener más información acerca del uso de Preinst.exe, consulte [Hierarchy Maintenance Tool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) (Herramienta de mantenimiento de jerarquía).

2. Cambie el modelo de copia de seguridad de la base de datos de sitio de **SENCILLA** a **COMPLETA**.
   Consulte [Ver o cambiar el modelo de recuperación de una base de datos (SQL Server)](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) en la documentación de SQL Server. (Los grupos de disponibilidad solo admiten COMPLETA).

3. Use SQL Server para crear una copia de seguridad completa de la base de datos de sitio. Después, realice una de las acciones siguientes acciones, dependiendo de si el servidor que hospeda la base de datos de sitio será miembro de la réplica del nuevo grupo de disponibilidad o no:
   - **Será miembro del grupo de disponibilidad:**  
     Si utiliza este servidor como miembro de la réplica principal inicial del grupo de disponibilidad, no es necesario restaurar una copia de la base de datos de sitio en este u otro servidor del grupo. La base de datos ya estará disponible en la réplica principal, y SQL Server replicará la base de datos en las réplicas secundarias en un paso posterior.  

     -    **No será miembro del grupo de disponibilidad:**    
     Restaure una copia de la base de datos de sitio en el servidor que hospedará la réplica principal del grupo.

   Para obtener información sobre cómo completar este paso, vea [Crear una copia de seguridad completa de base de datos (SQL Server)](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) y [Restaurar una copia de seguridad de base de datos con SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) en la documentación de SQL Server.

4. En el servidor que hospedará la réplica principal inicial del grupo, use el [Asistente para nuevo grupo de disponibilidad](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) para crear el grupo de disponibilidad. En el asistente:
   - En la página **Seleccionar base de datos**, elija la base de datos para el sitio de Configuration Manager.  

   - En la página **Especificar réplicas** , configure lo siguiente:
     -    **Réplicas:** especifique los servidores que hospedarán las réplicas secundarias.

     -    **Agente de escucha**: especifique el **Nombre DNS del agente de escucha** como un nombre DNS completo, como **&lt;servidor_agente_escucha>.fabrikam.com**. Esto sirve al configurar Configuration Manager para usar la base de datos de sitio en el grupo de disponibilidad.

   - En la página **Seleccionar sincronización de datos iniciales** seleccione **Completa**. Una vez que el asistente cree el grupo de disponibilidad, hará una copia de seguridad del registro de transacciones y la base de datos principal. Después, los restaurará en cada servidor que hospede una réplica secundaria (Si no sigue este paso, tendrá que restaurar una copia de la base de datos de sitio en cada servidor que hospeda una réplica secundaria y unir manualmente esa base de datos al grupo).   

5. Compruebe la configuración en cada réplica:   
   1.    Asegúrese de que la cuenta de equipo del servidor del sitio forme parte del grupo de **administradores locales** de cada equipo que sea miembro del grupo de disponibilidad.  

   2.  Ejecute el [script de comprobación](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) de los requisitos previos para confirmar que la base de datos de sitio de cada réplica está configurada correctamente.

   3.    Si hay que ajustar parámetros en las réplicas secundarias, debe conmutar por error manualmente la réplica principal en la secundaria antes de continuar porque solo puede configurar la base de datos de una réplica principal. Consulte [Realización de una conmutación por error manual planeada de un grupo de disponibilidad (SQL Server)](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) en la documentación de SQL Server.

6. Una vez que todas las réplicas cumplan los requisitos, el grupo de disponibilidad estará listo para su uso con Configuration Manager.

## <a name="configure-a-site-to-use-the-database-in-the-availability-group"></a>Configuración de un sitio para utilizar la base de datos en el grupo de disponibilidad
Después de [crear y configurar el grupo de disponibilidad](#create-and-configure-an-availability-group), utilice el mantenimiento del sitio de Configuration Manager para configurar el sitio de manera que utilice la base de datos que está hospedada en el grupo de disponibilidad.

No se admite la instalación de un sitio nuevo con su base de datos en un grupo de disponibilidad. Por ejemplo, si usa los medios de la base de referencia 1702, debe instalar el sitio mediante una sola instancia de SQL Server. Una vez instalado el sitio, podrá mover la base de datos de sitio al grupo de disponibilidad.

Para completar este procedimiento, la cuenta que utilice para ejecutar el programa de instalación de Configuration Manager debe cumplir los requisitos siguientes:
-   Debe ser miembro del grupo de **administradores locales** en cada equipo que sea miembro del grupo de disponibilidad.
-   Debe ser **Administrador del sistema** en cada instancia de SQL Server que hospeda la base de datos de sitio.

> [!IMPORTANT]
> Al utilizar Microsoft Intune con Configuration Manager en una configuración híbrida, el traslado de la base de datos de sitio desde o hacia un grupo de disponibilidad activa una resincronización de los datos con la nube. No se puede evitar esta resincronización.

### <a name="to-configure-a-site-to-use-the-availability-group"></a>Para configurar un sitio para utilizar un grupo de disponibilidad
1.  Ejecute el **programa de instalación de Configuration Manager** desde la **&lt;*carpeta de instalación del sitio de Configuration Manager*>\BIN\X64\setup.exe**.

2.  En la página **Primeros pasos** , seleccione **Realizar mantenimiento de sitio o restablecer este sitio**y, a continuación, haga clic en **Siguiente**.

3.  A continuación, seleccione la opción **Modificar configuración de SQL Server** y luego haga clic en **Siguiente**.

4.  Vuelva a configurar lo siguiente en la base de datos de sitio:
    -   **Nombre de SQL Server:** escriba el nombre virtual para el **agente de escucha** del grupo de disponibilidad que ha configurado al crear el grupo de disponibilidad. El nombre virtual debe ser un nombre DNS completo, como **&lt;*servidorPuntodeconexión*>.fabrikam.com**.  

    -   **Instancia:** este valor debe estar en blanco para especificar la instancia predeterminada para el *agente de escucha* del grupo de disponibilidad. Si la base de datos de sitio actual se ejecuta en una instancia con nombre, esta aparecerá y debe borrarse.

    -   **Base de datos:** deje el nombre tal y como aparece. Este es el nombre de la base de datos de sitio actual.

5.  Después de proporcionar la información de la nueva ubicación de la base de datos, complete el programa de instalación con los procesos y las configuraciones habituales.



## <a name="add-or-remove-synchronous-replica-members"></a>Adición o eliminación de miembros de la réplica sincrónica  
Si la base de datos de sitio está hospedada en un grupo de disponibilidad, utilice los procedimientos siguientes para agregar o quitar miembros de la réplica sincrónica. Para obtener información sobre el tipo y el número de réplicas que se admiten, consulte el apartado **Configuraciones de grupo de disponibilidad** de la sección [Requisitos previos](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) del tema sobre cómo utilizar grupos de disponibilidad.

Para completar los procedimientos siguientes, la cuenta que utilice debe cumplir los requisitos siguientes:
-   Debe ser miembro del grupo de **administradores locales** en cada equipo que sea miembro del grupo de disponibilidad.
-   Debe ser **administrador del sistema** en cada servidor SQL Server que hospede o vaya a hospedar la base de datos de sitio.


### <a name="to-add-a-new-synchronous-replica-member"></a>Procedimiento para agregar un nuevo miembro de réplica sincrónica  
El proceso para agregar una réplica secundaria a un grupo de disponibilidad utilizado con Configuration Manager puede ser complejo, dinámico y requerir pasos y procedimientos que varían en función de cada entorno. Estamos trabajando en mejoras de Configuration Manager para simplificar este proceso. Mientras tanto, si necesita agregar réplicas secundarias, consulte el blog siguiente de TechNet para obtener una guía.
-   [ConfigMgr 1702: agregar un nodo nuevo (réplica secundaria) a un grupo de disponibilidad AlwaysOn existente de SQL](https://blogs.technet.microsoft.com/umairkhan/2017/07/17/configmgr-1702-adding-a-new-node-secondary-replica-to-an-existing-sql-ao-ag/)

### <a name="to-remove-a-replica-member"></a>Para quitar un miembro de la réplica
Para este procedimiento, utilice la información de [Remove a Secondary Replica from an Availability Group](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server) (Quitar una réplica secundaria de un grupo de disponibilidad [SQL Server]) de la documentación de SQL Server.  


## <a name="configure-an-asynchronous-commit-replica"></a>Configuración de una réplica de confirmación asincrónica
A partir de 1706 de versión de Configuration Manager, puede agregar una réplica asincrónica a un grupo de disponibilidad que se utilice con Configuration Manager. Para ello, no hace falta ejecutar los scripts de configuración necesarios para configurar una réplica sincrónica. (El motivo es que no se admite el uso de esa réplica asincrónica como la base de datos de sitio). Consulte la [documentación de SQL Server](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot)) para obtener información sobre cómo agregar réplicas secundarias a grupos de disponibilidad.

## <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Uso de la réplica asincrónica para la recuperación del sitio
Con la versión 1706 de Configuration Manager y posteriores, puede usar una réplica asincrónica para recuperar la base de datos de sitio. Para ello, debe detener el sitio primario activo para evitar que se realicen escrituras adicionales en la base de datos de sitio. Una vez detenido el sitio, puede utilizar una réplica asincrónica en lugar de una [base de datos recuperada manualmente](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption).

Para detener el sitio, puede usar la [herramienta de mantenimiento de jerarquía](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) si desea detener servicios clave en el servidor del sitio. Use la línea de comandos: **Preinst.exe /stopsite**   

Detener el sitio equivale a detener el servicio Administrador de componentes del sitio (sitecomp) seguido por el servicio SMS_Executive en el servidor del sitio.

<!-- For inclusion with passive primary site support:
> [!TIP]  
> If you use a primary passive replica (introduced in version [TBD],  you do not need to stop the passive replica. Only the active primary site must be stopped.
-->  

## <a name="stop-using-an-availability-group"></a>Detención del uso de un grupo de disponibilidad
Utilice el procedimiento siguiente cuando ya no desee hospedar la base de datos de sitio en un grupo de disponibilidad. Esto implica mover la base de datos de sitio de nuevo a una sola instancia de SQL Server.

Para completar este procedimiento, la cuenta que utilice debe cumplir los requisitos siguientes:
-   Debe ser miembro del grupo de **administradores locales** en cada equipo que sea miembro del grupo de disponibilidad.
-   Debe ser **Administrador del sistema** en cada instancia de SQL Server que hospeda la base de datos de sitio.

> [!IMPORTANT]  
> Al utilizar Microsoft Intune con Configuration Manager en una configuración híbrida, el traslado de la base de datos de sitio desde o hacia un grupo de disponibilidad activa una resincronización de los datos con la nube. Esto no puede evitarse.

### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>Para mover la base de datos de sitio desde un grupo de disponibilidad de nuevo a una sola instancia de SQL Server
1.  Para detener el sitio de Configuration Manager, use el siguiente comando: **Preinst.exe /stopsite**. Para obtener más información, consulte [Hierarchy Maintenance Tool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) (Herramienta de mantenimiento de jerarquía).

2.  Use SQL Server para crear una copia de seguridad completa de la base de datos de sitio desde la réplica principal. Para obtener información sobre cómo completar este paso, consulte [Crear una copia de seguridad completa de base de datos (SQL Server)](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) en la documentación de SQL Server.

3.  Si el servidor que es la réplica principal del grupo de disponibilidad hospedará la única instancia de la base de datos de sitio, puede omitir este paso:  

    -   Utilice SQL Server para restaurar la copia de seguridad de la base de datos de sitio en el servidor que hospedará la base de datos de sitio. Consulte [Restaurar una copia de seguridad de base de datos con SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) en la documentación de SQL Server.   <br />  <br />

4.  En el servidor que hospedará la base de datos de sitio (la réplica principal o el servidor donde haya restaurado la base de datos de sitio), cambie el modelo de copia de seguridad de la base de datos de sitio de **COMPLETA** a **SIMPLE**. Consulte [Ver o cambiar el modelo de recuperación de una base de datos (SQL Server)](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) en la documentación de SQL Server.  

5.  Ejecute el **programa de instalación de Configuration Manager** desde la **&lt;*carpeta de instalación del sitio de Configuration Manager>* \BIN\X64\setup.exe**.

6.  En la página **Primeros pasos** , seleccione **Realizar mantenimiento de sitio o restablecer este sitio**y, a continuación, haga clic en **Siguiente**.  

7.  A continuación, seleccione la opción **Modificar configuración de SQL Server** y luego haga clic en **Siguiente**.  

8.  Vuelva a configurar lo siguiente en la base de datos de sitio:
    -   **Nombre de SQL Server:** escriba el nombre del servidor que hospeda ahora la base de datos de sitio.

    -   **Instancia:** especifique la instancia con nombre que hospeda la base de datos de sitio o deje este campo en blanco si la base de datos se encuentra en la instancia predeterminada.

    -   **Base de datos:** deje el nombre tal y como aparece. Este es el nombre de la base de datos de sitio actual.    

9.  Después de proporcionar la información de la nueva ubicación de la base de datos, complete el programa de instalación con los procesos y las configuraciones habituales. Cuando finalice la instalación, el sitio se reinicia y comienza a utilizar la nueva ubicación de la base de datos.    

10. Para limpiar los servidores que eran miembros del grupo de disponibilidad, siga las instrucciones de [Quitar un grupo de disponibilidad (SQL Server)](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server) en la documentación de SQL Server.
