---
title: "Configurar la administración híbrida de dispositivos Windows con System Center Configuration Manager y Microsoft Intune | Microsoft Docs"
description: "Configure la administración de dispositivos Windows con System Center Configuration Manager y Microsoft Intune."
ms.custom: na
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: "9"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 47348baeac26bfa2ad5016622fe4dbcb9f572483
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar la administración híbrida de dispositivos Windows con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*

En este tema, se explica a los administradores de TI cómo pueden permitir a los usuarios que incorporen PC de Windows y dispositivos móviles en la administración mediante Configuration Manager y Microsoft Intune.

## <a name="enable-windows-device-management"></a>Habilitar la administración de dispositivos Windows
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
      2. Si su organización necesita transferir localmente aplicaciones de empresa, puede cargar el archivo o token necesarios. Para más información sobre la instalación de prueba de las aplicaciones, vea [Crear aplicaciones de Windows](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
        - **Token de inscripción de aplicación**
        - **Archivo .pfx**
        - **Ninguno** Si usa un certificado de Symantec, puede especificar **Show an alert before Symantec certificates expire** (Mostrar una alerta antes de que expiren los certificados de Symantec).
4. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  Para simplificar el proceso de inscripción con el Portal de empresa, debe crear un alias DNS para la inscripción de dispositivos. Después puede indicar a los usuarios cómo inscribir sus dispositivos.

## <a name="choose-how-to-enroll-windows-devices"></a>Elegir cómo inscribir dispositivos Windows

Una vez que haya asignado licencias de Intune a los usuarios, los dispositivos Windows se pueden inscribir sin pasos adicionales, pero puede facilitar la inscripción para los usuarios.

Hay dos factores que determinan cómo puede simplificar la inscripción de dispositivos Windows:
- **¿Usa Azure Active Directory Premium?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) se incluye con Enterprise Mobility + Security y otros planes de licencias.
- **¿Qué versiones de los clientes de Windows se inscribirán?** <br>Los dispositivos Windows 10 pueden inscribirse automáticamente al agregar una cuenta profesional o educativa. Las versiones anteriores deben inscribirse mediante la aplicación de Portal de empresa.

