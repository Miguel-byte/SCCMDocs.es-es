---
title: "Inscribir dispositivos iOS con el programa de inscripción de dispositivos (DEP) en Configuration Manager | Microsoft Docs"
description: "Habilite la inscripción del Programa de inscripción de dispositivos (DEP) iOS para implementaciones híbridas en Configuration Manager con Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78d44adc-9b1c-4bc6-b72d-e93873916ea6
caps.latest.revision: 9
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1b9e49da1a5bbfca93fe683b82d2c0056a22cc1f
ms.openlocfilehash: 2ace86cc842d6a3a5b2114c4e4c33c2d65c2f256
ms.lasthandoff: 03/21/2017

---
# <a name="ios-device-enrollment-program-dep-enrollment-for-hybrid-deployments-with-configuration-manager"></a>Inscripción del Programa de inscripción de dispositivos (DEP) iOS para implementaciones híbridas con Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Las empresas pueden comprar dispositivos iOS mediante el Programa de inscripción de dispositivos de Apple y, después, administrarlos mediante Microsoft Intune. Para administrar los dispositivos iOS de la empresa con el Programa de inscripción de dispositivos de Apple (DEP), las empresas deben completar los pasos de Apple para participar en el programa y adquirir los dispositivos a través de este programa. Puede consultar los detalles de este proceso en:  [https://deploy.apple.com](https://deploy.apple.com). Entre las ventajas del programa se incluye la configuración manos libres de dispositivos sin USB que permite conectar cada dispositivo a un equipo.  

 Para poder inscribir dispositivos iOS de empresa con el programa DEP, necesita un token de DEP de Apple. Este token permite a Intune sincronizar información sobre dispositivos propiedad de la empresa que participan en DEP. También permite que Intune cargue los perfiles de inscripción en Apple y asigne dispositivos a estos perfiles.  

## <a name="apple-dep-enrollment-for-ios-devices"></a>Inscripción en DEP de Apple para dispositivos iOS  
 En los siguientes procedimientos se describe cómo especificar los dispositivos iOS comprados mediante DEP de Apple como dispositivos propiedad de la empresa administrados por Intune. Cuando el usuario suministra energía por primera vez al dispositivo, recibirá el perfil de administración de DEP, ejecutará el asistente para la instalación y pasará a administrarlos.  

###  <a name="enable-dep-enrollment-in-configuration-manager-with-intune"></a>Habilitar la inscripción en DEP en Configuration Manager con Intune  

1.  **Inicio de la administración de dispositivos iOS con Configuration Manager**   
    Antes de que pueda inscribir dispositivos del Programa de inscripción de dispositivos (DEP) iOS, debe completar los pasos para [Set up Hybrid mobile device management (Configurar la administración híbrida de dispositivos móviles)](../../mdm/deploy-use/setup-hybrid-mdm.md) incluidos los [pasos para admitir la inscripción de iOS](../deploy-use/enroll-hybrid-ios-mac.md).

2.  **Crear una solicitud de token de DEP**   
    En la consola de Configuration Manager, en el área de trabajo **Administración**, expanda **Configuración de jerarquía**, expanda **Servicios de nube** y haga clic en **Suscripciones de Windows Intune**. Haga clic en **Crear una solicitud de token de DEP** en la pestaña **Inicio** , haga clic en **Examinar** para especificar la ubicación de la descarga de la solicitud de token de DEP y, a continuación, haga clic en **Descargar**. Guarde el archivo de solicitud de token de DEP (.pem) en el equipo local. El archivo .pem se usa para solicitar un token de confianza (.p7m) en el portal del programa de inscripción de dispositivos de Apple.  

