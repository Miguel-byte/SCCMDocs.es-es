---
title: "Configurar la administración de dispositivos híbrida de Android con System Center Configuration Manager y Microsoft Intune"
description: "Prepárese para administrar dispositivos móviles Android con Configuration Manager e Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: 9
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fa189e812a2e3104cb337ccf40c693621745ee53


---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar la administración de dispositivos híbrida de Android con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*

Para System Center Configuration Manager, los usuarios pueden descargar la aplicación de portal de empresa de Android mediante Google Play para inscribir dispositivos Android (incluido Samsung KNOX). La aplicación del portal de la compañía de Android le permite administrar la configuración de cumplimiento, borrar o eliminar dispositivos Android, implementar aplicaciones y recopilar el inventario de hardware y software. Si la aplicación del portal de la compañía de Android no está instalada en los dispositivos Android, no dispondrá de todas las características de administración como, por ejemplo, la configuración de cumplimiento y el inventario, pero podrá implementar aplicaciones en dispositivos Android.  

## <a name="prepare-to-manage-android-mobile-devices-with-configuration-manager-and-intune"></a>Prepararse para administrar dispositivos móviles Android con Configuration Manager e Intune  
 Los pasos siguientes permiten que Configuration Manager administre dispositivos Android.  

#### <a name="to-enable-android-enrollment"></a>Cómo habilitar la inscripción de Android  

1.  **Requisitos previos**: para poder configurar la inscripción en cualquier plataforma, complete los requisitos previos y los procedimientos de [Setup hybrid MDM](setup-hybrid-mdm.md) (Configurar la MDM híbrida).  

2.  En la consola de Configuration Manager, en el área de trabajo **Administración** , vaya a **Servicios en la nube** > **Suscripción a Microsoft Intune**.  

3.  En la pestaña **Inicio** del grupo **Suscripción** , haga clic en **Configurar plataformas** > **Android**.  

4.  En el cuadro de diálogo **Propiedades de suscripción a Microsoft Intune** , seleccione la pestaña **Android** y haga clic para seleccionar la casilla **Habilitar la inscripción de Android** .  

 Cuando esté listo, necesitará que los usuarios sepan cómo inscribir sus dispositivos. Consulte [Qué decirles a los usuarios finales sobre el uso de Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Esta información se aplica a Microsoft Intune y a dispositivos móviles administrados por Configuration Manager.



<!--HONumber=Nov16_HO1-->


