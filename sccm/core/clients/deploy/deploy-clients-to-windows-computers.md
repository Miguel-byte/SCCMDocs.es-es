---
title: Implementar clientes en Windows | System Center Configuration Manager
description: "Obtenga información sobre cómo implementar clientes en equipos Windows con System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
caps.latest.revision: 13
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5a52386c6327ded3c5a400c7a046a6a12af96bae


---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>Implementar clientes en equipos Windows con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede usar distintos métodos de implementación de cliente para instalar el software de cliente de System Center Configuration Manager en los equipos. Para ayudarle a decidir qué método de implementación debe usar, consulte [Client installation methods in System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md) (Métodos de instalación de cliente en System Center Configuration Manager).  

 Antes de instalar los clientes de Configuration Manager, asegúrese de que todos los requisitos previos están en vigor y de que se completaron todas las configuraciones de implementación necesarias. Para obtener más información, consulte [Prerequisites for deploying clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) (Requisitos previos para la implementación de clientes en equipos Windows con System Center Configuration Manager).  


##  <a name="a-namebkmkclientpusha-how-to-install-configuration-manager-clients-by-using-client-push"></a><a name="BKMK_ClientPush"></a> Instalación de clientes de Configuration Manager mediante la inserción de cliente  

 Use la instalación de inserción de cliente para instalar software de cliente de Configuration Manager en los equipos detectados por Configuration Manager. Puede configurar una instalación de inserción de cliente para un sitio y la instalación de cliente se ejecutará automáticamente en los equipos detectados dentro de los límites configurados del sitio cuando estos límites se configuran como un grupo de límites. O bien, puede iniciar una instalación de inserción de cliente mediante la ejecución del Asistente para instalación de inserción de cliente para una recopilación o recurso específico dentro de una recopilación.  

 También puede usar el Asistente para instalación de inserción de cliente para instalar el cliente de Configuration Manager a los resultados obtenidos al ejecutar una consulta. Para que la instalación se realice correctamente en este escenario, uno de los elementos devueltos por la consulta seleccionada debe ser el atributo **ResourceID** de la clase de atributo **Recurso del sistema**. Para obtener más información sobre consultas, consulte [Queries technical reference for System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md) (Referencia técnica de consultas para System Center Configuration Manager).  

 Si el servidor de sitio no puede ponerse en contacto con el equipo cliente ni iniciar el proceso de instalación, repite automáticamente el intento de instalación cada hora durante un máximo de 7 días hasta que se realiza correctamente.  

 Para realizar un seguimiento del proceso de instalación de cliente, instale un sistema de sitio del punto de estado de reserva antes de instalar los clientes. Cuando se instala un punto de estado de reserva, se asigna automáticamente a los clientes cuando se instalan por el método de instalación de inserción de cliente. Consulte los informes de implementación y asignación de cliente para realizar un seguimiento del progreso de la instalación de cliente. Además, los archivos de registro de cliente proporcionan información más detallada acerca de la solución de problemas y no requieren la instalación de un punto de estado de reserva. Por ejemplo, el archivo CCM.log en el servidor de sitio registra todos los problemas que el servidor de sitio tiene al conectarse al equipo y el archivo CCMSetup.log en el cliente registra el proceso de instalación.  

> [!IMPORTANT]  
>  Para que la inserción de cliente se realice correctamente, asegúrese de que todos los requisitos previos están en vigor. Se muestran en la sección "Installation Method Dependencies" (Dependencias de los métodos de instalación) en [Prerequisites for deploying clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) (Requisitos previos para la implementación de clientes en equipos Windows en System Center Configuration Manager).  

#### <a name="to-configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Para configurar el sitio para que utilice automáticamente la inserción de cliente para equipos detectados  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.  

3.  En la lista **Sitios** , seleccione el sitio para el que va a configurar la instalación de inserción de cliente automática en todo el sitio.  

4.  En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Configuración de instalación de cliente**y, a continuación, haga clic en la pestaña **Instalación de inserción de cliente**.  

5.  En la pestaña **General** del cuadro de diálogo **Propiedades de instalación de inserción de cliente** , seleccione **Habilitar instalación de inserción de cliente automática en todo el sitio**. Seleccione los tipos de sistema a los que Configuration Manager debería insertar el software cliente mediante la selección de **Servidores**, **Estaciones de trabajo** o **Servidores del sistema de sitios de Configuration Manager**. La selección predeterminada es **Servidores** y **Estaciones de trabajo**.  

6.  Seleccione si quiere que la instalación de inserción de cliente automática en todo el sitio instale el software del cliente de Configuration Manager en los controladores de dominio.  

7.  En la pestaña **Cuentas**, especifique una o varias cuentas de Configuration Manager que se van a usar al conectarse al equipo para instalar el software cliente. Haga clic en el icono **Crear** , escriba el **Nombre de usuario** y **Contraseña**, confirme la contraseña y, a continuación, haga clic en **Aceptar**. Debe especificar al menos una cuenta de instalación de inserción de cliente, que debe tener derechos de administrador local en cada equipo en el que desea instalar el cliente. Si no especifica una cuenta de instalación de inserción de cliente, Configuration Manager intenta usar la cuenta de equipo del sistema de sitio, lo que producirá un error en la inserción de cliente entre dominios.  

    > [!IMPORTANT]  
    >  La contraseña para la cuenta de instalación de inserción de cliente se limita como máximo a 38 caracteres.  

    > [!NOTE]  
    >  Si se va a utilizar el método de instalación de inserción de cliente desde un sitio secundario, la cuenta debe especificarse en el sitio secundario que inicia la inserción de cliente.  
    >   
    >  Para obtener más información sobre la cuenta de instalación de inserción de cliente, consulte el procedimiento "Para usar el Asistente para instalación de inserción de cliente", incluido a continuación.  

