---
title: Versiones de Technical Preview
titleSuffix: Configuration Manager
description: Obtenga información sobre la versión Technical Preview para probar nuevas funcionalidades y capacidades de Configuration Manager.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 4509c7da3ca36d2ffd3de36774bf069c40d95ce2
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Technical Preview)*

**Le damos la bienvenida a System Center Configuration Manager Technical Preview**. En este artículo se proporcionan detalles sobre la versión preliminar en evolución que presenta nuevas funcionalidades y características en las que estamos trabajando. En cada nueva versión preliminar técnica se presentan nuevas características que no se incluyeron en la rama actual de Configuration Manager cuando se puso a disposición la versión preliminar técnica. Estas características podrían incluirse finalmente en una actualización de la versión actual de la rama, pero antes de finalizarlas y agregarlas, queremos que tenga la oportunidad de probarlas y enviarnos sus comentarios.  

 Como esta es una versión preliminar técnica, los detalles y las funcionalidades están sujetos a cambios.  

 Este artículo contiene información que se aplica a todas las versiones de Technical Preview. También se muestra cada nueva funcionalidad (o característica) junto con la versión de Technical Preview en la que aparece por primera vez, como la versión 1802 para febrero de 2018. Estas características se detallan en temas independientes dedicados a cada versión preliminar.  

 Para obtener más información sobre las novedades en la rama actual de Configuration Manager, consulte [Novedades de System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requisitos y limitaciones de Technical Preview  

> [!IMPORTANT]     
>  La versión Technical Preview solo tiene licencia para su uso en un entorno de laboratorio.  Es posible que Microsoft no proporcione servicios de soporte técnico y que algunas características no estén disponibles en el software de versión preliminar. Además, es posible que el software de versión preliminar tenga estándares de seguridad, privacidad, accesibilidad, disponibilidad y confiabilidad reducidos o diferentes a los del software proporcionado comercialmente.  

 Para la mayoría de requisitos previos del producto, use la información que aparece en [Configuraciones admitidas para System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). Las excepciones siguientes se aplican a las versiones Technical Preview:  

-   Todas las instalaciones permanecen activas durante 90 días y luego cambian a inactivas.  

-   El único idioma admitido es el inglés.


-   Solo se admiten los siguientes indicadores de instalación (conmutadores):  

    -   **/silent**  
    -   **/testdbupgrade**    


-   De forma predeterminada, cuando se usa Technical Preview, el punto de conexión de servicio se instala en modo en línea. No admite el cambio al modo sin conexión.

-   En los artículos independientes de cada versión específica de Technical Preview se incluyen limitaciones o requisitos adicionales, según corresponda.

-   No se admite la migración a esta versión preliminar o desde ella.  

-   No se admite la actualización a esta versión preliminar. 

-   No hay ninguna compatibilidad para la recuperación de sitio desde la carpeta cd.latest.  <!--507106-->

-   No se admite la actualización a una versión de producción (rama actual) desde esta versión preliminar. En cambio, cuando haya actualizaciones disponibles para una versión preliminar, puede buscarlas e instalarlas desde el nodo **Actualizaciones y mantenimiento** de la consola de Configuration Manager. Para ver un vídeo del proceso de actualización en la consola, consulte [Installing ConfigMgr Update Package (Instalación de paquetes de actualización de Configuration Manager)](https://www.youtube.com/embed/KBd_EGFbUT8) en youtube.com.  
-   Solo se admite un sitio primario independiente. No se admiten sitios de administración central, varios sitios primarios ni sitios secundarios.  

Los siguientes productos y tecnologías son compatibles con esta rama de Configuration Manager. Sin embargo, su inclusión en este contenido no implica una extensión de la compatibilidad con cualquier producto o versión más allá del ciclo de vida de soporte individual de los productos. Los productos que están fuera de su ciclo de vida de soporte no se pueden usar con Configuration Manager. Para obtener más información sobre los ciclos de vida de soporte de Microsoft, visite el sitio web [Ciclo de vida de soporte de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270).  

-   Solo se admiten las siguientes versiones de SQL Server:  

    -   SQL Server 2017 (con la actualización acumulativa 2 y versiones posteriores) a partir de la versión 1710 de Configuration Manager
    -   SQL Server 2016 (sin ningún Service Pack, y versiones posteriores)
    -   SQL Server 2014 (con Service Pack 1, o versiones posteriores)
    -   SQL Server 2012 (con Service Pack 3, o versiones posteriores)


-   El sitio admite hasta 10 clientes, que deben ejecutar una de las siguientes versiones de Windows:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

##  <a name="bkmk_install"></a> Instalar y actualizar la versión Technical Preview  
 System Center Configuration Manager Technical Preview es diferente de la versión actual de System Center Configuration Manager.  

 Para usar la versión preliminar técnica, primero debe instalar una **versión de base de referencia** de la compilación de dicha versión. Después de instalar una versión de referencia, use las **actualizaciones en consola** para que la instalación cuente con la versión preliminar más reciente. Normalmente, las nuevas versiones de Technical Preview están disponibles cada mes.

Cada versión preliminar se admite hasta que tres versiones sucesivas están disponibles. Es decir, cuando se publicó la versión 1708, la versión 1704 ya no se admitía, pero las versiones 1705, 1706 y 1707 seguían admitiéndose. Si una base de referencia deja de ser compatible, todavía se admite para instalar un nuevo sitio de Technical Preview hasta que haya una nueva versión disponible, siempre que después actualice la instalación a otra compatible. Actualice a la versión más reciente disponible y, después, repita el proceso hasta que pueda instalar la versión más reciente de la versión preliminar técnica.

> [!TIP]  
>  Cuando se instala una actualización de versión preliminar técnica, la instalación de versión preliminar se actualiza a la nueva versión preliminar técnica.    Una instalación de versión preliminar técnica nunca dispone de una opción para actualizar a una instalación de rama actual ni recibir actualizaciones de la versión de rama actual.  

**Versiones activas de línea base de Technical Preview:**
   
Puede instalar una versión de base de referencia hasta un año después de su lanzamiento. Sin embargo, al instalar un sitio nuevo de Technical Preview, se recomienda usar la última versión de línea base disponible.
-  **Technical Preview 1711**: la versión Configuration Manager Technical Preview 1711 está disponible como actualización en consola y como versión de base de referencia. Descargue las versiones de base de referencia [desde el centro de evaluación de TechNet](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


##  <a name="BKMK_TPFeedback"></a> Proporcionar comentarios  
 Nos encanta recibir sus comentarios sobre las características de nuestras versiones Technical Preview. Para obtener más información, vea [Comentarios sobre el producto](../understand/find-help.md#product-feedback).

También puede hablarnos sobre las ideas que tenga sobre características nuevas que le gustaría ver. Para enviar nuevas ideas y votar sobre las ideas enviadas por otros usuarios, [visite nuestra página de voz del usuario](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Funcionalidades ofrecidas en la vista preliminar técnica más reciente  
A continuación se enumeran las funcionalidades que ofrece cada versión preliminar técnica de Configuration Manager.  Las funcionalidades que estaban disponibles en una versión anterior de Technical Preview siguen estando disponibles en versiones posteriores. De igual forma, las funcionalidades que se han agregado a la rama actual de Configuration Manager siguen estando disponibles en las versiones de Technical Preview.  Haga clic en el contenido de cada versión preliminar para aprender más acerca de una capacidad específica.  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1802"></a>Technical Preview, versión 1802
- [Transición de la carga de trabajo de Endpoint Protection a Intune mediante la administración conjunta](capabilities-in-technical-preview-1802.md#transition-endpoint-protection-workload-to-intune-using-co-management) <!-- 1357365 -->
- [Configuración de la optimización de distribución de Windows para usar grupos de límites de Configuration Manager](capabilities-in-technical-preview-1802.md#configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups) <!-- 1324696 --> 
- [Secuencia de tareas de actualización en contexto de Windows 10 a través de Cloud Management Gateway](capabilities-in-technical-preview-1802.md#windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway) <!-- 1357149 -->
- [Mejoras en la secuencia de tareas de actualización en contexto de Windows 10](capabilities-in-technical-preview-1802.md#improvements-to-windows-10-in-place-upgrade-task-sequence) <!-- 1357425 --> 
- [Mejoras en los puntos de distribución habilitados con PXE](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) <!-- 1357580 --> 
- [Plantillas de implementación para secuencias de tareas](capabilities-in-technical-preview-1802.md#deployment-templates-for-task-sequences) <!-- 1357391 --> 
- [Panel de ciclo de vida del producto](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) <!--1319632 --> 
- [Mejoras en la creación de informes](capabilities-in-technical-preview-1802.md#improvements-to-reporting) <!--1357653 --> 
- [Mejoras en el Centro de software](capabilities-in-technical-preview-1802.md#improvements-to-software-center) <!--1357592 --> 
- [Mejoras para ejecutar scripts](capabilities-in-technical-preview-1802.md#improvements-to-run-scripts) <!--1236459 --> 
- [Reserva de grupo de límites para puntos de administración](capabilities-in-technical-preview-1802.md#boundary-group-fallback-for-management-points) <!-- 1324594 --> 
- [Mejora de la compatibilidad con certificados CNG](capabilities-in-technical-preview-1802.md#improved-support-for-cng-certificates) <!-- 1357314 --> 
- [Compatibilidad con Cloud Management Gateway para Azure Resource Manager](capabilities-in-technical-preview-1802.md#cloud-management-gateway-support-for-azure-resource-manager) <!-- 1324735 --> 
- [Aprobación de solicitudes de aplicación para los usuarios por dispositivo](capabilities-in-technical-preview-1802.md#approve-application-requests-for-users-per-device) <!-- 1357015 --> 
- [Usar el Centro de software para buscar e instalar aplicaciones disponibles para el usuario en dispositivos unidos a Azure AD](capabilities-in-technical-preview-1802.md#use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices) <!-- 1322613 --> 
- [Información de dispositivo Windows AutoPilot](capabilities-in-technical-preview-1802.md#report-on-windows-autopilot-device-information) <!-- 1351442 --> 
- [Mejoras en las directivas de Configuration Manager para Protección contra vulnerabilidades de seguridad de Windows Defender](capabilities-in-technical-preview-1802.md#improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard) <!-- 1356220 -->
- [Directivas del explorador Microsoft Edge](capabilities-in-technical-preview-1802.md#microsoft-edge-browser-policies) <!-- 1357310 -->
- [Informe sobre la cantidad de exploradores predeterminados](capabilities-in-technical-preview-1802.md#report-for-default-browser-counts) <!-- 1357830 --> 
- [Compatibilidad con dispositivos Windows 10 ARM64](capabilities-in-technical-preview-1802.md#support-for-windows-10-arm64-devices) <!-- 1353704 --> 
- [Cambios en las implementaciones por fases](capabilities-in-technical-preview-1802.md#changes-to-phased-deployments) <!-- 1357405 -->



## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Funcionalidades ofrecidas en Technical Preview recientes admitidas
A continuación se enumeran las funcionalidades ofrecidas en versiones anteriores de Technical Preview de Configuration Manager que todavía se admiten. 

<!-- This is the full list of new features in the past three TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Capacidad |Versión de Technical Preview |Versión de rama actual|  
 |----------------|---------------------|--------------------|
 | Transición de la carga de trabajo de Endpoint Protection a Intune mediante la administración conjunta <!-- 1357365 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#transition-endpoint-protection-workload-to-intune-using-co-management) | [Versión 1802](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune) |  
 | Configuración de la optimización de distribución de Windows para usar grupos de límites de Configuration Manager <!-- 1324696 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups) | [Versión 1802](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization) |  
 | Secuencia de tareas de actualización local de Windows 10 a través de Cloud Management Gateway <!-- 1357149 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway) | [Versión 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg) |  
 | Mejoras en la secuencia de tareas de actualización local de Windows 10 <!-- 1357425 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-windows-10-in-place-upgrade-task-sequence) | [Versión 1802](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system) |  
 | Mejoras en los puntos de distribución habilitados con PXE <!-- 1357580 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | ![Sin agregar](media/Red_X.gif) | 
 | Plantillas de implementación para secuencias de tareas <!-- 1357391 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#deployment-templates-for-task-sequences) | [Versión 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS) |  
 | Panel de ciclo de vida del producto <!--1319632 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | ![Sin agregar](media/Red_X.gif) | 
 | Mejoras en la creación de informes <!--1357653 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-reporting) | [Versión 1802](/sccm/core/servers/manage/list-of-reports#operating-system) |  
 | Mejoras en el Centro de software <!--1357592 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-software-center) | [Versión 1802](/sccm/core/clients/deploy/about-client-settings#BKMK_HideInstalled) |  
 | Reserva de grupo de límites para puntos de administración <!-- 1324594 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#boundary-group-fallback-for-management-points) | [Versión 1802](/sccm/core/servers/deploy/configure/boundary-groups#management-points) |  
 | Mejora de la compatibilidad con certificados CNG <!-- 1357314 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improved-support-for-cng-certificates) | [Versión 1802](/sccm/core/plan-design/network/cng-certificates-overview) |  
 | Compatibilidad con Cloud Management Gateway para Azure Resource Manager <!-- 1324735 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#cloud-management-gateway-support-for-azure-resource-manager) | [Versión 1802](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager) |  
 | Aprobación de solicitudes de aplicación para los usuarios por dispositivo <!-- 1357015 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#approve-application-requests-for-users-per-device) | [Versión 1802](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) |  
 | Uso del Centro de software para buscar e instalar aplicaciones disponibles para el usuario en dispositivos unidos a Azure AD <!-- 1322613 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices) | [Versión 1802](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices) |  
 | Información de dispositivo Windows AutoPilot <!-- 1351442 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#report-on-windows-autopilot-device-information) | [Versión 1802](/sccm/core/clients/manage/co-management-prepare#new-windows-10-devices) |  
 | Mejoras en las directivas de Configuration Manager para Protección contra vulnerabilidades de seguridad de Windows Defender <!-- 1356220 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard) | [Versión 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |  
 | Directivas del explorador Microsoft Edge <!-- 1357310 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#microsoft-edge-browser-policies) | [Versión 1802](/sccm/compliance/deploy-use/browser-profiles) | 
 | Informe sobre la cantidad de exploradores predeterminados <!-- 1357830 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#report-for-default-browser-counts) | [Versión 1802](/sccm/core/servers/manage/list-of-reports#software---companies-and-products) | 
 | Compatibilidad con dispositivos Windows 10 ARM64 <!-- 1353704 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#support-for-windows-10-arm64-devices) | [Versión 1802](/sccm/core/plan-design/configs/support-for-windows-10) |  
 | Creación de implementaciones por fases <!-- 1356837 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#create-phased-deployments) | [Versión 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) |
 | Informes de administración conjunta <!-- 1356648 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#co-management-reporting) | [Versión 1802](\sccm\core\clients\manage\client-management-dashboard) |
 | Mejoras en la programación de evaluación de reglas de implementación automática <!-- 1357133 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-automatic-deployment-rule-evaluation-schedule) | [Versión 1802](/sccm/sum/deploy-use/automatically-deploy-software-updates#BKMK_CreateAutomaticDeploymentRule) |
 | Reasignación de un punto de distribución <!-- 1306937 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#reassign-distribution-point) | [Versión 1802](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_reassign) |
 | Mejoras en el inventario de hardware <!-- 1357389 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-hardware-inventory) | [Versión 1802](/sccm/core/clients/manage/inventory/extend-hardware-inventory#BKMK_GreaterThan255) |
 | Mejoras en la configuración de cliente para el Centro de software <!-- 1355146 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-client-settings-for-software-center) | [Versión 1802](/sccm/core/clients/deploy/about-client-settings#BKMK_HideUnapproved) |
 | Nueva configuración de Protección de aplicaciones de Windows Defender <!-- 1356256 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#new-settings-for-windows-defender-application-guard) | [Versión 1802](/sccm/protect/deploy-use/create-deploy-application-guard-policy#BKMK_HIS) |
 | Mejoras para ejecutar scripts <!-- 1236459 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-run-scripts) | [Versión 1802](/sccm/apps/deploy-use/create-deploy-scripts) |
 | No actualizar automáticamente las aplicaciones reemplazadas <!-- 1351266 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#do-not-automatically-upgrade-superseded-applications) | [Versión 1802](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) | 
 | Instalación de varias aplicaciones en el Centro de software <!-- 1357126 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#install-multiple-applications-in-software-center) | [Versión 1802](/sccm/core/understand/software-center#install-multiple-applications) |
 | Servicio del respondedor PXE basado en cliente <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) | ![Sin agregar](media/Red_X.gif) |
 | Cambio en la instalación del cliente de Configuration Manager <!-- 1356195 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-in-the-configuration-manager-client-install) | [Versión 1802](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.#BKMK_ExternalDependencies) | 
 | Cambio en el panel de dispositivos Surface <!-- 1355788 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-to-the-surface-device-dashboard) | [Versión 1802](/sccm/core/clients/manage/surface-device-dashboard) | 
 | Mejoras en el panel de administración de clientes de Office 365 <!-- 1357281 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-office-365-client-management-dashboard) | [Versión 1802](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard) | 
 | Mejoras en la consola de Configuration Manager <!-- 1357280,1357282 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-the-configuration-manager-console) | Versión 1802 | 
 | Mejoras en la implementación del sistema operativo <!-- SMS 500897 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-operating-system-deployment) | Versión 1802 | 
 | Ejecutar paso de secuencia de tareas <!-- 1261338 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) | [Versión 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |
 | Permitir la interacción del usuario al instalar aplicaciones como <!-- 1356976 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) | [Versión 1802](/sccm/apps/deploy-use/create-applications#specify-user-experience-options-for-the-deployment-type) |

  

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Funcionalidades ofrecidas en anteriores versiones preliminares técnicas
A continuación se enumeran las funcionalidades específicas ofrecidas en versiones anteriores de Technical Preview de Configuration Manager. Estas funcionalidades siguen estando disponibles en versiones posteriores, pero todavía no están disponibles en una versión de rama actual. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |Capacidad |Versión de Technical Preview |  
 |----------------|---------------------|
 |Experiencia mejorada del perfil VPN en la consola de Configuration Manager <!-- 1313282 --> | [Tech Preview 1709](capabilities-in-technical-preview-1709.md) |
 |Información de administración <!-- 1353967 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#management-insights)|
 |Panel de dispositivos Surface <!-- 1355788 --> |[Tech Preview 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|
 |Alta disponibilidad del rol del servidor de sitio <!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |Compatibilidad con el arranque de red de PXE para IPv6 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Evaluación de Atestación de estado de dispositivo para las directivas de cumplimiento de acceso condicional <!-- 1235616 -->|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|
 |Uso de Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Evaluación del cumplimiento para actualizaciones de Windows Update para empresas <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |Acceso a datos de punto de conexión de OData <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |Mejoras en Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |Los usuarios finales pueden instalar aplicaciones desde el Portal de empresa <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>Véase también  
[Novedades de System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introducción a System Center Configuration Manager](../../core/understand/introduction.md)
