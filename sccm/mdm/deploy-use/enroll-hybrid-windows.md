---
title: "Configurar la administración híbrida de dispositivos Windows con System Center Configuration Manager y Microsoft Intune | Microsoft Docs"
description: "Configure la administración de dispositivos Windows con System Center Configuration Manager y Microsoft Intune."
ms.custom: na
ms.date: 03/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a8218e23743dafaf8ff1166142cf2dcca1212133
ms.openlocfilehash: 996d01d3c5d5be4544246a5f321f67b60a8f5508
ms.lasthandoff: 03/14/2017


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar la administración híbrida de dispositivos Windows con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*

En este tema, se explica a los administradores de TI cómo pueden permitir a los usuarios que incorporen PC de Windows y dispositivos móviles en la administración mediante Configuration Manager y Microsoft Intune. Hay disponibles dos métodos de inscripción:
-  Inscripción automática de Azure Active Directory (AD) cuando los usuarios conectan su cuenta con un dispositivo
- Inscripción al instalar la aplicación de Portal de empresa e iniciar sesión con ella

## <a name="choose-how-to-enroll-windows-devices"></a>Elegir cómo inscribir dispositivos Windows

Hay dos factores que determinan cómo inscribirá dispositivos Windows:
- **¿Usa Azure Active Directory Premium?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) se incluye con Enterprise Mobility + Security y otros planes de licencias.
- **¿Qué versiones de los clientes de Windows se inscribirán?** <br>Los dispositivos Windows 10 pueden inscribirse automáticamente al agregar una cuenta profesional o educativa. Las versiones anteriores deben inscribirse mediante la aplicación de Portal de empresa.

