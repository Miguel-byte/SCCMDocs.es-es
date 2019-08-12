---
title: Características de la versión preliminar
titleSuffix: Configuration Manager
description: Las características de versión preliminar son características que se encuentran en la Rama actual para realizar las primeras pruebas en un entorno de producción.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bfcaa12634b313cc1d0071d76e704ed07fc06608
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536147"
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



## <a name="bkmk_table"></a>Características de la versión preliminar

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features).  


> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1906, it's no longer a pre-release feature.  

-->

<!-- With each current branch release, to help purge this list a bit, remove any entries that were added as a full feature in a version that's no longer supported -->
| Característica          | Agregado como versión preliminar | Agregado como característica completa |  
|------------------|----------------------|-------------------------|
| [Depurador de secuencia de tareas](/sccm/osd/deploy-use/debug-task-sequence) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71--> | Versión 1906 | ![Todavía no](media/red_x.png) |
| [Grupos de aplicaciones](/sccm/apps/deploy-use/create-app-groups) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D--> | Versión 1906 | ![Todavía no](media/red_x.png) |
| [Detección de grupos de usuarios de Azure Active Directory](/sccm/core/servers/deploy/configure/configure-discovery-methods#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->| Versión 1906 | ![Todavía no](media/red_x.png) |
| [Sincronización de los resultados de pertenencia a recopilaciones con Azure Active Directory](/sccm/core/clients/manage/collections/create-collections#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->| Versión 1906| ![Todavía no](media/red_x.png)|
| [CMPivot independiente](/sccm/core/servers/manage/cmpivot#bkmk_standalone) <!--3555890/4692885,no GUID--> | Versión 1906 | ![Todavía no](media/red_x.png) |
| [Servicio de administración Proveedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_admin-service) <!--1359052--> | Versión 1810 | Versión 1906 |
| [Sistema de sitio HTTP mejorado](/sccm/core/plan-design/hierarchy/enhanced-http) <!--1356889,1358228--> | Versión 1806 | Versión 1810 |
| [Aplicaciones cliente para dispositivos administrados conjuntamente](/sccm/comanage/workloads#client-apps) <!--1357892,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C--> | Versión 1806 | ![Todavía no](media/red_x.png) |
| [Extensiones SCAP](/sccm/compliance/plan-design/scap/about-scap) <!--3607889--> | Versión 1806 | ![Todavía no](media/red_x.png) |
| [Administrador de conversión de paquetes](/sccm/apps/pcm/package-conversion-manager) <!--1357861--> | Versión 1806 | Versión 1810 |
| [Compatibilidad con Cisco AnyConnect 4.0.07x y versiones posteriores para iOS](/sccm/mdm/deploy-use/create-vpn-profiles) <!--1357393--> | Versión 1802 | Versión 1802 <br>con la actualización 4163547 |
| [Implementaciones por fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) <!--1356837--> | Versión 1802 | Versión 1806 |
| [Ejecutar paso de secuencia de tareas](/sccm/osd/understand/task-sequence-steps#child-task-sequence) <!--1261338--> |  Versión 1710 | Versión 1802 |
| [Protección contra vulnerabilidades de seguridad de Windows Defender](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468--> | Versión 1710 | Versión 1802 |
| [Evaluación de la Atestación de mantenimiento del dispositivo para las directivas de cumplimiento en el acceso condicional](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616--> | Versión 1710 | Versión 1802 |
| [Crear y ejecutar scripts de Windows PowerShell](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459--> | Versión 1706 | Versión 1802 |
| [Administración de Device Guard](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) <!--3600958 (fka 1355092 & 1319346)--> | Versión 1702 | Versión 1906 |
| [Puerta de enlace de administración en la nube](/sccm/core/clients/manage/plan-cloud-management-gateway) <!--1101764--> | Versión 1610 | Versión 1802 |
| [Conector de Log Analytics de Azure](/sccm/core/clients/manage/sync-data-log-analytics) <!--1236739--> | Versión 1606 | Versión 1802 |
| [Mantenimiento de una recopilación compatible con clústeres (grupos de servidores)](/sccm/sum/deploy-use/service-a-server-group) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697--> | Versión 1602 | ![Todavía no](media/red_x.png) |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!Tip]  
> Para más información sobre las características de versión preliminar que se deben habilitar primero, vea [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> 
> Para más información sobre las características que solo están disponibles en la rama de Technical Preview, vea [Technical Preview](/sccm/core/get-started/technical-preview).  
