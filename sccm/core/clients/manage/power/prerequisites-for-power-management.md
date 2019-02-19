---
title: Requisitos previos de la administración de energía
titleSuffix: Configuration Manager
description: Consulte los requisitos previos de la administración de energía en System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e965c9abede80bac488cfba0759d4f9e33974fb
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125813"
---
# <a name="prerequisites-for-power-management-in-system-center-configuration-manager"></a>Requisitos previos de la administración de energía en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La administración de energía en System Center Configuration Manager tiene dependencias externas y dependencias dentro del producto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependencias externas a Configuration Manager  
 En la tabla siguiente se enumeran las dependencias externas a Configuration Manager para usar la administración de energía.  

|Dependencia|Más información|  
|----------------|----------------------|  
|Los equipos cliente deben ser capaces de admitir los estados de energía necesarios|Para usar todas las características de administración de energía, los equipos cliente deben ser capaces de admitir las acciones de suspensión, hibernación, reactivación de una suspensión y reactivación de una hibernación. Puede usar el informe **Capacidades de energía** para determinar si los equipos pueden admitir estas acciones. Para obtener más información, consulte [Power Capabilities report](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) (Informe de las capacidades de energía) en el tema [How to Monitor and Plan for Power Management in Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md) (Cómo supervisar y planear la administración de energía en Configuration Manager).|  

## <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  
 En la tabla siguiente se enumeran las dependencias dentro de Configuration Manager para usar la administración de energía.  

|Dependencia|Más información|  
|----------------|----------------------|  
|La administración de energía debe estar habilitada para poder crear y supervisar planes de energía.|Para obtener información sobre cómo habilitar y configurar la administración de energía, consulte [Configuring Power Management in Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md) (Configuración de la administración de energía en Configuration Manager).|  
|Punto de servicios de informes|Debe configurar un punto de servicios de informes antes de poder ver los informes de administración de energía. Para obtener más información, consulte [Reporting in System Center Configuration Manager](../../../../core/servers/manage/reporting.md) (Generación de informes en System Center Configuration Manager).|  
