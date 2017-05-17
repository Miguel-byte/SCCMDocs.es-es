---
title: Inscribir dispositivos propiedad de la empresa en Configuration Manager | Microsoft Docs
description: "Obtenga información sobre los diferentes métodos para inscribir dispositivos de empresa para implementaciones híbridas con Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2754ce6-1460-4ddd-9050-2cc87e7964f4
caps.latest.revision: 13
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: f0b503d8c9eba2dd1b6eb4c41ec40c001b727326
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017


---
# <a name="enroll-company-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Inscribir dispositivos de empresa para implementaciones híbridas con Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los dispositivos de empresa (COD) o de la organización se pueden incorporar a la administración de varias maneras, según el dispositivo y la manera en que se adquirió.  

## <a name="enroll-device-enrollment-program-ios-devices"></a>Inscribir dispositivos iOS mediante el Programa de inscripción de dispositivos  
 Implementa un perfil de inscripción "de forma inalámbrica" en los dispositivos que se adquirieron a través del Programa de inscripción de dispositivos de Apple. Cuando el usuario ejecuta el Asistente de configuración en el dispositivo, este se inscribe en Intune.  Los usuarios no pueden anular la inscripción de dispositivos inscritos a través de DEP. Consulte [iOS Device Enrollment Program (DEP) enrollment for hybrid deployments with Configuration Manager](../../mdm/deploy-use/ios-device-enrollment-program-for-hybrid.md) (Inscripción del Programa de inscripción de dispositivos (DEP) iOS para implementaciones híbridas con Configuration Manager).  

## <a name="enroll-ios-devices-with-apple-configurator"></a>Inscribir dispositivos iOS con Apple Configurator  
 Este método requiere que el administrador conecte el dispositivo iOS a través de USB a un equipo Mac que ejecute Apple Configurator para preconfigurar la inscripción. Después, los dispositivos se entregan a sus usuarios, que ejecutan el proceso del Asistente de configuración, configuran el dispositivo con sus credenciales profesionales o educativas, y completan el proceso de inscripción. Consulte [iOS hybrid enrollment using Apple Configurator with Configuration Manager](../../mdm/deploy-use/ios-hybrid-enrollment-using-apple-configurator.md) (Inscripción híbrida de iOS mediante Apple Configurator con Configuration Manager).  

## <a name="device-enrollment-manager"></a>Administrador de inscripción de dispositivos  
 Las organizaciones pueden usar Intune para administrar un gran número de dispositivos móviles con una sola cuenta de usuario, denominada cuenta de administrador de inscripción de dispositivos. Después de crear la cuenta de administrador de inscripción de dispositivos, un administrador puede usarla para inscribir un número de dispositivos superior a los cinco estándar que se permiten de forma predeterminada a los usuarios normales. La inscripción de dispositivos con un administrador de inscripción de dispositivos solo funciona en el caso de los dispositivos que no son usados por un usuario específico. Estos dispositivos son buenos para aplicaciones de punto de venta o de utilidad, por ejemplo, pero inadecuados para usuarios que necesitan acceso al correo electrónico o a los recursos de empresa. Consulte [Enroll devices with device enrollment manager with Configuration Manager](../../mdm/deploy-use/enroll-devices-with-device-enrollment-manager.md) (Inscribir dispositivos con el administrador de inscripción de dispositivos con Configuration Manager).  

## <a name="user-affinity-for-managed-devices"></a>Afinidad de usuario para dispositivos administrados  
 Al configurar perfiles para dispositivos propiedad de la empresa, el administrador puede especificar si los dispositivos administrados admiten la *afinidad de usuario*, de modo que se identifique a un usuario específico con el dispositivo. Los dispositivos configurados con **user affinity** pueden instalar y ejecutar la aplicación del portal de empresa para descargar aplicaciones y administrar dispositivos. Consulte [User affinity for hybrid managed devices in Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md) (Afinidad de usuario para dispositivos administrados híbridos en Configuration Manager).  

## <a name="manage-devices-with-activation-lock"></a>Administrar dispositivos con el bloqueo de activación  
 Microsoft Intune puede ayudarle a administrar el bloqueo de activación de iOS, una característica de la aplicación Buscar mi iPhone para dispositivos iOS 7.1 y versiones posteriores. El bloqueo de activación se habilita automáticamente cuando se usa la aplicación Buscar mi iPhone en un dispositivo. Consulte [Manage iOS Activation Lock with System Center Configuration Manager](../../mdm/deploy-use/manage-ios-activation-lock.md) (Administrar el bloqueo de activación de iOS con System Center Configuration Manager).

 ## <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Declarar previamente dispositivos con números de serie de iOS o IMEI

Puede identificar los dispositivos corporativos si importa sus números de identidad internacional de equipo móvil (IMEI) o los números de serie de iOS. Puede cargar un archivo de valores separados por comas (.csv) que incluya los números IMEI de los dispositivos o escribir la información de los dispositivos de forma manual.  Consulte [Predeclare devices with hardware ID numbers](../../mdm/deploy-use/predeclare-devices-with-hardware-id.md) (Predeclarar dispositivos con números de Id. de hardware).

