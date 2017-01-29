---
title: "Lista de comprobación para la versión 1606 | Microsoft Docs"
description: "Obtenga información sobre los pasos necesarios previos a la actualización de la versión 1511 o 1602 de System Center Configuration Manager a la versión 1606."
ms.custom: na
ms.date: 1/11/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0d0735c170820259ac8bb6706aac7cc5569a1628
ms.openlocfilehash: ca0916791ccfba921866ebed7da0e2dc365f933b

---
# <a name="checklist-for-installing-update-1606-for-system-center-configuration-manager"></a>Lista de comprobación para la instalación de la actualización 1606 de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

La versión 1606 para la rama actual de System Center Configuration Manager es una actualización que se puede usar para actualizar desde la versión 1511 o 1602.

Antes de instalar la versión 1606 como una actualización, lea la información siguiente y la lista de comprobación para conocer los pasos necesarios antes del inicio de la actualización.

Para más información sobre las versiones de línea base, vea [Baseline and update versions (Versiones de línea base y actualización)](../../../core/servers/manage/updates.md#bkmk_Baselines) en [Updates for System Center Configuration Manager (Actualizaciones para System Center Configuration Manager)](../../../core/servers/manage/updates.md).

 ## <a name="about-installing-update-1606"></a>Acerca de la instalación de la actualización 1606

Como *actualización*, 1606 solo puede instalarse en el sitio de nivel superior de la jerarquía. Esto significa que se inicie la instalación desde el sitio de administración central, si existe, o desde el sitio primario independiente.  

-   Los sitios primarios secundarios realizan la instalación de la actualización automáticamente después de que el sitio de administración central haya terminado de instalarla. Puede usar períodos para tareas administrativas para controlar el momento en que un sitio instala actualizaciones. Antes de la versión 1606, los períodos para tareas administrativas se denominaban ventanas de mantenimiento. Para más información, vea [Ventanas de servicio para servidores de sitio](/sccm/core/servers/manage/service-windows).  

-   Una vez que el sitio principal primario termine de instalar la actualización, tendrá que actualizar manualmente los sitios secundarios desde la consola de Configuration Manager. No se admite la actualización automática de los servidores de sitio secundario.  

Cuando el servidor de sitio instala la actualización, los roles de sistema de sitio instalados en el servidor de sitio y en los equipos remotos se actualizan automáticamente. Por lo tanto, antes de instalar la actualización, asegúrese de que cada servidor de sistema de sitio cumple los requisitos previos nuevos de funcionamiento con la nueva versión de actualización.  

 La primera vez que use una consola de Configuration Manager tras el término de la actualización, se le pedirá que actualice esa consola.  Para ello, debe ejecutar el programa de instalación de Configuration Manager en el equipo que hospeda la consola y seleccionar la opción para actualizarla. Se recomienda no retrasar la instalación de la actualización de la consola.

 **Problemas conocidos de esta actualización**   
  En el estado de la instalación del paquete de actualización se pueden ver los siguientes problemas:
  - Al actualizar desde la versión 1602 a la 1606, el paso **Extraer carga de paquete de actualización** muestra el estado **No iniciada**, aun cuando la descarga ha terminado.
  - Al actualizar desde la versión 1511 a la 1606, algunos pasos mostrarán el estado **Completado**, pero no el valor de **Hora de la última actualización**.


## <a name="checklist"></a>Lista de comprobación  

 **Asegurarse de que todos los sitios tengan una versión compatible de System Center Configuration Manager:** antes de iniciar la instalación de la actualización 1606, cada servidor de sitio de la jerarquía debe tener la misma versión de System Center Configuration Manager, ya sea la 1511 o la 1602.

 **Revisar las versiones instaladas de .NET en los servidores del sistema de sitio:** cuando un sitio instala la actualización 1606, si todavía no está instalado .NET Framework 4.5 o posterior, Configuration Manager instala automáticamente .NET Framework 4.5.2 en cada equipo que hospeda alguno de los siguientes roles del sistema de sitio:  

-   punto de proxy de inscripción  

-   punto de inscripción  

-   punto de administración  

-   Punto de conexión de servicio  

Esta instalación puede poner el servidor de sistema de sitio en un estado pendiente de reinicio y notificar errores en el visor de estado de componentes de Configuration Manager. Además, las aplicaciones .NET del servidor pueden presentar errores aleatorios hasta que se reinicia el servidor.  

 Para más información, vea [Site and site system prerequisites (Requisitos previos del sitio y el sistema de sitio)](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  

 **Revisar el estado del sitio y la jerarquía, y comprobar que no hay problemas sin resolver:** antes de actualizar un sitio, resuelva todos los problemas de funcionamiento para el servidor de sitio, el servidor de base de datos del sitio y los roles de sistema de sitio instalados en equipos remotos. Una actualización del sitio puede generar errores debido a problemas de funcionamiento existentes.  
 Para más información, vea [Use alerts and the status system for System Center Configuration Manager (Usar las alertas y el sistema de estado de System Center Configuration Manager)](../../../core/servers/manage/use-alerts-and-the-status-system.md)  

 **Revisar la replicación de archivos y datos entre sitios:**  asegúrese de que la replicación de archivos y base de datos entre sitios funciona y está actualizada. Los retrasos o los trabajos pendientes pueden impedir una actualización correcta o sin problemas.    
Para la replicación de base de datos, puede utilizar Replication Link Analyzer para ayudar a resolver problemas antes de iniciar la actualización.    
 Para más información, consulte   
[About the Replication Link Analyzer (Acerca de Replication Link Analyzer)](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) en el tema [Monitor hierarchy and replication infrastructure in System Center Configuration Manager (Supervisar la infraestructura de jerarquía y replicación en System Center Configuration Manager)](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

 **Instalar todas las actualizaciones críticas aplicables para los sistemas operativos en equipos que hospedan el sitio, el servidor de base de datos del sitio y los roles del sistema de sitio remoto:** antes de instalar una actualización para Configuration Manager, instale todas las actualizaciones críticas para cada sistema de sitio aplicable. Si alguna de las actualizaciones que instala requiere un reinicio, reinicie los equipos correspondientes antes de iniciar la actualización.  

 **Deshabilitar réplicas de bases de datos para puntos de administración en sitios primarios:** Configuration Manager no puede actualizar correctamente un sitio primario que tiene habilitada una réplica de base de datos para puntos de administración. Deshabilite la replicación de base de datos antes de:  

-   Crear una copia de seguridad de la base de datos del sitio para probar la actualización de la base de datos.  

-   Instalar una actualización para Configuration Manager  

Para obtener más información, consulte   
[Database replicas for management points for System Center Configuration Manager (Réplicas de bases de datos para puntos de administración de System Center Configuration Manager)](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)  

 **Establecer los grupos de disponibilidad AlwaysOn de SQL Server en conmutación por error manual:**  
 Antes de instalar las actualizaciones, como en la versión 1606, asegúrese de que el grupo de disponibilidad está establecido para la conmutación por error manual. Después de que se actualice el sitio, puede restaurar la conmutación por error a automática. Para más información, vea [SQL Server AlwaysOn para una base de datos de sitio](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

 **Volver a configurar los puntos de actualización de software que usan NLB:** Configuration Manager no puede actualizar un sitio que use un clúster de equilibrio de carga de red (NLB) para hospedar puntos de actualización de software.  
Si utiliza clústeres NLB para puntos de actualización de software, use PowerShell para quitar el clúster NLB.    

 Para más información, vea [Planear las actualizaciones de software en System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

 **Deshabilitar todas las tareas de mantenimiento de sitio en cada sitio mientras dura la instalación de la actualización en el sitio:** antes de instalar la actualización, deshabilite cualquier tarea de mantenimiento de sitio que podría ejecutarse mientras el proceso de actualización está activo. Esto incluye, entre otras cosas, lo siguiente:  

-   Copia de seguridad del servidor del sitio  

-   Eliminar operaciones cliente antiguas  

-   Eliminar datos de detección antiguos  

Cuando se ejecuta una tarea de mantenimiento de la base de datos de sitio durante la instalación de la actualización, se puede producir un error en la instalación de la actualización. Antes de deshabilitar una tarea, programe la tarea de forma que pueda restaurar su configuración después de que se haya instalado la actualización.  
 Para más información, vea [Maintenance tasks for System Center Configuration Manager (Tareas de mantenimiento para System Center Configuration Manager)](../../../core/servers/manage/maintenance-tasks.md) y [Referencia de tareas de mantenimiento para System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 **Crear una copia de seguridad de la base de datos del sitio en el sitio de administración central y en los sitios primarios:** antes de actualizar un sitio, realice una copia de seguridad del sitio para asegurarse de que tiene una copia de seguridad correcta para utilizarla en la recuperación ante desastres.   
Para más información, vea [Copia de seguridad y recuperación de System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  


 **Probar la actualización de la base de datos en una copia de la última copia de seguridad de la base de datos del sitio:** antes de actualizar un sitio primario o un sitio de administración central de System Center Configuration Manager, pruebe el proceso de actualización de la base de datos del sitio en una copia de la base de datos del sitio.  

-   Debe probar el proceso de actualización de base de datos del sitio porque, al actualizar un sitio, la base de datos del sitio podría modificarse.  

-   Aunque una actualización de base de datos de prueba no es necesaria, puede identificar problemas de la actualización antes de que la base de datos de producción se vea afectada.  

-   Una actualización incorrecta de la base de datos del sitio podría inutilizar la base de datos del sitio, en cuyo caso podría ser necesaria una recuperación del sitio para restaurar la funcionalidad.  

-   Aunque se trate de una base de datos de sitio compartida entre varios sitios de una jerarquía, planee la prueba de la base de datos en cada uno de los sitios correspondientes antes de actualizar el sitio.  

-   Si usa réplicas de base de datos para puntos de administración en un sitio primario, deshabilite la replicación antes de crear la copia de seguridad de la base de datos del sitio.  

Configuration Manager no admite la realización de copias de seguridad de sitios secundarios ni la actualización de prueba de una base de datos de un sitio secundario.   
No se puede ejecutar una actualización de prueba de base de datos en la base de datos del sitio de producción. Esta acción actualiza la base de datos del sitio y podría inutilizar el sitio. Para más información, vea la sección [Test the site database upgrade (Probar la actualización de la base de datos del sitio)](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_test) de [Upgrade to System Center Configuration Manager (Actualizar a System Center Configuration Manager)](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

 **Plan piloto de cliente:** al instalar una actualización que actualiza el cliente, puede probar esa nueva actualización de cliente en preproducción antes de que implemente y actualice todos los clientes activos.   
 Para aprovechar las ventajas de esta opción, antes de comenzar la instalación de la actualización, debe configurar el sitio para admitir las actualizaciones automáticas de preproducción. Para más información, vea [Upgrade clients in System Center Configuration Manager (Actualizar clientes en System Center Configuration Manager)](../../../core/clients/manage/upgrade/upgrade-clients.md) y   
[Cómo probar las actualizaciones de cliente en una recopilación de preproducción en System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md)  

 **Planear el uso de períodos para tareas administrativas**  
 **para controlar el momento en que los servidores de sitio instalan actualizaciones:** puede usar períodos para tareas administrativas para definir un período aplicable a un servidor de sitio primario durante el cual se pueden instalar las actualizaciones para ese sitio.   
Esto puede ayudarle a controlar el momento en que los sitios de la jerarquía instalan la actualización.
Antes de la versión 1606, los períodos para tareas administrativas se denominaban ventanas de mantenimiento. Para más información, vea [Ventanas de servicio para servidores de sitio](/sccm/core/servers/manage/service-windows).  

 **Ejecutar el Comprobador de requisitos previos del programa de instalación:** antes de instalar la actualización 1606, puede ejecutar el Comprobador de requisitos previos independientemente de la instalación de la actualización. Al instalar la actualización en el sitio, el Comprobador de requisitos previos vuelve a ejecutarse.  
Para más información, vea **Step 3: Run the prerequisite checker before installing an update (Paso 3: ejecutar el Comprobador de requisitos previos antes de instalar una actualización)** en el tema [Updates for System Center Configuration Manager (Actualizaciones para System Center Configuration Manager)](../../../core/servers/manage/install-in-console-updates.md).  

> [!IMPORTANT]  
>  Cuando se ejecuta el Comprobador de requisitos previos como parte de la instalación de una actualización o de forma independiente, el proceso actualiza algunos archivos de origen del producto que se utilizan para tareas de mantenimiento del sitio. Por lo tanto, después de ejecutar el Comprobador de requisitos previos pero antes de instalar la actualización 1606, si tiene que realizar una tarea de mantenimiento del sitio, ejecute **Setupwpf.exe** (programa de instalación de Configuration Manager) desde la carpeta CD.Latest en el servidor de sitio.  

 **Actualizar sitios:** ya está listo para iniciar la instalación de la actualización de la jerarquía.  
  Se recomienda planear la instalación de la actualización fuera del horario comercial habitual para cada sitio, ya que será el momento en que el proceso de instalación de la actualización y sus acciones para volver a instalar los componentes del sitio y los roles de sistema de sitio afectarán menos a las operaciones comerciales. Para más información, vea [Updates for System Center Configuration Manager (Actualizaciones para System Center Configuration Manager)](../../../core/servers/manage/updates.md).  



<!--HONumber=Jan17_HO2-->


