---
title: Configuración de la administración de dispositivos híbridos de Android con Microsoft Intune
titleSuffix: Configuration Manager
description: Prepárese para administrar dispositivos móviles Android con Configuration Manager e Intune.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fb488ccfc186fcc56ea91c30b6c0319aead5208e
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416986"
---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar la administración de dispositivos híbrida de Android con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*

En este artículo se explica cómo habilitar la inscripción híbrida de dispositivos Android y Android for Work. Se puede usar Configuration Manager para administrar los dispositivos a través de una suscripción a Microsoft Intune configurada. Mediante Google Play, los usuarios pueden descargar la aplicación del portal de empresa de Android para inscribir dispositivos Android (incluido Samsung KNOX Standard) y Android for Work.

Con Configuration Manager, se puede administrar la configuración de cumplimiento, borrar o eliminar dispositivos Android, implementar aplicaciones y recopilar el inventario de software y hardware. Si la aplicación del Portal de empresa de Android no está instalada en el dispositivo, no dispondrá de las funcionalidades de administración (como la configuración de cumplimiento y el inventario), pero podrá implementar aplicaciones en dispositivos Android.  



## <a name="enable-android-enrollment"></a>Habilitar la inscripción de Android  
Los pasos siguientes permiten a Configuration Manager administrar dispositivos Android sin un perfil de trabajo (es decir, la inscripción a "Android clásico").

1. Para poder configurar la inscripción en cualquier plataforma, complete los requisitos previos y los procedimientos de [Configurar la administración híbrida de dispositivos móviles (MDM)](setup-hybrid-mdm.md).  
2. En la consola de Configuration Manager, en el área de trabajo **Administración**, seleccione **Información general** > **Cloud Services** > **Suscripción a Microsoft Intune** y elija la suscripción a Intune correspondiente.  
3. En la pestaña **Inicio** del grupo **Suscripción**, seleccione **Configurar plataformas** > **Android**.  
4. En el cuadro de diálogo **Propiedades de la suscripción a Microsoft Intune**, seleccione la pestaña **Android** y active el cuadro **Habilitar la inscripción de Android**. Puede elegir **Bloquear dispositivos de propiedad personal** para limitar la inscripción a [Dispositivos declarados previamente](predeclare-devices-with-hardware-id.md).

   Cuando esté listo, necesitará que los usuarios sepan cómo inscribir sus dispositivos. Consulte [Qué decirles a los usuarios finales sobre el uso de Microsoft Intune](/intune/end-user-educate). Esta información se aplica a Microsoft Intune y a dispositivos móviles administrados por Configuration Manager.



## <a name="enable-android-for-work-enrollment"></a>Habilitar la inscripción de Android for Work
Los pasos siguientes permiten a Configuration Manager administrar dispositivos Android sin un perfil de trabajo.

