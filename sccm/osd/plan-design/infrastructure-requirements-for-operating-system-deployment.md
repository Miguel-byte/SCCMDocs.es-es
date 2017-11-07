---
title: "Requisitos de infraestructura para la implementación de sistema operativo"
titleSuffix: Configuration Manager
description: "Asegúrese de que conoce las dependencias externas y las dependencias de producto antes de usar System Center 2012 Configuration Manager para la implementación de sistema operativo."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
caps.latest.revision: "24"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 0b90cb20707340bec6fc7d5ddbab6f39d78e10bf
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="infrastructure-requirements-for-operating-system-deployment-in-system-center-configuration-manager"></a>Requisitos de infraestructura para la implementación de sistema operativo en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

La implementación de sistema operativo en System Center 2012 Configuration Manager tiene dependencias externas y dependencias dentro del producto. Use las secciones siguientes para que le resulte más fácil prepararse para la implementación de sistema operativo.  

##  <a name="BKMK_ExternalDependencies"></a> Dependencias externas a Configuration Manager  
 En la tabla siguiente se proporciona información sobre herramientas externas, kits de instalación y sistemas operativos necesarios para implementar sistemas operativos en Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK para Windows 10  
 Windows ADK es un conjunto de herramientas y documentación para la configuración e implementación de sistemas operativos Windows. Configuration Manager usa Windows ADK para automatizar las instalaciones de Windows, capturar imágenes de Windows, migrar perfiles y datos de usuarios, etc.  

 Las siguientes características de Windows ADK deben estar instaladas en el servidor de sitio de nivel superior de la jerarquía, en el servidor de sitio de cada sitio primario en la jerarquía y en el servidor de sistema de sitio de proveedor de SMS:  

-   Herramienta de migración de estado de usuario (USMT) <sup>1</sup>  

-   Herramientas de implementación de Windows  

-   Entorno de preinstalación de Windows (Windows PE)

