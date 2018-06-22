---
title: Administración de clientes
titleSuffix: Configuration Manager
description: Aprenda a administrar clientes en System Center Configuration Manager.
ms.date: 12/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 623d7b6a048b7728e40adb3655dc1017408fb1d7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342229"
---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>Cómo administrar clientes en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Cuando el cliente de Configuration Manager se instala y se asigna correctamente a un sitio, puede ver el dispositivo en el área de trabajo **Activos y compatibilidad** del nodo **Dispositivos** y en una o varias recopilaciones del nodo **Recopilaciones de dispositivos**. Cuando selecciona el dispositivo o una recopilación, puede realizar operaciones de administración. Pero existen otras formas de administrar el cliente, que es posible que involucren otras áreas de trabajo de la consola o tareas externas a la consola.  

> [!NOTE]  
>  Si el cliente de Configuration Manager está instalado pero todavía no se ha asignado correctamente a un sitio, es posible que no aparezca en la consola. Después de que el cliente se asigne a un sitio, actualice la pertenencia a la colección y actualice la vista de consola.  
>   
>  Además, un dispositivo también puede mostrarse en la consola cuando el cliente de Configuration Manager no está instalado. Este comportamiento se produce si se detecta el dispositivo, pero el cliente no está instalado ni asignado. 
>
> Los dispositivos móviles que se administran mediante el conector de Exchange Server y los dispositivos inscritos con Microsoft Intune no instalan el cliente de Configuration Manager.  
>   
>  Use la columna **Cliente** de la consola de Configuration Manager para determinar si el cliente está instalado, para que pueda administrarlo desde la consola.  

##  <a name="BKMK_ManagingClients_DevicesNode"></a> Administrar clientes desde el nodo Dispositivos  

Dependiendo del tipo de dispositivo, es posible que algunas de estas opciones no estén disponibles.  

1.  En la consola de Configuration Manager, seleccione **Activos y compatibilidad** >  **Dispositivos**.  

