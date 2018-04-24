---
title: Implementación de aplicaciones de Lookout for Work
titleSuffix: Configuration Manager
description: Configure e implemente aplicaciones Lookout for Work.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
caps.latest.revision: ''
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 01c388377948ab362d60951cb8398a9276e668fb
ms.sourcegitcommit: a19e12d5c3198764901d44f4df7c60eb542e765f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Configurar e implementar aplicaciones Lookout for Work

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se explica cómo configurar e implementar la aplicación Lookout for Work para los dispositivos Android e iOS.

## <a name="android-google-play-store-app"></a>Android (aplicación Google Play Store)
1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.

2.  En la página **General** del Asistente para implementar software, especifique la información siguiente:  
    - Tipo: seleccione **Paquete de aplicaciones para Android en Google Play**.
    - Ubicación: copie el vínculo de la aplicación de Lookout for Work desde Google Play Store y péguelo aquí
    - Publicador: Lookout Mobile Security
    - Nombre: Lookout for Work
    - Descripción: Lookout ofrece la mejor protección contra amenazas móviles para proteger el dispositivo. Cuando instala la aplicación Lookout, su dispositivo queda protegido de amenazas. Si encuentra alguna amenaza, avisa al usuario y al administrador de TI.
    - Categoría administrativa: administración de equipos  

    Una vez que se completa correctamente, la aplicación Lookout for Work se muestra en la lista de aplicaciones.

3.  En la pestaña **Inicio**, en el grupo **Implementación**, pulse **Implementar** para implementar la aplicación Lookout for Work para los usuarios.   
    >[!IMPORTANT]  
    >Debe seleccionar los mismos usuarios que ha agregado en la opción Administración de la inscripción en la consola MTP de Lookout.  

    Elija la opción **Instalación requerida**. Esta opción exige que la aplicación Lookout se instale en el dispositivo del usuario.  



## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (versión para empresa de la aplicación Lookout)

- **Paso 1:** Asegúrese de que la **administración de iOS** está configurada en el dispositivo. Para obtener instrucciones sobre cómo configurar el dispositivo para la administración de iOS, vea [Configuración de la administración de dispositivos híbrida de iOS con System Center Configuration Manager y Microsoft Intune](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac).

- **Paso 2:** **Vuelva a firmar** la aplicación Lookout for Work de iOS. Lookout distribuye su aplicación Lookout for Work de iOS fuera de la tienda App Store de iOS. **Antes de distribuir la aplicación**, deberá volver a firmar la aplicación con su certificado de desarrollador empresarial de iOS. Para obtener instrucciones sobre cómo volver a firmar las aplicaciones Lookout for Work de iOS, consulte el [proceso de volver a firmar la aplicación Lookout for Work de iOS](https://personal.support.lookout.com/hc/articles/114094038714) en el sitio de Lookout.


- **Paso 3:** Habilite la autenticación de Azure Active Directory para los usuarios de iOS siguiendo estos pasos:
  1.  Inicie sesión en el [Portal de administración de Azure Active Directory](https:/portal.azure.com) y vaya a la página de la aplicación.
  2.  Agregue la **aplicación Lookout for Work de iOS** como una **aplicación de cliente nativo**.
  ![captura de pantalla del cuadro de diálogo Agregar aplicaciones que muestra la opción de aplicación de cliente nativo](media/aad-add-app.png)

  3. Reemplace **com.lookout.enterprise.yourcompanyname** por el id. de agrupación del cliente que ha seleccionado al registrar el IPA.
  4.  Agregue un URI de redireccionamiento adicional: **&lt;companyportal://code/>** seguido de una versión con codificación URL del URI de redireccionamiento original.
  5.  Agregue los **permisos delegados** a la aplicación.

  Para más información, vea [Configurar una aplicación de cliente nativo](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#optional-configure-a-native-client-application).


- **Paso 4:** Cargue el archivo .ipa que se ha vuelto a firmar como se describe en el tema [Crear aplicaciones iOS con System Center Configuration Manager](/sccm/apps/get-started/creating-ios-applications). Establezca la versión mínima del sistema operativo en iOS 8.0 o posterior.


- **Paso 5:** Cree la directiva de configuración de la aplicación administrada, tal como se describe en el tema [Configurar aplicaciones iOS con directivas de configuración de aplicaciones móviles en System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).


- **Paso 6:** **Para implementar la aplicación a los usuarios**, seleccione la aplicación Lookout for Work en la página **Aplicaciones** de la pestaña **Inicio**, en el grupo **Implementación** y elija **Implementar**.

  Seleccione los mismos usuarios que ha agregado en la opción Administración de la inscripción en la consola de Lookout. Elija la opción **Instalación requerida**. Esta opción exige que la aplicación Lookout se instale en el dispositivo del usuario.



## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>¿Qué ocurre cuando se abre la aplicación implementada en el dispositivo?

Cuando el usuario abre el Lookout for Work en el dispositivo, se le solicita que active la aplicación. Debe elegir iniciar sesión con la opción de Azure Active Directory. En los artículos siguientes encontrará un tutorial detallado con el flujo para el usuario final:

- [Se le pide que instale Lookout for Work en un dispositivo Android](/intune-user-help/you-are-prompted-to-install-lookout-for-work-android)

- [Debe solucionar una amenaza detectada por Lookout for Work en el dispositivo Android](/intune-user-help/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)



## <a name="next-steps"></a>Pasos siguientes
- [Habilitar la regla de protección contra amenazas de dispositivo en la directiva de cumplimiento](enable-device-threat-protection-rule-compliance-policy.md)
