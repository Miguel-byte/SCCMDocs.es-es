---
title: 'Inscripción de dispositivos iOS con Apple Configurator '
titleSuffix: Configuration Manager
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.date: 08/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e884b7c5d7ceca7fcb241a5bfef1832e66562d38
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/05/2019
ms.locfileid: "70378912"
---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>Inscripción híbrida de iOS híbrido con Apple Configurator con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las compañías que compran dispositivos iOS destinados para su uso por los empleados pueden administrarlos mediante Microsoft Intune. Para preparar los dispositivos iOS corporativos para la inscripción, configure un perfil de inscripción en la consola de Configuration Manager y, después, exporte la dirección URL del perfil para que Apple Configurator la use. Prepare el dispositivo iOS para la inscripción conectándolo a un equipo Mac con un cable USB y use Apple Configurator para configurarlo. Apple Configurator restablece la configuración de fábrica del dispositivo y agrega el perfil de inscripción de manera que el dispositivo pueda inscribirse cuando el usuario lo encienda por primera vez y se desplace a través del proceso del Asistente de configuración.

El siguiente procedimiento está recomendado para dispositivos iOS dedicados que tendrán un único usuario que emplea el dispositivo para tener acceso al correo electrónico de la empresa y a recursos corporativos, como aplicaciones y datos.  

## <a name="prerequisites"></a>Requisitos previos  

-   Acceso físico a dispositivos iOS  

