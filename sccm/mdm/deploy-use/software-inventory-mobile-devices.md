---
title: Inventario de software para dispositivos móviles inscritos con Microsoft Intune
titleSuffix: Configuration Manager
description: Inventario de software para dispositivos móviles inscritos con Microsoft Intune.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 91d298dae14c879e215b85483558898382c12055
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62227886"
---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventario de software para dispositivos móviles inscritos con Microsoft Intune

*Se aplica a: System Center Configuration Manager (Rama actual)*

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
