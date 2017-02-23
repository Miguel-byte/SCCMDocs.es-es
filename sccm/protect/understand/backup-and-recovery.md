---
title: "Copia de seguridad y recuperación | Microsoft Docs"
description: "Aprenda a realizar copias de seguridad de los sitios y a recuperarlos en caso de error o pérdida de datos en System Center Configuration Manager."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3aa9f2e4d3f7210981b5b84942485de11fe15cb2
ms.openlocfilehash: a7e052bc0e1c354b75a7f95afdd266ed742ce689

---

# <a name="backup-and-recovery"></a>Copia de seguridad y recuperación

*Se aplica a: System Center Configuration Manager (rama actual)*

Prepare enfoques de copia de seguridad y recuperación para evitar la pérdida de datos. En los sitios de Configuration Manager, un enfoque de copia de seguridad y recuperación puede ayudar a recuperar sitios y jerarquías más rápidamente y con la mínima pérdida de datos. Las secciones de este tema pueden ayudarle a realizar copias de seguridad de los sitios y a recuperar un sitio en caso de error o pérdida de datos.  



- [Hacer una copia de seguridad de un sitio de Configuration Manager](#BKMK_SiteBackup)   

  - [Tarea de mantenimiento de copia de seguridad](#BKMK_BackupMaintenanceTask)   

  - [Uso de Data Protection Manager para realizar copias de seguridad de la base de datos del sitio](#BKMK_DPMBackup)   

  -  [Archivo de la instantánea de copia de seguridad](#BKMK_ArchivingBackupSnapshot)   

  -  [Uso del archivo AfterBackup.bat](#BKMK_UsingAfterBackup)   

  -  [Tareas de copia de seguridad adicionales](#BKMK_SupplementalBackup)   

-  [Recuperar un sitio de Configuration Manager](#BKMK_RecoverSite)   

  -   [Determinar las opciones de recuperación](#BKMK_DetermineRecoveryOptions)   

         -   [Opciones de recuperación de servidor de sitio](#BKMK_SiteServerRecoveryOptions)   

         -   [Opciones de recuperación de base de datos de sitio](#BKMK_SiteDatabaseRecoveryOption)   

         -   [Período de retención de seguimiento de cambios de SQL Server](#bkmk_SQLretention)   

         -   [Proceso para reinicializar datos globales o del sitio](#bkmk_reinit)   

         -   [Escenarios de recuperación de base de datos de sitio](#BKMK_SiteDBRecoveryScenarios)  

  -   [Claves de archivo de script de recuperación de sitio desatendida](#BKMK_UnattendedSiteRecoveryKeys)  

  -   [Tareas posteriores a la recuperación](#BKMK_PostRecovery)  

  -   [Recuperar un sitio secundario](#BKMK_RecoverSecondarySite)  

-   [Servicio SMS Writer](#BKMK_SMSWriterService)  

> [!NOTE]  
>  Si usa un grupo de disponibilidad AlwaysOn de SQL Server para hospedar la base de datos de sitio, modifique los planes de recuperación y copia de seguridad tal como se explica en la sección [Changes for Backup and Recovery when you use a SQL Server AlwaysOn availability group (Cambios en Copia de seguridad y recuperación cuando se usa un grupo de disponibilidad AlwaysOn de SQL Server)](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#bkmk_BnR) del tema [SQL Server AlwaysOn for a highly available site database for System Center Configuration Manager (SQL Server AlwaysOn para una base de datos de sitio de alta disponibilidad para System Center Configuration Manager)](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

##  <a name="a-namebkmksitebackupa-back-up-a-configuration-manager-site"></a><a name="BKMK_SiteBackup"></a> Hacer una copia de seguridad de un sitio de Configuration Manager  
 Configuration Manager tiene una tarea de mantenimiento de copia de seguridad que:  

-   Se ejecuta según una programación  

-   Realiza copias de seguridad de la base de datos del sitio  

-   Realiza copias de seguridad de claves de registro específicas  

-   Realiza copias de seguridad de carpetas y archivos específicos  

-   Realiza copias de seguridad de la carpeta **CD.Latest** (vea [La carpeta CD.Latest para System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md))  

 Planee la ejecución de la tarea de copia de seguridad del sitio predeterminada cada cinco días como mínimo. Esto se debe a que Configuration Manager usa un [período de retención del seguimiento de cambios de SQL Server](#bkmk_SQLretention) de cinco días.  

 Para simplificar el proceso de copia de seguridad, puede crear un archivo **AfterBackup.bat** para realizar automáticamente acciones posteriores a la copia de seguridad después de que la tarea de mantenimiento de copia de seguridad se ejecute correctamente. El archivo AfterBackup.bat se suele usar para archivar la instantánea de copia de seguridad en una ubicación segura. También puede usar el archivo AfterBackup.bat para copiar archivos en la carpeta de copia de seguridad e iniciar otras tareas de copia de seguridad adicionales.

Use las secciones siguientes como ayuda para crear la estrategia de copia de seguridad de Configuration Manager.  

> [!NOTE]  
>  Configuration Manager puede recuperar la base de datos de sitio a partir de la tarea de mantenimiento de copia de seguridad de Configuration Manager o desde una copia de seguridad de la base de datos de sitio que creara con otro proceso. Por ejemplo, puede restaurar la base de datos de sitio desde una copia de seguridad creada como parte de un plan de mantenimiento de Microsoft SQL Server. Puede restaurar la base de datos de sitio a partir de una copia de seguridad creada con System Center 2012 Data Protection Manager (DPM). Para obtener más información, vea [Uso de Data Protection Manager para realizar copias de seguridad de la base de datos del sitio](#BKMK_DPMBackup).  

###  <a name="a-namebkmkbackupmaintenancetaska-backup-maintenance-task"></a><a name="BKMK_BackupMaintenanceTask"></a> Tarea de mantenimiento de copia de seguridad  
 Puede automatizar la copia de seguridad de sitios de Configuration Manager mediante la programación de la tarea de mantenimiento predefinida Copia de seguridad del servidor del sitio. Puede hacer una copia de seguridad de un sitio de administración central y un sitio primario, pero no existe compatibilidad con la copia de seguridad de servidores de sistema de sitio o sitios secundarios. Cuando se ejecuta el servicio de copia de seguridad de Configuration Manager, este sigue las instrucciones definidas en el archivo de control de copia de seguridad (**&lt;carpetaInstalaciónConfigMgr\>\Inboxes\Smsbkup.box\Smsbkup.ctl**). Puede modificar el archivo de control de copia de seguridad para cambiar el comportamiento del servicio de copia de seguridad. La información del estado de copia de seguridad del sitio se escribe en el archivo **Smsbkup.log** . Este archivo se crea en la carpeta de destino que especifique en las propiedades de la tarea de mantenimiento Copia de seguridad del servidor del sitio.  


##### <a name="to-enable-the-site-backup-maintenance-task"></a>Para habilitar la tarea de mantenimiento de copia de seguridad de sitio  

1.  En la consola de Configuration Manager, abra **Administración** > **Configuración del sitio**  

     \> **Sitios**.  

2.  Seleccione el sitio en el que desee habilitar la tarea de mantenimiento de copia de seguridad de sitio.  

3.  En la pestaña **Inicio**, en el grupo **Configuración**, elija **Tareas de mantenimiento del sitio**.  

4.  Elija **Copia de seguridad del servidor del sitio**  >  **Editar**.  

5.  Elija **Habilitar esta tarea** > **Rutas de acceso** para especificar el destino de la copia de seguridad. Dispone de las siguientes opciones:  

    > [!IMPORTANT]  
    >  Con el fin de evitar la manipulación de los archivos de copia de seguridad, almacene los archivos en una ubicación segura. La ruta de acceso de copia de seguridad más segura es una unidad local, por lo que puede establecer los permisos del sistema de archivos NTFS en la carpeta. Configuration Manager no cifra los datos de copia de seguridad que se almacenan en la ruta de acceso de copia de seguridad.  

    -   **Unidad local en servidor de sitio para los datos y la base de datos del sitio**: especifica que los archivos de copia de seguridad del sitio y de la base de datos del sitio se almacenen en la ruta de acceso especificada en la unidad de disco local del servidor de sitio. Debe crear la carpeta local antes de que se ejecute la tarea de copia de seguridad.   La cuenta Sistema local en el servidor de sitio debe tener permisos del sistema de archivos NTFS de **escritura** en la carpeta local para la copia de seguridad del servidor de sitio. La cuenta Sistema local en el equipo que ejecute SQL Server debe tener permisos de NTFS de **escritura** en la carpeta local para la copia de seguridad de la base de datos del sitio.  

    -   **Ruta de acceso de red (nombre UNC) para los datos y la base de datos del sitio**: especifica que los archivos de copia de seguridad del sitio y de la base de datos del sitio se almacenan en la ruta de acceso UNC especificada. Tiene que crear el recurso compartido para poder ejecutar la tarea de copia de seguridad. La cuenta de equipo del servidor de sitio y la cuenta de equipo de SQL Server, si SQL Server está instalado en otro equipo, deben tener permisos de recurso compartido y NTFS **Escribir** en la carpeta de red compartida.  

    -   **Unidades locales en el servidor de sitio y SQL Server**: especifica que los archivos de copia de seguridad del sitio se almacenan en la ruta de acceso especificada de la unidad local del servidor de sitio y que los archivos de copia de seguridad de la base de datos del sitio se almacenan en la ruta de acceso especificada de la unidad local del servidor de base de datos del sitio. Debe crear las carpetas locales antes de que se ejecute la tarea de copia de seguridad. La cuenta de equipo del servidor de sitio debe tener permisos de NTFS de **escritura** en la carpeta que se crea en el servidor de sitio. La cuenta de equipo del servidor de SQL Server debe tener permisos de NTFS de **escritura** en la carpeta que se crea en el servidor de la base de datos del sitio. Esta opción solo está disponible cuando la base de datos del sitio no esté instalada en el servidor de sitio.  

    > [!NOTE]  
    >    - La opción de examinar el destino de la copia de seguridad solo está disponible cuando se especifica la ruta de acceso UNC del destino de la copia de seguridad.

    > - El nombre de la carpeta o el nombre del recurso compartido que se utilizan para el destino de la copia de seguridad no pueden usar caracteres Unicode.  


6.  Configure una programación para la tarea de copia de seguridad del sitio. Como práctica recomendada, considere la posibilidad de programar la copia de seguridad fuera del horario de trabajo activo. Si tiene una jerarquía, considere la posibilidad de una programación que se ejecute al menos dos veces por semana para asegurar la máxima retención de datos en caso de error en el sitio.  

    Cuando ejecute la consola de Configuration Manager en el mismo servidor de sitio que esté configurando para la copia de seguridad, la tarea de mantenimiento Copia de seguridad del servidor del sitio usará la hora local para la programación. Cuando la consola de Configuration Manager se ejecute desde un equipo remoto con respecto al sitio que esté configurando para la copia de seguridad, la tarea de mantenimiento Copia de seguridad del servidor del sitio usará UTC para la programación.  

7.  Elija si quiere crear una alerta en caso de error de la tarea de copia de seguridad del sitio, haga clic en **Aceptar** y luego en **Aceptar**. Cuando se selecciona, Configuration Manager crea una alerta crítica para el error de copia de seguridad que puede revisar en el nodo **Alertas** del área de trabajo **Supervisión**.  

 Luego, compruebe que se está ejecutando la tarea de mantenimiento Copia de seguridad del servidor del sitio para asegurarse de que se están creando copias de seguridad.  

##### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>Para comprobar que la tarea de mantenimiento Copia de seguridad del servidor del sitio se está ejecutando  

-   Compruebe que la tarea de mantenimiento Copia de seguridad del servidor del sitio se está ejecutando revisando cualquiera de los siguientes:  

    -   Compruebe la marca de tiempo en los archivos de la carpeta de destino de la copia de seguridad que creó la tarea. Compruebe que la marca de tiempo se ha actualizado con una hora que coincida con la hora programada para la ejecución más reciente de la tarea.  

    -   En el nodo **Estado del componente** del área de trabajo **Supervisión** , revise los mensajes de estado para SMS_SITE_BACKUP. Cuando la copia de seguridad del sitio se complete correctamente, verá el identificador de mensaje 5035, que indica que la copia de seguridad del sitio se completó sin errores.  

    -   Cuando la tarea de mantenimiento Copia de seguridad del servidor del sitio se configure para crear una alerta si se produce un error en la copia de seguridad, puede comprobar el nodo **Alertas** del área de trabajo **Supervisión** en busca de errores.  

    -   En &lt;*carpetaInstalaciónConfigMgr*>\Logs, revise el archivo Smsbkup.log en busca de errores y advertencias. Cuando la copia de seguridad del sitio se complete correctamente, verá `Backup completed` con una marca de tiempo y un identificador de mensaje `STATMSG: ID=5035`.  

    > [!TIP]  
    >  Cuando se produce un error en la tarea de mantenimiento de copia de seguridad, reinicie la tarea de copia de seguridad. Para ello, detenga y reinicie el servicio SMS_SITE_BACKUP.  

###  <a name="a-namebkmkdpmbackupa-using-data-protection-manager-to-back-up-your-site-database"></a><a name="BKMK_DPMBackup"></a> Uso de Data Protection Manager para realizar copias de seguridad de la base de datos del sitio  
 Puede usar System Center 2012 Data Protection Manager (DPM) para hacer una copia de seguridad de la base de datos del sitio. Debe crear un nuevo grupo de protección en DPM para el equipo de la base de datos del sitio. En la página **Seleccionar miembros del grupo** del asistente Crear nuevo grupo de protección, seleccione el servicio SMS Writer de la lista de orígenes de datos y, a continuación, seleccione la base de datos del sitio como un miembro apropiado. Para obtener más información acerca del uso de DPM para realizar una copia de seguridad de la base de datos del sitio, consulte la [Data Protection Manager Documentation Library (Biblioteca de documentación de Data Protection Manager)](http://go.microsoft.com/fwlink/?LinkId=272772) en TechNet.  

> [!IMPORTANT]  
>  Configuration Manager no admite la copia de seguridad de DPM en un clúster de SQL Server que use una instancia con nombre, pero admite la copia de seguridad de DPM en un clúster de SQL Server que use la instancia predeterminada de SQL Server.  

 Después de restaurar la base de datos del sitio, siga los pasos descritos en el programa de instalación para recuperar el sitio. Seleccione la opción de recuperación **Usar una base de datos del sitio que se ha recuperado manualmente** para usar la base de datos de sitio que recuperó con Data Protection Manager.  

###  <a name="a-namebkmkarchivingbackupsnapshota-archiving-the-backup-snapshot"></a><a name="BKMK_ArchivingBackupSnapshot"></a> Archivo de la instantánea de copia de seguridad  
 La primera vez que se ejecuta la tarea de mantenimiento Copia de seguridad del servidor del sitio, se crea una instantánea de la copia de seguridad, que puede utilizar para recuperar el servidor de sitio en caso de error. Cuando la tarea de copia de seguridad se ejecuta de nuevo durante ciclos posteriores, se crea una nueva instantánea de la copia de seguridad que sobrescribe la instantánea anterior. Como resultado, el sitio solo tiene una instantánea de copia de seguridad y no hay forma de recuperar la instantánea de una copia de seguridad anterior.  

 Se recomienda conservar varios archivos de la instantánea de copia de seguridad por los siguientes motivos:  

-   Es común que los medios de copia de seguridad presenten errores, estén en una ubicación incorrecta o contengan solo una copia de seguridad parcial. La recuperación de un sitio primario independiente con errores desde una copia de seguridad antigua es mejor que una recuperación sin ninguna copia de seguridad. En el caso de un servidor de sitio de una jerarquía, la copia de seguridad debe estar en el período de retención de seguimiento de cambios de SQL Server, o no es necesaria.  

-   La existencia de daños en el sitio puede pasar desapercibida durante varios ciclos de copia de seguridad. Es posible que tenga que usar una instantánea de copia de seguridad anterior al momento en que el sitio resultó dañado. Esto se aplica a un sitio primario independiente y a los sitios de una jerarquía donde la copia de seguridad está en el período de retención de seguimiento de cambios de SQL Server.  

-   El sitio podría no tener ninguna instantánea de copia de seguridad si, por ejemplo, se produce un error en la tarea de mantenimiento Copia de seguridad del servidor del sitio. Dado que la tarea de copia de seguridad elimina la instantánea de copia de seguridad anterior antes de empezar a realizar la copia de seguridad de los datos actuales, no habrá una instantánea de copia de seguridad válida.  

###  <a name="a-namebkmkusingafterbackupa-using-the-afterbackupbat-file"></a><a name="BKMK_UsingAfterBackup"></a> Uso del archivo AfterBackup.bat  
 Después de realizar la copia de seguridad del sitio correctamente, la tarea Copia de seguridad del servidor del sitio automáticamente intenta ejecutar un archivo llamado AfterBackup.bat. Debe crear manualmente el archivo AfterBackup.bat en &lt;*carpetaInstalaciónConfigMgr*>\Inboxes\Smsbkup. Si hay un archivo AfterBackup.bat y está almacenado en la carpeta correcta, se ejecuta automáticamente después de completarse la tarea de copia de seguridad. El archivo AfterBackup.bat permite archivar la instantánea de copia de seguridad al final de cada operación de copia de seguridad y realizar automáticamente otras tareas posteriores a la copia de seguridad que no forman parte de la tarea de mantenimiento Copia de seguridad del servidor del sitio. El archivo AfterBackup.bat integra las operaciones de archivo y copia de seguridad, por lo que garantiza que se archiva cada nueva instantánea de copia de seguridad. Si el archivo AfterBackup.bat no está presente, la tarea de copia de seguridad lo omite sin que se vea afectada la operación de copia de seguridad. Para comprobar que la tarea de copia de seguridad del sitio ejecutó correctamente el archivo AfterBackup.bat, consulte el nodo **Estado del componente** del área de trabajo **Supervisión** y revise los mensajes de estado de SMS_SITE_BACKUP. Si la tarea inició correctamente el archivo de comandos AfterBackup.bat, verá el mensaje ID 5040.  

> [!TIP]  
>  Para crear el archivo AfterBackup.bat para archivar los archivos de copia de seguridad del servidor de sitio, debe usar una herramienta de comando de copia, como Robocopy, en el archivo por lotes. Por ejemplo, podría crear el archivo AfterBackup.bat y, en la primera línea, podría agregar algo similar a lo siguiente: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`. Para más información sobre Robocopy, consulte la página web de referencia de la línea de comandos de [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408) .  

 Aunque el uso previsto de AfterBackup.bat es archivar las instantáneas de copia de seguridad, puede crear un archivo AfterBackup.bat para realizar tareas adicionales al final de cada operación de copia de seguridad.  

###  <a name="a-namebkmksupplementalbackupa-supplemental-backup-tasks"></a><a name="BKMK_SupplementalBackup"></a> Tareas de copia de seguridad adicionales  
 La tarea de mantenimiento Copia de seguridad del servidor del sitio facilita una instantánea de copia de seguridad para los archivos de servidor de sitio y la base de datos de sitio, pero hay otros elementos cuya copia de seguridad no se realiza y que debe tener en cuenta cuando crea la estrategia de copia de seguridad. Use las secciones siguientes como ayuda para completar la estrategia de copia de seguridad de Configuration Manager.  

#### <a name="back-up-custom-reporting-services-reports"></a>Copia de seguridad de informes personalizados de Reporting Services  
 Si modifica informes personalizados creados o predefinidos de Reporting Services, la creación de una copia de seguridad de los archivos de base de datos del servidor de informes es una parte importante de la estrategia de copia de seguridad. La copia de seguridad del servidor de informes debe incluir una copia de seguridad de los archivos de origen de informes y modelos, claves de cifrado, extensiones o ensamblados personalizados, archivos de configuración, vistas personalizadas de SQL Server utilizadas en informes personalizados, procedimientos almacenados personalizados, etc.  

> [!IMPORTANT]  
>  Cuando Configuration Manager se actualiza a una versión más reciente, los nuevos informes podrían sobrescribir los informes predefinidos. Si modifica un informe predefinido, realice una copia de seguridad y luego restáurela en Reporting Services.  

 Para más información acerca de la copia de seguridad de los informes personalizados en Reporting Services, consulte [Operaciones de copias de seguridad y restauración para una instalación de Reporting Services](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) en Libros en pantalla de SQL Server 2014.  

#### <a name="backup-content-files"></a>Copia de seguridad de archivos de contenido  
 La biblioteca de contenido de Configuration Manager es la ubicación donde se almacenan todos los archivos de contenido de actualizaciones de software, aplicaciones, implementación de sistema operativo, etc. La biblioteca de contenido se encuentra en el servidor de sitio y en cada punto de distribución. La tarea de mantenimiento Copia de seguridad del servidor del sitio no incluye una copia de seguridad de la biblioteca de contenido o los archivos de origen del paquete. Cuando se produce un error en el servidor de sitio, la información acerca de los archivos de la biblioteca de contenido se restaura en la base de datos de sitio, pero usted debe restaurar la biblioteca de contenido y los archivos de origen del paquete en el servidor de sitio.  

-   **Biblioteca de contenido**: se debe restaurar esta biblioteca para poder redistribuir el contenido a los puntos de distribución. Cuando inicia la redistribución de contenido, Configuration Manager copia los archivos de la biblioteca de contenido del servidor de sitio en los puntos de distribución. La biblioteca de contenido del servidor de sitio se encuentra en la carpeta SCCMContentLib, que suele ubicarse en la unidad con más espacio libre en disco en el momento en que se instaló el sitio.  

-   **Archivos de origen del paquete**: es necesario restaurar estos archivos para poder actualizar el contenido de los puntos de distribución. Cuando inicia una actualización de contenido, Configuration Manager copia los archivos nuevos o modificados del origen del paquete en la biblioteca de contenido, que a su vez copia los archivos en los puntos de distribución asociados. Puede ejecutar la siguiente consulta en SQL Server para buscar la ubicación del origen del paquete para todos los paquetes y aplicaciones: `SELECT * FROM v_Package`. Puede identificar el sitio del origen del paquete mediante los tres primeros caracteres del identificador del paquete. Por ejemplo, si el identificador del paquete es CEN00001, el código de sitio del sitio de origen es CEN. Cuando restaure los archivos de origen del paquete, debe hacerlo en la misma ubicación en la que se encontraban antes del error.  

 Compruebe que incluye las ubicaciones de la biblioteca de contenido y del origen del paquete en la copia de seguridad del sistema de archivos del servidor de sitio.  

#### <a name="back-up-custom-software-updates"></a>Copia de seguridad de actualizaciones de software personalizadas  
 System Center Updates Publisher 2011 es una herramienta independiente que le permite publicar actualizaciones de software personalizadas en Windows Server Update Services (WSUS), sincronizar las actualizaciones de software con Configuration Manager, evaluar el cumplimiento de las actualizaciones de software e implementar las actualizaciones de software personalizadas en los clientes. Updates Publisher usa una base de datos local para el repositorio de actualizaciones de software. Si usa Updates Publisher para administrar las actualizaciones de software personalizadas, determine si tiene que incluir la base de datos de Updates Publisher en el plan de copias de seguridad. Para obtener más información acerca de Updates Publisher, consulte [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) en la biblioteca de TechCenter de System Center.  

 Use el siguiente procedimiento para realizar una copia de seguridad de la base de datos de Updates Publisher.  

###### <a name="to-back-up-the-updates-publisher-2011-database"></a>Para realizar una copia de seguridad de la base de datos de Updates Publisher 2011  

1.  En el equipo que ejecuta Updates Publisher, busque el archivo de base de datos de Updates Publisher (Scupdb.sdf) en %*PERFILUSUARIO*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\. Hay un archivo de base de datos diferente para cada usuario que ejecuta Updates Publisher.  

2.  Copie el archivo de base de datos en el destino de la copia de seguridad. Por ejemplo, si el destino de la copia de seguridad es E:\ConfigMgr_Backup, podría copiar el archivo de base de datos de Updates Publisher en E:\ConfigMgr_Backup\SCUP2011.  

    > [!TIP]  
    >  Si hay más de un archivo de base de datos en un equipo, puede almacenar el archivo en una subcarpeta que indique el perfil de usuario asociado al archivo de base de datos. Por ejemplo, podría tener un archivo de base de datos en E:\ConfigMgr_Backup\SCUP2011\Usuario1 y otro archivo de base de datos en E:\ConfigMgr_Backup\SCUP2011\Usuario2.  

### <a name="user-state-migration-data"></a>Datos de migración de estado de usuario  
 Puede usar secuencias de tareas de Configuration Manager para capturar y restaurar los datos de estado de usuario en los escenarios de implementación de sistema operativo donde quiere conservar el estado de usuario del sistema operativo actual. Las carpetas donde se almacenan los datos de estado de usuario se enumeran en las propiedades del punto de migración de estado. La tarea de mantenimiento Copia de seguridad del servidor del sitio no incluye la copia de seguridad de los datos de migración de estado de usuario. Como parte del plan de copias de seguridad, debe realizar manualmente la copia de seguridad de las carpetas que especifique para almacenar los datos de migración de estado de usuario.   

#### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>Para determinar las carpetas utilizadas para almacenar los datos de migración de estado de usuario  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración**, expanda **Configuración del sitio** y elija **Servidores y roles del sistema de sitios**.  

3.  Seleccione el sistema de sitio que hospeda el rol de migración de estado y luego elija **Punto de migración de estado** en **Roles del sistema de sitio**.  


4.  En la pestaña **Rol del sitio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  
5.  Las carpetas donde se almacenan los datos de migración de estado de usuario se enumeran en la sección **Detalles de la carpeta** de la pestaña **General**.  

## <a name="recover-a-configuration-manager-site"></a>Recuperar un sitio de Configuration Manager
 Es necesario llevar a cabo una recuperación de sitio de Configuration Manager siempre que se produce un error en un sitio de Configuration Manager o se pierden datos de la base de datos de sitio. Reparar y volver a sincronizar datos son las tareas principales de una recuperación de sitio y son necesarias para evitar la interrupción de las operaciones.  

> [!IMPORTANT]  
>  Al recuperar la base de datos de un sitio:  

>  -   Debe usar la misma versión y edición de SQL Server. Por ejemplo, no se admite la restauración de una base de datos que se ejecutaba en SQL Server 2012 en SQL Server 2014. De igual forma, no se admite la restauración de una base de datos de sitio que se ejecutaba en SQL Server 2014 Standard Edition en SQL Server 2014 Enterprise Edition.  
> -   SQL Server no debe estar establecido en el **modo de usuario único**.  
> -   Asegúrese de que los archivos .mdf y .ldf sean válidos. Al recuperar un sitio, no se realiza ninguna comprobación del estado de los archivos que se están restaurando.  


 La recuperación del sitio se inicia al ejecutar el Asistente para instalación de Configuration Manager desde la carpeta CD.Latest.  También puede configurar el script de instalación desatendida y luego usar la opción **/script** de comando de instalación para ejecutar la instalación desde esta misma carpeta CD.Latest. Las opciones de recuperación varían en función de si tiene o no una copia de seguridad de la base de datos de sitio de Configuration Manager. Para más información, vea [La carpeta CD.Latest para System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md).  

> [!IMPORTANT]  
>  Si ejecuta el programa de instalación de Configuration Manager desde el menú **Inicio** del servidor de sitio, la opción **Recuperar un sitio** no estará disponible.  

>  Si ha instalado alguna actualización desde la consola de Configuration Manager antes de hacer la copia de seguridad, no puede reinstalar correctamente el sitio mediante el programa de instalación desde medios de instalación o la ruta de instalación de Configuration Manager.  

> [!NOTE]  
>  Después de restaurar una base de datos de sitio configurada para réplicas de base de datos, para poder utilizar las réplicas de base de datos debe volver a configurar cada réplica de base de datos y volver a crear tanto las publicaciones como las suscripciones.  

###  <a name="a-namebkmkdeterminerecoveryoptionsa-determine-your-recovery-options"></a><a name="BKMK_DetermineRecoveryOptions"></a> Determinar las opciones de recuperación  
 Debe tener en cuenta dos áreas principales para la recuperación del sitio de administración central y del servidor de sitio primario de Configuration Manager: el servidor de sitio y la base de datos de sitio. Consulte las siguientes secciones para poder determinar las opciones que debe seleccionar para el escenario de recuperación.  

> [!NOTE]  

####  <a name="a-namebkmksiteserverrecoveryoptionsa-site-server-recovery-options"></a><a name="BKMK_SiteServerRecoveryOptions"></a> Opciones de recuperación de servidor de sitio  
 Debe iniciar el programa de instalación a partir de una copia de la carpeta CD.Latest creada fuera de la carpeta de instalación de Configuration Manager. A continuación, seleccione la opción **Recuperar un sitio** . Cuando ejecuta el programa de instalación, cuenta con las siguientes opciones de recuperación para el servidor de sitio con errores:  

-   **Recuperar el servidor de sitio mediante una copia de seguridad existente**: use esta opción si tiene una copia de seguridad del servidor de sitio de Configuration Manager que se creó en el servidor de sitio como parte de la tarea de mantenimiento **Copia de seguridad del servidor del sitio** antes de que se produjeran errores en el sitio. Se vuelve a instalar y se configura el sitio a partir del sitio cuya copia de seguridad se realizó.  

-   **Reinstalar el servidor de sitio**: use esta opción si no tiene una copia de seguridad del servidor de sitio. Se vuelve a instalar el servidor del sitio, y debe especificar la configuración del sitio tal como lo haría durante la instalación inicial. Para recuperar correctamente el sitio, debe utilizar el mismo código de sitio y el mismo nombre de base de datos de sitio utilizados cuando se instaló por primera vez el sitio con errores.  

> [!NOTE]  
>  Cuando el programa de instalación detecta que hay un sitio de Configuration Manager en el servidor, puede iniciar una recuperación de sitio, pero las opciones de recuperación del servidor de sitio estarán limitadas. Por ejemplo, si ejecuta el programa de instalación en un servidor de sitio existente, al elegir la recuperación podrá recuperar el servidor de base de datos de sitio, pero la opción de recuperación del servidor de sitio estará deshabilitada.  

####  <a name="a-namebkmksitedatabaserecoveryoptiona-site-database-recovery-options"></a><a name="BKMK_SiteDatabaseRecoveryOption"></a> Opciones de recuperación de base de datos de sitio  
 Cuando ejecuta el programa de instalación, tiene las siguientes opciones de recuperación para la base de datos de sitio:  

-   **Recuperar la base de datos de sitio con un conjunto de copia de seguridad**: use esta opción si tiene una copia de seguridad de la base de datos de sitio de Configuration Manager que se creó como parte de la tarea de mantenimiento **Copia de seguridad del servidor del sitio** ejecutada en el sitio antes de que se produjeran errores en la base de datos del sitio. Si hay una jerarquía, los cambios realizados en la base de datos de sitio después de la última copia de seguridad de la base de datos de sitio se recuperan del sitio de administración central para un sitio primario, o de un sitio primario de referencia para un sitio de administración central. Si recupera la base de datos del sitio para un sitio primario independiente, perderá los cambios que se hayan realizado en el sitio desde la copia de seguridad más reciente.  

     Cuando se recupera la base de datos de un sitio de una jerarquía, el comportamiento de la recuperación estará en función de si se trata del sitio de administración central o un sitio primario, o de si la copia de seguridad más reciente pertenece o no al período de retención de seguimiento de cambios de SQL. Para obtener más información, consulte la sección [Escenarios de recuperación de base de datos de sitio](#BKMK_SiteDBRecoveryScenarios) de este tema.  

    > [!NOTE]  
    >  La recuperación no se completará correctamente si selecciona restaurar la base de datos del sitio mediante un conjunto de copia de seguridad, pero la base de datos del sitio ya existe.  

-   **Crear una nueva base de datos para este sitio**: use esta opción si no tiene una copia de seguridad de la base de datos de sitio de Configuration Manager. Si hay una jerarquía, se creará una base de datos del sitio nueva, y los datos se recuperarán a partir de datos replicados del sitio de administración central para un sitio primario, o del sitio primario de referencia para un sitio de administración central. Esta opción no está disponible cuando se recupera un sitio primario independiente o un sitio de administración central que no tiene sitios primarios.  

-   **Usar una base de datos del sitio que se ha recuperado manualmente**: use esta opción si ya recuperó la base de datos de sitio de Configuration Manager, pero tiene que completar el proceso de recuperación. Configuration Manager puede recuperar la base de datos de sitio a partir de la tarea de mantenimiento de copia de seguridad de Configuration Manager o desde una copia de seguridad de la base de datos de sitio realizada mediante DPM u otro proceso. Si recupera la base de datos del sitio con un método ajeno a Configuration Manager, tendrá que ejecutar el programa de instalación y seleccionar esta opción para completar la recuperación de la base de datos del sitio. Si hay una jerarquía, los cambios realizados en la base de datos de sitio después de la última copia de seguridad de la base de datos de sitio se recuperan del sitio de administración central para un sitio primario, o de un sitio primario de referencia para un sitio de administración central. Si recupera la base de datos del sitio para un sitio primario independiente, perderá los cambios que se hayan realizado en el sitio desde la copia de seguridad más reciente.  

    > [!NOTE]  
    >  Si usa DPM para realizar la copia de seguridad de la base de datos del sitio, emplee los procedimientos de DPM para restaurar la base de datos del sitio en una ubicación determinada antes de continuar con el proceso de restauración en Configuration Manager. Para obtener más información acerca de DPM, consulte la [Data Protection Manager Documentation Library (Biblioteca de documentación de Data Protection Manager)](http://go.microsoft.com/fwlink/?LinkId=272772) en TechNet.  

-   **Omitir recuperación de base de datos**: use esta opción si no se produjo una pérdida de datos en el servidor de base de datos del sitio de Configuration Manager. Esta opción solo es válida si la base de datos del sitio no está en el mismo equipo que el servidor de sitio que está en proceso de recuperación.  

####  <a name="a-namebkmksqlretentiona-sql-server-change-tracking-retention-period"></a><a name="bkmk_SQLretention"></a> Período de retención de seguimiento de cambios de SQL Server  
 El seguimiento de cambios está habilitado para la base de datos del sitio en SQL Server. El seguimiento de cambios permite a Configuration Manager realizar consultas sobre los cambios que se realizaron en las tablas de base de datos a partir de un punto concreto en el tiempo. El período de retención especifica cuánto tiempo se conserva la información del seguimiento de cambios. De forma predeterminada, la base de datos del sitio está configurada para tener un período de retención de 5 días. Cuando se recupera una base de datos del sitio, el proceso de recuperación variará en función de si la copia de seguridad pertenece o no al período de retención. Por ejemplo, si se produce un error en el servidor de base de datos del sitio, y la última copia de seguridad se hizo hace 7 días, ésta no pertenecerá al período de retención.

 Para obtener más información sobre los datos internos de seguimiento de cambios de SQL Server, consulte los siguientes blogs del equipo de SQL Server: [Change Tracking Cleanup - part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1) (Limpieza de seguimiento de cambios - parte 1) y [Change Tracking Cleanup - part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2) (Limpieza de seguimiento de cambios - parte 2).



####  <a name="a-namebkmkreinita-process-to-reinitialize-site-or-global-data"></a><a name="bkmk_reinit"></a> Proceso para reinicializar datos globales o del sitio  
 El proceso para reinicializar datos globales o del sitio reemplaza los datos existentes de la base de datos del sitio por datos de otra base de datos del sitio. Por ejemplo, si el sitio ABC reinicializa datos desde el sitio XYZ, se producen los siguientes pasos:  

-   Los datos se copian desde el sitio XYZ al sitio ABC.  

-   Los datos existentes para el sitio XYZ se quitan de la base de datos del sitio en el sitio ABC.  

-   Los datos copiados desde el sitio XYZ se insertan en la base de datos del sitio para el sitio ABC.  

##### <a name="example-scenario-1"></a>Escenario de ejemplo 1  
 **El sitio primario reinicializa los datos globales desde el sitio de administración central**: el proceso de recuperación quita los datos globales existentes para el sitio primario en la base de datos del sitio primario y los reemplaza con los datos globales copiados desde el sitio de administración central.  

##### <a name="example-scenario-2"></a>Escenario de ejemplo 2  
 **El sitio de administración central reinicializa los datos del sitio desde un sitio primario**: el proceso de recuperación quita los datos de sitio existentes para ese sitio primario en la base de datos del sitio de administración central y los reemplaza con los datos de sitio copiados desde el sitio primario. No se ven afectados los datos del sitio para otros sitios primarios.  

####  <a name="a-namebkmksitedbrecoveryscenariosa-site-database-recovery-scenarios"></a><a name="BKMK_SiteDBRecoveryScenarios"></a> Escenarios de recuperación de base de datos de sitio  
 Una vez restaurada la base de datos del sitio desde una copia de seguridad, Configuration Manager intenta restaurar los cambios que tuvieron lugar en los datos globales y del sitio desde la última copia de seguridad de la base de datos. A continuación se indican las acciones que Configuration Manager inicia una vez que se restaura la base de datos del sitio desde una copia de seguridad.  

 **El sitio recuperado es un sitio de administración central:**  

-   **Copia de seguridad de base de datos dentro del período de retención del seguimiento de cambios**  

    -   **Datos globales** : los cambios en los datos globales posteriores a la copia de seguridad se replican desde todos los sitios principales.  

    -   **Datos del sitio** : los cambios en los datos del sitio posteriores a la copia de seguridad se replican desde todos los sitios principales.  

-   **Copia de seguridad de base de datos anterior al período de retención de seguimiento de cambios**  

    -   **Datos globales** : el sitio de administración central reinicializa los datos globales desde el sitio principal de referencia, si lo especifica. A continuación, el resto de sitios primarios reinicializan los datos globales desde el sitio de administración central. Si no se especifica ningún sitio de referencia, todos los sitios primarios reinicializan los datos globales desde el sitio de administración central (es decir, los datos que se restauraron a partir de la copia de seguridad).  

    -   **Datos del sitio** : el sitio de administración central reinicializa los datos del sitio desde cada sitio principal.  

 **El sitio recuperado es un sitio primario:**  

-   **Copia de seguridad de base de datos dentro del período de retención del seguimiento de cambios**  

    -   **Datos globales** : los cambios en los datos globales posteriores a la copia de seguridad se replican desde el sitio de administración central.  

    -   **Datos del sitio** : el sitio de administración central reinicializa los datos del sitio desde el sitio principal. Los cambios posteriores a la copia de seguridad se pierden, pero los clientes que envían información al sitio primario regeneran la mayor parte de ellos.  

-   **Copia de seguridad de base de datos anterior al período de retención de seguimiento de cambios**  

    -   **Datos globales** : el sitio primario reinicializa los datos globales desde el sitio de administración central.  

    -   **Datos del sitio** : el sitio de administración central reinicializa los datos del sitio desde el sitio principal. Los cambios posteriores a la copia de seguridad se pierden, pero los clientes que envían información al sitio primario regeneran la mayor parte de ellos.  

### <a name="site-recovery-procedures"></a>Procedimientos de recuperación de sitio  
 Utilice uno de los siguientes procedimientos para recuperar la base de datos del sitio y el servidor del sitio.  

##### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>Para iniciar una recuperación de sitio en el Asistente para instalación  

1.  Copie la carpeta CD.Latest en una ubicación fuera de la carpeta de instalación de Configuration Manager. (Vea [La carpeta CD.Latest para System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md))  

     Desde la copia de la carpeta CD.Latest, ejecute el Asistente para instalación de Configuration Manager.  

2.  En la página **Primeros pasos** , seleccione **Recuperar un sitio**y, a continuación, haga clic en **Siguiente**.  

3.  Complete el asistente con las opciones apropiadas para la recuperación de sitio que desea completar.  

    > [!IMPORTANT]  
    >  Durante la recuperación, el programa de instalación identifica el puerto de SQL Server Service Broker (SSB) que utiliza SQL Server. No cambie este puerto durante la recuperación; de lo contrario, la replicación de datos no funcionará correctamente una vez finalizada la recuperación.  

    > [!NOTE]  
    >  Puede especificar la ruta de acceso original o una nueva para la instalación de Configuration Manager en el Asistente para instalación.  

##### <a name="to-start-an-unattended-site-recovery"></a>Para iniciar una recuperación de sitio desatendida  

1.  Prepare el script de instalación desatendida para las opciones que necesita para la recuperación de sitio.  

2.  Ejecute el programa de instalación de Configuration Manager mediante la opción de comando **/script**. Por ejemplo, si designó el archivo de inicialización de instalación con el nombre ConfigMgrUnattend.ini y lo guardó en el directorio C:\Temp del equipo en el que ejecuta el programa de instalación, el comando sería: **Setup /script C:\temp\ConfigMgrUnattend.ini**  

> [!NOTE]  
>  Después de recuperar un sitio de administración central, la replicación de algunos datos de sitios secundarios no puede establecerse. Podrían incluirse el inventario de hardware, el inventario de software y los mensajes de estado.  
>   
>  Si esto ocurre, debe reinicializar la cola **ConfigMgrDRSSiteQueue** para la replicación de base de datos.  Para ello, use el **Administrador de SQL Server** para ejecutar la consulta siguiente en la base de datos de sitio de Configuration Manager en el sitio de administración central:  
>   
>  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**  
>   
>  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**  

###  <a name="a-namebkmkunattendedsiterecoverykeysa-unattended-site-recovery-script-file-keys"></a><a name="BKMK_UnattendedSiteRecoveryKeys"></a> Claves de archivo de script de recuperación de sitio desatendida  
 Para realizar una recuperación desatendida de un sitio primario o un sitio de administración central de Configuration Manager, puede crear un script de instalación desatendida y usar el programa de instalación con la opción de comando /script. El script proporciona el mismo tipo de información que solicita el Asistente para instalación, excepto por el hecho de que no existe configuración predeterminada. Deben especificarse todos los valores para las claves de instalación que se aplican al tipo de recuperación que se utiliza.  

 Puede ejecutar el programa de instalación de Configuration Manager en modo desatendido mediante un archivo de inicialización con la opción de línea de comandos de instalación /script. La instalación desatendida se admite para la recuperación de sitios primarios y sitios de administración central de Configuration Manager. Para utilizar la opción de línea de comandos de instalación de /script, debe crear un archivo de inicialización y especificar su nombre después de la opción de línea de comandos de instalación de /script. Más importante que el nombre del archivo es que éste tenga la extensión .ini. Cuando haga referencia al archivo de inicialización del programa de instalación desde la línea de comandos, tendrá que proporcionar la ruta de acceso completa al archivo. Por ejemplo, si el archivo de inicialización de instalación es setup.ini, y se almacena en la carpeta C:\setup, la línea de comandos sería:  

 **setup /script c:\setup\setup.ini**.  

> [!IMPORTANT]  
>  Debe tener derechos de administrador para ejecutar el programa de instalación. Cuando ejecute el programa de instalación con el script de instalación desatendida, inicie el símbolo del sistema en un contexto de administrador mediante **Ejecutar como administrador**.  

 El script contiene valores, nombres de clave y nombres de sección. Los nombres de clave de sección necesarios varían en función del tipo de recuperación para el que crea el script. No hay un orden determinado para las secciones ni para las claves de las secciones. Las claves no distinguen mayúsculas de minúsculas. Cuando proporciona valores para las claves, el nombre de la clave debe ir seguido por un signo de igual (=) y el valor de la clave.  

 Utilice las siguientes secciones como guía para crear un script para una recuperación de sitio desatendida. Las tablas enumeran las claves del script de instalación disponibles, sus valores correspondientes, si son necesarias o no, el tipo de instalación para el que se usan y una breve descripción de cada clave.  

#### <a name="recover-a-central-administration-site-unattended"></a>Recuperación de un sitio de administración central en modo desatendido  
 Utilice la información siguiente para configurar un archivo de script de instalación desatendida para recuperar un sitio de administración central.  

 **Identificación**  

-   **Nombre de clave** : Action  

    -   **Requerido** : sí  

    -   **Valores** : RecoverCCAR  

    -   **Detalles** : recupera un sitio de administración central  

**RecoveryOptions**  

-   **Nombre de clave** : ServerRecoveryOptions  

    -   **Requerido** : sí  

    -   **Valores** : 1, 2 o 4  

         1 = servidor de sitio de recuperación y SQL Server.  

         2 = recuperar sólo servidor de sitio.  

         4 = recuperar sólo SQL Server.  

    -   **Detalles** : especifica si el programa de instalación recuperará el servidor de sitio, SQL Server o ambos. Las claves asociadas son necesarias cuando se establece el siguiente valor para la configuración de ServerRecoveryOptions:  

        -   **Valor = 1** : tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

             se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se utiliza para restaurar la base de datos de sitio desde la copia de seguridad.  

        -   **Valor = 2** : tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

        -   **Value = 4** se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se utiliza para restaurar la base de datos de sitio desde la copia de seguridad.  

-   **Nombre de clave** : DatabaseRecoveryOptions  

    -   **Requerido** : quizás  

    -   **Valores:** 10, 20, 40, 80  

         10 = restaurar la base de datos de sitio desde la copia de seguridad.  

         20 = utilizar una base de datos de sitio que se recuperó manualmente mediante otro método.  

         40 = crear una base de datos nueva para el sitio. Utilice esta opción si no hay ninguna copia de seguridad de base de datos de sitio disponible. Los datos globales y de sitio se recuperan mediante la replicación desde otros sitios.  

         80 = omitir recuperación de base de datos.  

    -   **Detalles** : especifica cómo el programa de instalación recuperará la base de datos de sitio en SQL Server. Esta clave es necesaria cuando **ServerRecoveryOptions** tiene un valor de **1** o **4**.  

-   **Nombre de clave** : ReferenceSite  

    -   **Requerido** : quizás  

    -   **Valores:** &lt;ReferenceSiteFQDN\>  

    -   **Detalles** : especifica el sitio primario de referencia que usa el sitio de administración central para recuperar datos globales si la copia de seguridad de la base de datos es anterior al período de retención de seguimiento de cambios, o si se recupera el sitio sin usar una copia de seguridad.  

         Si no especifica ningún sitio de referencia y la copia de seguridad es anterior al período de retención de seguimiento de cambios, todos los sitios primarios se reinicializan con los datos restaurados desde el sitio de administración central.  

         Si no especifica ningún sitio de referencia y la copia de seguridad pertenece al período de retención de seguimiento de cambios, sólo se replicarán desde los sitios primarios los cambios que tuvieron lugar desde la copia de seguridad. Si existen cambios en conflicto de varios sitios primarios, el sitio de administración central utiliza el primero que recibe.  

         Esta clave es necesaria cuando **DatabaseRecoveryOptions** tiene un valor de **40**.  

-   **Nombre de clave** : SiteServerBackupLocation  

    -   **Requerido** : no  

    -   **Valores:** &lt;PathToSiteServerBackupSet\>  

    -   **Detalles** : especifica la ruta de acceso al conjunto de copia de seguridad del servidor de sitio. Esta clave es opcional si **ServerRecoveryOptions** tiene un valor de **1** o **2**. Especifique un valor para la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

-   **Nombre de clave** : BackupLocation  

    -   **Requerido** : quizás  

    -   **Valores:** &lt;PathToSiteDatabaseBackupSet\>  

    -   **Detalles** : especifica la ruta de acceso al conjunto de copia de seguridad de base de datos de sitio. La clave **BackupLocation** es necesaria cuando configura un valor de **1** o **4** para la clave **ServerRecoveryOptions** , y configura un valor de **10** para la clave **DatabaseRecoveryOptions** .  

**Opciones**  

-   **Nombre de clave** : ProductID  

    -   **Requerido** : sí  

    -   **Valores**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         Eval  

    -   **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones. Si escribe **Eval**, puede instalar la versión de evaluación de Configuration Manager.  

-   **Nombre de clave** : SiteCode  

    -   **Requerido** : sí  

    -   **Valores:** &lt;Código de sitio\>  

    -   **Detalles** : tres caracteres alfanuméricos que identifican de forma única el sitio en la jerarquía. Debe especificar el código del sitio que utilizó el sitio antes de que se produjera el error.  

-   **Nombre de clave** : SiteName  

    -   **Requerido** : sí  

    -   **Valores** : SiteName  

    -   **Detalles** : descripción de este sitio.  

-   **Nombre de clave** : SMSInstallDir  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*ConfigMgrInstallationPath*>  

    -   **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.  

        > [!NOTE]  
        >  Puede especificar la ruta de acceso original o una nueva para la instalación de Configuration Manager.  

-   **Nombre de clave** : SDKServer  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*FQDN del proveedor de SMS*>  

    -   **Detalles** : especifica el FQDN del servidor que hospedará el proveedor de SMS. Debe especificar el servidor que hospedaba el proveedor de SMS antes de producirse el error.  

         Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial.  

-   **Nombre de clave** : PrerequisiteComp  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = descargar  

         1 = ya se ha descargado  

    -   **Detalles** : especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si utiliza un valor de 0, el programa de instalación descargará los archivos.  

-   **Nombre de clave** : PrerequisitePath  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalles** : especifica la ruta de acceso a los archivos de requisitos previos de instalación. Dependiendo del valor **PrerequisiteComp** , el programa de instalación utiliza esta ruta para almacenar los archivos descargados o localizar los archivos descargados previamente.  

-   **Nombre de clave** : AdminConsole  

    -   **Requerido** : quizás  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si se va a instalar la consola de Configuration Manager. Esta clave es necesaria, salvo cuando **ServerRecoveryOptions** tiene un valor de **4**.  

-   **Nombre de clave** : JoinCEIP  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no unir  

         1 = unir  

    -   **Detalles** : especifica si se unirá al Programa para la mejora de la experiencia del usuario.  

**SQLConfigOptions**  

-   **Nombre de clave** : SQLServerName  

    -   **Requerido** : sí  

    -   **Valores:** *&lt;SQLServerName\>*  

    -   **Detalles**: nombre del servidor, o el nombre de instancia en clúster, que ejecuta SQL Server y donde se hospedará la base de datos del sitio. Debe especificar el mismo servidor que hospedaba la base de datos del sitio antes de producirse el error.  

-   **Nombre de clave** : DatabaseName  

    -   **Requerido** : sí  

    -   **Valores**  

         *&lt;SiteDatabaseName\>*  

         o  

         *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*  

    -   **Detalles**: especifica el nombre de la base de datos de SQL Server que se crea o se usa para instalar la base de datos del sitio de administración central. Debe especificar el mismo nombre de base de datos que se utilizó antes de producirse el error.  

        > [!IMPORTANT]  
        >  Debe especificar el nombre de instancia y el nombre de la base de datos del sitio si no utiliza la instancia predeterminada.  

-   **Nombre de clave** : SQLSSBPort  

    -   **Requerido** : no  

    -   **Valores:** &lt;*SSBPortNumber*>  

    -   **Detalles** : especifique el puerto de SQL Server Service Broker (SSB) usado por SQL Server. Normalmente, SSB está configurado para utilizar el puerto TCP 4022, pero se admiten otros puertos. Debe especificar el mismo puerto SSB que se utilizó antes de producirse el error.  

#### <a name="recover-a-primary-site-unattended"></a>Recuperación de un sitio primario desatendido  
 Utilice la información siguiente para configurar un archivo de script de instalación desatendida para recuperar un sitio de administración central.  

 **Identificación**  

-   **Nombre de clave** : Action  

    -   **Requerido** : sí  

    -   **Valores** : RecoverPrimarySite  

    -   **Detalles** : recupera un sitio primario.  

**RecoveryOptions**  

-   **Nombre de clave** : ServerRecoveryOptions  

    -   **Requerido** : sí  

    -   **Valores** : 1, 2 o 4  

         1 = servidor de sitio de recuperación y SQL Server.  

         2 = recuperar sólo servidor de sitio.  

         4 = recuperar sólo SQL Server.  

    -   **Detalles** : especifica si el programa de instalación recuperará el servidor de sitio, SQL Server o ambos. Las claves asociadas son necesarias cuando se establece el siguiente valor para la configuración de ServerRecoveryOptions:  

        -   **Valor = 1** : tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

             se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se utiliza para restaurar la base de datos de sitio desde la copia de seguridad.  

        -   **Valor = 2** : tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

        -   **Value = 4** se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se utiliza para restaurar la base de datos de sitio desde la copia de seguridad.  

-   **Nombre de clave** : DatabaseRecoveryOptions  

    -   **Requerido** : quizás  

    -   **Valores:** 10, 20, 40, 80  

         10 = restaurar la base de datos de sitio desde la copia de seguridad.  

         20 = utilizar una base de datos de sitio que se recuperó manualmente mediante otro método.  

         40 = crear una base de datos nueva para el sitio. Utilice esta opción si no hay ninguna copia de seguridad de base de datos de sitio disponible. Los datos globales y de sitio se recuperan mediante la replicación desde otros sitios.  

         80 = omitir recuperación de base de datos.  

    -   **Detalles** : especifica cómo el programa de instalación recuperará la base de datos de sitio en SQL Server. Esta clave es necesaria cuando **ServerRecoveryOptions** tiene un valor de **1** o **4**.  

-   **Nombre de clave** : SiteServerBackupLocation  

    -   **Requerido** : no  

    -   **Valores:** &lt;PathToSiteServerBackupSet\>  

    -   **Detalles** : especifica la ruta de acceso al conjunto de copia de seguridad del servidor de sitio. Esta clave es opcional si **ServerRecoveryOptions** tiene un valor de **1** o **2**. Especifique un valor para la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

-   **Nombre de clave** : BackupLocation  

    -   **Requerido** : quizás  

    -   **Valores:** &lt;PathToSiteDatabaseBackupSet\>  

    -   **Detalles** : especifica la ruta de acceso al conjunto de copia de seguridad de base de datos de sitio. La clave **BackupLocation** es necesaria cuando configura un valor de **1** o **4** para la clave **ServerRecoveryOptions** , y configura un valor de **10** para la clave **DatabaseRecoveryOptions** .  

**Opciones**  

-   **Nombre de clave** : ProductID  

    -   **Requerido** : sí  

    -   **Valores**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         Eval  

    -   **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones. Si escribe **Eval**, puede instalar la versión de evaluación de Configuration Manager.  

-   **Nombre de clave** : SiteCode  

    -   **Requerido** : sí  

    -   **Valores:** &lt;Código de sitio\>  

    -   **Detalles** : tres caracteres alfanuméricos que identifican de forma única el sitio en la jerarquía. Debe especificar el código del sitio que utilizó el sitio antes de que se produjera el error.  

-   **Nombre de clave** : SiteName  

    -   **Requerido** : sí  

    -   **Valores** : SiteName  

    -   **Detalles** : descripción de este sitio.  

-   **Nombre de clave** : SMSInstallDir  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*ConfigMgrInstallationPath*>  

    -   **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.  

        > [!NOTE]  
        >  Puede especificar la ruta de acceso original o una nueva para la instalación de Configuration Manager.  

-   **Nombre de clave** : SDKServer  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*FQDN del proveedor de SMS*>  

    -   **Detalles** : especifica el FQDN del servidor que hospedará el proveedor de SMS. Debe especificar el servidor que hospedaba el proveedor de SMS antes de producirse el error.  

         Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial.  

-   **Nombre de clave** : PrerequisiteComp  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = descargar  

         1 = ya se ha descargado  

    -   **Detalles** : especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si utiliza un valor de 0, el programa de instalación descargará los archivos.  

-   **Nombre de clave** : PrerequisitePath  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalles** : especifica la ruta de acceso a los archivos de requisitos previos de instalación. Dependiendo del valor **PrerequisiteComp** , el programa de instalación utiliza esta ruta para almacenar los archivos descargados o localizar los archivos descargados previamente.  

-   **Nombre de clave** : AdminConsole  

    -   **Requerido** : quizás  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si se va a instalar la consola de Configuration Manager. Esta clave es necesaria, salvo cuando **ServerRecoveryOptions** tiene un valor de **4**.  

-   **Nombre de clave** : JoinCEIP  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no unir  

         1 = unir  

    -   **Detalles** : especifica si se unirá al Programa para la mejora de la experiencia del usuario.  

**SQLConfigOptions**  

-   **Nombre de clave** : SQLServerName  

    -   **Requerido** : sí  

    -   **Valores:** *&lt;SQLServerName\>*  

    -   **Detalles**: nombre del servidor, o el nombre de instancia en clúster, que ejecuta SQL Server y donde se hospedará la base de datos del sitio. Debe especificar el mismo servidor que hospedaba la base de datos del sitio antes de producirse el error.  

-   **Nombre de clave** : DatabaseName  

    -   **Requerido** : sí  

    -   **Valores**  

         *&lt;SiteDatabaseName\>*  

         o  

         *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*  

    -   **Detalles**: especifica el nombre de la base de datos de SQL Server que se crea o se usa para instalar la base de datos del sitio de administración central. Debe especificar el mismo nombre de base de datos que se utilizó antes de producirse el error.  

        > [!IMPORTANT]  
        >  Debe especificar el nombre de instancia y el nombre de la base de datos del sitio si no utiliza la instancia predeterminada.  

-   **Nombre de clave** : SQLSSBPort  

    -   **Requerido** : no  

    -   **Valores:** &lt;*SSBPortNumber*>  

    -   **Detalles** : especifique el puerto de SQL Server Service Broker (SSB) usado por SQL Server. Normalmente, SSB está configurado para utilizar el puerto TCP 4022, pero se admiten otros puertos. Debe especificar el mismo puerto SSB que se utilizó antes de producirse el error.  

**Jerarquía ExpansionOption**  

-   **Nombre de clave** : CCARSiteServer  

    -   **Requerido** : quizás  

    -   **Valores:** &lt;*SiteCodeForCentralAdministrationSite*>  

    -   **Detalles:** especifica el sitio de administración central al que se asociará un sitio primario al unirse a la jerarquía de Configuration Manager. Esta configuración es necesaria si el sitio primario estaba asociado con un sitio de administración central antes de producirse el error. Debe especificar el código del sitio que utilizó el sitio de administración central antes de que se produjera el error.  

-   **Nombre de clave** : CASRetryInterval  

    -   **Requerido** : no  

    -   **Valores:** &lt;*Interval*>  

    -   **Detalles** : especifica el intervalo de reintento (en minutos) para tratar de establecer una conexión con el sitio de administración central después de que la conexión genera un error. Por ejemplo, si se produce un error en la conexión al sitio de administración central, el sitio primario espera el número de minutos especificado en CASRetryInterval y, a continuación, vuelve a intentar establecer la conexión.  

-   **Nombre de clave** : WaitForCASTimeout  

    -   **Requerido** : no  

    -   **Valores:** &lt;*Timeout*>  

    -   **Detalles** : especifica el valor de tiempo de espera máximo (en minutos) de un sitio primario para conectarse al sitio de administración central. Por ejemplo, si se produce un error de conexión del sitio primario con el sitio de administración central, el sitio primario vuelve a tratar de establecer la conexión conforme al valor especificado para CASRetryInterval hasta que se alcanza el valor de tiempo de WaitForCASTimeout. Puede especificar un valor entre 0 y 100.  

###  <a name="a-namebkmkpostrecoverya-post-recovery-tasks"></a><a name="BKMK_PostRecovery"></a> Tareas posteriores a la recuperación  
 Tras la recuperación del sitio, se pueden llevar a cabo varias tareas posteriores a la recuperación antes de que se complete totalmente la recuperación del sitio. Consulte las secciones siguientes para obtener información útil acerca de cómo completar el proceso de recuperación del sitio.  

#### <a name="re-enter-user-account-passwords"></a>Volver a escribir las contraseñas de cuentas de usuario  
 Tras la recuperación del servidor del sitio, es necesario volver a escribir las contraseñas de las cuentas de usuario especificadas para el sitio debido a que se restablecen durante el proceso de recuperación. Las cuentas se enumeran en la página **Finalizado** del Asistente para la instalación tras completarse la recuperación y se guardan en C:\ConfigMgrPostRecoveryActions.html en el servidor del sitio recuperado.  

###### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>Para volver a escribir las contraseñas de cuentas de usuario después de la recuperación del sitio  

1.  Abra la consola de Configuration Manager y conéctese con el sitio recuperado.  

2.  En la consola de Configuration Manager, haga clic en **Administración**.  

3.  En el área de trabajo **Administración** , expanda **Seguridad**y, a continuación, haga clic en **Cuentas**.  

4.  Para cada cuenta en la que deba volver a escribir la contraseña, haga lo siguiente:  

    1.  Seleccione la cuenta de la lista de cuentas que se identificaron después de la recuperación del sitio. Puede encontrar esta lista en C:\ConfigMgrPostRecoveryActions.html en el servidor del sitio recuperado.  

    2.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades** para abrir las propiedades de la cuenta.  

    3.  En la pestaña **General** , haga clic en **Establecer**y, a continuación, vuelva a escribir las contraseñas para la cuenta.  

    4.  Haga clic en **Comprobar**, seleccione el origen de datos apropiado para la cuenta de usuario seleccionada y, a continuación, haga clic en **Conexión de prueba** para comprobar que la cuenta de usuario se puede conectar al origen de datos.  

    5.  Haga clic en **Aceptar** para guardar los cambios de contraseña y, a continuación, haga clic en **Aceptar**.  

#### <a name="re-enter-sideloading-keys"></a>Volver a escribir las claves de instalación de prueba  
 Después de una recuperación del servidor de sitio, es preciso volver a escribir las claves de instalación de prueba de Windows especificadas para el sitio, ya que se restablecen durante la recuperación del sitio. Después de volver a escribir las claves de instalación de prueba, se restablece el contador de la columna **Activaciones usadas** de las claves de instalación de prueba de Windows en la consola de Configuration Manager. Por ejemplo, supongamos que antes del error del sitio, el valor del contador **Total de activaciones** era **100** y el de **Activaciones usadas** (el número de claves usadas por dispositivos) era **90**. Después de la recuperación del sitio, la columna **Total de activaciones** muestra **100**, pero la columna **Activaciones usadas** muestra, de forma incorrecta, **0**. Sin embargo, después de que 10 nuevos dispositivos utilicen una clave de instalación de prueba, no quedará ninguna clave de instalación de prueba y, por lo tanto, el siguiente dispositivo no podrá aplicar ninguna clave de instalación de prueba.  

#### <a name="recreate-the-microsoft-intune-subscription"></a>Volver a crear la suscripción a Microsoft Intune  
 Si recupera un servidor de sitio de Configuration Manager después de volver a crear la imagen del equipo del servidor de sitio, la suscripción de Microsoft Intune no se restaurará. Debe volver a conectar la suscripción después de recuperar el sitio.  No cree una nueva solicitud de APN. En su lugar, cargue el archivo .pem válido actual que se cargó la última vez que se configuró o se renovó la administración de iOS. Para más información, vea [Configuring the Microsoft Intune subscription (Configuración de la suscripción de Microsoft Intune)](../../mdm/deploy-use/setup-hybrid-mdm.md#step-3-configure-intune-subscription).  

#### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configuración de SSL para roles de sistema de sitio que usan IIS  
 Al recuperar sistemas de sitio que ejecutan IIS y que se habían configurado para HTTPS antes del error, debe volver a configurar IIS para utilizar el certificado de servidor web.  

#### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>Reinstalación de revisiones en el servidor del sitio recuperado  
 Tras una recuperación del sitio, debe reinstalar las revisiones que se han aplicado al servidor del sitio. Después de la recuperación, en la página **Finalizado** del Asistente para instalación se muestra una lista de las revisiones instaladas anteriormente y se guarda en **C:\ConfigMgrPostRecoveryActions.html** en el servidor de sitio recuperado.  

#### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>Recuperación de informes personalizados en el equipo en que se ejecuta Reporting Services  
 Si ha creado informes personalizados con Reporting Services y se produce algún error con Reporting Services, puede recuperar los informes si ha realizado una copia de seguridad del servidor de informes. Para obtener más información acerca de la restauración de los informes personalizados en Reporting Services, consulte [Operaciones de copias de seguridad y restauración para una instalación de Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=228724) en Libros en pantalla de SQL Server 2008.  

#### <a name="recover-content-files"></a>Recuperación de archivos de contenido  
 La base de datos del sitio contiene información acerca de dónde están almacenados los archivos de contenido en el servidor del sitio, pero no se realiza ninguna copia de seguridad ni restauración de estos archivos como parte del proceso de copia de seguridad y restauración. Para recuperar totalmente los archivos de contenido, debe restaurar la biblioteca de contenido y los archivos de origen del paquete en el servidor del sitio. Existen varios métodos para recuperar los archivos de contenido, pero el método más sencillo consiste en restaurar los archivos desde una copia de seguridad del sistema de archivos del servidor del sitio.  

 Si no dispone de una copia de seguridad del sistema de archivos de origen del paquete, debe copiarlos o descargarlos manualmente como lo hizo inicialmente la primera vez que creó el paquete. Puede ejecutar la siguiente consulta en SQL Server para buscar la ubicación del origen del paquete para todos los paquetes y aplicaciones: `SELECT * FROM v_Package`. Puede identificar el sitio del origen del paquete mediante los tres primeros caracteres del identificador del paquete. Por ejemplo, si el identificador del paquete es CEN00001, el código de sitio del sitio de origen es CEN. Cuando restaure los archivos de origen del paquete, se deben restaurar en la misma ubicación en la que se encontraban antes del error.  

 Si no tiene una copia de seguridad del sistema de archivos que contiene la biblioteca de contenido, tiene las siguientes opciones de restauración:  

-   **Importar un archivo de contenido preconfigurado**: si hay una jerarquía de Configuration Manager, puede crear un archivo de contenido preconfigurado con todos los paquetes y las aplicaciones de otra ubicación y luego importar el archivo de contenido preconfigurado para recuperar la biblioteca de contenido en el servidor de sitio.  

-   **Actualizar contenido**: cuando se inicia la acción de actualización de contenido para un tipo de implementación de paquete o aplicación, el contenido se copia desde el origen del paquete a la biblioteca de contenido. Los archivos de origen del paquete deben estar disponibles en la ubicación original para que esta acción se complete correctamente. Debe ejecutar esta acción en cada paquete y aplicación.  

#### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>Recuperación de actualizaciones de software personalizadas en el equipo que ejecuta Updates Publisher  
 Cuando se han incluido archivos de base de datos de Updates Publisher en el plan de copias de seguridad, es posible recuperar las bases de datos si se produce un error en el equipo en el que se ejecuta Updates Publisher. Para obtener más información acerca de Updates Publisher, consulte [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) en la biblioteca de TechCenter de System Center.  

 Use el siguiente procedimiento para restaurar la base de datos de Updates Publisher.  

###### <a name="to-restore-the-updates-publisher-2011-database"></a>Para restaurar la base de datos de Updates Publisher 2011  

1.  Vuelva a instalar Updates Publisher en el equipo recuperado.  

2.  Copie el archivo de base de datos (Scupdb.sdf) del destino de copia de seguridad en %*PERFILUSUARIO*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ en el equipo que ejecuta Updates Publisher.  

3.  Si más de un usuario ejecuta Updates Publisher en el equipo, debe copiar cada archivo de base de datos en la ubicación del perfil de usuario correspondiente.  

#### <a name="user-state-migration-data"></a>Datos de migración de estado de usuario  
 Como parte de las propiedades de sistema de sitio de punto de migración de estado, se especifican las carpetas que almacenan datos de migración de estado de usuario. Después de recuperar un servidor con una carpeta que almacena los datos de migración de estado de usuario, debe restaurar manualmente los datos de migración de estado de usuario del servidor en las mismas carpetas que almacenaban los datos antes del error.  

#### <a name="regenerate-the-certificates-for-distribution-points"></a>Regeneración de los certificados para puntos de distribución  
 Después de restaurar un sitio, el registro distmgr.log podría contener la siguiente entrada para uno o varios puntos de distribución: **Error al descifrar los datos de certificado PFX**. Esta entrada indica que el sitio no puede descifrar los datos del certificado de punto de distribución. Para resolver este problema debe regenerar o volver a importar el certificado para los puntos de distribución afectados. Se puede hacer con el cmdlet [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) de PowerShell.  

#### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Actualización de certificados que se utilizan para puntos de distribución basados en la nube  
 Configuration Manager exige un certificado de administración que usa para la comunicación entre servidores de sitio y puntos de distribución basados en la nube. Después de una recuperación de sitio, debe actualizar los certificados de los puntos de distribución basados en la nube.  

####  <a name="a-namebkmkrecoversecondarysitea-recover-a-secondary-site"></a><a name="BKMK_RecoverSecondarySite"></a> Recuperar un sitio secundario  
 Configuration Manager no admite la copia de seguridad de la base de datos en un sitio secundario, pero sí admite la recuperación mediante la reinstalación del sitio secundario. Se precisa la recuperación de sitio secundario si se produce un error en un sitio secundario de Configuration Manager. Puede recuperar un sitio secundario mediante la acción **Recuperar sitio secundario** del nodo **Sitios** de la consola de Configuration Manager. A diferencia de la recuperación de un sitio de administración central o de un sitio primario, en la recuperación de un sitio secundario no se usa un archivo de copia de seguridad, sino que se reinstalan los archivos de ese sitio secundario en el equipo con errores. A continuación, los datos del sitio secundario se reinicializan con los datos del sitio primario. Durante el proceso de recuperación, Configuration Manager verifica la existencia de la biblioteca de contenido en el equipo de sitio secundario y la disponibilidad del contenido correspondiente. El sitio secundario usará la biblioteca de contenido existente, si esta incluye el contenido adecuado. En caso contrario, para recuperar la biblioteca de contenido de un sitio secundario recuperado, es necesario redistribuir o preconfigurar el contenido en ese sitio recuperado. Si tiene un punto de distribución que no está en el sitio secundario, no es preciso que vuelva a instalar el punto de distribución durante la recuperación del sitio secundario. Después de la recuperación de sitio secundario, el sitio se sincroniza automáticamente con el punto de distribución.  

 Puede comprobar el estado de la recuperación del sitio secundario mediante la acción **Mostrar estado de instalación** del nodo **Sitios** de la consola de Configuration Manager.  

> [!IMPORTANT]  
>  Debe usar un equipo con la misma configuración que el equipo con errores, como su FQDN, para recuperar correctamente el sitio secundario. El equipo también debe cumplir todos los requisitos previos del sitio secundario y tener los derechos de seguridad correspondientes configurados. Además, use la misma ruta de instalación que se utilizó para el sitio con errores.  

> [!IMPORTANT]  
>  Durante la recuperación de sitio secundario, Configuration Manager no instala SQL Server Express si no está instalado en el equipo. Por lo tanto, antes de recuperar un sitio secundario, debe instalar manualmente SQL Server Express o SQL Server. Debe utilizar la misma versión de SQL Server y la misma instancia de SQL Server que se utilizaron para la base de datos del sitio secundario antes del error.  

##  <a name="a-namebkmksmswriterservicea-sms-writer-service"></a><a name="BKMK_SMSWriterService"></a> Servicio SMS Writer  
 SMS Writer es un servicio que interactúa con el Servicio de instantáneas de volumen (VSS) durante el proceso de copia de seguridad. Debe ejecutar el servicio SMS Writer para que la copia de seguridad del sitio de Configuration Manager se complete correctamente.  

### <a name="purpose"></a>Finalidad  
 SMS Writer se registra con el servicio VSS y se enlaza a sus interfaces y eventos. Cuando VSS difunde eventos o envía notificaciones específicas a SMS Writer, SMS Writer responde a la notificación y toma las medidas oportunas. El servicio SMS Writer lee el archivo de control de copia de seguridad (smsbkup.ctl), ubicado en &lt;*rutaInstalaciónConfigMgr*>\inboxes\smsbkup.box, y determina los archivos y datos cuya copia de seguridad se va a realizar. El servicio SMS Writer genera metadatos, que constan de varios componentes, basados en esta información, así como datos específicos de la clave del Registro SMS y las subclaves. Envía los metadatos a VSS cuando se solicita. Luego, VSS envía los metadatos a la aplicación solicitante, el Administrador de copias de seguridad de Configuration Manager. El Administrador de copias de seguridad selecciona los datos de los que se van a hacer copia de seguridad y los envía al servicio SMS Writer mediante VSS. El servicio SMS Writer realiza los pasos apropiados para prepararse para la copia de seguridad. Después, cuando VSS está listo para tomar la instantánea, envía un evento, SMS Writer detiene todos los servicios de Configuration Manager y se asegura de que las actividades de Configuration Manager se congelen mientras se crea la instantánea. Una vez completada la instantánea, SMS Writer reinicia los servicios y las actividades.  

 El servicio SMS Writer se instala automáticamente. Debe ejecutarse cuando la aplicación VSS solicite una copia de seguridad o restauración.  

### <a name="writer-id"></a>Identificador de escritor  
 El identificador de escritor de SMS Writer es: 03ba67dd-dc6d-4729-a038-251f7018463b.  

### <a name="permissions"></a>Permisos  
 El servicio SMS Writer debe ejecutarse bajo la cuenta Sistema local.  

### <a name="volume-shadow-copy-service"></a>Servicio de instantáneas de volumen  
 El servicio VSS es un conjunto de API de COM que implementan un marco para permitir la realización de copias de seguridad de volumen mientras se siguen escribiendo aplicaciones de un sistema en los volúmenes. El servicio VSS proporciona una interfaz coherente que permite la coordinación entre aplicaciones de usuario que actualizan datos en el disco (el servicio SMS Writer) y otras que realizan copias de seguridad de aplicaciones (el servicio Administrador de actualizaciones). Para obtener más información acerca de VSS, consulte el tema [Volume Shadow Copy Service (Servicio de instantáneas de volumen)](http://go.microsoft.com/fwlink/p/?LinkId=241968) en el TechCenter de Windows Server.  



<!--HONumber=Feb17_HO2-->


