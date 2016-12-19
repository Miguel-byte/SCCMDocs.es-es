---
title: Crear aplicaciones de iOS | Microsoft Docs
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
ms.sourcegitcommit: e9e34359f4412ba07b9fb49f871a1eb2d36cecf8
ms.openlocfilehash: eb2d1245932d71bd10fd63d95a155eae7d128836


---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>Crear aplicaciones iOS con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Tenga en cuenta las siguientes consideraciones cuando cree e implemente aplicaciones para dispositivos iOS.  

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



<!--HONumber=Dec16_HO3-->