1. [Cree una cuenta de Google](https://accounts.google.com/SignUp) para usarla como cuenta de administrador de Android for Work. También puede iniciar sesión con la cuenta asociada con todas las tareas de administración de Android for Work para este inquilino de Intune. Podría ser una cuenta de Google que se comparte entre los administradores que administran dispositivos Android. Esta cuenta es la cuenta de Google que su organización usa para administrar y publicar aplicaciones en la consola de Play for Work. Esta cuenta se usa para aprobar aplicaciones en la tienda de Play for Work, por lo que debe realizar el seguimiento del nombre y la contraseña de la cuenta.
2. Habilite la inscripción de Android. Para ello, enlace la cuenta de Google con el inquilino de Intune administrado en Configuration Manager:
   1. En la consola de Configuration Manager, en el área de trabajo **Administración**, seleccione **Información general** > **Cloud Services** > **Suscripciones a Microsoft Intune** y elija la suscripción a Intune correspondiente.
   2. En la pestaña **Inicio** del grupo **Suscripción**, seleccione **Configurar plataformas** > **Android for Work**.
   3. En el cuadro de diálogo, seleccione **Configurar Android for Work en la consola Intune**. Se abre la consola de Intune en el explorador web.
   4. Use sus credenciales de administrador de Intune para iniciar sesión en el portal de Intune o de Azure.
   5. Haga clic en **Google Play administrado**. 
       1. Seleccione **Acepto** para conceder permiso a Microsoft para [enviar información del usuario y del dispositivo a Google](/intune/data-intune-sends-to-google).
       2. Seleccione **Iniciar Google para conectarse ahora** para abrir el sitio web de Android for Work en Google Play. El sitio web se abre en una pestaña nueva del explorador.
       3. En la página de inicio de sesión de Google, escriba la cuenta de Google del paso 1.
       4. Especifique el nombre de su empresa en **Nombre de la organización**. En **Proveedor de administración de Enterprise Mobility (EMM)**, debería mostrarse "Microsoft Intune". 
       5. Acepte el contrato de Android for Work y, después, haga clic en **Confirmar**. La solicitud se procesará.

   6. En la página de inicio de sesión de Google, escriba las credenciales de la cuenta de Google del paso 1 y después proporcione la información de su empresa.
3. Cuando vuelva a Intune en Azure Portal, vaya a la hoja de inscripción de **Android for Work** y haga clic en **Perfiles de trabajo**. Android for Work ya está habilitado. Hay dos opciones de inscripción para los dispositivos de Android for Work:
   - **Administrar todos los dispositivos como Android** (deshabilitado). Todos los dispositivos Android se inscribirán como dispositivos Android convencionales, incluidos los dispositivos que admiten Android for Work.
   - **Administrar dispositivos compatibles como Android for Work** (habilitado). Todos los dispositivos que admiten Android for Work se inscriben como dispositivos Android for Work. Todo dispositivo Android que no admita Android for Work se inscribe como dispositivo Android convencional.

> [!NOTE]
> Un problema conocido impide que la opción **Administrar los dispositivos compatibles para usuarios solo en estos grupos como Android for Work** funcione según lo esperado. Los dispositivos de los usuarios en los grupos de Azure AD especificados se inscriben como Android en lugar de Android for Work. Para habilitar Android for Work, debe usar la opción **Manage supported devices as Android for Work** (Administrar dispositivos compatibles como Android for Work).


Cuando esté listo, indíqueles a los usuarios cómo deben inscribir sus dispositivos. Consulte [Qué decirles a los usuarios finales sobre el uso de Microsoft Intune](/intune/end-user-educate). Esta información se aplica a Microsoft Intune y a dispositivos móviles administrados por Configuration Manager.

Verá el nombre de la cuenta y el nombre de la organización en el portal de Intune o de Azure cuando se complete el enlace. En ese momento, podrá cerrar los dos exploradores.

### <a name="enroll-an-android-for-work-device"></a>Inscribir un dispositivo Android for Work
La forma en que los usuarios inscriben dispositivos Android for Work es similar a la inscripción para Android. Los usuarios pueden descargar e instalar la aplicación Portal de empresa para Android en los dispositivos móviles. La aplicación les pide que creen un perfil de trabajo como parte del proceso de inscripción. Una vez creado el perfil de trabajo, los usuarios deben cambiar a la versión administrada del portal de empresa. El portal de empresa administrado se etiqueta con un pequeño maletín de color naranja en la esquina inferior derecha.

### <a name="manage-android-for-work-devices"></a>Administración de dispositivos Android for Work
Una vez habilitada la inscripción de Android for Work, puede realizar las siguientes tareas de administración para los dispositivos Android for Work:
- [Aprobar aplicaciones](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Crear elementos de configuración](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Administrar la configuración de cumplimiento](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Administrar perfiles de correo electrónico](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Borrar de forma selectiva el perfil de trabajo](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
> [< Paso anterior](create-service-connection-point.md)  [Paso siguiente >](set-up-additional-management.md)
