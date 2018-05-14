---
title: Características de la versión preliminar
titleSuffix: Configuration Manager
description: Las características de versión preliminar son características que se encuentran en la Rama actual para realizar las primeras pruebas en un entorno de producción.
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d4e9664832b37dd05f001404012acab80fd87a43
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="pre-release-features-in-system-center-configuration-manager"></a>Características de versión preliminar en System Center Configuration Manager
*Se aplica a: System Center Configuration Manager (Rama actual)*

Las características de versión preliminar son características que se encuentran en la Rama actual para realizar las primeras pruebas en un entorno de producción. Estas características son totalmente compatibles pero aún se encuentran en proceso de desarrollo y podrían recibir cambios hasta que se saquen de la categoría de versión preliminar.

 Antes de poder usar las características de versión preliminar, debe dar su consentimiento para usarlas desde la consola de Configuration Manager para poder seleccionarlas y permitir su uso.  

Dar el consentimiento es una acción que se realiza una sola vez por jerarquía y que no se puede deshacer. Mientras no dé su consentimiento, no puede habilitar nuevas características de versión preliminar incluidas con las actualizaciones. Después de activar una característica de versión preliminar, no puede desactivarla.

Para dar su consentimiento, en la consola vaya a **Administración** > **Configuración de sitio** > **Sitios** y seleccione **Configuración de jerarquía**. En la pestaña **General**, seleccione **Consent to use Pre-Release features** (Consentimiento para usar características de versiones preliminares).

Cuando instale una actualización que incluya características de versión preliminar, dichas características estarán visibles en el Asistente de actualizaciones y mantenimiento con las características convencionales incluidas en la actualización:
  - **Si ha dado su consentimiento:** puede habilitar las características de versiones preliminares en el Asistente de actualizaciones y mantenimiento al instalar la actualización. Para ello, seleccione las características de versiones preliminares como lo haría con cualquier otra característica.     

    Opcionalmente, puede esperar a habilitar una característica de la versión preliminar posteriormente desde el nodo **Administración** > **Actualizaciones y mantenimiento** > **Características** de la consola. En el nodo **Características**, seleccione la función y, después, elija **Activar**. Esta opción aparecerá atenuada mientras no dé su consentimiento. (Antes de la versión 1702, la opción Actualizaciones y mantenimiento se encontraba en **Administración** > **Cloud Services**).
  -   **Si no ha dado su consentimiento:** al instalar una actualización, las características de versiones preliminares están visibles en el Asistente de actualizaciones y mantenimiento, pero están atenuadas y no se pueden habilitar. Después de instalar la actualización, puede ver estas características en el nodo **Características**. Sin embargo, no puede habilitarlas hasta después de que haya dado su consentimiento en **Configuración de jerarquía**.


> [!Important]  
> En una jerarquía multisitio solo se pueden habilitar características opcionales o de versión preliminar desde el sitio de administración central. Con este comportamiento se procura que no haya ningún conflicto en la jerarquía. <!--507197-->  
> Si ha dado su consentimiento en un sitio primario independiente y, después, expande la jerarquía mediante la instalación de un nuevo sitio de administración central, deberá dar su consentimiento de nuevo en el sitio de administración central.  

 Al habilitar una característica de versión preliminar, el Administrador de jerarquía de Configuration Manager (HMAN) debe procesar el cambio antes de que dicha característica esté disponible. Generalmente el procesamiento del cambio es inmediato, pero puede tardar hasta 30 minutos en completarse, en función del ciclo de procesamiento de HMAN. Una vez que se haya procesado el cambio, debe reiniciar la consola para poder ver la nueva interfaz de usuario relacionada con esa característica.

**Están disponibles las siguientes características de versión preliminar:**

 |Característica          |Agregado como versión preliminar | Agregado como característica completa|  
|------------------|---------------------|---------------------|
|Soporte para Cisco AnyConnect 4.0.07x y versiones posteriores para iOS<!--1357393-->|[Versión 1802](/sccm/mdm/deploy-use/create-vpn-profiles)|![Todavía no](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Implementaciones por fases <!--1356837-->|[Versión 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|![Todavía no](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Ejecutar paso de secuencia de tareas <!-- 1261338 --> |  [Versión 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |[Versión 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence)|
| Windows Defender Exploit Guard <!-- 1355468 --> |  [Versión 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |[Versión 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)|
| Evaluación de la Atestación de mantenimiento del dispositivo para las directivas de cumplimiento en el acceso condicional <!-- 1235616 --> |  [Versión 1710](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) |[Versión 1802](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)|
| Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager <!-- 1236459 --> |  [Versión 1706](/sccm/apps/deploy-use/create-deploy-scripts)|[Versión 1802](/sccm/apps/deploy-use/create-deploy-scripts)|
| Administración de actualizaciones de controladores de Microsoft Surface <!-- 1098490 --> |  [Versión 1706](/sccm/sum/get-started/configure-classifications-and-products) | [Versión 1710](/sccm/sum/get-started/configure-classifications-and-products)|
| Administración de Device Guard con Configuration Manager <!-- 1319346 --> |  [Versión 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Todavía no](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Almacenamiento en caché previa de contenido de secuencias de tareas <!-- 1021244 --> |  [Versión 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) | [Versión 1710](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
| Comprobación de los archivos ejecutables en ejecución antes de instalar una aplicación <!-- 1284624 --> |   [Versión 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[Versión 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| Punto de servicio de almacenamiento de datos <!-- 1277922 --> |  [Versión 1702](/sccm/core/servers/manage/data-warehouse) |[Versión 1706](/sccm/core/servers/manage/data-warehouse)|
| Almacenamiento en caché del mismo nivel para la distribución de contenido en los clientes <!-- 1101436 --> |  [Versión 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) | [Versión 1710](/sccm/core/plan-design/hierarchy/client-peer-cache)|
| Puerta de enlace de administración en la nube <!-- 1101764 --> |  [Versión 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |[Versión 1802](/sccm/core/clients/manage/plan-cloud-management-gateway)|
| Conector de Microsoft Operations Management Suite <!-- 1236739 --> | [Versión 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |[Versión 1802](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md)|
| Mantenimiento de una recopilación compatible con clústeres (dar servicio a un grupo de servidores) <!-- 1081776 --> | [Versión 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Todavía no](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Acceso condicional para equipos administrados por System Center Configuration Manager <!--  --> | [Versión 1602](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)     | [Versión 1702](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)                     |
<!--Image used = ![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif) -->

> [!Tip]  
> Para más información sobre las características de versión preliminar que se deben habilitar primero, vea [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> Para más información sobre las características que solo están disponibles en la rama de Technical Preview, vea [Technical Preview](/sccm/core/get-started/technical-preview).  
