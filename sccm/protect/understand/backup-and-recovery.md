---
title: Sitios de copia de seguridad
titleSuffix: Configuration Manager
description: "Aprenda a realizar copias de seguridad de los sitios ante la posibilidad de un error o pérdida de datos en System Center Configuration Manager."
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: "22"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 7dae5ada647146713b884b09d0eda1c7ec6531ef
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="back-up-a-configuration-manager-site"></a>Hacer una copia de seguridad de un sitio de Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Prepare enfoques de copia de seguridad y recuperación para evitar la pérdida de datos. En los sitios de Configuration Manager, un enfoque de copia de seguridad y recuperación puede ayudar a recuperar sitios y jerarquías más rápidamente y con la mínima pérdida de datos.  

Las secciones de este tema pueden ayudarle a realizar copias de seguridad de los sitios. Para recuperar un sitio, consulte [Recovery for Configuration Manager](/sccm/protect/understand/recover-sites) (Recuperación para Configuration Manager).  

## <a name="considerations-before-creating-a-backup"></a>Aspectos que debe tener en cuenta antes de crear una copia de seguridad  
-   **Si utiliza un grupo de disponibilidad AlwaysOn de SQL Server para hospedar la base de datos de sitio:** modifique los planes de recuperación y copia de seguridad, como se describe en [Prepararse para usar SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-backup).

-   Configuration Manager puede recuperar la base de datos de sitio a partir de la tarea de mantenimiento de copia de seguridad de Configuration Manager o desde una copia de seguridad de la base de datos de sitio que creara con otro proceso.   

    Por ejemplo, puede restaurar la base de datos de sitio desde una copia de seguridad creada como parte de un plan de mantenimiento de Microsoft SQL Server. También puede utilizar una copia de seguridad creada con Data Protection Manager (DPM) para hacer una copia de seguridad de la base de datos de sitio.

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Uso de Data Protection Manager para realizar copias de seguridad de la base de datos del sitio
Puede usar System Center 2012 Data Protection Manager (DPM) para hacer una copia de seguridad de la base de datos del sitio.

