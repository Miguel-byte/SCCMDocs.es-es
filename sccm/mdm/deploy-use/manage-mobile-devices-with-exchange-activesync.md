---
title: "Administrar dispositivos móviles | Microsoft Docs"
description: "Administre dispositivos móviles mediante el conector de Exchange Server en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
caps.latest.revision: 8
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0d6479bcc134103e6005159a8ea295a5f359a436
ms.openlocfilehash: 4a2b60d893e8d430b107a5bc43ec0748177c27c3


---
# <a name="manage-mobile-devices-with-system-center-configuration-manager-and-exchange"></a>Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange

*Se aplica a: System Center Configuration Manager (Rama actual)*

Utilice el conector de Exchange Server en System Center Configuration Manager si desea administrar dispositivos móviles que se conectan a Exchange Server (de forma local o en línea) mediante el protocolo Microsoft Exchange ActiveSync, y no puede inscribirlos a través de Configuration Manager. Puede configurar las características de administración de dispositivos móviles de Exchange, como la eliminación remota de datos del dispositivo móvil y el control de configuración para varios servidores de Exchange, desde la consola de Configuration Manager.  

 ![configmgr&#45;with&#45;exchange](../../mdm/deploy-use/media/configmgr-with-exchange.png "configmgr-with-exchange")  

 Cuando administra dispositivos móviles mediante el conector de Exchange Server, no se instala el cliente de Configuration Manager en los dispositivos móviles. Por lo tanto, se limitan algunas funciones de administración. Por ejemplo, no se puede instalar software en estos dispositivos ni utilizar elementos de configuración para configurarlos. Para obtener más información acerca de las diferentes funciones de administración que puede usar con Configuration Manager para dispositivos móviles, consulte [Choose a device management solution for System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md) (Selección de una solución de administración de dispositivos para System Center Configuration Manager).  

> [!IMPORTANT]  
>  Antes de instalar el conector de Exchange Server, confirme que Configuration Manager es compatible con la versión de Microsoft Exchange que está usando. Para más información, consulte "Exchange Server connector" (Conector de Exchange Server) en [Supported operating systems for sites and clients for System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers) (Sistemas operativos admitidos para sitios y clientes para System Center Configuration Manager).  

 Si usa el conector de Exchange Server, los dispositivos móviles pueden administrarse mediante la configuración que establezca en Configuration Manager en lugar de mediante las directivas de buzones predeterminadas de Exchange ActiveSync. Defina la configuración que quiere usar en las configuraciones de grupo siguientes: **General**, **Contraseña**, **Administración de correo electrónico**, **Seguridad**y **Aplicación**. Por ejemplo, en la configuración de grupo **Contraseña** , puede configurar que los dispositivos móviles requieran una contraseña, su longitud mínima, su complejidad y si se permite la recuperación de contraseñas.  

 Cuando se configura al menos una opción en el grupo, Configuration Manager administra toda la configuración del grupo para dispositivos móviles. Si no configura ninguna opción en un grupo, Exchange sigue administrando los dispositivos móviles para esas opciones de configuración. Igualmente, se seguirá aplicando toda directiva de buzón de Exchange ActiveSync que se haya configurado en Exchange Server y se haya asignado a los usuarios.  

 También puede configurar el conector de Exchange Server para administrar las reglas de acceso de Exchange y permitir, bloquear o poner en cuarentena dispositivos móviles. Puede borrar de forma remota dispositivos móviles mediante la consola de Configuration Manager, y los usuarios pueden borrar sus dispositivos móviles de forma remota a través del catálogo de aplicaciones.  

 El dispositivo móvil de un usuario aparece automáticamente en el catálogo de aplicaciones cuando el conector de Exchange Server lo administra y Exchange Server está instalado de forma local. Cuando se configura el conector de Exchange Server para Microsoft Exchange Online, se debe configurar manualmente la afinidad de dispositivo de usuario para que el dispositivo móvil del usuario aparezca en el catálogo de aplicaciones. Para obtener más información sobre la afinidad entre usuario y dispositivo, consulte [Link users and devices with user device affinity in System Center Configuration Manager](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) (Vinculación de usuarios y dispositivos con afinidad entre usuario y dispositivo en System Center Configuration Manager).  

> [!TIP]  
>  Si administra un dispositivo móvil mediante el conector de Exchange Server y el dispositivo móvil se transfiere a otro usuario, elimine el dispositivo móvil de la consola de Configuration Manager antes de que el nuevo propietario del dispositivo móvil configure su cuenta de Exchange en el dispositivo móvil transferido.  

## <a name="required-security-permissions"></a>Permisos de seguridad requeridos  
 Debe tener los permisos de seguridad siguientes para configurar el conector de Exchange Server:  

-   Para agregar, modificar y eliminar el conector de Exchange Server: permiso **Modificar** para el objeto **Sitio** .  

-   Para establecer la configuración del dispositivo móvil: permiso **ModifyConnectorPolicy** para el objeto **Sitio** .  

 El rol de seguridad **Administrador total** incluye los permisos necesarios para configurar el conector de Exchange Server.  

 Debe tener los siguientes permisos de seguridad para administrar los dispositivos móviles:  

-   Para borrar un dispositivo móvil: **Eliminar recurso** para el objeto **Recopilación** .  

-   Para cancelar un comando de borrado: **Modificar recurso** para el objeto **Recopilación** .  

-   Para permitir y bloquear dispositivos móviles: **Modificar recurso** para el objeto **Colección** .  

 El rol de seguridad **Administrador de operaciones** incluye los permisos necesarios para administrar dispositivos móviles mediante el conector de Exchange Server.  

 Para obtener más información acerca de cómo configurar permisos de seguridad, consulte [Configure role-based administration for System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) (Configurar administración basada en roles para System Center Configuration Manager).  

## <a name="installing-and-configuring-an-exchange-server-connector"></a>Instalar y configurar un conector de Exchange Server  
 Utilice el siguiente procedimiento para instalar y configurar un conector de Exchange Server para administrar dispositivos móviles. Configuration Manager solo admite un conector en una organización de Exchange. Una vez completados estos pasos, puede ver las recopilaciones que muestran los dispositivos móviles y utilizar los informes para dispositivos móviles para supervisar los dispositivos móviles encontrados y administrados por el conector.  

> [!NOTE]  
>  Configuration Manager genera nombres para los dispositivos móviles que encuentra empleando el formato *nombreDeUsuario*_*tipoDeDispositivo*. Si un usuario tiene más de un dispositivo móvil con el mismo tipo de dispositivo, Configuration Manager muestra el mismo nombre para estos dispositivos móviles en la consola y en los informes.  

#### <a name="to-install-and-configure-an-exchange-server-connector"></a>Para instalar y configurar un conector de Exchange Server  

1.  Decida qué cuenta se conectará al servidor de acceso de cliente Exchange para administrar los dispositivos móviles. La cuenta puede ser la cuenta de equipo del servidor de sitio o una cuenta de usuario de Windows. A continuación, configure esta cuenta para que ejecute los siguientes cmdlets de Exchange Server:  

    -   **Clear-ActiveSyncDevice**  

    -   **Get-ActiveSyncDevice**  

    -   **Get-ActiveSyncDeviceAccessRule**  

    -   **Get-ActiveSyncDeviceStatistics**  

    -   **Get-ActiveSyncMailboxPolicy**  

    -   **Get-ActiveSyncOrganizationSettings**  

    -   **Get-ExchangeServer**  

    -   **Get-Recipient**  

    -   **Set-ADServerSettings**  

    -   **Set-ActiveSyncDeviceAccessRule**  

    -   **Set-ActiveSyncMailboxPolicy**  

    -   **Set-CASMailbox**  

    -   **New-ActiveSyncDeviceAccessRule**  

    -   **New-ActiveSyncMailboxPolicy**  

    -   **Remove-ActiveSyncDevice**  

    > [!NOTE]  
    >  Los siguientes roles de administración de Exchange Server incluyen estos cmdlets: Administración de destinatarios, Administración de organización de solo lectura y Administración de servidores. Para obtener más información acerca de grupos de roles de administración en Microsoft Exchange Server 2010, consulte [Descripción de los grupos de funciones de administración](http://go.microsoft.com/fwlink/p/?LinkId=212914).  

    > [!TIP]  
    >  Si intenta instalar o usar el conector de Exchange Server sin los cmdlets necesarios, verá un error con el mensaje `Invoking cmdlet <cmdlet> failed` en el archivo de registro EasDisc.log en el equipo de servidor de sitio.  

2.  En la consola de Configuration Manager, haga clic en **Administración**.  

3.  En el área de trabajo **Administración** , expanda **Configuración de jerarquía**y, a continuación, haga clic en **Conectores de Exchange Server**.  

4.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Agregar servidor Exchange Server**.  

5.  Complete el Asistente para agregar servidor Exchange Server:  

    -   Si utiliza una instancia local de Exchange Server y especifica un servidor de acceso de cliente, puede especificar un solo servidor o una matriz de servidores de acceso de cliente para cada sitio de Active Directory. Si el servidor o la matriz están desconectados, Configuration Manager intentará detectar un servidor de acceso de cliente para usarlo. Si esta opción no produce el resultado esperado, Configuration Manager recurrirá al uso de un servidor de buzones de correo para realizar una conexión con el servidor de acceso de cliente. Los reintentos se registran como advertencias en el archivo EasDisc.log en el equipo de servidor de sitio. Por ejemplo, busque `Failed to open runspace for site <site_name>`.  

    -   Para la cuenta de conector de Exchange Server, especifique la cuenta que configuró en el paso 1.  

    -   Si también inscribe dispositivos móviles mediante Configuration Manager, habilite la opción **Administración de dispositivos móviles externos** para asegurarse de que estos dispositivos móviles sigan recibiendo el correo electrónico de Exchange después de que Configuration Manager los inscriba.  

    -   En la página **Cuenta** del asistente, puede configurar la cuenta usada para enviar notificaciones por correo electrónico a los clientes que están bloqueados por el acceso condicional de Configuration Manager. La cuenta especificada debe tener un buzón válido en el servidor de Exchange.  

         Para obtener más información, vea [Manage access to services in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md) (Administración del acceso a servicios en System Center Configuration Manager).  

6.  Puede comprobar la instalación del conector de Exchange Server mediante mensajes de estado y revisando los archivos de registro:  

    -   Para confirmar que el administrador de componentes de sitio haya instalado correctamente el conector de Exchange Server, busque el Id. de estado **1015** para el componente **SMS_EXCHANGE_CONNECTOR** . Si Configuration Manager no puede instalar correctamente el conector (por ejemplo, porque el equipo de servidor de acceso de cliente está desconectado), Configuration Manager reintenta la instalación cada 60 minutos hasta que la instalación finaliza correctamente o se quita el conector de Exchange Server.  

    -   En el equipo del servidor de sitio, busque el archivo SiteComp.log y, a continuación, en el archivo de registro, busque `Component SMS_EXCHANGE_CONNECTOR flagged for installation`. Una instalación correcta se registra con el texto siguiente: `STATMSG: ID=1015`.  



<!--HONumber=Dec16_HO3-->


