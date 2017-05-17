---
title: "Inventario de software para dispositivos móviles inscritos con Microsoft Intune | Microsoft Docs"
description: "Inventario de software para dispositivos móviles inscritos con Microsoft Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 2ed79d02535768de136947e4a5b63ad186d9a3cd
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017

---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventario de software para dispositivos móviles inscritos con Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*

 Puede recopilar inventario para aplicaciones instaladas en dispositivos móviles. Las aplicaciones que se incluyen en el inventario dependerán de si el dispositivo es propiedad de la empresa o personal. Para dispositivos personales, las únicas aplicaciones inventariadas son las administradas por Microsoft Intune.  

> [!NOTE]  
>  El inventario de las aplicaciones instaladas en dispositivos móviles se recopila como parte del proceso de [inventario de hardware](mobile-device-hardware-inventory-hybrid.md).  

 Aquí se enumeran las aplicaciones que están inventariadas para dispositivos de propiedad personal o de empresa.  

|Plataforma|Para dispositivos personales|Para dispositivos de la compañía|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (sin el cliente de Configuration Manager)|Solo aplicaciones administradas|Solo aplicaciones administradas|
|Windows 8.1 (sin el cliente de Configuration Manager)|Solo aplicaciones administradas|Solo aplicaciones administradas|  
|Windows Phone 8|Solo aplicaciones administradas|Solo aplicaciones administradas|  
|Windows RT|Solo aplicaciones administradas|Solo aplicaciones administradas|  
|iOS|Solo aplicaciones administradas|Todas las aplicaciones instaladas en el dispositivo|  
|Android|Solo aplicaciones administradas|Todas las aplicaciones instaladas en el dispositivo|  

Consulte [Introducción al inventario de software en System Center Configuration Manager](../../core/clients/manage/inventory/introduction-to-software-inventory.md) y [Cómo configurar el inventario de software en System Center Configuration Manager](../../core/clients/manage/inventory/configure-software-inventory.md) para obtener información detallada sobre el uso del inventario de software para recopilar información de archivos en dispositivos cliente.

