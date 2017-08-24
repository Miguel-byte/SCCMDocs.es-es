---
title: "Lista de comprobación para la versión 1610 | System Center Configuration Manager"
description: "Obtenga información sobre las acciones que se deben realizar antes de actualizar a la versión 1610 de System Center Configuration Manager."
ms.custom: na
ms.date: 6/6/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
caps.latest.revision: "7"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 54b243fd33ed13b8ccde48fa5e2525204455d96c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="checklist-for-installing-update-1610-for-system-center-configuration-manager"></a>Lista de comprobación para la instalación de la actualización 1610 de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Cuando usa la rama actual de System Center Configuration Manager, puede instalar la actualización en la consola para la versión 1610 para actualizar su jerarquía desde la versión 1606. Si su jerarquía ejecuta la versión 1511, 1602 o 1606, puede actualizar a la versión 1610.

Para obtener la actualización de la versión 1610, debe usar un rol de sistema de sitio de punto de conexión del servicio en el sitio de nivel superior de su jerarquía. Esto puede realizarse en el modo en línea o sin conexión. Después de que su jerarquía descargue el paquete de actualización de Microsoft, lo podrá encontrar en la consola, en **Administración &gt; Información general &gt; Cloud Services &gt; Actualizaciones y mantenimiento**.

-   Cuando la actualización aparezca como **Disponible**, ya está lista para instalarse. Antes de instalar la versión 1610, revise la siguiente información [sobre la instalación de la actualización 1610](#about-installing-update-1610) y la [lista de comprobación](#checklist) de las configuraciones que deben realizarse antes de iniciar la actualización.

-   Si la actualización se muestra como **Descargando** y no cambia, revise los archivos **hman.log** y **dmpdownloader.log** para ver los errores.

    -   Normalmente, también puede reiniciar el servicio **SMS_Executive** en el servidor de sitio para reiniciar la descarga de los archivos de redistribución de la actualización.

    -   Otro problema común de descarga se produce cuando la configuración del servidor proxy impide las descargas desde <http://silverlight.dlservice.microsoft.com> y <http://download.microsoft.com>.

Para obtener más información sobre la instalación de actualizaciones, consulte [Actualizaciones y servicio en la consola](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Para obtener más información sobre las versiones de la rama actual, consulte [Versiones de línea de base y versiones de actualización](/sccm/core/servers/manage/updates#bkmk_Baselines) en [Actualizaciones para System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="about-installing-update-1610"></a>Sobre la instalación de la actualización 1610

**Sitios:**  
La actualización 1610 solo puede instalarse en el sitio de nivel superior de la jerarquía. Esto significa que, si existe, la instalación se inicia desde el sitio de administración central, o bien desde el sitio principal independiente. Después de instalar la actualización en el sitio de nivel superior, los sitios secundarios tienen el siguiente comportamiento de actualización:

-   Los sitios primarios secundarios inician la instalación de la actualización automáticamente después de que el sitio de administración central haya terminado de instalarla. Puede usar períodos para tareas administrativas para controlar el momento en que un sitio instala actualizaciones. Antes de la versión 1606, los períodos para tareas administrativas se denominaban ventanas de mantenimiento. Para más información, vea [Ventanas de servicio para servidores de sitio](/sccm/core/servers/manage/service-windows).

-   Una vez que el sitio principal primario termine de instalar la actualización, tendrá que actualizar manualmente los sitios secundarios desde la consola de Configuration Manager. No se admite la actualización automática de los servidores de sitio secundario.

**Roles de sistema de sitio:**  
Cuando el servidor de sitio instala la actualización, los roles de sistema de sitio instalados en el servidor de sitio y aquellos instalados en los equipos remotos se actualizan automáticamente. Por tanto, antes de instalar la actualización, asegúrese de que cada servidor de sistema de sitio cumpla los requisitos previos nuevos de funcionamiento con la nueva versión de la actualización.

**Consolas de Configuration Manager:**   
La primera vez que use una consola de Configuration Manager una vez que la actualización haya terminado, se le pedirá que actualice esa consola. Para ello, debe ejecutar el programa de instalación de Configuration Manager en el equipo que hospeda la consola y, luego, seleccionar la opción para actualizarla. Se recomienda no retrasar la instalación de la actualización de la consola.



## <a name="checklist"></a>Lista de comprobación

**Asegurarse de que todos los sitios ejecuten una versión compatible de System Center Configuration Manager:** antes de iniciar la instalación de la actualización 1610, cada sitio de la jerarquía debe tener la misma versión de System Center Configuration Manager, ya sea la 1511, la 1602 o la 1606.

**Revisar el estado de Software Assurance o de los derechos de suscripción equivalentes:**   
Debe tener un contrato de Software Assurance (SA) activo para instalar la actualización 1610. Cuando instale la versión 1610, tendrá la opción en la pestaña **Licencias** para confirmar la **fecha de vencimiento de Software Assurance**.

Este es un valor opcional que puede especificar como recordatorio útil de la fecha de expiración de su licencia, que está visible al instalar futuras actualizaciones. Si ha instalado Configuration Manager desde los medios de línea base de la versión 1606, puede que haya especificado este valor anteriormente durante la configuración, o en la pestaña **Concesión de licencias** de la **Configuración de jerarquía** tras la instalación del sitio.

Para obtener más información, consulte [Licencias y ramas para System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

**Revisar las versiones instaladas de Microsoft.NET en los servidores de sistema de sitio:** cuando un sitio instala la actualización 1610, si todavía no está instalado .NET Framework 4.5 o una versión posterior, Configuration Manager instala .NET Framework 4.5.2 automáticamente en cada equipo que hospede alguno de los siguientes roles de sistema de sitio:

-   Punto de proxy de inscripción
-   Punto de inscripción
-   Punto de administración
-   Punto de conexión de servicio

Esta instalación puede poner el servidor de sistema de sitio en un estado pendiente de reinicio y notificar los errores al visor de estado de los componentes de Configuration Manager. Además, las aplicaciones .NET del servidor pueden experimentar errores aleatorios hasta que se reinicie el servidor.

Para obtener más información, consulte [Site and site system prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) (Requisitos previos de sitio y sistema de sitio).

**Revisar el estado del sitio y la jerarquía, y comprobar que no hay problemas sin resolver:** antes de actualizar un sitio, resuelva todos los problemas de funcionamiento para el servidor de sitio, el servidor de base de datos del sitio y los roles de sistema de sitio instalados en equipos remotos. Una actualización del sitio puede generar errores debido a problemas de funcionamiento existentes.

Para obtener más información, consulte [Use alerts and the status system for System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system) (Usar alertas y el sistema de estado para System Center Configuration Manager).

**Revisar la replicación de datos y archivos entre sitios:**   
Asegúrese de que la replicación de archivos y base de datos entre sitios funciona y está actualizada. Los retrasos o los trabajos pendientes pueden impedir una actualización correcta y sin problemas.
Para la replicación de base de datos, puede utilizar Replication Link Analyzer para ayudar a resolver problemas antes de iniciar la actualización.

Para obtener más información, consulte [Acerca de Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) en el tema [Supervisar la infraestructura de la jerarquía y replicación de System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure).

**Instalar todas las actualizaciones críticas aplicables para los sistemas operativos en equipos que hospedan el sitio, el servidor de base de datos del sitio y los roles del sistema de sitio remoto:** antes de instalar una actualización para Configuration Manager, instale todas las actualizaciones críticas para cada sistema de sitio aplicable. Si alguna de las actualizaciones que instala requiere un reinicio, reinicie los equipos correspondientes antes de iniciar la actualización de Configuration Manager.

**Deshabilitar las réplicas de la base de datos para los puntos de administración en los sitios primarios:**   
Configuration Manager no puede actualizar correctamente un sitio primario que tiene habilitada una réplica de base de datos para puntos de administración. Deshabilite la replicación de base de datos antes de instalar una actualización de Configuration Manager.

Para obtener más información, consulte [Réplicas de bases de datos para puntos de administración de System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Establecer los grupos de disponibilidad AlwaysOn de SQL Server en la conmutación por error manual:**   
Antes de instalar las actualizaciones, como la versión 1610, asegúrese de que el grupo de disponibilidad esté establecido para la conmutación por error manual. Después de actualizar el sitio, puede restaurar la conmutación por error a automática. Para obtener más información, consulte [SQL Server AlwaysOn para una base de datos de sitio](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

**Volver a configurar los puntos de actualización de software que usan NLB:**   
Configuration Manager no puede actualizar un sitio que usa un clúster de equilibrio de carga de red (NLB) para hospedar puntos de actualización de software.

Si utiliza clústeres NLB para puntos de actualización de software, use Windows PowerShell para quitar el clúster NLB.
Para obtener más información, consulte [Planear las actualizaciones de software en System Center Configuration Manager](/sccm/sum/plan-design/plan-for-software-updates).

**Deshabilitar todas las tareas de mantenimiento del sitio en cada sitio mientras dure la instalación de la actualización en ese sitio:**   
Antes de instalar la actualización, deshabilite cualquier tarea de mantenimiento del sitio que pueda estar en ejecución mientras el proceso de actualización esté activo. Esto incluye, entre otras cosas, lo siguiente:

-   Copia de seguridad del servidor del sitio
-   Eliminar operaciones cliente antiguas
-   Eliminar datos de detección antiguos

Cuando se ejecuta una tarea de mantenimiento de la base de datos de sitio durante la instalación de la actualización, se puede producir un error en la instalación de la actualización. Antes de deshabilitar una tarea, programe la tarea de forma que pueda restaurar su configuración después de instalar la actualización.

Para obtener más información, consulte [Tareas de mantenimiento para System Center Configuration Manager](/sccm/core/servers/manage/maintenance-tasks) y [Referencia de tareas de mantenimiento para System Center Configuration Manager](/sccm/core/servers/manage/reference-for-maintenance-tasks).

**Crear una copia de seguridad de la base de datos del sitio en el sitio de administración central y en los sitios primarios:** antes de actualizar un sitio, realice una copia de seguridad del sitio para asegurarse de que tiene una copia de seguridad correcta para utilizarla en la recuperación ante desastres.

Para obtener más información, consulte [Copia de seguridad y recuperación de System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** 
Before you update a System Center Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.

-   We recommend that you test the site database upgrade process because when you upgrade a site, the site database might be modified.

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, see [Step 2: Test the database upgrade before installing an update](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) from **Before you install an in-console update**.
-->

**Plan piloto de cliente:**   
Al instalar una actualización que actualiza el cliente, puede probar esa nueva actualización de cliente en preproducción antes de implementar y actualizar todos los clientes activos.

Para aprovechar las ventajas de esta opción, debe configurar el sitio para que admita las actualizaciones automáticas de preproducción antes de comenzar la instalación de la actualización.

Para obtener más información, vea [Actualizar clientes en System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) y [Cómo probar las actualizaciones de cliente en una recopilación de preproducción en System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Planear usar períodos para tareas administrativas para controlar el momento en que los servidores de sitio instalan actualizaciones:**   
Puede usar períodos para tareas administrativas para definir un período durante el cual se pueden instalar las actualizaciones de un servidor de sitio.

Esto puede ayudarle a controlar el momento en que los sitios de la jerarquía instalan la actualización. Antes de la versión 1606, los períodos para tareas administrativas se denominaban ventanas de mantenimiento. Para más información, vea [Ventanas de servicio para servidores de sitio](/sccm/core/servers/manage/service-windows).

**Ejecutar el Comprobador de requisitos previos del programa de instalación:**   
Cuando la actualización aparece en la consola como **Disponible**, puede ejecutar de manera independiente el Comprobador de requisitos previos antes de instalar la actualización. (Al instalar la actualización en el sitio, el Comprobador de requisitos previos vuelve a ejecutarse).

Para ejecutar una comprobación de requisitos previos desde la consola, vaya a **Administración > Información general > Cloud Services > Actualizaciones y mantenimiento**. Luego, haga clic con el botón derecho en **Paquete de actualización 1610 de Configuration Manager** y, a continuación, elija **Ejecutar comprobación de requisitos previos**.

Para obtener más información sobre iniciar y, después, supervisar la comprobación de requisitos previos, consulte **Paso 3: Ejecutar el Comprobador de requisitos previos antes de instalar una actualización** en el tema [Instalación de actualizaciones en la consola para System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

> [!IMPORTANT]  
> Cuando se ejecuta el Comprobador de requisitos previos de forma independiente o como parte de la instalación de una actualización, el proceso actualiza algunos archivos de origen del producto que se utilizan para tareas de mantenimiento del sitio. Por lo tanto, después de ejecutar el Comprobador de requisitos previos, pero antes de instalar la actualización 1610, si necesita realizar una tarea de mantenimiento del sitio, ejecute **Setupwpf.exe** (programa de instalación de Configuration Manager) desde la carpeta CD.Latest en el servidor de sitio.

**Actualizar sitios:**   
Ya está listo para iniciar la instalación de la actualización de la jerarquía. Para obtener más información sobre la instalación de la actualización, consulte [Instalación de actualizaciones en la consola](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

Se recomienda planear la instalación de la actualización fuera del horario comercial habitual de cada sitio, ya que será el momento en que el proceso de instalación de la actualización y sus acciones para volver a instalar los componentes del sitio y los roles de sistema de sitio afectarán menos a las operaciones comerciales.

Para más información, vea [Updates for System Center Configuration Manager (Actualizaciones para System Center Configuration Manager)](/sccm/core/servers/manage/updates).
