---
title: Administrar clientes | Microsoft Docs
description: Aprenda a administrar clientes en System Center Configuration Manager.
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
caps.latest.revision: 17
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 238ef5814c0c1b832c28d63c9f3879e21a6c439b
ms.openlocfilehash: dfdb5a95b672d3858d094750625cb5f6ef50700d


---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>Cómo administrar clientes en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Cuando un cliente de System Center Configuration Manager se instala y se asigna correctamente a un sitio de Configuration Manager, podrá ver el dispositivo en el área de trabajo **Activos y compatibilidad** en el nodo **Dispositivos** y en una o varias colecciones del nodo **Recopilaciones de dispositivos**. Al seleccionar el dispositivo o la recopilación que contiene el dispositivo, puede seleccionar varias operaciones de administración. Sin embargo, existen también otras formas de administrar el cliente, que pueden involucrar otras áreas de trabajo de la consola o tareas que no usan la consola de Configuration Manager.  

 Use este tema para obtener información general de las tareas que puede administrar un cliente de Configuration Manager desde el área de trabajo **Activos y compatibilidad**, así como información más detallada acerca de tareas adicionales que le ayudarán a administrar el cliente de Configuration Manager. Para obtener más información acerca de cómo configurar el cliente, consulte [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md) (Configuración del cliente en System Center Configuration Manager).  

> [!NOTE]  
>  Podría ocurrir que un cliente de Configuration Manager estuviera instalado pero no se mostrase en la consola de Configuration Manager. Este escenario puede producirse si el cliente aún no se asignó correctamente a un sitio, si hay que actualizar la consola o si hay que actualizar la pertenencia a una recopilación.  
>   
>  Además, un dispositivo también puede mostrarse en la consola cuando el cliente de Configuration Manager no está instalado. Este escenario puede producirse si se detecta el dispositivo, pero el cliente de Configuration Manager no está instalado ni asignado. Los dispositivos móviles que se administran mediante el conector de Exchange Server no instalan el cliente de Configuration Manager. Además, los dispositivos que se inscriben por Microsoft Intune no instalan el cliente de Configuration Manager.  
>   
>  Use la columna **Cliente** en la consola de Configuration Manager para determinar si el cliente de Configuration Manager está instalado, de forma que pueda administrarlo desde la consola de Configuration Manager.  

##  <a name="a-namebkmkmanagingclientsdevicesnodea-manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a> Administrar clientes desde el nodo Dispositivos  
 Use el siguiente procedimiento y la tabla para administrar uno o varios dispositivos desde el nodo **Dispositivos** en el área de trabajo **Activos y compatibilidad** .  

> [!IMPORTANT]  
>  Dependiendo del tipo de dispositivo, es posible que algunas de estas opciones no estén disponibles.  

#### <a name="to-manage-clients-from-the-devices-node"></a>Para administrar clientes desde el nodo Dispositivos  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Dispositivos**.  

