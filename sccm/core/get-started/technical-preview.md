---
title: Versiones de Technical Preview
titleSuffix: Configuration Manager
description: Obtenga información sobre la rama de Technical Preview para probar nuevas funcionalidades y funcionalidades de Configuration Manager.
ms.date: 10/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c43b501e8305f97f178d2eba9d3ab64fa9efe2a7
ms.sourcegitcommit: 3dfe3f4401651afa9dc65d14a8944ae4e4198b3e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/08/2018
ms.locfileid: "48862454"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview para Configuration Manager

*Se aplica a: System Center Configuration Manager (Technical Preview)*

Este artículo proporciona detalles sobre de la rama de Technical Preview mensual de Configuration Manager. Technical Preview presenta una funcionalidad nueva en que está trabajando Microsoft. Presenta características nuevas que no están todavía incluida en la rama actual de Configuration Manager. Estas características podrían incluirse finalmente en una actualización de la rama actual. Antes de finalizar la las características, queremos que las pruebe y nos comparta sus comentarios.  

Como esta es una versión preliminar técnica, los detalles y las funcionalidades están sujetos a cambios.  

Esta información se aplica a todas las versiones de la rama de Technical Preview de Configuration Manager. En este artículo se enumera cada una de las características nuevas junto con la versión de Technical Preview en las que aparece por primera vez. Por ejemplo, la versión **1809** de septiembre (09) de 2018 (18). Los artículos independientes dedicados a cada versión preliminar detallan las características individuales.  

Para más información sobre las novedades de la *rama actual* de Configuration Manager, consulte [Novedades de las versiones incrementales de Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).



##  <a name="bkmk_reqs"></a> Limitaciones y requisitos  

> [!IMPORTANT]     
>  La versión preliminar técnica solo tiene licencia para su uso en un entorno de laboratorio. Es posible que Microsoft no proporcione servicios de soporte técnico y que algunas características no estén disponibles en el software de versión preliminar. Además, es posible que el software de versión preliminar tenga estándares de seguridad, privacidad, accesibilidad, disponibilidad y confiabilidad reducidos o diferentes a los del software proporcionado comercialmente.  

Para la mayoría de requisitos previos de producto, use la información que se encuentra en las [configuraciones admitidas](/sccm/core/plan-design/configs/supported-configurations). Las excepciones siguientes se aplican a la rama de Technical Preview:  

-   Cada instalación permanece activa durante 90 días y luego cambia a inactiva.  

-   El único idioma admitido es el inglés.  

-   Solo admite los parámetros de línea de comandos de configuración siguientes:  
    -   `/silent`  
    -   `/testdbupgrade`    

-   El punto de conexión del servicio se instala en el modo en línea. No admite el modo sin conexión.  

-   En los artículos independientes de cada versión específica de Technical Preview se incluyen limitaciones o requisitos adicionales, según corresponda.

-   Las características siguientes no son compatibles con la rama de Technical Preview:  

    - [Migración](/sccm/core/migration/migrate-data-between-hierarchies) desde o hasta esta rama de versión preliminar.  

    - [Actualización](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) a esta rama de versión preliminar.  

    - [Recuperación del sitio](/sccm/core/servers/manage/recover-sites) desde la carpeta cd.latest.  <!--507106-->

