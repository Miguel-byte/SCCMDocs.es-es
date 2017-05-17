---
title: 'Inventario de hardware | Microsoft Docs | Linux y UNIX '
description: "Obtenga información sobre cómo usar el inventario de hardware para Linux y UNIX en System Center Configuration Manager."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
caps.latest.revision: 6
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: cb1ac4f33b9ef291050a3406291b8cc1f112b586
ms.contentlocale: es-es
ms.lasthandoff: 12/16/2016


---
# <a name="hardware-inventory-for-linux-and-unix-in-system-center-configuration-manager"></a>Inventario de hardware para Linux y UNIX en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

El cliente de System Center Configuration Manager para Linux y UNIX admite el inventario de hardware. Después de recopilar el inventario de hardware, puede ejecutar y ver el inventario en el Explorador de recursos o informes de Configuration Manager y usar esta información para crear consultas y recopilaciones que permiten las siguientes operaciones:  

-   Implementación de software  

-   Aplicar ventanas de mantenimiento  

-   Implementar configuraciones personalizadas de cliente  

 El inventario de hardware para servidores Linux y UNIX utiliza un servidor de Modelo de información común (CIM) basado en estándares. El servidor CIM se ejecuta como un servicio de software (o daemon) y proporciona una infraestructura de administración que se basa en estándares del grupo de trabajo de administración distribuida (DMTF). El servidor CIM proporciona una funcionalidad similar a las capacidades de CIM de la infraestructura de administración de Windows (WMI) que están disponibles en equipos basados en Windows.  

 A partir de la actualización acumulativa 1, el cliente para Linux y UNIX usa el código abierto **omiserver** versión 1.0.6 de **The Open Group**. (Antes de la actualización acumulativa 1, el cliente utilizaba **nanowbem** como servidor CIM).  

 El servidor CIM se instala como parte del cliente para Linux y UNIX. El cliente para Linux y UNIX se comunica directamente con el servidor CIM y no utiliza la interfaz de WS-MAN del servidor CIM. El puerto de WS-MAN en el servidor CIM está deshabilitado cuando se instala el cliente. Microsoft desarrolló el servidor CIM que ahora está disponible como código abierto a través del proyecto Open Management Infrastructure (OMI). Para obtener más información sobre el proyecto Open Management Infrastructure, consulte el sitio web de [The Open Group](http://go.microsoft.com/fwlink/p/?LinkId=262317) .  

 El inventario de hardware en servidores Linux y UNIX funciona mediante la asignación de clases y propiedades de WMI de Win32 existentes a clases y propiedades equivalentes para servidores Linux y UNIX. Esta asignación uno a uno de clases y propiedades permite que el inventario de hardware de Linux y UNIX se integre en Configuration Manager. Los datos de inventario de servidores Linux y UNIX se muestran junto con el inventario de equipos basados en Windows en la consola y los informes de Configuration Manager. Esto proporciona una experiencia coherente de administración heterogénea.  

> [!TIP]  
>  Puede usar el valor **Título** para la clase **Sistema operativo** a fin de identificar los diferentes sistemas operativos Linux y UNIX en consultas y recopilaciones.  

##  <a name="BKMK_ConfigHardwareforLnU"></a> Configurar el inventario de hardware para servidores Linux y UNIX  
 Puede utilizar la configuración de cliente predeterminada o crear configuraciones de dispositivo cliente personalizadas para configurar el inventario de hardware. Cuando se utiliza la configuración de dispositivo cliente personalizada, puede configurar las clases y propiedades que desea recopilar únicamente de los servidores Linux y UNIX. También puede especificar las programaciones personalizadas para cuándo recopilar inventarios completos y diferenciales de los servidores Linux y UNIX.  

 El cliente para Linux y UNIX admite las siguientes clases de inventario de hardware que están disponibles en servidores Linux y UNIX:  

-   Win32_BIOS  

-   Win32_ComputerSystem  

-   Win32_DiskDrive  

-   Win32_DiskPartition  

-   Win32_NetworkAdapter  

-   Win32_NetworkAdapterConfiguration  

-   Win32_OperatingSystem  

-   Win32_Process  

-   Win32_Service  

-   Win32Reg_AddRemovePrograms  

-   SMS_LogicalDisk  

-   SMS_Processor  

 No todas las propiedades para estas clases de inventario están habilitadas para equipos UNIX y Linux en Configuration Manager.  

##  <a name="BKMK_OperationsforHardwareforLnU"></a> Operaciones del inventario de hardware  
 Después de recopilar el inventario de hardware de los servidores Linux y UNIX, puede ver y utilizar esta información de la misma manera que ve el inventario que recopila de otros equipos:  

-   Utilizar el Explorador de recursos para ver información detallada sobre el inventario de hardware de servidores Linux y UNIX.  

-   Crear consultas basadas en configuraciones de hardware específicas.  

-   Crear recopilaciones basadas en consultas en función de configuraciones de hardware específicas.  

-   Ejecutar informes que muestran detalles específicos sobre las configuraciones de hardware.  

 El inventario de hardware en un servidor Linux o UNIX se ejecuta según la programación configurada en la configuración del cliente. De forma predeterminada, esto sucede cada siete días. El cliente para Linux y UNIX admite tanto ciclos de inventario completo como ciclos de inventario diferencial.  

 También puede forzar al cliente en un servidor Linux o UNIX para que ejecute el inventario de hardware de inmediato. Para ejecutar el inventario de hardware, en un cliente utilice las credenciales **raíz** para ejecutar el siguiente comando para iniciar un ciclo de inventario de hardware: **/opt/microsoft/configmgr/bin/ccmexec - rs hinv**  

 Las acciones del inventario de hardware se especifican en el archivo de registro de cliente, **scxcm.log**.  

##  <a name="BKMK_CustomHINVforLinux"></a> Cómo utilizar Open Management Infrastructure para crear un inventario de hardware personalizado  
 El cliente para Linux y UNIX admite el inventario de hardware personalizado que puede crear utilizando Open Management Infrastructure (OMI). Para ello, siga los pasos a continuación:  

1.  Cree un proveedor de inventario personalizado mediante el origen OMI.  

2.  Configure equipos para que usen el nuevo proveedor para informar el inventario.  

3.  Habilitar Configuration Manager para admitir el nuevo proveedor  

###  <a name="BKMK_LinuxProvider"></a> Cree un proveedor de  inventario de hardware personalizado para equipos UNIX y Linux:  
 Para crear un proveedor de inventario de hardware personalizado para el cliente de Configuration Manager para Linux y UNIX, use **OMI Source - v.1.0.6** y siga las instrucciones de la Guía de introducción de OMI. Este proceso incluye la creación de un archivo Managed Object Format (MOF) que define el esquema del nuevo proveedor. Después, importe el archivo MOF en Configuration Manager para habilitar la compatibilidad de la nueva clase de inventario personalizado.  

 Tanto OMI Source - v.1.0.6 como la Guía de introducción de OMI están disponibles para descargar desde el sitio web de [The Open Group](http://go.microsoft.com/fwlink/p/?LinkId=262317) . Puede encontrar estas descargas en la pestaña **Documentos** en la siguiente página web en el sitio web de OpenGroup.org: [Open Management Infrastructure (OMI)](http://go.microsoft.com/fwlink/p/?LinkId=286805).  

###  <a name="BKMK_AddProvidertoLinux"></a> Configure cada equipo que ejecute Linux o UNIX con el proveedor de inventario de hardware personalizado:  
 Después de crear un proveedor de inventario personalizado, debe copiar y, a continuación, registrar el archivo de la biblioteca del proveedor en cada equipo que tiene el inventario que desea recopilar.  

1.  Copie la biblioteca del proveedor en cada equipo Linux y UNIX del que desea recopilar el inventario. El nombre de la biblioteca del proveedor es similar al siguiente: **XYZ_MyProvider.so**  

2.  A continuación, en cada equipo Linux y UNIX, registre la biblioteca del proveedor en el servidor OMI. El servidor OMI se instala en el equipo al instalar el cliente de Configuration Manager para Linux y UNIX, pero debe registrar manualmente los proveedores personalizados. Utilice la siguiente línea de comandos para registrar el proveedor: **/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so**  

3.  Después de registrar el nuevo proveedor, pruebe el proveedor mediante la herramienta **omicli** . La herramienta de **omicli** se instala en cada equipo Linux y UNIX al instalar el cliente de Configuration Manager para Linux y UNIX. Por ejemplo, donde **XYZ_MyProvider** es el nombre del proveedor que creó, ejecute el siguiente comando en el equipo: **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     Para obtener información acerca de **omicli** y probar los proveedores personalizados, consulte la Guía de introducción de OMI.  

> [!TIP]  
>  Utilice la distribución de software para implementar proveedores personalizados y para registrar proveedores personalizados en cada equipo cliente con Linux y UNIX.  

###  <a name="BKMK_AddLinuxProvidertoCM"></a> Habilite la nueva clase de inventario en Configuration Manager:  
 Antes de que Configuration Manager puede informar sobre el inventario que notifica el nuevo proveedor en equipos Linux y UNIX, debe importar el archivo Managed Object Format (MOF) que define el esquema del proveedor personalizado.  

 Para importar un archivo MOF personalizado en Configuration Manager, consulte [How to configure hardware inventory in System Center Configuration Manager (Cómo configurar el inventario de hardware en System Center Configuration Manager)](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

