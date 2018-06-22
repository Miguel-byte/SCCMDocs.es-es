---
title: 'Configuración de la suscripción a Intune '
titleSuffix: Configuration Manager
description: Configure una suscripción de Intune para realizar el seguimiento de las licencias de la administración local de dispositivos móviles en System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: aa931c848bc3a25df452f8034530b6c740659e12
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347423"
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Configurar una suscripción de Microsoft Intune para la administración local de dispositivos móviles en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La administración local de dispositivos móviles de System Center Configuration Manager requiere una suscripción de Microsoft Intune para realizar el seguimiento de las licencias. El servicio de Intune no se usa para administrar los dispositivos ni para almacenar información de administración. Para la administración local de dispositivos móviles, la administración de dispositivos se controla mediante la infraestructura de Configuration Manager.  

> [!NOTE]  
> A partir de la versión 1610, Configuration Manager admite el uso de Microsoft Intune y la infraestructura de Configuration Manager local para administrar dispositivos móviles al mismo tiempo.   

> [!TIP]  
>  Se recomienda que configure la suscripción a Intune para la administración local de dispositivos móviles antes de instalar los roles de sistema de sitio requeridos para minimizar el tiempo necesario para que los roles de sistema de sitio recién instalados puedan funcionar.  

##  <a name="sign-up-for-microsoft-intune"></a>Suscribirse a Microsoft Intune  
 Intune es obligatorio para que la administración local de dispositivos móviles funcione. Solo tiene que [registrarse](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/) para una suscripción de prueba o de pago e ir al paso siguiente para agregar la suscripción en Configuration Manager.  

##  <a name="add-the-intune-subscription-to-configuration-manager"></a>Agregar la suscripción de Intune a Configuration Manager  
 Para agregar la suscripción a Configuration Manager, siga los mismos pasos básicos que daría al agregar la suscripción para la administración de dispositivos móviles con Intune. Lea las notas siguientes para conocer las diferencias específicas y después siga las instrucciones en [Configurar la suscripción a Intune](../deploy-use/configure-intune-subscription.md).  

> [!NOTE]  
>  Al agregar la suscripción a Intune, tenga en cuenta lo siguiente:  
>   
>  -   La recopilación especificada en el Asistente para agregar suscripciones de Microsoft Intune no se usa para la delegación de derechos de usuario de la administración local de dispositivos móviles. Solo se usa para la administración de dispositivos móviles con Intune. Sin embargo, debe especificar una recopilación para que el asistente continúe.  
> -   Se omite el valor del código de sitio especificado en el asistente para la administración local de dispositivos móviles. El código de sitio que se utiliza es la que especifique en el perfil de inscripción que otorga permisos de usuario para inscribir dispositivos.  
> -   No habilite la autenticación multifactor. No se admite en la administración local de dispositivos móviles.  

##  <a name="configure-the-intune-subscription-for-on-premises-mobile-device-management"></a>Configurar la suscripción a Intune para la administración local de dispositivos móviles  

1.  En la consola de Configuration Manager, haga clic con el botón derecho en **Suscripción a Microsoft Intune** y haga clic en **Propiedades**.  

2.  En el cuadro Administración de dispositivos móviles locales, seleccione una de las opciones siguientes:

  - Si planea tener solo dispositivos administrados localmente, active la casilla que aparece junto a **Only manage devices on-premises** (Solo administrar dispositivos locales) y haga clic en **Aceptar**.  

      > [!NOTE]  
      >  Si hace clic en esta casilla, configurará la suscripción a Intune para que mantenga toda la información de administración de forma local y no replique los datos en la nube.  

    - Si planea tener dispositivos administrados por Intune y Configuration Manager localmente, deje la casilla desactivada.

3.  Si planea administrar dispositivos con Windows 10 Mobile, haga clic con el botón secundario en **Suscripción a Microsoft Intune**, haga clic en **Configurar plataformas**y, a continuación, haga clic en  **Windows Phone**.  

4.  Haga clic en la casilla de verificación junto a **Windows Phone 8.1 y Windows 10 Mobile**, y, a continuación, haga clic en **Aceptar**.  

5.  Si planea administrar equipos de escritorio con Windows 10, haga clic con el botón secundario en **Suscripción a Microsoft Intune**, haga clic en **Configurar plataformas**y, a continuación, haga clic en **Habilitar la inscripción de Windows**.  

6.  Haga clic en la casilla de verificación junto a **Habilitar la inscripción de Windows**y, a continuación, haga clic en **Aceptar**.  
