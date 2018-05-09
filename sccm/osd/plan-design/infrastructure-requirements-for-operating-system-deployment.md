---
title: Requisitos de la infraestructura de OSD
titleSuffix: Configuration Manager
description: Obtenga información sobre las dependencias de producto externas y los requisitos para la implementación de sistema operativo.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6407344676230c12c66abb02c1394032e102e4b8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="infrastructure-requirements-for-os-deployment-in-system-center-configuration-manager"></a>Requisitos de infraestructura para la implementación de SO en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La implementación de SO en Configuration Manager tiene dependencias externas y dependencias dentro del producto. Use este artículo para facilitar la preparación de la infraestructura de implementación de SO.  



##  <a name="BKMK_ExternalDependencies"></a> Dependencias externas a Configuration Manager  
 En esta sección se proporciona información sobre herramientas externas, kits de instalación y versiones de sistema operativo necesarias para implementar sistemas operativos en Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK para Windows 10  
 Windows Assessment and Deployment Kit (ADK) es un conjunto de herramientas y documentación que admiten la configuración e implementación de Windows. Configuration Manager usa Windows ADK para automatizar acciones como la instalación de Windows, la captura de imágenes y la migración de datos y perfiles de usuario.  

 Las características siguientes de Windows ADK deben estar instaladas en el servidor de sitio del sitio de nivel superior de la jerarquía, en el servidor de sitio de cada sitio primario de la jerarquía y en el servidor de sistema de sitio de proveedor de SMS:  

-   Herramienta de migración de estado de usuario (USMT) <sup>1</sup>  

-   Herramientas de implementación de Windows  

-   Entorno de preinstalación de Windows (Windows PE)

