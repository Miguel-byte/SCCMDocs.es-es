---
title: Mantenimiento de las actualizaciones de software
titleSuffix: Configuration Manager
description: Para mantener las actualizaciones en Configuration Manager, puede programar la tarea de limpieza de WSUS o ejecutarla de forma manual.
author: mestew
ms.date: 07/30/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: mstewart
ms.collection: M365-identity-device-management
ms.openlocfilehash: 11a817b907a27c0991fe6fc610063e1151ae94f9
ms.sourcegitcommit: 75f48834b98ea6a238d39f24e04c127b2959d913
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2019
ms.locfileid: "68604537"
---
# <a name="software-updates-maintenance"></a>Mantenimiento de las actualizaciones de software

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede programar y ejecutar la tarea de limpieza de WSUS desde la consola de Configuration Manager desde las propiedades del componente de punto de actualización de software. Cuando se seleccione ejecutar la tarea de limpieza de WSUS por primera vez, se ejecutará después de la siguiente sincronización de actualizaciones de software.  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Para programar y ejecutar el trabajo de limpieza de WSUS

Programar el trabajo de limpieza de WSUS mediante la ejecución de los siguientes pasos:

1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Configuración del sitio** > **Sitios**.
2. Seleccione el sitio en la parte superior de la jerarquía de Configuration Manager.

3. Haga clic en **Configurar componentes de sitio** en el grupo **Configuración** y, a continuación, haga clic en **Punto de actualización de software** para abrir las propiedades del componente de punto de actualización de software.  

4. Revise el **Comportamiento de sustitución**. Modifique el comportamiento si es necesario.

   ![Captura de pantalla de comportamiento de sustitución](media/sccm-supersedence-behavior.PNG)

5. Haga clic en la pestaña **Reglas de sustitución**, seleccione **Ejecutar el Asistente para la limpieza de WSUS**. En la versión 1806, se cambia el nombre de la opción a **Ejecutar limpieza de WSUS después de la sincronización**.

6. Haga clic en **Aceptar** (haga clic en **Cerrar** si está ejecutando la versión 1806).

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>Comportamiento de limpieza de WSUS en la versión 1802 y versiones anteriores

Antes de la versión 1806 de Configuration Manager, la opción de limpieza de WSUS ejecuta el siguiente elemento:

- La opción **Actualizaciones caducadas** del Asistente para la limpieza de WSUS solo en el servidor de WSUS del sitio de nivel superior.

  ![Captura de pantalla de limpieza de actualizaciones expiradas de WSUS](media/wsus-cleanup-expired.PNG)

- Se produce una limpieza de los elementos de configuración de actualización de software en la base de datos de Configuration Manager cada siete días y quita las actualizaciones innecesarias de la consola.
  - Esta limpieza no quita las actualizaciones expiradas de la consola de Configuration Manager si están implementadas actualmente.

El mantenimiento adicional sigue siendo necesario en la base de datos de WSUS de nivel superior y todas las demás bases de datos de WSUS en el entorno. Para obtener más información e instrucciones, vea la entrada de blog [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance (La guía completa para el mantenimiento de Microsoft WSUS y Configuration Manager SUP)](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/).

## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>Comportamiento de limpieza de WSUS a partir de la versión 1806

A partir de la versión 1806, la opción de limpieza de WSUS se produce después de cada sincronización y realiza los siguientes elementos de limpieza:
<!--1357898 -->

- La opción **Actualizaciones expiradas** para los servidores WSUS en CAS y sitios primarios.
  - Los servidores WSUS para sitios secundarios no ejecutan la limpieza de WSUS para actualizaciones expiradas.
- Configuration Manager genera una lista de actualizaciones reemplazadas de su base de datos. La lista se basa en el comportamiento de sustitución en las propiedades del componente de punto de actualización de software.
  - Los elementos de configuración de actualización que cumplen los criterios de comportamiento de sustitución expiran en la consola de Configuration Manager.
  - Se rechazan las actualizaciones en WSUS para las CAS y los sitios primarios, pero no para los sitios secundarios.
- Se produce una limpieza de los elementos de configuración de actualización de software en la base de datos de Configuration Manager cada siete días y quita las actualizaciones innecesarias de la consola.
  - Esta limpieza no quita las actualizaciones expiradas de la consola de Configuration Manager si están implementadas actualmente.

