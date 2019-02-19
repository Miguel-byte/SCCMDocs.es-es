---
title: Configuration Manager y Windows como servicio
titleSuffix: Configuration Manager
description: Obtenga información básica sobre cómo adoptar la rama actual de Configuration Manager para admitir Windows como servicio.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1ea9e2ef8da09d0ab344d56fe0ad4f1b3fb9d94b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130510"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>Configuration Manager y Windows como servicio

*Se aplica a: System Center Configuration Manager (Rama actual)*

System Center Configuration Manager proporciona un amplio control sobre las actualizaciones de características para Windows 10. Para adoptar totalmente Windows como modelo de servicio, también debe adoptar el modelo de rama actual de Configuration Manager. Para mantenerse al día con Windows 10 y obtener la mejor experiencia posible, es necesario hacerlo también con Configuration Manager. Las nuevas versiones de Configuration Manager son necesarias para aprovechar al máximo las nuevas y emocionantes características empresariales para Windows 10. Este artículo está diseñado para ser la página de destino de los artículos clave necesarios para adoptar la rama actual de Configuration Manager. La rama actual de Configuration Manager permite iniciar el camino hacia Windows como servicio.

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>Artículos clave sobre la adopción de la rama actual de Configuration Manager

| Artículo        | Descripción          | 
| ------------- |-------------|
|[Overview of Configuration Manager current branch](/sccm/core/plan-design/changes/whats-new-incremental-versions) (Introducción a la rama actual de Configuration Manager)|Se proporciona un breve resumen de los puntos clave para el nuevo modelo de servicio para Configuration Manager (rama actual)|
|[Ciclo de vida de soporte técnico](/sccm/core/servers/manage/current-branch-versions-supported)|Se explica el nuevo modelo de soporte técnico y servicios.|
|[Elementos eliminados y en desuso](/sccm//core/plan-design/changes/deprecated/removed-and-deprecated)|Se proporcionan notificaciones anticipadas sobre los cambios futuros que es posible que afecten al uso de Configuration Manager.|
|[Updates to Configuration Manager current branch](/sccm/core/servers/manage/updates) (Actualizaciones de la rama actual de Configuration Manager)|Se explica el sencillo método en consola para aplicar actualizaciones de características a Configuration Manager.|
|[Obtención de actualizaciones disponibles](/sccm/core/servers/manage/install-in-console-updates#get-available-updates)|Se explican los dos modos disponibles para obtener las nuevas actualizaciones de características de Configuration Manager.|
|[Lista de comprobación de actualización](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall)|Se proporcionan listas de comprobación de actualización específicas de la versión, si procede.| 
|[Instalación de nuevas actualizaciones de características de Configuration Manager](/sccm/core/servers/manage/install-in-console-updates#bkmk_install)|Se explican los pasos de instalación para actualizaciones de características.|
|[Compatibilidad con Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)|Se proporciona una matriz de compatibilidad para versiones de Windows 10 (y ADK).|
|[Technical Preview para Configuration Manager](/sccm/core/get-started/technical-preview)|Se proporciona información sobre el programa de Technical Preview de Configuration Manager.|


## <a name="key-articles-about-adopting-windows-as-a-service"></a>Artículos clave sobre la adopción de Windows como servicio

| Artículo        | Descripción          | 
| ------------- |-------------|
|[Administración de Windows como servicio](/sccm/osd/deploy-use/manage-windows-as-a-service)|Se explica cómo usar los planes de mantenimiento para implementar actualizaciones de características de Windows 10.|
|[Upgrade Windows 10 via task sequence](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system) (Actualizar Windows 10 mediante la secuencia de tareas)|Detalles de la creación de una secuencia de tareas para actualizar Windows 10 con recomendaciones adicionales.|
|[Implementaciones por fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|Las implementaciones por fases automatizan una implementación coordinada y secuencial de una secuencia de tareas en varias recopilaciones.|  
|[Optimizar la distribución de actualizaciones de Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)|Use Configuration Manager para administrar el contenido de actualización para estar al día con Windows 10.|
|[Integrar con Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics)|Upgrade Readiness permite evaluar y analizar si los dispositivos del entorno están preparados para actualizarse a Windows 10.| 
|[Integración de Windows Update para empresas (opcional)](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|Se explica cómo definir e implementar directivas de Windows Update para empresas (WUfB) mediante Configuration Manager.|
|[Uso de la administración conjunta con Microsoft Intune y Windows Update para empresas (opcional)](/sccm/comanage/overview)|Se proporciona información general sobre la administración conjunta| 


## <a name="related-articles"></a>Artículos relacionados

- [Actualización inmediata a System Center Configuration Manager (Rama actual) desde Configuration Manager 2012](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [Plan de migración a System Center Configuration Manager (Rama actual) desde Configuration Manager 2007](/sccm/core/migration/planning-for-migration)
