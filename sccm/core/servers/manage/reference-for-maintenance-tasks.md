---
title: Referencia de las tareas de mantenimiento
titleSuffix: Configuration Manager
description: Vea la información de las tareas de mantenimiento del sitio de System Center Configuration Manager y compruebe si están habilitadas de forma predeterminada.
ms.date: 3/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5492382afdb523846fcdd40b68d498730073eb7e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342450"
---
# <a name="reference-for-maintenance-tasks-for-system-center-configuration-manager"></a>Referencia de tareas de mantenimiento para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este tema se describen los detalles de las tareas de mantenimiento del sitio de System Center Configuration Manager y se especifica en qué tipos de sitio están disponibles. Además, en cada entrada también se indica si la tarea está habilitada o no de forma predeterminada. Para obtener más información sobre la planeación y la configuración de sitios para ejecutar tareas de mantenimiento, consulte [Tareas de mantenimiento para System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md).  

**Servidor de sitio de copia de seguridad**: use esta tarea para preparar la recuperación de datos críticos. Puede crear una copia de seguridad de su información crítica para restaurar un sitio y la base de datos de Configuration Manager. Para obtener más información, consulte [Copia de seguridad y recuperación de System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

-   **Sitio de administración central**: habilitado    
-   **Sitio primario**: no habilitado    
-   Sitio secundario: no disponible  

**Comprobar título de la aplicación con información de inventario**: use esta tarea para mantener la coherencia entre los títulos de software del inventario de software y los títulos de software del catálogo Asset Intelligence. Para obtener más información, consulte [Introduction to Asset Intelligence in System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md) (Introducción a Asset Intelligence en System Center Configuration Manager).  

-   **Sitio de administración central**: habilitado    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Borrar marca de instalación**: use esta tarea para quitar la marca de instalación de los clientes que no envían un registro de detección de latidos durante el período de **nueva detección de cliente**. La marca instalada evita la instalación de inserción automática de clientes en un equipo que puede tener un cliente de Configuration Manager activo.  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: no habilitado    
-   Sitio secundario: no disponible  

**Eliminar datos antiguos de solicitud de la aplicación**: use esta tarea para eliminar de la base de datos las solicitudes antiguas de la aplicación. Para obtener más información sobre las solicitudes de la aplicación, consulte [Crear e implementar una aplicación con System Center Configuration Manager](/sccm/apps/get-started/create-and-deploy-an-application).  

-   Sitio de administración central: no disponible
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar historial de descargas de clientes antiguos**: use esta tarea para eliminar datos históricos sobre el origen de descarga que usan los clientes. La información del origen de descarga se utiliza para rellenar el [panel orígenes de datos de cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).  
-  Sitio de administración central (no disponible)
-    **Sitio primario**: habilitado
-  Sitio secundario: no disponible

**Eliminar operaciones cliente antiguas**: use esta tarea para eliminar de la base de datos del sitio los datos antiguos en las operaciones de cliente. Por ejemplo, esto incluye datos para las notificaciones de cliente antiguas o caducadas (como descargar solicitudes para directivas de equipo o usuario) y para Endpoint Protection (como las solicitudes realizadas por un usuario administrativo para que los clientes ejecuten un análisis o descarguen definiciones actualizadas).

-   **Sitio de administración central**: habilitado    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Historial de presencias de cliente vencidas eliminado**: use esta tarea para eliminar la información del historial sobre el estado de conexión de los clientes (registrado por la notificación de cliente) anterior a la hora especificada. Para obtener más información sobre la notificación del cliente, consulte [How to monitor clients in System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md) (Cómo supervisar clientes en System Center Configuration Manager).  

-   **Sitio de administración central**: habilitado   
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar datos antiguos del tráfico de la puerta de enlace de administración en la nube**: use esta tarea para eliminar todos los datos antiguos sobre el tráfico que atraviesa la [puerta de enlace de administración en la nube](/sccm/core/clients/manage/plan-cloud-management-gateway) desde la base de datos del sitio. Por ejemplo, esto incluye datos sobre el número de solicitudes, bytes de solicitud totales, bytes de respuesta totales, número de solicitudes con error y número máximo de solicitudes simultáneas.  
- **Sitio de administración central**: habilitado
- **Sitio primario**: habilitado
- Sitio secundario: no disponible


**Eliminar archivos recopilados antiguos**: use esta tarea para eliminar de la base de datos la información antigua sobre los archivos recopilados. Esta tarea también elimina los archivos recopilados desde la estructura de carpetas del servidor de sitio en el sitio seleccionado. De forma predeterminada, las cinco copias más recientes de los archivos recopilados se almacenan en el servidor de sitio en el directorio de **Inboxes\sinv.box\FileCol**. Para obtener más información, consulte [Introduction to software inventory in System Center Configuration Manager](/sccm/core/clients/manage/inventory/introduction-to-software-inventory) (Introducción al inventario de software en System Center Configuration Manager).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar datos antiguos de asociación de equipos**: use esta tarea para eliminar de la base de datos los datos antiguos de asociación de equipos de implementación de sistema operativo. Esta información se utiliza como parte de la realización de restauraciones de estado del usuario. Para obtener más información sobre las asociaciones de equipo, consulte [Manage user state in System Center Configuration Manager](../../../osd/get-started/manage-user-state.md) (Administrar el estado de usuario en System Center Configuration Manager).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar datos antiguos de detección de eliminación**: use esta tarea para eliminar de la base de datos los datos antiguos creados por las vistas de extracción. De forma predeterminada, las vistas de extracción están deshabilitadas. Solo se pueden habilitar con el SDK de Configuration Manager. Salvo que las vistas de extracción estén habilitadas, esta tarea no eliminará ningún dato.  

-   **Sitio de administración central**: habilitado    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar registro antiguo de borrado de dispositivo**: use esta tarea para eliminar de la base de datos los datos antiguos sobre acciones de borrado de dispositivos móviles. Para obtener más información sobre el borrado de dispositivos móviles, consulte [Protección de datos mediante eliminación remota, bloqueo o restablecimiento de código de acceso mediante System Center Configuration Manager](/sccm/mdm/deploy-use/wipe-lock-reset-devices).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar dispositivos antiguos administrados por el conector de Exchange Server**: use esta tarea para eliminar datos antiguos sobre los dispositivos móviles administrados por el conector de Exchange Server. Estos datos se eliminan según el intervalo configurado para la opción **Omitir dispositivos móviles que hayan estado inactivos durante más de (días)** en la pestaña **Detección** de las propiedades del conector de Exchange Server. Para más información, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

-   Sitio de administración central: no disponible   
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar datos de detección antiguos**: use esta tarea para eliminar de la base de datos los datos de detección antiguos. Estos datos pueden contener registros de detección de latidos, detección de redes y métodos de detección de Active Directory Domain Services (sistema, usuario y grupo). Esta tarea también quitará los dispositivos antiguos marcados como retirados. Cuando se ejecuta esta tarea en un sitio, se eliminan los datos asociados a ese sitio, y esos cambios se replican a otros sitios. Para obtener información sobre la detección, consulte [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md) (Ejecutar la detección para System Center Configuration Manager).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar datos antiguos de uso de punto de distribución**: use esta tarea para eliminar de la base de datos los datos antiguos de puntos de distribución que se hayan almacenado durante más tiempo del especificado.  

-   **Sitio de administración central**: habilitado    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar datos antiguos del historial de estado de mantenimiento de Endpoint Protection**: use esta tarea para eliminar de la base de datos la información de estado antigua de Endpoint Protection. Para obtener más información sobre la información de estado de Endpoint Protection, consulte [How to monitor Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md) (Cómo supervisar Endpoint Protection en System Center Configuration Manager).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar dispositivos inscritos antiguos**: a partir de la actualización de 1602, esta tarea está deshabilitada de forma predeterminada. Puede usar esta tarea para eliminar de la base de datos del sitio los datos antiguos sobre dispositivos móviles que no han enviado información al sitio durante un tiempo especificado.

Esta tarea se aplica en dispositivos inscritos con Microsoft Intune (híbrido) o con la administración de dispositivos móviles local de Configuration Manager. Para obtener más información sobre los sistemas operativos de los dispositivos inscritos con Configuration Manager o Intune, consulte la sección [Dispositivos móviles inscritos por Microsoft Intune](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mobile-devices-enrolled-by-microsoft-intune) de [Sistemas operativos compatibles con dispositivos y clientes de System Center Configuration Manager](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

-   Sitio de administración central: no disponible    
-   **Sitio primario**: no habilitado    
-   Sitio secundario: no disponible  

**Eliminar historial de inventario antiguo**: use esta tarea para eliminar de la base de datos los datos de inventario almacenados durante más tiempo del especificado. Para obtener información sobre el historial de inventario, consulte [Cómo usar el Explorador de recursos para ver el inventario de Hardware en Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar datos de registro antiguos**: use esta tarea para eliminar de la base de datos los datos de registro antiguos usados para solucionar problemas. Estos datos no están relacionados con las operaciones de componentes de Configuration Manager.  

> [!IMPORTANT]  
> De forma predeterminada, esta tarea se ejecuta a diario en cada sitio. En un sitio de administración central y en sitios primarios, la tarea elimina los datos más antiguos de 30 días. Al usar SQL Server Express en un sitio secundario, asegúrese de que esta tarea se ejecute todos los días y que elimine los datos que hayan estado inactivos durante siete días.  

-   **Sitio de administración central**: habilitado    
-   **Sitio primario**: habilitado    
-   **Sitio secundario**: habilitado  

**Eliminar historial de tareas de notificación vencidas**: use esta tarea para eliminar de la base de datos del sitio la información sobre tareas de notificación de cliente cuando no se ha actualizado durante un período de tiempo especificado. Para obtener más información sobre las notificaciones de cliente, consulte [Tareas de implementación de cliente para System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar datos de resumen de replicación vencidos**: use esta tarea para eliminar datos de resumen de replicación antiguos de la base de datos del sitio (si no se han actualizado durante un período de tiempo especificado). Para obtener más información, consulte la sección [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) (Cómo supervisar los vínculos de replicación de bases de datos y el estado de replicación) del tema [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) (Supervisar la infraestructura de la jerarquía y replicación en System Center Configuration Manager).  

-   **Sitio de administración central**: habilitado    
-   **Sitio primario**: habilitado    
-   **Sitio secundario**: habilitado  

**Eliminar registros de códigos de accesos antiguos**: use esta tarea en el sitio de primer nivel de la jerarquía para eliminar datos antiguos sobre restablecimientos de códigos de acceso para dispositivos Android y Windows Phone. Los datos de restablecimiento de código de acceso están cifrados, pero contienen el PIN para dispositivos. De forma predeterminada, esta tarea está habilitada y elimina los datos anteriores a un día.  

-   **Sitio de administración central**: habilitado    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar datos antiguos de seguimiento de replicación**: use esta tarea para eliminar de la base de datos los datos antiguos sobre la replicación de base de datos entre los sitios de Configuration Manager. Si cambia la configuración de esta tarea de mantenimiento, la configuración se aplica a todos los sitios aplicables en la jerarquía. Para obtener más información, consulte la sección [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) (Cómo supervisar los vínculos de replicación de bases de datos y el estado de replicación) del tema [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) (Supervisar la infraestructura de la jerarquía y replicación en System Center Configuration Manager).  

-   **Sitio de administración central**: habilitado    
-   **Sitio primario**: habilitado    
-   **Sitio secundario**: habilitado  

**Eliminar datos antiguos de disponibilidad de software**: use esta tarea para eliminar de la base de datos los datos antiguos sobre la medición de software almacenados durante más tiempo del especificado. Para obtener más información, consulte [Medición de software en System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar datos antiguos de resumen de disponibilidad de software**: use esta tarea para eliminar de la base de datos los datos antiguos de resumen de la medición de software almacenados durante más tiempo del especificado. Para obtener más información, consulte [Medición de software en System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar mensajes de estado antiguos**: use esta tarea para eliminar de la base de datos los datos de mensajes de estado antiguos según la configuración de las reglas de filtro de estado. Para obtener más información, consulte la sección “Supervisar el sistema de estado de Configuration Manager” del tema [Usar alertas y el sistema de estado de System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   **Sitio de administración central**: habilitado    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar datos de amenaza antiguos**: use esta tarea para eliminar de la base de datos los datos de amenazas antiguos de Endpoint Protection almacenados durante más tiempo del especificado. Para obtener información sobre Endpoint Protection, consulte [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md) (Endpoint Protection en System Center Configuration Manager).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar equipos desconocidos vencidos**: use esta tarea para eliminar de la base de datos del sitio la información sobre equipos desconocidos cuando no se ha actualizado durante un tiempo especificado. Para obtener más información, consulte [Prepare for unknown computer deployments in System Center Configuration Manager](../../../osd/get-started/prepare-for-unknown-computer-deployments.md) (Preparación para implementaciones en equipos desconocidos en System Center Configuration Manager).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar datos antiguos de afinidad de dispositivo del usuario**: use esta tarea para eliminar de la base de datos los datos antiguos de afinidad de dispositivo del usuario. Para obtener más información, consulte [Link users and devices with user device affinity in System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) (Vincular usuarios y dispositivos con afinidad entre usuario y dispositivo en System Center Configuration Manager).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar registros expirados del paquete de inscripción masiva de MDM**: use esta tarea para eliminar certificados antiguos de inscripción masiva y los perfiles correspondientes después de que caduque el certificado de inscripción. Para más información, vea [Crear perfiles de certificado](/sccm/protect/deploy-use/create-certificate-profiles).
-   **Sitio de administración central**: habilitado
-   **Sitio primario**: habilitado
-   Sitio secundario: no disponible

**Eliminar datos de detección de cliente inactivos**: use esta tarea para eliminar de la base de datos los datos de detección de clientes inactivos. Los clientes se marcan como inactivos cuando el cliente se marca como obsoleto y por las configuraciones realizadas para el estado de cliente.

Esta tarea solo funciona en los recursos que son clientes de Configuration Manager. Es diferente de la tarea **Eliminar datos de detección antiguos**, que elimina los registros de datos de detección antiguos. Cuando esta tarea se ejecuta en un sitio, quita los datos de la base de datos en todos los sitios de la jerarquía. Para más información, vea [Cómo configurar el estado de cliente en System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md).  

> [!IMPORTANT]  
> Si está habilitada, configure esta tarea para que se ejecute con un intervalo mayor que la programación de **detección de latidos**. Esto permite que los clientes activos envíen un registro de detección de latidos para marcar su registro de clientes como activo para que esta tarea no los elimine.  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: no habilitado    
-   Sitio secundario: no disponible  

**Eliminar alertas obsoletas**: use esta tarea para eliminar de la base de datos las alertas expiradas almacenadas durante más tiempo del especificado. Para obtener más información, consulte [Use alerts and the status system for System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md) (Usar alertas y el sistema de estado para System Center Configuration Manager).  

-   **Sitio de administración central**: habilitado    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar datos obsoletos de detección de cliente**: use esta tarea para eliminar de la base de datos los registros de cliente obsoletos. Por lo general, un registro marcado como obsoleto suele reemplazarse por registro más reciente para el mismo cliente. El registro más reciente se convierte en el registro actual del cliente. Para obtener información sobre la detección, consulte [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md) (Ejecutar la detección para System Center Configuration Manager).  

> [!IMPORTANT]  
> Si está habilitada, configure esta tarea para que se ejecute con un intervalo mayor que la programación de detección de latidos. Esto le permite al cliente enviar un registro de detección de latidos que establece correctamente el estado obsoleto.  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: no habilitado    
-   Sitio secundario: no disponible  

**Eliminar sitios y subredes obsoletos de detección de bosque**: use esta tarea para eliminar datos sobre sitios, subredes y dominios de Active Directory que el método de detección de bosques de Active Directory no ha detectado en los últimos 30 días. Esto elimina los datos de detección, pero no afecta a los límites creados desde estos datos de detección. Para obtener más información, consulte [Ejecutar la detección para System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

-   **Sitio de administración central**: habilitado    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Eliminar registros huérfanos de estado de implementación de cliente**: use esta tarea para purgar periódicamente la tabla que contiene información de estado de implementación de cliente. Esta tarea limpiará los registros asociados con dispositivos obsoletos o retirados.  
-   **Sitio de administración central**: habilitado    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible

**Eliminar revisiones de la aplicación sin usar**: use esta tarea para eliminar revisiones de la aplicación a las que ya no se hace referencia. Para obtener más información, consulte [How to revise and supersede applications in System Center Configuration Manager](../../../apps/deploy-use/revise-and-supersede-applications.md) (Cómo revisar y sustituir aplicaciones en System Center Configuration Manager).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Evaluar miembros de la recopilación**: puede configurar la evaluación de pertenencia a recopilación como componente del sitio. Para obtener información sobre los componentes del sitio, consulte [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md) (Componentes de sitio para System Center Configuration Manager).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Supervisar claves**: use esta tarea para supervisar la integridad de las claves principales de la base de datos de Configuration Manager. Una clave principal es una columna (o una combinación de columnas) que identifica de manera única una fila y la diferencia de otras filas en una tabla de base de datos de Microsoft SQL Server.  

-   **Sitio de administración central**: habilitado    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Recompilar índices**: use esta tarea para recompilar los índices de la base de datos de Configuration Manager. Un índice es una estructura de base de datos que se crea en una tabla de base de datos para acelerar la recuperación de datos. Por ejemplo, buscar en una columna indexada suele ser mucho más rápido que buscar en una columna no indexada.

Para mejorar el rendimiento, los índices de la base de datos de Configuration Manager se actualizan con frecuencia para permanecer sincronizados con los datos que se almacenan en la base de datos y que cambian continuamente. Esta tarea crea índices en columnas de base de datos que son como mínimo 50% únicas, retira los índices de las columnas que son menos de un 50% únicas y recompila los índices existentes que cumplen los criterios de unicidad de los datos.  

-   **Sitio de administración central**: no habilitado    
-   **Sitio primario**: no habilitado    
-   **Sitio secundario**: no habilitado  

**Resumir datos de software instalado**: use esta tarea para resumir los datos del software instalado de varios registros en un solo registro general. El resumen de datos puede comprimir los datos almacenados en la base de datos de Configuration Manager. Para obtener más información, consulte [Introduction to software inventory in System Center Configuration Manager](../../clients/manage/inventory\introduction-to-software-inventory.md) (Introducción al inventario de software en System Center Configuration Manager).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Resumir datos de uso de archivo de disponibilidad de software**: use esta tarea para resumir los datos de varios registros para el uso de archivos de medición de software en un único registro general. El resumen de datos puede comprimir los datos almacenados en la base de datos de Configuration Manager.

Puede usar esta tarea con la tarea **Resumir datos de uso mensual de disponibilidad de software** para resumir los datos de medición de software y conservar espacio en disco en la base de datos de Configuration Manager. Para obtener más información, consulte [Medición de software en System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Resumir datos de uso mensual de disponibilidad de software**: use esta tarea para resumir los datos de varios registros de uso mensual de medición de software en un único registro general. El resumen de datos puede comprimir los datos almacenados en la base de datos de Configuration Manager.

Puede usar esta tarea con la tarea **Resumir datos de uso de archivo de disponibilidad de software** para resumir los datos de medición de software y para conservar espacio en la base de datos de Configuration Manager. Para obtener más información, consulte [Medición de software en System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Actualizar destinatarios disponibles de la aplicación**: use esta tarea para que Configuration Manager actualice la asignación de las implementaciones de directiva y aplicación a los recursos en colecciones. Al implementar directivas o aplicaciones en una colección, Configuration Manager crea una asignación inicial entre los objetos que implemente y los miembros de la recopilación.

Estas asignaciones se almacenan en una tabla para una referencia rápida. Cuando cambia la pertenencia a colecciones, estas asignaciones almacenadas se actualizan para reflejar estos cambios. En cambio, es posible que estas asignaciones no se sincronicen. Por ejemplo, si el sitio no puede procesar correctamente un archivo de notificación, es posible que ese cambio no se refleje en un cambio en las asignaciones. Esta tarea actualiza esa asignación según la pertenencia a la colección actual.  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  

**Actualizar tablas del catálogo de aplicaciones**: use esta tarea para sincronizar la memoria caché de la base de datos del sitio web del catálogo de aplicaciones con la información más reciente de la aplicación. Si cambia la configuración de esta tarea de mantenimiento, la configuración se aplica a todos los sitios primarios en la jerarquía.  

-   Sitio de administración central: no disponible    
-   **Sitio primario**: habilitado    
-   Sitio secundario: no disponible  
