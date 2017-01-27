---
title: Configurar e implementar aplicaciones Lookout for Work | Microsoft Docs
description: "Instrucciones para configurar e implementar la aplicación Lookout for Work para dispositivos Android e iOS."
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dfdbfee6-4b9b-4d53-816a-62bbc3a43b6e
caps.latest.revision: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fa837c68eb073d2ceaf48c938137a94141a102e
ms.openlocfilehash: 5e7d67855dc7929b19ec1ae32457aa11700be56e


---
# <a name="deploy-lookout-for-work-apps"></a>Implementar aplicaciones Lookout for Work

*Se aplica a: System Center Configuration Manager (rama actual)*

En este artículo se explica cómo configurar e implementar la aplicación Lookout for Work para los dispositivos Android e iOS.

## <a name="android-google-play-store-app"></a>Android (aplicación Google Play Store)
1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.

2.  En la página **General** del Asistente para implementar software, especifique la información siguiente:
  * Tipo: seleccione **Paquete de aplicaciones para Android en Google Play**.
  * Ubicación: copie el vínculo de la aplicación de Lookout for Work desde Google Play Store y péguelo aquí
  * Publicador: Lookout Mobile Security
  * Nombre: Lookout for Work
  * Descripción: Lookout ofrece la mejor protección contra amenazas móviles para proteger el dispositivo. Cuando se instala la aplicación Lookout en el dispositivo, lo protege de amenazas y avisa, tanto a usted como al administrador de la empresa, si detecta alguna.
  * Categoría administrativa: administración de equipos

  Después de completarse correctamente, ahora verá la aplicación Lookout for Work en su lista de aplicaciones.

3.  En la pestaña **Inicio**, en el grupo **Implementación**, pulse **Implementar** para implementar la aplicación Lookout for Work para los usuarios.
>[!IMPORTANT]
>Debe seleccionar los mismos usuarios que ha agregado en la opción Administración de la inscripción en la consola MTP de Lookout.

  Seleccione la opción **Instalación requerida** para exigir que la aplicación Lookout se instale en el dispositivo del usuario.

## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (versión para empresa de la aplicación Lookout)

* **Paso 1:** Asegúrese de que la **administración de iOS** está configurada en el dispositivo. Para obtener instrucciones sobre cómo configurar el dispositivo para la administración de iOS, consulte [Configurar la administración de dispositivos iOS y Mac]().

* **Paso 2:** **Vuelva a firmar** la aplicación Lookout for Work de iOS. Lookout distribuye su aplicación Lookout for Work de iOS fuera de la tienda App Store de iOS. **Antes de distribuir la aplicación**, deberá volver a firmar la aplicación con su certificado de desarrollador empresarial de iOS. Para obtener instrucciones sobre cómo volver a firmar las aplicaciones Lookout for Work de iOS, consulte el [proceso de volver a firmar la aplicación Lookout for Work de iOS](https://personal.support.lookout.com/hc/en-us/articles/114094038714) en el sitio de Lookout.


* **Paso 3:** Habilite la autenticación de Azure Active Directory para los usuarios de iOS haciendo lo siguiente:
  1.  Inicie sesión en el [Portal de administración de Azure Active Directory](https://manage.windowsazure.com) y vaya a la página de aplicación.
  2.  Agregue la **aplicación Lookout for Work de iOS** como una **aplicación de cliente nativo**.
  ![captura de pantalla del cuadro de diálogo Agregar aplicaciones que muestra la opción de aplicación de cliente nativo](../media/aad-add-app.png)

  3. Reemplace **com.lookout.enterprise.yourcompanyname** por el id. de agrupación del cliente que ha seleccionado al registrar el IPA.
  4.  Agregue un URI de redireccionamiento adicional: **&lt;companyportal://code/>** seguido de una versión con codificación URL del URI de redireccionamiento original.
  5.  Agregue los **permisos delegados** a la aplicación.

  Para obtener más información, consulte [Configurar una aplicación de cliente nativo](https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application).


* **Paso 4:** Cargue el archivo .ipa que se ha vuelto a firmar como se describe en el tema [Crear aplicaciones iOS con System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/apps/get-started/creating-ios-applications). Establezca la versión mínima del sistema operativo en iOS 8.0 o posterior.


* **Paso 5:** Cree la directiva de configuración de la aplicación administrada, tal como se describe en el tema [Configurar aplicaciones iOS con directivas de configuración de aplicaciones móviles en System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).


* **Paso 6:** **Para implementar la aplicación a los usuarios**, seleccione la aplicación Lookout for Work en la página **Aplicaciones** de la pestaña **Inicio**, en el grupo **Implementación** y pulse **Implementar**.

  Debe seleccionar los mismos usuarios que ha agregado en la opción Administración de la inscripción en la consola de Lookout.  
Seleccione la opción **Instalación requerida** para exigir que la aplicación Lookout se instale en el dispositivo del usuario.

## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>¿Qué ocurre cuando se abre la aplicación implementada en el dispositivo?




Cuando el usuario abre Lookout for Work en el dispositivo, se le pide que active la aplicación y que seleccione la opción Iniciar sesión con Azure Active Directory. En los temas siguientes encontrará un tutorial detallado con el flujo para el usuario final:

* [Se le pide que instale Lookout for Work en un dispositivo Android](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

* [Debe solucionar una amenaza detectada por Lookout for Work en el dispositivo Android](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

## <a name="next-steps"></a>Pasos siguientes
* [Habilitar la regla de protección contra amenazas de dispositivo en la directiva de cumplimiento](enable-device-threat-protection-rule-compliance-policy.md)



<!--HONumber=Jan17_HO4-->