Para obtener una lista de las versiones de Windows 10 ADK que puede usar con varias versiones de Configuration Manager, consulte [Soporte técnico de Windows 10 para clientes](https://docs.microsoft.com/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

 <sup>1</sup> no se necesita USMT en el servidor de sistema de sitio de proveedor de SMS.  

> [!NOTE]  
>  Debe instalar manualmente Windows ADK en cada uno de los equipos donde vaya a hospedarse un servidor de sitio de administración central o servidor de sitio primario antes de instalar el sitio de Configuration Manager.  

 Para obtener más información, vea:  

-   [Escenarios de Windows ADK para Windows 10 para profesionales de TI](https://technet.microsoft.com/library/mt280162\(v=vs.85\).aspx)  

-   [Descargar Windows ADK para Windows 10](https://msdn.microsoft.com/windows/hardware/dn913721.aspx#adkwin10)  

-   [Compatibilidad con Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)  


### <a name="user-state-migration-tool-usmt"></a>Herramienta de migración de estado de usuario (USMT)  
 Configuration Manager usa un paquete USMT que contiene los archivos de código fuente de USMT 10 para capturar y restaurar el estado de usuario como parte de la implementación de sistema operativo. El programa de instalación de Configuration Manager en el sitio de nivel superior crea automáticamente el paquete USMT. USMT 10 puede capturar el estado de usuario de Windows 7, Windows 8, Windows 8.1 y Windows 10. USMT 10 se distribuye en Windows Assessment and Deployment Kit (Windows ADK) para Windows 10.  

 Para obtener más información, vea:  

-   [Escenarios de migración habituales para USMT 10](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx)  

-   [Administrar el estado de usuario](../get-started/manage-user-state.md)  

### <a name="windows-pe"></a>Windows PE  
 Windows PE se usa para que las imágenes de arranque inicien un equipo. Windows PE es un sistema operativo Windows con servicios limitados que se usa durante la preinstalación y la implementación de sistemas operativos Windows. En la tabla siguiente se proporciona una lista de las versiones de Configuration Manager y la versión admitida de Windows ADK, la versión de Windows PE en la que se basa la imagen de arranque y que se puede personalizar mediante la consola de Configuration Manager, y las versiones de Windows PE en las que se basa la imagen de arranque, que se pueden personalizar mediante DISM y, después, agregar la imagen a la versión especificada de Configuration Manager.  

#### <a name="configuration-manager-version-1511"></a>Versión de Configuration Manager 1511  
 En la tabla siguiente se proporciona la versión admitida de Windows ADK, la versión de Windows PE en la que se basa la imagen de arranque y que se puede personalizar mediante la consola de Configuration Manager, y las versiones de Windows PE en las que se basa la imagen de arranque, que se pueden personalizar mediante DISM y, después, agregar la imagen a Configuration Manager.  

-   **Versión de Windows ADK**  

     Windows ADK para Windows 10  

-   **Versiones de Windows PE para imágenes de arranque personalizables desde la consola de Configuration Manager**  

     Windows PE 10  

-   **Versiones admitidas de Windows PE para imágenes de arranque que no se pueden personalizar desde la consola de Configuration Manager**  

     Windows PE 3.1<sup>1</sup> y Windows PE 5  

     <sup>1</sup> Solo se puede agregar una imagen de arranque a Configuration Manager si se basa en Windows PE 3.1. Instale el complemento de AIK de Windows para Windows 7 SP1 a fin de actualizar AIK de Windows para Windows 7 (basado en Windows PE 3) con el complemento de AIK de Windows para Windows 7 SP1 (basado en Windows PE 3.1). Puede descargar el complemento de AIK de Windows para Windows 7 SP1 en el [Centro de descarga de Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

     Por ejemplo, si tiene Configuration Manager, puede personalizar imágenes de arranque desde Windows ADK para Windows 10 (basado en Windows PE 10) mediante la consola de Configuration Manager. Sin embargo, aunque se admiten imágenes de arranque basadas en Windows PE 5, debe personalizarlas desde otro equipo y usar la versión de DISM instalada con Windows ADK para Windows 8. Después, puede agregar la imagen de arranque a la consola de Configuration Manager. Para obtener más información sobre los pasos para personalizar una imagen de arranque (agregar componentes y controladores adicionales), habilitar la compatibilidad con comandos en la imagen de arranque, agregar la imagen de arranque a la consola de Configuration Manager y actualizar los puntos de distribución con la imagen de arranque, consulte [Personalizar imágenes de arranque](../get-started/customize-boot-images.md). Para obtener más información sobre las imágenes de arranque, consulte [Administrar imágenes de arranque](../get-started/manage-boot-images.md).  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
Debe instalar las siguientes revisiones de WSUS 4.0:
  - [Hotfix 3095113](https://support.microsoft.com/kb/3095113) para el mantenimiento de Windows 10, que usa la infraestructura de actualizaciones de software para obtener actualizaciones de características de Windows 10. Si tiene WSUS 3.2, debe usar las secuencias de tareas para actualizar Windows 10. Para obtener más información, consulte [Administración de Windows como servicio](../deploy-use/manage-windows-as-a-service.md).  
  - [Revisión 3159706](https://support.microsoft.com/kb/3159706) es necesaria para usar el mantenimiento de Windows 10 para actualizar equipos a la Actualización de aniversario de Windows 10, así como para las versiones posteriores. Existen pasos manuales descritos en el artículo de ayuda que debe seguir para instalar esta revisión. Para obtener más información, consulte [Administración de Windows como servicio](../deploy-use/manage-windows-as-a-service.md).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>Internet Information Services (IIS) en los servidores de sistema de sitio  
 Se necesita IIS para el punto de distribución, el punto de migración de estado y el punto de administración. Para obtener más información sobre este requisito, consulte [Requisitos previos para los sitios y sistemas de sitio](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-deployment-services-wds"></a>Servicios de implementación de Windows (WDS)  
 WDS es necesario para las implementaciones de PXE, al usar multidifusión para optimizar el ancho de banda en sus implementaciones y para la instalación sin conexión de imágenes. Si el proveedor está instalado en un servidor remoto, debe instalar WDS en el servidor de sitio y el proveedor remoto. Para obtener más información, vea [Servicios de implementación de Windows](#BKMK_WDS) en este tema.  

### <a name="dynamic-host-configuration-protocol-dhcp"></a>Protocolo de configuración dinámica de host (DHCP)  
 Se requiere DHCP para implementaciones de PXE. Debe tener un servidor DHCP en funcionamiento con un host activo para implementar sistemas operativos mediante PXE. Para obtener más información sobre las implementaciones de PXE, consulte [Usar PXE para implementar Windows a través de la red](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Sistemas operativos y configuraciones de disco duro compatibles  
 Para obtener más información sobre las versiones de sistema operativo y las configuraciones de disco duro compatibles con Configuration Manager al implementar sistemas operativos, consulte [Sistemas operativos compatibles](#BKMK_SupportedOS) y [Configuraciones de disco compatibles](#BKMK_SupportedDiskConfig).  

### <a name="windows-device-drivers"></a>Controladores de dispositivos de Windows  
 Los controladores de dispositivos de Windows pueden utilizarse cuando se instala el sistema operativo en el equipo de destino y cuando se ejecuta Windows PE mediante una imagen de arranque. Para obtener más información sobre los controladores de dispositivos, consulte [Administrar controladores](../get-started/manage-drivers.md).  

##  <a name="BKMK_InternalDependencies"></a> Dependencias de Configuration Manager  
 A continuación se proporciona información sobre los requisitos previos para la implementación del sistema operativo de Configuration Manager.  

### <a name="operating-system-image"></a>Imagen de sistema operativo  
 Las imágenes de sistema operativo de Configuration Manager se almacenan en el archivo de formato de archivo Windows Imaging (WIM) y representan una recopilación comprimida de carpetas y archivos de referencia que se necesitan para instalar y configurar correctamente un sistema operativo en un equipo. Para obtener más información, consulte [Administrar imágenes de sistema operativo](../get-started/manage-operating-system-images.md).  

### <a name="driver-catalog"></a>Catálogo de controladores  
 Para implementar un controlador de dispositivo, debe importarlo, habilitarlo y establecerlo como disponible en un punto de distribución al que el cliente de Configuration Manager pueda tener acceso. Para obtener más información sobre el catálogo de controladores, consulte [Administrar controladores](../get-started/manage-drivers.md).  

### <a name="management-point"></a>Punto de administración  
 Los puntos de administración transfieren información entre los equipos cliente y el sitio de Configuration Manager. El cliente utiliza un punto de administración para ejecutar las secuencias de tareas que son necesarias para completar la implementación del sistema operativo.  

 Para obtener más información sobre las secuencias de tareas, consulte [Planeación de consideraciones para la automatización de tareas](planning-considerations-for-automating-tasks.md).  

### <a name="distribution-point"></a>Punto de distribución  
 Los puntos de distribución se utilizan en la mayoría de las implementaciones para almacenar los datos que se emplean en la implementación de un sistema operativo, tales como los paquetes de controladores de dispositivos o una imagen de sistema operativo. Las secuencias de tareas normalmente recuperan datos de un punto de distribución para implementar el sistema operativo.  

 Para obtener más información sobre cómo instalar puntos de distribución y administrar contenido, consulte [Manage content and content infrastructure (Administrar el contenido y la infraestructura de contenido)](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="pxe-enabled-distribution-point"></a>Punto de distribución habilitado con PXE  
 Para implementar las implementaciones iniciadas con PXE, debe configurar un punto de distribución que acepte las solicitudes de PXE de los clientes. Para más información sobre cómo configurar el punto de distribución, vea [Configurar un punto de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).  

### <a name="multicast-enabled-distribution-point"></a>Punto de distribución habilitado con multidifusión  
 Para optimizar las implementaciones de sistema operativo mediante multidifusión, debe configurar un punto de distribución que admita multidifusión. Para más información sobre cómo configurar el punto de distribución, vea [Configurar un punto de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast).   

### <a name="state-migration-point"></a>Punto de migración de estado  
 Al capturar y restaurar datos de estado de usuario para las implementaciones en paralelo y de actualización, debe configurar un punto de migración de estado para almacenar los datos de estado de usuario en otro equipo.  

 Para obtener más información sobre cómo configurar el punto de migración de estado, consulte [Punto de migración de estado](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

 Para obtener más información sobre cómo capturar y restaurar el estado de usuario, consulte [Administrar el estado de usuario](../get-started/manage-user-state.md).  

### <a name="service-connection-point"></a>Punto de conexión de servicio  
 Si usa Windows como servicio (WaaS) para implementar la rama actual de Windows 10, debe tener instalado el punto de conexión de servicio. Para obtener más información, consulte [Administración de Windows como servicio](../deploy-use/manage-windows-as-a-service.md).  

### <a name="reporting-services-point"></a>Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.  
 Con el fin de usar informes de Configuration Manager para las implementaciones de sistema operativo, debe instalar y configurar un punto de servicios de informes. Para obtener más información, consulte [Informes](../../core/servers/manage/reporting.md).  

### <a name="security-permissions-for-operating-system-deployments"></a>Permisos de seguridad para las implementaciones de sistema operativo  
 El rol de seguridad **Administrador de implementaciones de sistema operativo** es un rol integrado que no se puede cambiar. Sin embargo, puede copiar el rol, realizar cambios y, a continuación, guardar estos cambios como un nuevo rol de seguridad personalizado. Estos son algunos de los permisos que se aplican directamente a las implementaciones de sistema operativo:  

-   **Paquete de imagen de arranque**: crear, eliminar, modificar, modificar carpeta, mover objeto, leer, establecer ámbito de seguridad  

-   **Controladores de dispositivos**: crear, eliminar, modificar, modificar carpeta, modificar informe, mover objeto, leer, ejecutar informe  

-   **Paquete de controladores**: crear, eliminar, modificar, modificar carpeta, mover objeto, leer, establecer ámbito de seguridad  

-   **Imagen de sistema operativo**: crear, eliminar, modificar, modificar carpeta, mover objeto, leer, establecer ámbito de seguridad  

-   **Paquete de instalación de sistema operativo**: crear, eliminar, modificar, modificar carpeta, mover objeto, leer, establecer ámbito de seguridad  

-   **Paquete de secuencia de tareas**: crear, crear medio de secuencia de tareas, eliminar, modificar, modificar carpeta, modificar informe, mover objeto, leer, ejecutar informe, establecer ámbito de seguridad  

 Para obtener más información sobre los roles de seguridad personalizados, consulte [Crear roles de seguridad personalizados](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  

### <a name="security-scopes-for-operating-system-deployments"></a>Ámbitos de seguridad para las implementaciones de sistema operativo  
 Use ámbitos de seguridad para hacer que los usuarios administrativos tengan acceso a los objetos protegibles utilizados en las implementaciones de sistema operativo, tales como las imágenes de sistema operativo y de arranque, los paquetes de controladores y los paquetes de secuencias de tareas. Para obtener más información, consulte [Ámbitos de seguridad](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  

##  <a name="BKMK_WDS"></a> Servicios de implementación de Windows  
 Para admitir PXE o multidifusión, servicios de implementación de Windows (WDS) debe instalarse en el mismo servidor que los puntos de distribución que se configuran. El sistema operativo del servidor incluye WDS. En las implementaciones de PXE, WDS es el servicio que realiza el arranque de PXE. Si el punto de distribución se instala y se habilita para PXE, Configuration Manager instala un proveedor en WDS que emplea las funciones de arranque de PXE de WDS.  

> [!NOTE]  
>  Si el servidor requiere un reinicio, puede que la instalación de WDS no se realice correctamente. 

 Entre las configuraciones de WDS que deben tenerse en cuenta se incluyen las siguientes:  

-   La instalación de WDS en el servidor requiere que el administrador sea miembro del grupo Administradores locales.  

-   El servidor de WDS debe ser miembro de un dominio de Active Directory o de un controlador de dominio para un dominio de Active Directory. Todas las configuraciones de dominio y de bosque de Windows son compatibles con WDS.  

-   Si el proveedor está instalado en un servidor remoto, debe instalar WDS en el servidor de sitio y el proveedor remoto.  

###  <a name="BKMK_WDSandDHCP"></a> Consideraciones si se tiene WDS y DHCP en el mismo servidor  
 Tenga en cuenta las siguientes consideraciones sobre configuración si planea hospedar conjuntamente el punto de distribución en un servidor que ejecuta DHCP.  

-   Debe tener un servidor DHCP en funcionamiento con un ámbito activo. Servicios de implementación de Windows utiliza PXE, el cual requiere un servidor DHCP.  

-   DHCP y Servicios de implementación de Windows requieren el puerto número 67. Si hospeda conjuntamente Servicios de implementación de Windows y DHCP, puede mover DHCP o el punto de distribución que esté configurado para PXE a otro servidor. Alternativamente, puede utilizar el siguiente procedimiento para configurar el servidor de Servicios de implementación de Windows para que escuche en otro puerto.  

    #### <a name="to-configure-the-windows-deployment-services-server-to-listen-on-a-different-port"></a>Para configurar el servidor de Servicios de implementación de Windows para que escuche en otro puerto  

    1.  Modifique la siguiente Clave del registro:  

         **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE**  

    2.  Establezca el valor del Registro en: **UseDHCPPorts = 0**  

    3.  Para que la nueva configuración surta efecto, ejecute el siguiente comando en el servidor:  

         `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

-   Se requiere un servidor DNS para ejecutar Servicios de implementación de Windows.  

-   Los siguientes puertos UDP deben estar abiertos en el servidor de Servicios de implementación de Windows.  

    -   Puerto 67 (DHCP)  

    -   Puerto 69 (TFTP)  

    -   Puerto 4011 (PXE)  

    > [!NOTE]  
    >  Además, si se requiere una autorización de DHCP en el servidor, será necesario que el puerto 68 del cliente DHCP esté abierto en el servidor.  

##  <a name="BKMK_SupportedOS"></a> Sistemas operativos compatibles  
 Todos los sistemas operativos de Windows enumerados como sistemas operativos de cliente compatibles en [Sistemas operativos compatibles con clientes y dispositivos](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) se admiten en las implementaciones de sistema operativo.  

##  <a name="BKMK_SupportedDiskConfig"></a> Configuraciones de disco compatibles  
 Las combinaciones de configuración de disco duro en los equipos de referencia y de destino compatibles con la implementación de sistema operativo de Configuration Manager se muestran en la tabla siguiente.  

|Configuración de disco duro del equipo de referencia|Configuración de disco duro del equipo de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco básico|  
|Volumen simple en un disco dinámico|Volumen simple en un disco dinámico|  

 Configuration Manager admite la captura de una imagen de sistema operativo solamente desde equipos que estén configurados con volúmenes simples. No hay soporte para las siguientes configuraciones de disco duro:  

-   Volúmenes distribuidos  

-   Volúmenes seccionados (RAID 0)  

-   Volúmenes reflejados (RAID 1)  

-   Volúmenes de paridad (RAID 5)  

 La tabla siguiente muestra una configuración de disco duro adicional en el equipo de destino y en el de referencia que no se admite con la implementación de sistema operativo de Configuration Manager.  

|Configuración de disco duro del equipo de referencia|Configuración de disco duro del equipo de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco dinámico|  

## <a name="next-steps"></a>Pasos siguientes
[Prepararse para la implementación de sistema operativo](../get-started/prepare-for-operating-system-deployment.md)
