---
title: "Características de versión preliminar| Microsoft Docs"
description: "Características de versión preliminar en System Center Configuration Manager"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: c164ae7ca17a3a7d96b010f41b5ecf72ab34976b
ms.lasthandoff: 03/04/2017


---
# <a name="pre-release-feaures-in-system-center-configuration-manager"></a>Características de versión preliminar en System Center Configuration Manager
*Se aplica a: System Center Configuration Manager (rama actual)*

 Las características de versión preliminar son características que se incluyen en la rama actual para realizar las primeras pruebas en un entorno de producción. Estas características no se considerará preparadas para producción, pero se pueden utilizar en el entorno de producción.

 Antes de poder usar las características de versión preliminar, debe dar su consentimiento para usarlas desde la consola de Configuration Manager para poder seleccionarlas y permitir su uso.  

Dar el consentimiento es una acción que se realiza una sola vez por jerarquía y que no se puede deshacer. Mientras no dé su consentimiento, no puede habilitar nuevas características de versión preliminar incluidas con las actualizaciones.

Para dar su consentimiento, en la consola vaya a **Administración** > **Configuración de sitio** > **Sitios** y seleccione **Configuración de jerarquía**. En la pestaña **General**, seleccione **Consent to use Pre-Release features** (Consentimiento para usar características de versiones preliminares).

 > [!NOTE]
 > Si previamente ha habilitado características de versión preliminar desde la actualización 1602 antes de instalar una versión de actualización posterior, esas características permanecerán habilitadas para su uso aunque no dé su consentimiento para usarlas.

Cuando instale una actualización que incluya características de versión preliminar, dichas características estarán visibles en el Asistente de actualizaciones y mantenimiento con las características convencionales incluidas en la actualización:
  - **Si ha dado su consentimiento:** puede habilitar las características de versiones preliminares en el Asistente de actualizaciones y mantenimiento al instalar la actualización. Para ello, seleccione las características de versiones preliminares como lo haría con cualquier otra característica.     

    Opcionalmente, puede esperar a habilitar una característica de la versión preliminar posteriormente desde el nodo **Administración** > **Servicios en la nube** > **Actualizaciones y mantenimiento** > **Características** de la consola. En el nodo **Características**, seleccione la función y, después, elija **Activar**. (Esta opción aparecerá atenuada mientras no dé su consentimiento).  
  -   **Si no ha dado su consentimiento:** al instalar una actualización, las características de versiones preliminares están visibles en el Asistente de actualizaciones y mantenimiento, pero están atenuadas y no se pueden habilitar. Una vez instalada la actualización, puede ver estas características en el nodo **Características**, pero no puede habilitarlas hasta después de dar su consentimiento en **Configuración de jerarquía**.

Si ha dado su consentimiento en un sitio primario independiente y, después, expande la jerarquía mediante la instalación de un nuevo sitio de administración central, deberá dar su consentimiento de nuevo en el sitio de administración central.

**Están disponibles las siguientes características de versión preliminar:**

 |Característica          |Agregado como versión preliminar | Agregado como característica completa|  
|------------------|---------------------|---------------------|
| Punto de servicio de almacenamiento de datos  |  [Versión 1702](/sccm/core/servers/manage/data-warehouse) |![Todavía no](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Almacenamiento en caché del mismo nivel para la distribución de contenido en los clientes |  [Versión 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![Todavía no](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Puerta de enlace de administración en la nube |  [Versión 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![Todavía no](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Panel de orígenes de datos de cliente |  [Versión 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![Todavía no](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Conector de Microsoft Operations Management Suite  | [Versión 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Todavía no](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Mantenimiento de una recopilación compatible con clústeres (Dar servicio a un grupo de servidores).| [Versión 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Todavía no](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Acceso condicional para equipos administrados por System Center Configuration Manager | [Versión 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     |![Todavía no](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)                        |

