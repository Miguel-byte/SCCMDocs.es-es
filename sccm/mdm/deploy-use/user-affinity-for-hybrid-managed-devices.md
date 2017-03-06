---
title: "Afinidad de usuario para dispositivos administrados híbridos en Configuration Manager | Microsoft Docs"
description: Configure la afinidad de usuario para dispositivos administrados en Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5d520a7-e9e5-40ee-91f9-f2684214beb6
caps.latest.revision: 6
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 74dcc0f4e680893db804956615248b7e1230d2b5
ms.lasthandoff: 12/16/2016

---
# <a name="user-affinity-for-hybrid-managed-devices-in-configuration-manager"></a>Afinidad de usuario para dispositivos administrados híbridos en Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Al configurar perfiles para dispositivos propiedad de la empresa, el administrador puede especificar si los dispositivos administrados pueden tener *afinidad de usuario*, de modo que se identifique a un usuario específico con el dispositivo.  

##  <a name="a-namebkmkioscpa-managed-devices-with-user-affinity"></a><a name="BKMK_iOSCP"></a> Dispositivos administrados con afinidad de usuario  
 Los dispositivos configurados con **user affinity** pueden instalar y ejecutar la aplicación del portal de empresa para descargar aplicaciones y administrar dispositivos. Cuando los usuarios reciben sus dispositivos, deben realizar una serie de pasos adicionales para completar el Asistente para la instalación e instalar la aplicación del Portal de empresa.  

#### <a name="how-to-enroll-ios-devices-with-user-affinity"></a>Inscripción de dispositivos iOS con la afinidad de usuario  

1.  Cuando los usuarios encienden por primera vez su dispositivo nuevo, se les pide que completen el Asistente para la instalación. El perfil de inscripción puede especificar que se soliciten las credenciales durante la instalación. Los usuarios deben usar las credenciales (es decir, el nombre único personal o UPN) asociadas con su suscripción en Intune.  

2.  Durante la instalación, también se les puede pedir a los usuarios un identificador de Apple. El identificador de Apple debe proporcionarse antes de que el dispositivo instale el portal de empresa. Los usuarios también pueden proporcionar el identificador de Apple cuando finalice la instalación desde el menú **Configuración** de iOS.  

3.  Tras completar la instalación, el dispositivo iOS debe instalar la aplicación de portal de empresa desde App Store, por ejemplo, la [aplicación de portal de empresa](https://itunes.apple.com/us/app/id719171358).  

4.  El usuario puede ahora iniciar sesión en el portal de empresa con el UPN que usó al configurar el dispositivo.  

5.  Después de iniciar sesión, se pide al usuario que inscriba el dispositivo. El primer paso es **identificar su dispositivo**. La aplicación presenta una lista de dispositivos iOS que están inscritos en la empresa y que se han asignado a la cuenta de Intune del usuario final. Elija el dispositivo que corresponda.  

     Si este dispositivo no está inscrito en la empresa, seleccione "nuevo dispositivo" para continuar con el flujo de inscripción estándar.  

6.  En la siguiente pantalla, el usuario debe confirmar la serie del nuevo dispositivo. El usuario puede pulsar en el vínculo "confirmar el número de serie" para iniciar la aplicación de configuración para comprobar el número de serie. El usuario debe especificar los últimos cuatro caracteres del número de serie en la aplicación del Portal de empresa.  

     Este paso comprueba que el dispositivo es el dispositivo de empresa inscrito en Intune. Si el número de serie del dispositivo no coincide, significa que se ha seleccionado el dispositivo equivocado. Vuelva a la pantalla anterior y seleccione un dispositivo diferente.  

7.  Después de comprobar el número de serie, la aplicación del Portal de empresa redirige al sitio web del Portal de empresa para finalizar la inscripción y luego pide al usuario que vuelva a la aplicación.  

8.  La inscripción ya se ha completado. Ahora puede usar este dispositivo con el conjunto completo de funcionalidades.  

##  <a name="a-namebkmknouaa-managed-devices-without-user-affinity"></a><a name="BKMK_noUA"></a> Dispositivos administrados sin afinidad de usuario  
 Los dispositivos configurados con **no user affinity** no admiten el portal de empresa y no deben instalar la aplicación. El Portal de empresa está diseñado para usuarios que tienen credenciales corporativas y que necesitan acceso a recursos corporativos personalizados (por ejemplo, correo electrónico). Los dispositivos inscritos **sin afinidad de usuario** no están diseñados para tener un inicio de sesión de usuario dedicado. Los quioscos, puntos de venta (POS) y dispositivos de utilidad compartida son casos de uso típicos de dispositivos inscritos sin afinidad de usuario. En caso de que la afinidad de usuario sea un requisito, asegúrese de que el perfil de inscripción del dispositivo tenga seleccionada la **afinidad de usuario** antes de inscribirlo. Para cambiar el estado de afinidad en un dispositivo, debe cancelar su inscripción y realizarla de nuevo.

