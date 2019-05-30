---
title: Versiones de Technical Preview
titleSuffix: Configuration Manager
description: Obtenga información sobre la rama de Technical Preview para probar nuevas funcionalidades y funcionalidades de Configuration Manager.
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6e4475e5db6562fc95d3fafc7c88805b2df53075
ms.sourcegitcommit: d1df13fc95a1f1540177c294555d9be26161b9cb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974129"
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
> La versión preliminar técnica solo tiene licencia para su uso en un entorno de laboratorio. Es posible que Microsoft no proporcione servicios de soporte técnico y que algunas características no estén disponibles en el software de versión preliminar. Además, es posible que el software de versión preliminar tenga estándares de seguridad, privacidad, accesibilidad, disponibilidad y confiabilidad reducidos o diferentes a los del software proporcionado comercialmente.  

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

- **Versión 1902.2 de Technical Preview**: La versión 1902.2 de Technical Preview de Configuration Manager está disponible como actualización en consola y como una versión de base de referencia nueva. Descargue las versiones de base de referencia [del centro de evaluación de TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="BKMK_TPFeedback"></a> Proporcionar comentarios  

Nos encanta recibir sus comentarios sobre las características nuevas en Technical Preview. Para obtener más información, vea [Comentarios sobre el producto](/sccm/core/understand/find-help#product-feedback).

También puede hablarnos sobre las ideas que tenga sobre características nuevas que le gustaría ver. Para enviar nuevas ideas y votar sobre las ideas enviadas por otros usuarios, [visite nuestra página de UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->

## <a name="bkmk_tpCaps"></a> Características de la versión más reciente  

Las características siguientes están disponibles con la versión de Technical Preview de Configuration Manager más reciente:

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1905"></a>Versión 1905 de Technical Preview

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor) <!--ID-->

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

> [!Note]  
> Las características que estaban disponibles en una versión anterior de Technical Preview siguen estando disponibles en versiones posteriores. Del mismo modo, las características que se agregan a la rama actual de Configuration Manager siguen estando disponibles en la rama de Technical Preview.  

## <a name="features-in-recent-supported-technical-previews"></a>Características en versiones Technical Preview compatibles recientes

Las características siguientes se lanzaron con versiones anteriores de la rama de Technical Preview de Configuration Manager que todavía se admiten:

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 | Característica | Versión de Technical Preview | Versión de rama actual |  
 |---------|---------------------------|------------------------|
 | Panel de Upgrade Readiness para Office 365 ProPlus <!--4021125--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_o365) | ![Sin agregar](media/Red_X.gif) |
 | Configurar la actualización dinámica durante las actualizaciones de características <!--4062619--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#configure-dynamic-update-during-feature-updates) | ![Sin agregar](media/Red_X.gif) |
 | GitHub y Centro de comunidad <!--3555935,3555936--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#community-hub-and-github) | ![Sin agregar](media/Red_X.gif) |
 | CMPivot independiente <!--3555890--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_cmpivot) | ![Sin agregar](media/Red_X.gif) |
 | Mejoras de la infraestructura del Centro de software <!--3555950--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_swctr) | ![Sin agregar](media/Red_X.gif) |
 | Control mejorado del mantenimiento de WSUS <!--4110109--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#improved-control-over-wsus-maintenance) | ![Sin agregar](media/Red_X.gif) |
 | Imágenes de sistema operativo y paquetes de controladores de caché previa <!--4224642--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_precache) | ![Sin agregar](media/Red_X.gif) |
 | Mejoras en la implementación del sistema operativo <!--2839943,4447680--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_osd) | ![Sin agregar](media/Red_X.gif) |
 | Programa de estimación de costes de servicios en la nube <!--3555774--> | [Versión preliminar técnica 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_cmg) | ![Sin agregar](media/Red_X.gif) |
 | Uso del punto de distribución como servidor de caché local para la Optimización de distribución <!--3555764--> | [Versión preliminar técnica 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_doinc) | ![Sin agregar](media/Red_X.gif) |
 | Reclamación de bloqueo para editar secuencias de tareas <!--3699337--> | [Versión preliminar técnica 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_sedo) | ![Sin agregar](media/Red_X.gif) |
 | Obtención de detalles de actualizaciones necesarias <!--4224414--> | [Versión preliminar técnica 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_req-updates) | ![Sin agregar](media/Red_X.gif) |
 | Mejoras en la creación de medios de secuencia de tareas <!--4090666--> | [Versión preliminar técnica 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_tsmedia) | ![Sin agregar](media/Red_X.gif) |
 | Idiomas adicionales para las actualizaciones de Office 365 <!--3555955--> | [Tech Preview 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_o365lang) | Versión 1902 |
 | Integración con los análisis para la preparación de Office 365 ProPlus <!--3735402--> | [Tech Preview 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_o365) | Versión 1902 |
 | Mejora de los criterios de éxito para la implementación por fases <!--3555946--> | [Tech Preview 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_pod) | Versión 1902 |
 | Optimización de HTTP mejorado <!--3798957--> | [Tech Preview 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_ehttp) | Versión 1902 |
 | Reemplazo de las notificaciones del sistema por una ventana de cuadro de diálogo <!--3555947--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_impact) | Versión 1902 |
 | Estado de progreso durante la secuencia de tareas de actualización local <!--3747129--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_ipu) | Versión 1902 |
 | Redirección de carpetas conocidas de Windows a OneDrive <!--3556021--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_odfb) | Versión 1902 |
 | Visualización de la primera pantalla solo durante el control remoto <!--3231732--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_rcmulti) | Versión 1902 |
 | Edición o copia de scripts de PowerShell <!--3705507--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_psedit) | Versión 1902 |
 | Adición de una puerta de enlace de administración de la nube a grupos de límites <!--3640932--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_cmgbg) | Versión 1902 |
 | Configuración de vistas predeterminadas en el Centro de software <!--3612112--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_swctr) | Versión 1902 |
 | Mejoras en el panel de mantenimiento del cliente <!--3599209--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_health) | Versión 1902 |


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
