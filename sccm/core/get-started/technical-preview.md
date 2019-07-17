---
title: Versiones de Technical Preview
titleSuffix: Configuration Manager
description: Obtenga información sobre la rama de Technical Preview para probar nuevas funcionalidades y funcionalidades de Configuration Manager.
ms.date: 07/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3cb49531bd6d10106b17cca65218d7158c24dc3e
ms.sourcegitcommit: 5a36200c738f20a78299a30723c8e613af71efce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843863"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview para Configuration Manager

*Se aplica a: System Center Configuration Manager (Technical Preview)*

Este artículo proporciona detalles sobre de la rama de Technical Preview mensual de Configuration Manager. Technical Preview presenta una funcionalidad nueva en que está trabajando Microsoft. Presenta características nuevas que no están todavía incluida en la rama actual de Configuration Manager. Estas características podrían incluirse finalmente en una actualización de la rama actual. Antes de finalizar la las características, queremos que las pruebe y nos comparta sus comentarios.  

Como esta es una versión preliminar técnica, los detalles y las funcionalidades están sujetos a cambios.  

Esta información se aplica a todas las versiones de la rama de Technical Preview de Configuration Manager. En este artículo se enumera cada una de las características nuevas junto con la versión de Technical Preview en las que aparece por primera vez. Por ejemplo, la versión **1901** de enero (01) de 2019 (19). Los artículos independientes dedicados a cada versión preliminar detallan las características individuales.  

Para más información sobre las novedades de la *rama actual* de Configuration Manager, consulte [Novedades de las versiones incrementales de Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).