3.  Seleccione uno o más dispositivos y, después, seleccione una de estas tareas de administración de cliente en la cinta de opciones o haga clic con el botón derecho en el dispositivo:  

    -   **Administrar la información de afinidad de dispositivo de usuario**  

         Configure las asociaciones entre usuarios y dispositivos, de manera que pueda implementar de manera eficaz el software a los usuarios.  

         Consulte [Link users and devices with user device affinity in System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) (Vinculación de usuarios y dispositivos con afinidad entre usuario y dispositivo en System Center Configuration Manager).  

    -   **Agregar el dispositivo a una recopilación nueva o existente**  

         Agregue el dispositivo a una recopilación con una regla directa.  

    -   **Instalar y volver a instalar el cliente mediante el asistente Inserción del cliente**  

         Instale y vuelva a instalar el cliente de Configuration Manager para repararlo o volver a configurarlo. Esta opción incluye valores de configuración de sitios y las propiedades client.msi que se establecen para la instalación de inserción del cliente.  

        > [!TIP]  
        >  Hay muchas maneras diferentes de instalar (y volver a instalar) el cliente de Configuration Manager. Aunque el asistente Inserción del cliente ofrezca un método de instalación de cliente conveniente porque puede ejecutarlo desde la consola, este método tiene muchas dependencias y no es adecuado para todos los entornos. Para obtener más información sobre las dependencias, consulte [Prerequisites for deploying clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) (Requisitos previos para la implementación de clientes en equipos Windows con System Center Configuration Manager). Para más información sobre los diferentes métodos de instalación de cliente, consulte [Client installation methods in System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md) (Métodos de instalación de cliente en System Center Configuration Manager).  

         Consulte [Instalación de clientes de Configuration Manager mediante la inserción de cliente](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

    -   **Reasignar el sitio**  

         Reasigne uno o más clientes, incluidos dispositivos móviles administrados, a otro sitio primario en la jerarquía. Los clientes pueden reasignarse individualmente o pueden ser seleccionados en grupo y reasignarse a un sitio nuevo.  

    -   **Administrar de forma remota el cliente**  

         Ejecute el Explorador de recursos para ver la información de inventario de hardware y software de un cliente de Windows. Administre el dispositivo de forma remota mediante Control remoto, Asistencia remota o Escritorio remoto.  

         Vea [Cómo usar el Explorador de recursos para ver el inventario de hardware](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) y [Cómo usar el Explorador de recursos para ver el inventario de software](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

         Vea [Cómo administrar de forma remota un equipo cliente de Windows](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

    -   **Aprobar un cliente**  

         Cuando el cliente se comunica con los sistemas de sitio mediante HTTP y un certificado autofirmado, debe aprobar estos clientes para identificarlos como equipos de confianza. De forma predeterminada, la configuración del sitio aprueba automáticamente los clientes del mismo bosque de Active Directory y los bosques de confianza, por lo que no es necesario aprobar manualmente cada cliente. Pero debe aprobar manualmente los equipos del grupo de trabajo de confianza y cualquier otro equipo de confianza que no esté aprobado.  

        > [!WARNING]  
        >  Aunque algunas funciones de administración puedan funcionar para los clientes no aprobados, este es un escenario no compatible para Configuration Manager.  

         No tiene que aprobar clientes que se comunican siempre con sistemas de sitio mediante HTTPS, o clientes que usan un certificado PKI al comunicarse con sistemas de sitio mediante HTTP. Estos clientes establecen confianza mediante el uso de los certificados PKI.  

    -   **Bloquear o desbloquear un cliente**  

         Bloquee un cliente que ya no sea de confianza. El bloqueo impide que el cliente reciba la directiva y evita que los sistemas de sitio se comuniquen con el cliente.  

        > [!WARNING]  
        >  El bloqueo de un cliente solo impide la comunicación del cliente con sistemas de sitio de Configuration Manager y no evita la comunicación con otros dispositivos. Asimismo, cuando el cliente se comunica con sistemas de sitio mediante HTTP en lugar de HTTPS, existen algunas limitaciones de seguridad.  

         También puede desbloquear a un cliente que está bloqueado. 

         Consulte [Determine whether to block clients in System Center Configuration Manager](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md) (Determinación del bloqueo de clientes en System Center Configuration Manager).  

    -   **Desactivar una implementación de PXE necesaria**  

         Vuelva a implementar implementaciones de PXE necesarias para el equipo.  

         Consulte [Use PXE to deploy Windows over the network with System Center Configuration Manager](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Uso de PXE para implementar Windows a través de la red con System Center Configuration Manager).  

    -   **Administrar las propiedades del cliente**  

         Vea las implementaciones y los datos de detección destinados al cliente. También puede configurar variables que usan las secuencias de tareas para implementar un sistema operativo en el dispositivo.  

    -   **Eliminar el cliente**  

        > [!WARNING]  
        >  No elimine un cliente si desea desinstalar el cliente de Configuration Manager o quitarlo de una recopilación.  

         La acción **Eliminar** elimina manualmente el registro del cliente de la base de datos de Configuration Manager y, normalmente, no debe usar esta acción excepto en escenarios de solución de problemas. Si elimina el registro del cliente pero el cliente sigue estando instalado y se comunica con el sitio, Heartbeat Discovery vuelve a crear el registro del cliente. El registro del cliente vuelve a aparecer en la consola de Configuration Manager, aunque se pierden el historial del cliente y todas las asociaciones anteriores.  

        > [!NOTE]  
        >  Cuando elimina un cliente de dispositivo móvil inscrito por Configuration Manager, esta acción también revoca el certificado PKI emitido para el dispositivo móvil. El punto de administración rechaza este certificado, aunque IIS no compruebe la CRL. Cuando elimina estos clientes, no se revocan los certificados en los clientes heredados de dispositivos móviles.  

         Para desinstalar el cliente, consulte [Desinstalar el cliente de Configuration Manager](#BKMK_UninstalClient).  

         Para asignar el cliente a un nuevo sitio primario, consulte [How to assign clients to a site in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md) (Asignación de clientes a un sitio en System Center Configuration Manager).  

         Para quitar el cliente de una recopilación, vuelva a configurar las propiedades de la recopilación. Consulte [How to manage collections in System Center Configuration Manager](../../../core/clients/manage/collections/manage-collections.md) (Administración de recopilaciones en System Center Configuration Manager).  

    -   **Borrar un dispositivo móvil**  

         Puede borrar dispositivos móviles compatibles con el comando de borrado.  

         Esta acción elimina permanentemente todos los datos en el dispositivo móvil, incluida la configuración personal y los datos personales. Normalmente, esta acción restablece el dispositivo móvil a sus valores predeterminados de fábrica. Borre un dispositivo móvil cuando ya no sea de confianza. Por ejemplo, en caso de pérdida o robo del dispositivo.  

        > [!TIP]  
        >  Compruebe la documentación del fabricante para obtener más información acerca de cómo el dispositivo móvil procesa un comando de borrado remoto.  

         Suele producirse un retraso hasta que el dispositivo móvil recibe el comando de borrado:  

        -   Si el dispositivo móvil está inscrito por Configuration Manager o Microsoft Intune, el cliente recibe el comando cuando descarga su directiva de cliente.  

        -   Si el dispositivo móvil está administrado por el conector de Exchange Server, recibe el comando cuando se sincroniza con Exchange.  

         Puede usar la columna **Estado de borrado** para supervisar la recepción en el dispositivo del comando de borrado. Hasta que el dispositivo no envíe una confirmación de borrado a Configuration Manager, puede cancelar el comando de borrado.  

    -   **Retirar un dispositivo móvil**  

         La opción **Retirar** solo es compatible con dispositivos móviles que estén inscritos por Microsoft Intune o la administración de dispositivos móviles local.  

         Para obtener más información, consulte [Help protect your data with remote wipe, remote lock, or passcode reset using System Center Configuration Manager](../../../mdm/deploy-use/wipe-lock-reset-devices.md) (Ayuda a la protección de datos mediante la eliminación remota, el bloqueo remoto o el restablecimiento de código de acceso con System Center Configuration Manager).  

    -   **Cambiar la propiedad de un dispositivo**  

         Si un dispositivo no se ha unido a un dominio y no tiene el cliente de Configuration Manager instalado, use esta opción para cambiar la propiedad a **Compañía** o **Personal**.  

         Puede usar este valor en requisitos de aplicaciones para controlar las implementaciones y para controlar la cantidad de inventario que se recopila de los dispositivos de los usuarios.  

        Puede que necesite agregar la columna **Propietario del dispositivo** a la vista haciendo clic con el botón derecho en cualquier encabezado de columna y seleccionándola.

         Para obtener más información, consulte [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md) (Administración híbrida de dispositivos móviles [MDM] con System Center Configuration Manager y Microsoft Intune)  

##  <a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Administrar clientes desde el nodo Recopilaciones de dispositivos  
  Muchas de las tareas que están disponibles para los dispositivos en el nodo **Dispositivos** también lo están en las colecciones. La consola aplica automáticamente la operación en todos los dispositivos aptos de la recopilación. Esta acción en una recopilación completa genera paquetes de red adicionales y aumenta el uso de la CPU en el servidor del sitio.  

  Tenga en cuenta lo siguiente antes de realizar tareas de nivel de recopilación. Una vez que se haya iniciado, no puede detener la tarea de la consola. 
 - ¿Cuántos dispositivos hay en la recopilación?
 - ¿Los dispositivos están conectados mediante conexiones de red de ancho de banda reducido?
 - ¿Cuánto tiempo tarda esta tarea en completarse para todos los dispositivos?

#### <a name="to-manage-clients-from-the-device-collections-node"></a>Para administrar clientes desde el nodo Recopilaciones de dispositivos  

1.  En la consola de Configuration Manager, pulse **Activos y compatibilidad** > **Recopilaciones de dispositivos**.  

3.  Seleccione una recopilación y, después, una de las tareas de administración de cliente disponibles en la cinta o haga clic con el botón derecho en la recopilación. Estas tareas de administración de clientes *solo* pueden realizarse en el nivel de recopilación.  

    -   **Examinar equipos en busca de malware y descargar archivos de definición de antimalware**  

         Vea [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md) (Endpoint Protection en System Center Configuration Manager).  

    -   **Implementar software, líneas de base de configuración y secuencias de tareas**  

         Vea:  

        -   [Deploy software updates in System Center Configuration Manager](../../../sum/deploy-use/deploy-software-updates.md) (Administración de actualizaciones de software en System Center Configuration Manager)  

        -   [Plan for and configure compliance settings in System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) (Planeación y configuración de cumplimiento en System Center Configuration Manager)  

    -   **Configurar opciones de administración de energía**  

         Consulte [How to create and apply power plans in System Center Configuration Manager](../../../core/clients/manage/power/create-and-apply-power-plans.md) (Creación y aplicación de planes de energía en System Center Configuration Manager). Los planes de energía solo se pueden usar con equipos que ejecuten Windows.  

    -   **Notificar a los equipos que descarguen la directiva lo antes posible**  

         Use la notificación de cliente para notificar a los clientes de Windows seleccionados que descarguen la directiva de equipo lo antes posible fuera del intervalo de sondeo de la directiva de cliente.  

         Las tareas de notificación de cliente se muestran en el nodo **Operaciones de cliente** del área de trabajo **Supervisión** .  


## <a name="restart-clients"></a>Reinicio de clientes
A partir de la versión 1710, se puede usar la consola de Configuration Manager para identificar los clientes que precisan un reinicio. Después, use una acción de notificación de cliente para reiniciarlos.

> [!Tip]
> También debe actualizar a los clientes a la versión 1710 para que esta característica funcione. Se recomienda habilitar la actualización automática del cliente para mantenerlo al día con la mínima sobrecarga administrativa. Para obtener más información, vea [Usar una actualización de cliente automática](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).

Para identificar los dispositivos pendientes de reinicio, vaya al área de trabajo **Activos y compatibilidad** de la consola de Configuration Manager y seleccione el nodo **Dispositivos**. Después, puede ver el estado de cada dispositivo en el panel de detalles en una nueva columna denominada **Reinicio pendiente**. Cada dispositivo tiene uno o varios de los valores siguientes: 
 - **No**: no hay ningún reinicio pendiente
 - **Configuration Manager**: este valor proviene del componente de coordinador de reinicio de cliente (RebootCoordinator.log)
 - **Cambiar nombre de archivo**: este valor proviene de una operación de cambio de nombre de archivo pendiente notificada por Windows (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations)
 - **Windows Update**: este valor proviene de la notificación de Windows Update Agent de un reinicio pendiente necesario para una o varias actualizaciones (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired)
 - **Agregar o quitar características**: este valor proviene del servicio basado en componentes de Windows que notifica que la adición o eliminación de una característica de Windows requiere un reinicio (HKLM\Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\Reboot Pending)

**Para crear la notificación de cliente para reiniciar un dispositivo:**
1.  Busque el dispositivo que quiera reiniciar dentro de una recopilación en el nodo **Recopilaciones de dispositivos** de la consola.
2.  Haga clic con el botón derecho en el dispositivo, seleccione **Notificación de cliente** y, después, seleccione **Reiniciar**. Se abre una ventana de información sobre el reinicio. Haga clic en **Aceptar** para confirmar la solicitud de reinicio.

Cuando el cliente recibe la notificación de un **Centro de software**, se abre la ventana de notificación para informar al usuario sobre el reinicio. De forma predeterminada, el reinicio se produce al cabo de 90 minutos. Puede modificar la hora de reinicio en la [configuración de cliente](/sccm/core/clients/deploy/configure-client-settings). La configuración para el comportamiento del reinicio se encuentra en la pestaña [Reinicio de equipo](/sccm/core/clients/deploy/about-client-settings#computer-restart) de la configuración predeterminada.


##  <a name="BKMK_ClientCache"></a> Configurar la caché del cliente para clientes de Configuration Manager  
La caché del cliente almacena los archivos temporales para el momento en que los clientes instalen aplicaciones y programas. Las actualizaciones de software también usan la caché de cliente, pero siempre intentan descargar a la caché independientemente de la configuración de tamaño. Configure las opciones de caché, como el tamaño y ubicación, al instalar manualmente el cliente, al usar la instalación de inserción de cliente o después de la instalación.

A partir de la versión 1606 de Configuration Manager, puede especificar el tamaño de la carpeta de caché mediante la configuración del cliente en la consola de Configuration Manager.   

 La ubicación predeterminada de la caché de cliente de Configuration Manager es %*windir*%\ccmcache y el espacio en disco predeterminado es 5120 MB.  

> [!IMPORTANT]  
>  No cifre la carpeta utilizada para la caché de cliente. Configuration Manager no puede descargar contenido en una carpeta cifrada.  

### <a name="about-client-cache"></a>Acerca de la caché de cliente  

El cliente de Configuration Manager descarga el contenido del software necesario en cuanto recibe la implementación, pero espera el tiempo programado para ejecutar la implementación. Cuando llega el momento programado, el cliente de Configuration Manager comprueba si el contenido está disponible en la caché. Si el contenido está en la caché y es la versión correcta, el cliente usa el contenido almacenado en caché. Cuando cambia la versión requerida del contenido, o bien si el cliente elimina el contenido para hacer sitio a otro paquete, el cliente descarga de nuevo el contenido en la caché.  

Si el cliente trata de descargar el contenido de un programa o aplicación cuyo tamaño es mayor que el de la caché, se produce un error de implementación debido a la falta de espacio en la caché. El cliente genera el mensaje de estado 10050 de tamaño de caché insuficiente. Si aumenta el tamaño de caché más adelante, el resultado es el siguiente:  

-   Para un programa necesario: el cliente no reintenta descargar el contenido automáticamente. Vuelva a implementar el paquete y el programa en el cliente.  
-   Para una aplicación necesaria: el cliente reintenta descargar el contenido automáticamente cuando descarga su directiva de cliente.  

Si el cliente trata de descargar un paquete cuyo tamaño es inferior al de la caché, pero la caché está llena, se reintentan todas las implementaciones necesarias hasta que la caché disponga de espacio o se alcance el tiempo de espera de la descarga o el límite de número de reintentos. Si aumenta el tamaño de la caché más adelante, el cliente de Configuration Manager trata de volver a descargar el paquete durante el próximo intervalo de reintento. El cliente trata de descargar el contenido cada cuatro horas hasta un máximo de 18 intentos.  

El contenido de la caché no se elimina automáticamente, sino que permanece en la caché durante al menos un día después de que el cliente utiliza ese contenido. Si configura las propiedades del paquete con la opción para conservar el contenido de la caché del cliente, el cliente no elimina automáticamente el contenido del paquete de la caché. Si los paquetes descargados en las últimas 24 horas ocupan el espacio de la caché y el cliente debe descargar paquetes nuevos, puede aumentar el tamaño de la caché u optar por eliminar el contenido conservado en la caché.  

 Utilice los procedimientos siguientes para configurar la caché del cliente durante la instalación manual del cliente, o después de instalar el cliente.  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>Para configurar la caché del cliente al instalar los clientes mediante la instalación manual del cliente  

Ejecute el comando CCMSetup.exe desde la ubicación de origen de instalación y especifique las siguientes propiedades necesarias, que han de estar separadas por espacios:  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Para la versión 1606, use la configuración de tamaño de caché disponible en **Configuración de cliente** en la consola de Configuration Manager en lugar de SMSCACHESIZE. Para obtener más información, vea [Configuración de la memoria caché del cliente](../../../core/clients/deploy/about-client-settings.md#client-cache-settings).

Para obtener más información sobre estas propiedades de línea de comandos para CCMSetup.exe, vea [Acerca de las propiedades de instalación de clientes](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>Para configurar la carpeta de caché de cliente al instalar los clientes mediante la instalación de inserción de cliente  

1.  En la consola de Configuration Manager, pulse **Administración** > **Configuración del sitio** > **Sitios**.  

3.  Seleccione el sitio apropiado y en la pestaña **Inicio**, en el grupo **Configuración**, pulse **Configuración de instalación de cliente** > **pestaña Propiedades de instalación**.  

5.  Especifique las siguientes propiedades, separadas por espacios:  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Para la versión 1606, use la configuración de tamaño de caché disponible en **Configuración de cliente** en la consola de Configuration Manager en lugar de SMSCACHESIZE. Para obtener más información, vea [Configuración de la memoria caché del cliente](../../../core/clients/deploy/about-client-settings.md#client-cache-settings).

       Para obtener más información sobre estas propiedades de línea de comandos para CCMSetup.exe, vea [Acerca de las propiedades de instalación de clientes](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>Para configurar la carpeta de caché de cliente en el equipo del cliente  

1.  En el equipo cliente, vaya a **Configuration Manager** en el Panel de control y haga doble clic para abrir las propiedades.  

2.  En la pestaña **Caché** establezca las propiedades de espacio y ubicación. La ubicación predeterminada es *%windir%* \ccmcache.  

3.  Para eliminar los archivos de la carpeta de caché, pulse **Eliminar archivos**.  

### <a name="to-configure-client-cache-size-in-client-settings"></a>Para configurar el tamaño de la caché de cliente en la configuración de cliente

Ajuste el tamaño de la caché del cliente sin tener que volver a instalar el cliente mediante la configuración del tamaño de la caché en la consola de Configuration Manager con la configuración de cliente.  

1. En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente**.

2. Haga doble clic en **Configuración de cliente predeterminada**.
  También puede crear una configuración de cliente personalizada para aplicar el tamaño de caché de forma más selectiva. Para obtener más información acerca de las configuraciones personalizadas y de cliente, consulte [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md) (Configuración del cliente en System Center Configuration Manager).

 3. Pulse **Configuración de caché de cliente** y pulse **Sí** para **Configurar el tamaño de caché de cliente**, después use la opción **MB** o **Porcentaje de disco**. La memoria caché se ajusta al tamaño que sea menor.

     El cliente de Configuration Manager configurará el tamaño de caché con estos valores cuando se descargue la próxima directiva de cliente.



##  <a name="BKMK_UninstalClient"></a> Desinstalar el cliente de Configuration Manager  
 Para desinstalar de un equipo con Windows el software cliente de Configuration Manager, use **CCMSetup.exe** con la propiedad **/Uninstall**. Ejecute CCMSetup.exe en un equipo individual desde el símbolo del sistema o implemente un paquete y el programa para desinstalar el cliente de una recopilación de equipos.  

> [!WARNING]  
>  No puede desinstalar al cliente de Configuration Manager desde un dispositivo móvil. Si debe quitar el cliente de Configuration Manager de un dispositivo móvil, debe borrar el dispositivo y, de esta forma, se eliminan todos los datos del dispositivo móvil.  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>Para desinstalar el cliente de Configuration Manager desde el símbolo del sistema  

1.  Abra un símbolo del sistema de Windows y cambie la carpeta a la ubicación en la que se encuentra CCMSetup.exe.  

2.  Escriba **Ccmsetup.exe /uninstall**y, a continuación, presione **Entrar**.  

> [!NOTE]  
>  El proceso de desinstalación no muestra ningún resultado en la pantalla. Para comprobar que la desinstalación del cliente se ha realizado correctamente, examine el archivo de registro **CCMSetup.log** en la carpeta *%windir%\ ccmsetup* del equipo cliente.  

##  <a name="BKMK_ConflictingRecords"></a> Administrar registros en conflicto para clientes de Configuration Manager  
 Configuration Manager usa el identificador de hardware para tratar de identificar los clientes que puedan estar duplicados y alertarle de los registros en conflicto. Por ejemplo, si reinstala un equipo, el identificador de hardware sería el mismo, pero el GUID que usa Configuration Manager es posible que cambie.  

 Configuration Manager resuelve automáticamente los conflictos mediante la autenticación de Windows de la cuenta del equipo o un certificado PKI de un origen de confianza. Pero cuando Configuration Manager no puede resolver el conflicto de identificadores de hardware duplicados, una configuración de jerarquía determina si se deben combinar los registros automáticamente o le permite determinar el comportamiento. Si decide administrar los registros duplicados manualmente, debe resolver manualmente los registros en conflicto de la consola de Configuration Manager.  


#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>Para cambiar la configuración de la jerarquía a fin de administrar los registros en conflicto  

1.  En la consola de Configuration Manager, pulse **Administración** > **Configuración del sitio** > **Sitios** > **Configuración de jerarquía**.
2.  En la pestaña **Aprobación de cliente y registros conflictivos**, pulse **Resolver automáticamente los registros conflictivos** o **Resolver manualmente los registros conflictivos**.  

#### <a name="to-manually-resolve-conflicting-records"></a>Para resolver manualmente los registros en conflicto  

1.  En la consola de Configuration Manager, pulse **Supervisión** > **Estado del sistema** > **Registros en conflicto**.  

3.  Seleccione uno o más registros en conflicto y, después, pulse **Registros en conflicto**.  

4.  Seleccione una de las siguientes opciones:  

    -   **Combinar** para combinar el registro recién detectado con el registro de cliente existente.  

    -   **Nuevo** para crear un nuevo registro de cliente en conflicto.  

    -   **Bloquear** para crear un nuevo registro de cliente en conflicto, pero se marca como bloqueado.  

## <a name="manage-duplicate-hardware-identifiers"></a>Administrar identificadores de hardware duplicados
Proporcionar una lista de identificadores de hardware que Configuration Manager ignora para el arranque de PXE y el registro de cliente, ayuda a resolver dos problemas comunes.

1. Muchos dispositivos nuevos, como Surface Pro 3, no incluyen un puerto Ethernet integrado. Los técnicos usan un adaptador de USB a Ethernet para establecer una conexión con cable para la implementación del sistema operativo. Pero suele tratarse de adaptadores compartidos debido a su costo y su facilidad de uso general. Dado que la dirección MAC de este adaptador se usa para identificar el dispositivo, resulta problemático volver a usar el adaptador si no se realizan acciones de administrador adicionales entre cada implementación. Para volver a usar el adaptador en este escenario, excluya su dirección MAC.
2. Aunque el atributo SMBIOS debe ser único, algunos dispositivos de hardware especiales tienen identificadores duplicados. Excluya este identificador duplicado y use la dirección MAC única de cada dispositivo como base.

#### <a name="to-add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Para agregar identificadores de hardware a fin de que Configuration Manager los omita  
1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Configuración del sitio** > **Sitios**.
2. En la pestaña **Inicio**, en el grupo **Sitios**, pulse **Configuración de jerarquía**.
3. En la pestaña **Aprobación de cliente y registros conflictivos**, pulse **Agregar** en la sección **Identificadores de hardware duplicados** para agregar nuevos identificadores de hardware.

##  <a name="BKMK_PolicyRetrieval"></a> Iniciar la recuperación de directivas para un cliente de Configuration Manager  
 Un cliente de Configuration Manager en Windows descarga su directiva de cliente en una programación que se configura como una configuración de cliente. Pero pueden darse casos en los que quiera iniciar la recuperación de directiva a petición desde el cliente (por ejemplo para solucionar problemas o realizar pruebas).  

Puede iniciar la recuperación de directivas con:


- [Notificación de cliente](#initiate-client-policy-retrieval-using-client-notification)
- [La pestaña **Acciones** en el cliente](#manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client)
- [Un script](#manually-initiate-client-policy-retrieval-by-script)

> [!NOTE]  
>   
>  Para obtener más información sobre la recuperación de directivas de clientes que ejecutan Linux y UNIX, consulte [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU) (Directiva de equipo para servidores de Linux y UNIX).  

#### <a name="initiate-client-policy-retrieval-using-client-notification"></a>Iniciar la recuperación de directivas de cliente mediante la notificación de cliente  

1.  En la consola de Configuration Manager, pulse **Activos y compatibilidad** > **Recopilaciones de dispositivos**.  

3.  Seleccione la recopilación de dispositivos que contiene los equipos en los que quiere descargar la directiva. En la pestaña **Inicio**, en el grupo **Recopilaciones**, pulse **Notificación de cliente** > **Descargar directiva de equipo**.  

    > [!NOTE]  
    >  También puede utilizar la notificación de cliente para iniciar la recuperación de directiva de uno o varios dispositivos seleccionados mostrados en un nodo de recopilación temporal en el nodo **Dispositivos** .  

#### <a name="manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client"></a>Iniciar manualmente la recuperación de directiva de cliente en la pestaña Acciones del cliente de Configuration Manager  

1.  Seleccione **Configuration Manager** en el Panel de control del equipo.  

2.  En la pestaña **Acciones**, pulse **Ciclo de evaluación y recuperación de directivas de equipo** para iniciar la directiva de equipo y, después, pulse **Ejecutar ahora**.  

4.  Pulse **Aceptar** para confirmar el aviso.  

5.  Repita los pasos 3 y 4 para todas las demás acciones que desee aplicar, como **Ciclo de evaluación y recuperación de directivas de usuario** para la configuración de cliente del usuario.  

#### <a name="manually-initiate-client-policy-retrieval-by-script"></a>Iniciar manualmente la recuperación de directiva de cliente mediante script  

1.  Abra un editor de texto, como el Bloc de notas.  

2.  Copie e inserte el siguiente código de ejemplo de Visual Basic Scripting Edition en el archivo:  

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

5.  Pulse **Aceptar** en el cuadro de diálogo **Windows Script Host**.  
