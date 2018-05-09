---
title: Implementar clientes en Windows
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo implementar el cliente de Configuration Manager en equipos Windows.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5efca393afe2fc6441d074f987549228e7d0418f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>Implementar clientes en equipos Windows con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Antes de instalar los clientes de Configuration Manager, asegúrese de que todos los [requisitos previos](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) están en vigor y de que se completaron todas las configuraciones de implementación necesarias.   



##  <a name="BKMK_ClientPush"></a> Cómo instalar clientes con inserción de cliente  

Puede configurar la instalación de inserción de cliente para un sitio. La instalación de cliente se ejecuta automáticamente en los equipos detectados dentro de los límites configurados del sitio cuando estos se configuran como un grupo de límites. O bien, puede iniciar una instalación de inserción de cliente mediante la ejecución del Asistente para instalación de inserción de cliente para una recopilación o recurso específico dentro de una recopilación.  

También puede usar el Asistente para instalación de inserción de cliente para instalar el cliente de Configuration Manager a los resultados de [consulta](../../../core/servers/manage/queries-technical-reference.md). Para que la instalación se realice correctamente, uno de los elementos devueltos por la consulta debe ser el atributo **ResourceID** de la clase **Recurso del sistema**.   

Si el servidor de sitio no se puede poner en contacto con el equipo cliente ni iniciar el proceso de instalación, reintenta automáticamente la instalación cada hora. El servidor continúa intentándolo hasta un máximo de siete días.  

Para realizar el seguimiento del proceso de instalación de cliente, instale un punto de estado de reserva antes de instalar los clientes. Cuando se instala un punto de estado de reserva, se asigna automáticamente a los clientes cuando se instalan por el método de instalación de inserción de cliente. Para realizar el seguimiento del progreso de la instalación de cliente, vea los informes de implementación y asignación de cliente. 

Los archivos de registro de cliente proporcionan información más detallada sobre la solución de problemas. Los archivos de registro no requieren un punto de estado de reserva. Por ejemplo, el archivo **CCM.log** en el servidor de sitio registra todos los problemas del servidor de sitio cuando se conecta al equipo. El archivo **CCMSetup.log** en el cliente registra el proceso de instalación.  

> [!IMPORTANT]  
>  Para que la inserción de cliente se realice correctamente, asegúrese de que todos los requisitos previos están en vigor. Para obtener más información, vea [Dependencias de los métodos de instalación](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies).  

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Configurar el sitio para que use automáticamente la inserción de cliente para los equipos detectados

1.  En la consola de Configuration Manager, pulse **Administración** > **Configuración del sitio** > **Sitios**.  

3.  Seleccione el sitio para el que va a configurar la instalación de inserción de cliente automática en todo el sitio.  

4.  En la pestaña **Inicio**, en el grupo **Configuración**, pulse **Configuración de instalación de cliente** > **Instalación de inserción de cliente**.  

5.  En la pestaña **General** del cuadro de diálogo **Propiedades de instalación de inserción de cliente**, seleccione **Habilitar instalación de inserción de cliente automática en todo el sitio**. Seleccione los tipos de sistema en los que Configuration Manager debe insertar el software cliente.  

6.  Seleccione si quiere instalar el cliente en controladores de dominio.  

