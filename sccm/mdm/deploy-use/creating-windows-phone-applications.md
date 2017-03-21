---
title: Crear aplicaciones de Windows Phone | Microsoft Docs
description: Consulte las consideraciones que debe tener en cuenta al crear e implementar aplicaciones para dispositivos de Windows Phone.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 6d5d5eb9e4bf0297e2d86bf591dab5b3f42c95fa
ms.lasthandoff: 03/06/2017


---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>Crear aplicaciones de Windows Phone con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Una aplicación de System Center Configuration Manager tiene uno o varios tipos de implementación que incluyen la información y los archivos de instalación necesarios para implementar un dispositivo. Además tiene reglas que especifican cuándo y cómo se implementa el software.  

 Puede crear aplicaciones mediante los métodos siguientes:  

-   Crear automáticamente los tipos de aplicación y de implementación mediante la lectura de los archivos de instalación de la aplicación.  

-   Crear manualmente la aplicación y, a continuación, agregar los tipos de implementación más adelante.  

-   Importe una aplicación desde un archivo.  

Consulte [Inicie el Asistente para crear aplicaciones](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) para conocer los pasos necesarios para crear aplicaciones de Configuration Manager y los tipos de implementación. Tenga en cuenta también las siguientes consideraciones cuando cree e implemente aplicaciones para dispositivos Windows Phone.  

## <a name="general-considerations"></a>Consideraciones generales  
 Configuration Manager admite la implementación de los siguientes tipos de archivo de aplicaciones:  

|Tipo de dispositivo|Tipos de archivo compatibles|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8,1|.xap, .appx, .appxbundle|
|Windows 10 Mobile|.xap, .appx, .appxbundle|

 Se admiten las siguientes acciones de implementación:  

|Tipo de dispositivo|Acciones admitidas|  
|-----------------|-----------------------|  
|Windows Phone 8, Windows Phone 8.1 y Windows 10 Mobile|Disponible, necesario, desinstalar|  

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
