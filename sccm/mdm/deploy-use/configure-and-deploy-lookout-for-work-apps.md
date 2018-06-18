---
title: Implementación de aplicaciones de Lookout for Work
titleSuffix: Configuration Manager
description: Configure e implemente aplicaciones Lookout for Work.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87ad7a768128cb11a1fc361c90a6eccac454a28c
ms.sourcegitcommit: 9cff0702c2cc0f214173b47ec241f7e5a40f84e6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34752597"
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Configurar e implementar aplicaciones Lookout for Work

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se explica cómo configurar e implementar la aplicación Lookout for Work para los dispositivos Android e iOS.



## <a name="android-google-play-store-app"></a>Android (aplicación de Google Play Store)
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

1. Asegúrese de que la administración de iOS está configurada en el dispositivo. Para obtener instrucciones sobre cómo configurar el dispositivo para la administración de iOS, vea [Configuración de la administración de dispositivos híbrida de iOS con System Center Configuration Manager y Microsoft Intune](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac).  

2. Vuelva a firmar la aplicación Lookout for Work de iOS. Lookout distribuye su aplicación Lookout for Work de iOS fuera de la tienda App Store de iOS. Antes de distribuir la aplicación, deberá volver a firmarla con su certificado de desarrollador empresarial de iOS. Para obtener instrucciones sobre cómo volver a firmar las aplicaciones Lookout for Work de iOS, consulte el [proceso de volver a firmar la aplicación Lookout for Work de iOS](https://personal.support.lookout.com/hc/articles/114094038714) en el sitio de Lookout.  

3. Habilite la autenticación de Azure Active Directory (Azure AD) para los usuarios de iOS.
   1.  Inicie sesión en la [hoja de Azure AD de Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) y desplácese a la página de registros de aplicaciones.  
   2.  Especifique el nombre **Aplicación iOS Lookout for Work** y seleccione **Nativa** en el tipo de aplicación.  
  ![captura de pantalla del cuadro de diálogo Agregar aplicaciones que muestra la opción de aplicación de cliente nativo](media/aad-add-app-reg.png)

   3.  Para el URI de redirección, utilice el formato `lookoutwork://com.lookout.enterprise.<yourcompanyname>`, sustituyendo `<yourcompanyname>` por el nombre de su compañía. Por ejemplo: `lookoutwork://com.lookout.enterprise.contoso`
   4. Haga clic en **Crear** para crear la aplicación. 
   5.  Abra la nueva aplicación, haga clic en **Configuración** y agregue otro URI de redirección. Utilice el formato `companyportal://code/<originalURI>`, donde `<originalURI>` es una versión con codificación URL del URI de redirección original. Por ejemplo, `companyportal://code/lookoutwork%3A%2F%2Fcom.lookout.enterprise.contoso`.
   6.  En la configuración de la aplicación, vaya a **Permisos necesarios** y haga clic en **Agregar**. Seleccione los siguientes permisos delegados:  

       | API  | Permiso  |
       |---------|---------|
       | Lookout MTP     | Acceder a Lookout MTP         |
       | Microsoft Graph     | Iniciar sesión y leer el perfil de usuario        |  

   Para más información, vea [Configurar una aplicación de cliente nativo](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#optional-configure-a-native-client-application).  


4. En Configuration Manager, cargue el archivo .ipa con la nueva firma. Establezca la versión mínima del sistema operativo en iOS 8.0 o posterior. Para obtener más información, consulte [Crear aplicaciones iOS](/sccm/apps/get-started/creating-ios-applications).   


5. Cree una directiva de configuración de aplicaciones administradas. Para obtener más información, consulte [Configuración de aplicaciones iOS con directivas de configuración de aplicaciones móviles](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  


6. Implemente la aplicación Lookout for Work para los usuarios. Para obtener más información, consulte [Deploy applications](/sccm/apps/deploy-use/deploy-applications) (Implementar aplicaciones).  

  Seleccione los mismos usuarios que ha agregado en la opción Administración de la inscripción en la consola de Lookout. Elija la opción **Instalación requerida**. Esta opción exige que la aplicación Lookout se instale en el dispositivo del usuario.



## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>¿Qué ocurre cuando se abre la aplicación implementada en el dispositivo?

Cuando el usuario abre el Lookout for Work en el dispositivo, se le solicita que active la aplicación. Debe elegir iniciar sesión con la opción de Azure AD. En los artículos siguientes encontrará un tutorial detallado con el flujo para el usuario final:

- [Se le pide que instale Lookout for Work en un dispositivo Android](/intune-user-help/you-are-prompted-to-install-lookout-for-work-android)

- [Debe solucionar una amenaza detectada por Lookout for Work en el dispositivo Android](/intune-user-help/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)



## <a name="next-steps"></a>Pasos siguientes
- [Habilitar la regla de protección contra amenazas de dispositivo en la directiva de cumplimiento](enable-device-threat-protection-rule-compliance-policy.md)
