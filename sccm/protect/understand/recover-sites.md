---
title: "Recuperación del sitio"
titleSuffix: Configuration Manager
description: Aprenda a recuperar sus sitios en System Center Configuration Manager.
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 74d01e151efa19f91104ad99f393f7e7b1a23836
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2017
---
#  <a name="recover-a-configuration-manager-site"></a>Recuperar un sitio de Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Ejecute una recuperación de sitio de Configuration Manager después de que se produzca un error en un sitio de Configuration Manager o se pierdan datos de la base de datos de sitio. Reparar y volver a sincronizar datos son las tareas principales de una recuperación de sitio y son necesarias para evitar la interrupción de las operaciones.

Las secciones de este tema pueden ayudarle a recuperar un sitio de Configuration Manager. Para crear una copia de seguridad, consulte [Copia de seguridad y recuperación](/sccm/protect/understand/backup-and-recovery).

## <a name="considerations-before-recovering-a-site"></a>Consideraciones antes de recuperar un sitio
> [!Important]  
> Esta información se aplica únicamente a escenarios de recuperación del sitio.  Cuando está actualizando su infraestructura local y no recuperando activamente un sitio erróneo, revise la información de los temas siguientes:
> - [Actualizar la infraestructura local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure)
> - [Modificar la infraestructura](/sccm/core/servers/manage/modify-your-infrastructure)


**Debe usar la misma versión y edición de SQL Server:** por ejemplo, la restauración una base de datos que se ejecutaba en SQL Server 2014 en SQL Server 2016 no se admite. De igual forma, no se admite la restauración de una base de datos de sitio que se ejecutaba en SQL Server 2016 Standard Edition en SQL Server 2016 Enterprise Edition.
-   SQL Server no debe estar establecido en el **modo de usuario único**.
-   Asegúrese de que los archivos .mdf y .ldf sean válidos. Al recuperar un sitio, no se realiza ninguna comprobación del estado de los archivos que se están restaurando.

**Si utiliza un grupo de disponibilidad AlwaysOn de SQL Server para hospedar la base de datos de sitio:** modifique los planes de recuperación, como se describe en [Prepararse para usar SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery).

**Al utilizar réplicas de bases de datos**: después de restaurar una base de datos de sitio configurada para réplicas de base de datos, para poder utilizar las réplicas de base de datos debe volver a configurar cada réplica de base de datos y volver a crear tanto las publicaciones como las suscripciones.

## <a name="determine-your-recovery-options"></a>Determinar las opciones de recuperación
Debe tener en cuenta dos áreas principales para la recuperación del sitio de administración central y del servidor de sitio primario de Configuration Manager: el **servidor de sitio** y la **base de datos de sitio**.
Las secciones siguientes pueden ayudarle a seleccionar las mejores opciones para el escenario de recuperación.

> [!NOTE]   
> Cuando el programa de instalación detecta que hay un sitio de Configuration Manager en el servidor, puede iniciar una recuperación de sitio, pero las opciones de recuperación del servidor de sitio estarán limitadas. Por ejemplo, si ejecuta el programa de instalación en un servidor de sitio existente, al elegir la recuperación podrá recuperar el servidor de base de datos de sitio, pero la opción de recuperación del servidor de sitio estará deshabilitada.

### <a name="site-server-recovery-options"></a>Opciones de recuperación de servidor de sitio
Inicie el programa de instalación a partir de una copia de la carpeta **CD.Latest** creada fuera de la carpeta de instalación de Configuration Manager.
-   Si ejecuta el programa de instalación de Configuration Manager desde el menú **Inicio** del servidor de sitio, la opción **Recuperar un sitio** no estará disponible.
-   Si ha instalado alguna actualización desde la consola de Configuration Manager antes de hacer la copia de seguridad, no puede reinstalar correctamente el sitio mediante el programa de instalación desde los medios de instalación o la ruta de instalación de Configuration Manager.

A continuación, seleccione la opción **Recuperar un sitio** . Cuenta con las siguientes opciones de recuperación para el servidor de sitio con errores:

