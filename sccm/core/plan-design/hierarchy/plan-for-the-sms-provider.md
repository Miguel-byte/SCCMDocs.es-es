---
title: Planear el proveedor de SMS | Microsoft Docs
description: "Obtenga información sobre cómo el proveedor de SMS le ayuda a administrar System Center Configuration Manager."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 11ac851696ce52642412ca29e4873679d50cf398
ms.openlocfilehash: 547dc39d5659c7c2e6f1ca670caddc127dbf22c4


---
# <a name="plan-for-the-sms-provider-for-system-center-configuration-manager"></a>Plan para el proveedor de SMS de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Para administrar System Center Configuration Manager, use una consola de Configuration Manager que se conecte a una instancia del **proveedor de SMS**. De forma predeterminada, se instala un proveedor de SMS en el servidor de sitio al instalar un sitio de administración central o sitio primario. 


##  <a name="a-namebkmkplansmsprova-about-the-sms-provider"></a><a name="BKMK_PlanSMSProv"></a> Acerca del proveedor de SMS  
 El proveedor de SMS es un proveedor de Instrumental de administración de Windows (WMI) que asigna acceso de **lectura** y **escritura** a la base de datos de Configuration Manager en un sitio:  

-   Cada sitio de administración central y cada sitio principal requiere al menos un proveedor de SMS. Puede instalar a proveedores adicionales según sea necesario.  
-   El grupo de seguridad **Administradores de SMS** permite acceder al proveedor de SMS. Configuration Manager crea automáticamente este grupo en el servidor de sitio y en todos los equipos donde instale una instancia del proveedor de SMS.  

-   Los sitios secundarios no admiten el proveedor de SMS.  


Los usuarios administrativos de Configuration Manager usan un proveedor de SMS para acceder a la información almacenada en la base de datos. Para hacerlo, los administradores pueden usar la consola de Configuration Manager, el Explorador de recursos, herramientas y scripts personalizados. El proveedor de SMS no interactúa con clientes de Configuration Manager. Cuando una consola de Configuration Manager se conecta a un sitio, consulta a WMI en el servidor de sitio para localizar una instancia del proveedor de SMS que usar.  

 El proveedor de SMS ayuda a reforzar la seguridad de Configuration Manager. Devuelve solo la información que el usuario administrativo que se está ejecutando la consola de Configuration Manager está autorizado a ver.  

> [!IMPORTANT]  
>  Cuando todos los equipos que contienen un proveedor de SMS para un sitio están sin conexión, las consolas de Configuration Manager no se pueden conectar a la base de datos de ese sitio.  

 Para obtener información sobre cómo administrar el proveedor de SMS, consulte [Administrar el proveedor de SMS](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) en [Modificar la infraestructura de System Center Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md).  

## <a name="prerequisites-to-install-the-sms-provider"></a>Requisitos previos para instalar el proveedor de SMS  

 Para admitir el proveedor de SMS:  

-   Es necesario que el equipo esté en un dominio que tenga una relación de confianza bidireccional con el servidor de sitio y los sistemas de sitio de la base de datos del sitio.  

-   El equipo no puede tener un rol de sistema de sitio de un sitio diferente.  

-   El equipo no puede tener un proveedor de SMS de cualquier sitio.  

-   El equipo debe ejecutarse en un sistema operativo que sea compatible con un servidor de sitio.  

