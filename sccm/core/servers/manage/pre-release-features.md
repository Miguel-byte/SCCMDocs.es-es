---
title: Características de la versión preliminar
titleSuffix: Configuration Manager
description: Las características de versión preliminar son características que se encuentran en la Rama actual para realizar las primeras pruebas en un entorno de producción.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e72cdf667f96828fb6730cf3294c8d20ec553130
ms.sourcegitcommit: 759098de944b8f7d5eedfc2bae2cb9a6ba15276f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43289261"
---
# <a name="pre-release-features-in-configuration-manager"></a>Características de versión preliminar en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las características de versión preliminar son las que se encuentran en la rama actual para realizar las primeras pruebas en un entorno de producción. Estas características son totalmente compatibles, pero siguen en fase de desarrollo activo. Es posible que reciban cambios hasta que se saquen de la categoría de versión preliminar.



## <a name="give-consent"></a>Dar el consentimiento  

Antes de usar las características de versión preliminar, dé su consentimiento para usarlas. Dar el consentimiento es una acción que se realiza una sola vez por jerarquía y no se puede deshacer. Mientras no dé su consentimiento, no podrá habilitar las características de versión preliminar nuevas incluidas con las actualizaciones. Después de activar una característica de versión preliminar, no se puede desactivar.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.  

2. Haga clic en **Configuración de jerarquía** en la cinta de opciones.  

3. En la pestaña **General** de las Propiedades de configuración de la jerarquía, habilite la opción **Consentimiento para usar características de versión preliminar**. Haga clic en **Aceptar**.  



## <a name="enabling-pre-release-features"></a>Habilitación de características de versión preliminar

Cuando se instala una actualización que incluye características de versión preliminar, esas características son visibles en el Asistente de actualizaciones y mantenimiento con las características convencionales incluidas en la actualización.

#### <a name="if-you-have-given-consent"></a>Si ha dado su consentimiento
En el Asistente de actualizaciones y mantenimiento, habilite las características de versión preliminar. Seleccione las características de versión preliminar como haría con cualquier otra característica.     

Opcionalmente, espere a habilitar las características de versión preliminar más tarde desde el nodo **Características** de **Actualizaciones y mantenimiento** en el área de trabajo **Administración**. Seleccione una característica y, después, haga clic en **Activar** en la cinta. Hasta que dé su consentimiento, esta opción no está disponible para su uso.

#### <a name="if-you-havent-given-consent"></a>Si no ha dado su consentimiento
En el Asistente de actualizaciones y mantenimiento, las características de versión preliminar están visibles pero no se pueden habilitar. Después de instalar la actualización, estas características son visibles en el nodo **Características**. Pero no las puede habilitar hasta que no dé su consentimiento.


> [!Important]  
> En una jerarquía multisitio solo se pueden habilitar características opcionales o de versión preliminar desde el sitio de administración central. Con este comportamiento se procura que no haya ningún conflicto en la jerarquía. <!--507197-->  
> 
> Si ha dado su consentimiento en un sitio primario independiente y, después, expande la jerarquía mediante la instalación de un sitio de administración central nuevo, deberá volver a dar su consentimiento en el sitio de administración central.  

Al habilitar una característica de versión preliminar, el Administrador de jerarquía de Configuration Manager (HMAN) debe procesar el cambio antes de que dicha característica esté disponible. El procesamiento del cambio suele ser inmediato. Según el ciclo de procesamiento de HMAN, puede tardar hasta 30 minutos en completarse. Una vez procesado el cambio, reinicie la consola antes de usar la característica.



## <a name="pre-release-features"></a>Características de la versión preliminar

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features).  


> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1706, this feature is no longer a pre-release feature.  

-->


| Característica          | Agregado como versión preliminar | Agregado como característica completa |  
|------------------|----------------------|-------------------------|
| Sistema de sitios HTTP mejorado<!--1356889,1358228-->|Versión 1806|![Todavía no](media/red_x.png)|
| Aplicaciones móviles para dispositivos administrados conjuntamente<!--1357892-->|[Versión 1806](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune)|![Todavía no](media/red_x.png)|
| Administrador de conversión de paquetes<!--1357861-->|[Versión 1806](/sccm/apps/pcm/package-conversion-manager)|![Todavía no](media/red_x.png)|
| Soporte para Cisco AnyConnect 4.0.07x y versiones posteriores para iOS<!--1357393-->|[Versión 1802](/sccm/mdm/deploy-use/create-vpn-profiles)| [Versión 1802 con la actualización 4163547](/sccm/mdm/deploy-use/create-vpn-profiles) |
| Implementaciones por fases <!--1356837-->|[Versión 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|[Versión 1806](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|
| Ejecutar paso de secuencia de tareas <!-- 1261338 --> |  [Versión 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |[Versión 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence)|
| Windows Defender Exploit Guard <!-- 1355468 --> |  [Versión 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |[Versión 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)|
| Evaluación de la Atestación de mantenimiento del dispositivo para las directivas de cumplimiento en el acceso condicional <!-- 1235616 --> |  [Versión 1710](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) |[Versión 1802](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)|
| Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager <!-- 1236459 --> |  [Versión 1706](/sccm/apps/deploy-use/create-deploy-scripts)|[Versión 1802](/sccm/apps/deploy-use/create-deploy-scripts)|
| Administración de actualizaciones de controladores de Microsoft Surface <!-- 1098490 --> |  [Versión 1706](/sccm/sum/get-started/configure-classifications-and-products) | [Versión 1710](/sccm/sum/get-started/configure-classifications-and-products)|
| Administración de Device Guard con Configuration Manager <!-- 1319346 --> |  [Versión 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Todavía no](media/red_x.png)|
| Almacenamiento en caché previa de contenido de secuencias de tareas <!-- 1021244 --> |  [Versión 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) | [Versión 1710](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
| Comprobación de los archivos ejecutables en ejecución antes de instalar una aplicación <!-- 1284624 --> |   [Versión 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[Versión 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| Punto de servicio de almacenamiento de datos <!-- 1277922 --> |  [Versión 1702](/sccm/core/servers/manage/data-warehouse) |[Versión 1706](/sccm/core/servers/manage/data-warehouse)|
| Almacenamiento en caché del mismo nivel para la distribución de contenido en los clientes <!-- 1101436 --> |  [Versión 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) | [Versión 1710](/sccm/core/plan-design/hierarchy/client-peer-cache)|
| Puerta de enlace de administración en la nube <!-- 1101764 --> |  [Versión 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |[Versión 1802](/sccm/core/clients/manage/plan-cloud-management-gateway)|
| Conector de Microsoft Operations Management Suite <!-- 1236739 --> | [Versión 1606](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) |[Versión 1802](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)|
| Mantenimiento de una recopilación compatible con clústeres (dar servicio a un grupo de servidores) <!-- 1081776 --> | [Versión 1602](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_ServerGroups)|![Todavía no](media/red_x.png)|
| Acceso condicional para equipos administrados por System Center Configuration Manager <!--  --> | [Versión 1602](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)     | [Versión 1702](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)                     |
<!--Image used = ![Not yet](media/red_x.png) -->

> [!Tip]  
> Para más información sobre las características de versión preliminar que se deben habilitar primero, vea [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> 
> Para más información sobre las características que solo están disponibles en la rama de Technical Preview, vea [Technical Preview](/sccm/core/get-started/technical-preview).  
