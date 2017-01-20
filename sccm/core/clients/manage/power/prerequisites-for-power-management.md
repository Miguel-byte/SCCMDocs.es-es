---
title: "Requisitos previos de la administración de energía | System Center Configuration Manager"
description: "Consulte los requisitos previos de la administración de energía en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
caps.latest.revision: 4
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e83b57997c702779dfa2a198a60c99c7205d7b51


---
# <a name="prerequisites-for-power-management-in-system-center-configuration-manager"></a>Requisitos previos de la administración de energía en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

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
|Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.|Debe configurar un punto de servicios de informes antes de poder ver los informes de administración de energía. Para obtener más información, consulte [Generación de informes en System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  



<!--HONumber=Nov16_HO1-->


