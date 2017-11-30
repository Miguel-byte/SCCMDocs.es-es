---
title: Versiones de Technical Preview
titleSuffix: Configuration Manager
description: "Obtenga información sobre la versión Technical Preview que le permite probar nuevas funcionalidades y capacidades de System Center Configuration Manager."
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: "157"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: c03581ba5d582d6b86f17c7ec34c3e6e0e8d627e
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Technical Preview)*

**Le damos la bienvenida a System Center Configuration Manager Technical Preview**. Este tema proporciona detalles acerca de la versión preliminar en evolución que presenta nuevas funcionalidades y capacidades en las que estamos trabajando. Con cada nueva versión preliminar técnica se presentan nuevas características que no se han incluido aún en la rama actual de System Center Configuration Manager cuando se pone a disposición la versión preliminar técnica. Estas características podrían incluirse finalmente en una actualización de la versión actual de la rama, pero antes de finalizarlas y agregarlas, queremos que tenga la oportunidad de probarlas y enviarnos sus comentarios.  

 Puesto que esta es una versión preliminar técnica, los detalles y las funcionalidades están sujetos a cambios.  

 Este tema contiene información que afecta a todas las versiones de Technical Preview y enumera todas las nuevas funciones (o características), junto con la versión de Technical Preview en la que la función aparece por primera vez, como la versión 1710 para octubre de 2017. Los detalles de estas capacidades se proporcionan en otros temas dedicados a cada versión preliminar.  

 Para obtener más información sobre las novedades en la rama actual de Configuration Manager, consulte [Novedades de System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requisitos y limitaciones de Technical Preview  

> [!IMPORTANT]     
>  La versión Technical Preview solo tiene licencia para su uso en un entorno de laboratorio.  Es posible que Microsoft no proporcione servicios de soporte técnico y que algunas características no estén disponibles en el software de versión preliminar. Además, es posible que el software de versión preliminar tenga unos estándares de seguridad, privacidad, accesibilidad, disponibilidad y confiabilidad reducidos o diferentes a los del software proporcionado comercialmente.  

 Para la mayoría de requisitos previos del producto, use la información que aparece en [Configuraciones admitidas para System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). Las excepciones siguientes se aplican a las versiones Technical Preview:  

-   Todas las instalaciones permanecen activas durante 90 días y luego cambian a inactivas.  

-   El único idioma admitido es el inglés.


-   Solo se admiten los siguientes indicadores de instalación (conmutadores):  

    -   **/silent**  
    -   **/testdbupgrade**    


-   De forma predeterminada, al usar Technical Preview, el punto de conexión de servicio se establece en el modo en línea cuando se instala y no se admite el cambio al modo sin conexión.

-   Cuando proceda, se incluyen limitaciones o requisitos adicionales con los detalles de cada versión específica de Technical Preview  

-   No se admite la migración a esta versión preliminar o desde ella.  

-   No se admite la actualización a esta versión preliminar.  

-   No se admite la actualización a una versión de producción (rama actual) desde esta versión preliminar. En cambio, cuando haya actualizaciones disponibles para una versión preliminar, puede buscarlas e instalarlas desde el nodo **Actualizaciones y mantenimiento** de la consola de Configuration Manager. Para ver un vídeo del proceso de actualización en la consola, consulte [Installing ConfigMgr Update Package (Instalación de paquetes de actualización de Configuration Manager)](https://www.youtube.com/embed/KBd_EGFbUT8) en youtube.com.  
-   Solo se admite un sitio primario independiente. No se admiten sitios de administración central, varios sitios primarios ni sitios secundarios.  

Los siguientes productos y tecnologías son compatibles con esta rama de Configuration Manager. Sin embargo, su inclusión en este contenido no implica una extensión de la compatibilidad con cualquier producto o versión más allá del ciclo de vida de soporte individual de los productos. Los productos que están fuera de su ciclo de vida de soporte no se pueden usar con Configuration Manager. Para obtener más información sobre los ciclos de vida de soporte de Microsoft, visite el sitio web [Ciclo de vida de soporte de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270).  

-   Solo se admiten las siguientes versiones de SQL Server:  

    -   SQL Server 2016 (sin ningún Service Pack, y versiones posteriores)
    -   SQL Server 2014 (con Service Pack 1, o versiones posteriores)
    -   SQL Server 2012 (con Service Pack 3, o versiones posteriores)


-   El sitio admite hasta 10 clientes, que deben ejecutar una de las siguientes opciones:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 8  
      -   Windows 7  

##  <a name="bkmk_install"></a> Instalar y actualizar la versión Technical Preview  
 System Center Configuration Manager Technical Preview es diferente de la versión actual de System Center Configuration Manager.  

 Para usar la versión preliminar técnica, primero debe instalar una **versión de línea base** de la compilación de dicha versión. Después de instalar una versión de línea base, podrá usar las **actualizaciones en consola** para que la instalación cuente con la versión preliminar más reciente. Normalmente, las nuevas versiones de Technical Preview están disponibles cada mes.

Cada versión preliminar se admite hasta que tres versiones sucesivas están disponibles. Es decir, cuando se presente la versión 1708, la versión 1704 ya no se admitirá, pero las versiones 1705, 1706 y 1707 seguirán admitiéndose. Si una línea base deja de ser compatible, como en el caso de la versión 1703, todavía se admitirá para instalar un nuevo sitio de Technical Preview hasta que haya una nueva versión disponible, siempre que después actualice la instalación a otra compatible. Al actualizar, si no ve la última versión compatible en la consola, actualice a la última disponible y, luego, repita el proceso hasta que pueda instalar la más reciente de Technical Preview.

> [!TIP]  
>  Cuando se instala una actualización de versión preliminar técnica, la instalación de versión preliminar se actualiza a la nueva versión preliminar técnica.    Una instalación de versión preliminar técnica nunca dispone de una opción para actualizar a una instalación de rama actual ni recibir actualizaciones de la versión de rama actual.  

**Versiones activas de línea base de Technical Preview:**  
Puede instalar una versión de línea base hasta 1 año después de su lanzamiento. Sin embargo, al instalar un sitio nuevo de Technical Preview, se recomienda usar la última versión de línea base disponible.
-  **Technical Preview 1711**: la versión Configuration Manager Technical Preview 1711 está disponible como actualización en consola para Configuration Manager Technical Preview y como nueva versión de base de referencia, [disponible en el sitio web TechNet Evaluation Center](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).
-  **Technical Preview 1703**: la versión Configuration Manager Technical Preview 1703 estaba disponible como actualización en consola para Configuration Manager Technical Preview y como versión de línea base. Si va a instalar una nueva línea base, se recomienda usar la versión 1711.


##  <a name="BKMK_TPFeedback"></a> Proporcionar comentarios  
 Deseamos recibir sus comentarios sobre nuestras versiones Technical Preview. Para enviar comentarios sobre las funcionalidades de cada versión preliminar, siga el vínculo a nuestro formulario de comentarios en la página del [programa de comentarios de Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) en el sitio de Microsoft Connect.  

 También puede hablarnos de cualquier característica nueva que le gustaría ver. Para enviar nuevas ideas y votar sobre las ideas enviadas por otros usuarios, [visite nuestra página de voz del usuario](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Funcionalidades ofrecidas en la vista preliminar técnica más reciente  
A continuación se enumeran las capacidades que ofrece cada versión preliminar técnica de Configuration Manager.  Las capacidades que están disponibles a partir de una versión preliminar técnica siguen estando disponibles en versiones posteriores. De igual forma, las capacidades que se han agregado a System Center Configuration Manager Release (rama actual) siguen estando disponibles en las versiones preliminares técnicas posteriores.  Haga clic en el contenido de cada versión preliminar para aprender más acerca de una capacidad específica.  

 |Capacidad |Versión de Technical Preview |Versión de rama actual|  
 |----------------|---------------------|--------------------|
 |Mejoras para ejecutar el paso de secuencia de tareas <!-- 1261338 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |![Sin agregar](media/Red_X.gif)    |
 |Permitir la interacción del usuario al instalar aplicaciones como <!-- 1356976 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |![Sin agregar](media/Red_X.gif)    |
 |Nuevas directivas de cumplimiento para Windows 10 <!-- 1356976 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md#new-compliance-policy-options-for-windows-10) |![Sin agregar](media/Red_X.gif)    |


## <a name="capabilities-delivered-in-previous-technical-previews"></a>Funcionalidades ofrecidas en anteriores versiones preliminares técnicas
 Cuando todas las características de una versión preliminar técnica estén disponibles en la versión mínima admitida de la Rama actual, los detalles de esa versión preliminar se quitan de esta tabla siguiente.  

 |Capacidad |Versión de Technical Preview |Versión de rama actual|  
 |----------------|---------------------|--------------------|
 |Telemetría de Windows 10 para el estado de dispositivos de Windows Analytics<!--1356148 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health) |![Sin agregar](media/Red_X.gif)    |
 |Mejoras de los iconos del Centro de software<!-- 1356194 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#software-center-no-longer-distorts-icons-larger-than-250x250) |![Sin agregar](media/Red_X.gif)    |
 |Comprobación del cumplimiento del Centro de software en dispositivos administrados conjuntamente<!-- 1356374 -->|[Tech Preview 1710](capabilities-in-technical-preview-1710.md#check-compliance-from-software-center-for-co-managed-devices)|![Sin agregar](media/Red_X.gif)    |
 |Compatibilidad limitada con certificados CNG<!-- 1356191 -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md#limited-support-for-cng-certificates)|![Sin agregar](media/Red_X.gif)    |
 |Compatibilidad con la Protección contra vulnerabilidades de seguridad<!--1355468 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#support-for-exploit-guard) |[Versión 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)    |
 |Descripciones mejoradas para reinicios de equipo pendientes <!-- 1356283  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[Versión 1710](/sccm/core/clients/manage/manage-clients)    |
 |Cambios en la directiva de Device Guard <!-- 1355092  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[Versión 1710](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)    |
 |Configuración e implementación de directivas de Protección de aplicaciones de Windows Defender <!-- 1351960  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[Versión 1710](/sccm/protect/deploy-use/create-deploy-application-guard-policy)    |
 |Mejoras en la implementación de scripts de PowerShell desde Configuration Manager <!-- 1236459 -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md#improvements-for-deploying-powershell-scripts-from-configuration-manager) | [Versión 1710](/sccm/apps/deploy-use/create-deploy-scripts)

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Funcionalidades ofrecidas en anteriores versiones preliminares técnicas
 Cuando todas las características de una versión preliminar técnica estén disponibles en la versión mínima admitida de la Rama actual, los detalles de esa versión preliminar se quitan de esta tabla siguiente.  

 |Capacidad |Versión de Technical Preview |Versión de rama actual|  
 |----------------|---------------------|--------------------|
 |Experiencia mejorada del perfil VPN en la consola de Configuration Manager <!-- 1313282 --> | [Tech Preview 1709](capabilities-in-technical-preview-1709.md) |![Sin agregar](media/Red_X.gif)    |
 |Administración conjunta para dispositivos de Windows 10|[Tech Preview 1709](capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices)|[Versión 1710](/sccm/core/clients/manage/co-management-overview.md)|
 |Mejora para especificar parámetros de script al implementar scripts de PowerShell desde Configuration Manager <!-- 1236459 -->|[Tech Preview 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)|[Versión 1710](/sccm/apps/deploy-use/create-deploy-scripts)|
 |Información de administración <!-- 1353967 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#management-insights)|![Sin agregar](media/Red_X.gif)|
 |Reinicio de equipos desde la consola de Configuration Manager <!-- 1356283 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console)|[Versión 1710](/sccm/core/clients/manage/manage-clients) |
 |Personalización del Centro de software <!-- 1351224 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#software-center-customization)|![Sin agregar](media/Red_X.gif)|
|Compatibilidad con la caché del mismo nivel de cliente para archivos de instalación rápida en Windows 10 y Office 365|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365)|[Versión 1706](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache)|
 |Panel de Surface Device|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|![Sin agregar](media/Red_X.gif)|
 |Configuración e implementación de directivas de Protección de aplicaciones de Windows Defender|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#configure-and-deploy-windows-defender-application-guard-policies)|[Versión 1710](/sccm/protect/deploy-use/create-deploy-application-guard-policy)|
 |Agregar parámetros al implementar scripts de PowerShell desde Configuration Manager|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)|[Versión 1710](/sccm/apps/deploy-use/create-deploy-scripts)|
 |Configuración de nueva directiva de administración de aplicaciones móviles|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-mobile-application-management-policy-settings)|[Versión 1710](/sccm/mdm/deploy-use/protect-apps-using-mam-policies#step-3-create-an-application-management-policy)|
 |Mejoras de los grupos de límites para puntos de actualización de software|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#improved-boundary-groups-for-software-update-points)|[Versión 1706](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)|
 |Alta disponibilidad del rol del servidor de sitio|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |![Sin agregar](media/Red_X.gif)|
 |Inclusión de la confianza para determinados archivos y carpetas en una directiva de Device Guard|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#include-trust-for-specific-files-and-folders-in-a-device-guard-policy)|[Versión 1706](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|
 |Ocultación del progreso de la secuencia de tareas|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#hide-task-sequence-progress)|![Sin agregar](media/Red_X.gif)|
 |Especificación de una ubicación de contenido diferente para el contenido de instalación y el contenido de desinstalación|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#specify-a-different-content-location-for-install-content-and-uninstall-content)|[Versión 1706](/sccm/core/get-started/capabilities-in-technical-preview-1706#hide-task-sequence-progress)|
 |Mejoras de accesibilidad |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#accessibility-improvements)|[Versión 1706](/sccm/core/understand/accessibility-features)|
 |Compatibilidad del Asistente para servicios de Azure para Upgrade Readiness |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#changes-to-the-azure-services-wizard-to-support-upgrade-readiness)|[Versión 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Nueva configuración de cliente para Cloud Services|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-client-settings-for-cloud-services)|[Versión 1706](/sccm/core/clients/deploy/deploy-clients-cmg-azure)|
 |Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)|[Versión 1710](/sccm/apps/deploy-use/create-deploy-scripts)|
 |Compatibilidad con el arranque de red de PXE para IPv6 |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|![Sin agregar](media/Red_X.gif)|
 |Administración de las actualizaciones de controladores de Microsoft Surface |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#manage-microsoft-surface-driver-updates)|[Versión 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#manage-microsoft-surface-driver-updates)|
 |Configuración de directivas de aplazamiento de Windows Update para empresas |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#configure-windows-update-for-business-deferral-policies)|[Versión 1706](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies)|
 |Restricciones de inscripción de iOS|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#android-and-ios-enrollment-restrictions)|[Versión 1706](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac#configure-enrollment-restrictions)|
 |Restricciones de inscripción de Android|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#android-and-ios-enrollment-restrictions)|[Versión 1706](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-enrollment)|
 |Directiva de administración de aplicaciones de Android for Work para copiar y pegar|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#android-for-work-application-management-policy-for-copy-paste)|[Versión 1706](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client#android-for-work-configuration-item-settings-reference)|
 |Nuevas opciones para elementos de configuración de Windows|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-windows-configuration-item-settings)|[Versión 1706](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Nuevas reglas de directiva de cumplimiento de dispositivos|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-device-compliance-policy-rules)|[Versión 1706](/sccm/mdm/deploy-use/create-compliance-policy)|
 |Evaluación de Atestación de estado de dispositivo para las directivas de cumplimiento de acceso condicional|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|![Sin agregar](media/Red_X.gif)|
 |Compatibilidad con entidades de certificación de Entrust|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#support-for-entrust-certification-authorities)|[Versión 1706](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |Compatibilidad con Cisco (IPsec) para perfiles de VPN de macOS|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#cisco-ipsec-support-for-macos-vpn-profiles)|[Versión 1706](/sccm/protect/deploy-use/vpn-profiles)|
 |Nuevas funcionalidades para Azure AD y administración en la nube|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management)|[Versión 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#azure-ad-integration-with-configuration-manager)|
 |Configuración e implementación de directivas de Protección de aplicaciones de Windows Defender|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#configure-and-deploy-windows-defender-application-guard-policies)|[Versión 1710](/sccm/protect/deploy-use/create-deploy-application-guard-policy)|
 |Herramienta de restablecimiento de actualizaciones  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#update-reset-tool)|[Versión 1706](/sccm/core/servers/manage/update-reset-tool)|
 |Compatibilidad de la consola con una configuración elevada de ppp  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#high-dpi-console-support)|[Versión 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#high-dpi-console-support)|
 |Mejoras de almacenamiento en caché del mismo nivel  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#peer-cache-improvements) |[Versión 1706](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache)|
 |Mejoras de los grupos de disponibilidad AlwaysOn de SQL Server |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#improvements-for-sql-server-always-on-availability-groups) |[Versión 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#improvements-for-sql-server-always-on-availability-groups)|
 |Mejora en las notificaciones de usuario para las actualizaciones de Office 365|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#improved-user-notifications-for-office-365-updates) |[Versión 1706](/sccm/sum/deploy-use/manage-office-365-proplus-updates#restart-behavior-and-client-notifications-for-office-365-updates)|
 |Uso del Asistente para servicios de Azure para configurar una conexión a OMS|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) |[Versión 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Configuración de aplicaciones de Android con directivas de configuración de aplicaciones  |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#configure-android-apps-with-app-configuration-policies)|![Sin agregar](media/Red_X.gif)|
 |El inventario de hardware recopila información de arranque seguro |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#hardware-inventory-collects-secure-boot-information)|[Versión 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#hardware-inventory-collects-secure-boot-information)|
 |Adición de secuencias de tareas secundarias a una secuencia de tareas|[Tech Preview 1704](capabilities-in-technical-preview-1704.md#add-child-task-sequences-to-a-task-sequence)|![Sin agregar](media/Red_X.gif)|
 |Nueva carga de imágenes de arranque con la versión actual de Windows PE |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#reload-boot-images-with-current-windows-pe-version)|[Versión 1706](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image)|
 |Mejoras en la implementación de sistema operativo   <!-- This item does not track to be added to the Current Branch. It is covered by various other incremental work. --> |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#improvements-to-operating-system-deployment)|![Sin agregar](media/Red_X.gif)|
 |Implementación de aplicaciones iOS adquiridas por volumen en colecciones de dispositivos|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#deploy-volume-purchased-ios-apps-to-device-collections)|[Versión 1702](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)|
 |Vínculos directos a aplicaciones del centro de software|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#direct-links-to-applications-in-software-center)|[Versión 1706](/sccm/apps/deploy-use/share-applications)
 |Certificados PFX para equipos cliente Windows de Configuration Manager|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#pfx-certificates-for-configuration-manager-windows-client-computers)|[Versión 1706](/sccm/protect/deploy-use/create-certificate-profiles)|
 |Asistente para configuración de Servicios de Azure|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#configure-azure-services-wizard)|[Versión 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Conversión de BIOS a UEFI en secuencias de tareas de actualización del sistema operativo| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#convert-from-bios-to-uefi-during-an-in-place-upgrade) |[Versión 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)|
 |Grupos de secuencias de tareas contraíbles| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#collapsible-task-sequence-groups) |[Versión 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#collapsible-task-sequence-groups)|
 |Configuración de cliente para configurar Windows Analytics para Upgrade Readiness | [Tech Preview 1703](capabilities-in-technical-preview-1703.md#client-settings-to-configure-windows-analytics-for-upgrade-readiness) |[Versión 1706](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics)|
 |Nueva configuración de cumplimiento para dispositivos iOS|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#new-compliance-settings-for-ios-devices)|[Versión 1702](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)|
 |Crear certificados PFX con compatibilidad con S/MIME|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#create-pfx-certificates-with-s-mime-support)|[Versión 1706](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |Comprobar los archivos ejecutables en ejecución antes de instalar una aplicación|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#check-for-running-executable-files-before-installing-an-application)|[Versión 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Enviar comentarios desde la consola de Configuration Manager | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#send-feedback-from-the-configuration-manager-console)    |[Versión 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#send-feedback-from-the-configuration-managercconsole)  |
 |Cambios para actualizaciones y mantenimiento  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#changes-for-updates-and-servicing)  |[Versión 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#changes-for-updates-and-servicing) |
 |Mejoras de almacenamiento en caché del mismo nivel  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#peer-cache-improvements) |[Versión 1702](/sccm/core/plan-design/hierarchy/client-peer-cache)|
 |Uso de Azure Active Directory <!-- This item does not track to be added to the Current Branch. It is covered by various other incremental work. --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |![Sin agregar](media/Red_X.gif)|
 |Mejoras de la directiva de cumplimiento de dispositivos de acceso condicional | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#conditional-access-device-compliance-policy-improvements) |[Versión 1702](/sccm/mdm/deploy-use/create-compliance-policy)|
 |Alerta de versión de cliente antimalware | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert) |[Versión 1702](/sccm/protect/deploy-use/endpoint-configure-alerts?branch=live#alert-for-outdated-malware-client)|
 |Evaluación del cumplimiento para actualizaciones de Windows Update for Business | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |![Sin agregar](media/Red_X.gif)|
 |Mejoras en la configuración del Centro de software y los mensajes de notificación para las secuencias de tareas de alto impacto|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert)|[Versión 1702](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)|
 |Compatibilidad de Android for Work| [Tech Preview 1702](capabilities-in-technical-preview-1702.md#android-for-work-support) |[Versión 1702](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment)|
 |Mejoras de los grupos de límites para puntos de actualización de software | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |[Versión 1702](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)  |
 |El inventario de hardware recopila información de UEFI | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|[Versión 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#hardware-inventory-collects-uefi-information) |
 |Mejoras en la implementación de sistema operativo| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|[Versión 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment) |
 |Hospedar actualizaciones de software en puntos de distribución basados en la nube| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|[Versión 1702](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#plan-to-use-a-cloud-based-distribution-point) |
 |Validar datos de atestación de estado de dispositivo mediante puntos de administración| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)| [Versión 1702](/sccm/core/servers/manage/health-attestation) |
 |Conector de OMS para la nube de Microsoft Azure Government |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |[Versión 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig) |
 |En los asistentes para creación ya no se pueden seleccionar como destino las versiones de iOS y Android. |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |[Versión 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |
 |Acceso a datos del punto de conexión de OData |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![Sin agregar](media/Red_X.gif)|
 |Punto del servicio de almacenamiento de datos |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|[Versión 1702](/sccm/core/servers/manage/data-warehouse)|
 |Herramienta de limpieza de la biblioteca de contenido |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|[Versión 1702](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) |
 |Mejoras de búsqueda en consola |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|[Versión 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-for-in-console-search)|
 |Impedir la instalación de una aplicación si se está ejecutando un programa específico|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|[Versión 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Nueva notificación de Windows Hello para empresas para los usuarios finales|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|[Versión 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#new-windows-hello-for-business-notification-for-end-users)|
 |Compatibilidad con la Tienda Windows para empresas en Configuration Manager|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|[Versión 1702](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Volver a la página anterior cuando se produce un error en una secuencia de tareas|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|[Versión 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment)|
 |Compatibilidad con archivos de instalación rápida de actualizaciones de Windows 10|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|[Versión 1702](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)|
 |Incorporación de Azure Active Directory|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|[Versión 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Cambiar para configurar la autenticación multifactor para la inscripción de dispositivos|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![Sin agregar](media/Red_X.gif)|
 |Almacenar en la caché previa contenido para las implementaciones y las secuencias de tareas |[Tech Preview 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|[Versión 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
 |Opciones de configuración de Windows Defender|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[Versión 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Solicitar la sincronización de directivas desde la consola de administrador|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[Versión 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |Compatibilidad adicional con el rol de seguridad para el nodo Todos los dispositivos corporativos|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[Versión 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Acceso condicional para perfiles de VPN de Windows 10|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[Versión 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |Filtrar por tamaño del contenido en las reglas de implementación automática|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[Versión 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |Funcionalidad mejorada para los cuadros de diálogo de software obligatorios|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[Versión 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Rechazar solicitudes de aplicación aprobadas previamente|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[Versión 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Excluir a clientes de la actualización automática|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[Versión 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Mejoras de Endpoint Protection|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|[Versión 1610](/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service)|
 |Mayor número de dispositivos inscritos|[Tech Preview 1609](/sccm/mdm/deploy-use/enable-platform-enrollment)|[Versión 1610](/sccm/mdm/deploy-use/enable-platform-enrollment)|
 |Opciones adicionales del DEP de Apple|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[Versión 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |Mejoras en la integración de la Tienda Windows para empresas con Configuration Manager|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|[Versión 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Nueva configuración de cumplimiento para elementos de configuración|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[Versión 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Integración con Upgrade Analytics|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[Versión 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Tipos de conexión nativos para perfiles híbridos de VPN de Windows 10|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Sin agregar](media/Red_X.gif)|
 |Mejoras en los grupos de límites|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[Versión 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Panel de administración de clientes de Office 365|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[Versión 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |Implementar aplicaciones de Office 365 en clientes|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|[Versión 1702](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)|
 |Mejoras en la conversión de BIOS a UEFI|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[Versión 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Gráficos de cumplimiento de Intune|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[Versión 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|


 <!--  TP 1608 and earlier have aged out of support. Features from these previews are either in the minimum supported Current Branch version, or are not scheduled for inclusion.
 |Improvements to the Prepare ConfigMgr Client for Capture task sequence step|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Improvements to Software Center|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |Improvements to Asset Intelligence|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|N/A|
 |Remote control keyboard translation|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|[Version 1702](/sccm/core/clients/manage/remote-control/configuring-remote-control#enable-keyboard-translation)|
 |Improvements to the Windows 10 Edition Upgrade Policy|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[Version 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |Customizable Branding for Software Center Dialogs|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#customizable-branding-for-software-center-dialogs)|  
 |Multiple device management points for On-premises Mobile Device Management|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Automatically categorize devices into collections|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Version 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Enforcement grace period for required application and software update deployments|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Using Configuration Manager as a Managed Installer with Device Guard|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|[Version 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|
 |Cloud management gateway (formerly Cloud Proxy Service)|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway)|  
 |Manage the Office 365 client agent in Configuration Manager|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |The OSDPreserveDriveLetter task sequence variable has been deprecated|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Version 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Changes for the Updates and Servicing Node|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |Per-app VPN for Windows 10 devices|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Version 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Improvements to the Install software updates task sequence|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Improvements to the Prepare ConfigMgr Client for Capture task sequence step |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) |
 |Grace period for required application deployments |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|N/A|  
 |New experience for remote device actions |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Windows Store for Business apps |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |General improvements for volume-purchased apps|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Enterprise Data Protection (EDP)|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |End users can install apps from the Company Portal |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|N/A|  
 |New tabs for Updates and Operating Systems in Software Center|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[Version 1606 ](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Service a server group |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[Version 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Support for Windows Defender Advanced Threat Protection service |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[Version 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |New restart options for Windows 10 clients after software update installation|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |On-premises Device Health Attestation |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |Pre-declare corporate-owned devices with IMEI or iOS serial number|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[Version 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  
 |Manage volume-purchased apps from the Windows Store for Business| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Improvements to Microsoft Passport for Work management|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Option for clients to switch to a new software update point|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |Client settings to manage Client Cache Settings and client Peer Cache |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|Client Settings: [Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)<br/>Peer Cache: [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache)|  
 |Support for Passport for Work as a KSP |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Version 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |On-premises Device Health Attestation|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |SmartLock setting for Android devices|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Version 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |Improvements to Software Center|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Improvements to remote control|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
-->



## <a name="see-also"></a>Véase también  
[Novedades de System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introducción a System Center Configuration Manager](../../core/understand/introduction.md)
