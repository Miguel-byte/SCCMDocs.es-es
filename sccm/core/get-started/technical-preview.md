---
title: Versiones de Technical Preview
titleSuffix: Configuration Manager
description: Obtenga información sobre la rama de Technical Preview para probar nuevas funcionalidades y funcionalidades de Configuration Manager.
ms.date: 02/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c48e7fdd2826af942cc94017d58614760f61545d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136990"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview para Configuration Manager

*Se aplica a: System Center Configuration Manager (Technical Preview)*

Este artículo proporciona detalles sobre de la rama de Technical Preview mensual de Configuration Manager. Technical Preview presenta una funcionalidad nueva en que está trabajando Microsoft. Presenta características nuevas que no están todavía incluida en la rama actual de Configuration Manager. Estas características podrían incluirse finalmente en una actualización de la rama actual. Antes de finalizar la las características, queremos que las pruebe y nos comparta sus comentarios.  

Como esta es una versión preliminar técnica, los detalles y las funcionalidades están sujetos a cambios.  

Esta información se aplica a todas las versiones de la rama de Technical Preview de Configuration Manager. En este artículo se enumera cada una de las características nuevas junto con la versión de Technical Preview en las que aparece por primera vez. Por ejemplo, la versión **1901** de enero (01) de 2019 (19). Los artículos independientes dedicados a cada versión preliminar detallan las características individuales.  

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

    -   SQL Server 2017 (con la actualización acumulativa 2 o posterior) 
    -   SQL Server 2016 (sin ningún Service Pack)
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

-  **Technical Preview, versión 1810.2**: la versión 1810.2 de Technical Preview de Configuration Manager está disponible como actualización en consola y como una versión de base de referencia nueva. Descargue las versiones de base de referencia [del centro de evaluación de TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).



##  <a name="BKMK_TPFeedback"></a> Proporcionar comentarios  

