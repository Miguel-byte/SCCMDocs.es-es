---
title: "Creación de recopilaciones | System Center Configuration Manager"
description: "Realice tareas de administración de recopilaciones en System Center Configuration Manager de colecciones comunes."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
caps.latest.revision: 8
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d7d0b9c40f22bf1a7c477d1b8626d5a531c959d7


---
# <a name="how-to-manage-collections-in-system-center-configuration-manager"></a>Cómo administrar recopilaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Utilice la información de introducción de este tema como ayuda para realizar tareas de administración para las recopilaciones en System Center Configuration Manager.  

> [!NOTE]  
>  Para obtener más información sobre la creación de recopilaciones, consulte [Cómo crear recopilaciones en System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).  

## <a name="how-to-manage-device-collections"></a>Cómo administrar de recopilaciones de dispositivos  
 En el área de trabajo **Activos y compatibilidad** , seleccione **Recopilaciones de dispositivos**, seleccione la recopilación que se debe administrar y luego seleccione una tarea de administración.  

 Utilice la tabla siguiente para obtener más información acerca de las tareas de administración que pueden requerir información para poder seleccionarlas.  

|Tarea de administración|Detalles|Más información|  
|---------------------|-------------|----------------------|  
|**Mostrar miembros**|Muestra todos los recursos que sean miembros de la recopilación seleccionada en un nodo temporal en el nodo **Dispositivos** .|No hay información adicional.|  
|**Agregar elementos seleccionados**|Ofrece las opciones siguientes para realizar una de las acciones siguientes:<br /><br /> - <br />                    **Agregar elementos seleccionados a la recopilación de dispositivos existente**: abre el cuadro de diálogo **Seleccionar recopilación**, donde puede seleccionar la recopilación en la que quiere agregar los miembros de la recopilación seleccionada. La recopilación seleccionada se incluye en esta recopilación mediante una regla de pertenencia **Incluir recopilaciones** .<br /><br /> - **Agregar elementos seleccionados a la nueva recopilación de dispositivos**: abre el **Asistente para crear recopilación de dispositivos**, donde puede crear una nueva recopilación. La recopilación seleccionada se incluye en esta recopilación mediante una regla de pertenencia **Incluir recopilaciones** .|[Cómo crear recopilaciones en System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|**Instalar cliente**|Abre el **Asistente para instalar clientes**, que utiliza la instalación de inserción de cliente para instalar un cliente de Configuration Manager en todos los equipos de la recopilación seleccionada.|[Client deployment tasks for System Center Configuration Manager](../../../../core/clients/deploy/client-deployment-tasks.md) (Tareas de implementación de cliente para System Center Configuration Manager)|  
|**Administrar solicitudes de afinidad**|Abre el cuadro de diálogo **Administrar solicitudes de afinidad de dispositivo de usuario** , donde puede aprobar o rechazar solicitudes pendientes para establecer afinidades de dispositivos de usuario de dispositivos de la recopilación seleccionada.|[Link users and devices with user device affinity in System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) (Vinculación de usuarios y dispositivos con afinidad entre usuario y dispositivo en System Center Configuration Manager).|  
|**Desactivar implementaciones de PXE necesarias**|Borra las implementaciones de arranque PXE necesarias de todos los miembros de la recopilación seleccionada.|[Introduction to operating system deployment](../../../../osd/understand/introduction-to-operating-system-deployment.md) (Introducción a la implementación de sistema operativo)|  
|**Actualizar pertenencia**|Evalúa la pertenencia de la recopilación seleccionada. En las recopilaciones con muchos miembros, esta actualización puede tardar algo de tiempo en finalizar. Utilice la acción **Actualizar** para actualizar la pantalla con los nuevos miembros de las recopilaciones después de que se complete la actualización.|No hay información adicional.|  
|**Agregar recursos**|Abre el cuadro de diálogo **Agregar recursos a la recopilación** , donde puede buscar nuevos recursos para agregarlos a la recopilación seleccionada.<br /><br /> El icono de la recopilación seleccionada mostrará un símbolo de reloj de arena mientras la actualización está en curso.|No hay información adicional.|  
|**Notificación de cliente**|Indica a todos los clientes de la recopilación de dispositivos seleccionada que descarguen la directiva de equipo o usuario.|No hay información adicional.|  
|**Endpoint Protection**|Realiza un examen rápido o completo en busca de antimalware o descarga de las últimas definiciones de antimalware en los equipos de la recopilación seleccionada.|[Endpoint Protection in System Center Configuration Manager](../../../../protect/deploy-use/endpoint-protection.md) (Endpoint Protection en System Center Configuration Manager)|  
|**Exportarar**|Abre el **Asistente para exportar recopilaciones** que le ayuda a exportar esta recopilación en un archivo MOF que después puede archivarse o utilizarse en otro sitio de Configuration Manager.<br /><br /> Cuando se exporta una recopilación, las recopilaciones a las que hace referencia la recopilación seleccionada mediante una regla de **inclusión** o **exclusión** no se exportan.|No hay información adicional.|  
|**Copiar**|Crea una copia de la recopilación seleccionada. La nueva recopilación utiliza la recopilación seleccionada como una recopilación de restricción.|No hay información adicional.|  
|**Eliminar**|Elimina la recopilación seleccionada. También puede eliminar todos los recursos de la recopilación de la base de datos del sitio.<br /><br /> No se pueden eliminar las recopilaciones integradas en Configuration Manager.|Para obtener una lista de las colecciones integradas, consulte [Introducción a las recopilaciones en System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).|  
|**Simular implementación**|Abre el **Asistente para simular implementación de aplicación** , que le permite probar los resultados de una implementación de aplicación en equipos sin instalar ni desinstalar la aplicación.|[How to simulate application deployments with System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md) (Simulación de implementaciones de aplicaciones con System Center Configuration Manager)|  
|**Implementar**|Se muestran las opciones siguientes:<br /><br /> - <br />                    **Aplicación**: abre el **Asistente para implementar software**, donde puede seleccionar y configurar una implementación de aplicación en la recopilación seleccionada.<br /><br /> - <br />                    **Programa** : abre el **Asistente para implementar software** , donde puede seleccionar y configurar una implementación de paquete y programa en la recopilación seleccionada.<br /><br /> - **Línea base de configuración**: abre el cuadro de diálogo **Implementar líneas de base de configuración**, donde puede configurar la implementación de una o varias líneas base de configuración en la recopilación seleccionada.<br /><br /> - <br />                    **Secuencia de tareas** : abre el **Asistente para implementar software** , donde puede seleccionar y configurar una implementación de secuencia de tareas en la recopilación seleccionada.<br /><br /> - <br />                    **Actualizaciones de software**: abre el **Asistente para implementar actualizaciones de software**, donde puede configurar la implementación de actualizaciones de software en recursos de la recopilación seleccionada.|[How to deploy applications with System Center Configuration Manager](../../../../apps/deploy-use/deploy-applications.md) (Implementación de aplicaciones con System Center Configuration Manager)<br /><br /> [Packages and programs in System Center Configuration Manager](../../../../apps/deploy-use/packages-and-programs.md) (Paquetes y programas en System Center Configuration Manager)<br /><br /> [How to deploy configuration baselines in System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md) (Implementación de líneas base de configuración en System Center Configuration Manager)<br /><br /> [Manage task sequences to automate tasks in System Center Configuration Manager](../../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md) (Administración de secuencias de tareas para automatizar tareas en System Center Configuration Manager)<br /><br /> [Administrar actualizaciones de software en System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction)|  

## <a name="how-to-manage-user-collections"></a>Cómo administrar recopilaciones de usuarios  
 En el área de trabajo **Activos y compatibilidad** , seleccione **Recopilaciones de usuarios**, seleccione la recopilación que se debe administrar y luego seleccione una tarea de administración.  

 Utilice la tabla siguiente para obtener más información acerca de las tareas de administración que pueden requerir información para poder seleccionarlas.  

|Tarea de administración|Detalles|Más información|  
|---------------------|-------------|----------------------|  
|**Mostrar miembros**|Muestra todos los recursos que sean miembros de la recopilación seleccionada en un nodo temporal en el nodo **Usuarios** .|No hay información adicional.|  
|**Agregar elementos seleccionados**|Esta opción le permite realizar una de las acciones siguientes:<br /><br /> - <br />                    **Agregar elementos seleccionados a la recopilación de usuario existente**: abre el cuadro de diálogo **Seleccionar recopilación**, donde puede seleccionar la recopilación en la que quiere agregar los miembros de la recopilación seleccionada. La recopilación seleccionada se incluye en esta recopilación mediante una regla de pertenencia **Incluir recopilaciones** .<br /><br /> - **Agregar elementos seleccionados a la nueva recopilación de usuarios**: abre el **Asistente para crear recopilación de usuarios**, donde puede crear una nueva recopilación. La recopilación seleccionada se incluye en esta recopilación mediante una regla de pertenencia **Incluir recopilaciones** .|[Cómo crear recopilaciones en System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|**Administrar solicitudes de afinidad**|Abre el cuadro de diálogo **Administrar solicitudes de afinidad de dispositivo de usuario** , donde puede aprobar o rechazar solicitudes pendientes para establecer afinidades de dispositivos de usuario de usuarios de la recopilación seleccionada.|[Link users and devices with user device affinity in System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) (Vinculación de usuarios y dispositivos con afinidad entre usuario y dispositivo en System Center Configuration Manager).|  
|**Actualizar pertenencia**|Evalúa la pertenencia de la recopilación seleccionada. En las recopilaciones con muchos miembros, esta actualización puede tardar algo de tiempo en finalizar. Utilice la acción **Actualizar** para actualizar la pantalla con los nuevos miembros de las recopilaciones después de que se complete la actualización.<br /><br /> El icono de la recopilación seleccionada mostrará un símbolo de reloj de arena mientras la actualización está en curso.|No hay información adicional.|  
|**Agregar recursos**|Abre el cuadro de diálogo **Agregar recursos a la recopilación** , donde puede buscar nuevos recursos para agregarlos a la recopilación seleccionada.|No hay información adicional.|  
|**Exportarar**|Abre el **Asistente para exportar recopilaciones** que le ayuda a exportar esta recopilación en un archivo MOF que después puede archivarse o utilizarse en otro sitio de Configuration Manager.<br /><br /> Cuando se exporta una recopilación, las recopilaciones a las que hace referencia la recopilación seleccionada mediante una regla de **inclusión** o **exclusión** no se exportan.|No hay información adicional.|  
|**Copiar**|Crea una copia de la recopilación seleccionada. La nueva recopilación utiliza la recopilación seleccionada como una recopilación de restricción.|No hay información adicional.|  
|**Eliminar**|Elimina la recopilación seleccionada. También puede eliminar todos los recursos de la recopilación de la base de datos del sitio.<br /><br /> No se pueden eliminar las recopilaciones integradas en Configuration Manager.|Para obtener una lista de las colecciones integradas, consulte [Introducción a las recopilaciones en System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).|  
|**Simular implementación**|Abre el **Asistente para simular implementación de aplicación** , que le permite probar los resultados de una implementación de aplicación en equipos sin instalar ni desinstalar la aplicación.|[How to simulate application deployments with System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md) (Simulación de implementaciones de aplicaciones con System Center Configuration Manager)|  
|**Implementar**|Se muestran las opciones siguientes:<br /><br /> - **Aplicación**: abre el **Asistente para implementar software**, donde puede seleccionar y configurar una implementación de aplicación en la recopilación seleccionada.<br /><br /> - <br />                    **Programa** : abre el **Asistente para implementar software** , donde puede seleccionar y configurar una implementación de paquete y programa en la recopilación seleccionada.<br /><br /> - **Línea base de configuración**: abre el cuadro de diálogo **Implementar líneas de base de configuración**, donde puede configurar la implementación de una o varias líneas base de configuración en la recopilación seleccionada.|[How to deploy applications with System Center Configuration Manager](../../../../apps/deploy-use/deploy-applications.md) (Implementación de aplicaciones con System Center Configuration Manager)<br /><br /> [Packages and programs in System Center Configuration Manager](../../../../apps/deploy-use/packages-and-programs.md) (Paquetes y programas en System Center Configuration Manager)<br /><br /> [How to deploy configuration baselines in System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md) (Implementación de líneas base de configuración en System Center Configuration Manager)|  

##  <a name="a-namebkmkcollpropa-collection-properties"></a><a name="BKMK_CollProp"></a> Propiedades de recopilación  
 Al abrir el cuadro de diálogo **Propiedades** de una recopilación, puede ver y configurar las siguientes propiedades de una recopilación.  

|Nombre de la pestaña|Más información|  
|--------------|----------------------|  
|**General**|Permite ver y configurar información general sobre la recopilación seleccionada, incluidos el nombre de la recopilación y la recopilación de restricción.|  
|**Reglas de pertenencia**|Permite configurar las reglas de pertenencia que definen la pertenencia de esta recopilación. Para obtener más información, vea [Cómo crear recopilaciones en System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|**Administración de energía**|Permite configurar los planes de administración de energía que se asignan a los equipos de la recopilación seleccionada. Para obtener más información, consulte [Introduction to power management](../../../../core/clients/manage/power/introduction-to-power-management.md) (Introducción a la administración de energía).|  
|**Implementaciones**|Muestra cualquier software que se haya implementado en los miembros de la recopilación seleccionada.|  
|**Ventanas de mantenimiento**|Permite ver y configurar ventanas de mantenimiento que se aplican a los miembros de la recopilación seleccionada. Para obtener más información, consulte [How to use maintenance windows in System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md) (Uso de ventanas de mantenimiento en Configuration Manager).|  
|**Variables de recopilación**|Permite configurar las variables que se aplican a esta recopilación y que las secuencias de tareas pueden utilizar. Para obtener más información, consulte [Variables integradas de secuencia de tareas](../../../../osd/understand/task-sequence-built-in-variables.md).|  
|**Grupos de puntos de distribución**|Permite asociar uno o varios grupos de puntos de distribución a los miembros de la recopilación seleccionada. Para obtener más información, vea [Manage content and content infrastructure for System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administración del contenido y de la infraestructura de contenido en System Center Configuration Manager).|  
|**Seguridad**|Muestra los usuarios administrativos que tienen permisos para la recopilación seleccionada de ámbitos de seguridad y roles asociados.|  
|**Monitor**|Permite configurar cuándo se generan alertas del estado de los clientes y Endpoint Protection. Para obtener más información, vea [How to configure client status in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-status.md) (Configuración del estado de cliente en System Center Configuration Manager) y [How to monitor Endpoint Protection in System Center Configuration Manager](../../../../protect/deploy-use/monitor-endpoint-protection.md) (Supervisión de Endpoint Protection en System Center Configuration Manager).|  



<!--HONumber=Nov16_HO1-->