-   **Recuperar el servidor de sitio mediante una copia de seguridad existente**: use esta opción si tiene una copia de seguridad del servidor de sitio de Configuration Manager que se creó en el servidor de sitio como parte de la tarea de mantenimiento **Copia de seguridad del servidor del sitio** antes de que se produjeran errores en el sitio. Se vuelve a instalar y se configura el sitio a partir del sitio cuya copia de seguridad se realizó.
-   **Reinstalar el servidor de sitio**: use esta opción si no tiene una copia de seguridad del servidor de sitio. Se vuelve a instalar el servidor del sitio, y debe especificar la configuración del sitio tal como lo haría durante la instalación inicial.
  -   Debe utilizar el mismo código de sitio y el mismo nombre de base de datos de sitio utilizados cuando se instaló por primera vez el sitio con errores.
  -   Puede volver a instalar el sitio en un nuevo equipo que ejecuta un nuevo sistema operativo.
  -   El equipo debe usar el mismo nombre, el nombre de dominio completo, del servidor del sitio original.   

### <a name="site-database-recovery-options"></a>Opciones de recuperación de base de datos de sitio
Cuando ejecuta el programa de instalación, tiene las siguientes opciones de recuperación para la base de datos de sitio:
-   **Recuperar la base de datos de sitio con un conjunto de copia de seguridad**: use esta opción si tiene una copia de seguridad de la base de datos de sitio de Configuration Manager que se creó como parte de la tarea de mantenimiento **Copia de seguridad del servidor del sitio** ejecutada en el sitio antes de que se produjeran errores en la base de datos del sitio. Si hay una jerarquía, los cambios realizados en la base de datos de sitio después de la última copia de seguridad de la base de datos de sitio se recuperan del sitio de administración central para un sitio primario, o de un sitio primario de referencia para un sitio de administración central. Si recupera la base de datos del sitio para un sitio primario independiente, perderá los cambios que se hayan realizado en el sitio desde la copia de seguridad más reciente.

   Cuando se recupera la base de datos de un sitio de una jerarquía, el comportamiento de la recuperación estará en función de si se trata del sitio de administración central o un sitio primario, o de si la copia de seguridad más reciente pertenece o no al período de retención de seguimiento de cambios de SQL. Para obtener más información, consulte la sección [Escenarios de recuperación de base de datos de sitio](##site-database-recovery-scenarios) de este tema.
  > [!NOTE]   
  > La recuperación no se completará correctamente si selecciona restaurar la base de datos del sitio mediante un conjunto de copia de seguridad, pero la base de datos del sitio ya existe.  

-   **Crear una nueva base de datos para este sitio**: use esta opción si no tiene una copia de seguridad de la base de datos de sitio de Configuration Manager. Si hay una jerarquía, se creará una base de datos del sitio nueva, y los datos se recuperarán a partir de datos replicados del sitio de administración central para un sitio primario, o del sitio primario de referencia para un sitio de administración central. Esta opción no está disponible cuando se recupera un sitio primario independiente o un sitio de administración central que no tiene sitios primarios.

-   **Usar una base de datos del sitio que se ha recuperado manualmente**: use esta opción si ya recuperó la base de datos de sitio de Configuration Manager, pero tiene que completar el proceso de recuperación.
    -   Configuration Manager puede recuperar la base de datos de sitio a partir de la tarea de mantenimiento de copia de seguridad de Configuration Manager o desde una copia de seguridad de la base de datos de sitio realizada mediante DPM u otro proceso. Si recupera la base de datos del sitio con un método ajeno a Configuration Manager, tendrá que ejecutar el programa de instalación y seleccionar esta opción para completar la recuperación de la base de datos del sitio.

    > [!NOTE]   
    > Si usa DPM para realizar la copia de seguridad de la base de datos del sitio, emplee los procedimientos de DPM para restaurar la base de datos del sitio en una ubicación determinada antes de continuar con el proceso de restauración en Configuration Manager. Para obtener más información acerca de DPM, consulte la [Data Protection Manager Documentation Library (Biblioteca de documentación de Data Protection Manager)]() en TechNet.    

    -   Si hay una jerarquía, los cambios realizados en la base de datos de sitio después de la última copia de seguridad de la base de datos de sitio se recuperan del sitio de administración central para un sitio primario, o de un sitio primario de referencia para un sitio de administración central. Si recupera la base de datos del sitio para un sitio primario independiente, perderá los cambios que se hayan realizado en el sitio desde la copia de seguridad más reciente.     


-   **Omitir recuperación de base de datos**: use esta opción si no se produjo una pérdida de datos en el servidor de base de datos del sitio de Configuration Manager. Esta opción solo es válida si la base de datos del sitio no está en el mismo equipo que el servidor de sitio que está en proceso de recuperación.

### <a name="sql-server-change-tracking-retention-period"></a>Período de retención de seguimiento de cambios de SQL Server
El seguimiento de cambios está habilitado para la base de datos del sitio en SQL Server. El seguimiento de cambios permite a Configuration Manager realizar consultas sobre los cambios que se realizaron en las tablas de base de datos a partir de un punto concreto en el tiempo. El período de retención especifica cuánto tiempo se conserva la información del seguimiento de cambios. De forma predeterminada, la base de datos del sitio está configurada para tener un período de retención de 5 días. Cuando se recupera una base de datos del sitio, el proceso de recuperación variará en función de si la copia de seguridad pertenece o no al período de retención. Por ejemplo, si se produce un error en el servidor de base de datos del sitio, y la última copia de seguridad se hizo hace 7 días, ésta no pertenecerá al período de retención.

Para obtener más información sobre los datos internos de seguimiento de cambios de SQL Server, consulte los siguientes blogs del equipo de SQL Server: [Change Tracking Cleanup - part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) (Limpieza de seguimiento de cambios - parte 1) y [Change Tracking Cleanup - part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2) (Limpieza de seguimiento de cambios - parte 2).

### <a name="reinitialization-of-site-or-global-data"></a>Reinicialización de los datos globales o del sitio
El proceso para reinicializar datos globales o del sitio reemplaza los datos existentes de la base de datos del sitio por datos de otra base de datos del sitio. Por ejemplo, si el sitio ABC reinicializa datos desde el sitio XYZ, se producen los siguientes pasos:
-   Los datos se copian desde el sitio XYZ al sitio ABC.
-   Los datos existentes para el sitio XYZ se quitan de la base de datos del sitio en el sitio ABC.
-   Los datos copiados desde el sitio XYZ se insertan en la base de datos del sitio para el sitio ABC.

#### <a name="example-scenario-1"></a>Escenario de ejemplo 1
**El sitio primario reinicializa los datos globales desde el sitio de administración central**: el proceso de recuperación quita los datos globales existentes para el sitio primario en la base de datos del sitio primario y los reemplaza con los datos globales copiados desde el sitio de administración central.

#### <a name="example-scenario-2"></a>Escenario de ejemplo 2
**El sitio de administración central reinicializa los datos del sitio desde un sitio primario**: el proceso de recuperación quita los datos de sitio existentes para ese sitio primario en la base de datos del sitio de administración central y los reemplaza con los datos de sitio copiados desde el sitio primario. No se ven afectados los datos del sitio para otros sitios primarios.

### <a name="site-database-recovery-scenarios"></a>Escenarios de recuperación de base de datos de sitio
Una vez restaurada la base de datos del sitio desde una copia de seguridad, Configuration Manager intenta restaurar los cambios que tuvieron lugar en los datos globales y del sitio desde la última copia de seguridad de la base de datos. A continuación se indican las acciones que Configuration Manager inicia una vez que se restaura la base de datos del sitio desde una copia de seguridad.

**El sitio recuperado es un sitio de administración central:**
-   **Copia de seguridad de base de datos dentro del período de retención del seguimiento de cambios**
    -   **Datos globales** : los cambios en los datos globales posteriores a la copia de seguridad se replican desde todos los sitios principales.
    -   **Datos del sitio** : los cambios en los datos del sitio posteriores a la copia de seguridad se replican desde todos los sitios principales.


-   **Copia de seguridad de base de datos anterior al período de retención de seguimiento de cambios**
    -   **Datos globales**: el sitio de administración central reinicializa los datos globales desde el sitio principal de referencia, si lo especifica. A continuación, el resto de sitios primarios reinicializan los datos globales desde el sitio de administración central. Si no se especifica ningún sitio de referencia, todos los sitios primarios reinicializan los datos globales desde el sitio de administración central (es decir, los datos que se restauraron a partir de la copia de seguridad).
    -   **Datos del sitio** : el sitio de administración central reinicializa los datos del sitio desde cada sitio principal.


**El sitio recuperado es un sitio primario:**
-   **Copia de seguridad de base de datos dentro del período de retención del seguimiento de cambios**
    -   **Datos globales** : los cambios en los datos globales posteriores a la copia de seguridad se replican desde el sitio de administración central.
    -   **Datos del sitio** : el sitio de administración central reinicializa los datos del sitio desde el sitio principal. Los cambios posteriores a la copia de seguridad se pierden, pero los clientes que envían información al sitio primario regeneran la mayor parte de ellos.


-   **Copia de seguridad de base de datos anterior al período de retención de seguimiento de cambios**
    -   **Datos globales** : el sitio primario reinicializa los datos globales desde el sitio de administración central.
    -   **Datos del sitio** : el sitio de administración central reinicializa los datos del sitio desde el sitio principal. Los cambios posteriores a la copia de seguridad se pierden, pero los clientes que envían información al sitio primario regeneran la mayor parte de ellos.

## <a name="site-recovery-procedures"></a>Procedimientos de recuperación de sitio
Utilice uno de los siguientes procedimientos para recuperar la base de datos del sitio y el servidor del sitio.

### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>Para iniciar una recuperación de sitio en el Asistente para instalación
1.  Copie la carpeta [CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) en una ubicación fuera de la carpeta de instalación de Configuration Manager.
Desde la copia de la carpeta CD.Latest, ejecute el Asistente para instalación de Configuration Manager.

2.  En la página **Primeros pasos** , seleccione **Recuperar un sitio**y, a continuación, haga clic en **Siguiente**.

3.  Complete el asistente con las opciones apropiadas para la recuperación de sitio que desea completar.

  -   Durante la recuperación, el programa de instalación identifica el puerto de SQL Server Service Broker (SSB) que utiliza SQL Server. No cambie este puerto durante la recuperación; de lo contrario, la replicación de datos no funcionará correctamente una vez finalizada la recuperación.

  -   Puede especificar la ruta de acceso original o una nueva para la instalación de Configuration Manager en el Asistente para instalación.

### <a name="to-start-an-unattended-site-recovery"></a>Para iniciar una recuperación de sitio desatendida
  1.    Prepare el script de instalación desatendida para las opciones que necesita para la recuperación de sitio.  Consulte [Claves de archivo de script de recuperación de sitio desatendida](/sccm/protect/understand/unattended-site-recovery-script-file-keys).

  2.    Ejecute el programa de instalación de Configuration Manager mediante la opción de comando **/script**. Por ejemplo, si designó el archivo de inicialización de instalación con el nombre ConfigMgrUnattend.ini y lo guardó en el directorio C:\Temp del equipo en el que ejecuta el programa de instalación, el comando sería: **Setup /script C:\temp\ConfigMgrUnattend.ini**

  > [!NOTE]   
  >  Después de recuperar un sitio de administración central, la replicación de algunos datos de sitios secundarios no puede establecerse. Podrían incluirse el inventario de hardware, el inventario de software y los mensajes de estado.
  >
  >  Si esto ocurre, debe reinicializar la cola **ConfigMgrDRSSiteQueue** para la replicación de base de datos.  Para ello, use el **Administrador de SQL Server** para ejecutar la consulta siguiente en la base de datos de sitio de Configuration Manager en el sitio de administración central:
  >
  >  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**
  >
  >  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**


## <a name="post-recovery-tasks"></a>Tareas posteriores a la recuperación
Tras la recuperación del sitio, se pueden llevar a cabo varias tareas posteriores a la recuperación antes de que se complete totalmente la recuperación del sitio. Consulte las secciones siguientes para obtener información útil acerca de cómo completar el proceso de recuperación del sitio.

### <a name="re-enter-user-account-passwords"></a>Volver a escribir las contraseñas de cuentas de usuario
Tras la recuperación del servidor del sitio, es necesario volver a escribir las contraseñas de las cuentas de usuario especificadas para el sitio debido a que se restablecen durante el proceso de recuperación. Las cuentas se enumeran en la página **Finalizado** del Asistente para la instalación tras completarse la recuperación y se guardan en C:\ConfigMgrPostRecoveryActions.html en el servidor del sitio recuperado.

#### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>Para volver a escribir las contraseñas de cuentas de usuario después de la recuperación del sitio

1.  Abra la consola de Configuration Manager y conéctese con el sitio recuperado.

2.  En la consola de Configuration Manager, haga clic en **Administración**.

3.  En el área de trabajo **Administración** , expanda **Seguridad**y, a continuación, haga clic en **Cuentas**.

4.  Para cada cuenta en la que deba volver a escribir la contraseña, haga lo siguiente:

    1.  Seleccione la cuenta de la lista de cuentas que se identificaron después de la recuperación del sitio. Puede encontrar esta lista en C:\ConfigMgrPostRecoveryActions.html en el servidor del sitio recuperado.

    2.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades** para abrir las propiedades de la cuenta.

    3.  En la pestaña **General** , haga clic en **Establecer**y, a continuación, vuelva a escribir las contraseñas para la cuenta.

    4.  Haga clic en **Comprobar**, seleccione el origen de datos apropiado para la cuenta de usuario seleccionada y, a continuación, haga clic en **Conexión de prueba** para comprobar que la cuenta de usuario se puede conectar al origen de datos.

    5.  Haga clic en **Aceptar** para guardar los cambios de contraseña y, a continuación, haga clic en **Aceptar**.

### <a name="re-enter-sideloading-keys"></a>Volver a escribir las claves de instalación de prueba
Después de una recuperación del servidor de sitio, es preciso volver a escribir las claves de instalación de prueba de Windows especificadas para el sitio, ya que se restablecen durante la recuperación del sitio. Después de volver a escribir las claves de instalación de prueba, se restablece el contador de la columna **Activaciones usadas** de las claves de instalación de prueba de Windows en la consola de Configuration Manager. Por ejemplo, supongamos que antes del error del sitio, el valor del contador **Total de activaciones** era **100** y el de **Activaciones usadas** (el número de claves usadas por dispositivos) era **90**. Después de la recuperación del sitio, la columna **Total de activaciones** muestra **100**, pero la columna **Activaciones usadas** muestra, de forma incorrecta, **0**. Sin embargo, después de que 10 nuevos dispositivos utilicen una clave de instalación de prueba, no quedará ninguna clave de instalación de prueba y, por lo tanto, el siguiente dispositivo no podrá aplicar ninguna clave de instalación de prueba.

### <a name="recreate-the-microsoft-intune-subscription"></a>Volver a crear la suscripción a Microsoft Intune
 Si recupera un servidor de sitio de Configuration Manager después de volver a crear la imagen del equipo del servidor de sitio, la suscripción de Microsoft Intune no se restaurará. Debe volver a conectar la suscripción después de recuperar el sitio.  No cree una nueva solicitud de APN. En su lugar, cargue el archivo .pem válido actual que se cargó la última vez que se configuró o se renovó la administración de iOS. Para más información, vea [Configuring the Microsoft Intune subscription (Configuración de la suscripción de Microsoft Intune)](/sccm/mdm/deploy-use/configure-intune-subscription).

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configuración de SSL para roles de sistema de sitio que usan IIS
Al recuperar sistemas de sitio que ejecutan IIS y que se habían configurado para HTTPS antes del error, debe volver a configurar IIS para utilizar el certificado de servidor web.

### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>Reinstalación de revisiones en el servidor del sitio recuperado
Tras una recuperación del sitio, debe reinstalar las revisiones que se han aplicado al servidor del sitio. Vea la lista de las revisiones instaladas anteriormente en la página **Finalizado** del Asistente para instalación después de la recuperación del sitio. La lista se guarda también en **C:\ConfigMgrPostRecoveryActions.html** en el servidor del sitio recuperado.

### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>Recuperación de informes personalizados en el equipo en que se ejecuta Reporting Services
Si ha creado informes personalizados con Reporting Services y se produce algún error con Reporting Services, puede recuperar los informes si ha realizado una copia de seguridad del servidor de informes. Para obtener más información acerca de la restauración de los informes personalizados en Reporting Services, consulte [Operaciones de copias de seguridad y restauración para una instalación de Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=228724) en Libros en pantalla de SQL Server 2008.

### <a name="recover-content-files"></a>Recuperación de archivos de contenido
 La base de datos del sitio contiene información acerca de dónde están almacenados los archivos de contenido en el servidor del sitio, pero no se realiza ninguna copia de seguridad ni restauración de estos archivos como parte del proceso de copia de seguridad y restauración. Para recuperar totalmente los archivos de contenido, debe restaurar la biblioteca de contenido y los archivos de origen del paquete en el servidor del sitio. Existen varios métodos para recuperar los archivos de contenido, pero el método más sencillo consiste en restaurar los archivos desde una copia de seguridad del sistema de archivos del servidor del sitio.

 Si no dispone de una copia de seguridad del sistema de archivos de origen del paquete, debe copiarlos o descargarlos manualmente como lo hizo inicialmente la primera vez que creó el paquete. Puede ejecutar la siguiente consulta en SQL Server para buscar la ubicación del origen del paquete para todos los paquetes y aplicaciones: `SELECT * FROM v_Package`. Puede identificar el sitio del origen del paquete mediante los tres primeros caracteres del identificador del paquete. Por ejemplo, si el identificador del paquete es CEN00001, el código de sitio del sitio de origen es CEN. Cuando restaure los archivos de origen del paquete, se deben restaurar en la misma ubicación en la que se encontraban antes del error.

 Si no tiene una copia de seguridad del sistema de archivos que contiene la biblioteca de contenido, tiene las siguientes opciones de restauración:

-   **Importar un archivo de contenido preconfigurado**: si hay una jerarquía de Configuration Manager, puede crear un archivo de contenido preconfigurado con todos los paquetes y las aplicaciones de otra ubicación y luego importar el archivo de contenido preconfigurado para recuperar la biblioteca de contenido en el servidor de sitio.

-   **Actualizar contenido**: cuando se inicia la acción de actualización de contenido para un tipo de implementación de paquete o aplicación, el contenido se copia desde el origen del paquete a la biblioteca de contenido. Los archivos de origen del paquete deben estar disponibles en la ubicación original para que esta acción se complete correctamente. Debe ejecutar esta acción en cada paquete y aplicación.

### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>Recuperación de actualizaciones de software personalizadas en el equipo que ejecuta Updates Publisher
Cuando se han incluido archivos de base de datos de Updates Publisher en el plan de copias de seguridad, es posible recuperar las bases de datos si se produce un error en el equipo en el que se ejecuta Updates Publisher. Para obtener más información acerca de Updates Publisher, consulte [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) en la biblioteca de TechCenter de System Center.

Use el siguiente procedimiento para restaurar la base de datos de Updates Publisher.

#### <a name="to-restore-the-updates-publisher-2011-database"></a>Para restaurar la base de datos de Updates Publisher 2011
1.  Vuelva a instalar Updates Publisher en el equipo recuperado.

2.  Copie el archivo de base de datos (Scupdb.sdf) del destino de copia de seguridad en %*PERFILUSUARIO*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ en el equipo que ejecuta Updates Publisher.

3.  Si más de un usuario ejecuta Updates Publisher en el equipo, debe copiar cada archivo de base de datos en la ubicación del perfil de usuario correspondiente.

### <a name="user-state-migration-data"></a>Datos de migración de estado de usuario
Como parte de las propiedades de sistema de sitio de punto de migración de estado, se especifican las carpetas que almacenan datos de migración de estado de usuario. Después de recuperar un servidor con una carpeta que almacena los datos de migración de estado de usuario, debe restaurar manualmente los datos de migración de estado de usuario del servidor en las mismas carpetas que almacenaban los datos antes del error.

### <a name="regenerate-the-certificates-for-distribution-points"></a>Regeneración de los certificados para puntos de distribución
Después de restaurar un sitio, el registro distmgr.log podría contener la siguiente entrada para uno o varios puntos de distribución: **Error al descifrar los datos de certificado PFX**. Esta entrada indica que el sitio no puede descifrar los datos del certificado de punto de distribución. Para resolver este problema debe regenerar o volver a importar el certificado para los puntos de distribución afectados. Se puede hacer con el cmdlet [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) de PowerShell.

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Actualización de certificados que se utilizan para puntos de distribución basados en la nube
 Configuration Manager exige un certificado de administración que usa para la comunicación entre servidores de sitio y puntos de distribución basados en la nube. Después de una recuperación de sitio, debe actualizar los certificados de los puntos de distribución basados en la nube.

## <a name="recover-a-secondary-site"></a>Recuperar un sitio secundario
 Configuration Manager no admite la copia de seguridad de la base de datos en un sitio secundario, pero sí admite la recuperación mediante la reinstalación del sitio secundario. Se precisa la recuperación de sitio secundario si se produce un error en un sitio secundario de Configuration Manager.

### <a name="requirements-for-reinstalling-a-secondary-site"></a>Requisitos para volver a instalar un sitio secundario
-   El equipo debe cumplir todos los requisitos previos del sitio secundario y tener los derechos de seguridad correspondientes configurados.
-   Debe utilizar la misma ruta de instalación que se utilizó para el sitio con errores.
-   Debe usar un equipo con la misma configuración que el equipo con errores, como su FQDN, para recuperar correctamente el sitio secundario.
-   El equipo debe tener la misma configuración de SQL Server que el sitio con errores.
  -   Durante la recuperación de sitio secundario, Configuration Manager no instala SQL Server Express si no está instalado ya en el equipo.
  -   Debe utilizar la misma versión de SQL Server y la misma instancia de SQL Server que se utilizaron para la base de datos del sitio secundario antes del error.

### <a name="to-recover-a-secondary-site"></a>Para recuperar un sitio secundario:
Para recuperar un sitio secundario, utilice la acción **Recuperar sitio secundario** del nodo **Sitios** de la consola de Configuration Manager. A diferencia de la recuperación de un sitio de administración central o de un sitio primario, en la recuperación de un sitio secundario no se usa un archivo de copia de seguridad, sino que se reinstalan los archivos de ese sitio secundario en el equipo con errores. Una vez reinstalado el sitio, los datos del sitio secundario se reinicializan con los datos del sitio primario.

Durante el proceso de recuperación, Configuration Manager verifica la existencia de la biblioteca de contenido en el equipo de sitio secundario y la disponibilidad del contenido correspondiente. El sitio secundario usará la biblioteca de contenido existente, si esta incluye el contenido adecuado. En caso contrario, para recuperar la biblioteca de contenido de un sitio secundario recuperado, es necesario redistribuir o preconfigurar el contenido en ese sitio recuperado.

Si tiene un punto de distribución que no está en el sitio secundario, no es preciso que vuelva a instalar el punto de distribución durante la recuperación del sitio secundario. Después de la recuperación de sitio secundario, el sitio se sincroniza automáticamente con el punto de distribución.

Puede comprobar el estado de la recuperación del sitio secundario mediante la acción **Mostrar estado de instalación** del nodo **Sitios** de la consola de Configuration Manager.
