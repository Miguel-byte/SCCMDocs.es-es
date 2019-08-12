---
title: Versiones de Technical Preview
titleSuffix: Configuration Manager
description: Obtenga información sobre la rama de Technical Preview para probar nuevas funcionalidades y funcionalidades de Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 977f5cc2d9719a333aa4f063a6e4f9c505e82d3b
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68535881"
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

<!-- comment out until 1908.1 TP
## Features in recent technical previews

The following features were released with previous versions of the Configuration Manager technical preview branch since current branch version 1906:

> [!Tip]  
> When a new current branch version is available, features that are available in that version are listed in the latest *What's new* article. For more information, see [What's new in incremental versions](/sccm/core/plan-design/changes/whats-new-incremental-versions#supported-versions).

<!-- This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->


## <a name="features-in-previous-technical-previews"></a>Características de las versiones de Technical Preview anteriores

Las características siguientes se lanzaron con versiones anteriores de la rama de Technical Preview de Configuration Manager. Estas características siguen estando disponibles en versiones posteriores, pero todavía no están disponibles en la rama actual.

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Característica        | Versión de Technical Preview |  
|----------------|---------------------------|
| Control remoto en cualquier lugar mediante Cloud Management Gateway <!--4575930--> | [Tech Preview 1906](/sccm/core/get-started/2019/technical-preview-1906#remote-control-anywhere-using-cloud-management-gateway) |
| Mejoras en el Centro de comunidad <!--3555935--> | [Tech Preview 1906](/sccm/core/get-started/2019/technical-preview-1906#bkmk_hub) |
| Opciones adicionales para los catálogos de actualizaciones de terceros <!--4469002--> | [Tech Preview 1906](/sccm/core/get-started/2019/technical-preview-1906#additional-options-for-third-party-update-catalogs) |
| Secuencia de tareas como un tipo de implementación de modelo de aplicación <!--3555953--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdt) |
| Administración de BitLocker <!--3601034--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_bitlocker) |
| Mejoras en el Centro de comunidad <!--4224401--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_hub) |
| GitHub y Centro de comunidad <!--3555935--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#community-hub-and-github) |
| Programa de estimación de costes de servicios en la nube <!--3555774--> | [Versión preliminar técnica 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_cmg) |
| Descarga de informes desde el Centro de comunidad <!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Centro de comunidad <!--3556020, fka 1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| Servicio del respondedor PXE basado en cliente <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Compatibilidad con el arranque de red de PXE para IPv6 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Uso de Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Mejoras en Asset Intelligence <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |


## <a name="see-also"></a>Consulte también  

Vea los siguientes artículos para más información:  

- [Evaluar Configuration Manager en un laboratorio](/sccm/core/get-started/evaluate-with-lab-environment)
- [Novedades de las versiones incrementales de Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introducción a Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Para más información sobre las características de la rama actual que requieren consentimiento, consulte las [características de versión preliminar](/sccm/core/servers/manage/pre-release-features).  
>
> Para más información sobre las características de la rama actual que se deben habilitar primero, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
