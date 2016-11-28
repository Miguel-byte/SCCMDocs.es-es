---
title: "Seguridad y privacidad de la administración de energía | System Center Configuration Manager"
description: "Obtenga información sobre seguridad y privacidad aplicadas a la administración de energía en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 26880f6682e2bdf61cb7f29416e5dfded3559e8e


---
# <a name="security-and-privacy-for-power-management-in-system-center-configuration-manager"></a>Seguridad y privacidad de la administración de energía en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Esta sección contiene información sobre la seguridad y privacidad en la administración de energía en System Center Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Procedimientos recomendados de seguridad para la administración de energía  
 No hay ningún procedimiento recomendado relacionado con la seguridad para la administración de energía.  

## <a name="privacy-information-for-power-management"></a>Información de privacidad para la administración de energía  
 La administración de energía usa características que están integradas en Windows para supervisar el uso de energía y para aplicar la configuración de energía a equipos durante el horario laboral y fuera del horario laboral. Configuration Manager recopila información sobre el uso de energía de los equipos, por ejemplo, los datos sobre cuándo un usuario utiliza un equipo. Aunque Configuration Manager supervisa el uso de energía de una recopilación en lugar de cada equipo, una recopilación puede contener un solo equipo. La administración de energía no está habilitada de forma predeterminada y un administrador debe configurarla.  

 La información de uso de energía se almacena en la base de datos de Configuration Manager y no se envía a Microsoft. La información detallada se conserva en la base de datos durante 31 días y la información resumida durante 13 meses. No puede configurar el intervalo de eliminación.  

 Antes de configurar la administración de energía, tenga en cuenta los requisitos de privacidad.  



<!--HONumber=Nov16_HO1-->


