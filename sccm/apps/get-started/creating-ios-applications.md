---
title: Crear aplicaciones iOS | System Center Configuration Manager
description: Consulte las consideraciones que debe tener en cuenta al crear e implementar aplicaciones para dispositivos iOS.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5420109-6538-4430-9ca6-db352ee84c2e
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4c3845635846cae183e81d0ddb9c8222dabd8929


---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>Crear aplicaciones iOS con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Además de los otros requisitos y procedimientos de System Center Configuration Manager para crear una aplicación, también debe tener en cuenta las consideraciones siguientes al crear e implementar aplicaciones para dispositivos iOS.  

## <a name="general-considerations"></a>Consideraciones generales  
 Configuration Manager admite la implementación de los siguientes tipos de aplicaciones:  

|Tipo de dispositivo|Archivos compatibles|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> En System Center Configuration Manager, no es necesario especificar un archivo de lista de propiedades (.plist) al importar una aplicación de iOS.|  

 Se admiten las siguientes acciones de implementación:  

|Tipo de dispositivo|Acciones admitidas|  
|-----------------|-----------------------|  
|iOS|Disponible, Requerido (aunque el usuario debe dar su consentimiento para la instalación), Desinstalar|  

> [!IMPORTANT]  
>  Actualmente, los usuarios finales no pueden instalar aplicaciones corporativas desde la aplicación Portal de empresa de Microsoft Intune para iOS. Esto se debe a las restricciones establecidas para aplicaciones que se publican en la App Store de iOS (consulte la sección 2 de App Store Review Guidelines [Instrucciones de revisión para App Store]). Los usuarios pueden instalar aplicaciones corporativas (incluidas las aplicaciones administradas de App Store y los paquetes de aplicaciones de línea de negocio) si examinan el portal web de Intune desde su dispositivo (portal.manage.microsoft.com). Para obtener más información sobre las funciones de administración de dispositivos móviles que se habilitan con la aplicación Portal de empresa de Microsoft Intune, consulte [Enrolled device management capabilities in Microsoft Intune](https://technet.microsoft.com/library/dn600287.aspx) (Funciones de administración de dispositivos inscritos en Microsoft Intune).  



<!--HONumber=Nov16_HO1-->


