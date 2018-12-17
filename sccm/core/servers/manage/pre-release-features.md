---
title: Características de la versión preliminar
titleSuffix: Configuration Manager
description: Las características de versión preliminar son características que se encuentran en la Rama actual para realizar las primeras pruebas en un entorno de producción.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6fb24c3e262f3d1f3991ab549592e3f21631b32d
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456144"
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
| API del proveedor de SMS <!--1359052--> | Versión 1810 | ![Todavía no](media/red_x.png) |
| [Sistema de sitios HTTP mejorado](/sccm/core/plan-design/hierarchy/enhanced-http) <!--1356889,1358228--> | Versión 1806 | Versión 1810 |
| [Aplicaciones móviles para dispositivos administrados conjuntamente](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune) <!--1357892--> | Versión 1806 | ![Todavía no](media/red_x.png) |
| [Administrador de conversión de paquetes](/sccm/apps/pcm/package-conversion-manager) <!--1357861--> | Versión 1806 | Versión 1810 |
| [Compatibilidad con Cisco AnyConnect 4.0.07x y versiones posteriores para iOS](/sccm/mdm/deploy-use/create-vpn-profiles) <!--1357393--> | Versión 1802 | Versión 1802 <br>con la actualización 4163547 |
| [Implementaciones por fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) <!--1356837--> | Versión 1802 | Versión 1806 |
| [Ejecutar paso de secuencia de tareas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence) <!--1261338--> |  Versión 1710 | Versión 1802 |
| [Windows Defender Exploit Guard](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468--> | Versión 1710 | Versión 1802 |
| [Evaluación de la Atestación de mantenimiento del dispositivo para las directivas de cumplimiento en el acceso condicional](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616--> | Versión 1710 | Versión 1802 |
| [Crear y ejecutar scripts de Windows PowerShell](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459--> | Versión 1706 | Versión 1802 |
| [Administración de actualizaciones de controladores de Microsoft Surface](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490--> | Versión 1706 | Versión 1710 |
| [Administración de Device Guard](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) <!--1355092 (1319346)--> | Versión 1702 | ![Todavía no](media/red_x.png) |
| [Almacenamiento en caché previa de contenido de secuencias de tareas](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244--> | Versión 1702 | Versión 1710 |
| [Comprobación de los archivos ejecutables en ejecución antes de instalar una aplicación](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) <!--1284624--> | Versión 1702 | Versión 1706 |
| [Punto de servicio de almacenamiento de datos](/sccm/core/servers/manage/data-warehouse) <!--1277922--> | Versión 1702 | Versión 1706 |
| [Almacenamiento en caché del mismo nivel para la distribución de contenido en los clientes](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436--> | Versión 1610 | Versión 1710 |
| [Cloud Management Gateway](/sccm/core/clients/manage/plan-cloud-management-gateway) <!--1101764--> | Versión 1610 | Versión 1802 |
| [Conector de Log Analytics de Azure](/sccm/core/clients/manage/sync-data-log-analytics) <!--1236739--> | Versión 1606 | Versión 1802 |
| [Mantenimiento de una recopilación compatible con clústeres (dar servicio a un grupo de servidores)](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_ServerGroups) <!--1081776--> | Versión 1602 | ![Todavía no](media/red_x.png) |
| [Acceso condicional para equipos administrados por Configuration Manager](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--  --> | Versión 1602 | Versión 1702 |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!Tip]  
> Para más información sobre las características de versión preliminar que se deben habilitar primero, vea [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> 
> Para más información sobre las características que solo están disponibles en la rama de Technical Preview, vea [Technical Preview](/sccm/core/get-started/technical-preview).  