> [!Tip]  
> Para obtener una notificación cuando se actualice esta página, copie y pegue la siguiente dirección URL en su lector de fuentes RSS: `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="bkmk_reqs"></a> Limitaciones y requisitos  

> [!IMPORTANT]  
> La versión preliminar técnica solo tiene licencia para su uso en un entorno de laboratorio. Es posible que Microsoft no proporcione servicios de soporte técnico y que algunas características no estén disponibles en las versiones preliminares técnicas. Además, es posible que el software de versión preliminar técnica tenga estándares de seguridad, privacidad, accesibilidad, disponibilidad y confiabilidad reducidos o diferentes a los del software proporcionado comercialmente.  

Para la mayoría de requisitos previos de producto, use la información que se encuentra en las [configuraciones admitidas](/sccm/core/plan-design/configs/supported-configurations). Las excepciones siguientes se aplican a la rama de Technical Preview:  

- Cada instalación permanece activa durante 90 días y luego cambia a inactiva.  

- El único idioma admitido es el inglés.  

- Solo admite los parámetros de línea de comandos de configuración siguientes:  

    - `/silent`  
    - `/testdbupgrade`  

- El punto de conexión del servicio se instala en el modo en línea. No admite el modo sin conexión.  

- En los artículos independientes de cada versión específica de Technical Preview se incluyen limitaciones o requisitos adicionales, según corresponda.

- Las características siguientes no son compatibles con la rama de Technical Preview:  

    - [Migración](/sccm/core/migration/migrate-data-between-hierarchies) desde o hasta esta rama de versión preliminar.  

    - [Actualización](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) a esta rama de versión preliminar.  

    - [Recuperación del sitio](/sccm/core/servers/manage/recover-sites) desde la carpeta cd.latest.  <!--507106-->

- No se admite la actualización de esta rama de versión preliminar a la rama actual.  

    > [!Note]  
    > Cuando haya actualizaciones disponibles para una versión preliminar, seguirá siendo posible buscarlas e instalarlas desde el nodo **Actualizaciones y mantenimiento** de la consola de Configuration Manager. Para ver un vídeo del proceso de actualización en la consola, vea [Installing Configuration Manager update packages](https://www.youtube.com/embed/KBd_EGFbUT8) (Instalación de las actualizaciones de Configuration Manager) en youtube.com.  

- Solo admite un sitio primario independiente. No se admiten sitios de administración central, varios sitios primarios ni sitios secundarios.  

La rama de Technical Preview de Configuration Manager admite los productos y las tecnologías siguientes:

- Solo es compatible con las versiones siguientes de **SQL Server**:  

    - SQL Server 2017 (con la actualización acumulativa 2 o posterior)
    - SQL Server 2016 (sin ningún Service Pack)
    - SQL Server 2014 (con Service Pack 1, o versiones posteriores)
    - SQL Server 2012 (con Service Pack 3, o versiones posteriores)  

- El sitio admite hasta 10 clientes, que deben ejecutar una de las siguientes versiones de Windows:  

    - Windows 10  
    - Windows 8.1  
    - Windows 7  

> [!Note]  
> La inclusión de estos productos en este contenido no implica una extensión de la compatibilidad con una versión que están fuera de su ciclo de vida de soporte. Configuration Manager no es compatible con los productos que están fuera de su ciclo de vida de soporte. Para más información, consulte [Directiva de ciclo de vida de Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270).  

## <a name="bkmk_install"></a> Instalación y actualización  

La rama de Technical Preview de Configuration Manager para su uso en laboratorio es distinta de la rama actual de Configuration Manager para su uso en producción.  

En primer lugar, instale una versión de base de referencia de la rama de Technical Preview. Después de instalar una versión de referencia, use las actualizaciones en consola para que la instalación cuente con la versión preliminar más reciente. Normalmente, las nuevas versiones de Technical Preview están disponibles cada mes.

Microsoft admite cada versión de Technical Preview hasta que hay disponibles tres versiones sucesivas. Por ejemplo, cuando se publica la versión 1708, se deja de admitir la versión 1704. Las versiones 1705, 1706 y 1707 siguen siendo compatibles. Cuando una base de referencia deja de ser compatible, todavía se admite para instalar un nuevo sitio de Technical Preview, suponiendo que se actualiza inmediatamente a una versión compatible. La base de referencia anterior se admite hasta que haya disponible una versión de base de referencia nueva. Actualice a la versión disponible más reciente desde la base de referencia y repita el proceso de actualización hasta instalar la versión de Technical Preview más reciente.

> [!TIP]  
> Cuando se instala una actualización de versión preliminar técnica, la instalación de versión preliminar se actualiza a la nueva versión preliminar técnica. Una instalación de Technical Preview nunca tiene la opción de actualizar a una instalación de rama actual. Tampoco recibe nunca actualizaciones desde la versión de rama actual.
>
> Varias veces a lo largo del año, hay versiones de rama de Technical Preview y versiones de rama actuales con el mismo número de versión. Por ejemplo, hay una versión 1802 de Technical Preview y una versión 1802 de rama actual.

### <a name="active-baseline-versions"></a>Versiones de base de referencia activas

Instale una versión de base de referencia hasta un año después de su lanzamiento. Cuando instale un sitio de Technical Preview nuevo, use la versión de base de referencia más reciente si hay más de una versión de base de referencia disponible actualmente.

- **Versión 1907 de Technical Preview**: La versión 1907 de Technical Preview de Configuration Manager está disponible como actualización en consola y como versión de base de referencia nueva. Descargue las versiones de base de referencia [del centro de evaluación de TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


## <a name="BKMK_TPFeedback"></a> Proporcionar comentarios  

Nos encanta recibir sus comentarios sobre las características nuevas en Technical Preview. Para obtener más información, vea [Comentarios sobre el producto](/sccm/core/understand/find-help#product-feedback).

También puede hablarnos sobre las ideas que tenga sobre características nuevas que le gustaría ver. Para enviar nuevas ideas y votar sobre las ideas enviadas por otros usuarios, [visite nuestra página de UserVoice](https://configurationmanager.uservoice.com).  


<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->


## <a name="bkmk_tpCaps"></a> Características de la versión más reciente  

Las características siguientes están disponibles con la versión de Technical Preview de Configuration Manager más reciente:

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1907"></a>Versión 1907 de Technical Preview

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor) <!--ID-->

- [Búsqueda en el editor de secuencias de tareas](/sccm/core/get-started/2019/technical-preview-1907#bkmk_tsedit) <!--4621085-->
- [Mejoras en el panel de Upgrade Readiness para Office 365 ProPlus](/sccm/core/get-started/2019/technical-preview-1907#improvements-to-office-365-proplus-upgrade-readiness-dashboard) <!--4021125-->

> [!Note]  
> Las características que estaban disponibles en una versión anterior de Technical Preview siguen estando disponibles en versiones posteriores. Del mismo modo, las características que se agregan a la rama actual de Configuration Manager siguen estando disponibles en la rama de Technical Preview.  


## <a name="features-in-recent-technical-previews"></a>Características en versiones recientes de Technical Preview

Las características siguientes se publicaron con versiones anteriores de la rama Technical Preview de Configuration Manager desde la publicación de la última versión de la rama actual:

> [!Tip]  
> Cuando esté disponible una nueva versión de la rama actual, se mostrarán las características que disponibles en esa versión en el último artículo sobre las *novedades*. Para obtener más información, vea [Novedades en las versiones incrementales](/sccm/core/plan-design/changes/whats-new-incremental-versions#supported-versions).

<!-- This is the full list of new features in the past TP releases since the last CB release. 
Each month, add features from the list above to a new H3 section at the top of this section. 
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

### <a name="technical-preview-version-1906"></a>Versión 1906 de Technical Preview

- [Mejoras en las tareas de mantenimiento](/sccm/core/get-started/2019/technical-preview-1906#improvements-to-maintenance-tasks) <!--3555894-->
- [Supervisión de la actualización de base de datos de actualización de Configuration Manager](/sccm/core/get-started/2019/technical-preview-1906#configuration-manager-update-database-upgrade-monitoring) <!--4200581-->
- [Varios grupos piloto para las cargas de trabajo de administración conjunta](/sccm/core/get-started/2019/technical-preview-1906#bkmk_comgmt_pilot) <!--3555750-->
- [Lógica de notificación rediseñada para el nuevo software disponible](/sccm/core/get-started/2019/technical-preview-1906#redesigned-notification-logic-for-newly-available-software) <!--3555904-->
- [RBAC en carpetas](/sccm/core/get-started/2019/technical-preview-1906#rbac-on-folders) <!--3600867-->
- [Detección de grupos de usuarios de Azure Active Directory](/sccm/core/get-started/2019/technical-preview-1906#bkmk_aad-disco) <!--3611956-->
- [Control remoto en cualquier lugar mediante Cloud Management Gateway](/sccm/core/get-started/2019/technical-preview-1906#remote-control-anywhere-using-cloud-management-gateway) <!--4575930-->
- [Mejoras en el Centro de comunidad](/sccm/core/get-started/2019/technical-preview-1906#bkmk_hub) <!--3555935-->
- [Adición de combinaciones, operadores adicionales y agregadores en CMPivot](/sccm/core/get-started/2019/technical-preview-1906#bkmk_cmpivot) <!--4054074-->
- [Mejoras en CMPivot](/sccm/core/get-started/2019/technical-preview-1906#improvements-to-cmpivot) <!--4619340,4683130-->
- [Mejoras en la consola de Configuration Manager](/sccm/core/get-started/2019/technical-preview-1906#bkmk_console) <!--4223683-->
- [Soporte técnico para Windows Virtual Desktop](/sccm/core/get-started/2019/technical-preview-1906#bkmk_winsku) <!--3556025-->
- [Notificaciones de cuenta regresiva más frecuentes para reinicios](/sccm/core/get-started/2019/technical-preview-1906#more-frequent-countdown-notifications-for-restarts) <!--3976435-->
- [Administración conjunta de la inscripción automática mediante el token del dispositivo](/sccm/core/get-started/2019/technical-preview-1906#bkmk_comgmt) <!--4454491-->
- [Opciones adicionales para los catálogos de actualizaciones de terceros](/sccm/core/get-started/2019/technical-preview-1906#additional-options-for-third-party-update-catalogs) <!--4469002-->
- [Limpieza del contenido de la aplicación de la caché de cliente durante la secuencia de tareas](/sccm/core/get-started/2019/technical-preview-1906#bkmk_tscache) <!--4485675-->
- [Nueva categoría de producto Windows 10, versión 1903 y posteriores](/sccm/core/get-started/2019/technical-preview-1906#new-windows-10-version-1903-and-later-product-category) <!--4682946-->
- [Regla de información de administración para la reserva de NTLM](/sccm/core/get-started/2019/technical-preview-1906#bkmk_ntlm) <!--4572953-->
- [Filtrado de aplicaciones implementadas en dispositivos](/sccm/core/get-started/2019/technical-preview-1906#bkmk_appcategory) <!--4451056-->
- [Mejoras de la implementación del sistema operativo](/sccm/core/get-started/2019/technical-preview-1906#bkmk_osd) <!--4668846, 2840337, 4512937-->
- [Vínculo directo a pestañas personalizadas en el Centro de software](/sccm/core/get-started/2019/technical-preview-1906#bkmk_swctr) <!--4655176-->

### <a name="technical-preview-version-1905"></a>Versión 1905 de Technical Preview

- [Control mejorado del mantenimiento de WSUS](/sccm/core/get-started/2019/technical-preview-1905#improved-control-over-wsus-maintenance) <!--4110109-->
- [Mejoras en la consola de Configuration Manager](/sccm/core/get-started/2019/technical-preview-1905#bkmk_console) <!--4616810-->
- [Configuración del tiempo de ejecución máximo predeterminado para las actualizaciones de software](/sccm/core/get-started/2019/technical-preview-1905#bkmk_timeout) <!--3734426-->
- [Criterios de confianza de archivos de Protección de aplicaciones de Windows Defender](/sccm/core/get-started/2019/technical-preview-1905#bkmk_wdag) <!--3555858-->
- [Grupos de aplicaciones](/sccm/core/get-started/2019/technical-preview-1905#bkmk_app-group) <!--3555907-->
- [Secuencia de tareas como un tipo de implementación de modelo de aplicación](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdt) <!--3555953-->
- [Administración de BitLocker](/sccm/core/get-started/2019/technical-preview-1905#bkmk_bitlocker) <!--3601034-->
- [Depurador de secuencia de tareas](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdebug) <!--3612274-->
- [Optimización de distribución en el panel de orígenes de datos de cliente](/sccm/core/get-started/2019/technical-preview-1905#bkmk_do) <!--3555759-->
- [Mejoras en el Centro de comunidad](/sccm/core/get-started/2019/technical-preview-1905#bkmk_hub) <!--4224401-->
- [Vista de la GUID de SMBIOS en listas de dispositivos](/sccm/core/get-started/2019/technical-preview-1905#bkmk_smbios) <!--4526580-->
- [Visor de registros OneTrace](/sccm/core/get-started/2019/technical-preview-1905#bkmk_onetrace) <!--3555962-->
- [Mejoras de la infraestructura del Centro de software](/sccm/core/get-started/2019/technical-preview-1905#bkmk_swctr) <!--3555950-->
- [Mejoras en las personalizaciones de la pestaña Centro de software](/sccm/core/get-started/2019/technical-preview-1905#improvements-to-software-center-tab-customizations) <!--4063773-->
- [Mejoras en las aprobaciones de aplicaciones](/sccm/core/get-started/2019/technical-preview-1905#bkmk_approve) <!--4224910-->
- [Reintento de la instalación de aplicaciones aprobadas previamente](/sccm/core/get-started/2019/technical-preview-1905#bkmk_retry) <!--4336307-->
- [Instalación de aplicaciones para un dispositivo](/sccm/core/get-started/2019/technical-preview-1905#bkmk_device-app) <!--4402180-->
- [Notificaciones de cuenta regresiva más frecuentes para reinicios](/sccm/core/get-started/2019/technical-preview-1905#bkmk_restart) <!--3976435-->
- [Sincronización de los resultados de pertenencia a recopilaciones con grupos de Azure Active Directory](/sccm/core/get-started/2019/technical-preview-1905#bkmk_aadcollsync) <!--3607475-->
- [Configuración del período de retención mínimo de caché de cliente](/sccm/core/get-started/2019/technical-preview-1905#bkmk_cache) <!--4485509-->
- [Mejoras de la implementación del sistema operativo](/sccm/core/get-started/2019/technical-preview-1905#bkmk_osd) <!--4512937,4224642-->
- [Adición de un nodo Always On de SQL](/sccm/core/get-started/2019/technical-preview-1905#bkmk_sqlao) <!--3127336-->

### <a name="technical-preview-version-1904"></a>Versión 1904 de la versión preliminar técnica

- [Panel de Upgrade Readiness para Office 365 ProPlus](/sccm/core/get-started/2019/technical-preview-1904#bkmk_o365) <!--4021125-->  
- [Configurar la actualización dinámica durante las actualizaciones de características](/sccm/core/get-started/2019/technical-preview-1904#configure-dynamic-update-during-feature-updates) <!--4062619-->  
- [GitHub y Centro de comunidad](/sccm/core/get-started/2019/technical-preview-1904#community-hub-and-github) <!--3555935,3555936-->  
- [CMPivot independiente](/sccm/core/get-started/2019/technical-preview-1904#bkmk_cmpivot) <!--3555890-->  
- [Mejoras de la infraestructura del Centro de software](/sccm/core/get-started/2019/technical-preview-1904#bkmk_swctr) <!--3555950-->  
- [Control mejorado del mantenimiento de WSUS](/sccm/core/get-started/2019/technical-preview-1904#improved-control-over-wsus-maintenance) <!--4110109-->  
- [Imágenes de sistema operativo y paquetes de controladores de caché previa](/sccm/core/get-started/2019/technical-preview-1904#bkmk_precache) <!--4224642-->  
- [Mejoras de la implementación del sistema operativo](/sccm/core/get-started/2019/technical-preview-1904#bkmk_osd) <!--2839943,4447680-->  

### <a name="technical-preview-version-1903"></a>Versión 1903 de Technical Preview

- [Programa de estimación de costes de servicios en la nube](/sccm/core/get-started/2019/technical-preview-1903#bkmk_cmg) <!--3555774-->  
- [Uso del punto de distribución como servidor de caché local para la Optimización de distribución](/sccm/core/get-started/2019/technical-preview-1903#bkmk_doinc) <!--3555764-->  
- [Reclamación de bloqueo para editar secuencias de tareas](/sccm/core/get-started/2019/technical-preview-1903#bkmk_sedo) <!--3699337-->  
- [Obtención de detalles de actualizaciones necesarias](/sccm/core/get-started/2019/technical-preview-1903#bkmk_req-updates) <!--4224414-->  
- [Mejoras en la creación de medios de secuencia de tareas](/sccm/core/get-started/2019/technical-preview-1903#bkmk_tsmedia) <!--4090666-->  


## <a name="features-in-previous-technical-previews"></a>Características de las versiones de Technical Preview anteriores

Las características siguientes se lanzaron con versiones anteriores de la rama de Technical Preview de Configuration Manager. Estas características siguen estando disponibles en versiones posteriores, pero todavía no están disponibles en la rama actual.

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Característica        | Versión de Technical Preview |  
|----------------|---------------------------|
| Descarga de informes desde el Centro de comunidad<!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Centro de comunidad <!--3556020, fka 1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| Servicio del respondedor PXE basado en cliente <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Compatibilidad con el arranque de red de PXE para IPv6 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Uso de Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Mejoras en Asset Intelligence <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |
| Los usuarios finales pueden instalar aplicaciones desde el Portal de empresa <!--3601249, fka 1037233--> | [Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End) |


## <a name="see-also"></a>Consulte también  

Vea los siguientes artículos para más información:  

- [Evaluar Configuration Manager en un laboratorio](/sccm/core/get-started/evaluate-with-lab-environment)
- [Novedades de las versiones incrementales de Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introducción a Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Para más información sobre las características de la rama actual que requieren consentimiento, consulte las [características de versión preliminar](/sccm/core/servers/manage/pre-release-features).  
>
> Para más información sobre las características de la rama actual que se deben habilitar primero, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
