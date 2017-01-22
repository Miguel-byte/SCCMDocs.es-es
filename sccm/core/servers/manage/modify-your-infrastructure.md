---
title: Modificar infraestructura | Microsoft Docs
description: Aprenda a realizar cambios o adoptar medidas que afectan a la infraestructura de Configuration Manager que ha implementado.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
caps.latest.revision: 19
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: fa9881e06abd410438fe5985151309c45f337802


---
# <a name="modify-your-system-center-configuration-manager-infrastructure"></a>Modificar la infraestructura de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Después de instalar uno o varios sitios, es posible que deba modificar las configuraciones o realizar acciones que afecten a la infraestructura que tiene implementada.  


##  <a name="a-namebkmkmanagesmsprovidera-manage-the-sms-provider"></a><a name="BKMK_ManageSMSprovider"></a> Administración del proveedor de SMS  
 El proveedor de SMS [un archivo de biblioteca de vínculos dinámicos (smsprov.dll)] proporciona el punto de contacto administrativo para una o varias consolas de Configuration Manager. Al instalar varios proveedores de SMS, puede proporcionar redundancia a los puntos de contacto para administrar el sitio y la jerarquía.  

 En cada sitio de Configuration Manager, puede volver a ejecutar el programa de instalación para:  

-   Agregar una instancia adicional del proveedor de SMS (cada instancia adicional del proveedor de SMS debe estar en un equipo independiente).  