> [!NOTE]
> Los "Meses de espera antes de que una actualización reemplazada expire" se basan en la fecha de creación de la actualización de reemplazo. Por ejemplo, si usa 2 meses para esta configuración, WSUS rechazará las actualizaciones que han sido reemplazadas y expirarán en Configuration Manager cuando la actualización de reemplazo tenga 2 meses de antigüedad.

Todo el mantenimiento de WSUS debe ejecutarse manualmente en las bases de datos de WSUS del sitio secundario. Las siguientes opciones del **Asistente para la limpieza de WSUS Server** no se ejecutan en las CAS y los sitios primarios:

- Actualizaciones y revisiones de actualización sin usar
- Equipos que no se ponen en contacto con el servidor
- Archivos de actualización innecesarios

  Para obtener más información e instrucciones, vea la entrada de blog [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance (La guía completa para el mantenimiento de Microsoft WSUS y Configuration Manager SUP)](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/).

## <a name="wsus-cleanup-behavior-starting-in-version-1810"></a>Comportamiento de limpieza de WSUS a partir de la versión 1810

A partir de la versión 1810, puede especificar reglas de sustitución por un lado para actualizaciones de características, y por otro para actualizaciones que no son de características, en las propiedades de componentes del punto de actualización de software. La opción de limpieza de WSUS se produce después de cada sincronización y realiza los siguientes elementos de limpieza:
<!--2839349,3098809, 2977644-->

- La opción **Actualizaciones expiradas** para los servidores WSUS en CAS, sitios primarios y sitios secundarios.
- Configuration Manager genera una lista de actualizaciones reemplazadas de su base de datos. La lista se basa en el comportamiento de sustitución en las propiedades del componente de punto de actualización de software.
  - Los elementos de configuración de actualización que cumplen los criterios de comportamiento de sustitución expiran en la consola de Configuration Manager.
  - Se rechazarán las actualizaciones en WSUS para CAS, los sitios primarios y los sitios secundarios.
- Se produce una limpieza de los elementos de configuración de actualización de software en la base de datos de Configuration Manager cada siete días y quita las actualizaciones innecesarias de la consola.
  - Esta limpieza no quita las actualizaciones expiradas de la consola de Configuration Manager si están implementadas actualmente.

> [!NOTE]
> Los "Meses de espera antes de que una actualización reemplazada expire" se basan en la fecha de creación de la actualización de reemplazo. Por ejemplo, si usa 2 meses para esta configuración, WSUS rechazará las actualizaciones que han sido reemplazadas y expirarán en Configuration Manager cuando la actualización de reemplazo tenga 2 meses de antigüedad.

Las siguientes opciones del **Asistente para la limpieza de WSUS Server** no se ejecutan en las CAS, los sitios primarios y los sitios secundarios:

- Actualizaciones y revisiones de actualización sin usar
- Equipos que no se ponen en contacto con el servidor
- Archivos de actualización innecesarios

  Para obtener más información e instrucciones, vea la entrada de blog [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance (La guía completa para el mantenimiento de Microsoft WSUS y Configuration Manager SUP)](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/).

## <a name="wsus-cleanup-starting-in-version-1906"></a>Limpieza de WSUS a partir de la versión 1906
<!--41101009-->

 Tiene tareas de mantenimiento de WSUS adicionales que Configuration Manager pueden ejecutar para mantener puntos de actualización de software correctos. Además de rechazar las actualizaciones expiradas en WSUS, Configuration Manager puede agregar índices no clúster a las bases de datos de WSUS y quitar las actualizaciones obsoletas de las bases de datos de WSUS. El mantenimiento de WSUS se produce después de cada sincronización.

### <a name="add-non-clustered-indexes-to-the-wsus-database-to-improve-wsus-cleanup-performance"></a>Agregar índices no agrupados a la base de datos de WSUS para mejorar el rendimiento de la limpieza de WSUS

La adición de índices no clúster mejora el rendimiento de la limpieza de WSUS que Configuration Manager.

1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Configuración del sitio** > **Sitios**.
2. Seleccione el sitio en la parte superior de la jerarquía de Configuration Manager.
3. Haga clic en **Configurar componentes de sitio** en el grupo Configuración y, a continuación, haga clic en **Punto de actualización de software** para abrir las propiedades del componente de punto de actualización de software.
4. En la pestaña **WSUS Maintenance** (Mantenimiento de WSUS), seleccione **Add non-clustered indexes to the WSUS database** (Agregar índices no en clúster a la base de datos de WSUS).
5. En cada SUSDB usado por Configuration Manager, los índices se agregan a las tablas siguientes:
   - tbLocalizedPropertyForRevision
   - tbRevisionSupersedesUpdate

