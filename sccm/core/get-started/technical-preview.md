---
title: Versiones de Technical Preview
titleSuffix: Configuration Manager
description: Obtenga información sobre la versión Technical Preview para probar nuevas funcionalidades y capacidades de Configuration Manager.
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1fd848c3e0ed663e0731eb86d39c930db3af7819
ms.sourcegitcommit: d1bf26bcf0d78b37ac7598fab36eb58ca69b1dc5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37066290"
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Technical Preview)*

**Le damos la bienvenida a System Center Configuration Manager Technical Preview**. En este artículo se proporcionan detalles sobre la versión preliminar en evolución que presenta nuevas funcionalidades y características en las que estamos trabajando. En cada nueva versión preliminar técnica se presentan nuevas características que no se incluyeron en la rama actual de Configuration Manager cuando se puso a disposición la versión preliminar técnica. Estas características podrían incluirse finalmente en una actualización de la versión actual de la rama, pero antes de finalizarlas y agregarlas, queremos que tenga la oportunidad de probarlas y enviarnos sus comentarios.  

 Como esta es una versión preliminar técnica, los detalles y las funcionalidades están sujetos a cambios.  

 Este artículo contiene información que se aplica a todas las versiones de Technical Preview. También se muestran las nuevas capacidades (o características) junto con la versión de Technical Preview en las que aparecen por primera vez, como la versión 1806 de junio de 2018. Estas características se detallan en temas independientes dedicados a cada versión preliminar.  

 Para obtener más información sobre las novedades en la rama actual de Configuration Manager, consulte [Novedades de System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requisitos y limitaciones de Technical Preview  

> [!IMPORTANT]     
>  La versión Technical Preview solo tiene licencia para su uso en un entorno de laboratorio. Es posible que Microsoft no proporcione servicios de soporte técnico y que algunas características no estén disponibles en el software de versión preliminar. Además, es posible que el software de versión preliminar tenga estándares de seguridad, privacidad, accesibilidad, disponibilidad y confiabilidad reducidos o diferentes a los del software proporcionado comercialmente.  

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

Los siguientes productos y tecnologías son compatibles con esta rama de Configuration Manager. Sin embargo, su inclusión en este contenido no implica una extensión de la compatibilidad con cualquier producto o versión más allá del ciclo de vida de soporte individual de los productos. Los productos que están fuera de su ciclo de vida de soporte no se pueden usar con Configuration Manager. Para obtener más información sobre los ciclos de vida de soporte de Microsoft, visite el sitio web [Ciclo de vida de soporte de Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270).  

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
>  Cuando se instala una actualización de versión preliminar técnica, la instalación de versión preliminar se actualiza a la nueva versión preliminar técnica. Una instalación de versión preliminar técnica nunca dispone de una opción para actualizar a una instalación de rama actual ni recibir actualizaciones de la versión de rama actual.  

**Versiones activas de línea base de Technical Preview:**
   
Puede instalar una versión de base de referencia hasta un año después de su lanzamiento. Sin embargo, al instalar un sitio nuevo de Technical Preview, se recomienda usar la última versión de línea base disponible.
-  **Technical Preview 1806**: la versión Configuration Manager Technical Preview 1806 está disponible como actualización en la consola y como nueva versión de línea base. Descargue las versiones de base de referencia [desde el centro de evaluación de TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


##  <a name="BKMK_TPFeedback"></a> Proporcionar comentarios  
 Nos encanta recibir sus comentarios sobre las características de nuestras versiones Technical Preview. Para obtener más información, vea [Comentarios sobre el producto](../understand/find-help.md#product-feedback).

También puede hablarnos sobre las ideas que tenga sobre características nuevas que le gustaría ver. Para enviar nuevas ideas y votar sobre las ideas enviadas por otros usuarios, [visite nuestra página de voz del usuario](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Funcionalidades ofrecidas en la vista preliminar técnica más reciente  
A continuación se enumeran las funcionalidades que ofrece cada versión preliminar técnica de Configuration Manager. Las funcionalidades que estaban disponibles en una versión anterior de Technical Preview siguen estando disponibles en versiones posteriores. De igual forma, las funcionalidades que se han agregado a la rama actual de Configuration Manager siguen estando disponibles en las versiones de Technical Preview. Haga clic en el contenido de cada versión preliminar para aprender más acerca de una capacidad específica.  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-18062"></a>Technical Preview, versión 1806.2
- [Mejoras en las implementaciones por fases](capabilities-in-technical-preview-1806-2.md#bkmk_pod) <!--1358577,1358147,1358578-->
- [Compatibilidad con nuevos formatos de paquete de aplicaciones de Windows](capabilities-in-technical-preview-1806-2.md#bkmk_msix) <!--1357427-->
- [Mejora de seguridad de inserción de cliente](capabilities-in-technical-preview-1806-2.md#bkmk_client-push) <!--1358204-->
- [Información de administración para un mantenimiento proactivo](capabilities-in-technical-preview-1806-2.md#bkmk_insights) <!--1352184,et al-->
- [Carga de trabajo de aplicaciones móviles de transición para los dispositivos administrados conjuntamente](capabilities-in-technical-preview-1806-2.md#bkmk_comgmt) <!--1357892-->
- [Opciones de grupo de límites para descargas del mismo nivel](capabilities-in-technical-preview-1806-2.md#bkmk_bgoptions) <!--1356193-->
- [Soporte técnico de actualizaciones de software de terceros para catálogos personalizados](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate) <!--1358714-->
- [Mejoras de las características de administración en la nube](capabilities-in-technical-preview-1806-2.md#bkmk_cloud) <!--511980,515854-->
- [Informe de cumplimiento de nuevas actualizaciones de software](capabilities-in-technical-preview-1806-2.md#bkmk_report) <!--1357775-->



## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Funcionalidades ofrecidas en Technical Preview recientes admitidas
A continuación se enumeran las funcionalidades ofrecidas en versiones anteriores de Technical Preview de Configuration Manager que todavía se admiten. 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Capacidad |Versión de Technical Preview |Versión de rama actual|  
 |----------------|---------------------|--------------------|
 | Actualizaciones de software de terceros <!--1352101--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate)  | ![Sin agregar](media/Red_X.gif) |  
 | Configurar SmartScreen de Windows Defender para Microsoft Edge <!--1353701--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#configure-windows-defender-smartscreen-settings-for-microsoft-edge)  | ![Sin agregar](media/Red_X.gif) |  
 | Sincronizar directiva MDM desde Microsoft Intune para un dispositivo administrado conjuntamente <!--1357377--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device)  | ![Sin agregar](media/Red_X.gif) |  
 | Transición de la carga de trabajo de Office 365 a Intune mediante la administración conjunta <!--1357841--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#transition-office-365-workload-to-intune-using-co-management)  | ![Sin agregar](media/Red_X.gif) |  
 | Package Conversion Manager <!--1357861--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#package-conversion-manager)  | ![Sin agregar](media/Red_X.gif) |  
 | Implementar actualizaciones de software sin contenido <!--1357933--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#deploy-software-updates-without-content)  | ![Sin agregar](media/Red_X.gif) |  
 | Integración de la Herramienta de personalización de Office en el instalador de Office 365 <!--1358149--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#office-customization-tool-integration-with-the-office-365-installer)  | ![Sin agregar](media/Red_X.gif) |  
 | Mejoras en Cloud Management Gateway <!--1358215,1358651,503899--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-cloud-management-gateway)   | ![Sin agregar](media/Red_X.gif) |  
 | Mejoras en las comunicaciones de cliente seguras <!--1358278,1358279--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-secure-client-communications)  | ![Sin agregar](media/Red_X.gif) |  
 | Mejoras de la infraestructura del Centro de software <!--1358309--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#software-center-infrastructure-improvements)  | ![Sin agregar](media/Red_X.gif) |  
 | Aprovisionar los paquetes de aplicación de Windows para todos los usuarios en un dispositivo <!--1358310--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#provision-windows-app-packages-for-all-users-on-a-device)  | ![Sin agregar](media/Red_X.gif) |  
 | Mejoras en el panel de Surface <!--1358654--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-the-surface-dashboard)  | ![Sin agregar](media/Red_X.gif) |  
 | Revisión de unidad predeterminada de inventario de hardware <!--514442--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#hardware-inventory-default-unit-revision)  | ![Sin agregar](media/Red_X.gif) |  
 | Creación de una implementación por fases con fases configuradas manualmente para una secuencia de tareas <!--1358148--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence)  | ![Sin agregar](media/Red_X.gif) |  
 | Compatibilidad con puntos de distribución de nube para Azure Resource Manager <!--1322209--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  | ![Sin agregar](media/Red_X.gif) |  
 | Realización de acciones basadas en la información de administración <!--1357930--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#take-actions-based-on-management-insights)  | ![Sin agregar](media/Red_X.gif) |  
 | Transición de la carga de trabajo de la configuración del dispositivo a Intune mediante la administración conjunta <!--1357903--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#transition-device-configuration-workload-to-intune-using-co-management)  | ![Sin agregar](media/Red_X.gif) |  
 | Habilitación de los puntos de distribución para usar el control de congestión de red <!--1358112--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#enable-distribution-points-to-use-network-congestion-control)  | ![Sin agregar](media/Red_X.gif) |  
 | Panel de administración en la nube <!--1358461--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-management-dashboard)  | ![Sin agregar](media/Red_X.gif) |  
 | CMPivot <!--1358456--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmpivot)  | ![Sin agregar](media/Red_X.gif) |  
 | Comunicaciones de cliente seguras mejoradas <!--1356889,1358228,1358460--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)  | ![Sin agregar](media/Red_X.gif) |  
 | Mejoras para habilitar la compatibilidad de actualización de software de terceros <!--1357605--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)  | ![Sin agregar](media/Red_X.gif) |  
 | Mejoras en la secuencia de tareas de actualización local de Windows 10 <!--1358500--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-windows-10-in-place-upgrade-task-sequence)  | ![Sin agregar](media/Red_X.gif) |  
 | Herramienta CMTrace instalada con el cliente <!--1357971--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmtrace-installed-with-client)  | ![Sin agregar](media/Red_X.gif) |  
 | Mejora en la consola de Configuration Manager <!--1358202--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-the-configuration-manager-console)  | ![Sin agregar](media/Red_X.gif) |  
 | Mejoras en los comentarios de la consola <!--1357542--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-console-feedback)  | ![Sin agregar](media/Red_X.gif) |  
 | Mejoras en los puntos de distribución habilitados con PXE <!--1357580--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-pxe-enabled-distribution-points)  | ![Sin agregar](media/Red_X.gif) |  
 | Mejora en el inventario de hardware para los valores enteros grandes <!--1357880--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)  | ![Sin agregar](media/Red_X.gif) |  
 | Mejora en el mantenimiento de WSUS <!--1357898--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-wsus-maintenance)  | ![Sin agregar](media/Red_X.gif) |  
 | Mejora en la compatibilidad con certificados CNG <!--1357314--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-support-for-cng-certificates)  | ![Sin agregar](media/Red_X.gif) |  