||**Azure AD Premium**|**Otro AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Inscripción automática](#enable-windows-10-automatic-enrollment) |[Inscripción de usuarios](#enable-windows-enrollment-without-azure-ad-premium)|
|**Versiones anteriores de Windows**|[Inscripción de usuarios](#enable-windows-enrollment-without-azure-ad-premium)|[Inscripción de usuarios](#enable-windows-enrollment-without-azure-ad-premium)|

## <a name="enable-windows-10-automatic-enrollment"></a>Habilitar la inscripción automática de Windows 10

La inscripción automática permite a los usuarios inscribir en Intune PC Windows 10 y dispositivos móviles Windows 10 corporativos o personales. Para ello, deben agregar una cuenta profesional o educativa y aceptar su administración. Es así de sencillo. En segundo plano, el dispositivo del usuario se registra y se une a Azure Active Directory. Una vez se registra un dispositivo, este se administra con Intune.

**Requisitos previos**
- Suscripción a Azure Active Directory Premium ([suscripción de prueba](http://go.microsoft.com/fwlink/?LinkID=816845))
- Suscripción a Microsoft Intune


### <a name="configure-automatic-mdm-enrollment"></a>Configurar la inscripción de MDM automática

1. Inicie sesión en el [Portal de administración de Azure](https://portal.azure.com) (https://manage.windowsazure.com) y seleccione **Azure Active Directory**.

  ![Captura de pantalla de Azure Portal](../media/auto-enroll-azure-main.png)

2. Seleccione **Movilidad (MDM y MAM)**.

  ![Captura de pantalla de Azure Portal](../media/auto-enroll-mdm.png)

3. Seleccione **Microsoft Intune**.

  ![Captura de pantalla de Azure Portal](../media/auto-enroll-intune.png)

4. Configure **Ámbito de usuario de MDM**. Especifique qué dispositivos de los usuarios deben administrarse mediante Microsoft Intune. Los dispositivos Windows 10 de estos usuarios se inscribirán automáticamente para la administración con Microsoft Intune.

    - **Ninguno**
    - **Algunos**
    - **Todos**

   ![Captura de pantalla de Azure Portal](../media/auto-enroll-scope.png)

5. Utilice los valores predeterminados para las direcciones URL siguientes:
    - **URL de los términos de uso de MDM**
    - **URL de detección de MDM**
    - **URL de cumplimiento de MDM**

6. Seleccione **Guardar**.


De manera predeterminada, la autenticación en dos fases no está habilitada para el servicio. En cambio, se recomienda la autenticación en dos fases al registrar un dispositivo. Antes de requerir la autenticación en dos fases para este servicio, debe configurar un proveedor de autenticación de dos fases en Azure Active Directory y configurar las cuentas de usuario para la autenticación multifactor. Vea [Introducción a Servidor Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## <a name="enable-windows-enrollment-without-azure-ad-premium"></a>Habilitar la inscripción de Windows sin Azure AD Premium
Puede permitir que los usuarios inscriban sus dispositivos sin la inscripción automática de Azure AD Premium. Una vez que asigne licencias, los usuarios pueden realizar la inscripción después de agregar la cuenta profesional a sus dispositivos personales o unir sus dispositivos corporativos a Azure AD. La creación de un alias DNS (tipo de registro CNAME) permite que los usuarios puedan inscribir sus dispositivos fácilmente. Al crear registros de recursos CNAME de DNS, los usuarios se conectan a Intune y se inscriben sin escribir el nombre de servidor de Intune.

### <a name="create-cnames-to-simplify-enrollment"></a>Crear CNAME para simplificar la inscripción
Cree registros de recursos DNS CNAME para el dominio de su empresa. Por ejemplo, si el sitio web de la empresa es contoso.com, debe crear un registro CNAME en DNS que redirija EnterpriseEnrollment.contoso.com a EnterpriseEnrollment-s.manage.microsoft.com.

Aunque la creación de entradas DNS CNAME es opcional, los registros CNAME facilitan la inscripción para los usuarios. Si no se encuentra ningún registro CNAME de inscripción, se pedirá a los usuarios que escriban de forma manual el nombre del servidor MDM (enrollment.manage.microsoft.com).

|Tipo|Nombre de host|Apunta a|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hora|

Si tiene más de un sufijo UPN, debe crear un CNAME para cada nombre de dominio y apuntar todos a EnterpriseEnrollment-s.manage.microsoft.com. Por ejemplo, si los usuarios de Contoso usan name@contoso.com, pero también usan name@us.contoso.com y name@eu.constoso.com como su correo electrónico o UPN, el administrador de DNS de Contoso necesitaría crear los CNAME siguientes.

|Tipo|Nombre de host|Apunta a|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hora|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hora|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hora|

`EnterpriseEnrollment-s.manage.microsoft.com`: admite un redireccionamiento al servicio Intune con reconocimiento de dominio del nombre de dominio del correo electrónico.

Los cambios en los registros DNS pueden tardar hasta 72 horas en propagarse. No se puede comprobar el cambio de DNS en Intune hasta que el registro DNS se propague.

## <a name="tell-users-how-to-enroll-devices"></a>Indicar a los usuarios cómo inscribir dispositivos  

 Cuando esté listo, necesitará que los usuarios sepan cómo inscribir sus dispositivos. Vea [Qué decirles a los usuarios finales sobre el uso de Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) para obtener instrucciones. Puede dirigir a los usuarios a [Inscribir su dispositivo Windows en Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). Esta información se aplica a Microsoft Intune y a dispositivos móviles administrados por Configuration Manager.

> [!div class="button"]
[< Paso anterior](create-service-connection-point.md)  [Paso siguiente >](set-up-additional-management.md)