3.  **Obtener un token del programa de inscripción de dispositivos**   
    Vaya al [portal del programa de inscripción de dispositivos](https://deploy.apple.com) (https://deploy.apple.com) e inicie sesión con su identificador de Apple de empresa. Este identificador de Apple debe usarse posteriormente para renovar el token de DEP.  

    1.  En la consola de [portal del programa de inscripción de dispositivos](https://deploy.apple.com), vaya a **Programa de inscripción de dispositivos** > **Administrar servidores**y, después, haga clic en **Add MDM Server**.  

    2.  Escriba el **nombre del servidor MDM**y, después, haga clic en **Siguiente**. El nombre del servidor es su referencia para identificar el servidor MDM. No es el nombre ni la dirección URL del servidor de Intune o Configuration Manager.  

    3.  Se abre el cuadro de diálogo **Agregar <NombreDeServidor\>**. Haga clic en **Elegir archivo…** para cargar el archivo .pem que creó en el paso anterior y, a continuación, haga clic en **Siguiente**.  

    4.  En el cuadro de diálogo **Agregar <NombreDeServidor\>** se muestra el vínculo **Su token de servidor**. Descargue el archivo de token de servidor (.p7m) en el equipo y, a continuación, haga clic en **Listo**.  

     Este archivo de certificado (.p7m) se usa para establecer una relación de confianza entre los servidores de Intune y los del programa de inscripción de dispositivos de Apple.  

4.  **Agregar el token de DEP a Configuration Manager**   
    En la consola de Configuration Manager, en el área de trabajo **Administración**, expanda **Configuración de jerarquía** y haga clic en **Suscripciones de Windows Intune**. Haga clic en **Configurar plataformas** en la pestaña **Inicio** y haga clic en **iOS**. Seleccione **Activar el programa de inscripción de dispositivos**, navegue hasta el archivo de certificado (.p7m), haga clic en **Abrir**, **Cargar**y **Aceptar**.  

#### <a name="set-up-enrollment-for-apple-device-enrollment-program-dep-ios-devices"></a>Configuración de inscripción para dispositivos iOS del Programa de Inscripción de Dispositivos de Apple (DEP)  

1.  **Agregar una directiva de inscripción de dispositivos corporativos**   
    En la consola de Configuration Manager, en el área de trabajo **Activos y compatibilidad**, expanda **Información general**, expanda **Todos los dispositivos corporativos**, expanda **iOS** y haga clic en **Perfiles de inscripción**. Haga clic en **Crear perfil** en la pestaña **Inicio** para abrir el Asistente para crear el perfil. Establezca la configuración en las siguientes páginas:  

    1.  On the **General** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

        -   **Nombre** : nombre del perfil de inscripción de dispositivo. (No es visible para los usuarios)  

        -   **Descripción** : descripción del perfil de inscripción de dispositivo. (No es visible para los usuarios)  

        -   **Afinidad de usuario** : especifica cómo se inscriben los dispositivos. Consulte [Afinidad de usuario para dispositivos administrados híbridos en Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md).  

            -   **Solicitar afinidad de usuario**: el dispositivo debe estar afiliado a un usuario durante la instalación inicial y, a continuación, se le puede permitir el acceso a los datos y al correo electrónico de la compañía como dicho usuario.  Se debe configurar la afinidad de usuario para dispositivos administrados por DEP que pertenecen a los usuarios y necesitan usar el Portal de empresa (por ejemplo, para instalar aplicaciones).  

            > [!NOTE]
            > DEP con afinidad de usuario requiere el punto de conexión de ADFS WS-Trust 1.3 nombreDeUsuario/Mixto para habilitarse al solicitar el token de usuario.

            -   **Sin afinidad de usuario**: el dispositivo no está afiliado a ningún usuario. Utilice esta afiliación para dispositivos que realizan tareas sin tener acceso a datos de usuario local. Las aplicaciones que requieren la afiliación de un usuario no funcionarán.  

    2.  On the **Programa de inscripción de dispositivos** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

        -   **Departamento**: esta información aparece cuando los usuarios pulsan "Acerca de la configuración" durante la activación.  

        -   **Número de teléfono de soporte técnico**: aparece cuando el usuario hace clic en el botón **Necesito ayuda** durante la activación.  

        -   **Modo de preparación**: este estado se establece durante la activación y no se puede cambiar sin restablecer el dispositivo de fábrica:  

            -   **No supervisado**: funcionalidades de administración limitadas  

            -   **Supervisado**: permite más opciones de administración y deshabilita el bloqueo de activación de manera predeterminada  

        -   **Bloquear el perfil de inscripción al dispositivo**: este estado se establece durante la activación y no se puede cambiar sin un restablecimiento de fábrica.  

            -   **Deshabilitar**: permite el perfil de administración que se va a quitar del menú **Configuración**  

            -   **Habilitar** (requiere **Modo de preparación** = **Supervisado**): deshabilita la configuración de iOS que podría permitir la eliminación del perfil de administración  

    3.  En la página **Asistente de configuración** , configure las opciones que personalizan el asistente de configuración de iOS, que se inicia al encender el dispositivo por primera vez y, a continuación, haga clic en **Siguiente**. Estas opciones incluyen:  
        -   **Código de acceso**: solicitar el código de acceso durante la activación. Siempre se requiere un código de acceso a no ser que el dispositivo vaya a protegerse o a tener el acceso controlado de alguna otra manera (es decir, el modo de quiosco restringe el dispositivo a una aplicación).  
        -   **Servicios de ubicación**: si está habilitado, el asistente de configuración solicita el servicio durante la activación  
        -   **Restaurar**: si está habilitado, el asistente de configuración solicita la copia de seguridad de iCloud durante la activación  
        -   **Id. de Apple**: se requiere un identificador de Apple para descargar las aplicaciones de iOS App Store, incluidas las instaladas mediante Intune. Si está habilitado, iOS solicitará a los usuarios un identificador de Apple cuando Intune intente instalar una aplicación sin un identificador.  
        -   **Términos y condiciones**: si está habilitado, el asistente de configuración solicita a los usuarios aceptar los términos y condiciones de Apple durante la activación  
        -   **Touch ID**: si está habilitado, el asistente para la configuración solicita este servicio durante la activación
        -   **Apple Pay**: si está habilitado, el asistente para la configuración solicita este servicio durante la activación
        -   **Zoom**: si está habilitado, el asistente para la configuración solicita este servicio durante la activación
        -   **Siri**: si está habilitado, el asistente de configuración solicita este servicio durante la activación  
        -   **Enviar datos de diagnóstico a Apple**: si está habilitado, el asistente de configuración solicita este servicio durante la activación  

    4.  En la página **Administración adicional**, especifique si una conexión USB puede usarse para la configuración de administración adicional. Al seleccionar **Requerir certificado**, debe importar un certificado de administración de Apple Configurator que se usará para este perfil.  Establezca en **No permitir** para evitar la sincronización de archivos con iTunes o la administración mediante Apple Configurator. Microsoft le recomienda establecer en **No permitir**, exportar cualquier configuración adicional de Apple Configurator y, después, implementar como un perfil de configuración iOS personalizado en lugar de usar esta configuración para permitir la implementación manual con o sin un certificado.  

        -   **No permitir**: evita que el dispositivo se comunique mediante USB (deshabilita el emparejamiento)  

        -   **Permitir**: permite que el dispositivo se comunique mediante conexión USB con cualquier equipo PC o Mac  

        -   **Requerir certificado**: permite el emparejamiento con un equipo Mac con un certificado que se ha importado al perfil de inscripción  

2.  **Asignar dispositivos DEP para la administración**   
    Vaya al [portal del programa de inscripción de dispositivos](https://deploy.apple.com) (https://deploy.apple.com) e inicie sesión con su identificador de Apple de empresa. Vaya a **Programa de implementación** > **Programa de inscripción de dispositivos** > **Administrar dispositivos**. Especifique cómo va a **elegir los dispositivos**, proporcione información del dispositivo y especifique los detalles de cada dispositivo, como **Número de serie**, **Número de pedido**, o seleccione **Cargar archivo CSV**. Después, seleccione **Asignar al servidor**, seleccione el <*NombreDeServidor*> que ha especificado en el paso 3 y, después, haga clic en **Aceptar**.  

3.  **Sincronizar los dispositivos administrados por DEP**   
    En la consola de **Activos y compatibilidad** , vaya a **Todos los dispositivos corporativos** > **iOS** > **Información del dispositivo**. En la pestaña **Inicio** , haga clic en **Sincronización de DEP**. Se envía una solicitud de sincronización a Apple. Una vez completada la sincronización, se muestran los dispositivos administrados por DEP. Se abre el cuadro de diálogo **Estado de inscripción** de los dispositivos administrados es **No contactado** hasta que el dispositivo se enciende y ejecuta el Asistente de configuración para inscribir el dispositivo.  

4.  **Distribuir los dispositivos a los usuarios**   
    Ahora puede proporcionar los dispositivos corporativos a los usuarios. Los dispositivos iOS quedan inscritos para su administración mediante Intune al activarlos.

