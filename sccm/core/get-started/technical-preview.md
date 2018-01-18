---
title: Versiones de Technical Preview
titleSuffix: Configuration Manager
description: "Obtenga información sobre la versión Technical Preview que le permite probar nuevas funcionalidades y capacidades de System Center Configuration Manager."
ms.custom: na
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: "157"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 692cf74cbae3f176bab254aeec0e63c10929cfcc
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/04/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Technical Preview)*

**Le damos la bienvenida a System Center Configuration Manager Technical Preview**. En este artículo se proporcionan detalles sobre la versión preliminar en evolución que presenta nuevas funcionalidades y características en las que estamos trabajando. En cada nueva versión preliminar técnica se presentan nuevas características que no se incluyeron en la rama actual de Configuration Manager cuando se puso a disposición la versión preliminar técnica. Estas características podrían incluirse finalmente en una actualización de la versión actual de la rama, pero antes de finalizarlas y agregarlas, queremos que tenga la oportunidad de probarlas y enviarnos sus comentarios.  

 Puesto que esta es una versión preliminar técnica, los detalles y las funcionalidades están sujetos a cambios.  

 Este artículo contiene información que se aplica a todas las versiones de Technical Preview. También se muestra cada nueva funcionalidad (o característica) junto con la versión de Technical Preview en la que aparece por primera vez, como la versión 1712 para diciembre de 2017. Estas características se detallan en temas independientes dedicados a cada versión preliminar.  

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