Nos encanta recibir sus comentarios sobre las características nuevas en Technical Preview. Para obtener más información, vea [Comentarios sobre el producto](/sccm/core/understand/find-help#product-feedback).

También puede hablarnos sobre las ideas que tenga sobre características nuevas que le gustaría ver. Para enviar nuevas ideas y votar sobre las ideas enviadas por otros usuarios, [visite nuestra página de UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> Características de la versión más reciente  

Las características siguientes están disponibles con la versión de Technical Preview de Configuration Manager más reciente: 

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1902"></a>Technical Preview, versión 1902

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor)<!--ID-->

- [Reemplazo de las notificaciones del sistema por una ventana de diálogo](/sccm/core/get-started/2019/technical-preview-1902#bkmk_impact)<!--3555947-->
- [Estado de progreso durante la secuencia de tareas de actualización local](/sccm/core/get-started/2019/technical-preview-1902#bkmk_ipu)<!--3747129-->
- [Redirección de carpetas conocidas de Windows a OneDrive](/sccm/core/get-started/2019/technical-preview-1902#bkmk_odfb)<!--3556021-->
- [Visualización de la primera pantalla solo durante el control remoto](/sccm/core/get-started/2019/technical-preview-1902#bkmk_rcmulti)<!--3231732-->
- [Edición o copia de scripts de PowerShell](/sccm/core/get-started/2019/technical-preview-1902#bkmk_psedit)<!--3705507-->
- [Adición de una puerta de enlace de administración de la nube a los grupos de límites](/sccm/core/get-started/2019/technical-preview-1902#bkmk_cmgbg)<!--3640932-->
- [Configuración de vistas predeterminadas en el Centro de software](/sccm/core/get-started/2019/technical-preview-1902#bkmk_swctr)<!--3612112-->
- [Mejoras en el panel de mantenimiento del cliente](/sccm/core/get-started/2019/technical-preview-1902#bkmk_health)<!--3599209-->



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
 | Panel de mantenimiento del cliente <!--3599209--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_health) | ![Sin agregar](media/Red_X.gif) | 
 | Especificación de la prioridad de las actualizaciones de características en el mantenimiento de Windows 10 <!--3734525--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_neo) | ![Sin agregar](media/Red_X.gif) | 
 | Supervisión dedicada para implementaciones por fases <!--3555949--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_pod) | ![Sin agregar](media/Red_X.gif) | 
 | Ejecución de CMPivot desde el sitio de administración central <!--3610960--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmpivot) | ![Sin agregar](media/Red_X.gif) | 
 | Mejoras del paso de secuencia de tareas Ejecutar script de PowerShell <!--3556028--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_posh) | ![Sin agregar](media/Red_X.gif) | 
 | Productos de Office en el panel de ciclo de vida <!--3556026--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_lifecycle) | ![Sin agregar](media/Red_X.gif) | 
 | Reglas de información de administración para colecciones <!--3555752--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_micoll) | ![Sin agregar](media/Red_X.gif) | 
 | Vistas de búsqueda de dispositivos mediante dirección MAC <!--3600878--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_mac) | ![Sin agregar](media/Red_X.gif) | 
 | Modo de mantenimiento del punto de distribución <!--3555754--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_dpmaint) | ![Sin agregar](media/Red_X.gif) | 
 | Servicio de imágenes optimizado <!--3555951--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_resetbase) | ![Sin agregar](media/Red_X.gif) | 
 | Importación de un índice único de una imagen de sistema operativo <!--3719699--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_index) | ![Sin agregar](media/Red_X.gif) | 
 | Uso de Azure Resource Manager para servicios en la nube <!--3605704--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_arm) | ![Sin agregar](media/Red_X.gif) | 
 | Confirmación de comentarios de la consola <!--3556010--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_feedback) | ![Sin agregar](media/Red_X.gif) | 
 | Creación de un laboratorio de Configuration Manager Technical Preview en Azure <!--3556017--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_azurevm) | ![Sin agregar](media/Red_X.gif) | 
 | Especificación de un puerto personalizado para reactivación del mismo nivel <!--3605925--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_sleep) | ![Sin agregar](media/Red_X.gif) | 
 | Consulta de las consolas conectadas recientemente <!--3699367--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_console) | ![Sin agregar](media/Red_X.gif) | 
 | Detención del servicio en la nube cuando se supera el umbral <!--3735092--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmg) | ![Sin agregar](media/Red_X.gif) | 
 | Tiempo de espera del modo de aprovisionamiento de cliente <!--3197824--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osdprov) | ![Sin agregar](media/Red_X.gif) | 
 | Mejoras en la implementación del sistema operativo <!--3633146,3641475,3654172,3734270--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osd) | ![Sin agregar](media/Red_X.gif) | 
 | Mejoras del paso de secuencia de tareas Ejecutar script de PowerShell <!--3556028 fka 1359389--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_posh) | ![Sin agregar](media/Red_X.gif) | 
 | Mejoras de las aprobaciones de aplicación por correo electrónico <!--3594063--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_email) | ![Sin agregar](media/Red_X.gif) | 
 | Configurar afinidad entre usuario y dispositivo en el Centro de software <!--3485366--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_uda) | ![Sin agregar](media/Red_X.gif) | 
 | Mejoras en la consola de Configuration Manager <!--3594151--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_console) | ![Sin agregar](media/Red_X.gif) | 
 | Descargar informes desde el Centro de comunidad<!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) | ![Sin agregar](media/Red_X.gif) | 
 | No cargar perfiles de Windows PowerShell <!--1359239--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_noprofile) | ![Sin agregar](media/Red_X.gif) | 
 | Ya no se requiere una conexión de Intune para MDM local <!--1359124--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_opmdm) | ![Sin agregar](media/Red_X.gif) | 
 | Notificaciones de la consola de Configuration Manager <!--1318035--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_notify) | ![Sin agregar](media/Red_X.gif) | 
 | Mejoras en la creación de medios de secuencia de tareas <!--1359388--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_tsmedia) | ![Sin agregar](media/Red_X.gif) | 
 | Mejora del paso de secuencia de tareas Ejecutar script de PowerShell <!--1359389--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_posh) | ![Sin agregar](media/Red_X.gif) | 



## <a name="features-in-previous-technical-previews"></a>Características de las versiones de Technical Preview anteriores

Las características siguientes se lanzaron con versiones anteriores de la rama de Technical Preview de Configuration Manager. Estas características siguen estando disponibles en versiones posteriores, pero todavía no están disponibles en la rama actual. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Característica        | Versión de Technical Preview |  
|----------------|---------------------------|
| Panel de documentación en consola <!--1357546--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_doc-dashboard) | 
| Central de comunidad <!--1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) | 
| Actividad de sincronización de dispositivos administrados conjuntamente desde Intune <!--1358565--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_comgmt) | 
| Servicio del respondedor PXE basado en cliente <!--1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Compatibilidad con el arranque de red de PXE para IPv6 <!--1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Uso de Azure Active Directory <!--1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Evaluación del cumplimiento para actualizaciones de Windows Update para empresas <!--1235390--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
| Mejoras en Asset Intelligence <!--1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |
| Los usuarios finales pueden instalar aplicaciones desde el Portal de empresa <!--1037233?--> | [Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End) |



## <a name="see-also"></a>Consulte también  

Vea los siguientes artículos para más información:  

- [Evaluar Configuration Manager en un laboratorio](/sccm/core/get-started/evaluate-with-lab-environment)
- [Novedades de las versiones incrementales de Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introducción a Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Para más información sobre las características de la rama actual que requieren consentimiento, consulte las [características de versión preliminar](/sccm/core/servers/manage/pre-release-features).  
> 
> Para más información sobre las características de la rama actual que se deben habilitar primero, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