-   No se admite la actualización de esta rama de versión preliminar a la rama actual.  

    > [!Note]  
    > Cuando haya actualizaciones disponibles para una versión preliminar, seguirá siendo posible buscarlas e instalarlas desde el nodo **Actualizaciones y mantenimiento** de la consola de Configuration Manager. Para ver un vídeo del proceso de actualización en la consola, vea [Installing Configuration Manager update packages](https://www.youtube.com/embed/KBd_EGFbUT8) (Instalación de las actualizaciones de Configuration Manager) en youtube.com.  

-   Solo admite un sitio primario independiente. No se admiten sitios de administración central, varios sitios primarios ni sitios secundarios.  

La rama de Technical Preview de Configuration Manager admite los productos y las tecnologías siguientes: 

-   Solo es compatible con las versiones siguientes de **SQL Server**:  

    -   SQL Server 2017 (con la actualización acumulativa 2 y versiones posteriores) a partir de la versión 1710 de Configuration Manager
    -   SQL Server 2016 (sin ningún Service Pack, y versiones posteriores)
    -   SQL Server 2014 (con Service Pack 1, o versiones posteriores)
    -   SQL Server 2012 (con Service Pack 3, o versiones posteriores)  


-   El sitio admite hasta 10 clientes, que deben ejecutar una de las siguientes versiones de Windows:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

> [!Note]  
> La inclusión de estos productos en este contenido no implica una extensión de la compatibilidad con una versión que están fuera de su ciclo de vida de soporte. Configuration Manager no es compatible con los productos que están fuera de su ciclo de vida de soporte. Para más información, consulte [Directiva de ciclo de vida de Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270).  



##  <a name="bkmk_install"></a> Instalación y actualización  

La rama de Technical Preview de Configuration Manager para su uso en laboratorio es distinta de la rama actual de Configuration Manager para su uso en producción.  

En primer lugar, instale una versión de base de referencia de la rama de Technical Preview. Después de instalar una versión de referencia, use las actualizaciones en consola para que la instalación cuente con la versión preliminar más reciente. Normalmente, las nuevas versiones de Technical Preview están disponibles cada mes.

Microsoft admite cada versión de Technical Preview hasta que hay disponibles tres versiones sucesivas. Por ejemplo, cuando se publica la versión 1708, se deja de admitir la versión 1704. Las versiones 1705, 1706 y 1707 siguen siendo compatibles. Cuando una base de referencia deja de ser compatible, todavía se admite para instalar un nuevo sitio de Technical Preview, suponiendo que se actualiza inmediatamente a una versión compatible. La base de referencia anterior se admite hasta que haya disponible una versión de base de referencia nueva. Actualice a la versión disponible más reciente desde la base de referencia y repita el proceso de actualización hasta instalar la versión de Technical Preview más reciente.

> [!TIP]  
>  Cuando se instala una actualización de versión preliminar técnica, la instalación de versión preliminar se actualiza a la nueva versión preliminar técnica. Una instalación de Technical Preview nunca tiene la opción de actualizar a una instalación de rama actual. Tampoco recibe nunca actualizaciones desde la versión de rama actual. 
> 
> Varias veces a lo largo del año, hay versiones de rama de Technical Preview y versiones de rama actuales con el mismo número de versión. Por ejemplo, hay una versión 1802 de Technical Preview y una versión 1802 de rama actual. 


### <a name="active-baseline-versions"></a>Versiones de base de referencia activas
   
Instale una versión de base de referencia hasta un año después de su lanzamiento. Cuando instale un sitio de Technical Preview nuevo, use la versión de base de referencia más reciente si hay más de una versión de base de referencia disponible actualmente.

-  **Versión de Technical Preview 1806**: la versión 1806 de Technical Preview de Configuration Manager está disponible tanto como actualización en consola como una versión de base de referencia nueva. Descargue las versiones de base de referencia [desde el centro de evaluación de TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).



##  <a name="BKMK_TPFeedback"></a> Proporcionar comentarios  

Nos encanta recibir sus comentarios sobre las características nuevas en Technical Preview. Para obtener más información, vea [Comentarios sobre el producto](/sccm/core/understand/find-help#product-feedback).

También puede hablarnos sobre las ideas que tenga sobre características nuevas que le gustaría ver. Para enviar nuevas ideas y votar sobre las ideas enviadas por otros usuarios, [visite nuestra página de UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> Características de la versión más reciente  

Las características siguientes están disponibles con la versión de Technical Preview de Configuration Manager más reciente: 

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1810"></a>Versión de Technical Preview 1810

- [Mejora en la instalación del cliente](capabilities-in-technical-preview-1810.md#bkmk_ccmsetup) <!--1358840-->
- [Directiva de cumplimiento de aplicaciones requerida para los dispositivos administrados conjuntamente](capabilities-in-technical-preview-1810.md#bkmk_app-compliance) <!--1358196-->
- [Mejora en el panel de administración conjunta](capabilities-in-technical-preview-1810.md#bkmk_comgmt-report) <!--1358980-->
- [Nuevas opciones del grupo de límites](capabilities-in-technical-preview-1810.md#bkmk_bgoptions) <!--1358749-->
- [Sistema de sitio en el nodo del clúster de Windows](capabilities-in-technical-preview-1810.md#bkmk_cluster) <!--1359132-->
- [Mejoras en CMPivot](capabilities-in-technical-preview-1810.md#bkmk_cmpivot) <!--1359068-->
- [Mejoras para scripts](capabilities-in-technical-preview-1810.md#bkmk_scripts) <!--1358239-->
- [Nueva acción de notificación de cliente para reactivar el dispositivo](capabilities-in-technical-preview-1810.md#bkmk_wakeup) <!--1317364-->
- [Compatibilidad de la secuencia de tareas para grupos de límites](capabilities-in-technical-preview-1810.md#bkmk_bgr-osd) <!--1359025-->
- [Panel de información de administración](capabilities-in-technical-preview-1810.md#bkmk_insights) <!--1357979-->
- [Panel de documentación en consola](capabilities-in-technical-preview-1810.md#bkmk_doc-dashboard) <!--1357546-->
- [Mejoras en el mantenimiento del controlador](capabilities-in-technical-preview-1810.md#bkmk_drivers) <!--1358270-->  


> [!Note]  
> Las características que estaban disponibles en una versión anterior de Technical Preview siguen estando disponibles en versiones posteriores. Del mismo modo, las características que se agregan a la rama actual de Configuration Manager siguen estando disponibles en la rama de Technical Preview.   



## <a name="features-in-recent-supported-technical-previews"></a>Características en versiones Technical Preview compatibles recientes

Las características siguientes se lanzaron con versiones anteriores de la rama de Technical Preview de Configuration Manager que todavía se admiten: 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Característica |Versión de Technical Preview |Versión de rama actual|  
 |----------------|---------------------|--------------------|
 | Mejoras en CMPivot <!--1359068--> | [Tech Preview 1809](capabilities-in-technical-preview-1809.md#bkmk_cmpivot) | ![Sin agregar](media/Red_X.gif) | 
 | Mejoras en el panel de ciclo de vida <!--1358702--> | [Tech Preview 1809](capabilities-in-technical-preview-1809.md#bkmk_lifecycle) | ![Sin agregar](media/Red_X.gif) | 
 | Mejoras en el almacén de datos <!--1358870--> | [Tech Preview 1809](capabilities-in-technical-preview-1809.md#bkmk_dataw) | ![Sin agregar](media/Red_X.gif) | 
 | Mejoras en las ventanas de mantenimiento para actualizaciones de software <!--vso2839307--> | [Tech Preview 1809](capabilities-in-technical-preview-1809.md#bkmk_sum-mw) | ![Sin agregar](media/Red_X.gif) | 
 | Implementación por fases de las actualizaciones de software <!--1358146--> | [Tech Preview 1808](capabilities-in-technical-preview-1808.md#bkmk_pod) | ![Sin agregar](media/Red_X.gif) | 
 | Mejoras para reparar las aplicaciones <!--1357866--> | [Tech Preview 1808](capabilities-in-technical-preview-1808.md#bkmk_repair) | ![Sin agregar](media/Red_X.gif) | 
 | Central de comunidad <!--1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) | ![Sin agregar](media/Red_X.gif) | 
 | Especificación de la unidad para la instalación sin conexión de imágenes de SO <!--1358924--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_osd) | ![Sin agregar](media/Red_X.gif) | 
 | Actividad de sincronización de dispositivos administrados conjuntamente desde Intune <!--1358565--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_comgmt) | ![Sin agregar](media/Red_X.gif) | 
 | Reparación de aplicaciones <!--1357866--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_app-repair) | ![Sin agregar](media/Red_X.gif) | 
 | Aprobación de solicitudes de aplicación por correo electrónico <!--1321550--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_email-approve) | ![Sin agregar](media/Red_X.gif) | 
 | Mejora en la salida del script <!--1236459--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_script) | ![Sin agregar](media/Red_X.gif) | 
 | Mejora de las actualizaciones de software de terceros <!--1358714--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_3pupdate) | ![Sin agregar](media/Red_X.gif) | 



## <a name="features-in-previous-technical-previews"></a>Características de las versiones de Technical Preview anteriores

Las características siguientes se lanzaron con versiones anteriores de la rama de Technical Preview de Configuration Manager. Estas características siguen estando disponibles en versiones posteriores, pero todavía no están disponibles en la rama actual. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

|Característica |Versión de Technical Preview |  
|----------------|---------------------|
|Centro de soporte técnico <!--1357489--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#support-center)  | 
|Servicio del respondedor PXE basado en cliente <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
|Compatibilidad con el arranque de red de PXE para IPv6 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
|Uso de Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
|Evaluación del cumplimiento para actualizaciones de Windows Update para empresas <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
|Acceso a datos de punto de conexión de OData <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
|Mejoras en Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
|Los usuarios finales pueden instalar aplicaciones desde el Portal de empresa <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>Consulte también  

Vea los siguientes artículos para más información:  

- [Evaluar Configuration Manager en un laboratorio](/sccm/core/get-started/evaluate-with-lab-environment)
- [Novedades de las versiones incrementales de Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introducción a Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Para más información sobre las características de la rama actual que requieren consentimiento, consulte las [características de versión preliminar](/sccm/core/servers/manage/pre-release-features).  
> 
> Para más información sobre las características de la rama actual que se deben habilitar primero, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
