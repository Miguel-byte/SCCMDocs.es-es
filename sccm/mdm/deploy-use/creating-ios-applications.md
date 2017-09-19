---
title: Crear aplicaciones de iOS | Microsoft Docs
description: Consulte las consideraciones que debe tener en cuenta al crear e implementar aplicaciones para dispositivos iOS.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
caps.latest.revision: "10"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: af3479a75a1024bdcf9ce6c354c073ee5fb837b6
ms.sourcegitcommit: f6a428a8db7145affa388f59e0ad880bdfcf17b5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/14/2017
---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>Crear aplicaciones iOS con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Una aplicación de System Center Configuration Manager tiene uno o varios tipos de implementación que incluyen la información y los archivos de instalación necesarios para implementar un dispositivo. Además tiene reglas que especifican cuándo y cómo se implementa el software.  

 Puede crear aplicaciones mediante los métodos siguientes:  

-   Crear automáticamente los tipos de aplicación y de implementación mediante la lectura de los archivos de instalación de la aplicación.  

-   Crear manualmente la aplicación y, a continuación, agregar los tipos de implementación más adelante.  

-   Importe una aplicación desde un archivo.  

Consulte [Inicie el Asistente para crear aplicaciones](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) para conocer los pasos necesarios para crear aplicaciones de Configuration Manager y los tipos de implementación. Tenga en cuenta también las siguientes consideraciones cuando cree e implemente aplicaciones para dispositivos iOS.  

## <a name="general-considerations"></a>Consideraciones generales  
 Configuration Manager admite la implementación de los siguientes tipos de aplicaciones:  

|Tipo de dispositivo|Archivos compatibles|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> En System Center Configuration Manager, no es necesario especificar un archivo de lista de propiedades (.plist) al importar una aplicación de iOS.|  

 Se admiten las siguientes acciones de implementación:  

|Tipo de dispositivo|Acciones admitidas|  
|-----------------|-----------------------|  
|iOS|**Disponible**, **Necesario**. El usuario debe dar su consentimiento para la instalación y desinstalación.

> [!IMPORTANT]  
>  Actualmente, los usuarios finales no pueden instalar aplicaciones corporativas desde la aplicación Portal de empresa de Microsoft Intune para iOS. Esto se debe a las restricciones establecidas para aplicaciones que se publican en la App Store de iOS (consulte la sección 2 de App Store Review Guidelines [Instrucciones de revisión para App Store]). Los usuarios pueden instalar aplicaciones corporativas (incluidas las aplicaciones administradas de App Store y los paquetes de aplicaciones de línea de negocio) si examinan el portal web de Intune desde su dispositivo (portal.manage.microsoft.com). Para más información acerca de las funciones de administración de dispositivos móviles que se habilitan con la aplicación Portal de empresa de Microsoft Intune, vea [Funciones de administración de dispositivos inscritos en Microsoft Intune](https://technet.microsoft.com/library/dn600287.aspx).  
