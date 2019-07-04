---
title: Solución de problemas de integración de Lookout
titleSuffix: Configuration Manager
description: En este tema se describen los problemas que se producen normalmente con la integración de Lookout.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e36b98c7-d0f4-4dd6-bac3-6a6c4b4bf841
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9066983e631e1444cccb7b8c686c5b31e6fcf096
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67551446"
---
# <a name="troubleshoot-lookout-integration-with-intune"></a>Solucionar problemas de integración de Lookout con Intune

*Se aplica a: System Center Configuration Manager (Rama actual)*

## <a name="troubleshoot-login-errors"></a>Solucionar los errores de inicio de sesión
### <a name="403-errors"></a>Errores 403
Puede ver un error 403 cuando inicie sesión en la [consola de Lookout MTP](https://aad.lookout.com): **No está autorizado a acceder al servicio**. Esto puede suceder cuando el nombre de usuario que ha especificado no es un miembro del grupo de Azure Active Directory (Azure AD) que está configurado para tener acceso a Lookout MTP.

Lookout MTP está configurado para permitir que solo tengan acceso los usuarios de un grupo de Azure AD configurado. Si no está seguro de qué grupo está configurado para acceder a Lookout MTP, póngase en contacto con el soporte técnico de Lookout.

Puede ponerse en contacto con el soporte técnico de Lookout de las siguientes maneras:

* Correo electrónico: enterprisesupport@lookout.com
* Inicie sesión en la [Consola de MTP](http://aad.lookout.com) y vaya al módulo **Soporte técnico**.
* Vaya a: https://enterprise.support.lookout.com/hc/requests y realice una solicitud de soporte técnico.

### <a name="unable-to-sign-in"></a>No se puede iniciar sesión
Puede que vea el siguiente error cuando el usuario de administrador global de Azure AD no ha aceptado la configuración inicial de Lookout.

![captura de pantalla de la pantalla de inicio de sesión de Lookout que muestra un error de inicio de sesión](media/lookout-consent-not-accepted-error.png)

Para resolver este problema, el usuario administrador global debe iniciar sesión en https://aad.lookout.com/les?action=consent y aceptar la solicitud para iniciar la configuración. Puede encontrar más información detallada en el tema [Set up your subscription with Lookout MTP (Configurar su suscripción con Lookout MTP)](set-up-your-subscription-with-lookout.md).

## <a name="troubleshoot-device-status-issues"></a>Solución de problemas del estado del dispositivo

### <a name="device-not-showing-up-in-the-lookout-mtp-console-device-list"></a>El dispositivo no aparece en la lista de dispositivos de la consola de Lookout MTP

Esto puede suceder en alguno de los siguientes escenarios:
* Cuando el usuario propietario de este dispositivo no está en el **Grupo de inscripción** especificado en la **Consola de Lookout MTP**.  En el módulo **Sistema**, vaya a la pestaña **Conector de Intune** y busque la opción **Administración de inscripciones**.  Debe ver uno o más grupos de Azure AD configurados para la inscripción.  Compruebe que el usuario propietario del dispositivo que falta forma parte de uno de los grupos especificados de Azure AD.  Una vez que se haya agregado el usuario al grupo de inscripción verá el dispositivo en el intervalo de sondeo configurado (5 minutos es el valor predeterminado) en el módulo **Dispositivos** de la consola de Lookout MTP.

* Si el dispositivo no es compatible con Lookout MTP.  Los dispositivos que no son compatibles aparecerán en la sección **Dispositivos administrados** de la configuración del conector en la consola de Lookout MTP.

### <a name="device-continues-to-be-reported-as-pending"></a>El dispositivo sigue apareciendo como **pendiente**

Si un dispositivo se muestra como **Pendiente** significa que el usuario final no ha abierto la aplicación Lookout for Work y no ha pulsado el botón **Activar**. Para obtener más información sobre la activación de dispositivos con la aplicación Lookout for Work, lea el siguiente tema:

[Se le pide que instale Lookout for Work en un dispositivo Android](https://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

### <a name="in-the-lookout-mtp-console-a-device-is-showing-as-active-but-does-not-have-a-device-id"></a>En la consola de Lookout MTP, un dispositivo se muestra como activo, pero no tiene un id. de dispositivo.
Esto significa que el usuario propietario de este dispositivo no está en el grupo de inscripción, especificado en la consola de Lookout MTP.   Un dispositivo puede encontrarse en este estado si el usuario propietario del dispositivo se ha quitado del grupo de inscripción o el grupo al que pertenece el usuario se ha eliminado.

En el módulo **Sistema** de la consola de Lookout MTP, vaya a la pestaña **Conector de Intune** y revise la configuración de **Inscripción**.  Debe ver uno o más grupos de Azure AD configurados para la inscripción.  Compruebe que el usuario propietario del dispositivo forma parte de uno de los grupos especificados de Azure AD.

Aunque un dispositivo se encuentre en este estado, Lookout seguirá notificando a los usuarios cualquier amenaza que detecte, pero no enviará ninguna información sobre amenazas a Intune.

### <a name="device-shows-disconnected-state"></a>El dispositivo muestra el estado Desconectado

Desconectado significa que Lookout MTP no ha tenido noticias del dispositivo durante más tiempo que el que marca el intervalo preconfigurado (el valor predeterminado es 30 días con un mínimo de 7 días). Esto significa que la aplicación de portal de empresa o la aplicación Lookout for Work no está instalada en el dispositivo o se ha desinstalado. El problema se resolverá volviendo a instalar las aplicaciones. Cuando el usuario abre Lookout for Work y activa la aplicación, el dispositivo se vuelve a sincronizar con Lookout MTP e Intune.

### <a name="forcing-a-resync-on-the-device"></a>Forzar una nueva sincronización en el dispositivo
Desde el módulo **Dispositivos** de la consola de Lookout MTP, el administrador puede seleccionar el dispositivo y decidir eliminarlo.   La próxima vez que el propietario del dispositivo abra la aplicación Lookout for Work y pulse **Activar**, el estado del dispositivo realizará una resincronización completa.

### <a name="the-owner-of-the-device-is-no-longer-using-this-device"></a>El propietario del dispositivo ya no usa este dispositivo
Debe borrar el dispositivo y solicitar al nuevo usuario que lo inscriba como se describe en [este tema](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#full-wipe).


También puede ir al módulo **Dispositivos** de la consola de Lookout MTP y pulsar **Eliminar**.

Siempre que el usuario nuevo se encuentre en uno de los grupos de inscripción especificados en la consola de Lookout MTP, el dispositivo aparecerá una vez que Azure AD asocie el dispositivo al usuario nuevo.

## <a name="compliance-remediation-workflows"></a>Flujos de trabajo de corrección de cumplimiento
[Se le pide que instale Lookout for Work en un dispositivo Android]( https://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

[Debe solucionar una amenaza detectada por Lookout for Work en el dispositivo Android](https://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)
