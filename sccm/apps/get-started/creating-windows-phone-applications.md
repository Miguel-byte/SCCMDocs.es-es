---
title: Crear aplicaciones de Windows Phone | Microsoft Docs
description: Consulte las consideraciones que debe tener en cuenta al crear e implementar aplicaciones para dispositivos de Windows Phone.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 866113ff-efd0-40d2-ac3a-2edd49732a24
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 557888d1f1f899e3198c430bbe5ccdd44178f824
ms.openlocfilehash: 5cd1ba42afd13e98565d24d1ec8a3ee209e8532c


---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>Crear aplicaciones de Windows Phone con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Además de los otros requisitos y procedimientos de System Center Configuration Manager para crear una aplicación, también debe tener en cuenta las consideraciones siguientes al crear e implementar aplicaciones para dispositivos de Windows Phone.  

## <a name="general-considerations"></a>Consideraciones generales  
 Configuration Manager admite la implementación de los siguientes tipos de archivo de aplicaciones:  

|Tipo de dispositivo|Tipos de archivo compatibles|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8,1|.xap, .appx, .appxbundle|  

 Se admiten las siguientes acciones de implementación:  

|Tipo de dispositivo|Acciones admitidas|  
|-----------------|-----------------------|  
|Windows Phone 8 y Windows Phone 8.1|Disponible, necesario, desinstalar|  

## <a name="steps-to-deploy-the-latest-windows-phone-company-portal-app-with-supersedence"></a>Pasos para implementar la aplicación de portal de empresa de Windows Phone más reciente con sustitución  
 En la tabla siguiente se proporciona información, pasos y detalles para la creación e implementación de la aplicación del portal de la compañía de Windows Phone 8 más reciente.  

|Paso|Más información|  
|----------|----------------------|  
|**Paso 1:** obtener la aplicación de portal de empresa más reciente.|Descargue la [Ap de portal de empresa de Windows Phone 8](http://go.microsoft.com/fwlink/?LinkId=268440).|  
|**Paso 2:** firmar la aplicación de portal de empresa con el certificado de Symantec.|Para obtener información sobre cómo iniciar sesión en la aplicación de portal de empresa, consulte [Set up Windows Phone and Windows 10 Mobile hybrid device management with System Center Configuration Manager and Microsoft Intune](../../mdm/deploy-use/enroll-hybrid-windows.md) (Configurar la administración de dispositivos híbridos de Windows Phone y Windows 10 Mobile con System Center Configuration Manager y Microsoft Intune).|  
|**Paso 3:** crear una nueva aplicación con la versión más reciente de la aplicación de portal de empresa y especificar una relación de sustitución.|Para obtener más información, consulte [Create applications](../../apps/deploy-use/create-applications.md) (Crear aplicaciones) y [Revise and supersede applications](../../apps/deploy-use/revise-and-supersede-applications.md) (Revisar y sustituir aplicaciones).|  
|**Paso 4:** agregar la aplicación al Asistente para crear suscripción de Microsoft Intune.|Para obtener más información, consulte [Set up Windows Phone and Windows 10 Mobile hybrid device management with System Center Configuration Manager and Microsoft Intune](../../mdm/deploy-use/enroll-hybrid-windows.md) (Configurar la administración de dispositivos híbridos de Windows Phone y Windows 10 Mobile con System Center Configuration Manager y Microsoft Intune).|  
|**Paso 5**: eliminar la implementación que se crea automáticamente cuando se agrega la aplicación de portal de empresa al Asistente para crear suscripción de Microsoft Intune.|La suscripción a Microsoft Intune ha creado una implementación automática de esta aplicación, ya que la implementación no admite la sustitución.|  
|**Paso 6:** crear una nueva implementación de la aplicación. En la página **Configuración de implementación** del **Asistente para implementar software**, active **Actualizar automáticamente cualquier versión reemplazada de esta aplicación**.|Cree una nueva implementación con sustitución mediante la aplicación creada con la relación de sustitución.|  
|**Paso 7 (opcional):** de manera predeterminada, las aplicaciones de sustitución se instalan en los dispositivos después de 7 días. Para implementar la aplicación del portal de la compañía en dispositivos inscritos previamente más pronto, asigne un valor menor a la opción **Programar la reevaluación para implementaciones** .<br /><br /> Si establece esta opción en un valor inferior al predeterminado, podría afectar negativamente al rendimiento de la red y los equipos cliente.|No hay información adicional.|  



<!--HONumber=Dec16_HO1-->