7.  En la pestaña **Cuentas**, especifique una o varias cuentas de Configuration Manager que se van a usar al conectarse al equipo de destino. Haga clic en el icono **Crear**, escriba el **Nombre de usuario** y **Contraseña** (inferior a 38 caracteres), confirme la contraseña y, después, haga clic en **Aceptar**. Especifique al menos una cuenta de instalación de inserción de cliente. Esta cuenta debe tener derechos de administrador local en el equipo de destino para instalar el cliente. Si no especifica al menos una cuenta de instalación de inserción de cliente, Configuration Manager intenta usar la cuenta de equipo de sistema de sitio. Se produce un error en la inserción de cliente entre dominios cuando se usa la cuenta de equipo de sistema de sitio.  
    > [!NOTE]  
    >  Para usar la inserción de cliente desde un sitio secundario, especifique la cuenta en el sitio secundario que inicia la inserción de cliente.  
    >   
    >  Para obtener más información sobre la cuenta de instalación de inserción de cliente, vea el procedimiento siguiente, [Usar el Asistente para instalación de inserción de cliente](#use-the-client-push-installation-wizard).  

8.  Complete la pestaña **Propiedades de instalación**.

     Si se amplía el esquema para Configuration Manager, el sitio publica en Active Directory Domain Services las [propiedades de instalación de cliente](../../../core/clients/deploy/about-client-installation-properties.md) que se especifiquen en esta pestaña. Las instalaciones de cliente leen estas propiedades cuando se ejecuta CCMSetup sin propiedades de instalación.  

    > [!NOTE]  
    >  Si se habilita la instalación de inserción de cliente en un sitio secundario, asegúrese de que la propiedad **SMSSITECODE** esté establecida en el nombre de sitio de Configuration Manager de su sitio primario principal. Si el esquema de Active Directory se extiende a Configuration Manager, también se puede establecer esta propiedad en AUTO para que busque automáticamente la asignación de sitio correcta.  

### <a name="use-the-client-push-installation-wizard"></a>Usar el Asistente para instalación de inserción de cliente

1.  En la consola de Configuration Manager, pulse **Administración** >  **Configuración del sitio** > **Sitios**.  

3.  Seleccione el sitio para el que va a configurar la instalación de inserción de cliente automática en todo el sitio.  

4.  En la pestaña **Inicio** > grupo **Configuración**, pulse **Configuración de instalación de cliente** > **Instalación de inserción de cliente**.  

5.  Complete la pestaña **Propiedades de instalación**.  

     Si se amplía el esquema para Configuration Manager, el sitio publica en Active Directory Domain Services las [propiedades de instalación de cliente](../../../core/clients/deploy/about-client-installation-properties.md) que se especifiquen en esta pestaña. Las instalaciones de cliente leen estas propiedades cuando se ejecuta CCMSetup sin propiedades de instalación.   

6.  En la consola de Configuration Manager, elija **Activos y compatibilidad**.  

7.  En el área de trabajo **Activos y compatibilidad** , seleccione uno o varios equipos o una recopilación de equipos.  

8.  En la pestaña **Inicio**, elija una de las opciones siguientes:  

    -   Si quiere instalar el cliente en un único equipo o en varios, en el grupo **Dispositivo**, pulse **Instalar cliente**.  

    -   Si quiere instalar el cliente en una recopilación de equipos, en el grupo **Recopilación**, pulse **Instalar cliente**.  

9. En la página **Antes de comenzar** del **Asistente para instalación de cliente**, revise la información y, después, pulse **Siguiente**.  

10. Complete la página **Opciones de instalación**.  

11. Revise la configuración de instalación y, a continuación, cierre el asistente.  

> [!NOTE]  
>  Se puede usar el asistente para instalar clientes incluso si el sitio no está configurado para la inserción de clientes.  



##  <a name="BKMK_ClientSUP"></a> Cómo instalar clientes con la instalación basada en actualizaciones de software  
 La instalación de clientes basada en actualizaciones de software publica el cliente en un punto de actualización de software como una actualización de software. Use este método para una actualización o instalación por primera vez.  

 Si un equipo tiene instalado el cliente de Configuration Manager, recibe la directiva de cliente desde el sitio. Esta directiva incluye el nombre del servidor de punto de actualización de software y el puerto desde el que se van a obtener las actualizaciones de software.   

> [!IMPORTANT]  
>  Para utilizar la instalación basada en actualizaciones de software, debe utilizar el mismo servidor de Windows Server Update Services (WSUS) para la instalación de cliente y actualizaciones de software. Este servidor debe ser el punto de actualización de software activo de un sitio primario. Para obtener más información, consulte [Install a software update point](../../../sum/get-started/install-a-software-update-point.md) (Instalar un punto de actualización de software).  

Si un equipo no tiene instalado el cliente de Configuration Manager, configure y asigne un objeto de directiva de grupo en Active Directory Domain Services para especificar el nombre de servidor del punto de actualización de software.  

No se pueden agregar propiedades de línea de comandos a una instalación de cliente basada en actualizaciones de software. Si se extendió el esquema de Active Directory a Configuration Manager, los equipos cliente consultan automáticamente las propiedades de instalación en Active Directory Domain Services cuando realizan la instalación.  

Si no se extendió el esquema de Active Directory, se puede usar la directiva de grupo para aprovisionar la configuración de instalación de cliente en el sitio. Esta configuración se aplica automáticamente a cualquier instalación de cliente basada en actualizaciones de software. Para obtener más información, vea [Cómo aprovisionar propiedades de instalación de cliente (instalación de cliente con directivas de grupo y basada en actualizaciones de software)](#BKMK_Provision) y [Cómo asignar clientes a un sitio en System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

Use los procedimientos siguientes para configurar equipos sin un cliente de Configuration Manager para usar el punto de actualización de software para la instalación de cliente y actualizaciones de software, y para publicar el software de cliente en el punto de actualización de software.  

> [!NOTE]  
>  Si los equipos se encuentran en un estado de reinicio pendiente tras una instalación de software previa, una instalación de clientes basada en actualizaciones de software podría provocar que el equipo se reinicie.  

### <a name="configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>Configure un objeto de directiva de grupo en Active Directory Domain Services para especificar el punto de actualización de software para la instalación de cliente y las actualizaciones de software:  

1.  Use la Consola de administración de directivas de grupo para abrir un objeto de directiva de grupo nuevo o existente.  

2.  En la consola, expanda **Configuración del equipo**, expanda **Plantillas administrativas** y **Componentes de Windows** y, después, pulse **Windows Update**.  

3.  Abra las propiedades de la configuración **Especificar la ubicación del servicio Windows Update en la intranet** y, después, pulse **Habilitado**.  

4.  En el cuadro **Establecer el servicio de actualización de la intranet para detectar actualizaciones**, especifique el nombre y el puerto del servidor de punto de actualización de software:  

    -   Si el sistema de sitio de Configuration Manager está configurado para usar un nombre de dominio completo (FQDN), use el formato de FQDN.  

    -   Si el sistema de sitio de Configuration Manager no está configurado para usar un FQDN, use un formato de nombre corto.  

    > [!NOTE]  
    >  Para determinar el número de puerto, vea [Configuración del puerto de WSUS](../../../sum/plan-design/plan-for-software-updates.md).  

     Ejemplo: **http://server1.contoso.com:8530**  

5.  En el cuadro **Establecer el servidor de estadísticas de la intranet**, especifique el nombre del servidor de estadísticas de la intranet. No tiene que ser el mismo que el servidor de punto de actualización de software. Si es el mismo servidor, no es necesario que el formato coincida.  

6.  Asigne el objeto de directiva de grupo a los equipos en los que se quiere instalar el cliente y recibir actualizaciones de software.  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Publicar el cliente de Configuration Manager en el punto de actualización de software  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración del sitio** > **Sitios**.  

3.  Seleccione el sitio para el que va a configurar la instalación de cliente basada en actualizaciones de software.  

4.  En la pestaña **Inicio**, en el grupo **Configuración**, pulse **Configuración de instalación de cliente** y, después, pulse **Instalación de cliente basada en actualizaciones de software**.  

5.  Seleccione **Habilitar instalación de cliente basada en actualizaciones de software**.  

6.  Si el software cliente del servidor de sitio de Configuration Manager es una versión posterior a la del punto de actualización de software, se abre el cuadro de diálogo **Se detectó una versión más reciente del paquete de cliente**. Haga clic en **Sí** para publicar la versión más reciente.  

    > [!NOTE]  
    >  Si el software cliente no se ha publicado anteriormente en el punto de actualización de software, este cuadro está en blanco.  

La actualización de software para el cliente de Configuration Manager no se actualiza automáticamente cuando hay una versión nueva. Si se actualiza el sitio, lo que incluye una versión de cliente nueva, se debe repetir este procedimiento y hacer clic en **Sí** para el paso 6.  



##  <a name="BKMK_ClientGP"></a> Cómo instalar clientes con directiva de grupo  
 Se puede usar una directiva de grupo de Active Directory Domain Services para publicar o asignar el cliente de Configuration Manager para instalarlo en los equipos de la empresa. El cliente se instala cuando se inicia el equipo. Cuando se usa la directiva de grupo, el cliente se muestra en **Agregar o quitar programas** del Panel de Control para que el usuario lo instale.  

 Use el paquete de Windows Installer (CCMSetup.msi) para instalaciones basadas en directiva de grupo. Este archivo se encuentra en la carpeta **&lt;directorio de instalación de ConfigMgr\>\bin\i386** en el servidor de sitio de Configuration Manager. No se pueden agregar propiedades a este archivo para modificar el comportamiento de la instalación.  

> [!IMPORTANT]  
>  Es necesario tener permisos de administrador para tener acceso a los archivos de instalación del cliente.  

-   Si el esquema de Active Directory se extiende para Configuration Manager y se selecciona **Publish this site in Active Directory Domain Services** (Publicar este sitio en Active Directory Domain Services) en la pestaña **Avanzadas** del cuadro de diálogo **Propiedades del sitio**, los equipos cliente buscan automáticamente en Active Directory Domain Services las propiedades de instalación. Para obtener más información sobre las propiedades de instalación publicadas, vea [Acerca de las propiedades de instalación de cliente publicadas en Active Directory Domain Services](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

-   Si no se ha ampliado el esquema de Active Directory, se puede usar el procedimiento de este tema para almacenar las propiedades de instalación en el Registro de los equipos: [Cómo aprovisionar propiedades de instalación de cliente (instalación de cliente con directivas de grupo y basada en actualizaciones de software)](#BKMK_Provision). Estas propiedades de instalación se usan cuando se instala el cliente.  

Para obtener información sobre cómo usar una directiva de grupo en Active Directory Domain para instalar software, consulte la documentación de Windows Server.  



##  <a name="BKMK_Manual"></a> Cómo instalar clientes manualmente  
 Es posible instalar manualmente el software cliente en los equipos de su empresa mediante el programa CCMSetup.exe. Este programa y los archivos auxiliares se encuentran en la carpeta **Cliente** de la carpeta de instalación de Configuration Manager del servidor de sitio y en los puntos de administración de su sitio. Esta carpeta se comparte en la red como  

 \\\\*&lt;Nombre del servidor de sitio\>* \SMS_*&lt;Código de sitio\>* \Client\  

 donde *&lt;Nombre del servidor de sitio\>* es el nombre de uno de los servidores que hospedan un punto de administración y *&lt;Código de sitio\>* es el código del sitio primario al que se asigna el cliente. Para ejecutar CCMSetup.exe desde la línea de comandos en el cliente, debe asignar una unidad de red a esta ubicación y luego ejecutar el comando.  

> [!IMPORTANT]  
>  Es necesario tener permisos de administrador para tener acceso a los archivos de instalación del cliente.  

 CCMSetup.exe copia todos los requisitos previos necesarios en el equipo cliente y llama al paquete de Windows Installer (Client.msi) para instalar el cliente. No se puede ejecutar Client.msi directamente.  

 Es posible especificar propiedades de línea de comandos para CCMSetup.exe y Client.msi para modificar el comportamiento de la instalación del cliente. Asegúrese de especificar las propiedades de CCMSetup (las propiedades que comienzan por **/**) antes de especificar las propiedades de Client.msi. Por ejemplo:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`    

y el cliente se instala mediante las propiedades siguientes:  

|Propiedad|Descripción|  
|--------------|-----------------|  
|**/mp:SMSMP01**|Esta propiedad de CCMSetup especifica que el punto de administración SMSMP01 descargue los archivos de instalación de cliente requeridos.|  
|**/logon**|Esta propiedad de CCMSetup especifica que la instalación se debe detener si se encuentra un cliente de Configuration Manager en el equipo.|  
|**SMSSITECODE=AUTO**|Esta propiedad de Client.msi especifica que el cliente intenta localizar el código de sitio de Configuration Manager que va a usar, por ejemplo, mediante Active Directory Domain Services.|  
|**FSP=SMSFP01**|Esta propiedad de Client.msi especifica que el punto de estado de reserva denominado SMSFP01 se usa para recibir mensajes de estado enviados desde el equipo cliente.|  

 Para obtener más información sobre todas las propiedades de CCMSetup.exe, vea [Acerca de las propiedades de instalación de cliente](../../../core/clients/deploy/about-client-installation-properties.md).  

> [!Tip]  
> Para el procedimiento de instalación del cliente de Configuration Manager en un dispositivo Windows 10 moderno mediante identidades de Azure AD, vea [Instalación y asignación de clientes Windows 10 para Configuration Manager mediante la autenticación basada en Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Ese procedimiento es para los clientes en la intranet o Internet.  


### <a name="examples"></a>Ejemplos
 Estos ejemplos son para los clientes de Active Directory en la intranet. Usan los valores siguientes para representar diferentes aspectos del sitio:  

 **MPSERVER** = servidor que hospeda el punto de administración   
**FSPSERVER** = servidor que hospeda el punto de estado de reserva  
**ABC** = código de sitio  
**contoso.com** = nombre de dominio  

 Todos los servidores de sistema de sitio se configuran con un FQDN de intranet. El sitio se publica en el bosque de Active Directory del cliente.  

 En el equipo cliente, inicie sesión como administrador local, asigne una unidad (z:) a \\\\MPSERVER\SMS_ABC\Client, cambie el símbolo del sistema a la unidad z y luego ejecute uno de los comandos siguientes:  

 **Ejemplo 1:**  

`CCMSetup.exe`  

En este ejemplo se instala el cliente sin propiedades adicionales. El cliente se configura automáticamente con las propiedades de instalación de Active Directory Domain Services. Se configura automáticamente para las opciones siguientes: 
- Código de sitio. Esta configuración requiere que la ubicación de red del cliente se incluya en un grupo de límites configurado para la asignación de cliente. 
- Punto de administración
- Punto de estado de reserva
- Comunicación solo mediante HTTPS  
  
Para obtener más información, vea [Acerca de las propiedades de instalación de cliente publicadas en Active Directory Domain Services](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 **Ejemplo 2:**  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
En este ejemplo se reemplaza la configuración automática que proporciona Active Directory Domain Services. No requiere que la ubicación de red del cliente esté incluida en un grupo de límites configurado para la asignación de cliente. En su lugar, la instalación especifica los valores siguientes:
- Código de sitio
- Punto de administración de intranet 
- Punto de administración basado en Internet
- Punto de estado de reserva que acepta conexiones desde Internet
- Usar un certificado PKI de cliente (si está disponible) con el período de validez más largo  



##  <a name="BKMK_ClientLogonScript"></a> Cómo instalar clientes con scripts de inicio de sesión  
 Configuration Manager admite scripts de inicio de sesión para instalar el software de cliente de Configuration Manager. Puede utilizar el archivo de programa **CCMSetup.exe** en un script de inicio de sesión para activar la instalación del cliente.  

 La instalación del script de inicio de sesión utiliza los mismos métodos que la instalación manual del cliente. Se puede especificar la propiedad de instalación **/logon** para CCMSsetup.exe. Si ya existe una versión del cliente en el equipo, esta propiedad evita que el cliente se instale. Este comportamiento impide que se vuelva a instalar el cliente cada vez que se ejecute el script de inicio de sesión.  

 Si no se especifica ningún origen de instalación mediante la propiedad **/Source** ni ningún punto de administración del que obtener la instalación mediante la propiedad **/MP**, CCMSetup.exe localiza el punto de administración buscando en Active Directory Domain Services. Este comportamiento solo se produce si el esquema se ha ampliado para Configuration Manager y el sitio está publicado en Active Directory Domain Services. Como alternativa, el cliente puede utilizar DNS o WINS para localizar un punto de administración.  



##  <a name="BKMK_ClientApp"></a> Cómo instalar clientes con un paquete y un programa  
 Es posible usar Configuration Manager para crear e implementar un paquete y un programa que actualice el software cliente para equipos seleccionados de la jerarquía. Con Configuration Manager se suministra un archivo de definición del paquete que rellena las propiedades del paquete con los valores que se suelen usar. Se puede personalizar el comportamiento de la instalación del cliente mediante la especificación de propiedades de línea de comandos adicionales.  

> [!NOTE]  
>  No puede actualizar clientes de Configuration Manager 2007 con este método. En su lugar, utilice la actualización de cliente automática, que automáticamente crea e implementa un paquete que contiene la versión más reciente del cliente. Para obtener más información, vea [Actualizar clientes](../../../core/clients/manage/upgrade/upgrade-clients.md).  
>   
>  Para obtener más información sobre cómo migrar desde versiones anteriores del cliente de Configuration Manager, vea [Planear una estrategia de migración de clientes](../../../core/migration/planning-a-client-migration-strategy.md).  

 
### <a name="create-a-package-and-program-for-the-client-software"></a>Crear un paquete y un programa para el software cliente  

Use el procedimiento siguiente para crear un paquete y un programa de Configuration Manager que pueda implementar en equipos cliente de Configuration Manager para actualizar el software cliente.  

1.  En la consola de Configuration Manager, seleccione **Biblioteca de software** > **Administración de aplicaciones** > **Paquetes**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear paquete a partir de definición**.  

4.  En la página **Definición de paquete** del asistente, seleccione **Microsoft** en la lista desplegable **Editor** y seleccione **Actualización de cliente de Configuration Manager** en la lista **Definición de paquete**.  

5.  En la página **Archivos de origen**, seleccione **Obtener siempre los archivos de la carpeta de origen**.  

6.  En la página **Carpeta de origen**, seleccione **Ruta de red (nombre UNC)**. Después, escriba la ruta de acceso de red al equipo y la carpeta que contiene los archivos de instalación de cliente.  

    > [!NOTE]  
    >  El equipo en el que se ejecuta la implementación de Configuration Manager debe tener acceso a la carpeta de red especificada; en caso contrario se produce un error en la instalación.  

    Para cambiar alguna de las propiedades de instalación de cliente, modifique los parámetros de la línea de comandos de CCMSetup.exe en la pestaña **General** del cuadro de diálogo del programa **Propiedades de actualización silenciosa de agente de Configuration Manager**. Las propiedades de instalación predeterminadas son **/noservice SMSSITECODE=AUTO**.  

9. Distribuya el paquete a todos los puntos de distribución en los que desea hospedar el paquete de actualización de cliente. A continuación, puede implementar el paquete en recopilaciones de equipos que contengan los clientes que quiere actualizar.  



## <a name="bkmk_mdm"></a>Cómo instalar clientes en dispositivos Windows administrados por MDM con Intune

Puede implementar los archivos de instalación de cliente en equipos inscritos con Microsoft Intune. 

Este procedimiento es para un cliente tradicional que está conectado a la intranet. Usa métodos de autenticación de cliente tradicionales. Para asegurarse de que el dispositivo permanece en un estado administrado después de instalar el software cliente, el dispositivo debe encontrarse en la intranet y dentro de los límites del sitio de Configuration Manager.  

Para el procedimiento de instalación del cliente de Configuration Manager en un dispositivo Windows 10 moderno mediante identidades de Azure AD, vea [Instalación y asignación de clientes Windows 10 para Configuration Manager mediante la autenticación basada en Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

> [!NOTE]
> Una vez instalado el software cliente, se anula la inscripción del dispositivo en Intune.
> 
> A partir de la versión 1710, no se anula la inscripción de los clientes de Intune. Pueden tener el cliente de Configuration Manager y la inscripción de MDM al mismo tiempo. Para obtener más información, vea [Administración conjunta para dispositivos de Windows 10](/sccm/core/clients/manage/co-management-overview).

###  <a name="install-clients-with-intune"></a>Instalar clientes con Intune:

1. En Intune, [cree una aplicación](/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune) que contenga el archivo de instalación de cliente de Configuration Manager **ccmsetup.msi**. Este archivo se encuentra en la carpeta **&lt;directorio de instalación de ConfigMgr\>\bin\i386** en el servidor de sitio de Configuration Manager.

2. En el editor de software de Intune, escribe los parámetros de línea de comandos. Por ejemplo, use la línea de comandos siguiente con un cliente tradicional en la intranet:

  `CCMSETUPCMD="/MP:&lt;FQDN of management point> SMSMP=&lt;FQDN of management point> SMSSITECODE=&lt;Your site code> DNSSUFFIX=&lt;DNS Suffix of management point>"`  

   > [!Note]  
   > Para obtener una línea de comandos de ejemplo para usar con un cliente de Windows 10 moderno mediante autenticación de Azure AD, vea [Preparar dispositivos de Windows 10 para la administración conjunta](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).

3. [Implemente la aplicación](/intune/deploy-use/deploy-apps-in-microsoft-intune) en los equipos Windows inscritos.



##  <a name="BKMK_ClientImage"></a> Cómo instalar clientes con una imagen de equipo  
Se puede preinstalar el software cliente de Configuration Manager en un equipo de referencia que se use para crear una imagen de SO.   

> [!Important]
> Al usar la secuencia de tareas de Configuration Manager para implementar la imagen de SO, el paso de secuencia de comandos [Preparar el cliente de Configuration Manager](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) quita completamente el cliente de Configuration Manager. 

### <a name="prepare-the-client-computer-for-imaging"></a>Preparar el equipo cliente para la creación de imágenes  

1.  Instale manualmente el software de cliente de Configuration Manager en el equipo de referencia. Para obtener más información, vea [Instalación manual de clientes de Configuration Manager](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  No especifique un código de sitio de Configuration Manager para el cliente en las propiedades de línea de comandos de CCMSetup.exe.  

2.  En una línea de comandos, escriba `net stop ccmexec` para asegurarse de que el servicio **Host de agente de SMS** (Ccmexec.exe) no se ejecuta en el equipo de referencia.
3.  Elimine el archivo **SMSCFG.INI** de la carpeta **Windows** del equipo de referencia.  
3.  Quite todos los certificados almacenados en el almacén del equipo local en el equipo de referencia. Por ejemplo, si utiliza certificados de infraestructura de clave pública (PKI), debe quitar los certificados en el almacén **Personal** para **Equipo** y **Usuario** antes de crear la imagen del equipo.

4.  Si los clientes están instalados en otra jerarquía de Configuration Manager que la del equipo de referencia, quite la clave raíz confiable del equipo de referencia.  
    > [!NOTE]  
    >  Si los clientes no pueden consultar los Servicios de dominio de Active Directory para localizar un punto de administración, utilizan la clave raíz de confianza para determinar los puntos de administración de confianza. Si todos los clientes con imágenes están implementados en la misma jerarquía que el equipo maestro, deje la clave raíz confiable. Si los clientes están implementados en jerarquías distintas, quite la clave raíz confiable. Aprovisione también estos clientes con la nueva clave raíz confiable. Para obtener más información, consulte [Planeación de la clave raíz confiable](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK). 

5.  Utilice software de creación de imágenes para capturar la imagen del equipo maestro.  

6.  Implemente la imagen en equipos de destino.  



##  <a name="BKMK_ClientWorkgroup"></a> Cómo instalar clientes en equipos del grupo de trabajo  
 Configuration Manager admite la instalación de cliente para equipos del grupo de trabajo. Instale el cliente en los equipos del grupo de trabajo mediante el método especificado en [Instalación manual de clientes de Configuration Manager](#BKMK_Manual).  

 Requisitos previos:  

-   El cliente debe instalarse manualmente en cada equipo del grupo de trabajo. Durante la instalación, el usuario que ha iniciado sesión debe tener derechos de administrador local.  

-   Con el fin de obtener acceso a recursos en el dominio de servidor del sitio de Configuration Manager, la cuenta de acceso de red debe estar configurada para el sitio. Especifique esta cuenta como una propiedad del componente de distribución de software. Para obtener más información, consulte [Componentes de sitio para System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

 Limitaciones:  

-   Los clientes del grupo de trabajo no pueden encontrar puntos de administración desde los Servicios de dominio de Active Directory y, en su lugar, deben utilizar DNS, WINS u otro punto de administración.  

-   No se admite la itinerancia global, ya que los clientes no pueden consultar los Servicios de dominio de Active Directory para obtener información del sitio.  

-   Los métodos de detección de Active Directory no pueden detectar equipos en los grupos de trabajo.  

-   No se puede implementar software para usuarios de equipos del grupo de trabajo.  

-   No se puede utilizar el método de instalación de inserción de cliente para instalar al cliente en equipos del grupo de trabajo.  

-   Los clientes del grupo de trabajo no pueden usar Kerberos para autenticación, por lo que podrían requerir la aprobación manual.  

-   No se puede configurar un cliente de grupo de trabajo como punto de distribución. Configuration Manager requiere que los equipos de punto de distribución pertenezcan a un dominio.  

### <a name="install-the-client-on-workgroup-computers"></a>Instalar el cliente en equipos del grupo de trabajo  

Compruebe los requisitos previos y, después, siga las instrucciones de la sección [Cómo instalar clientes manualmente](#BKMK_Manual).  

   En este ejemplo se instala al cliente para la administración de cliente de intranet y se especifica el código de sitio y el sufijo DNS para localizar un punto de administración. `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     

   En este ejemplo se requiere que el cliente se encuentre en una ubicación de red configurada en un grupo de límites. Este requisito es para que la asignación automática de sitio se pueda realizar correctamente. El comando incluye un punto de estado de reserva en el servidor FSPSERVER. Esta propiedad ayuda a realizar el seguimiento de la implementación de cliente y a identificar cualquier problema comunicación del cliente. 
   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a> Cómo instalar clientes para la administración de cliente basada en Internet  
 
> [!Note]
> Esta sección no se aplica a los clientes que usan una instancia de [Cloud Management Gateway](/sccm/core/clients/manage/plan-cloud-management-gateway). Para instalar clientes basados en Internet mediante una instancia de Cloud Management Gateway, vea [Instalación y asignación de clientes Windows 10 para Configuration Manager mediante la autenticación basada en Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

Si el sitio de Configuration Manager admite la [administración de cliente basada en Internet](/sccm/core/clients/manage/plan-internet-based-client-management) para clientes que a veces se encuentran en la intranet y a veces en Internet, dispone de dos opciones para instalar clientes en la intranet:  

-   Puede incluir la propiedad Client.msi de CCMHOSTNAME=*&lt;FQDN de Internet del punto de administración basado en Internet\>* al instalar el cliente, por ejemplo, mediante instalación manual o inserción de cliente. Cuando se utiliza este método, también debe asignar directamente el cliente al sitio y no se puede utilizar la asignación automática de sitio. En la sección [Cómo instalar clientes manualmente](#BKMK_Manual) de este tema se proporciona un ejemplo de este método de configuración.  

-   Puede instalar el cliente para la administración de cliente de intranet y después asignar un punto de administración de cliente basado en Internet al cliente. Cambie el punto de administración mediante las propiedades de cliente de Configuration Manager en el Panel de control, o bien mediante un script. Cuando utilice este método, puede utilizar la asignación automática de cliente. Para obtener más información, vea la sección [Cómo configurar clientes para la administración de cliente basada en Internet después de la instalación de cliente](#BKMK_ConfigureIBCM_MP) de este tema.  

 Si tiene que instalar clientes que están en Internet, elija uno de los siguientes métodos admitidos:  

-   Proporcione un mecanismo para que estos clientes se conecten temporalmente a la intranet con una VPN. Después, instale el cliente mediante cualquier método de instalación de cliente adecuado.  

-   Use un método de instalación independiente de Configuration Manager. Por ejemplo, empaquete los archivos de origen de instalación de cliente en medios extraíbles que se puedan enviar a los usuarios para que realicen la instalación con instrucciones. Los archivos de origen de instalación de cliente están ubicados en la carpeta *&lt;rutaDeInstalación\>* \Client, en el servidor de sitio de Configuration Manager y en los puntos de administración. Incluya un script en los medios para copiarlo manualmente en la carpeta de cliente y, desde esta carpeta, instale el cliente mediante CCMSetup.exe y todas las propiedades de línea de comandos apropiadas de CCMSetup.  

> [!NOTE]  
>  Configuration Manager no admite la instalación de un cliente directamente desde el punto de administración basado en Internet ni desde el punto de actualización de software basado en Internet.  

 Los clientes que se administran a través de Internet se deben comunicar con sistemas de sitio basados en Internet. Asegúrese de que estos clientes también disponen de certificados de infraestructura de clave pública (PKI) antes de instalar al cliente. Instale estos certificados con independencia de Configuration Manager. Para obtener más información sobre los requisitos de certificado, vea [Requisitos de certificados PKI](../../../core/plan-design/network/pki-certificate-requirements.md).  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Instalar clientes en Internet mediante la especificación de propiedades de línea de comandos de CCMSetup  

1.  Siga las instrucciones de la sección [Cómo instalar clientes manualmente](#BKMK_Manual) e incluya siempre lo siguiente:  

    -   Propiedad de línea de comandos de CCMSetup **/source:***&lt;ruta de acceso local a la carpeta de cliente copiada\>*  

    -   Propiedad de línea de comandos de CCMSetup **/UsePKICert**  

    -   Propiedad de Client.msi **CCMHOSTNAME=***&lt;FQDN del punto de administración basado en Internet\>*  

    -   Propiedad de Client.msi **SMSSIGNCERT=***&lt;ruta de acceso local al certificado que firma el servidor de sitio exportado\>*  

    -   Propiedad de Client.msi **SMSSITECODE=***&lt;código de sitio del punto de administración basado en Internet\>*  

    > [!NOTE]  
    >  Si el sitio tiene más de un punto de administración basado en Internet, no importa cuál se especifique para la propiedad CCMHOSTNAME. Cuando un cliente de Configuration Manager se conecta al punto de administración basado en Internet especificado, el punto de administración envía al cliente una lista de los puntos de administración basados en Internet disponibles en el sitio. El cliente selecciona uno de la lista de manera aleatoria.  

2.  Si no desea que el cliente compruebe la lista de revocación de certificados (CRL), especifique la propiedad de línea de comandos de CCMSetup **/NoCRLCheck**.  

3.  Si se usa un punto de estado de reserva basado en Internet, especifique la propiedad de Client.msi **FSP=***&lt;FQDN de Internet del punto de estado de reserva basado en Internet\>*.  

4.  Si va a instalar el cliente para la administración de cliente solo de Internet, especifique la propiedad de Client.msi **CCMALWAYSINF=1**.  

5.  Compruebe si tiene que especificar propiedades de línea de comandos de CCMSetup adicionales. Por ejemplo, es posible que tenga que especificar un criterio de selección de certificado si el cliente tiene más de un certificado válido de PKI. Para obtener una lista de las propiedades disponibles, vea [Acerca de las propiedades de instalación de clientes en System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

   Ejemplo:  
   `CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

   En este ejemplo se instala el cliente con los comportamientos siguientes:
   - Usar archivos de origen de una carpeta en la unidad D.
   - Usar un certificado PKI de cliente. 
   - Seleccionar el certificado con el mayor período de validez. 
   - Administración de cliente solo de Internet.
   - Asignar el cliente para usar el punto de administración basado en Internet denominado SERVER1.
   - Asignar el punto de estado de reserva basado en Internet en el dominio contoso.com.
   - Asignar al cliente al sitio ABC.  

###  <a name="BKMK_ConfigureIBCM_MP"></a>Para configurar clientes para la administración de cliente basada en Internet después de la instalación de cliente  
 Para asignar el punto de administración basado en Internet después de instalar el cliente, use uno de estos procedimientos. El primero necesita una configuración manual y es apropiado para pocos clientes. El segundo es más apropiado para configurar muchos clientes.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>Configurar clientes para la administración de clientes basados en Internet después de la instalación de cliente mediante la asignación del punto de administración basado en Internet en propiedades de Configuration Manager  

1.  Navegue a **Configuration Manager** en el Panel de Control del equipo cliente y, a continuación, haga doble clic para abrir sus propiedades.  

2.  En la pestaña **Internet**, escriba el nombre de dominio completo del punto de administración basado en Internet en el cuadro de texto FQDN de Internet.  

    > [!NOTE]  
    >  La pestaña **Internet** solo está disponible si el cliente tiene un certificado de PKI de cliente.  

3.  Si el cliente va a tener acceso a Internet mediante un servidor proxy, escriba la configuración del servidor proxy.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Configurar clientes para la administración de cliente basada en Internet después de la instalación de cliente mediante un script  

1.  Abra un editor de texto, como el Bloc de notas.  

2.  Copie e inserte el ejemplo de VBScript siguiente en el archivo. Reemplace *mp.contoso.com* por el FQDN de Internet del punto de administración basado en Internet.  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the internet-based management point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  Si tiene que eliminar un punto de administración basado en Internet específico para que el cliente no se configure para usar un punto de administración basado en Internet, quite el valor dentro de las comillas para que esta línea sea: `newInternetBasedManagementPointFQDN = ""`.  

4.  Guarde el archivo con una extensión .vbs.  

5.  Use cscript.exe para ejecutar el script en los equipos cliente, mediante uno de los métodos siguientes:  

    -   Implemente el archivo en clientes de Configuration Manager existentes mediante un paquete y un programa.  

    -   Ejecute el archivo localmente en los clientes existentes de Configuration Manager mediante un doble clic en el archivo de script en el Explorador de Windows.  

 Tendrá que reiniciar el cliente para que los cambios surtan efecto.  



##  <a name="BKMK_Provision"></a> Cómo aprovisionar propiedades de instalación de cliente (instalación de cliente con directivas de grupo y basada en actualizaciones de software)  
 Puede usar la directiva de grupo de Windows para aprovisionar los equipos con las propiedades de instalación de cliente de Configuration Manager. Estas propiedades se almacenan en el Registro del equipo y se leen cuando se instala el software de cliente. Normalmente, este procedimiento no es necesario, pero es posible que se necesite en algunos escenarios de instalación de cliente como:  

-   Se está usando la configuración de directiva de grupo o métodos de instalación de cliente basados en actualizaciones de software. No se ha ampliado el esquema de Active Directory para Configuration Manager.  

-   Desea reemplazar las propiedades de instalación de cliente en equipos específicos.  

> [!NOTE]  
>  Si se proporcionan propiedades de instalación en la línea de comandos de CCMSetup.exe, no se usan las propiedades de instalación aprovisionadas en los equipos.  

 En el medio de instalación de Configuration Manager se proporciona una plantilla administrativa de directiva de grupo denominada ConfigMgrInstallation.adm. Esta plantilla se puede usar para aprovisionar equipos cliente con propiedades de instalación.   

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Configurar y asignar propiedades de instalación de cliente mediante un objeto de directiva de grupo  

1.  Importe la plantilla administrativa ConfigMgrInstallation.adm en un objeto de directiva de grupo nuevo o existente, mediante un editor como el Editor de objetos de directiva de grupo de Windows. El archivo puede encontrarse en la carpeta **TOOLS\ConfigMgrADMTemplates** en los medios de instalación de Configuration Manager.  

2.  Abra las propiedades de la configuración importada **Configurar opciones de implementación de cliente**.  

3.  Pulse **Habilitado**.  

4.  En el cuadro **CCMSetup** , escriba las propiedades de línea de comandos de CCMSetup necesarias. Para obtener una lista de las propiedades de la línea de comandos de CCMSetup y ejemplos de su uso, vea [Acerca de las propiedades de instalación de clientes en System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

5.  Asigne el objeto de directiva de grupo a los equipos que quiera aprovisionar con las propiedades de instalación de cliente de Configuration Manager.  

Para obtener información sobre la directiva de grupo de Windows, consulte la documentación de Windows Server.  



## <a name="next-steps"></a>Pasos siguientes
Para obtener ayuda para la instalación del cliente de Configuration Manager, vea [Métodos de instalación de cliente en System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).