-   No se admite la actualización a una versión de producción (rama actual) desde esta versión preliminar. En cambio, cuando haya actualizaciones disponibles para una versión preliminar, puede buscarlas e instalarlas desde el nodo **Actualizaciones y mantenimiento** de la consola de Configuration Manager. Para ver un vídeo del proceso de actualización en la consola, consulte [Installing ConfigMgr Update Package (Instalación de paquetes de actualización de Configuration Manager)](https://www.youtube.com/embed/KBd_EGFbUT8) en youtube.com.  
-   Solo se admite un sitio primario independiente. No se admiten sitios de administración central, varios sitios primarios ni sitios secundarios.  

Los siguientes productos y tecnologías son compatibles con esta rama de Configuration Manager. Sin embargo, su inclusión en este contenido no implica una extensión de la compatibilidad con cualquier producto o versión más allá del ciclo de vida de soporte individual de los productos. Los productos que están fuera de su ciclo de vida de soporte no se pueden usar con Configuration Manager. Para obtener más información sobre los ciclos de vida de soporte de Microsoft, visite el sitio web [Ciclo de vida de soporte de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270).  

-   Solo se admiten las siguientes versiones de SQL Server:  

    -   SQL Server 2016 (sin ningún Service Pack, y versiones posteriores)
    -   SQL Server 2014 (con Service Pack 1, o versiones posteriores)
    -   SQL Server 2012 (con Service Pack 3, o versiones posteriores)


-   El sitio admite hasta 10 clientes, que deben ejecutar una de las siguientes versiones de Windows:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 8  
      -   Windows 7  

##  <a name="bkmk_install"></a> Instalar y actualizar la versión Technical Preview  
 System Center Configuration Manager Technical Preview es diferente de la versión actual de System Center Configuration Manager.  

 Para usar la versión preliminar técnica, primero debe instalar una **versión de base de referencia** de la compilación de dicha versión. Después de instalar una versión de línea base, podrá usar las **actualizaciones en consola** para que la instalación cuente con la versión preliminar más reciente. Normalmente, las nuevas versiones de Technical Preview están disponibles cada mes.

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

### <a name="technical-preview-version-1712"></a>Technical Preview versión 1712
- [No actualizar automáticamente las aplicaciones reemplazadas](capabilities-in-technical-preview-1712.md#do-not-automatically-upgrade-superseded-applications) <!-- 1351266 --> 
- [Instalar varias aplicaciones en el Centro de software](capabilities-in-technical-preview-1712.md#install-multiple-applications-in-software-center) <!-- 1357126 --> 
- [Cambio en la instalación del cliente de Configuration Manager](capabilities-in-technical-preview-1712.md#change-in-the-configuration-manager-client-install) <!-- 1356195 --> 
- [Cambio en el panel de dispositivos Surface](capabilities-in-technical-preview-1712.md#change-to-the-surface-device-dashboard) <!-- 1355788 --> 
- [Mejoras en el panel de administración de clientes de Office 365](capabilities-in-technical-preview-1712.md#improvements-to-office-365-client-management-dashboard) <!-- 1357281 --> 
- [Mejoras en la consola de Configuration Manager](capabilities-in-technical-preview-1712.md#improvements-to-the-configuration-manager-console) <!-- 1357280,1357282 --> 
- [Mejoras en la implementación de sistema operativo](capabilities-in-technical-preview-1712.md#improvements-to-operating-system-deployment) <!-- SMS 500897 --> 
- [Integración de la aplicación Centro de opiniones de Windows 10](capabilities-in-technical-preview-1712.md#windows-10-feedback-hub-app-integration) <!-- NA -->




## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Funcionalidades ofrecidas en Technical Preview recientes admitidas
A continuación se enumeran las funcionalidades ofrecidas en versiones anteriores de Technical Preview de Configuration Manager que todavía se admiten. 

<!-- This is the full list of new features in the past three TP releases. Each month, add features from the list above to the top of this table. Then remove the bottom of this list (and/or move individual items not in CB to the third table below). -->

 |Capacidad |Versión de Technical Preview |Versión de rama actual|  
 |----------------|---------------------|--------------------|
 |Ejecutar paso de secuencia de tareas <!-- 1261338 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |[Versión 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence)    |
 |Permitir la interacción del usuario al instalar aplicaciones como <!-- 1356976 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |![Sin agregar](media/Red_X.gif)    |
 |Telemetría de Windows 10 para el estado de dispositivos de Windows Analytics<!--1356148 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health) |[Versión 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#reporting)    |
 |Mejoras de los iconos del Centro de software<!-- 1356194 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#software-center-no-longer-distorts-icons-larger-than-250x250) |[Versión 1710](/sccm/apps/plan-design/plan-for-and-configure-application-management#supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center)    |
 |Comprobación del cumplimiento del Centro de software en dispositivos administrados conjuntamente<!-- 1356374 -->|[Tech Preview 1710](capabilities-in-technical-preview-1710.md#check-compliance-from-software-center-for-co-managed-devices)|[Versión 1710](/sccm/core/clients/manage/co-management-overview)    |
 |Compatibilidad limitada con certificados CNG<!-- 1356191 -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md#limited-support-for-cng-certificates)|[Versión 1710](/sccm/core/plan-design/network/cng-certificates-overview)    |
 |Compatibilidad con la Protección contra vulnerabilidades de seguridad<!--1355468 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#support-for-exploit-guard) |[Versión 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)    |
 |Descripciones mejoradas para reinicios de equipo pendientes <!-- 1356283  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[Versión 1710](/sccm/core/clients/manage/manage-clients)    |
 |Cambios en la directiva de Device Guard <!-- 1355092  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[Versión 1710](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)    |
 |Configuración e implementación de directivas de Protección de aplicaciones de Windows Defender <!-- 1351960  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[Versión 1710](/sccm/protect/deploy-use/create-deploy-application-guard-policy)    |
 |Mejoras en la implementación de scripts de PowerShell desde Configuration Manager <!-- 1236459 -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md#improvements-for-deploying-powershell-scripts-from-configuration-manager) | [Versión 1710](/sccm/apps/deploy-use/create-deploy-scripts)
 |Experiencia mejorada del perfil VPN en la consola de Configuration Manager <!-- 1313282 --> | [Tech Preview 1709](capabilities-in-technical-preview-1709.md) |[Versión 1710](/sccm/protect/deploy-use/create-vpn-profiles)    |
 |Administración conjunta para dispositivos de Windows 10|[Tech Preview 1709](capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices)|[Versión 1710](/sccm/core/clients/manage/co-management-overview.md)|
 

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Funcionalidades ofrecidas en anteriores versiones preliminares técnicas
A continuación se enumeran las funcionalidades específicas ofrecidas en versiones anteriores de Technical Preview de Configuration Manager. Estas funcionalidades siguen estando disponibles en versiones posteriores, pero todavía no están disponibles en una versión de rama actual. 

<!-- This is the list of individual features that are still in TP (not in CB). Note there is no third column in this table! Each month review and remove from this list for anything that's now available in CB. Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column) -->

 |Capacidad |Versión de Technical Preview |  
 |----------------|---------------------|
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