-   Quitar una instancia del proveedor de SMS (para quitar el último proveedor de SMS de un sitio, debe desinstalar el sitio).  

 Para supervisar la instalación o eliminación del proveedor de SMS, consulte el archivo **ConfigMgrSetup.log** en la carpeta raíz del servidor del sitio en el que ejecuta el programa de instalación.  

 Antes de modificar el proveedor de SMS en un sitio, familiarícese con la información en [Plan para el proveedor de SMS de System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

#### <a name="to-manage-the-sms-provider-configuration-for-a-site"></a>Para administrar la configuración del proveedor de SMS para un sitio  

1.  Ejecute el **programa de instalación de Configuration Manager** desde la **&lt;carpeta de instalación del sitio de Configuration Manager\>\BIN\X64\setup.exe**.  

2.  En la página **Primeros pasos** , seleccione **Realizar mantenimiento de sitio o restablecer este sitio**y, a continuación, haga clic en **Siguiente**.  

3.  En la página **Mantenimiento del sitio** , seleccione **Modificar configuración de proveedor de SMS**y, a continuación, haga clic en **Siguiente**.  

4.  En la página **Administrar proveedores de SMS** , seleccione una de las siguientes opciones y complete el asistente mediante una de las opciones siguientes:  

    -   Para agregar un proveedor de SMS adicional en este sitio:  

         seleccione **Agregar un nuevo proveedor de SMS**, especifique el FQDN para el equipo que va a hospedar el proveedor de SMS y no hospeda actualmente un proveedor de SMS y, a continuación, haga clic en **Siguiente**.  

    -   Para quitar un proveedor de SMS desde un servidor:  

         seleccione **Desinstalar el proveedor de SMS especificado**, seleccione el nombre del equipo desde el que desea quitar el proveedor de SMS, haga clic en **Siguiente**y, a continuación, confirme la acción.  

        > [!TIP]  
        >  Para mover el proveedor de SMS entre dos equipos, debe instalar el proveedor de SMS en el nuevo equipo y quitar el proveedor de SMS de la ubicación original. No hay ninguna opción dedicada para mover el proveedor de SMS entre equipos en un único proceso.  

 Cuando finalice el Asistente para instalación, se completa la configuración del proveedor de SMS. En la pestaña **General** del cuadro de diálogo **Propiedades** del sitio, puede comprobar los equipos que tienen un proveedor de SMS instalado para el sitio.  

##  <a name="a-namebkmkconsolea-manage-the-configuration-manager-console"></a><a name="bkmk_Console"></a> Administración de la consola de Configuration Manager  
 A continuación, se indican las tareas que puede realizar para administrar la consola de Configuration Manager:  

-   **Modificar el idioma que se muestra en la consola de Configuration Manager**: para modificar los idiomas instalados, consulte [Administración del idioma de la consola de Configuration Manager](#BKMK_ManageConsoleLanguages) en este tema.  

-   **Instalar consolas adicionales**: para instalar consolas adicionales, consulte [Install System Center Configuration Manager consoles](/sccm/core/servers/deploy/install/install-consoles) (Instalación de consolas de System Center Configuration Manager).  

-   **Configurar DCOM**: para configurar los permisos de DCOM para habilitar consolas remotas desde el servidor de sitio que se va a conectar, consulte [Configuración de permisos de DCOM para consolas remotas de Configuration Manager](#BKMK_ConfigDCOMforRemoteConsole) en este tema.  

-   **Modificar permisos para limitar los usuarios administrativos que pueden ver contenido en la consola**: para modificar los permisos administrativos, que limitan qué usuarios pueden ver contenido y realizar acciones en la consola, consulte [Modify the administrative scope of an administrative user](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_ModAdminUser) (Modificación del ámbito administrativo de un usuario administrativo).     

###  <a name="a-namebkmkmanageconsolelanguagesa-manage-configuration-manager-console-language"></a><a name="BKMK_ManageConsoleLanguages"></a> Administración del idioma de la consola de Configuration Manager  
 Durante la instalación del servidor de sitio, los archivos de instalación de la consola de Configuration Manager y los paquetes de idiomas compatibles con el sitio se copian en la subcarpeta **&lt;ConfigMgrInstallationPath\>\Tools\ConsoleSetup** del servidor de sitio.  

-   Cuando inicia la instalación de la consola de Configuration Manager desde esta carpeta en el servidor de sitio, la consola de Configuration Manager y los archivos de paquetes de idioma admitidos se copian en el equipo.  

-   Cuando un paquete de idioma está disponible para la configuración de idioma actual del equipo, la consola de Configuration Manager se abre en dicho idioma.  

-   Si el paquete de idioma asociado no está disponible para la consola de Configuration Manager, esta se abre en inglés.  

Por ejemplo, considere un escenario donde se instala la consola de Configuration Manager desde un servidor de sitio que admite inglés, alemán y francés. Si abre la consola de Configuration Manager en un equipo con francés como idioma configurado, la consola se abre en francés. Si abre la consola de Configuration Manager en un equipo con japonés como idioma configurado, la consola se abre en inglés porque el paquete de idioma japonés no está disponible.  

 Cada vez que se abre la consola de Configuration Manager, esta determina el idioma configurado para el equipo, comprueba si un paquete de idioma asociado está disponible para la consola de Configuration Manager y, a continuación, abre la consola mediante el paquete de idioma apropiado. Si opta por abrir la consola de Configuration Manager en inglés, independientemente del idioma configurado en el equipo, debe quitar los archivos del paquete de idioma del equipo, o bien cambiarles el nombre.  

 Utilice los siguientes procedimientos para iniciar la consola de Configuration Manager en inglés, independientemente de la configuración regional establecida en el equipo.  

##### <a name="to-install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Para instalar sólo la versión en inglés de la consola de Configuration Manager en equipos.  

1.  En el Explorador de Windows, examine **&lt;ConfigMgrInstallationPath\>\Tools\ConsoleSetup\LanguagePack**.  

2.  Cambie el nombre de los archivos **.msp** y **.mst** . Por ejemplo, puede cambiar **&lt;nombre archivo\>.MSP** a **&lt;nombre archivo\>.MSP.deshabilitado**.  

3.  Instale la consola de Configuration Manager en el equipo.  

    > [!IMPORTANT]  
    >  Cuando se configuran idiomas de servidor nuevos para el servidor de sitio, los archivos .msp y .mst se copian de nuevo en la carpeta **LanguagePack**. Debe repetir este procedimiento cada vez que instala una consola de Configuration Manager solo en inglés.  

##### <a name="to-temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>Para deshabilitar temporalmente un idioma de la consola en una instalación de la consola de Configuration Manager  

1.  En el equipo que ejecuta la consola de Configuration Manager, cierre la consola de Configuration Manager.  

2.  En el Explorador de Windows, examine &lt;*ConsoleInstallationPath*>\Bin\ en el equipo de la consola de Configuration Manager.  

3.  Cambie el nombre de la carpeta de idioma del idioma que está configurado en el equipo. Por ejemplo, si el idioma configurado para el equipo era el alemán, puede cambiar el nombre de la carpeta **de** a **de.deshabilitado**.  

4.  Para abrir la consola de Configuration Manager en el idioma configurado para el equipo, cambie el nombre de la carpeta al nombre original. Por ejemplo, cambie el nombre de **de.dehabilitado** a **de**.  

##  <a name="a-namebkmkconfigdcomforremoteconsolea-configure-dcom-permissions-for-remote-configuration-manager-consoles"></a><a name="BKMK_ConfigDCOMforRemoteConsole"></a> Configuración de permisos de DCOM para consolas remotas de Configuration Manager  
 La cuenta de usuario que ejecuta la consola de Configuration Manager requiere el permiso para obtener acceso a la base de datos del sitio mediante el proveedor de SMS. Sin embargo, un usuario administrativo que usa una consola remota de Configuration Manager también requiere permisos de DCOM de **Activación remota** en:  

-   El equipo de servidor de sitio  

-   Cada equipo que hospede una instancia del proveedor de SMS  

 El grupo de seguridad denominado **Administradores de SMS** concede acceso al proveedor de SMS y también puede usarse para conceder los permisos de DCOM necesarios. (Este grupo es local para el equipo cuando el proveedor de SMS se ejecuta en un servidor miembro, y es un grupo local de dominio cuando el proveedor de SMS se ejecuta en un controlador de dominio).  

> [!IMPORTANT]  
>  La consola de Configuration Manager utiliza el Instrumental de administración de Windows (WMI) para conectarse con el proveedor de SMS, y WMI utiliza internamente DCOM. Por tanto, Configuration Manager requiere permisos para activar un servidor de DCOM en el equipo del proveedor de SMS si la consola de Configuration Manager se ejecuta en un equipo distinto del equipo del proveedor de SMS. De forma predeterminada, la activación remota solo se concede a los miembros del grupo de administradores integrados. Si permite que el grupo de administradores de SMS tengan el permiso de activación remota, un miembro de este grupo podría intentar ataques de DCOM contra el equipo del proveedor de SMS. Esta configuración también aumenta la superficie expuesta a ataques del equipo. Para mitigar esta amenaza, debe supervisar cuidadosamente la pertenencia al grupo de administradores de SMS.  

 Utilice el procedimiento siguiente para configurar cada sitio de administración central, servidor de sitio primario y cada equipo en donde está instalado el proveedor de SMS para conceder acceso remoto a la consola de Configuration Manager a usuarios administrativos.  

#### <a name="to-configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>Para configurar permisos de DCOM para conexiones remotas de la consola de Configuration Manager  

1.  Ejecute  **Dcomcnfg.exe** para abrir **Servicios de componentes**.  

2.  En **para abrir**, haga clic en **Raíz de consola** >  **para abrir** > **Equipos**y, a continuación, haga clic en **Mi PC**. En el menú **Acción** , haga clic en **Propiedades**.  

3.  En el cuadro de diálogo **Propiedades de Mi PC** , en la pestaña **Seguridad COM** , en la sección **Permisos de inicio y activación** , haga clic en **Editar límites**.  

4.  En el cuadro de diálogo **Permisos de inicio y activación** , haga clic en **Agregar**.  

5.  En el cuadro de diálogo **Seleccionar usuario, equipos, cuentas de servicio o grupos** , en el cuadro **Escribir los nombres de objeto para seleccionar (ejemplos)** , escriba **SMS Admins**y después haga clic en **Aceptar**.  

    > [!NOTE]  
    >  Es posible que tenga que cambiar la configuración de **Desde esta ubicación** para ubicar el grupo de administradores de SMS. Este grupo es local al equipo cuando el proveedor de SMS se ejecuta en un servidor miembro, y es un grupo local de dominio cuando el proveedor de SMS se ejecuta en un controlador de dominio.  

6.  En la sección **Permisos para administradores de SMS** , para permitir la activación remota, active la casilla **Activación remota** .  

7.  Haga clic en **Aceptar** y vuelva a hacer clic en **Aceptar** y, a continuación, cierre **Administración de equipos**. El equipo ya está configurado para permitir el acceso remoto a la consola de Configuration Manager a los miembros del grupo de administradores de SMS.  

 Repita este procedimiento en cada equipo del proveedor de SMS que pueda admitir consolas remotas de Configuration Manager.  

##  <a name="a-namebkmkdbconfiga-modify-the-site-database-configuration"></a><a name="bkmk_dbconfig"></a> Modificación de la configuración de la base de datos del sitio  
 Después de instalar un sitio, puede modificar la configuración de la base de datos del sitio y el servidor de la base de datos del sitio mediante la ejecución del programa de instalación en un servidor de sitio de administración central o un servidor de sitio primario. Puede mover la base de datos del sitio a una nueva instancia de SQL Server en el mismo equipo o a otro equipo que ejecute una versión compatible de SQL Server. Estos y otros cambios relacionados no se admiten para la configuración de la base de datos en sitios secundarios.  

 Para obtener más información acerca de los límites de compatibilidad, consulte [Directiva de soporte técnico para los cambios de la base de datos manualmente en un entorno de Configuration Manager](https://support.microsoft.com/kb/3106512).  

> [!NOTE]  
>  Al modificar la configuración de la base de datos de un sitio, Configuration Manager reinicia o vuelve a instalar servicios de Configuration Manager en el servidor de sitio y en servidores de sistema de sitio remoto que se comunican con la base de datos.  

**Para modificar la configuración de la base de datos**, debe ejecutar el programa de instalación en el servidor de sitio y seleccionar la opción **Realizar mantenimiento de sitio o restablecer este sitio**. A continuación, seleccione la opción **Modificar configuración de SQL Server** . Puede cambiar las siguientes configuraciones de base de datos del sitio:  

-   El servidor basado en Windows que aloja la base de datos.  

-   La instancia de SQL Server en uso en un servidor que aloja la base de datos de SQL Server.  

-   Nombre de la base de datos.  

-   Puerto de SQL Server en uso por Configuration Manager  

-   Puerto de SQL Server Service Broker en uso por Configuration Manager  

**Si mueve la base de datos del sitio, debe configurar lo siguiente:**  

-   **Configurar acceso:** si mueve la base de datos del sitio a un nuevo equipo, agregue la cuenta de equipo del servidor de sitio al grupo **Administradores locales** del equipo que ejecuta SQL Server. Si utiliza un clúster de SQL Server para la base de datos del sitio, debe agregar la cuenta de equipo al grupo **Administradores locales** de cada equipo de de nodo de clúster de Windows Server.  

-   **Habilitar integración con Common Language Runtime (CLR):**  si mueve la base de datos a una nueva instancia de SQL Server, o a un nuevo equipo de SQL Server, debe habilitar la integración con Common Language Runtime (CLR). Para habilitar CLR, use **SQL Server Management Studio** para conectarse a la instancia de SQL Server que hospeda la base de datos del sitio y ejecute el siguiente procedimiento almacenado como una consulta: **sp_configure 'clr enabled',1; reconfigure**.  
-  **Asegurarse de que el nuevo servidor de SQL Server tiene acceso a la ubicación de copia de seguridad:** cuando use una ruta UNC para almacenar la copia de seguridad de base de datos de su sitio, después de mover la base de datos a un nuevo servidor, incluido el movimiento a un grupo de disponibilidad AlwaysOn de SQL Server o a un clúster de SQL Server, asegúrese de que la cuenta de equipo del nuevo servidor de SQL Server tiene permisos de **escritura** en la ubicación UNC.  


> [!IMPORTANT]  
>  Antes de mover una base de datos que tenga una o más réplicas de base de datos para puntos de administración, deberá quitar primero las réplicas de la base de datos. Después de completar el traslado de la base de datos, se pueden reconfigurar las réplicas de la base de datos. Para obtener más información, vea [Database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) (Réplicas de bases de datos para puntos de administración de System Center Configuration Manager).  

##  <a name="a-namebkmkspna-manage-the-spn-for-the-site-database-server"></a><a name="bkmk_SPN"></a> Administración del SPN para el servidor de base de datos del sitio  
Puede elegir la cuenta que ejecuta los servicios de SQL para la base de datos del sitio:  

-   Cuando los servicios se ejecutan con la cuenta de sistema de equipos, el SPN se registra automáticamente.  

-   Cuando los servicios se ejecutan con una cuenta de usuario local de dominio, debe registrar manualmente el SPN para garantizar que los clientes SQL y otro sistema de sitio puedan ejecutar la autenticación Kerberos. Sin la autenticación Kerberos, podrían producirse errores de comunicación con la base de datos.  

La documentación de SQL Server puede ayudarle a [registrar manualmente el SPN](https://technet.microsoft.com/library/ms191153\(v=sql.120\).aspx)y proporcionar información adicional acerca de las conexiones de los SPN y Kerberos.  

> [!IMPORTANT]  
>  -   Cuando se crea un SPN para SQL Server en clúster, debe especificar el nombre virtual del clúster de SQL Server como el nombre de equipo de SQL Server.  
> -   El comando para registrar un SPN para una instancia con nombre de SQL Server es el mismo que se usa para registrar un SPN para una instancia predeterminada, excepto en que el número de puerto debe coincidir con el puerto usado por la instancia con nombre.  

Puede registrar un SPN para la cuenta de servicio SQL Server del servidor de base de datos del sitio mediante la herramienta **Setspn** . Debe ejecutar la herramienta Setspn en un equipo que reside en el dominio de SQL Server, y debe utilizar credenciales de administrador de dominio para ejecutarla.  

 Utilice los procedimientos siguientes como ejemplos de cómo administrar el SPN para la cuenta de servicio de SQL Server que utiliza la herramienta Setspn en Windows Server 2008 R2. Para obtener instrucciones específicas sobre Setspn, consulte [Setspn Overview (Información general de Setspn)](http://go.microsoft.com/fwlink/p/?LinkId=226343), o documentación similar específica de su sistema operativo.  

> [!NOTE]  
>  Los procedimientos siguientes hacen referencia a la herramienta de línea de comandos Setspn. La herramienta de línea de comandos Setspn se incluye al instalar Herramientas de soporte de Windows Server 2003 desde el CD de producto o desde [Microsoft Download Center (Centro de descarga de Microsoft)](http://go.microsoft.com/fwlink/p/?LinkId=100114). Para obtener más información sobre la instalación de Herramientas de soporte de Windows desde el CD de producto, consulte [Instalar las herramientas de soporte de Windows](http://go.microsoft.com/fwlink/p/?LinkId=62270).  

#### <a name="to-manually-create-a-domain-user-service-principal-name-spn-for-the-sql-server-service-account"></a>Para crear manualmente un nombre de entidad de seguridad de servicio (SPN) de usuario de dominio para la cuenta de servicio de SQL Server  

1.  En el menú **Inicio** , haga clic en **Ejecutar**y, a continuación, escriba **cmd** en el cuadro de diálogo Ejecutar.  

2.  En la línea de comandos, desplácese hasta el directorio de instalación de las herramientas de soporte de Windows Server. De forma predeterminada, estas herramientas se encuentran en el directorio **C:\Program Files\Support Tools** .  

3.  Escriba un comando válido para crear el SPN. Para crear el SPN, puede utilizar el nombre NetBIOS o el nombre de dominio completo (FQDN) del equipo que ejecuta SQL Server. Sin embargo, debe crear un SPN para el nombre NetBIOS y el FQDN.  

    > [!IMPORTANT]  
    >  Cuando se crea un SPN para un clúster de SQL Server, debe especificar el nombre virtual del clúster de SQL Server como el nombre del equipo de SQL Server.  

    -   Para crear un SPN para el nombre NetBIOS del equipo de SQL Server, escriba el comando siguiente: **setspn –A MSSQLSvc/&lt;nombre de equipo de SQL Server\>:1433 &lt;Dominio\Cuenta**  

    -   Para crear un SPN para el FQDN del equipo de SQL Server, escriba el comando siguiente: **setspn –A MSSQLSvc/&lt;FQDN de SQL Server\>:1433 &lt;dominio\cuenta>**  

    > [!NOTE]  
    >  El comando para registrar un SPN para una instancia con nombre de SQL Server es el mismo que se utiliza para registrar un SPN para instancia predeterminada, excepto en que el número de puerto debe coincidir con el puerto utilizado por la instancia con nombre.  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-by-using-the-setspn-command"></a>Para comprobar si el SPN de usuario de dominio está registrado correctamente mediante el comando Setspn  

1.  En el menú **Inicio** , haga clic en **Ejecutar**y, a continuación, escriba **cmd** en el cuadro de diálogo **Ejecutar** .  

2.  En el símbolo del sistema, escriba el siguiente comando: **setspn –L &lt;dominio\cuenta de servicio de SQL>**.  

3.  Revise el **ServicePrincipalName** registrado para asegurarse de que se ha creado un SPN válido para el SQL Server.  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-when-using-the-adsiedit-mmc-console"></a>Para comprobar que el SPN del usuario de dominio está registrado correctamente cuando se utiliza la consola de MMC ADSIEdit  

1.  En el menú **Inicio** , haga clic en **Ejecutar**y, a continuación, escriba **adsiedit.msc** para iniciar la consola de ADSIEdit MMC.  

2.  Si es necesario, conéctese al dominio del servidor de sitio.  

3.  En el panel de consola, expanda el dominio del servidor de sitio, expanda **DC=&lt;nombre distintivo del servidor\>**, expanda **CN=Users**, haga clic con el botón derecho en **CN=&lt;usuario de cuenta de servicio\>** y, a continuación, haga clic en **Propiedades**.  

4.  En el cuadro de diálogo **CN=&lt;usuario de cuenta de servicio\> Propiedades**, revise el valor **servicePrincipalName** para asegurarse de que se ha creado un SPN válido y que se ha asociado con el equipo de SQL Server correcto.  

#### <a name="to-change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>Para cambiar la cuenta de servicio de SQL Server de sistema local a una cuenta de usuario de dominio  

1.  Cree o seleccione una cuenta de usuario de sistema local o de dominio que desee utilizar como cuenta de servicio de SQL Server.  

2.  Abra **Administrador de configuración de SQL Server**.  

3.  Haga clic en **Servicios de SQL Server** y, a continuación, haga doble clic en **SQL Server&lt;NOMBRE DE INSTANCIA\>**.  

4.  En la pestaña **Iniciar sesión** , seleccione **Esta cuenta**y, a continuación, escriba el nombre de usuario y la contraseña de la cuenta de usuario de dominio creada en el paso 1, o haga clic en **Examinar** para buscar la cuenta de usuario en Servicios de dominio de Active Directory y, a continuación, haga clic en **Aplicar**.  

5.  Haga clic en **Sí** en el cuadro de diálogo **Confirmar cambio de cuenta** para confirmar el cambio de cuenta de servicio y reiniciar el servicio de SQL Server.  

6.  Haga clic en **OK** después de que se haya cambiado correctamente la cuenta de servicio.  

##  <a name="a-namebkmkreseta-run-a-site-reset"></a><a name="bkmk_reset"></a> Ejecutar un restablecimiento de sitio  
 Cuando se ejecuta un restablecimiento de sitio en un sitio de administración central o un sitio primario, el sitio:  

-   Vuelve a aplicar los permisos de registro y archivo de Configuration Manager predeterminados.  

-   Reinstala en el sitio todos los componentes del sitio y todos roles del sistema de sitio.  

Los sitios secundarios no son compatibles con el restablecimiento de sitio.  

Los restablecimientos de sitio se pueden ejecutar manualmente, si elige esta opción, pero también pueden ejecutarse automáticamente después de modificar la configuración del sitio.  

Por ejemplo, si se produjo un cambio en las cuentas usadas por los componentes de Configuration Manager, considere un restablecimiento de sitio manual para garantizar que los componentes del sitio se actualicen para usar los nuevos detalles de cuenta. No obstante, si modifica los idiomas de cliente o servidor en un sitio, Configuration Manager ejecuta automáticamente un restablecimiento de sitio porque es necesario para que un sitio pueda usar este cambio.  

> [!NOTE]  
>  Un restablecimiento de sitio no restablece los permisos de acceso a objetos externos de Configuration Manager.  

Cuando se ejecuta un restablecimiento de sitio:  

1.  El programa de instalación se detiene y reinicia el servicio **SMS_SITE_COMPONENT_MANAGER** y los componentes de subproceso del servicio **SMS_EXECUTIVE** .  

2.  El programa de instalación quita y, a continuación, vuelve a crear la carpeta de recurso compartido de sistema de sitio y el componente **SMS Executive** en el equipo local y en los equipos de sistema de sitio remoto.  

3.  El programa de instalación reinicia el servicio **SMS_SITE_COMPONENT_MANAGER** . Este servicio instala los servicios **SMS_EXECUTIVE** y **SMS_SQL_MONITOR** .  

Además, un restablecimiento de sitio restaura los objetos siguientes:  

-   Las claves del Registro **SMS** o **NAL** y todas las subclaves predeterminadas bajo estas claves.  

-   El árbol de directorio de archivos de Configuration Manager y los archivos o subdirectorios predeterminados en este árbol de directorio de archivos.  

**Requisitos previos para ejecutar un restablecimiento de sitio**  

La cuenta que utiliza para realizar un restablecimiento de sitio debe tener los permisos siguientes:  

-   La cuenta que utiliza para realizar un restablecimiento de sitio debe tener los permisos siguientes:  

    -   **Sitio de administración central**: la cuenta que usa para ejecutar un restablecimiento de sitio en este sitio debe ser una cuenta de administrador local en el servidor de sitio de administración central y debe tener privilegios equivalentes a los del rol de seguridad de administración basada en roles **Administrador total** .  

    -   **Sitio primario**: la cuenta que usa para ejecutar un restablecimiento de sitio en este sitio debe ser una cuenta de administrador local en el servidor de sitio primario y debe tener privilegios equivalentes a los del rol de seguridad de administración basada en roles **Administrador total** . Si el sitio primario está en una jerarquía con un sitio de administración central, esta cuenta también debe ser un administrador local en el servidor de sitio de administración central.  

**Limitaciones para un restablecimiento del sitio**
  - A partir de la versión 1602, no puede usar un restablecimiento del sitio para cambiar el paquete de idioma de servidor o cliente que instaló en los sitios siempre que la jerarquía esté configurada para admitir la [prueba de actualizaciones de cliente en una recopilación de preproducción](/sccm/core/clients/manage/upgrade/test-client-upgrades).

#### <a name="to-perform-a-site-reset"></a>Para realizar un restablecimiento de sitio  

1.  Ejecute el **programa de instalación de Configuration Manager** desde la **&lt;carpeta de instalación del sitio de Configuration Manager\>\BIN\X64\setup.exe**.  

    > [!TIP]  
    >  Para ejecutar un restablecimiento del sitio, también puede iniciar el programa de instalación de Configuration Manager en el menú **Inicio** del equipo del servidor de sitio o desde los medios de origen de Configuration Manager.  

2.  En la página **Primeros pasos** , seleccione **Realizar mantenimiento de sitio o restablecer este sitio**y, a continuación, haga clic en **Siguiente**.  

3.  En la página **Mantenimiento del sitio** , seleccione **Restablecer el sitio sin cambios de configuración**y, a continuación, haga clic en **Siguiente**.  

4.  Haga clic en **Sí** para iniciar el restablecimiento del sitio.  

Cuando el restablecimiento del sitio haya finalizado, haga clic en **Cerrar** para completar este procedimiento.  

##  <a name="a-namebkmksitelanga-manage-language-packs-at-a-site"></a><a name="bkmk_sitelang"></a> Administración de paquetes de idioma en un sitio  
Después de instalar un sitio, puede cambiar los paquetes de idioma de servidor y cliente que se usan:  

**Paquetes de idioma de servidor:**  

-   **Se aplica a:**  

     Instalaciones de la consola de Configuration Manager  

     Nuevas instalaciones de roles de sistema de sitio aplicables  

-   **Detalles:**  

     Después de actualizar los paquetes de idioma de servidor en un sitio, puede agregar compatibilidad para los paquetes de idioma en consolas de Configuration Manager.  

     Para agregar compatibilidad para un determinado paquete de idioma de servidor en una consola de Configuration Manager, debe instalar la consola de Configuration Manager desde la carpeta **ConsoleSetup** en un servidor de sitio que incluye el paquete de idioma que desea usar. Si la consola de Configuration Manager ya está instalada, desinstálela para permitir que la nueva instalación identifique la lista actual de paquetes de idioma admitidos.  

**Paquetes de idioma del cliente:**  

-   **Se aplica a:**  

     Los cambios en los paquetes de idioma de cliente actualizan los archivos de origen de instalación de cliente para que las nuevas instalaciones y actualizaciones del cliente agreguen compatibilidad con la lista actualizada de idiomas de cliente.  

-   **Detalles:**  

     Después de actualizar los paquetes de idioma de cliente en un sitio, debe instalar cada cliente que usará los paquetes de idioma mediante los archivos de origen que incluyen los paquetes de idioma de cliente.  

Para obtener más información acerca de los idiomas de cliente y servidor que son compatibles con Configuration Manager, consulte [Language Packs in System Center Configuration Manager](../../../core/servers/deploy/install/language-packs.md) (Paquetes de idioma en System Center Configuration Manager).  

#### <a name="to-modify-the-language-packs-that-are-supported-at-a-site"></a>Para modificar los paquetes de idioma que se admiten en un sitio  

1.  En el servidor de sitio, ejecute el programa de instalación de Configuration Manager en **&lt;Carpeta de instalación de sitio de Configuration Manager\>\BIN\X64\setup.exe.**  

2.  En la página **Primeros pasos** , seleccione **Realizar mantenimiento de sitio o restablecer este sitio**y, a continuación, haga clic en **Siguiente**.  

3.  En la página **Mantenimiento del sitio** , seleccione **Modificar la configuración de idioma**y, a continuación, haga clic en **Siguiente**.  

4.  En la página de **Descargas de requisitos previos** , seleccione **Descargar archivos requeridos** para obtener las actualizaciones de los paquetes de idioma, o seleccione **Usar archivos descargados anteriormente** para usar archivos descargados anteriormente que incluyen los paquetes de idioma que desea agregar al sitio. Haga clic en **Siguiente** para validar los archivos y continuar.  

5.  En la página **Selección de idioma de servidor** , active las casillas de los idiomas de servidor admitidos por el sitio y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Selección de idioma de cliente** , active las casillas de los idiomas de cliente admitidos por el sitio y, a continuación, haga clic en **Siguiente**.  

7.  Haga clic en **Siguiente**, para modificar la compatibilidad de idioma en el sitio.  

    > [!NOTE]  
    >  Configuration Manager inicia un restablecimiento del sitio. Este proceso vuelve a instalar todos los roles de sistema de sitio en el sitio.  

8.  Haga clic en **Cerrar** para completar este procedimiento.  

##  <a name="a-namebkmkmoddbalerta-modify-the-database-server-alert-threshold"></a><a name="BKMK_ModDBAlert"></a> Modificación del umbral de alerta del servidor de bases de datos  
 De forma predeterminada, Configuration Manager genera alertas cuando en un servidor de base de datos de sitio queda poco espacio libre en disco. De forma predeterminada, se genera una advertencia cuando el espacio libre en disco es 10 GB o menor, y una alerta crítica cuando el espacio libre en disco es 5 GB o menor. Puede modificar estos valores o deshabilitar las alertas para cada sitio.  

 Para cambiar esta configuración:  

1.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.  

2.  Seleccione el sitio que desea configurar y abra las **Propiedades**de ese sitio.  

3.  En el cuadro de diálogo **Propiedades** del sitio, seleccione la pestaña **Alerta** y, a continuación, edite la configuración.  

4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo de propiedades del sitio.  



<!--HONumber=Dec16_HO3-->