3.  Seleccione uno o más dispositivos y, a continuación, seleccione una de las tareas de administración de cliente disponibles en la cinta o haga clic con el botón derecho en el dispositivo:  

    -   **Administrar la información de afinidad de dispositivo de usuario**  

         Le permite configurar las asociaciones entre usuarios y dispositivos, lo que permite implementar eficazmente software para los usuarios.  

         Consulte [Link users and devices with user device affinity in System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) (Vinculación de usuarios y dispositivos con afinidad entre usuario y dispositivo en System Center Configuration Manager).  

    -   **Agregar el dispositivo a una recopilación nueva o existente**  

         Utilice estas acciones relacionadas con la recopilación para agregar rápidamente el dispositivo seleccionado a una recopilación mediante una regla directa.  

         [Operaciones y mantenimiento de colecciones en System Center Configuration Manager](../../../core/clients/manage/collections/operations-and-maintenance-for-collections.md)  

    -   **Instalar y volver a instalar el cliente mediante el asistente Inserción del cliente**  

         El Asistente para inserción del cliente ofrece un modo eficaz de instalar y volver a instalar el cliente de Configuration Manager para repararlo o volver a configurarlo en equipos que ejecuten Windows con opciones de configuración de sitio y con las propiedades de client.msi adicionales que haya especificado para la instalación de inserción de cliente.  

        > [!TIP]  
        >  Hay muchas maneras diferentes de instalar (y volver a instalar) el cliente de Configuration Manager. Aunque el asistente Inserción del cliente ofrezca un método de instalación de cliente conveniente, porque puede ejecutarlo desde la consola, este método tiene muchas dependencias y no es adecuado para todos los entornos. Si no puede instalar correctamente el cliente mediante la inserción del cliente, existen muchos otros métodos de instalación de cliente que puede utilizar. Para obtener más información sobre las dependencias, consulte [Prerequisites for deploying clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) (Requisitos previos para la implementación de clientes en equipos Windows con System Center Configuration Manager). Para más información sobre los diferentes métodos de instalación de cliente, consulte [Client installation methods in System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md) (Métodos de instalación de cliente en System Center Configuration Manager).  

         Consulte [Instalación de clientes de Configuration Manager mediante la inserción de cliente](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

    -   **Reasignar el sitio**  

         Reasigne uno o más clientes, incluidos dispositivos móviles administrados, a otro sitio primario en la jerarquía. Los clientes pueden reasignarse individualmente o pueden ser seleccionados en grupo y reasignarse a un sitio nuevo.  

    -   **Administrar de forma remota el cliente**  

         Puede ejecutar el Explorador de recursos para ver información del inventario de hardware y software desde un cliente de Windows y administrarlo de forma remota mediante Control remoto, Asistencia remota y Escritorio remoto.  

         Consulte [How to use Resource Explorer to view hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) (Uso del Explorador de recursos para ver inventario de hardware en System Center Configuration Manager) y [How to use Resource Explorer to view software inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) (Uso del Explorador de recursos para ver inventario de software en System Center Configuration Manager).  

         Consulte [How to remotely administer a Windows client computer by using System Center Configuration Manager](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md) (Administración remota de un equipo cliente de Windows mediante System Center Configuration Manager).  

    -   **Aprobar un cliente**  

         Cuando el cliente se comunica con los sistemas de sitio mediante HTTP y un certificado autofirmado, debe aprobar estos clientes para identificarlos como equipos de confianza. De forma predeterminada, la configuración del sitio aprueba automáticamente los clientes del mismo bosque de Active Directory y los bosques de confianza, por lo que no es necesario aprobar manualmente cada cliente. Sin embargo, debe aprobar manualmente los equipos del grupo de trabajo de confianza y cualquier otro equipo de confianza que no estén aprobados.  

        > [!WARNING]  
        >  Aunque algunas funciones de administración puedan funcionar para los clientes no aprobados, este es un escenario no compatible para Configuration Manager.  

         No tiene que aprobar clientes que se comunican siempre con sistemas de sitio mediante HTTPS en lugar de HTTP, o clientes que usan un certificado PKI al comunicarse con sistemas de sitio mediante HTTP. Estos clientes establecen confianza con Configuration Manager mediante el uso de los certificados PKI.  

    -   **Bloquear o desbloquear un cliente**  

         Bloquee un cliente que ya no sea de confianza para evitar que reciba directiva de cliente e impedir que los sistemas de sitio de Configuration Manager se comuniquen con él.  

        > [!WARNING]  
        >  El bloqueo de un cliente solo impide la comunicación del cliente con sistemas de sitio de Configuration Manager y no evita la comunicación con otros dispositivos. Asimismo, cuando el cliente se comunica con sistemas de sitio mediante HTTP en lugar de HTTPS, existen algunas limitaciones de seguridad.  

         Si más adelante cambia de opinión, puede desbloquear un cliente bloqueado. No obstante, si desbloquea un equipo basado en Intel AMT aprovisionado para AMT cuando se bloqueó, debe realizar otras acciones antes de poder administrar el equipo de nuevo fuera de banda.  

         Consulte [Determine whether to block clients in System Center Configuration Manager](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md) (Determinación del bloqueo de clientes en System Center Configuration Manager).  

    -   **Desactivar una implementación de PXE necesaria**  

         Utilice esta opción para volver a implementar todas las implementaciones de PXE necesarias para el equipo seleccionado.  

         Consulte [Use PXE to deploy Windows over the network with System Center Configuration Manager](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Uso de PXE para implementar Windows a través de la red con System Center Configuration Manager).  

    -   **Administrar las propiedades del cliente**  

         Puede ver las implementaciones y los datos de detección destinados al cliente. También puede configurar las variables que utilizan las secuencias de tareas para implementar un sistema operativo en el dispositivo.  

    -   **Eliminar el cliente**  

        > [!WARNING]  
        >  No elimine un cliente si desea desinstalar el cliente de Configuration Manager o quitarlo de una recopilación.  

         La acción **Eliminar** elimina manualmente el registro del cliente de la base de datos de Configuration Manager y, normalmente, no debe usar esta acción a menos que deba resolver un problema. Si elimina el registro del cliente y el cliente de Configuration Manager sigue instalado y comunicándose con Configuration Manager, Detección de latido volverá a crear el registro de cliente y este volverá a aparecer en la consola de Configuration Manager, aunque se perderá el historial del cliente y todas las asociaciones anteriores.  

        > [!NOTE]  
        >  Cuando elimina un cliente de dispositivo móvil inscrito por Configuration Manager, esta acción también revoca el certificado PKI emitido para el dispositivo móvil. El punto de administración rechaza este certificado, aunque IIS no compruebe la CRL. Cuando elimina estos clientes, no se revocan los certificados en los clientes heredados de dispositivos móviles.  

         Para desinstalar el cliente, consulte [Desinstalar el cliente de Configuration Manager](#BKMK_UninstalClient).  

         Para asignar el cliente a un nuevo sitio primario, consulte [How to assign clients to a site in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md) (Asignación de clientes a un sitio en System Center Configuration Manager).  

         Para quitar el cliente de una recopilación, vuelva a configurar las propiedades de la recopilación. Consulte [How to manage collections in System Center Configuration Manager](../../../core/clients/manage/collections/manage-collections.md) (Administración de recopilaciones en System Center Configuration Manager).  

    -   **Borrar un dispositivo móvil**  

         Puede borrar dispositivos móviles compatibles con el comando de borrado.  

         Esta acción elimina permanentemente todos los datos en el dispositivo móvil, lo que incluye configuración personal y datos personales. Normalmente, esta acción restablece el dispositivo móvil a sus valores predeterminados de fábrica. Borre un dispositivo móvil cuando este ya no sea de confianza; por ejemplo, cuando se haya perdido o haya sido robado.  

        > [!TIP]  
        >  Compruebe la documentación del fabricante para obtener más información acerca de cómo el dispositivo móvil procesa un comando de borrado remoto.  

         Cuando se envía una solicitud de borrado, suele producirse un retraso hasta que el dispositivo móvil recibe el comando de borrado:  

        -   Si el dispositivo móvil está inscrito por Configuration Manager o Windows Intune, el cliente recibe el comando de borrado cuando descarga a continuación su directiva de cliente.  

        -   Si el dispositivo móvil está administrado por el conector de Exchange Server, el dispositivo móvil recibe el comando de borrado cuando se sincroniza después con Exchange.  

         Puede utilizar la columna **Estado de borrado** para supervisar la recepción en el dispositivo móvil del comando de borrado. Hasta que el dispositivo móvil no envíe una confirmación de borrado a Configuration Manager, puede cancelar el comando de borrado.  

    -   **Retirar un dispositivo móvil**  

         La opción **Retirar** solo es compatible con dispositivos móviles que estén inscritos por Windows Intune o la administración de dispositivos móviles local.  

         Para obtener más información, consulte [Help protect your data with remote wipe, remote lock, or passcode reset using System Center Configuration Manager](../../../mdm/deploy-use/wipe-lock-reset-devices.md) (Ayuda a la protección de datos mediante la eliminación remota, el bloqueo remoto o el restablecimiento de código de acceso con System Center Configuration Manager).  

    -   **Cambiar la propiedad de un dispositivo**  

         Puede cambiar la propiedad de dispositivos a **Compañía** o **Personal** si un dispositivo no se ha unido a un dominio y no tiene el cliente Configuration Manager instalado.  

         Puede utilizar este valor en requisitos de aplicaciones para controlar las implementaciones y también puede usar esta configuración para controlar la cantidad de inventario que se recopila de los dispositivos de los usuarios.  

        Para ver el valor de propiedad en la lista de dispositivos, puede que necesite agregar la columna a la vista haciendo clic en cualquier encabezado de columna y elegir **Propietario del dispositivo**.

         Para obtener más información, consulte [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md) (Administración híbrida de dispositivos móviles [MDM] con System Center Configuration Manager y Microsoft Intune)  

##  <a name="a-namebkmkmanagingclientsdevicecollectionsnodea-manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Administrar clientes desde el nodo Recopilaciones de dispositivos  
 Use el siguiente procedimiento y la tabla para administrar dispositivos en una recopilación desde el nodo **Recopilaciones de dispositivos** en el área de trabajo **Activos y compatibilidad** .  

 Muchas de las tareas de administración de cliente que realiza al seleccionar un dispositivo o varios desde el nodo **Dispositivos** también se pueden realizar en el nivel de recopilación. Esto tiene una ventaja: la aplicación automática de la tarea de administración en todos los dispositivos válidos de la recopilación. Aunque este pueda ser un método conveniente para administrar varios clientes a la vez, también puede generar muchos paquetes de red y aumentar el uso de CPU en el servidor de sitio.  

 También hay algunas tareas de administración de cliente que solo se pueden realizar en el nivel de la recopilación, que se enumeran en la tabla siguiente.  

 Antes de llevar a cabo tareas de administración de cliente en el nivel de la recopilación, considere el número de dispositivos que hay en la recopilación, si están conectados por conexiones de red de ancho de banda bajo y el tiempo que tardará en completarse la tarea para todos los dispositivos. Cuando lleve a cabo una tarea de administración de cliente, no puede detenerla desde la consola.  

#### <a name="to-manage-clients-from-the-device-collections-node"></a>Para administrar clientes desde el nodo Recopilaciones de dispositivos  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Recopilaciones de dispositivos**.  

3.  Seleccione una recopilación y, a continuación, una de las tareas de administración de cliente disponibles en la cinta o haga clic con el botón derecho en la recopilación:  

    -   **Examinar equipos en busca de malware y descargar archivos de definición de antimalware**  

         Vea [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md) (Endpoint Protection en System Center Configuration Manager).  

    -   **Implementar software, líneas de base de configuración y secuencias de tareas**  

         Para obtener más información acerca de la implementación de líneas de base de configuración y software, consulte lo siguiente:  

        -   [Deploy software updates in System Center Configuration Manager](../../../sum/deploy-use/deploy-software-updates.md) (Administración de actualizaciones de software en System Center Configuration Manager)  

        -   [Plan for and configure compliance settings in System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) (Planeación y configuración de cumplimiento en System Center Configuration Manager)  

    -   **Configurar opciones de administración de energía**  

         Consulte [How to create and apply power plans in System Center Configuration Manager](../../../core/clients/manage/power/create-and-apply-power-plans.md) (Creación y aplicación de planes de energía en System Center Configuration Manager). Los planes de energía solo se pueden usar con equipos que ejecuten Windows.  

    -   **Notificar a los equipos que descarguen la directiva lo antes posible**  

         Use la notificación de cliente para notificar a los clientes de Windows seleccionados que descarguen la directiva de equipo lo antes posible fuera del intervalo de sondeo de la directiva de cliente configurado.  

         Las tareas de notificación de cliente se muestran en el nodo **Operaciones de cliente** del área de trabajo **Supervisión** .  

##  <a name="a-namebkmkclientcachea-configure-the-client-cache-for-configuration-manager-clients"></a><a name="BKMK_ClientCache"></a> Configurar la caché del cliente para clientes de Configuration Manager  
 Puede configurar la ubicación y el espacio en disco que consumen los clientes de Configuration Manager en Windows para almacenar archivos temporales cuando instalan aplicaciones y programas. Las actualizaciones de software también utilizan la caché de cliente, pero estas actualizaciones no están limitadas por el tamaño de caché configurado y siempre tratarán de descargarse en la caché. Puede configurar la caché de cliente al instalar manualmente el cliente de Configuration Manager, al utilizar la instalación de inserción de cliente o después de la instalación del cliente.

En la versión 1606 de Configuration Manager, puede especificar el tamaño de la carpeta de caché mediante la configuración del cliente en la consola de Configuration Manager.   

 La ubicación predeterminada de la caché de cliente de Configuration Manager es %*windir*%\ccmcache y el espacio en disco predeterminado es 5120 MB.  

> [!IMPORTANT]  
>  No cifre la carpeta utilizada para la caché de cliente. Configuration Manager no puede descargar contenido en una carpeta cifrada.  

### <a name="about-client-cache"></a>Acerca de la caché de cliente  

El cliente de Configuration Manager descarga el contenido del software necesario en cuanto recibe la implementación, pero espera el tiempo programado para ejecutar la implementación. Cuando llega el momento programado, el cliente de Configuration Manager comprueba si el contenido está disponible en la caché. En su caso, y siempre que se trate de la versión correcta, el cliente siempre utiliza el contenido almacenado en caché. No obstante, si ha cambiado la versión requerida del contenido o si éste se ha eliminado con la intención de dejar espacio para otro paquete, el contenido se vuelve a descargar en la caché.  

Si el cliente trata de descargar el contenido de un programa o aplicación cuyo tamaño es mayor que el de la caché, se produce un error de implementación debido a la falta de espacio en la caché y, en consecuencia, Configuration Manager genera el identificador de mensaje de estado 10050. En cambio, si el tamaño de la caché se incrementa con posterioridad, el comportamiento para reintentar la descarga difiere en función de si se trata de un programa o una aplicación necesarios:  

-   Para un programa necesario: el cliente no reintenta descargar el contenido automáticamente. Debe volver a implementar el paquete y el programa en el cliente.  
-   Para una aplicación necesaria: habida cuenta de que la implementación de una aplicación se basa en el estado, el cliente reintenta descargar el contenido automáticamente la próxima vez que descarga la directiva de cliente.  

Si el cliente trata de descargar un paquete cuyo tamaño es inferior al de la caché, pero la caché está llena actualmente, se reintentan todas las implementaciones necesarias hasta que la caché disponga de espacio, hasta que se alcanza el tiempo de espera de la descarga o hasta que se alcanza el límite de reintentos para el error de espacio de la caché. Si aumenta el tamaño de la caché más adelante, el cliente de Configuration Manager trata de volver a descargar el paquete durante el próximo intervalo de reintento. El cliente trata de descargar el contenido cada cuatro horas hasta un máximo de 18 intentos.  

El contenido de la caché no se elimina automáticamente, sino que permanece en la caché durante al menos un día después de que el cliente utiliza ese contenido. Si configura las propiedades del paquete con la opción para conservar el contenido de la caché del cliente, el cliente no elimina automáticamente el contenido del paquete de la caché. Si los paquetes descargados en las últimas 24 horas ocupan el espacio de la caché del cliente y el cliente debe descargar paquetes nuevos, puede aumentar el tamaño de la caché del cliente o elegir la opción disponible para eliminar el contenido conservado en la caché.  

 Utilice los procedimientos siguientes para configurar la caché del cliente durante la instalación manual del cliente, o después de instalar el cliente.  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>Para configurar la caché del cliente al instalar los clientes mediante la instalación manual del cliente  

Ejecute el comando CCMSetup.exe desde la ubicación de origen de instalación y especifique las siguientes propiedades necesarias, que han de estar separadas por espacios:  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Para la versión 1606, use la configuración de tamaño de caché disponible en **Configuración de cliente** en la consola de Configuration Manager en lugar de SMSCACHESIZE. Para obtener más información consulte [Client Cache Settings](../../../core/clients/deploy/about-client-settings.md#client-cache-settings) (Configuración de caché de cliente).

Para obtener más información sobre cómo utilizar estas propiedades de línea de comandos para CCMSetup.exe, consulte [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (Acerca de las propiedades de instalación de clientes en System Center Configuration Manager).  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>Para configurar la carpeta de caché de cliente al instalar los clientes mediante la instalación de inserción de cliente  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.  

3.  En la lista **Sitios** , seleccione el sitio para el que va a configurar la instalación de inserción de cliente automática en todo el sitio.  

4.  En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Configuración de instalación de cliente**y, a continuación, haga clic en la pestaña **Propiedades de instalación**.  

5.  En la pestaña **Propiedades de instalación** , especifique las siguientes propiedades necesarias y sepárelas con espacios:  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Para la versión 1606, use la configuración de tamaño de caché disponible en **Configuración de cliente** en la consola de Configuration Manager en lugar de SMSCACHESIZE. Para obtener más información consulte [Client Cache Settings](../../../core/clients/deploy/about-client-settings.md#client-cache-settings) (Configuración de caché de cliente).

       Para obtener más información sobre cómo utilizar estas propiedades de línea de comandos para CCMSetup.exe, consulte [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (Acerca de las propiedades de instalación de clientes en System Center Configuration Manager).  

6.  Haga clic en **Aceptar** para guardar las propiedades especificadas.  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>Para configurar la carpeta de caché de cliente en el equipo del cliente  

1.  En el equipo cliente, vaya a **Configuration Manager** en el Panel de control y, a continuación, haga doble clic para abrir las propiedades.  

2.  Haga clic en la pestaña **Caché** .  

3.  Especifique el espacio en disco para reservarlo para la caché del cliente.  

4.  Para cambiar la ubicación de la carpeta de caché de cliente, haga clic en **Cambiar ubicación**y, a continuación, especifique la nueva ubicación. La ubicación predeterminada es *%windir%*\ccmcache.  

5.  Para eliminar los archivos que están almacenados actualmente en la carpeta de caché de cliente, haga clic en **Eliminar archivos**.  

6.  Haga clic en **Aceptar** para cerrar **Propiedades de Configuration Manager**.  

### <a name="to-configure-client-cache-size-in-client-settings"></a>Para configurar el tamaño de la caché de cliente en la configuración de cliente

A partir de la versión 1606, puede ajustar el tamaño de la carpeta de caché de cliente sin tener que volver a instalar el cliente. Para ello, tiene que configurar el tamaño de la caché de cliente en la consola de Configuration Manager usando la configuración de cliente.  

1. En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente**.

2. Haga doble clic en **Configuración de cliente predeterminada**.
  También puede crear una configuración de cliente personalizada para aplicar el tamaño de caché de forma más selectiva. Para obtener más información acerca de las configuraciones personalizadas y de cliente, consulte [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md) (Configuración del cliente en System Center Configuration Manager).

 3. Haga clic en **Configuración de caché de cliente** y elija **Sí** para **Configurar el tamaño de caché de cliente**.

 4. Ajuste el tamaño máximo de caché usando **MB** o **porcentaje de la configuración del disco**. La memoria caché se ajusta al tamaño que sea menor.

 5. Haga clic en **Aceptar**.

    El cliente de Configuration Manager configurará el tamaño de caché con estos valores cuando se descargue la próxima directiva de cliente.

##  <a name="a-namebkmkuninstalclienta-uninstall-the-configuration-manager-client"></a><a name="BKMK_UninstalClient"></a> Desinstalar el cliente de Configuration Manager  
 Para desinstalar de un equipo con Windows el software cliente de Configuration Manager, use **CCMSetup.exe** con la propiedad **/Uninstall**. Ejecute CCMSetup.exe en un equipo individual desde el símbolo del sistema o implemente un paquete y el programa para desinstalar el cliente de una recopilación de equipos.  

> [!WARNING]  
>  No puede desinstalar al cliente de Configuration Manager desde un dispositivo móvil. Si debe quitar el cliente de Configuration Manager de un dispositivo móvil, debe borrar el dispositivo y, de esta forma, se eliminan todos los datos del dispositivo móvil.  

 Utilice el procedimiento siguiente para desinstalar el cliente de Configuration Manager de los equipos.  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>Para desinstalar el cliente de Configuration Manager desde el símbolo del sistema  

1.  Abra un símbolo del sistema de Windows y cambie la carpeta a la ubicación en la que se encuentra CCMSetup.exe.  

2.  Escriba **Ccmsetup.exe /uninstall**y, a continuación, presione **Entrar**.  

> [!NOTE]  
>  El proceso de desinstalación es silencioso y no muestra ningún resultado en la pantalla. Para comprobar que la desinstalación del cliente se ha realizado correctamente, examine el archivo de registro **CCMSetup.log** en la carpeta *%windir%\ ccmsetup* del equipo cliente.  

##  <a name="a-namebkmkconflictingrecordsa-manage-conflicting-records-for-configuration-manager-clients"></a><a name="BKMK_ConflictingRecords"></a> Administrar registros en conflicto para clientes de Configuration Manager  
 Configuration Manager usa el identificador de hardware para tratar de identificar los clientes que puedan estar duplicados y alertarle así de los registros en conflicto. Por ejemplo, si reinstala un equipo, el identificador de hardware podría ser el mismo, pero el GUID que utiliza Configuration Manager podría cambiar.  

 Si Configuration Manager puede resolver un conflicto mediante la autenticación de Windows de la cuenta del equipo, o un certificado PKI de un origen de confianza, el conflicto se resolverá automáticamente. Sin embargo, si Configuration Manager no puede resolver el conflicto, utilizará una configuración de jerarquía que, bien combina automáticamente los registros cuando detecta identificadores de hardware duplicados (configuración predeterminada), o bien permite al usuario decidir cuando combinar, bloquear o crear registros de cliente nuevos. Si decide administrar los registros duplicados manualmente, tendrá que resolver, también manualmente, los registros en conflicto mediante la consola de Configuration Manager.  


#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>Para cambiar la configuración de la jerarquía a fin de administrar los registros en conflicto  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.  

3.  En el grupo **Sitios** , haga clic en **Configuración de jerarquía**y, a continuación, en la pestaña **Aprobación de cliente y registros conflictivos** .  

4.  Haga clic en **Resolver automáticamente los registros conflictivos** para combinar automáticamente los registros en conflicto, o bien haga clic en **Resolver manualmente los registros conflictivos**y, a continuación, en **Aceptar**.  

    > [!NOTE]  
    >  Si Configuration Manager puede resolver el conflicto con la cuenta del equipo o un certificado PKI, esta configuración se ignora y el conflicto se resuelve automáticamente.  

#### <a name="to-manually-resolve-conflicting-records"></a>Para resolver manualmente los registros en conflicto  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Estado del sistema**y, a continuación, haga clic en **Registros en conflicto**.  

3.  En el panel de resultados, seleccione uno o más registros en conflicto y, a continuación, haga clic en **Registros en conflicto**.  

4.  En el cuadro de diálogo **Registros en conflicto** , seleccione alguna de las siguientes opciones y, a continuación, haga clic en **Aceptar**:  

    -   **Combinar** para combinar el registro recién detectado con el registro de cliente existente, de manera que se crea un registro unificado.  

    -   **Nuevo** para crear un nuevo registro de cliente en conflicto.  

    -   **Bloquear** para crear un nuevo registro de cliente en conflicto, pero se marca como bloqueado.  

## <a name="manage-duplicate-hardware-identifiers"></a>Administrar identificadores de hardware duplicados
A partir de la versión 1610 de Configuration Manager, puede proporcionar una lista de identificadores de hardware que Configuration Manager omitirá en el registro de clientes y el arranque PXE. Esto ayuda a resolver dos problemas comunes.

1. Muchos dispositivos nuevos, como Surface Pro 3, no incluyen un puerto Ethernet integrado. Generalmente se usa un adaptador de USB a Ethernet a fin de establecer una conexión con cable para la implementación del sistema operativo, pero suele tratarse de adaptadores compartidos debido a su costo y su facilidad de uso general. Dado que la dirección MAC de este adaptador se usa para identificar el dispositivo, resulta problemático reutilizar el adaptador sin no se llevan a cabo acciones de administrador adicionales entre cada implementación. Ahora, en la versión 1610 de Rama actual de Configuration Manager, puede excluir la dirección MAC de este adaptador para que se puede reutilizar fácilmente en este escenario.
2. A pesar de que se supone que el identificador de SMBIOS es un identificador de hardware único, algunos dispositivos de hardware especiales se crean con identificadores duplicados. Aunque esto no es tan común como el anterior escenario de adaptador de USB a Ethernet, también se puede usar la lista de identificadores de hardware para solucionar este problema.

#### <a name="to-add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Para agregar identificadores de hardware a fin de que Configuration Manager los omita  
1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Configuración del sitio** > **Sitios**.
2. En la pestaña **Inicio** , en el grupo **Sitios** , haga clic en **Configuración de jerarquía**.
3. Vaya a la pestaña **Aprobación de cliente y registros conflictivos**.
4. Haga clic en **Agregar** en la sección **Identificadores de hardware duplicados** para agregar nuevos identificadores de hardware.

##  <a name="a-namebkmkpolicyretrievala-initiate-policy-retrieval-for-a-configuration-manager-client"></a><a name="BKMK_PolicyRetrieval"></a> Iniciar la recuperación de directivas para un cliente de Configuration Manager  
 Un cliente de Configuration Manager en Windows descarga su directiva de cliente en una programación que se configura como una configuración de cliente. Sin embargo, pueden darse casos en que desee iniciar la recuperación de directiva ad-hoc desde el cliente como, por ejemplo, en un escenario de solución de problemas o al realizar pruebas.  

 Utilice los siguientes procedimientos para iniciar la recuperación de directiva ad-hoc de cliente fuera de su intervalo de sondeo programado, bien en la pestaña **Acciones** del cliente de Configuration Manager o mediante la ejecución de un script en el equipo. Debe iniciar sesión en el equipo cliente con derechos administrativos locales para realizar estos procedimientos.  

> [!NOTE]  
>  Puede utilizar la notificación de cliente para iniciar la recuperación de directiva de cliente fuera del intervalo de sondeo de la directiva de cliente programada.  
>   
>  Puede administrar los clientes que ejecutan Linux y UNIX. Para obtener más información sobre la recuperación de directivas de clientes que ejecutan Linux y UNIX, consulte [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU) (Directiva de equipo para servidores de Linux y UNIX).  

#### <a name="to-initiate-client-policy-retrieval-by-using-client-notification"></a>Para iniciar la recuperación de directivas de cliente mediante el uso de notificación de cliente  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Recopilaciones de dispositivos**.  

3.  Seleccione la recopilación de dispositivos que contiene los equipos para los que desea descargar la directiva y, a continuación, en la pestaña **Inicio** , en el grupo **Recopilaciones** , haga clic en **Notificación de cliente** y, a continuación, en **Descargar directiva de equipo**.  

    > [!NOTE]  
    >  También puede utilizar la notificación de cliente para iniciar la recuperación de directiva de uno o varios dispositivos seleccionados mostrados en un nodo de recopilación temporal en el nodo **Dispositivos** .  

#### <a name="to-manually-initiate-client-policy-retrieval-by-using-the-actions-tab-on-the-configuration-manager-client"></a>Para iniciar manualmente la recuperación de directiva de cliente con la utilización de la pestaña Acciones del cliente de Configuration Manager  

1.  Seleccione **Configuration Manager** en el Panel de control del equipo.  

2.  Haga clic en la pestaña **Acciones** .  

3.  Haga clic en **Ciclo de evaluación y recuperación de directivas de equipo** para iniciar la directiva de equipo y, a continuación, haga clic en **Ejecutar ahora**.  

4.  Haga clic en **Aceptar** para confirmar el aviso.  

5.  Repita los pasos 3 y 4 para todas las demás acciones que desee aplicar, como **Ciclo de evaluación y recuperación de directivas de usuario** para la configuración de cliente del usuario.  

6.  Haga clic en **Aceptar** para cerrar **Propiedades de Configuration Manager**.  

#### <a name="to-manually-initiate-client-policy-retrieval-by-using-a-script"></a>Para iniciar manualmente la recuperación de directiva de cliente con un script  

1.  Abra un editor de texto, como el Bloc de notas.  

2.  Copie e inserte lo siguiente en el archivo:  

    ```  
    on error resume next  

    dim oCPAppletMgr 'Control Applet manager object.  
    dim oClientAction 'Individual client action.  
    dim oClientActions 'A collection of client actions.  

    'Get the Control Panel manager object.  
    set  oCPAppletMgr=CreateObject("CPApplet.CPAppletMgr")  
    if err.number <> 0 then  
        Wscript.echo "Couldn't create control panel application manager"  
        WScript.Quit  
    end if  

    'Get a collection of actions.  
    set oClientActions=oCPAppletMgr.GetClientActions  
    if err.number<>0 then  
        wscript.echo "Couldn't get the client actions"  
        set oCPAppletMgr=nothing  
        WScript.Quit  
    end if  

    'Display each client action name and perform it.  
    For Each oClientAction In oClientActions  

        if oClientAction.Name = "Request & Evaluate Machine Policy" then  
            wscript.echo "Performing action " + oClientAction.Name   
            oClientAction.PerformAction  
        end if  
    next  

    set oClientActions=nothing  
    set oCPAppletMgr=nothing  
    ```  

3.  Guarde el archivo con una extensión .vbs.  

4.  En el equipo cliente, ejecute el archivo con alguno de los métodos siguientes:  

    -   Desplácese hasta el archivo en el Explorador de Windows y haga doble clic en el archivo de script.  

    -   Abra un símbolo del sistema y escriba: **cscript &lt;ruta\nombredearchivo.vbs>**.  

5.  Haga clic en **Aceptar** en el cuadro de diálogo **Windows Script Host** .  



<!--HONumber=Dec16_HO3-->