||**Azure AD Premium**|**Otro AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Inscripción automática](#automatic-enrollment) |[Inscripción de Portal de empresa](#company-portal-enrollment)|
|**Versiones anteriores de Windows**|[Inscripción de Portal de empresa](#company-portal-enrollment)|[Inscripción de Portal de empresa](#company-portal-enrollment)|

## <a name="automatic-enrollment"></a>Inscripción automática

La inscripción automática permite a los usuarios inscribir dispositivos Windows 10 corporativos o personales al agregar una cuenta profesional o educativa, y aceptar que se administre. En segundo plano, el dispositivo del usuario se registra y se conecta con Azure Active Directory. Una vez que se ha registrado, el dispositivo puede administrarse con Intune. Los dispositivos administrados aún pueden usar el Portal de empresa para tareas, pero no tienen que instalarlo para inscribirse.

**Requisitos previos**
- Suscripción a Azure Active Directory Premium ([suscripción de prueba](http://go.microsoft.com/fwlink/?LinkID=816845))
- Suscripción a Microsoft Intune

### <a name="configure-automatic-enrollment"></a>Configurar la inscripción automática

1. Inicie sesión en [Azure Portal](https://manage.windowsazure.com), vaya al nodo **Active Directory** en el panel izquierdo y seleccione el directorio.
2. Haga clic en la pestaña **Configurar** y desplácese hasta la sección denominada **Dispositivos**.
3. Seleccione **Todos** en **Users may workplace join devices** (Los usuarios pueden unir dispositivos al área de trabajo).
4. Seleccione el número máximo de dispositivos que quiere autorizar por usuario.

De manera predeterminada, la autenticación en dos fases no está habilitada para el servicio. En cambio, se recomienda la autenticación en dos fases al registrar un dispositivo. Antes de requerir la autenticación en dos fases para este servicio, debe configurar un proveedor de autenticación de dos fases en Azure Active Directory y configurar las cuentas de usuario para la autenticación multifactor. Vea [Introducción a Servidor Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## <a name="company-portal-enrollment"></a>Inscripción de Portal de empresa
Los usuarios finales o un [administrador de inscripción de dispositivos](enroll-devices-with-device-enrollment-manager.md) pueden inscribir dispositivos Windows al instalar la aplicación de Portal de empresa y después iniciar sesión con sus credenciales de trabajo. Para simplificar la inscripción para los usuarios finales, debe agregar un registro CNAME en el registro de DNS.

### <a name="enable-windows-device-management"></a>Habilitar la administración de dispositivos Windows
Para habilitar la administración de dispositivos Windows para equipos o dispositivos móviles, siga estos pasos:

1.  Para poder configurar la inscripción en cualquier plataforma, complete los requisitos previos y los procedimientos de [Configurar la MDM híbrida](setup-hybrid-mdm.md).  
2.  En la consola de Configuration Manager, en el área de trabajo **Administración**, vaya a **Información general** > **Cloud Services** > **Suscripciones a Microsoft Intune**.  
3.  En la cinta de opciones, seleccione **Configurar plataformas** y luego seleccione la plataforma de Windows:
    - **Windows** para portátiles y PC Windows, después realice los pasos siguientes:
      1. En la pestaña **General**, active la casilla **Habilitar la inscripción de Windows**.
      2. Si usa un certificado para firmar el código e implementar la aplicación de Portal de empresa, vaya al **Certificado de firma de código**. Los usuarios de dispositivos también pueden instalar la aplicación de Portal de empresa desde la Tienda Windows o puede implementar la aplicación desde la Tienda Windows para empresas sin firma de código.
      3. También puede configurar [Windows Hello para empresas](windows-hello-for-business-settings.md).
    - **Windows Phone** para tabletas y teléfonos Windows, después realice los pasos siguientes:
      1. En la pestaña **General**, active la casilla **Windows Phone 8.1 y Windows 10 Mobile**. Ya no se admite Windows Phone 8.0.
      2. Si su organización necesita transferir localmente aplicaciones de empresa, puede cargar el archivo o token necesarios. Para más información sobre cómo transferir localmente aplicaciones, vea [Crear aplicaciones de Windows](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
        - **Token de inscripción de aplicación**
        - **Archivo .pfx**
        - **Ninguno** Si usa un certificado de Symantec, puede especificar **Show an alert before Symantec certificates expire** (Mostrar una alerta antes de que expiren los certificados de Symantec).
4. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  Para simplificar el proceso de inscripción con el Portal de empresa, debe crear un alias DNS para la inscripción de dispositivos. Después puede indicar a los usuarios cómo inscribir sus dispositivos.

### <a name="create-dns-alias-for-device-enrollment"></a>Creación de un alias DNS para la inscripción de dispositivos  
Un alias DNS (tipo de registro CNAME) facilita a los usuarios la inscripción de sus dispositivos al conectarse al servicio sin necesidad de que el usuario escriba una dirección de servidor. Para crear un alias DNS (tipo de registro CNAME), tendrá que configurar un CNAME en los registros DNS de su empresa que redirija las solicitudes enviadas a una dirección URL del dominio de su empresa a servidores de servicios en la nube de Microsoft.  Por ejemplo, si el dominio de su empresa es contoso.com, debe crear un CNAME en DNS que redirija EnterpriseEnrollment.contoso.com a EnterpriseEnrollment-s.manage.microsoft.com.  

 Aunque la creación de entradas DNS CNAME es opcional, los registros CNAME facilitan la inscripción para los usuarios. Si no se encuentra ningún registro CNAME de inscripción, se pedirá a los usuarios que escriban de forma manual el nombre del servidor MDM (enrollment.manage.microsoft.com).

|Tipo|Nombre de host|Apunta a|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hora|

Si tiene más de un sufijo UPN, debe crear un CNAME para cada nombre de dominio y apuntar todos a EnterpriseEnrollment-s.manage.microsoft.com. Por ejemplo, si los usuarios de Contoso usan name@contoso.com, pero también usan name@us.contoso.com y name@eu.constoso.com como su correo electrónico o UPN, el administrador de DNS de Contoso necesitaría crear los siguientes CNAME.

|Tipo|Nombre de host|Apunta a|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hora|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hora|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hora|

## <a name="tell-users-how-to-enroll-devices"></a>Indicar a los usuarios cómo inscribir dispositivos  

 Cuando esté listo, necesitará que los usuarios sepan cómo inscribir sus dispositivos. Vea [Qué decirles a los usuarios finales sobre el uso de Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) para obtener instrucciones. Puede dirigir a los usuarios a [Inscribir su dispositivo Windows en Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). Esta información se aplica a Microsoft Intune y a dispositivos móviles administrados por Configuration Manager.

> [!div class="button"]
[< Paso anterior](create-service-connection-point.md)  [Paso siguiente >](set-up-additional-management.md)

