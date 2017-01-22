---
title: "Configurar la MDM híbrida | Microsoft Docs"
description: "Configure la inscripción de dispositivos híbridos con Configuration Manager e Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 48b91e88f78752cf7c05162b701ea2ca2f401de3
ms.openlocfilehash: 85df3df19f01f8ed6f5240851c47afce01a92880

---

# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar la administración híbrida de dispositivos móviles (MDM) con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*


Para poder administrar dispositivos iOS, Windows y Android con Configuration Manager, deben estar inscritos con Intune. Use los pasos siguientes para configurar la inscripción de dispositivos híbridos con Configuration Manager mediante Intune. Al completar los pasos siguientes, habilitará la inscripción "Bring Your Own Device" (BYOD) para los usuarios. Estos pasos son también requisitos previos para [inscribir dispositivos propiedad de la empresa](enroll-company-owned-devices.md).

 |Pasos|Detalles|  
 |-----------|-------------|  
 |**Paso 1:** [Crear una recopilación de MDM](#step-1-create-an-mdm-collection)|Crear una recopilación de usuarios de Configuration Manager con los usuarios que pueden inscribir sus dispositivos|  
 |**Paso 2:** [Requisitos de nombre de dominio](#step-2-domain-name-requirements)|Confirmar que la administración de usuarios de Active Directory y el servicio de nombres de dominio (DNS) de su organización cumple los requisitos de MDM|
 |**Paso 3:** [Configurar la suscripción a Intune](#step-3-configure-intune-subscription)|El servicio de Intune le permite administrar dispositivos a través de Internet.|  
 |**Paso 4:** [Agregar términos y condiciones](#step-4-add-terms-and-conditions)| Crear términos y condiciones que deben aceptar los usuarios para poder usar la aplicación Portal de empresa|
 |**Paso 5:** [Crear el punto de conexión de servicio](#step-5-create-service-connection-point)|El punto de conexión de servicio envía información de configuración e implementación de software a Configuration Manager y recupera mensajes de inventario y estado de dispositivos móviles. |  
 |**Paso 6:** [Habilitar la inscripción de plataforma](#step-6-enable-platform-enrollment)|La inscripción de MDM para dispositivos [iOS](#ios-and-mac-enrollment-setup) y [Windows](#windows-enrollment-setup) requiere pasos adicionales para la comunicación entre los servicios y dispositivos. Android no requiere ninguna configuración adicional.|  
 |**Paso 7:** [Configurar la administración adicional](#step-7-set-up-additional-management)|(Opcional) Configurar los elementos de configuración y de acceso condicional para dispositivos inscritos|
 |**Paso 8:** [Comprobar la configuración de MDM](#step-8-verify-mdm-configuration)|Ver los archivos de registro para confirmar que el punto de conexión de servicio se ha creado correctamente y las cuentas de usuario se sincronizan.|
 |**Paso 9:** [Inscribir dispositivos](#step-9-enroll-devices)|Indique a los usuarios cómo inscribir sus dispositivos o empiece a inscribir los dispositivos propiedad de la empresa para satisfacer las necesidades de su organización|

¿Busca Intune sin Configuration Manager?
> [!div class="button"]
[Ver documentos de Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)

## <a name="step-1-create-an-mdm-collection"></a>Paso 1: Crear una recopilación de MDM
Necesitará una recopilación de usuarios de Configuration Manager para especificar qué usuarios pueden inscribir dispositivos en la administración. Solo se pueden poner como destino recopilaciones de usuarios, porque las licencias de Intune se asignan a usuarios. Con fines de prueba, puede configurar una **regla directa** y agregar usuarios específicos que pueden inscribir dispositivos. En la consola de Configuration Manager, elija **Activos y compatibilidad** > **Recopilaciones de usuarios**, haga clic en la pestaña **Inicio** > grupo **Crear** y luego haga clic en **Crear recopilación de usuario**. Para una distribución más amplia, debe usar **reglas de consulta** para definir usuarios. Para obtener más información sobre las recopilaciones, consulte [Cómo crear recopilaciones](https://technet.microsoft.com/library/mt629371.aspx).

![Crear una recopilación de usuarios de MDM](../media/mdm-create-user-collection.png)

## <a name="step-2-domain-name-requirements"></a>Paso 2: Requisitos de nombre de dominio

Si es necesario, siga estos pasos para satisfacer todas las dependencias externas a Configuration Manager:

1. Cada usuario debe tener una licencia de Intune asignada para inscribir dispositivos. Para asociar licencias de Intune a usuarios, cada usuario debe tener un nombre principal de usuario (UPN) que se pueda resolver públicamente (por ejemplo, johndoe@contoso.com) o un identificador de inicio de sesión alternativo configurado en Azure Active Directory). Configurar un identificador de inicio de sesión alternativo permite a los usuarios iniciar sesión con una dirección de correo, por ejemplo, incluso si su UPN está en un formato de NetBIOS (por ejemplo, CONTOSO\johndoe).

  - Si su empresa usa UPN que se pueden resolver públicamente (por ejemplo, johndoe@contoso.com), no se requiere ninguna configuración adicional.
  - Si su empresa usa un UPN que no se puede resolver (por ejemplo, CONTOSO\johndoe), deberá [configurar un identificador alternativo en Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync).

2.  Implemente y configure los Servicios de federación de Active Directory (AD FS). (Opcional)

     Al configurar el inicio de sesión único, los usuarios pueden iniciar sesión con sus credenciales corporativas para obtener acceso a los servicios de Intune.

     Para obtener más información, consulte los temas siguientes:
    -   [Preparar el inicio de sesión único](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [Planear e implementar AD FS 2.0 para su uso con el inicio de sesión único](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  Implementar y configurar la sincronización de directorios.

     La sincronización de directorios permite rellenar Intune con cuentas de usuario sincronizadas. Las cuentas de usuario y los grupos de seguridad sincronizados se agregan a Intune. Los errores al habilitar la sincronización de directorios es una causa común por la que los dispositivos no pueden inscribirse al configurar la MDM de Configuration Manager con Microsoft Intune.

     Para obtener más información, consulte [Integración de directorios](http://go.microsoft.com/fwlink/?LinkID=271120) en la biblioteca de documentación de Active Directory.

4.  Opcional, pero no recomendado: si no se usan los Servicios de federación de Active Directory, restablezca las contraseñas de Microsoft Online de los usuarios.

     Si no utiliza AD FS, debe establecer una contraseña de Microsoft Online para cada usuario.

## <a name="step-3-configure-intune-subscription"></a>Paso 3: Configurar la suscripción a Intune
 La suscripción de Intune le permite administrar dispositivos a través de Internet. Esto incluye la especificación de qué recopilación de usuarios puede inscribir dispositivos y la definición de la información que se presenta a los usuarios. La suscripción a Intune hace lo siguiente:

-   Recupera el certificado que el punto de conexión de servicio requiere para establecer la conexión con el servicio de Intune.
-   Define la recopilación de usuarios que permite a los usuarios inscribir dispositivos móviles.
-   Define y configura las plataformas móviles que se quieren admitir.

> [!IMPORTANT]
>  Al crear una suscripción de Microsoft Intune en Configuration Manager, el punto de conexión de servicio del sitio se colocará en "modo en línea". Consulte [Acerca del punto de conexión de servicio en System Center Configuration Manager](../../core/servers/deploy/configure/about-the-service-connection-point.md).

### <a name="to-create-the-microsoft-intune-subscription"></a>Para crear la suscripción a Microsoft Intune

1.  Si aún no lo ha hecho, regístrese para obtener una cuenta de Microsoft Intune en [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216).  Después de crear la cuenta de Intune, no tiene que agregar usuarios a la cuenta de Intune ni realizar configuraciones adicionales.

2.  En la consola de Configuration Manager, haga clic en **Administración**.

3.  En el área de trabajo **Administración** , expanda **Servicios en la nube**y haga clic en **Suscripciones de Microsoft Intune**. En la pestaña **Inicio** , haga clic en **Agregar suscripción de Microsoft Intune**.

![Crear una suscripción a Intune](../media/mdm-set-intune.png)

4.  En la página **Introducción** del Asistente para crear suscripción de Microsoft Intune, revise el texto y haga clic en **Siguiente**.

5.  En la página **Suscripción** , haga clic en **Iniciar sesión** e inicie sesión con su cuenta profesional o educativa. En el cuadro de diálogo **Establecer entidad de administración de dispositivos móviles**, active la casilla para administrar solo dispositivos móviles mediante Configuration Manager a través de la consola de Configuration Manager. Para continuar con su suscripción, debe seleccionar esta opción.

    > [!IMPORTANT]
    >  Si se selecciona Configuration Manager como entidad de administración, no podrá modificarla en Microsoft Intune en el futuro.

6.  Haga clic en los vínculos de privacidad para revisarlos y, a continuación, haga clic en **Siguiente**.

7.  En la página **General** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**.

  -   **Recopilación**: especifique una recopilación de usuarios que contenga los usuarios que inscribirán sus dispositivos móviles.

      > [!NOTE]
      >  Si se quita un usuario de la recopilación, el dispositivo del usuario se seguirá administrando durante 24 horas hasta que se quite el registro del usuario de la base de datos de usuarios.

  -   **Nombre de compañía**: especifique el nombre de su compañía.

  -   **Dirección URL a la documentación de privacidad de la compañía**: si publica la información de privacidad de su compañía en un vínculo accesible desde Internet, proporcione un vínculo al que los usuarios puedan acceder desde el portal de empresa, por ejemplo, http://www.contoso.com/CP_privacy.html. La información de privacidad puede aclarar la información que comparten los usuarios con su compañía.

  -   **Combinación de colores del portal de la compañía**: si lo desea, cambie el color predeterminado azul de los portales de la compañía.

  -   **Código de sitio de Configuration Manager**: especifique un código de sitio para un sitio primario para administrar los dispositivos móviles.

    > [!NOTE]
    >  El cambio del código de sitio solo afecta a nuevas inscripciones, y no afecta a dispositivos ya inscritos.

8.  En la página **Información de contacto de la compañía**, especifique la información de contacto de la compañía que se muestra a los usuarios en la aplicación Portal de empresa en **Contactar con TI**. Proporcione la información de contacto de la empresa y luego haga clic en **Siguiente**.

9. En la página **Logotipo de la compañía**, puede elegir si quiere mostrar logotipos en el portal de empresa, después haga clic en **Siguiente**.

10. Complete el asistente.

## <a name="step-4-add-terms-and-conditions"></a>Paso 4: Agregar términos y condiciones
 Después de configurar la administración de Intune para dispositivos móviles, puede crear **Términos y condiciones**. Use los términos y condiciones para explicar a los usuarios qué sucede cuando inscriben sus dispositivos. Los usuarios deben aceptar los términos y condiciones para poder inscribir un dispositivo. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Información general** > **Configuración de cumplimiento** > **Términos y condiciones** y luego haga clic en **Crear términos y condiciones**. Consulte [Términos y condiciones en System Center Configuration Manager](terms-and-conditions.md).

##  <a name="step-5-create-service-connection-point"></a>Paso 5: Crear el punto de conexión de servicio
Una vez creada la suscripción, puede instalar el rol de sistema de sitio del punto de conexión de servicio que le permite conectarse al servicio de Intune. Este rol de sistema de sitio insertará configuraciones y aplicaciones en el servicio de Intune.

 El punto de conexión de servicio envía información de configuración e implementación de software a Configuration Manager y recupera mensajes de inventario y estado de dispositivos móviles. El servicio Configuration Manager actúa como una puerta de enlace que se comunica con los dispositivos móviles y almacena la configuración.

> [!NOTE]
>  El rol del sistema de sitio del punto de conexión de servicio solo se debe instalar en un sitio de administración central o en un sitio primario independiente. El punto de conexión de servicio debe tener acceso a Internet.


### <a name="configure-the-service-connection-point-role"></a>Configurar el rol de punto de conexión de servicio

1.  En la consola de Configuration Manager, haga clic en **Administración**.

2.  En el área de trabajo **Administración**, expanda **Sitios** y después haga clic en **Servidores y roles del sistema de sitios**.

3.  Agregue el rol **Punto de conexión de servicio** a un servidor de sistema de sitio nuevo o existente mediante la etapa asociada:

    -   Nuevo servidor de sistema de sitio: en la pestaña **Inicio** , del grupo **Crear** , haga clic en **Crear servidor del sistema de sitio** para iniciar el asistente para creación de servidor de sistema de sitio.

    -   Servidor de sistema de sitio existente: haga clic en el servidor en el que quiere instalar el rol de punto de conexión de servicio. A continuación, en la pestaña **Inicio** , en el grupo **Servidor** , haga clic en **Agregar roles del sistema de sitio** para iniciar el Asistente para agregar roles de sistema de sitio.

4.  En la página **Selección de rol del sistema** , seleccione **Punto de conexión de servicio**y haga clic en **Siguiente**.

![Crear un punto de conexión de servicio](../media/mdm-service-connection-point.png)

5.  Complete el asistente.

### <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>¿Cómo se autentica el punto de conexión de servicio con el servicio de Microsoft Intune?
 El punto de conexión de servicio amplía Configuration Manager; para ello, establece una conexión con el servicio de Intune basado en la nube, que administra los dispositivos móviles mediante Internet. El punto de conexión de servicio se autentica con el servicio de Intune de la manera siguiente:

1.  Cuando se crea una suscripción a Intune en la consola de Configuration Manager, el administrador de Configuration Manager se autentica mediante la conexión a Azure Active Directory, que lo redirige al servidor de ADFS correspondiente para solicitar el nombre de usuario y la contraseña. Después, Intune emite un certificado para el inquilino.

2.  El certificado de la etapa 1 se instala en el rol de sitio del punto de conexión de servicio, y se usa para autenticar y autorizar la comunicación posterior con el servicio de Microsoft Intune.

## <a name="step-6-enable-platform-enrollment"></a>Paso 6: Habilitar la inscripción de plataforma
  Las diferentes plataformas de dispositivos requieren una configuración adicional para habilitar la inscripción de dispositivos:
  - [Configuración de inscripción de iOS y Mac](#ios-and-mac-enrollment-setup): obtenga un certificado de inserción de MDM de Apple
  - [Configuración de inscripción de Windows](#windows-enrollment-setup): configure DNS y habilite la inscripción para dispositivos Windows Phone, Windows 10 Mobile y PC Windows
  - Android: los dispositivos Android no requieren ningún paso adicional para habilitar la inscripción

Una vez habilitada la administración de MDM, puede especificar el número de dispositivos que puede inscribir a cada usuario, con un máximo de 15 dispositivos por usuario.

### <a name="ios-and-mac-enrollment-setup"></a>Configuración de inscripción de iOS y Mac
  Los pasos siguientes habilitan la administración de dispositivos de Apple al cargar un certificado de inserción de MDM de Apple en el servicio Intune.

  1.  **Descargue una solicitud de firma de certificado** : se necesita un archivo de solicitud de firma de certificado (.csr) para solicitar un certificado de APNs de Apple.  

      1.  En la consola de Configuration Manager, en el área de trabajo **Administración** , vaya a **Servicios en la nube**> **Suscripciones a Microsoft Intune**.  

      2.  En la pestaña **Inicio** , haga clic en **Crear solicitud de certificado APN**. Se abre el cuadro de diálogo **Solicitar petición de firma de certificado de servicio de notificaciones push de Apple** .  

      3.  Utilice la función**Examinar** para seleccionar la ruta de acceso donde se guardará el nuevo archivo de solicitud de firma de certificado (.csr). Guarde la solicitud de firma de certificado (.csr) en el equipo local.  

      4.  Haga clic en **Descargar**. El nuevo archivo .csr de Microsoft Intune se descarga y Configuration Manager lo guarda. Se utiliza el archivo .csr para solicitar un certificado de relación de confianza desde el portal de certificados push de Apple.  

  2.  **Solicite un certificado de APNs de Apple** : el certificado del Servicio de notificaciones push Apple (APNs) se usa para establecer una relación de confianza entre el servicio de administración, Intune y los dispositivos móviles iOS inscritos.  

      1.  En un explorador, vaya al [portal de certificados push de Apple](http://go.microsoft.com/fwlink/?LinkId=269844) e inicie sesión con su identificador de Apple de empresa. Este ID de Apple debe utilizarse en el futuro para renovar el certificado APNs.  

      2.  Complete el asistente usando el archivo de solicitud de firma de certificado (.csr). Descargue el certificado de APNs y guarde el archivo .pem localmente. Este archivo de certificado de APNs (.pem) se usa para establecer una relación de confianza entre el servidor de notificaciones push de Apple y la entidad de administración de dispositivos móviles de Intune.  

  3.  **Habilite la inscripción y cargue el certificado de APNs** : para habilitar la inscripción de iOS, cargue el certificado de APNs.  

      1.  En la consola de Configuration Manager, en el área de trabajo **Administración** , vaya a **Servicios en la nube** > **Suscripción a Microsoft Intune**.  

      2.  En la pestaña **Inicio** en el grupo **Suscripción** , haga clic en **Configurar plataformas** > **IOS**.  

          > [!NOTE]  
          >  No cargue el certificado del Servicio de notificaciones push de Apple (APNs) hasta que habilite la inscripción de iOS en la consola de Configuration Manager.  

      3.  En el cuadro de diálogo **Propiedades de suscripción a Microsoft Intune** , seleccione la pestaña **iOS** y haga clic para seleccionar la casilla **Habilitar la inscripción de iOS** .  

      4.  Haga clic en **Examinar**y vaya al archivo de certificado de APNs (.cer) que descargó de Apple. Manager Configuration muestra la información del certificado de APNs. Haga clic en **Aceptar** para guardar en Intune el certificado de APNs.    


Información adicional sobre [la inscripción de iOS y Mac](enroll-hybrid-ios-mac.md).

### <a name="windows-enrollment-setup"></a>Configuración de inscripción de Windows  
Puede usar Configuration Manager con Intune para administrar equipos de escritorio, equipos portátiles y otros dispositivos que ejecutan Windows como dispositivos móviles. También puede configurar dispositivos Windows 10 para que se [inscriban de forma automática cuando se unen a Azure Active Directory](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/enroll-hybrid-windows#azure-active-directory-enrollment) al agregar una cuenta profesional o educativa en el dispositivo.

Un alias DNS (tipo de registro CNAME) facilita a los usuarios la inscripción de sus dispositivos, ya que rellena automáticamente el nombre del servidor durante la inscripción. Después, puede habilitar la inscripción para dispositivos móviles de PC Windows.  

1. En la consola de Configuration Manager, en el área de trabajo **Administración**, vaya a **Servicios en la nube** > **Suscripciones a Microsoft Intune** y después haga lo siguiente:  
  - **PC Windows:** En la pestaña **Inicio**, haga clic en **Configurar plataformas** y después haga clic en **Windows**. En la pestaña **General** , seleccione **Habilitar la inscripción de Windows**.  
  - **Windows 10 Mobile y Windows Phone:** En la pestaña **Inicio**, haga clic en **Configurar plataformas** y después haga clic en **Windows Phone**.  En la pestaña **General** , elija  **Windows Phone 8.1 y Windows 10 Mobile**.

2.  También puede configurar Configuration Manager para que simplifique la inscripción al usar la aplicación Portal de empresa.
(Opcional) Cree un alias DNS (tipo de registro CNAME) en los registros DNS de su empresa que redirija las solicitudes enviadas a una dirección URL del dominio de su empresa a servidores de servicios en la nube de Microsoft.  Por ejemplo, si el dominio de su empresa es contoso.com, debe crear un CNAME en DNS que redirija EnterpriseEnrollment.contoso.com a EnterpriseEnrollment-s.manage.microsoft.com.  

|Tipo|Nombre de host|Apunta a|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  

Para obtener información adicional, consulte la [inscripción de Windows](enroll-hybrid-windows.md).

### <a name="android-enrollment-setup"></a>Configuración de inscripción de Android
Puede usar Configuration Manager con Intune para administrar teléfonos y tabletas con Android.
1.  En la consola de Configuration Manager, en el área de trabajo **Administración** , vaya a **Servicios en la nube** > **Suscripción a Microsoft Intune**.  

2.  En la pestaña **Inicio** del grupo **Suscripción** , haga clic en **Configurar plataformas** > **Android**.  

3.  En el cuadro de diálogo **Propiedades de suscripción a Microsoft Intune** , seleccione la pestaña **Android** y haga clic para seleccionar la casilla **Habilitar la inscripción de Android** .

Para obtener información adicional, consulte [Android](enroll-hybrid-android.md).

## <a name="step-7-set-up-additional-management"></a>Paso 7: Configurar la administración adicional
(Opcional) Puede configurar administración adicional antes de que se inscriban los dispositivos. Estas soluciones de administración se pueden crear e implementar una vez que los dispositivos están inscritos, aunque muchas organizaciones prefieren implementarlas según se incorporan los dispositivos a la administración.

Los **elementos de configuración** le permiten administrar la configuración (por ejemplo, exigir un PIN o requerir cifrado en dispositivos inscritos) según la plataforma del dispositivo:
- [Dispositivos Windows 10 y Windows 8.1](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)
- [Dispositivos Windows Phone](/sccm/compliance/deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client)
- [Dispositivos iOS y Mac](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)
- [Dispositivos Android y Samsung KNOX Standard](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)

Se pueden implementar **aplicaciones** en dispositivos administrados:
- [Aplicaciones de iOS](/sccm/apps/get-started/creating-ios-applications)
- [Aplicaciones de Mac](/sccm/apps/get-started/creating-mac-computer-applications)
- [Aplicaciones de PC Windows](/sccm/apps/get-started/creating-windows-applications)
- [Aplicaciones de Windows Phone](/sccm/apps/get-started/creating-windows-phone-applications)
- [Aplicaciones de Android](/sccm/apps/get-started/creating-android-applications)

El **acceso condicional** le permite administrar el acceso a los recursos de empresa, entre los que se incluyen:  
- [Acceso a correo electrónico](/sccm/protect/deploy-use/manage-email-access)
- [Acceso a SharePoint](/sccm/protect/deploy-use/manage-sharepoint-online-access)
- [Acceso a Skype Empresarial](/sccm/protect/deploy-use/manage-skype-for-business-online-access)
- [Dynamic CRM Online](/sccm/protect/deploy-use/manage-dynamics-crm-online-access)

## <a name="step-8-verify-mdm-configuration"></a>Paso 8: Comprobar la configuración de MDM

 Puede comprobar ciertos componentes de administración de dispositivos mediante la comprobación de los archivos de registro siguientes:

-   Compruebe en Cloudusersync.log que las cuentas de usuario están sincronizadas correctamente.

-   Compruebe en Sitecomp.log que el punto de conexión de servicio se creó correctamente.

## <a name="step-9-enroll-devices"></a>Paso 9: Inscribir dispositivos
Ha completado la configuración híbrida. Se pueden inscribir dispositivos en Configuration Manager de varias maneras:
- Dispositivos propiedad del usuario (BYOD): [informar a los usuarios sobre cómo inscribir sus dispositivos](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) (la guía de inscripción es la misma para los dispositivos administrados por Intune e híbridos)
- Dispositivos propiedad de la empresa (COD): la [inscripción de dispositivos propiedad de la empresa](enroll-company-owned-devices.md) proporciona directrices sobre las diferentes formas específicas de la plataforma de inscribir dispositivos propiedad de la empresa.

## <a name="managing-intune-subscriptions-associated-with-configuration-manager"></a>Administración de suscripciones de Intune asociadas con Configuration Manager

Si agrega una suscripción de Microsoft Intune (una suscripción de prueba o suscripción de pago) a Configuration Manager y luego necesita cambiar a otra suscripción de Intune, debe eliminar tanto la **suscripción a Microsoft Intune** como el **punto de conexión de servicio** desde la consola de Configuration Manager antes de poder agregar una nueva suscripción.

### <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Cómo eliminar una suscripción a Intune en Configuration Manager

> [!IMPORTANT]
>  Al eliminar la suscripción se elimina todo el contenido, incluidas las inscripciones de usuario, las directivas y las implementaciones de aplicaciones configuradas para dispositivos administrados por la suscripción a Intune.

1.  En la consola de Configuration Manager, vaya a **Administración** > **General** > **Cloud Services** > **Suscripciones a Microsoft Intune**.

2.  Haga clic con el botón derecho en la **Suscripción a Microsoft Intune** que se muestra y, luego, haga clic en **Eliminar**.

3.   En el asistente, haga clic en **Remove Microsoft Intune Subscription from Configuration Manager** (Quitar suscripción a Microsoft Intune de Configuration Manager), en **Siguiente** y, después, otra vez en **Siguiente** para quitar la suscripción.


### <a name="how-to-remove-the-service-connection-point-role"></a>Cómo quitar el rol de punto de conexión de servicio

1.  Vaya a **Administración** > **General** > **Configuración de sitio** > **Servidores y roles de sistema de sitio**.

2.  Seleccione el servidor que hospeda el rol **Punto de conexión de servicio**.

3.  En la lista **Roles del sistema de sitio**, seleccione **Punto de conexión de servicio** y haga clic en **Quitar rol** en la cinta de opciones. Confirme que desea quitar el rol. Se elimina el punto de conexión de servicio.

Ahora puede crear un nuevo punto de conexión de servicio, agregar una nueva suscripción de Intune a Configuration Manager y establecer Configuration Manager como la entidad de MDM.

### <a name="how-to-change-mdm-authority-to-intune"></a>Cómo cambiar la entidad de MDM a Intune

A partir de la versión 1610, puede para cambiar la entidad de MDM de Configuration Manager a Intune. Próximamente habrá disponible información sobre esta característica.



<!--HONumber=Dec16_HO3-->