8.  En la pestaña **Propiedades de instalación**, especifique las propiedades de instalación que se van a usar al instalar el cliente de Configuration Manager. Puede especificar cualquier propiedad de instalación del paquete de Windows Installer (Client.msi) y las propiedades de CCMSetup.exe siguientes:  

    -   /forcereboot  

    -   /skipprereq  

    -   /logon  

    -   /BITSPriority  

    -   /downloadtimeout  

    -   /forceinstall  

     Las propiedades de instalación de cliente que se especifican en esta pestaña se publican en Active Directory Domain Services si el esquema se extiende a Configuration Manager y las leen las instalaciones cliente en donde se ejecuta CCMSetup sin propiedades de instalación. Para obtener más información sobre las propiedades de instalación de cliente, consulte [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (Acerca de las propiedades de instalación de cliente en System Center Configuration Manager).  

    > [!NOTE]  
    >  Si habilita la instalación de inserción de cliente en un sitio secundario, asegúrese de que la propiedad SMSSITECODE esté establecida en el nombre de sitio de Configuration Manager de su sitio primario principal. Si el esquema de Active Directory se extiende a Configuration Manager, también puede establecerlo en AUTO para que busque automáticamente la asignación correcta de sitio.  

#### <a name="to-use-the-client-push-installation-wizard"></a>Para utilizar el Asistente para instalación de inserción de cliente  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.  

3.  En la lista **Sitios** , seleccione el sitio para el que va a configurar la instalación de inserción de cliente automática en todo el sitio.  

4.  En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Configuración de instalación de cliente**y, a continuación, haga clic en la pestaña **Instalación de inserción de cliente**.  

5.  En la pestaña **Propiedades de instalación**, especifique las propiedades de instalación que se van a usar al instalar el cliente de Configuration Manager. Puede especificar cualquier propiedad de instalación del paquete de Windows Installer (Client.msi) y las propiedades de CCMSetup.exe siguientes:  

    -   /forcereboot  

    -   /skipprereq  

    -   /logon  

    -   /BITSPriority  

    -   /downloadtimeout  

    -   /forceinstall  

     Las propiedades de instalación de cliente que se especifican en esta pestaña se publican en Active Directory Domain Services si el esquema se extiende a Configuration Manager y las leen las instalaciones cliente en donde se ejecuta CCMSetup sin propiedades de instalación. Para obtener más información sobre las propiedades de instalación de cliente, consulte [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (Acerca de las propiedades de instalación de cliente en System Center Configuration Manager).  

6.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

7.  En el área de trabajo **Activos y compatibilidad** , seleccione uno o varios equipos o una recopilación de equipos.  

8.  En la pestaña **Inicio** , elija una de las opciones siguientes:  

    -   Si desea instalar el cliente en un único equipo o en varios, en el grupo **Dispositivo** , haga clic en **Instalar cliente**.  

    -   Si desea instalar el cliente en una recopilación de equipos, en el grupo **Recopilación** , haga clic en **Instalar cliente**.  

9. En la página **Antes de comenzar** del **Asistente para instalación de cliente**, revise la información y, a continuación, haga clic en **Siguiente**.  

10. En la página **Opciones de instalación** , configure si el cliente se puede instalar en controladores de dominio, si se va a volver a instalar, actualizar o reparar en equipos con un cliente existente, así como el nombre del sitio que instalará el software de cliente. Haga clic en **Siguiente**.  

11. Revise la configuración de instalación y, a continuación, cierre el asistente.  

> [!NOTE]  
>  Puede utilizar el asistente para instalar clientes, incluso si el sitio no está configurado para la inserción de clientes.  

##  <a name="a-namebkmkclientsupa-how-to-install-configuration-manager-clients-by-using-software-update-based-installation"></a><a name="BKMK_ClientSUP"></a> Instalación de clientes de Configuration Manager mediante la instalación basada en actualizaciones de software  
 La instalación de cliente basada en actualizaciones de software publica el cliente de Configuration Manager en un punto de actualización de software como actualización de software adicional. Se puede usar este método de instalación de cliente para instalar el cliente de Configuration Manager en equipos que todavía no tienen el cliente instalado o para actualizar clientes de Configuration Manager existentes.  

 Si un equipo tiene instalado el cliente de Configuration Manager, Configuration Manager proporciona al cliente el puerto y nombre de servidor del punto de actualización de software desde el que podrá obtener actualizaciones de software. Esta información se incluye en la directiva de cliente.  

> [!IMPORTANT]  
>  Para utilizar la instalación basada en actualizaciones de software, debe utilizar el mismo servidor de Windows Server Update Services (WSUS) para la instalación de cliente y actualizaciones de software. Este servidor debe ser el punto de actualización de software activo de un sitio primario. Para obtener más información, consulte [Install a software update point](../../../sum/get-started/install-a-software-update-point.md) (Instalar un punto de actualización de software).  

 Si un equipo no tiene instalado el cliente de Configuration Manager, debe configurar y asignar un objeto de directiva de grupo (GPO) en Active Directory Domain Services para especificar el nombre de servidor del punto de actualización de software a partir del cual el equipo obtendrá actualizaciones de software.  

 No se pueden agregar propiedades de línea de comandos a una instalación de cliente basada en actualizaciones de software. Si extendió el esquema de Active Directory a Configuration Manager, los equipos cliente consultan automáticamente las propiedades de instalación en Active Directory Domain Services cuando realizan la instalación.  

 Si no se extendió el esquema de Active Directory, puede utilizar la directiva de grupo para aprovisionar la configuración de instalación de cliente en su sitio. Esta configuración se aplica automáticamente a cualquier instalación de cliente basada en actualizaciones de software. Para obtener más información, consulte [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](#BKMK_Provision) [Cómo aprovisionar propiedades de instalación de cliente (instalación de cliente con directivas de grupo y basada en actualizaciones de software)] y [How to assign clients to a site in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md) (Cómo asignar clientes a un sitio en System Center Configuration Manager).  

 Use los procedimientos siguientes para configurar equipos sin un cliente de Configuration Manager para usar el punto de actualización de software para la instalación de cliente y actualizaciones de software, y para publicar el software de cliente de Configuration Manager en el punto de actualización de software.  

> [!NOTE]  
>  Si los equipos se encuentran en un estado de reinicio pendiente tras una instalación de software previa, una instalación de clientes basada en actualizaciones de software podría provocar que el equipo se reinicie.  

#### <a name="to-configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>Para configurar un objeto de directiva de grupo en los Servicios de dominio de Active Directory para especificar el punto de actualización de software para la instalación de cliente y actualizaciones de software.  

1.  Utilice la Consola de administración de directivas de grupo para abrir un objeto de directiva de grupo nuevo o existente.  

2.  En la consola, expanda **Configuración del equipo**, expanda **Plantillas administrativas**y **Componentes de Windows**y, a continuación, haga clic en **Windows Update**.  

3.  Abra las propiedades de la configuración **Especificar la ubicación del servicio Windows Update en la intranet**y, a continuación, haga clic en **Habilitado**.  

4.  En el cuadro **Establecer el servicio de actualización de la intranet para detectar actualizaciones**, especifique el nombre del servidor de actualización de software que desea usar, así como el puerto. Deben coincidir exactamente con el formato de nombre de servidor y con el puerto que utiliza el punto de actualización de software:  

    -   Si el sistema de sitio de Configuration Manager está configurado para utilizar un nombre de dominio completo (FQDN), especifique el nombre del servidor con el formato de nombre de dominio completo.  

    -   Si el sistema de sitio de Configuration Manager no está configurado para utilizar un nombre de dominio completo (FQDN), especifique el nombre del servidor con un formato de nombre corto.  

    > [!NOTE]  
    >  Para determinar el número de puerto que usa el punto de actualización de software, consulte [How to determine the port settings used by WSUS in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md) (Cómo determinar la configuración de puerto usada por WSUS en System Center Configuration Manager).  

     Ejemplo: **http://server1.contoso.com:8530**  

5.  En el cuadro **Establecer el servidor de estadísticas de la intranet**, especifique el nombre del servidor de estadísticas de la intranet que desea utilizar. No hay ningún requisito específico para especificar este servidor. No tiene que ser el mismo equipo que el servidor de punto de actualización de software, y el formato no tiene que coincidir si es el mismo servidor.  

6.  Asigne el objeto de directiva de grupo a los equipos en los que se va a instalar al cliente de Configuration Manager y recibir actualizaciones de software.  

#### <a name="to-publish-the-configuration-manager-client-to-the-software-update-point"></a>Para publicar el cliente de Configuration Manager en el punto de actualización de software  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.  

3.  En la lista **Sitios** , seleccione el sitio para el que va a configurar la instalación de cliente basada en actualizaciones de software.  

4.  En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Configuración de instalación de cliente**y, a continuación, haga clic en la pestaña **Instalación de cliente basada en actualizaciones de software**.  

5.  En el cuadro de diálogo **Propiedades de instalación de cliente de punto de actualización de software** , seleccione **Habilitar instalación de cliente basada en actualizaciones de software** para habilitar este método de instalación de cliente.  

6.  Si el software cliente del servidor de sitio de Configuration Manager es una versión posterior a la versión de cliente almacenada en el punto de actualización de software, se abre el cuadro de diálogo **Se detectó una versión más reciente del paquete de cliente**. Haga clic en **Sí** para publicar la versión más reciente del software de cliente en el punto de actualización de software.  

    > [!NOTE]  
    >  Si el software de cliente no se publicó anteriormente en el punto de actualización de software, este cuadro quedará en blanco.  

7.  Para terminar de configurar la instalación de cliente del punto de actualización de software, haga clic en **Aceptar**.  

> [!NOTE]  
>  La actualización de software para el cliente de Configuration Manager no se actualiza automáticamente cuando hay una nueva versión. Si actualiza el sitio, lo que incluye una nueva versión de cliente, debe repetir este procedimiento y hacer clic en **Sí** para el paso 6.  

##  <a name="a-namebkmkclientgpa-how-to-install-configuration-manager-clients-by-using-group-policy"></a><a name="BKMK_ClientGP"></a> Instalación de clientes de Configuration Manager mediante directiva de grupo  
 Puede usar una directiva de grupo de Active Directory Domain Services para publicar o asignar el cliente de Configuration Manager con el fin de instalarlo en equipos de su empresa. Cuando se asigna el cliente de Configuration Manager a equipos mediante una directiva de grupo, el cliente se instala cuando se inicia por primera vez el equipo. Al publicar el cliente de Configuration Manager en los usuarios mediante la directiva de grupo, el cliente muestra en el Panel de Control **Agregar o quitar programas** para el equipo, de modo que el usuario pueda instalarlo.  

 Utilice el paquete de Windows Installer (CCMSetup.msi) para instalaciones basadas en directiva de grupo. Este archivo se encuentra en la carpeta **&lt;directorio de instalación de ConfigMgr\>\bin\i386** en el servidor de sitio de Configuration Manager. No se puede agregar propiedades a este archivo para modificar el comportamiento de la instalación:  

> [!IMPORTANT]  
>  Es necesario tener permisos de administrador en la carpeta para tener acceso a los archivos de instalación del cliente.  

-   Si el esquema de Active Directory se extiende para Configuration Manager y se selecciona **Publish this site in Active Directory Domain Services** (Publicar este sitio en Active Directory Domain Services) en la pestaña **Avanzadas** del cuadro de diálogo **Propiedades del sitio**, los equipos cliente buscan automáticamente en Active Directory Domain Services las propiedades de instalación. Para obtener más información sobre las propiedades de instalación publicadas, consulte [About client installation properties published to Active Directory Domain Services in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md) (Acerca de las propiedades de instalación de cliente publicadas en Active Directory Domain Services en System Center Configuration Manager).  

-   Si no se amplió el esquema de Active Directory, puede usar el siguiente procedimiento de este tema para almacenar las propiedades de instalación en el Registro de los equipos: [Aprovisionamiento de propiedades de instalación de cliente (instalación de clientes con directivas de grupo y basada en actualizaciones de software)](#BKMK_Provision). Estas propiedades de instalación se usan una vez que se ha instalado el cliente de Configuration Manager.  

 Para obtener información acerca del uso de una directiva de grupo en Servicios de dominio de Active Directory para instalar software, consulte la documentación de Windows Server.  

##  <a name="a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually"></a><a name="BKMK_Manual"></a> Instalación manual de clientes de Configuration Manager  
 Es posible instalar manualmente el software de cliente de Configuration Manager en los equipos de la empresa mediante el programa CCMSetup.exe. Este programa y los archivos auxiliares se encuentran en la carpeta **Cliente** de la carpeta de instalación de Configuration Manager del servidor de sitio y en los puntos de administración de su sitio. Esta carpeta se comparte en la red como  

 \\\\*&lt;Nombre del servidor de sitio\>*\SMS_*&lt;Código de sitio\>*\Client\  

 donde *&lt;Nombre del servidor de sitio\>* es el nombre de uno de los servidores que hospedan un punto de administración y *&lt;Código de sitio\>* es el código del sitio primario al que pertenece el cliente.  Para ejecutar CCMSetup.exe desde la línea de comandos en el cliente, debe asignar una unidad de red a esta ubicación y luego ejecutar el comando.  

> [!IMPORTANT]  
>  Es necesario tener permisos de administrador en la carpeta para tener acceso a los archivos de instalación del cliente.  

 CCMSetup.exe copia todos los requisitos previos de instalación necesarios en el equipo cliente y llama al paquete de Windows Installer (Client.msi) para realizar la instalación del cliente.  

> [!IMPORTANT]  
>  No se puede ejecutar Client.msi directamente.  

 Es posible especificar propiedades de línea de comandos para CCMSetup.exe y Client.msi para modificar el comportamiento de la instalación del cliente. Asegúrese de especificar las propiedades de CCMSetup (las propiedades que comienzan por **/**) antes de especificar las propiedades de Client.msi.  

 Por ejemplo, podría especificar el siguiente comando:  

```  
CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01  
```  

 y el cliente se instala mediante las propiedades siguientes:  

|Propiedad|Descripción|  
|--------------|-----------------|  
|**/mp:SMSMP01**|Esta propiedad de CCMSetup especifica que el punto de administración SMSMP01 descargue los archivos de instalación de cliente requeridos.|  
|**/logon**|Esta propiedad de CCMSetup especifica que la instalación se debe detener si se encuentra un cliente de Configuration Manager en el equipo.|  
|**SMSSITECODE=AUTO**|Esta propiedad de Client.msi especifica que el cliente intenta localizar el código de sitio de Configuration Manager que va a usar, por ejemplo, mediante Active Directory Domain Services.|  
|**FSP=SMSFP01**|Esta propiedad de Client.msi especifica que el punto de estado de reserva denominado SMSFP01 se utilizará para recibir mensajes de estado enviados desde el equipo cliente.|  

 Para obtener más información sobre todas las propiedades de CCMSetup.exe, consulte [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (Acerca de las propiedades de instalación de cliente en System Center Configuration Manager).  

### <a name="examples-for-installing-configuration-manager-clients-manually"></a>Ejemplos de instalación manual de Configuration Manager  
 Estos ejemplos son para clientes de Active Directory de la intranet y utilizan los siguientes valores para representar diferentes aspectos del sitio:  

 **MPSERVER** = servidor que hospeda el punto de administración   
**FSPSERVER** = servidor que hospeda el punto de estado de reserva  
**ABC** = código de sitio  
**contoso.com** = nombre de dominio  

 Todos los servidores de sistema de sitio están configurados con un FQDN de intranet y el sitio se publica en el bosque de Active Directory del cliente.  

 En el equipo cliente, inicie sesión como administrador local, asigne una unidad (z:) a\\\\MPSERVER\SMS_ABC\Client, cambie el símbolo del sistema a la unidad z y luego ejecute uno de los siguientes comandos.  

 **Ejemplo 1:**  

```  
CCMSetup.exe  
```  

> [!NOTE]  
>  En este ejemplo se instala el cliente sin propiedades adicionales para que el cliente se configure automáticamente utilizando las propiedades de instalación del cliente publicadas en Active Directory Domain Services. Por ejemplo, el cliente se configura automáticamente para el código de sitio (requiere que la ubicación de red del cliente se incluya en un grupo de límites configurado para asignación de clientes), un punto de administración, el punto de estado de reserva y para comunicación mediante HTTPS solamente. Para obtener más información sobre las propiedades de instalación de cliente que se pueden configurar automáticamente para clientes de Active Directory, consulte [About client installation properties published to Active Directory Domain Services in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md) (Acerca de las propiedades de instalación de cliente publicadas en Active Directory Domain Services en System Center Configuration Manager).  

 **Ejemplo 2:**  

```  
CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com  
```  

> [!NOTE]  
>  En este ejemplo se invalida la configuración automática que Active Directory Domain Services puede proporcionar y no se requiere que la ubicación de red del cliente se incluya en un grupo de límites configurado para la asignación de clientes. En su lugar, la instalación especifica el sitio, un punto de administración de intranet y un punto de administración basado en Internet, un punto de estado de reserva que acepte conexiones de Internet, y el uso de un certificado PKI de cliente (si está disponible) que tenga un periodo de validez mayor.  

##  <a name="a-namebkmkclientlogonscripta-how-to-install-configuration-manager-clients-by-using-logon-scripts"></a><a name="BKMK_ClientLogonScript"></a> Instalación de clientes de Configuration Manager mediante scripts de inicio de sesión  
 Configuration Manager admite scripts de inicio de sesión para instalar el software de cliente de Configuration Manager. Puede utilizar el archivo de programa **CCMSetup.exe** en un script de inicio de sesión para activar la instalación del cliente.  

 La instalación del script de inicio de sesión utiliza los mismos métodos que la instalación manual del cliente. Es posible especificar la propiedad de instalación **/logon** para CCMSsetup.exe, lo cual evita que se instale el cliente si ya existe alguna versión del cliente en el equipo. De este modo, se impide que se vuelva a instalar el cliente cada vez que se ejecute el script de inicio de sesión.  

 Si no se especifica ningún origen de instalación que use la propiedad **/Source** y no se especifica ningún punto de administración del que obtener la instalación mediante la propiedad **/MP**, CCMSetup.exe puede localizar el punto de administración mediante una búsqueda en Active Directory Domain Services si el esquema se ha ampliado para Configuration Manager y el sitio está publicado en Active Directory Domain Services. Como alternativa, el cliente puede utilizar DNS o WINS para localizar un punto de administración.  

##  <a name="a-namebkmkclientappa-how-to-install-configuration-manager-clients-by-using-a-package-and-program"></a><a name="BKMK_ClientApp"></a> Instalación de clientes de Configuration Manager mediante un paquete y un programa  
 Es posible usar Configuration Manager para crear e implementar un paquete y un programa que actualice el software cliente para equipos seleccionados de la jerarquía. Con Configuration Manager se suministra un archivo de definición del paquete que rellena las propiedades del paquete con los valores que se suelen usar. Es posible personalizar el comportamiento de la instalación del cliente mediante la especificación de propiedades de línea de comandos adicionales.  

> [!NOTE]  
>  No se puede actualizar clientes de Configuration Manager 2007 con este método. En su lugar, utilice la actualización de cliente automática, que automáticamente crea e implementa un paquete que contiene la versión más reciente del cliente. Para obtener más información, consulte [Upgrade clients in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) (Actualizar clientes en System Center Configuration Manager).  
>   
>  Para obtener más información sobre cómo migrar desde versiones anteriores del cliente de Configuration Manager, consulte [Planning a client migration strategy in System Center Configuration Manager](../../../core/migration/planning-a-client-migration-strategy.md) (Planear una estrategia de migración de clientes en System Center Configuration Manager).  

 Use el procedimiento siguiente para crear un paquete y un programa de Configuration Manager que pueda implementar en equipos cliente de Configuration Manager para actualizar el software cliente.  

#### <a name="to-create-a-package-and-program-for-the-client-software"></a>Para crear un paquete y un programa para el software cliente  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Administración de aplicaciones**y, a continuación, haga clic en **Paquetes**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear paquete a partir de definición**.  

4.  En la página **Definición de paquete** del **Asistente para crear paquete a partir de definición**, seleccione **Microsoft** en la lista desplegable **Editor** , seleccione **Actualización de cliente de Configuration Manager** en la lista **Definición de paquete** y, a continuación, haga clic en **Siguiente**.  

5.  En la página **Archivos de origen** del asistente, seleccione **Obtener siempre los archivos de la carpeta de origen**y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Carpeta de origen** del **Asistente para crear paquete a partir de definición**, seleccione **Ruta de red (nombre UNC)** y especifique la ruta de acceso de red al equipo y la carpeta que contiene los archivos de instalación del cliente de Configuration Manager.  

    > [!NOTE]  
    >  El equipo en el que se ejecute la implementación de Configuration Manager debe tener acceso a la carpeta de red especificada. Si el equipo no tiene acceso, se producirá un error en la instalación.  

7.  Haga clic en **Siguiente** y complete el asistente.  

8.  Si desea cambiar alguna de las propiedades de instalación de cliente, puede modificar los parámetros de la línea de comandos de CCMSetup.exe en la pestaña **General** del cuadro de diálogo del programa **Propiedades de actualización silenciosa de agente de Configuration Manager** . Las propiedades de instalación predeterminadas son **/noservice SMSSITECODE=AUTO**.  

9. Distribuya el paquete a todos los puntos de distribución en los que desea hospedar el paquete de actualización de cliente. Después, puede implementar el paquete en colecciones de equipos que contengan los clientes de Configuration Manager que quiere actualizar.  

##  <a name="a-namebkmkclientimagea-how-to-install-configuration-manager-clients-by-using-computer-imaging"></a><a name="BKMK_ClientImage"></a> Instalación de clientes de Configuration Manager mediante la creación de imágenes de equipos  
 Puede preinstalar el software de cliente de Configuration Manager en un equipo de imagen maestra que se usará para crear equipos de la empresa. Para instalar el cliente en un equipo maestro, no especifique un código de sitio para el cliente. Cuando se crea la imagen de los equipos desde esta imagen maestra, contendrá el cliente de Configuration Manager y deberá completar la asignación de sitio cuando la instalación se haya completado.  

> [!IMPORTANT]  
>  Los equipos con imagen no pueden funcionar como clientes de Configuration Manager hasta que los clientes de Configuration Manager se asignen a un sitio de Configuration Manager.  

 Debe quitar todos los certificados específicos del equipo instalados en el equipo de imagen maestra. Por ejemplo, si utiliza certificados de infraestructura de clave pública (PKI), debe quitar los certificados en el almacén **Personal** para **Equipo** y **Usuario** antes de crear la imagen del equipo.  

 Si los clientes no pueden consultar los Servicios de dominio de Active Directory para localizar un punto de administración, utilizan la clave raíz de confianza para determinar los puntos de administración de confianza. Si todos los clientes con imágenes se van a implementar en la misma jerarquía que el equipo maestro, deje la clave raíz de confianza. Si los clientes se van a implementar en jerarquías distintas, quite la clave raíz de confianza y, como práctica recomendada, aprovisione previamente a estos clientes con la nueva clave raíz de confianza. Para obtener más información, consulte [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) (Planeación de la clave raíz confiable).  

#### <a name="to-prepare-the-client-computer-for-imaging"></a>Para preparar el equipo cliente para la creación de imágenes  

1.  Instale manualmente el software de cliente de Configuration Manager en el equipo de imagen maestra. Para obtener más información, vea [Instalación manual de clientes de Configuration Manager](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  No especifique un código de sitio de Configuration Manager para el cliente en las propiedades de línea de comandos CCMSetup.exe.  

2.  En una línea de comandos, escriba **net stop ccmexec** para asegurarse de que el servicio **Host de agente de SMS** (Ccmexec.exe) no se ejecuta en el equipo de imagen maestra.  

3.  Quite todos los certificados almacenados en el almacén del equipo local del equipo de imagen maestra.  

4.  Si los clientes se van a instalar en una jerarquía de Configuration Manager diferente del equipo de imagen maestra, quite la clave raíz confiable del equipo de imagen maestra.  

5.  Utilice software de creación de imágenes para capturar la imagen del equipo maestro.  

6.  Implemente la imagen en equipos de destino.  

##  <a name="a-namebkmkclientworkgroupa-how-to-install-configuration-manager-clients-on-workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a> Instalación de clientes de Configuration Manager en equipos de grupo de trabajo  
 Configuration Manager admite la instalación de cliente para equipos del grupo de trabajo. Instale el cliente en los equipos del grupo de trabajo mediante el método especificado en [Instalación manual de clientes de Configuration Manager](#BKMK_Manual).  

 Deben cumplirse los siguientes requisitos previos para instalar el cliente de Configuration Manager en los equipos del grupo de trabajo:  

-   El cliente debe instalarse manualmente en cada equipo del grupo de trabajo. Durante la instalación, el usuario que inició la sesión debe tener derechos de administrador local en el equipo del grupo de trabajo.  

-   Con el fin de obtener acceso a recursos en el dominio de servidor del sitio de Configuration Manager, la cuenta de acceso de red debe estar configurada para el sitio. Especifique esta cuenta como una propiedad del componente de distribución de software. Para obtener más información, consulte [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md) (Componentes de sitio para System Center Configuration Manager).  

 Hay una serie de limitaciones para dar soporte a los equipos del grupo de trabajo:  

-   Los clientes del grupo de trabajo no pueden encontrar puntos de administración desde los Servicios de dominio de Active Directory y, en su lugar, deben utilizar DNS, WINS u otro punto de administración.  

-   No se admite la itinerancia global, ya que los clientes no pueden consultar los Servicios de dominio de Active Directory para obtener información del sitio.  

-   Los métodos de detección de Active Directory no pueden detectar equipos en los grupos de trabajo.  

-   No se puede implementar software para usuarios de equipos del grupo de trabajo.  

-   No se puede utilizar el método de instalación de inserción de cliente para instalar al cliente en equipos del grupo de trabajo.  

-   Los clientes del grupo de trabajo no pueden utilizar Kerberos para autenticación, por lo que podrían requerir la aprobación manual.  

-   No se puede configurar un cliente de grupo de trabajo como punto de distribución. Configuration Manager requiere que los equipos de punto de distribución pertenezcan a un dominio.  

#### <a name="to-install-the-client-on-workgroup-computers"></a>Para instalar el cliente en equipos del grupo de trabajo  

1.  Asegúrese de que los equipos en los que desea instalar al cliente cumplen los requisitos anteriores.  

2.  Siga las instrucciones de la sección [Instalación manual de clientes de Configuration Manager](#BKMK_Manual).  

     Ejemplo 1: **CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com**  

    > [!NOTE]  
    >  En este ejemplo se instala al cliente para la administración de cliente de intranet y se especifica el código de sitio y el sufijo DNS para localizar un punto de administración.  

     Ejemplo 2: **CCMSetup.exe FSP=fspserver.constoso.com**  

    > [!NOTE]  
    >  En este ejemplo se requiere que el cliente se encuentre en una ubicación de red configurada en un grupo de límites para que la asignación automática de sitio pueda realizarse correctamente. El comando incluye un punto de estado de reserva en el servidor FSPSERVER, para realizar un seguimiento de la implementación de cliente e identificar cualquier problema de comunicación de cliente.  

##  <a name="a-namebkmkclientinterneta-how-to-install-configuration-manager-clients-for-internet-based-client-management"></a><a name="BKMK_ClientInternet"></a> Instalación de clientes de Configuration Manager para administración de cliente basada en Internet  
 Si el sitio de Configuration Manager admite la administración de cliente basada en Internet para clientes que a veces se encuentran en la intranet y a veces en Internet, el usuario dispone de dos opciones para instalar clientes en la intranet:  

-   Puede incluir la propiedad Client.msi de CCMHOSTNAME=*&lt;FQDN de Internet del punto de administración basado en Internet\>* al instalar el cliente, por ejemplo, mediante instalación manual o inserción de cliente. Cuando se utiliza este método, también debe asignar directamente el cliente al sitio y no se puede utilizar la asignación automática de sitio. En la sección [Instalación manual de clientes de Configuration Manager](#BKMK_Manual) de este tema se proporciona un ejemplo de este método de configuración.  

-   Puede instalar el cliente para la administración de cliente de intranet y, después, asignar un punto de administración de cliente basada en Internet al cliente mediante las propiedades de cliente de Configuration Manager en el Panel de control, o mediante un script. Cuando utilice este método, puede utilizar la asignación automática de cliente. Para obtener más información, consulte la sección [Configuración de clientes para administración de cliente basada en Internet después de la instalación de cliente](#BKMK_ConfigureIBCM_MP) de este tema.  

 Si tiene que instalar clientes que se encuentran en Internet porque son clientes únicamente de Internet o porque debe instalarlos antes de que vuelvan a la intranet, elija uno de los siguientes métodos admitidos:  

-   Proporcione un mecanismo para que estos clientes se conecten temporalmente a la intranet mediante una red privada virtual (VPN) y, a continuación, instálelos mediante cualquier método de instalación de cliente apropiado.  

-   Debe usarse un método de instalación que sea independiente de Configuration Manager, como el empaquetado de los archivos de origen de instalación de cliente en medios extraíbles que se pueden enviar a los usuarios para que realicen la instalación con instrucciones. Los archivos de origen de instalación de cliente están ubicados en la carpeta *&lt;rutaDeInstalación\>*\Client, en el servidor de sitio de Configuration Manager y en los puntos de administración. Incluya un script en los medios para copiarlo manualmente en la carpeta de cliente y, desde esta carpeta, instale el cliente mediante CCMSetup.exe y todas las propiedades de línea de comandos apropiadas de CCMSetup.  

> [!NOTE]  
>  Configuration Manager no admite la instalación de un cliente directamente desde el punto de administración basado en Internet ni desde el punto de actualización de software basado en Internet.  

 Como los clientes administrados en Internet deben comunicarse con los sistemas de sitio basados en Internet, asegúrese de que estos clientes también disponen de certificados de infraestructura de clave pública (PKI) instalados antes de instalarlos. Debe instalar estos certificados con independencia de Configuration Manager. Para obtener más información sobre los requisitos de certificados, consulte [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md) (Requisitos de certificados PKI para System Center Configuration Manager).  

#### <a name="to-install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Para instalar clientes en Internet mediante la especificación de propiedades de línea de comandos de CCMSetup  

1.  Siga las instrucciones de la sección [Instalación manual de clientes de Configuration Manager](#BKMK_Manual) e incluya siempre lo siguiente:  

    -   Propiedad de la línea de comandos de CCMSetup **/source:***&lt;ruta de acceso local a la carpeta de cliente copiada\>*  

    -   Propiedad de línea de comandos de CCMSetup **/UsePKICert**  

    -   Propiedad Client.msi **CCMHOSTNAME=***&lt;FQDN del punto de administración basado en Internet\>*  

    -   Propiedad Client.msi **SMSSIGNCERT=***&lt;ruta de acceso local al certificado que firma el servidor de sitio exportado\>*  

    -   Propiedad Client.msi **SMSSITECODE=***&lt;código de sitio del punto de administración basado en Internet\>*  

    > [!NOTE]  
    >  Si el sitio tiene más de un punto de administración basado en Internet, no importa qué punto de administración basado en Internet se especifique para la propiedad CCMHOSTNAME. Cuando un cliente de Configuration Manager se conecta al punto de administración basado en Internet especificado, el punto de administración envía al cliente una lista de puntos de administración basados en Internet disponibles del sitio, y el cliente selecciona uno de la lista. La selección no es determinista.  

2.  Si no desea que el cliente compruebe la lista de revocación de certificados (CRL), especifique la propiedad de línea de comandos de CCMSetup **/NoCRLCheck**.  

3.  Si usa un punto de estado de reserva basado en Internet, especifique la propiedad Client.msi **FSP=***&lt;FQDN de Internet del punto de estado de reserva basado en Internet\>*.  

4.  Si va a instalar el cliente para la administración de cliente solo de Internet, especifique la propiedad Client.msi **CCMALWAYSINF=1**.  

5.  Compruebe si hay que especificar alguna propiedad de línea de comandos de CCMSetup adicional. Por ejemplo, es posible que tenga que especificar los criterios de selección de un certificado si el cliente tiene más de un certificado válido de PKI. Para ver la lista de las propiedades, consulte [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (Acerca de las propiedades de instalación de clientes en System Center Configuration Manager).  

     Ejemplo: **CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1**  

    > [!NOTE]  
    >  En este ejemplo se instalan los archivos de origen de cliente desde una carpeta en la unidad D con la opción de utilizar un certificado PKI de cliente y seleccionar el certificado con el período de validez más largo para la administración de cliente solo de Internet, se asigna el cliente para utilizar el punto de administración basado en Internet denominado SERVER1 y el punto de estado de reserva basado en Internet del dominio contoso.com, y se asigna el cliente al sitio ABC.  

###  <a name="a-namebkmkconfigureibcmmpa-how-to-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a> Configuración de clientes para administración de cliente basada en Internet después de la instalación de cliente  
 Para asignar el punto de administración basado en Internet después de instalar el cliente, utilice uno de los procedimientos siguientes. El primer procedimiento requiere una configuración manual, por lo que es adecuado para algunos clientes, mientras que el segundo procedimiento es más adecuado si cuenta con muchos clientes para configurar.  

##### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>Para configurar clientes para la administración de clientes basados en Internet después de la instalación de cliente mediante la asignación del punto de administración basado en Internet en Propiedades de Configuration Manager  

1.  Navegue a **Configuration Manager** en el Panel de Control del equipo cliente y, a continuación, haga doble clic para abrir sus propiedades.  

2.  En la pestaña **Internet** , escriba el nombre de dominio completo del punto de administración basado en Internet en el cuadro de texto FQDN de Internet.  

    > [!NOTE]  
    >  La pestaña **Internet** solo está disponible si el cliente tiene un certificado de PKI de cliente.  

3.  Especifique la configuración del servidor proxy si el cliente va a tener acceso a Internet mediante un servidor proxy.  

4.  Haga clic en **Aceptar**.  

##### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Para configurar clientes para administración de cliente basada en Internet después de la instalación de cliente mediante el uso de un script  

1.  Abra un editor de texto, como el Bloc de notas.  

2.  Copie e inserte lo siguiente en el archivo:  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the Internet-Based Management Point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

3.  Reemplace *mp.contoso.com* por el FQDN de Internet de su punto de administración basado en Internet.  

    > [!NOTE]  
    >  Si tiene que eliminar un punto de administración específico basado en Internet para que el cliente no se configure para utilizar un punto de administración basado en Internet, quite el valor dentro de las comillas para que esta línea sea **newInternetBasedManagementPointFQDN = ""**.  

4.  Guarde el archivo con una extensión .vbs.  

5.  Utilice cscript para ejecutar el script en los equipos cliente, mediante uno de los métodos siguientes:  

    -   Implemente el archivo en clientes de Configuration Manager existentes mediante un paquete y un programa.  

    -   Ejecute el archivo localmente en los clientes existentes de Configuration Manager mediante un doble clic en el archivo de script en el Explorador de Windows.  

 Tendrá que reiniciar el cliente para que la nueva configuración de este script surta efecto.  

##  <a name="a-namebkmkprovisiona-how-to-provision-client-installation-properties-group-policy-and-software-update-based-client-installation"></a><a name="BKMK_Provision"></a> Aprovisionamiento de propiedades de instalación de cliente (instalación de clientes con directivas de grupo y basada en actualizaciones de software)  
 Puede usar la directiva de grupo de Windows para aprovisionar los equipos en la empresa con las propiedades de instalación de cliente de Configuration Manager. Estas propiedades se almacenan en el Registro del equipo y se leen cuando se instala el software de cliente. Este procedimiento no suele ser necesario para Configuration Manager. Sin embargo, puede requerirse para algunos escenarios de instalación de cliente, como los siguientes:  

-   Usa la configuración de directiva de grupo o métodos de instalación de cliente basados en actualizaciones de software y no amplió el esquema de Active Directory para Configuration Manager.  

-   Desea reemplazar las propiedades de instalación de cliente en equipos específicos.  

> [!NOTE]  
>  Si las propiedades de instalación se incluyen en la línea de comandos de CCMSetup.exe, no se utilizarán las propiedades de instalación aprovisionadas en los equipos.  

 Se incluye una plantilla administrativa de directiva de grupo denominada ConfigMgrInstallation.adm en el medio de instalación de Configuration Manager, que se puede usar para aprovisionar equipos cliente con propiedades de instalación. Utilice el siguiente procedimiento para configurar y asignar esta plantilla a los equipos de su organización.  

#### <a name="to-configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Para configurar y asignar propiedades de instalación de cliente mediante un objeto de directiva de grupo  

1.  Importe la plantilla administrativa ConfigMgrInstallation.adm en un nuevo objeto de directiva de grupo, o en un objeto existente, mediante un editor como el Editor de objetos de directiva de grupo de Windows.  

    > [!NOTE]  
    >  Este archivo puede encontrarse en la carpeta **TOOLS\ConfigMgrADMTemplates** en los medios de instalación de Configuration Manager.  

2.  Abra las propiedades de la configuración importada **Configurar opciones de implementación de cliente**.  

3.  Haga clic en **Habilitar**.  

4.  En el cuadro **CCMSetup** , escriba las propiedades de línea de comandos de CCMSetup necesarias. Para ver la lista de todas las propiedades de la línea de comandos de CCMSetup y ejemplos de su uso, consulte [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (Acerca de las propiedades de instalación de cliente en System Center Configuration Manager).  

5.  Asigne el objeto de directiva de grupo a los equipos que quiera aprovisionar con las propiedades de instalación de cliente de Configuration Manager.  

 Para obtener información acerca de la directiva de grupo de Windows, consulte la documentación de Windows Server.  



<!--HONumber=Nov16_HO1-->


