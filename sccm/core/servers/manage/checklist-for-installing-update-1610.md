---
title: "Lista de comprobación para la versión 1610 | System Center Configuration Manager"
description: "Obtenga información sobre las acciones que se deben realizar antes de actualizar a la versión 1610 de System Center Configuration Manager."
ms.custom: na
ms.date: 1/7/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0d0735c170820259ac8bb6706aac7cc5569a1628
ms.openlocfilehash: 3ad5ca180759769bc22300eb406df4f606bfbd13

---
# <a name="checklist-for-installing-update-1610-for-system-center-configuration-manager"></a>Lista de comprobación para la instalación de la actualización 1610 de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Cuando usa la rama actual de System Center Configuration Manager, puede instalar la actualización en la consola para la versión 1610 para actualizar su jerarquía desde la versión 1606. Si su jerarquía ejecuta la versión 1511, 1602 o 1606, puede actualizar a la versión 1610.

Para obtener la actualización de la versión 1610, debe usar un rol de sistema de sitio de punto de conexión del servicio en el sitio de nivel superior de su jerarquía. Esto puede realizarse en el modo en línea o sin conexión. Después de que su jerarquía descargue el paquete de actualización de Microsoft, lo encontrará en la consola en **Administración&gt;Información general&gt;Cloud Services&gt;Actualizaciones y mantenimiento**.