| Configuración de una biblioteca de contenido remoto para el servidor de sitio <!--1357525--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server)  | ![Sin agregar](media/Red_X.gif) | 
 | Envío de comentarios desde la consola de Configuration Manager <!--1357542--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#bkmk_feedback)  | ![Sin agregar](media/Red_X.gif) | 
 | Centro de soporte técnico <!--1357489--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#support-center)  | ![Sin agregar](media/Red_X.gif) | 
 | Kit de herramientas de Configuration Manager <!--1357145--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configuration-manager-toolkit)  | ![Sin agregar](media/Red_X.gif) | 
 | Desinstalación de aplicaciones al revocarse la aprobación <!--1357891--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#uninstall-application-on-approval-revocation)  | ![Sin agregar](media/Red_X.gif) | 
 | Exclusión de contenedores de Active Directory de la detección <!--1358143--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#exclude-active-directory-containers-from-discovery)  | ![Sin agregar](media/Red_X.gif) | 
 | Especificación de la visibilidad del vínculo al sitio web del catálogo de aplicaciones en el Centro de software <!--1358214--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#specify-the-visibility-of-the-application-catalog-website-link-in-software-center)  | ![Sin agregar](media/Red_X.gif) | 
 | Filtrado de las reglas de implementación automáticas por arquitectura de actualización de software <!--1322266--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#filter-automatic-deployment-rules-by-software-update-architecture)  | ![Sin agregar](media/Red_X.gif) | 
 | Mejoras en la implementación del sistema operativo <!--1358330,1358493--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#improvements-to-os-deployment) | ![Sin agregar](media/Red_X.gif) | 
 | Compatibilidad de puntos de distribución de extracción con puntos de distribución de nube como orígenes<!--1321554--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source)  | ![Sin agregar](media/Red_X.gif) | 
 | Compatibilidad de descarga parcial en la memoria caché del mismo nivel de cliente para reducir la utilización de la WAN <!--1357346--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization)  | ![Sin agregar](media/Red_X.gif) | 
 | Ventanas de mantenimiento en el Centro de software <!--1358131--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center)  | ![Sin agregar](media/Red_X.gif) | 
 | Pestaña Personalizado de la página web del Centro de software <!--1358132--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center)  | ![Sin agregar](media/Red_X.gif) | 
 | Habilitación de la compatibilidad con actualizaciones de software de terceros en clientes <!--1357605--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients)  | ![Sin agregar](media/Red_X.gif) | 
 | Habilitación del copiado y pegado de detalles de recursos desde vistas de supervisión <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views)  | ![Sin agregar](media/Red_X.gif) | 
 | Extensiones SCAP <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#scap-extensions)  | ![Sin agregar](media/Red_X.gif) | 
 
  

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Funcionalidades ofrecidas en anteriores versiones preliminares técnicas
A continuación se enumeran las funcionalidades específicas ofrecidas en versiones anteriores de Technical Preview de Configuration Manager. Estas funcionalidades siguen estando disponibles en versiones posteriores, pero todavía no están disponibles en una versión de rama actual. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |Capacidad |Versión de Technical Preview |  
 |----------------|---------------------|
 | Mejoras en los puntos de distribución habilitados con PXE <!-- 1357580 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | 
 | Panel de ciclo de vida del producto <!--1319632 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | 
 | Servicio del respondedor PXE basado en cliente <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
 |Alta disponibilidad del rol del servidor de sitio <!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |Compatibilidad con el arranque de red de PXE para IPv6 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Uso de Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Evaluación del cumplimiento para actualizaciones de Windows Update para empresas <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |Acceso a datos de punto de conexión de OData <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |Mejoras en Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |Los usuarios finales pueden instalar aplicaciones desde el Portal de empresa <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>Véase también  
[Novedades de System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introducción a System Center Configuration Manager](../../core/understand/introduction.md)

> [!Tip]  
> Para más información sobre las características de la rama actual que requieren consentimiento, consulte las [características de versión preliminar](/sccm/core/servers/manage/pre-release-features).  
> Para más información sobre las características de la rama actual que se deben habilitar primero, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