#### <a name="sql-permissions-for-creating-indexes"></a>Permisos SQL para crear índices

Cuando la base de datos WSUS se encuentra en un servidor SQL remoto, la cuenta de equipo del servidor de sitio necesita los siguientes permisos de SQL:

- Para crear un índice se requiere el permiso `ALTER` en la tabla o la vista. La cuenta de equipo del servidor de sitio debe ser un miembro del rol fijo de servidor `sysadmin` o de los roles fijos de base de datos `db_ddladmin` y `db_owner`. Para más información sobre la creación, el índice y los permisos, consulte [CREATE INDEX (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-index-transact-sql?view=sql-server-2017#permissions).
- El permiso de servidor `CONNECT SQL` se debe conceder a la cuenta de equipo del servidor de sitio. Para más información, consulte [GRANT (permisos de servidor de Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017). 

> [!NOTE]  
>  Si la base de datos de WSUS se encuentra en un servidor SQL remoto mediante un puerto no predeterminado, entonces puede que los índices no se agreguen. Puede crear un [alias de servidor mediante SQL Server Configuration Manager](https://docs.microsoft.com/sql/database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client?view=sql-server-2017) para este escenario. Una vez que se agrega el alias y Configuration Manager puede realizar una conexión a la base de datos de WSUS, se agregarán los índices.

### <a name="remove-obsolete-updates-from-the-wsus-database"></a>Quitar actualizaciones obsoletas de la base de datos de WSUS

Las actualizaciones obsoletas son actualizaciones sin usar y revisiones de actualización en la base de datos de WSUS. Por lo general, una actualización se considera obsoleta una vez que ya no está en el [Catálogo de Microsoft Update](https://www.catalog.update.microsoft.com/) y no es necesaria para otras actualizaciones como requisito previo o dependencia.

1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Configuración del sitio** > **Sitios**.
2. Seleccione el sitio en la parte superior de la jerarquía de Configuration Manager.
3. Haga clic en **Configurar componentes de sitio** en el grupo Configuración y, a continuación, haga clic en **Punto de actualización de software** para abrir las propiedades del componente de punto de actualización de software.
4. En la pestaña **Mantenimiento de WSUS**, seleccione **Remove obsolete updates from the WSUS database** (Quitar las actualizaciones obsoletas de la base de datos de WSUS).
   - Se permitirá que la eliminación de actualizaciones obsoletas se ejecute hasta un máximo de 30 minutos antes de detenerse. Se volverá a iniciar después de que se produzca la siguiente sincronización.  

#### <a name="sql-permissions-for-removing-obsolete-updates"></a>Permisos SQL para quitar actualizaciones obsoletas

Cuando la base de datos WSUS se encuentra en un servidor SQL remoto, la cuenta de equipo del servidor de sitio necesita los siguientes permisos de SQL:

- Los roles fijos de base de datos `db_datareader` y `db_datawriter`. Para más información, consulte [Roles de nivel de base de datos](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles?view=sql-server-2017#fixed-database-roles).
- El permiso de servidor `CONNECT SQL` se debe conceder a la cuenta de equipo del servidor de sitio. Para más información, consulte [GRANT (permisos de servidor de Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017).

## <a name="updates-cleanup-log-entries"></a>Actualiza las entradas de registro de limpieza

Puede comprobar esta limpieza revisando el archivo wsyncmgr.log para las siguientes entradas:

- El rechazo de actualizaciones reemplazadas en WSUS estará completado cuando vea esta entrada del registro: `Cleanup processed <number> total updates and declined <number>`
- Cuando vea esta entrada se estará iniciando la limpieza de WSUS: `Calling WSUS Cleanup.`
- La limpieza de WSUS para las actualizaciones expiradas estará completa cuando vea esta entrada: `Successfully completed WSUS Cleanup.`
- El limpiador de elementos de configuración de actualizaciones expiradas de Configuration Manager se estará iniciando cuando vea esta entrada: `Deleting old expired updates...`
- El limpiador de elementos de configuración de actualizaciones expiradas de Configuration Manager estará completado cuando vea esta entrada: `Deleted <number> expired updates total`