-   Cuando la actualización aparezca como **Disponible**, ya está lista para instalarse. Antes de instalar la versión 1610, revise la siguiente información [sobre la instalación de la actualización 1610](#about-installing-update-1610) y la [lista de comprobación](#checklist) de las configuraciones que deben realizarse antes de iniciar la actualización.

-   Si la actualización se muestra como **Descargando** y no cambia, revise los archivos **hman.log** y **dmpdownloader.log** para ver los errores.

    -   Normalmente, también puede reiniciar el servicio de SMS\_EXECUTIVE en el servidor de sitio para reiniciar la descarga de los archivos de redistribución de actualizaciones.

    -   Otro problema común de descarga se debe a la configuración del servidor proxy que impide las descargas desde <http://silverlight.dlservice.microsoft.com> y <http://download.microsoft.com>.

Para obtener más información sobre la instalación de actualizaciones, consulte [Actualizaciones y servicio en la consola](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Para obtener más información sobre las versiones de la rama actual, consulte [Versiones de línea de base y versiones de actualización](/sccm/core/servers/manage/updates#bkmk_Baselines) en [Actualizaciones para System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="about-installing-update-1610"></a>Sobre la instalación de la actualización 1610

**Sitios:**  
La actualización 1610 solo puede instalarse en el sitio de nivel superior de la jerarquía. Esto significa que se inicie la instalación desde el sitio de administración central, si existe, o desde el sitio primario independiente. Después de que la actualización se instale en el sitio de nivel superior, los sitios secundarios tienen el siguiente comportamiento de actualización:

-   Los sitios primarios secundarios realizan la instalación de la actualización automáticamente después de que el sitio de administración central haya terminado de instalarla. Puede usar períodos para tareas administrativas para controlar el momento en que un sitio instala actualizaciones. Antes de la versión 1606, los períodos para tareas administrativas se denominaban ventanas de mantenimiento. Para más información, vea [Ventanas de servicio para servidores de sitio](/sccm/core/servers/manage/service-windows).

-   Una vez que el sitio principal primario termine de instalar la actualización, tendrá que actualizar manualmente los sitios secundarios desde la consola de Configuration Manager. No se admite la actualización automática de los servidores de sitio secundario.

**Roles de sistema de sitio:**  
Cuando el servidor de sitio instala la actualización, los roles de sistema de sitio instalados en el servidor de sitio y en los equipos remotos se actualizan automáticamente. Por lo tanto, antes de instalar la actualización, asegúrese de que cada servidor de sistema de sitio cumple los requisitos previos nuevos de funcionamiento con la nueva versión de actualización.

**Consolas de Configuration Manager:**   
La primera vez que use una consola de Configuration Manager tras el término de la actualización, se le pedirá que actualice esa consola. Para ello, debe ejecutar el programa de instalación de Configuration Manager en el equipo que hospeda la consola y seleccionar la opción para actualizarla. Se recomienda no retrasar la instalación de la actualización de la consola.



## <a name="checklist"></a>Lista de comprobación

**Asegurarse de que todos los sitios ejecutan una versión compatible de System Center Configuration Manager:** antes de iniciar la instalación de la actualización 1610, cada sitio de la jerarquía debe ejecutar la misma versión de System Center Configuration Manager, ya sea la versión 1511, 1602 o 1606.

**Revisar el estado de Software Assurance o de los derechos de suscripción equivalentes:**   
Debe tener un contrato de Software Assurance (SA) activo para instalar la actualización 1610. Cuando instale la versión 1610, tendrá la opción en la pestaña **Licencias** para confirmar la **fecha de vencimiento de Software Assurance**. Este es un valor opcional que puede especificar como un recordatorio útil de la fecha de vencimiento de su licencia que está visible al instalar futuras actualizaciones. Si ha instalado Configuration Manager desde el medio de línea base de la versión 1606, puede que haya especificado este valor anteriormente durante la instalación, o después de que el sitio se haya instalado en la pestaña **Licencias** de la **Configuración de jerarquía**.

Para obtener más información, consulte [Licensing and branches for System Center Configuration Manager (Licencias y ramas para System Center Configuration Manager)](/sccm/core/understand/learn-more-editions).

**Revisar las versiones instaladas de .NET en los servidores del sistema de sitio:** cuando un sitio instala la actualización 1610, Configuration Manager instala automáticamente .NET Framework 4.5.2 en cada equipo que hospeda alguno de los siguientes roles del sistema de sitio cuando .NET Framework 4.5 o versiones posteriores todavía no está instalado:

-   punto de proxy de inscripción
-   punto de inscripción
-   punto de administración
-   Punto de conexión de servicio

Esta instalación puede poner el servidor de sistema de sitio en un estado pendiente de reinicio y notificar errores en el visor de estado de componentes de Configuration Manager. Además, las aplicaciones .NET del servidor pueden presentar errores aleatorios hasta que se reinicia el servidor.

Para obtener más información, consulte [Requisitos previos de sitio y sistema de sitio para System Center Configuration Manager](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

**Revisar el estado del sitio y la jerarquía, y comprobar que no hay problemas sin resolver:** antes de actualizar un sitio, resuelva todos los problemas de funcionamiento para el servidor de sitio, el servidor de base de datos del sitio y los roles de sistema de sitio instalados en equipos remotos. Una actualización del sitio puede generar errores debido a problemas de funcionamiento existentes.

Para obtener más información, consulte [Use alerts and the status system for System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system) (Usar alertas y el sistema de estado para System Center Configuration Manager).

**Revisar la replicación de datos y archivos entre sitios:**   
Asegúrese de que la replicación de archivos y base de datos entre sitios funciona y está actualizada. Los retrasos o los trabajos pendientes pueden impedir una actualización correcta o sin problemas.\
Para la replicación de base de datos, puede utilizar Replication Link Analyzer para ayudar a resolver problemas antes de iniciar la actualización.

Para obtener más información, consulte [Acerca de Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) en el tema [Supervisar la infraestructura de la jerarquía y replicación de System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure).

**Instalar todas las actualizaciones críticas aplicables para los sistemas operativos en equipos que hospedan el sitio, el servidor de base de datos del sitio y los roles del sistema de sitio remoto:** antes de instalar una actualización para Configuration Manager, instale todas las actualizaciones críticas para cada sistema de sitio aplicable. Si alguna de las actualizaciones que instala requiere un reinicio, reinicie los equipos correspondientes antes de iniciar la actualización de Configuration Manager.

**Deshabilitar las réplicas de la base de datos para los puntos de administración en los sitios primarios:**   
Configuration Manager no puede actualizar correctamente un sitio primario que tiene habilitada una réplica de base de datos para puntos de administración. Deshabilite la replicación de base de datos antes de:

-   Crear una copia de seguridad de la base de datos del sitio para probar la actualización de la base de datos.
-   Instalar una actualización para Configuration Manager

Para obtener más información, consulte [Réplicas de bases de datos para puntos de administración de System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Establecer los grupos de disponibilidad AlwaysOn de SQL Server en la conmutación por error manual:**   
Antes de instalar las actualizaciones, como la versión 1610, asegúrese de que el grupo de disponibilidad está establecido para la conmutación por error manual. Después de que se actualice el sitio, puede restaurar la conmutación por error a automática. Para más información, vea [SQL Server AlwaysOn para una base de datos de sitio](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

**Volver a configurar los puntos de actualización de software que usan NLB:**   
Configuration Manager no puede actualizar un sitio que usa un clúster de equilibrio de carga de red (NLB) para hospedar puntos de actualización de software.

Si utiliza clústeres NLB para puntos de actualización de software, use PowerShell para quitar el clúster NLB.
Para obtener más información, consulte [Planear las actualizaciones de software en System Center Configuration Manager](/sccm/sum/plan-design/plan-for-software-updates).

**Deshabilitar todas las tareas de mantenimiento del sitio en cada sitio mientras dure la instalación de la actualización en ese sitio:**   
Antes de instalar la actualización, deshabilite cualquier tarea de mantenimiento del sitio que pueda estar en ejecución mientras el proceso de actualización está activo. Esto incluye, entre otras cosas, lo siguiente:

-   Copia de seguridad del servidor del sitio
-   Eliminar operaciones cliente antiguas
-   Eliminar datos de detección antiguos

Cuando se ejecuta una tarea de mantenimiento de la base de datos de sitio durante la instalación de la actualización, se puede producir un error en la instalación de la actualización. Antes de deshabilitar una tarea, programe la tarea de forma que pueda restaurar su configuración después de que se haya instalado la actualización.

Para obtener más información, consulte [Tareas de mantenimiento para System Center Configuration Manager](/sccm/core/servers/manage/maintenance-tasks) y [Referencia de tareas de mantenimiento para System Center Configuration Manager](/sccm/core/servers/manage/reference-for-maintenance-tasks).

**Crear una copia de seguridad de la base de datos del sitio en el sitio de administración central y en los sitios primarios:** antes de actualizar un sitio, realice una copia de seguridad del sitio para asegurarse de que tiene una copia de seguridad correcta para utilizarla en la recuperación ante desastres.

Para obtener más información, consulte [Copia de seguridad y recuperación de System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

**Probar la actualización de la base de datos en una copia de la última copia de seguridad de la base de datos del sitio:** antes de actualizar un sitio primario o un sitio de administración central de System Center Configuration Manager, pruebe el proceso de actualización de la base de datos del sitio en una copia de la base de datos del sitio.

-   Debe probar el proceso de actualización de base de datos del sitio porque, al actualizar un sitio, la base de datos del sitio podría modificarse.
-   Aunque una actualización de base de datos de prueba no es necesaria, puede identificar problemas de la actualización antes de que la base de datos de producción se vea afectada.
-   Una actualización incorrecta de la base de datos del sitio podría inutilizar la base de datos del sitio, en cuyo caso podría ser necesaria una recuperación del sitio para restaurar la funcionalidad.
-   Aunque se trate de una base de datos de sitio compartida entre varios sitios de una jerarquía, planee la prueba de la base de datos en cada uno de los sitios correspondientes antes de actualizar el sitio.
-   Si usa réplicas de base de datos para puntos de administración en un sitio primario, deshabilite la replicación antes de crear la copia de seguridad de la base de datos del sitio.

Configuration Manager no admite la realización de copias de seguridad de sitios secundarios ni la actualización de prueba de una base de datos de un sitio secundario.

No se puede ejecutar una actualización de prueba de base de datos en la base de datos del sitio de producción. Esta acción actualiza la base de datos del sitio y podría inutilizar el sitio. Para más información, vea la sección [Test the site database upgrade (Probar la actualización de la base de datos del sitio)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#bkmk_test) de [Upgrade to System Center Configuration Manager (Actualizar a System Center Configuration Manager)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).

**Plan piloto de cliente:**   
Cuando instale una actualización que actualiza el cliente, puede probar esa nueva actualización de cliente en preproducción antes de que implemente y actualice todos los clientes activos.

Para aprovechar las ventajas de esta opción, antes de comenzar la instalación de la actualización, debe configurar el sitio para admitir las actualizaciones automáticas de preproducción.

Para obtener más información, vea [Actualizar clientes en System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) y [Cómo probar las actualizaciones de cliente en una recopilación de preproducción en System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Planear usar períodos para tareas administrativas para controlar el momento en que los servidores de sitio instalan actualizaciones:**   
Puede usar períodos para tareas administrativas para definir un período aplicable a un servidor de sitio primario durante el cual se pueden instalar las actualizaciones para ese sitio.

Esto puede ayudarle a controlar el momento en que los sitios de la jerarquía instalan la actualización. Antes de la versión 1606, los períodos para tareas administrativas se denominaban ventanas de mantenimiento. Para más información, vea [Ventanas de servicio para servidores de sitio](/sccm/core/servers/manage/service-windows).

**Ejecutar el Comprobador de requisitos previos del programa de instalación:**   
Cuando la actualización aparece en la consola como **Disponible**, puede ejecutar de manera independiente el Comprobador de requisitos previos antes de instalar la actualización. (Al instalar la actualización en el sitio, el Comprobador de requisitos previos vuelve a ejecutarse).

Para ejecutar una comprobación de requisitos previos desde la consola, vaya a **Administración > Información general > Cloud Services > Actualizaciones y mantenimiento**, haga clic con el botón derecho en **Paquete de actualizaciones 1610 de Configuration Manager** y seleccione **Run prerequisite check (Ejecutar comprobación de requisitos previos)**.

Para obtener más información sobre iniciar y, después, supervisar la comprobación de requisitos previos, consulte **Paso 3: Ejecutar el Comprobador de requisitos previos antes de instalar una actualización** en el tema [Instalación de actualizaciones en la consola para System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

> [!IMPORTANT]  
> Cuando se ejecuta el Comprobador de requisitos previos como parte de la instalación de una actualización o de forma independiente, el proceso actualiza algunos archivos de origen del producto que se utilizan para tareas de mantenimiento del sitio. Por lo tanto, después de ejecutar el Comprobador de requisitos previos pero antes de instalar la actualización 1610, si tiene que realizar una tarea de mantenimiento del sitio, ejecute **Setupwpf.exe** (programa de instalación de Configuration Manager) desde la carpeta CD.Latest en el servidor de sitio.

**Actualizar sitios:**   
Ya está listo para iniciar la instalación de la actualización de la jerarquía. Para obtener más información sobre la instalación de la actualización, consulte [Install in-console updates (Instalación de actualizaciones en la consola)](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

Se recomienda planear la instalación de la actualización fuera del horario comercial habitual para cada sitio, ya que será el momento en que el proceso de instalación de la actualización y sus acciones para volver a instalar los componentes del sitio y los roles de sistema de sitio afectarán menos a las operaciones comerciales. Para más información, vea [Updates for System Center Configuration Manager (Actualizaciones para System Center Configuration Manager)](/sccm/core/servers/manage/updates).



<!--HONumber=Jan17_HO2-->


