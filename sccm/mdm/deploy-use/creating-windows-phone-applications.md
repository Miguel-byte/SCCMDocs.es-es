---
title: Creación de aplicaciones de Windows Phone
titleSuffix: Configuration Manager
description: Crear e implementar aplicaciones para dispositivos Windows Phone en Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 24ce7609a2e3e3ec9cfd9363ebd58cba3ec4dadd
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120678"
---
# <a name="create-windows-phone-applications-in-configuration-manager"></a>Crear aplicaciones Windows Phone en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Una aplicación de Configuration Manager tiene uno o varios tipos de implementación. Los tipos de implementación incluyen los archivos de instalación y la información requerida para implementar software en un dispositivo. Además tiene reglas que especifican cuándo y cómo se implementa el software.  

Consulte [crear una aplicación](/sccm/apps/deploy-use/create-applications#bkmk_create) para conocer los pasos para crear aplicaciones de Configuration Manager y los tipos de implementación. 

Tenga en cuenta las siguientes consideraciones cuando cree e implemente aplicaciones para dispositivos Windows Phone:  


Configuration Manager admite la implementación de los siguientes tipos de archivo de aplicaciones:  

|Tipo de dispositivo|Tipos de archivo compatibles|  
|-----------------|---------------------|  
|Windows Phone 8|xap|  
|Windows Phone 8.1|xap, appx, appxbundle|
|Windows 10 Mobile|xap, appx, appxbundle|

Implemente las aplicaciones de Windows Phone como **Disponible** o **Requerida**. También puede usar las implementaciones para desinstalar las aplicaciones.  