Para obtener una lista de las versiones de Windows 10 ADK que se pueden usar con otras versiones de Configuration Manager, vea [Compatibilidad con Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

 <sup>1</sup> No se necesita USMT en el servidor de sistema de sitio de proveedor de SMS.  

> [!NOTE]  
>  Debe instalar manualmente Windows ADK en cada servidor de sitio antes de instalar el sitio de Configuration Manager.  

 Para obtener más información, vea:  

-   [Escenarios de Windows ADK para Windows 10 para profesionales de TI](/windows/deployment/windows-adk-scenarios-for-it-pros)  

-   [Descargar Windows ADK para Windows 10](/windows-hardware/get-started/adk-install)  

-   [Compatibilidad con Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)  


### <a name="user-state-migration-tool-usmt"></a>Herramienta de migración de estado de usuario (USMT)  
 Configuration Manager usa un paquete USMT que incluye los archivos de código fuente de USMT 10 para capturar y restaurar el estado de usuario como parte de la implementación de SO. El programa de instalación de Configuration Manager en el sitio de nivel superior crea automáticamente el paquete USMT. USMT 10 captura el estado de usuario de Windows 7, Windows 8, Windows 8.1 y Windows 10.  

 Para obtener más información, vea:  

-   [Escenarios de migración habituales para USMT 10](/windows/deployment/usmt/usmt-common-migration-scenarios)  

-   [Administrar el estado de usuario](../get-started/manage-user-state.md)  

### <a name="windows-pe"></a>Windows PE  
 Windows PE se usa para que las imágenes de arranque inicien un equipo. Es una versión de Windows con servicios limitados que se usa durante la preinstalación y la implementación de Windows. En la lista siguiente se incluyen las versiones admitidas de Windows ADK para Configuration Manager (Rama actual):  

-   **Versión de Windows ADK**  

     Windows ADK para Windows 10 Para obtener más información, vea [Compatibilidad con Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

-   **Versiones de Windows PE para imágenes de arranque personalizables desde la consola de Configuration Manager**  

     Windows PE 10  

-   **Versiones admitidas de Windows PE para imágenes de arranque que no se pueden personalizar desde la consola de Configuration Manager**  

     Windows PE 3.1<sup>1</sup> y Windows PE 5  

     <sup>1</sup> Solo se puede agregar una imagen de arranque a Configuration Manager si se basa en Windows PE 3.1. Instale el complemento de AIK de Windows para Windows 7 SP1 a fin de actualizar AIK de Windows para Windows 7 (basado en Windows PE 3) con el complemento de AIK de Windows para Windows 7 SP1 (basado en Windows PE 3.1). Puede descargar el complemento de AIK de Windows para Windows 7 SP1 en el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

     Por ejemplo, si tiene Configuration Manager, puede personalizar imágenes de arranque desde Windows ADK para Windows 10 (basado en Windows PE 10) mediante la consola de Configuration Manager. Sin embargo, aunque se admiten imágenes de arranque basadas en Windows PE 5, debe personalizarlas desde otro equipo y usar la versión de DISM instalada con Windows ADK para Windows 8. Después, puede agregar la imagen de arranque a la consola de Configuration Manager. Para obtener más información sobre los pasos para personalizar una imagen de arranque (agregar componentes y controladores adicionales), habilitar la compatibilidad con comandos en la imagen de arranque, agregar la imagen de arranque a la consola de Configuration Manager y actualizar los puntos de distribución con la imagen de arranque, consulte [Personalizar imágenes de arranque](../get-started/customize-boot-images.md). Para obtener más información sobre las imágenes de arranque, consulte [Administrar imágenes de arranque](../get-started/manage-boot-images.md).  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
 WSUS es necesario para el punto de actualización de software, que es necesario para instalar las actualizaciones de software durante la implementación de SO. Para obtener más información, vea [Instalar y configurar un punto de actualización de software](/sccm/sum/get-started/install-a-software-update-point).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>Internet Information Services (IIS) en los servidores de sistema de sitio  
 Se necesita IIS para el punto de distribución, el punto de migración de estado y el punto de administración. Para obtener más información, consulte [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Requisitos previos de sitio y sistema de sitio).  


### <a name="windows-deployment-services-wds"></a>Servicios de implementación de Windows (WDS)  
 WDS es necesario para las implementaciones de PXE y al utilizar multidifusión para optimizar el ancho de banda en sus implementaciones. Para obtener más información, vea [Servicios de implementación de Windows](#BKMK_WDS) en este artículo.  


### <a name="dynamic-host-configuration-protocol-dhcp"></a>Protocolo de configuración dinámica de host (DHCP)  
 Se requiere DHCP para implementaciones de PXE. Debe tener un servidor DHCP en funcionamiento con un host activo para implementar sistemas operativos mediante PXE. Para obtener más información sobre las implementaciones de PXE, consulte [Usar PXE para implementar Windows a través de la red](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Sistemas operativos y configuraciones de disco duro compatibles  
 Para obtener más información sobre las versiones de sistema operativo y las configuraciones de disco duro compatibles con Configuration Manager al implementar sistemas operativos, vea [Sistemas operativos compatibles](#BKMK_SupportedOS) y [Configuraciones de disco compatibles](#BKMK_SupportedDiskConfig).  


### <a name="windows-device-drivers"></a>Controladores de dispositivos de Windows  
 Se pueden usar controladores de dispositivo de Windows cuando se instala el sistema operativo en el equipo de destino. También se usan cuando se ejecuta Windows PE en una imagen de arranque. Para obtener más información, consulte [Administrar controladores](../get-started/manage-drivers.md).  



##  <a name="BKMK_InternalDependencies"></a> Dependencias de Configuration Manager  
 En esta sección se proporciona información sobre los requisitos previos para la implementación de SO de Configuration Manager.  


### <a name="os-image"></a>Imagen del sistema operativo  
 Las imágenes de SO en Configuration Manager se almacenan en el formato de archivo Windows Imaging (WIM). Representan una colección comprimida de carpetas y archivos de referencia. Estas imágenes son necesarias para instalar y configurar correctamente un sistema operativo en un equipo. Para obtener más información, consulte [Administrar imágenes de sistema operativo](../get-started/manage-operating-system-images.md).  


### <a name="driver-catalog"></a>Catálogo de controladores  
 Para implementar un controlador de dispositivo, debe importarlo, habilitarlo y establecerlo como disponible en un punto de distribución al que el cliente de Configuration Manager pueda tener acceso. Para obtener más información sobre el catálogo de controladores, consulte [Administrar controladores](../get-started/manage-drivers.md).  


### <a name="management-point"></a>Punto de administración  
 Los puntos de administración transfieren información entre los clientes y el sitio de Configuration Manager. El cliente usa un punto de administración para ejecutar la secuencia de tareas para completar la implementación de SO. Para obtener más información sobre las secuencias de tareas, consulte [Planeación de consideraciones para la automatización de tareas](planning-considerations-for-automating-tasks.md).  


### <a name="distribution-point"></a>Punto de distribución  
 Los puntos de distribución se usan en la mayoría de las implementaciones para almacenar los datos que se usan para implementar un sistema operativo, como los paquetes de imagen o controladores. Las secuencias de tareas normalmente recuperan datos de un punto de distribución para implementar el sistema operativo. Para obtener más información sobre cómo instalar puntos de distribución y administrar contenido, consulte [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administrar el contenido y la infraestructura de contenido).  


### <a name="pxe-enabled-distribution-point"></a>Punto de distribución habilitado con PXE  
 Para implementar las implementaciones iniciadas con PXE, debe configurar un punto de distribución que acepte las solicitudes de PXE de los clientes. Para obtener más información, vea [Configuración de puntos de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).


### <a name="multicast-enabled-distribution-point"></a>Punto de distribución habilitado con multidifusión  
 Para optimizar las implementaciones de SO mediante multidifusión, debe configurar un punto de distribución que admita multidifusión. Para obtener más información, vea [Configuración de puntos de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast).   


### <a name="state-migration-point"></a>Punto de migración de estado  
 Al capturar y restaurar datos de estado de usuario para las implementaciones en paralelo y de actualización, debe configurar un punto de migración de estado para almacenar los datos de estado de usuario en otro equipo.  

 Para obtener más información sobre cómo configurar el punto de migración de estado, consulte [Punto de migración de estado](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

 Para obtener más información sobre cómo capturar y restaurar el estado de usuario, consulte [Administrar el estado de usuario](../get-started/manage-user-state.md).  


### <a name="reporting-services-point"></a>Punto de servicios de informes  
 Para usar informes de Configuration Manager para las implementaciones de SO, debe instalar y configurar un punto de servicios de informes. Para obtener más información, consulte [Informes](../../core/servers/manage/reporting.md).  


### <a name="security-permissions-for-os-deployments"></a>Permisos de seguridad para las implementaciones de SO  
 El rol de seguridad **Administrador de implementaciones de sistema operativo** es un rol integrado que no se puede cambiar. Sin embargo, puede copiar el rol, realizar cambios y, a continuación, guardar estos cambios como un nuevo rol de seguridad personalizado. Estos son algunos de los permisos que se aplican directamente a las implementaciones de SO:  

-   **Paquete de imagen de arranque**: crear, eliminar, modificar, modificar carpeta, mover objeto, leer, establecer ámbito de seguridad  

-   **Controladores de dispositivos**: crear, eliminar, modificar, modificar carpeta, modificar informe, mover objeto, leer, ejecutar informe  

-   **Paquete de controladores**: crear, eliminar, modificar, modificar carpeta, mover objeto, leer, establecer ámbito de seguridad  

-   **Imagen de sistema operativo**: crear, eliminar, modificar, modificar carpeta, mover objeto, leer, establecer ámbito de seguridad  

-   **Paquete de instalación de sistema operativo**: crear, eliminar, modificar, modificar carpeta, mover objeto, leer, establecer ámbito de seguridad  

-   **Paquete de secuencia de tareas**: crear, crear medio de secuencia de tareas, eliminar, modificar, modificar carpeta, modificar informe, mover objeto, leer, ejecutar informe, establecer ámbito de seguridad  

 Para obtener más información, vea [Crear roles de seguridad personalizados](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  


### <a name="security-scopes-for-os-deployments"></a>Ámbitos de seguridad para las implementaciones de SO  
 Use ámbitos de seguridad para proporcionar a los usuarios administrativos acceso a los objetos protegibles que se usan en las implementaciones de SO, como las imágenes de SO y de arranque, los paquetes de controladores y los paquetes de secuencias de tareas. Para obtener más información, consulte [Ámbitos de seguridad](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  



##  <a name="BKMK_WDS"></a> Servicios de implementación de Windows  
 Para admitir PXE o multidifusión, servicios de implementación de Windows (WDS) debe instalarse en el mismo servidor que los puntos de distribución que se configuran. El sistema operativo del servidor incluye WDS. En las implementaciones de PXE, WDS es el servicio que realiza el arranque de PXE. Si el punto de distribución se instala y se habilita para PXE, Configuration Manager instala un proveedor en WDS que emplea las funciones de arranque de PXE de WDS.  

> [!NOTE]  
>  Si el servidor requiere un reinicio, puede que la instalación de WDS no se realice correctamente. 


### <a name="wds-requirements"></a>Requisitos de WDS  

-   La instalación de WDS en el servidor requiere que el administrador sea miembro del grupo Administradores locales.  

-   El servidor de WDS debe ser miembro de un dominio de Active Directory o de un controlador de dominio para un dominio de Active Directory. Todas las configuraciones de dominio y de bosque de Windows son compatibles con WDS.  

-   Si el proveedor está instalado en un servidor remoto, debe instalar WDS en el servidor de sitio y el proveedor remoto.  


###  <a name="BKMK_WDSandDHCP"></a> Consideraciones si se tiene WDS y DHCP en el mismo servidor  
 Tenga en cuenta las siguientes consideraciones sobre configuración si planea hospedar conjuntamente el punto de distribución en un servidor que ejecuta DHCP.  

-   Debe tener un servidor DHCP en funcionamiento con un ámbito activo. WDS usa PXE, que requiere un servidor DHCP.  

-   DHCP y WDS requieren el puerto número 67. Si WDS y DHCP se hospedan conjuntamente, se puede mover DHCP o el punto de distribución que esté configurado para PXE a otro servidor. O bien, puede usar el procedimiento siguiente para configurar el servidor de WDS para que escuche en otro puerto.  

    #### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>Para configurar el servidor de WDS para que escuche en otro puerto  

    1.  Modifique la siguiente Clave del registro:  

         `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

    2.  Establezca el valor del Registro **UseDHCPPorts** en **0**.  

    3.  Para que la nueva configuración surta efecto, ejecute el siguiente comando en el servidor:  

         `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

-   Se necesita un servidor DNS para ejecutar WDS.  

-   Los puertos UDP siguientes deben estar abiertos en el servidor de WDS.  

    -   Puerto 67 (DHCP)  

    -   Puerto 69 (TFTP)  

    -   Puerto 4011 (PXE)  

    > [!NOTE]  
    >  Si se requiere autorización de DHCP en el servidor, será necesario que el puerto 68 del cliente DHCP esté abierto en el servidor.  



##  <a name="BKMK_SupportedOS"></a> Sistemas operativos compatibles  
 Todos los sistemas operativos de Windows enumerados como clientes compatibles en [Sistemas operativos compatibles con clientes y dispositivos](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) se admiten en las implementaciones de SO.  



##  <a name="BKMK_SupportedDiskConfig"></a> Configuraciones de disco compatibles  
 Las combinaciones de configuración de disco duro en los equipos de referencia y de destino compatibles con la implementación de SO de Configuration Manager se muestran en la tabla siguiente:  

|Configuración de disco duro del equipo de referencia|Configuración de disco duro del equipo de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco básico|  
|Volumen simple en un disco dinámico|Volumen simple en un disco dinámico|  

 Configuration Manager admite la captura de una imagen de SO solamente desde equipos que estén configurados con volúmenes simples. No hay soporte para las configuraciones de disco duro siguientes:  

-   Volúmenes distribuidos  

-   Volúmenes seccionados (RAID 0)  

-   Volúmenes reflejados (RAID 1)  

-   Volúmenes de paridad (RAID 5)  

 En la tabla siguiente se muestra una configuración de disco duro adicional en los equipo de referencia y de destino que no se admite con la implementación de SO de Configuration Manager.  

|Configuración de disco duro del equipo de referencia|Configuración de disco duro del equipo de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco dinámico|  



## <a name="next-steps"></a>Pasos siguientes
- [Preparar los roles de sistema de sitio para la implementación de SO](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments)
- [Preparar la implementación de SO](../get-started/prepare-for-operating-system-deployment.md)
