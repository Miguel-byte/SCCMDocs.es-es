---
title: Versiones de Technical Preview
titleSuffix: Configuration Manager
description: Obtenga información sobre la rama de Technical Preview para probar nuevas funcionalidades y funcionalidades de Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4be568e997a85acf49c3c86971f8d678d916aef0
ms.sourcegitcommit: 7eebd112a9862bf98359c1914bb0c86affc5dbc0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2018
ms.locfileid: "42589532"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview para Configuration Manager

*Se aplica a: System Center Configuration Manager (Technical Preview)*

Este artículo proporciona detalles sobre de la rama de Technical Preview mensual de Configuration Manager. Technical Preview presenta una funcionalidad nueva en que está trabajando Microsoft. Presenta características nuevas que no están todavía incluida en la rama actual de Configuration Manager. Estas características podrían incluirse finalmente en una actualización de la rama actual. Antes de finalizar la las características, queremos que las pruebe y nos comparta sus comentarios.  

Como esta es una versión preliminar técnica, los detalles y las funcionalidades están sujetos a cambios.  

Esta información se aplica a todas las versiones de la rama de Technical Preview de Configuration Manager. En este artículo se enumera cada una de las características nuevas junto con la versión de Technical Preview en las que aparece por primera vez. Por ejemplo, la versión **1806** de junio (06) de 2018 (18). Los artículos independientes dedicados a cada versión preliminar detallan las características individuales.  

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

### <a name="technical-preview-version-1808"></a>Versión de Technical Preview 1808

- [Implementación por fases de las actualizaciones de software](capabilities-in-technical-preview-1808.md#bkmk_pod) <!--1358146-->
- [Mejoras para reparar las aplicaciones](capabilities-in-technical-preview-1808.md#bkmk_repair) <!--1357866-->


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
 | Central de comunidad <!--1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) | ![Sin agregar](media/Red_X.gif) | 
 | Especificación de la unidad para la instalación sin conexión de imágenes de SO <!--1358924--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_osd) | ![Sin agregar](media/Red_X.gif) | 
 | Actividad de sincronización de dispositivos administrados conjuntamente desde Intune <!--1358565--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_comgmt) | ![Sin agregar](media/Red_X.gif) | 
 | Reparación de aplicaciones <!--1357866--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_app-repair) | ![Sin agregar](media/Red_X.gif) | 
 | Aprobación de solicitudes de aplicación por correo electrónico <!--1321550--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_email-approve) | ![Sin agregar](media/Red_X.gif) | 
 | Mejora en la salida del script <!--1236459--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_script) | ![Sin agregar](media/Red_X.gif) | 
 | Mejora de las actualizaciones de software de terceros <!--1358714--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_3pupdate) | ![Sin agregar](media/Red_X.gif) | 
 | Mejoras en las implementaciones por fases <!--1358577,1358147,1358578--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_pod)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Compatibilidad con nuevos formatos de paquete de aplicaciones de Windows <!--1357427--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_msix)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mejora de seguridad de inserción de cliente <!--1358204--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_client-push)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Información de administración para un mantenimiento proactivo <!--1352184,et al--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_insights)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Carga de trabajo de aplicaciones móviles de transición para los dispositivos administrados conjuntamente <!--1357892--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_comgmt)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Opciones de grupo de límites para descargas del mismo nivel <!--1356193--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_bgoptions)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Soporte técnico de actualizaciones de software de terceros para catálogos personalizados <!--1358714--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mejoras de las características de administración en la nube <!--511980,515854--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_cloud)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Informe de cumplimiento de nuevas actualizaciones de software <!--1357775--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_report)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Actualizaciones de software de terceros <!--1352101--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Configurar SmartScreen de Windows Defender para Microsoft Edge <!--1353701--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#configure-windows-defender-smartscreen-settings-for-microsoft-edge)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Sincronizar directiva MDM desde Microsoft Intune para un dispositivo administrado conjuntamente <!--1357377--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Transición de la carga de trabajo de Office 365 a Intune mediante la administración conjunta <!--1357841--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#transition-office-365-workload-to-intune-using-co-management)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Package Conversion Manager <!--1357861--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#package-conversion-manager)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Implementar actualizaciones de software sin contenido <!--1357933--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#deploy-software-updates-without-content)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Integración de la Herramienta de personalización de Office en el instalador de Office 365 <!--1358149--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#office-customization-tool-integration-with-the-office-365-installer)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mejoras en Cloud Management Gateway <!--1358215,1358651,503899--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-cloud-management-gateway)   | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mejoras en las comunicaciones de cliente seguras <!--1358278,1358279--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-secure-client-communications)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mejoras de la infraestructura del Centro de software <!--1358309--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#software-center-infrastructure-improvements)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Aprovisionar los paquetes de aplicación de Windows para todos los usuarios en un dispositivo <!--1358310--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#provision-windows-app-packages-for-all-users-on-a-device)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mejoras en el panel de Surface <!--1358654--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-the-surface-dashboard)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Revisión de unidad predeterminada de inventario de hardware <!--514442--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#hardware-inventory-default-unit-revision)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Creación de una implementación por fases con fases configuradas manualmente para una secuencia de tareas <!--1358148--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Compatibilidad con puntos de distribución de nube para Azure Resource Manager <!--1322209--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Realización de acciones basadas en la información de administración <!--1357930--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#take-actions-based-on-management-insights)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Transición de la carga de trabajo de la configuración del dispositivo a Intune mediante la administración conjunta <!--1357903--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#transition-device-configuration-workload-to-intune-using-co-management)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Habilitación de los puntos de distribución para usar el control de congestión de red <!--1358112--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#enable-distribution-points-to-use-network-congestion-control)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Panel de administración en la nube <!--1358461--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-management-dashboard)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | CMPivot <!--1358456--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmpivot)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Comunicaciones de cliente seguras mejoradas <!--1356889,1358228,1358460--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mejoras para habilitar la compatibilidad de actualización de software de terceros <!--1357605--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mejoras en la secuencia de tareas de actualización local de Windows 10 <!--1358500--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-windows-10-in-place-upgrade-task-sequence)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Herramienta CMTrace instalada con el cliente <!--1357971--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmtrace-installed-with-client)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mejora en la consola de Configuration Manager <!--1358202--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-the-configuration-manager-console)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mejoras en los comentarios de la consola <!--1357542--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-console-feedback)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mejoras en los puntos de distribución habilitados con PXE <!--1357580--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-pxe-enabled-distribution-points)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mejora en el inventario de hardware para los valores enteros grandes <!--1357880--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mejora en el mantenimiento de WSUS <!--1357898--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-wsus-maintenance)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mejora en la compatibilidad con certificados CNG <!--1357314--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-support-for-cng-certificates)  | [Versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  

  

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