Debe crear un nuevo grupo de protección en DPM para el equipo de la base de datos del sitio. En la página **Seleccionar miembros del grupo** del asistente Crear nuevo grupo de protección, seleccione el servicio SMS Writer de la lista de orígenes de datos y, a continuación, seleccione la base de datos del sitio como un miembro apropiado. Para obtener más información acerca del uso de DPM para realizar una copia de seguridad de la base de datos del sitio, consulte la [Data Protection Manager Documentation Library (Biblioteca de documentación de Data Protection Manager)](http://go.microsoft.com/fwlink/?LinkId=272772) en TechNet.  

> [!IMPORTANT]  
>  Configuration Manager no admite la copia de seguridad de DPM en un clúster de SQL Server que use una instancia con nombre, pero admite la copia de seguridad de DPM en un clúster de SQL Server que use la instancia predeterminada de SQL Server.  

 Después de restaurar la base de datos del sitio, siga los pasos descritos en el programa de instalación para recuperar el sitio. Seleccione la opción de recuperación **Usar una base de datos del sitio que se ha recuperado manualmente** para usar la base de datos de sitio que recuperó con Data Protection Manager.  

## <a name="backup-maintenance-task"></a>Tarea de mantenimiento de copia de seguridad
Puede automatizar la copia de seguridad de sitios de Configuration Manager mediante la programación de la tarea de mantenimiento predefinida Copia de seguridad del servidor del sitio. Esta tarea:

-   Se ejecuta según una programación
-   Realiza copias de seguridad de la base de datos del sitio
-   Realiza copias de seguridad de claves de registro específicas
-   Realiza copias de seguridad de carpetas y archivos específicos
-   Realiza copias de seguridad de la carpeta [CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder)   

Planee la ejecución de la tarea de copia de seguridad del sitio predeterminada cada cinco días como mínimo. Esto se debe a que Configuration Manager usa un *período de retención del seguimiento de cambios de SQL Server* de cinco días.  (Consulte [SQL Server change tracking retention period](/sccm/protect/understand/recover-sites#bkmk_SQLretention) [Período de retención de seguimiento de cambios de SQL Server] en el tema Recuperar sitios).

Para simplificar el proceso de copia de seguridad, puede crear un archivo **AfterBackup.bat** para realizar automáticamente acciones posteriores a la copia de seguridad después de que la tarea de mantenimiento de copia de seguridad se ejecute correctamente. El archivo AfterBackup.bat se suele usar para archivar la instantánea de copia de seguridad en una ubicación segura. También puede usar el archivo AfterBackup.bat para copiar archivos en la carpeta de copia de seguridad e iniciar otras tareas de copia de seguridad adicionales.  

Puede hacer una copia de seguridad de un sitio de administración central y un sitio primario, pero no existe compatibilidad con la copia de seguridad de servidores de sistema de sitio o sitios secundarios.

Cuando se ejecuta el servicio de copia de seguridad de Configuration Manager, este sigue las instrucciones definidas en el archivo de control de copia de seguridad (**&lt;carpetaInstalaciónConfigMgr\>\Inboxes\Smsbkup.box\Smsbkup.ctl**). Puede modificar el archivo de control de copia de seguridad para cambiar el comportamiento del servicio de copia de seguridad.  

La información del estado de copia de seguridad del sitio se escribe en el archivo **Smsbkup.log** . Este archivo se crea en la carpeta de destino que especifique en las propiedades de la tarea de mantenimiento Copia de seguridad del servidor del sitio.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>Para habilitar la tarea de mantenimiento de copia de seguridad de sitio  

1.  En la consola de Configuration Manager, abra **Administración** > **Configuración del sitio** > **Sitios**.  

2.  Seleccione el sitio en el que desee habilitar la tarea de mantenimiento de copia de seguridad de sitio.  

3.  En la pestaña **Inicio**, en el grupo **Configuración**, elija **Tareas de mantenimiento del sitio**.  

4.  Elija **Copia de seguridad del servidor del sitio**  >  **Editar**.  

5.  Elija **Habilitar esta tarea** > **Rutas de acceso** para especificar el destino de la copia de seguridad. Dispone de las siguientes opciones:  

    > [!IMPORTANT]  
    >  Con el fin de evitar la manipulación de los archivos de copia de seguridad, almacene los archivos en una ubicación segura. La ruta de acceso de copia de seguridad más segura es una unidad local, por lo que puede establecer los permisos del sistema de archivos NTFS en la carpeta. Configuration Manager no cifra los datos de copia de seguridad que se almacenan en la ruta de acceso de copia de seguridad.  

    -   **Unidad local en servidor de sitio para los datos y la base de datos del sitio**: especifica que los archivos de copia de seguridad del sitio y de la base de datos del sitio se almacenen en la ruta de acceso especificada en la unidad de disco local del servidor de sitio. Debe crear la carpeta local antes de que se ejecute la tarea de copia de seguridad. La cuenta Sistema local en el servidor de sitio debe tener permisos del sistema de archivos NTFS de **escritura** en la carpeta local para la copia de seguridad del servidor de sitio. La cuenta Sistema local en el equipo que ejecute SQL Server debe tener permisos de NTFS de **escritura** en la carpeta local para la copia de seguridad de la base de datos del sitio.  

    -   **Ruta de acceso de red (nombre UNC) para los datos y la base de datos del sitio**: especifica que los archivos de copia de seguridad del sitio y de la base de datos del sitio se almacenan en la ruta de acceso UNC especificada. Debe crear el recurso compartido antes de que se ejecute la tarea de copia de seguridad. La cuenta de equipo en el servidor de sitio y la cuenta de equipo en el servidor SQL Server, si SQL Server está instalado en otro equipo, deben tener permisos de recurso compartido y NTFS de **escritura** en la carpeta de red compartida.  

    -   **Unidades locales en el servidor de sitio y SQL Server**: especifica que los archivos de copia de seguridad del sitio se almacenan en la ruta de acceso especificada de la unidad local del servidor de sitio y que los archivos de copia de seguridad de la base de datos del sitio se almacenan en la ruta de acceso especificada de la unidad local del servidor de base de datos del sitio. Debe crear las carpetas locales antes de que se ejecute la tarea de copia de seguridad. La cuenta de equipo del servidor de sitio debe tener permisos de NTFS de **escritura** en la carpeta que se crea en el servidor de sitio. La cuenta de equipo del servidor de SQL Server debe tener permisos de NTFS de **escritura** en la carpeta que se crea en el servidor de la base de datos del sitio. Esta opción solo está disponible cuando la base de datos del sitio no esté instalada en el servidor de sitio.  

    > [!NOTE]  
    >   La opción de examinar el destino de la copia de seguridad solo está disponible cuando se especifica la ruta de acceso UNC del destino de la copia de seguridad.

    > El nombre de la carpeta o el nombre del recurso compartido que se utilizan para el destino de la copia de seguridad no pueden usar caracteres Unicode.  

6.  Configure una programación para la tarea de copia de seguridad del sitio. Como práctica recomendada, considere la posibilidad de programar la copia de seguridad fuera del horario de trabajo activo. Si tiene una jerarquía, considere la posibilidad de una programación que se ejecute al menos dos veces por semana para asegurar la máxima retención de datos en caso de error en el sitio.  

    Cuando ejecute la consola de Configuration Manager en el mismo servidor de sitio que esté configurando para la copia de seguridad, la tarea de mantenimiento Copia de seguridad del servidor del sitio usará la hora local para la programación. Cuando la consola de Configuration Manager se ejecute desde un equipo remoto con respecto al sitio que esté configurando para la copia de seguridad, la tarea de mantenimiento Copia de seguridad del servidor del sitio usará UTC para la programación.  

7.  Elija si quiere crear una alerta en caso de error de la tarea de copia de seguridad del sitio, haga clic en **Aceptar** y luego en **Aceptar**. Cuando se selecciona, Configuration Manager crea una alerta crítica para el error de copia de seguridad que puede revisar en el nodo **Alertas** del área de trabajo **Supervisión**.  

 Luego, compruebe que se está ejecutando la tarea de mantenimiento Copia de seguridad del servidor del sitio para asegurarse de que se están creando copias de seguridad.  

#### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>Para comprobar que la tarea de mantenimiento Copia de seguridad del servidor del sitio se está ejecutando  
Compruebe que la tarea de mantenimiento Copia de seguridad del servidor del sitio se está ejecutando revisando cualquiera de los siguientes:  

-   Compruebe la marca de tiempo en los archivos de la carpeta de destino de la copia de seguridad que creó la tarea. Compruebe que la marca de tiempo se ha actualizado con una hora que coincida con la hora programada para la ejecución más reciente de la tarea.  

-   En el nodo **Estado del componente** del área de trabajo **Supervisión** , revise los mensajes de estado para SMS_SITE_BACKUP. Cuando la copia de seguridad del sitio se complete correctamente, verá el identificador de mensaje 5035, que indica que la copia de seguridad del sitio se completó sin errores.  

-   Cuando la tarea de mantenimiento Copia de seguridad del servidor del sitio se configure para crear una alerta si se produce un error en la copia de seguridad, puede comprobar el nodo **Alertas** del área de trabajo **Supervisión** en busca de errores.  

-   En &lt;*carpetaInstalaciónConfigMgr*>\Logs, revise el archivo Smsbkup.log en busca de errores y advertencias. Cuando la copia de seguridad del sitio se complete correctamente, verá `Backup completed` con una marca de tiempo y un identificador de mensaje `STATMSG: ID=5035`.  

    > [!TIP]  
    >  Cuando se produce un error en la tarea de mantenimiento de copia de seguridad, reinicie la tarea de copia de seguridad. Para ello, detenga y reinicie el servicio SMS_SITE_BACKUP.  

## <a name="archive-the-backup-snapshot"></a>Archivo de la instantánea de copia de seguridad  
La primera vez que se ejecuta la tarea de mantenimiento Copia de seguridad del servidor del sitio, se crea una instantánea de la copia de seguridad, que puede utilizar para recuperar el servidor de sitio en caso de error. Cuando la tarea de copia de seguridad se ejecuta de nuevo durante ciclos posteriores, se crea una nueva instantánea de la copia de seguridad que sobrescribe la instantánea anterior. Como resultado, el sitio solo tiene una instantánea de copia de seguridad y no hay forma de recuperar la instantánea de una copia de seguridad anterior.  

Se recomienda conservar varios archivos de la instantánea de copia de seguridad por los siguientes motivos:  

-   Es común que los medios de copia de seguridad presenten errores, estén en una ubicación incorrecta o contengan solo una copia de seguridad parcial. La recuperación de un sitio primario independiente con errores desde una copia de seguridad antigua es mejor que una recuperación sin ninguna copia de seguridad. En el caso de un servidor de sitio de una jerarquía, la copia de seguridad debe estar en el período de retención de seguimiento de cambios de SQL Server, o no es necesaria.  

-   La existencia de daños en el sitio puede pasar desapercibida durante varios ciclos de copia de seguridad. Es posible que tenga que usar una instantánea de copia de seguridad anterior al momento en que el sitio resultó dañado. Esto se aplica a un sitio primario independiente y a los sitios de una jerarquía donde la copia de seguridad está en el período de retención de seguimiento de cambios de SQL Server.  

-   El sitio podría no tener ninguna instantánea de copia de seguridad si, por ejemplo, se produce un error en la tarea de mantenimiento Copia de seguridad del servidor del sitio. Dado que la tarea de copia de seguridad elimina la instantánea de copia de seguridad anterior antes de empezar a realizar la copia de seguridad de los datos actuales, no habrá una instantánea de copia de seguridad válida.  

## <a name="using-the-afterbackupbat-file"></a>Uso del archivo AfterBackup.bat  
Después de realizar la copia de seguridad del sitio correctamente, la tarea Copia de seguridad del servidor del sitio automáticamente intenta ejecutar un archivo llamado AfterBackup.bat. Debe crear manualmente el archivo AfterBackup.bat en &lt;*carpetaInstalaciónConfigMgr*>\Inboxes\Smsbkup. Si hay un archivo AfterBackup.bat y está almacenado en la carpeta correcta, se ejecuta automáticamente después de completarse la tarea de copia de seguridad.

El archivo AfterBackup.bat permite archivar la instantánea de copia de seguridad al final de cada operación de copia de seguridad y realizar automáticamente otras tareas posteriores a la copia de seguridad que no forman parte de la tarea de mantenimiento Copia de seguridad del servidor del sitio. El archivo AfterBackup.bat integra las operaciones de archivo y copia de seguridad, por lo que garantiza que se archiva cada nueva instantánea de copia de seguridad.

Si el archivo AfterBackup.bat no está presente, la tarea de copia de seguridad lo omite sin que se vea afectada la operación de copia de seguridad. Para comprobar que la tarea de copia de seguridad del sitio ejecutó correctamente el archivo AfterBackup.bat, consulte el nodo **Estado del componente** del área de trabajo **Supervisión** y revise los mensajes de estado de SMS_SITE_BACKUP. Si la tarea inició correctamente el archivo de comandos AfterBackup.bat, verá el mensaje ID 5040.  

> [!TIP]  
>  Para crear el archivo AfterBackup.bat para archivar los archivos de copia de seguridad del servidor de sitio, debe usar una herramienta de comando de copia, como [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408), en el archivo por lotes. Por ejemplo, podría crear el archivo AfterBackup.bat y, en la primera línea, podría agregar algo similar a lo siguiente: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

 Aunque el uso previsto de AfterBackup.bat es archivar las instantáneas de copia de seguridad, puede crear un archivo AfterBackup.bat para realizar tareas adicionales al final de cada operación de copia de seguridad.  

##  <a name="supplemental-backup-tasks"></a>Tareas de copia de seguridad adicionales  
La tarea de mantenimiento Copia de seguridad del servidor del sitio facilita una instantánea de copia de seguridad para los archivos de servidor de sitio y la base de datos de sitio, pero hay otros elementos cuya copia de seguridad no se realiza y que debe tener en cuenta cuando crea la estrategia de copia de seguridad. Use las secciones siguientes como ayuda para completar la estrategia de copia de seguridad de Configuration Manager.  

### <a name="back-up-custom-reporting-services-reports"></a>Copia de seguridad de informes personalizados de Reporting Services  
Si modifica informes personalizados creados o predefinidos de Reporting Services, la creación de una copia de seguridad de los archivos de base de datos del servidor de informes es una parte importante de la estrategia de copia de seguridad. La copia de seguridad del servidor de informes debe incluir una copia de seguridad de los archivos de origen de informes y modelos, claves de cifrado, extensiones o ensamblados personalizados, archivos de configuración, vistas personalizadas de SQL Server utilizadas en informes personalizados, procedimientos almacenados personalizados, etc.  

> [!IMPORTANT]  
>  Cuando Configuration Manager se actualiza a una versión más reciente, los nuevos informes podrían sobrescribir los informes predefinidos. Si modifica un informe predefinido, realice una copia de seguridad y luego restáurela en Reporting Services.  

 Para más información acerca de la copia de seguridad de los informes personalizados en Reporting Services, consulte [Operaciones de copias de seguridad y restauración para una instalación de Reporting Services](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) en Libros en pantalla de SQL Server 2014.  

### <a name="back-up-content-files"></a>Copia de seguridad de archivos de contenido  
La biblioteca de contenido de Configuration Manager es la ubicación donde se almacenan todos los archivos de contenido de actualizaciones de software, aplicaciones, implementación de sistema operativo, etc. La biblioteca de contenido se encuentra en el servidor de sitio y en cada punto de distribución. La tarea de mantenimiento Copia de seguridad del servidor del sitio no incluye una copia de seguridad de la biblioteca de contenido o los archivos de origen del paquete. Cuando se produce un error en el servidor de sitio, la información acerca de los archivos de la biblioteca de contenido se restaura en la base de datos de sitio, pero usted debe restaurar la biblioteca de contenido y los archivos de origen del paquete en el servidor de sitio.  

-   **Biblioteca de contenido**: se debe restaurar esta biblioteca para poder redistribuir el contenido a los puntos de distribución. Cuando inicia la redistribución de contenido, Configuration Manager copia los archivos de la biblioteca de contenido del servidor de sitio en los puntos de distribución. La biblioteca de contenido del servidor de sitio se encuentra en la carpeta SCCMContentLib, que suele ubicarse en la unidad con más espacio libre en disco en el momento en que se instaló el sitio.  

-   **Archivos de origen del paquete**: es necesario restaurar estos archivos para poder actualizar el contenido de los puntos de distribución. Cuando inicia una actualización de contenido, Configuration Manager copia los archivos nuevos o modificados del origen del paquete en la biblioteca de contenido, que a su vez copia los archivos en los puntos de distribución asociados. Puede ejecutar la siguiente consulta en SQL Server para buscar la ubicación del origen del paquete para todos los paquetes y aplicaciones: `SELECT * FROM v_Package`. Puede identificar el sitio del origen del paquete mediante los tres primeros caracteres del identificador del paquete. Por ejemplo, si el identificador del paquete es CEN00001, el código de sitio del sitio de origen es CEN. Cuando restaure los archivos de origen del paquete, debe hacerlo en la misma ubicación en la que se encontraban antes del error.  

 Compruebe que incluye las ubicaciones de la biblioteca de contenido y del origen del paquete en la copia de seguridad del sistema de archivos del servidor de sitio.  

### <a name="back-up-custom-software-updates"></a>Copia de seguridad de actualizaciones de software personalizadas  
 System Center Updates Publisher 2011 es una herramienta independiente que le permite publicar actualizaciones de software personalizadas en Windows Server Update Services (WSUS), sincronizar las actualizaciones de software con Configuration Manager, evaluar el cumplimiento de las actualizaciones de software e implementar las actualizaciones de software personalizadas en los clientes. Updates Publisher usa una base de datos local para el repositorio de actualizaciones de software. Si usa Updates Publisher para administrar las actualizaciones de software personalizadas, determine si tiene que incluir la base de datos de Updates Publisher en el plan de copias de seguridad. Para obtener más información acerca de Updates Publisher, consulte [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) en la biblioteca de TechCenter de System Center.  

 Use el siguiente procedimiento para realizar una copia de seguridad de la base de datos de Updates Publisher.  

#### <a name="to-back-up-the-updates-publisher-2011-database"></a>Para realizar una copia de seguridad de la base de datos de Updates Publisher 2011  

1.  En el equipo que ejecuta Updates Publisher, busque el archivo de base de datos de Updates Publisher (Scupdb.sdf) en %*PERFILUSUARIO*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\. Hay un archivo de base de datos diferente para cada usuario que ejecuta Updates Publisher.  

2.  Copie el archivo de base de datos en el destino de la copia de seguridad. Por ejemplo, si el destino de la copia de seguridad es E:\ConfigMgr_Backup, podría copiar el archivo de base de datos de Updates Publisher en E:\ConfigMgr_Backup\SCUP2011.  

    > [!TIP]  
    >  Si hay más de un archivo de base de datos en un equipo, puede almacenar el archivo en una subcarpeta que indique el perfil de usuario asociado al archivo de base de datos. Por ejemplo, podría tener un archivo de base de datos en E:\ConfigMgr_Backup\SCUP2011\Usuario1 y otro archivo de base de datos en E:\ConfigMgr_Backup\SCUP2011\Usuario2.  

## <a name="user-state-migration-data"></a>Datos de migración de estado de usuario  
Puede usar secuencias de tareas de Configuration Manager para capturar y restaurar los datos de estado de usuario en los escenarios de implementación de sistema operativo donde quiere conservar el estado de usuario del sistema operativo actual. Las carpetas donde se almacenan los datos de estado de usuario se enumeran en las propiedades del punto de migración de estado. La tarea de mantenimiento Copia de seguridad del servidor del sitio no incluye la copia de seguridad de los datos de migración de estado de usuario. Como parte del plan de copias de seguridad, debe realizar manualmente la copia de seguridad de las carpetas que especifique para almacenar los datos de migración de estado de usuario.   

### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>Para determinar las carpetas utilizadas para almacenar los datos de migración de estado de usuario  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración**, expanda **Configuración del sitio** y elija **Servidores y roles del sistema de sitios**.  

3.  Seleccione el sistema de sitio que hospeda el rol de migración de estado y luego elija **Punto de migración de estado** en **Roles del sistema de sitio**.  


4.  En la pestaña **Rol del sitio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  
5.  Las carpetas donde se almacenan los datos de migración de estado de usuario se enumeran en la sección **Detalles de la carpeta** de la pestaña **General**.  



## <a name="about-the-sms-writer-service"></a>Acerca del servicio SMS Writer  
SMS Writer es un servicio que interactúa con el Servicio de instantáneas de volumen (VSS) durante el proceso de copia de seguridad. Debe ejecutar el servicio SMS Writer para que la copia de seguridad del sitio de Configuration Manager se complete correctamente.  

### <a name="purpose"></a>Finalidad  
SMS Writer se registra con el servicio VSS y se enlaza a sus interfaces y eventos. Cuando VSS difunde eventos o envía notificaciones específicas a SMS Writer, SMS Writer responde a la notificación y toma las medidas oportunas. El servicio SMS Writer lee el archivo de control de copia de seguridad (smsbkup.ctl), ubicado en &lt;*rutaInstalaciónConfigMgr*>\inboxes\smsbkup.box, y determina los archivos y datos cuya copia de seguridad se va a realizar. El servicio SMS Writer genera metadatos, que constan de varios componentes, basados en esta información, así como datos específicos de la clave del Registro SMS y las subclaves. Envía los metadatos a VSS cuando se solicita. Luego, VSS envía los metadatos a la aplicación solicitante, el Administrador de copias de seguridad de Configuration Manager. El Administrador de copias de seguridad selecciona los datos de los que se van a hacer copia de seguridad y los envía al servicio SMS Writer mediante VSS. El servicio SMS Writer realiza los pasos apropiados para prepararse para la copia de seguridad. Después, cuando VSS está listo para tomar la instantánea, envía un evento, SMS Writer detiene todos los servicios de Configuration Manager y se asegura de que las actividades de Configuration Manager se congelen mientras se crea la instantánea. Una vez completada la instantánea, SMS Writer reinicia los servicios y las actividades.  

El servicio SMS Writer se instala automáticamente. Debe ejecutarse cuando la aplicación VSS solicite una copia de seguridad o restauración.  

### <a name="writer-id"></a>Identificador de escritor  
El identificador de escritor de SMS Writer es: 03ba67dd-dc6d-4729-a038-251f7018463b.  

### <a name="permissions"></a>Permisos  
El servicio SMS Writer debe ejecutarse bajo la cuenta Sistema local.  

### <a name="volume-shadow-copy-service"></a>Servicio de instantáneas de volumen  
El servicio VSS es un conjunto de API de COM que implementan un marco para permitir la realización de copias de seguridad de volumen mientras se siguen escribiendo aplicaciones de un sistema en los volúmenes. El servicio VSS proporciona una interfaz coherente que permite la coordinación entre aplicaciones de usuario que actualizan datos en el disco (el servicio SMS Writer) y otras que realizan copias de seguridad de aplicaciones (el servicio Administrador de actualizaciones). Para obtener más información, consulte el tema [Volume Shadow Copy Service](http://go.microsoft.com/fwlink/p/?LinkId=241968) (Servicio de copia de instantáneas de volumen) en el TechCenter de Windows Server.  

## <a name="next-steps"></a>Pasos siguientes
Después de crear una copia de seguridad, practique la [recuperación del sitio](/sccm/protect/understand/recover-sites) con esa copia de seguridad. Esto puede ayudarle a familiarizarse con el proceso de recuperación antes de que deba utilizarlo y confirmar que la copia de seguridad se completó correctamente para su finalidad prevista.  