-   Números de serie del dispositivo: [cómo obtener un número de serie de iOS](https://support.apple.com/en-us/HT204308)  

-   Equipo Mac con [Apple Configurator 2.0](https://go.microsoft.com/fwlink/?LinkId=518017)  

-   Cables USB para conectar los dispositivos al equipo Mac  

## <a name="add-a-corporate-owned-device-enrollment-profile"></a>Agregar un perfil de inscripción de dispositivos corporativos

1.  En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Información general** > **Todos los dispositivos corporativos** > **iOS** > **Perfiles de inscripción**. Haga clic en **Crear perfil** para abrir el Asistente para crear el perfil. Establezca la configuración en las siguientes páginas:  

2.  En la página **General** , especifique la siguiente información:  

    -   **Nombre** (No es visible para los usuarios)  

    -   **Descripción** (No es visible para los usuarios)  

    -   **Afinidad de usuario** : especifica cómo se inscriben los dispositivos. En la mayoría de los escenarios del Asistente de configuración, use **Solicitar afinidad de usuarios**.  

        -   **Solicitar afinidad de usuario**: El dispositivo debe estar afiliado a un usuario durante la instalación inicial y, a continuación, se le puede permitir el acceso a los datos y al correo electrónico de la empresa como dicho usuario.  

        -   **Sin afinidad de usuario**: El dispositivo no está afiliado a un usuario. Utilice esta afiliación para dispositivos que realizan tareas sin tener acceso a datos de usuario local. Las aplicaciones que requieren la afiliación de un usuario no funcionarán.

    Haga clic en **Siguiente** para continuar.  

3.  En la página **Programa de inscripción de dispositivos**, deje la casilla **Configurar ajustes del programa de inscripción de dispositivos de este perfil** desactivada y haga clic en **Siguiente**.  

4.  Revise el resumen y, después, haga clic en **Siguiente** para crear el perfil de inscripción. Para finalizar el asistente, haga clic en **Cerrar**. Ahora está listo para agregar números IMEI o números de serie a los dispositivos que quiere inscribir.  

## <a name="predeclare-devices-to-enroll-with-setup-assistant"></a>Predeclarar los dispositivos para su inscripción con el Asistente de configuración

En este paso, predeclare los dispositivos como corporativos proporcionando una lista de identificadores de hardware (IMEI o números de serie).

Para obtener más información, consulte [Predeclare devices with IMEI and iOS serial number (Predeclarar dispositivos con IMEI y números de serie de iOS)](predeclare-devices-with-hardware-id.md). Cuando haya terminado con esa tarea, vuelva a la página para seguir con el siguiente paso.

## <a name="export-the-profile-to-deploy-to-ios-devices"></a>Exportar el perfil que se va a implementar en dispositivos iOS

1.  En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Información general** > **Todos los dispositivos corporativos** > **iOS** > **Perfiles de inscripción**.

2.  Seleccione el perfil de inscripción que se va a implementar en los dispositivos móviles y haga clic en **Exportar...** .

3.  Copie y guarde la **URL de perfil** en un archivo que pueda editar.   

4.  Para admitir Apple Configurator 2, se debe editar la URL de perfil 2.0. Reemplace la siguiente parte de la dirección URL:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     with  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  Guarde la dirección URL de perfil editada. La usará para agregar la dirección URL de perfil de inscripción en Apple Configurator en la [siguiente sección](#prepare-the-device-with-apple-configurator).  

> [!NOTE]
> La dirección URL del perfil de inscripción es válida durante dos semanas desde que se exporta. Después de dos semanas, debe exportar una nueva dirección URL para inscribir dispositivos iOS.

## <a name="prepare-the-device-with-apple-configurator"></a>Preparación del dispositivo con Apple Configurator

Para preparar los dispositivos iOS para la inscripción, conecte cada dispositivo a un equipo Mac y cargue el perfil de inscripción en este.  

> [!WARNING]  
>  Apple Configurator borra y restablece los dispositivos a la configuración de fábrica.  

1. En un equipo Mac, abra **Apple Configurator 2**.  

2. En la barra de menús, haga clic en **Apple Configurator 2** > **Preferencias**.  

3. En el panel de preferencias, seleccione **Servers** (Servidores) y haga clic en el símbolo "+" debajo del panel izquierdo para iniciar el asistente del servidor MDM. Haga clic en **Next**.  

4. Escriba el **Nombre** y la **URL de inscripción** que ha guardado [antes](#export-the-profile-to-deploy-to-ios-devices). Haga clic en **Next**.  

   > [!NOTE]
   > Si recibe una advertencia sobre los requisitos de perfil de confianza para Apple TV, puede cancelar con seguridad la opción **Trust Profile (Perfil de confianza)** haciendo clic en la "X" de color gris. También de forma segura, puede omitir cualquier advertencia de marcador de certificado.

   Para continuar, haga clic en **Next** (Siguiente) hasta que finalice el asistente.  

5. En el panel **Servers** (Servidores), haga clic en "Edit" (Editar) junto a perfil del nuevo servidor. Asegúrese de que la dirección URL de inscripción coincide exactamente con la dirección URL que ha especificado anteriormente. Vuelva a escribir la dirección URL si es diferente y haga clic en **Guardar**.  

6. Con un cable USB, conecte un dispositivo iOS al equipo Mac.  

   > [!WARNING]  
   >  Este proceso restablece los dispositivos a la configuración de fábrica. Antes de conectar el dispositivo, restablezca el dispositivo y enciéndalo. Como procedimiento recomendado, en el dispositivo debe aparecer la pantalla Hello antes de continuar.  

7. Haga clic en **Prepare** (Preparar). En el panel **Prepare iOS Device (Preparar dispositivo iOS)** , seleccione **Manual** y, después, haga clic en **Siguiente**.  

8. En el panel **Enroll in MDM Server (Inscribir en servidor MDM)** , seleccione el nombre del servidor que ha creado y haga clic en **Siguiente**.  

9. En el panel **Create an Organization** (Crear una organización), elija la **organización** o cree una nueva y luego haga clic en **Next** (Siguiente).  

10. En el panel **Configure iOS Setup Assistant (Configurar Asistente de configuración de iOS)** , elija los pasos que se van a presentar al usuario y, después, haga clic en **Preparar**. Si se le solicita, autentíquese para actualizar la configuración de confianza.  

11. Cuando termine, puede desconectar el cable USB.  

Repita estos pasos en todos los dispositivos que quiera preparar para la inscripción.

## <a name="distribute-devices"></a>Distribución de los dispositivos

Los dispositivos ya están listos para la inscripción corporativa. Apague los dispositivos y distribúyalos a los usuarios. Cuando el dispositivo se encienda, se iniciará el Asistente de configuración y se solicitará al usuario su cuenta profesional o educativa para comenzar la inscripción.