-   El equipo debe tener al menos 650 MB de espacio libre en disco para admitir los componentes del Kit de implementación automatizada de Windows (Windows ADK) que se instalan con el proveedor de SMS. Para más información sobre Windows ADK y el proveedor de SMS, consulte [Requisitos de implementación de sistema operativo del proveedor de SMS](#BKMK_WAIKforSMSProv) en este tema.  

##  <a name="a-namebkmklocationa-sms-provider-locations"></a><a name="bkmk_location"></a> Ubicaciones del proveedor de SMS  
 Al instalar un sitio, instalará automáticamente el primer proveedor de SMS para el sitio. Puede especificar cualquiera de las siguientes ubicaciones compatibles para el proveedor de SMS:  

-   El equipo de servidor de sitio  

-   El equipo de base de datos del sitio  

-   Un equipo de clase de servidor que no tiene un proveedor de SMS, o un rol de sistema de sitio de un sitio diferente  


Para ver las ubicaciones de cada proveedor de SMS instalado en un sitio, seleccione la pestaña **General** del cuadro de diálogo **Propiedades** del sitio.  

 Cada proveedor de SMS admite conexiones simultáneas de varias solicitudes. Las únicas limitaciones de estas conexiones son el número de conexiones de servidor disponibles en el equipo proveedor de SMS y los recursos disponibles en el equipo proveedor de SMS para atender las solicitudes de conexión.  

 Una vez se ha instalado un sitio, puede volver a ejecutar el programa de instalación en el servidor de sitio para cambiar la ubicación de un proveedor de SMS existente, o para instalar proveedores de SMS adicionales en ese sitio. Solo puede instalar un proveedor de SMS en un equipo, y un equipo no puede instalar un proveedor de SMS de más de un sitio.  

 Utilice la siguiente información para identificar las ventajas y desventajas de instalar un proveedor de SMS en cada ubicación admitida:  

 **Servidor de sitio de Configuration Manager**  

-   **Ventajas:**  

    -   El proveedor de SMS no utiliza los recursos de sistema del equipo de base de datos de sitio.  

    -   Esta ubicación puede proporcionar un mejor rendimiento que un proveedor de SMS que se encuentre en un equipo que no sea el servidor de sitio o el equipo de base de datos de sitio.  

-   **Desventajas:**  

    -   El proveedor de SMS utiliza los recursos de red y de sistema que podrían estar dedicados a las operaciones de servidor de sitio.  


**SQL Server que aloja la base de datos del sitio**  

-   **Ventajas:**  

    -   El proveedor de SMS no utiliza recursos de sistema de sitio en el servidor de sitio.  

    -   Esta ubicación puede proporcionar el mejor rendimiento de las tres ubicaciones, si hay disponibles suficientes recursos de servidor.  

-   **Desventajas:**  

    -   El proveedor de SMS utiliza los recursos de red y de sistema que podrían estar dedicados a las operaciones de base de datos de sitio.  

    -   Cuando la base de datos del sitio está hospedada en una instancia en clúster de SQL Server, no se puede usar esa ubicación.  


**Equipo distinto al servidor de sitio o el equipo de base de datos de sitio**  

-   **Ventajas:**  

    -   El proveedor de SMS no utiliza recursos de servidor de sitio o de equipo de base de datos de sitio.  

    -   Este tipo de ubicación le permite implementar proveedores de SMS adicionales para proporcionar alta disponibilidad para las conexiones.  

-   **Desventajas:**  

    -   El rendimiento del proveedor de SMS puede reducirse debido a la actividad de red adicional necesaria para coordinar con el servidor de sitio y el equipo de base de datos del sitio.  

    -   Este servidor necesita ser siempre accesible para el equipo de base de datos del sitio y todos los equipos que tengan instalada la consola de Configuration Manager.  

    -   Esta ubicación puede utilizar recursos del sistema que de lo contrario se dedicarían a otros servicios.  

##  <a name="a-namebkmksmsprovlanguagesa-about-sms-provider-languages"></a><a name="BKMK_SMSProvLanguages"></a> Información sobre los idiomas del proveedor de SMS  
 El proveedor de SMS funciona independientemente del idioma de visualización del equipo donde está instalado.  

 Cuando un usuario administrativo o un proceso de Configuration Manager solicitan datos a través del proveedor de SMS, el proveedor de SMS intenta devolver los datos en un formato que coincida con el idioma del sistema operativo del equipo que realiza la solicitud.

La forma en la que intenta hacer coincidir el idioma es parcialmente indirecta. El proveedor de SMS no traduce la información de un idioma a otro. En su lugar, cuando los datos se devuelven para su visualización en la consola de Configuration Manager, el idioma de visualización de los datos depende del origen del objeto y del tipo de almacenamiento.  

 Cuando los datos de un objeto se almacenan en la base de datos, los idiomas que estarán disponibles dependen de lo siguiente:  

-   Los objetos creados por Configuration Manager se almacenan en la base de datos usando el soporte para varios idiomas. El objeto se almacena mediante el uso de los idiomas configurados en el sitio donde el objeto se crea al ejecutar el programa de instalación. Estos objetos se muestran en la consola de Configuration Manager en el idioma de visualización del equipo que realiza la solicitud, cuando ese idioma está disponible para el objeto. Si el objeto no se puede mostrar en el idioma de visualización del equipo que realiza la solicitud, se muestra en el idioma predeterminado, que es el inglés.  

-   Los objetos creados por un usuario administrativo se almacenan en la base de datos en el idioma que se utilizó para crear el objeto. Estos objetos se muestran en la consola de Configuration Manager en este mismo idioma. El proveedor de SMS no puede traducirlos y no tienen varias opciones de idioma.  

##  <a name="a-namebkmkmultismsprova-use-multiple-sms-providers"></a><a name="BKMK_MultiSMSProv"></a> Uso de proveedores de SMS múltiples  
 Cuando un sitio completa la instalación, puede instalar proveedores de SMS adicionales para el sitio. Para instalar proveedores de SMS adicionales, ejecute el programa de instalación de Configuration Manager en el servidor del sitio. Considere la posibilidad de instalar proveedores de SMS adicionales cuando se cumpla cualquiera de las siguientes condiciones:  

-   Tendrá varios usuarios administrativos que ejecutarán una consola de Configuration Manager y se conectarán a un sitio al mismo tiempo.  

-   Va a usar el SDK de Configuration Manager u otros productos, que podrían introducir frecuentan llamadas al proveedor de SMS.  

-   Desea garantizar una alta disponibilidad para el proveedor de SMS.  


Cuando se instalan varios proveedores de SMS en un sitio y se establece una solicitud de conexión, el sitio asigna de forma aleatoria cada nueva solicitud de conexión para que use un proveedor de SMS instalado. No se puede especificar la ubicación del proveedor de SMS para utilizarla con una sesión de conexión específica.  

> [!NOTE]  
>  Tenga en cuenta las ventajas e inconvenientes de cada ubicación de proveedor de SMS. Compare estas consideraciones con la información que no puede controlar el proveedor de SMS que se usará para cada nueva conexión.  

Por ejemplo, al conectar por primera vez una consola de Configuration Manager a un sitio, la conexión consulta a WMI en el servidor de sitio para identificar la instancia del proveedor de SMS que usará la consola. La consola de Configuration Manager mantiene en uso esta instancia específica del proveedor de SMS hasta que finaliza la sesión de la consola de Configuration Manager. Si la sesión finaliza porque el equipo del proveedor de SMS deja de estar disponible en la red, al volver a conectar la consola de Configuration Manager, el sitio repetirá la tarea de identificar una instancia del proveedor de SMS al que conectarse. Es posible que se asigne al mismo equipo de proveedor de SMS que no está disponible. Si esto ocurre, puede intentar volver a conectar la consola de Configuration Manager hasta que se asigne un equipo de proveedor de SMS disponible.  

##  <a name="a-namebkmkaboutsmsadminsa-about-the-sms-admins-group"></a><a name="BKMK_AboutSMSAdmins"></a> Acerca del grupo de administradores de SMS  
 Utilice el grupo de administradores de SMS para proporcionar acceso de usuario administrativo al proveedor de SMS. El grupo se crea automáticamente en el servidor de sitio cuando se instala el sitio, y en cada equipo que instala un proveedor de SMS. Aquí encontrará más información sobre el grupo Administradores de SMS:  

-   Cuando el equipo es un servidor miembro, se crea el grupo de administradores de SMS como un grupo local.  

-   Cuando el equipo es un controlador de dominio, se crea el grupo de administradores de SMS como un grupo local de dominio.  

-   Cuando se desinstala el proveedor de SMS de un equipo, el grupo de administradores de SMS no se quita del equipo.  


Antes de que un usuario pueda realizar una conexión correcta a un proveedor de SMS, su cuenta de usuario debe ser miembro del grupo de administradores de SMS. Cada usuario administrativo que se configure en la consola de Configuration Manager se agrega automáticamente al grupo de administradores de SMS de cada servidor de sitio y a cada equipo de proveedor de SMS de la jerarquía. Cuando se elimina un usuario administrativo de la consola de Configuration Manager, se quita ese usuario del grupo de administradores de SMS de cada servidor de sitio y de cada equipo proveedor de SMS de la jerarquía.  

Una vez que un usuario realiza una conexión correcta con el proveedor de SMS, la administración basada en roles determina los recursos de Configuration Manager a los que el usuario puede tener acceso o administrar.  

Puede ver y configurar permisos y derechos de grupo de administradores de SMS con el complemento MMC Control WMI. De forma predeterminada, **Todos** tiene permisos **Ejecutar métodos**, **Escritura de proveedor**y **Habilitar cuenta** . Cuando un usuario se conecta al proveedor de SMS, se le concederá acceso a los datos de la base de datos del sitio (según los derechos de seguridad administrativa basada en roles definidos en la consola de Configuration Manager). El grupo Administradores de SMS recibe de forma explícita los permisos **Habilitar cuenta** y **Llamada remota habilitada** en el espacio de nombres **Root\SMS**.  

> [!NOTE]  
>  Cada usuario administrativo que usa una consola de Configuration Manager remota requiere permisos de DCOM de activación remota en el equipo de servidor de sitio y en el equipo de proveedor de SMS. Aunque puede conceder estos derechos a cualquier usuario o grupo, le recomendamos que los conceda al grupo Administradores de SMS para simplificar la administración. Para obtener más información, consulte la sección [Configure DCOM permissions for remote Configuration Manager consoles](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) del tema [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) .  


##  <a name="a-namebkmksmsprovnamespacea-about-the-sms-provider-namespace"></a><a name="BKMK_SMSProvNamespace"></a> Información sobre el espacio de nombres del proveedor de SMS  
La estructura del proveedor de SMS se define por el esquema de WMI. Los espacios de nombres del esquema describen la ubicación de los datos de Configuration Manager dentro del esquema del proveedor de SMS. La tabla siguiente contiene algunos de los espacios de nombres comunes utilizados por el proveedor de SMS.  

|Espacio de nombres|Descripción|  
|---------------|-----------------|  
|Root\SMS\site_*&lt;código de sitio\>*|El proveedor de SMS, que se usa con frecuencia en la consola de Configuration Manager, el Explorador de recursos, las herramientas de Configuration Manager y los scripts.|  
|Root\SMS\SMS_ProviderLocation|La ubicación de los equipos del proveedor de SMS de un sitio.|  
|Root\CIMv2|La ubicación inventariada de la información del espacio de nombres WMI durante el inventario de hardware y software.|  
|Root\CCM|Directivas de configuración del cliente de Configuration Manager y datos de cliente.|  
|root\CIMv2\SMS|La ubicación de clases de informes de inventario recopiladas por el agente cliente de inventario. Los clientes compilan esta configuración durante la evaluación de directiva de equipo y se basan en la configuración del cliente para el equipo.|  

##  <a name="a-namebkmkwaikforsmsprova-operating-system-deployment-requirements-for-the-sms-provider"></a><a name="BKMK_WAIKforSMSProv"></a> Requisitos de implementación de sistema operativo del proveedor de SMS  
Es necesario que el equipo donde instale una instancia del proveedor de SMS tenga la versión correcta de Windows ADK que necesita la versión de Configuration Manager que use.  

 -   Por ejemplo, la versión 1511 de Configuration Manager necesita la versión Windows 10 RTM (10.0.10240) de Windows ADK.  

 -   Para obtener más información sobre este requisito, consulte [Requisitos de infraestructura para la implementación de sistema operativo en System Center Configuration Manager](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

Al administrar implementaciones de sistema operativo, Windows ADK permite al proveedor de SMS completar varias tareas, como las siguientes:  

-   Ver detalles del archivo WIM.  

-   Agregar archivos de controlador a imágenes de arranque existentes.  

-   Crear archivos .ISO de arranque.  


La instalación de Windows ADK puede requerir hasta 650 MB de espacio libre en disco en cada equipo en el que se instala al proveedor de SMS. Estos importantes requisitos de espacio de disco son necesarios para que Configuration Manager pueda instalar las imágenes de arranque de Windows PE.  



<!--HONumber=Feb17_HO2-->


