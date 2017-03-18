---
title: "Configuración de Windows Hello para empresas | Microsoft Docs"
description: Aprenda a integrar Windows Hello para empresas con System Center Configuration Manager.
ms.custom: na
ms.date: 10/10/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: 17
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: ec3d130674d606410e6da7babee126e017aff234
ms.lasthandoff: 03/04/2017


---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Configuración de Windows Hello para empresas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

System Center Configuration Manager le permite integrarse con Windows Hello para empresas (anteriormente Microsoft Passport para Windows), que es un método de inicio de sesión alternativo para dispositivos Windows 10. Hello para empresas utiliza Active Directory o una cuenta de Azure Active Directory para reemplazar una contraseña, una tarjeta inteligente o una tarjeta inteligente virtual.  

Hello para empresas permite usar un **gesto de usuario** al iniciar sesión, en lugar de una contraseña. Un gesto de usuario podría ser un simple PIN, una autenticación biométrica o un dispositivo externo, como un lector de huellas digitales.  

 Configuration Manager se integra con Windows Hello para empresas de dos maneras:  

-   Puede usar Configuration Manager para controlar cuáles gestos pueden emplear los usuarios para iniciar sesión y cuáles no.  

-   Puede almacenar certificados de autenticación en el proveedor de almacenamiento de claves de Windows Hello para empresas. Para obtener más información, consulte [Introduction to certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Introducción a perfiles de certificado en Configuration Manager).  

- Puede implementar directivas de Windows Hello para empresas para dispositivos de Windows 10 unidos a dominio que ejecutan el cliente de Configuration Manager. Esta configuración se describe en [Configuración de Windows Hello para empresas en dispositivos unidos a dominio de Windows 10](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices), más adelante. Cuando se usa Configuration Manager con Intune (híbrido), puede configurar estas opciones en Windows 10 y dispositivos Windows 10 Mobile, pero no en dispositivos unidos a dominio que ejecutan al cliente de Configuration Manager. Consulte [Configure Windows Hello for Business settings (hybrid)](../../mdm/deploy-use/windows-hello-for-business-settings.md) (Configuración de Windows Hello para empresas (híbrido)) para información.

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Configuración de Windows Hello para empresas en dispositivos unidos a dominio de Windows 10
Puede controlar la configuración de Windows Hello para empresas en dispositivos unidos a dominio de Windows 10 de tres maneras:

- Puede crear e implementar un perfil de Windows Hello para empresas. Esta es la opción recomendada.
- Puede usar la directiva de grupo.  
- Puede usar un script de PowerShell.

Tenga en cuenta que, además de esta configuración, también debe implementar un perfil de certificado, como se describe en [Configure a certificate profile](#configure-a-certificate-profile) (Configuración de un perfil de certificado).

### <a name="recommended-approach----configure-a-windows-hello-for-business-profile"></a>Opción recomendada: configurar un perfil de Windows Hello para empresas  

En la consola de administración, en **Acceso a los recursos de la compañía**, haga clic en **Perfiles de Windows Hello para la empresa** y elija **Nuevo** para iniciar el Asistente para el perfil. Proporcione la configuración solicitada por el asistente, revise y confirme la configuración en la última página y haga clic en **Cerrar**. Este es un ejemplo del aspecto que podría tener la configuración:  

![Configuración de Windows Hello para empresas](../media/Hello-for-Business-settings.png)

### <a name="configure-windows-hello-for-business-with-group-policy-in-active-directory"></a>Configurar Windows Hello para empresas con directiva de grupo en Active Directory  

Puede usar una directiva de grupo de Active Directory para configurar sus dispositivos unidos a dominio de Windows 10 a fin de aprovisionar credenciales de Windows Hello para empresas cuando un usuario inicia sesión en Windows:

1.  En un equipo con Windows Server, abra el Administrador de servidores y navegue hasta **Herramientas** > **Administración de directivas de grupo**.    

2.  En el cuadro de diálogo **Administración de directivas de grupo** , expanda el dominio en el que quiere habilitar la unión al área de trabajo automática.    

3.  Haga clic con el botón derecho en **Objetos de directiva de grupo**y luego haga clic en **Nuevo**.  

4.  En el cuadro de diálogo **Nuevo GPO**, escriba un nombre para el nuevo objeto de Directiva de grupo, como **Habilitar Windows Hello para empresas**, y luego haga clic en **Aceptar**.  

5.  En el nodo **Objetos de directiva de grupo** , haga clic con el botón derecho en el objeto que acaba de crear y luego haga clic en **Editar**.  

6.  En el cuadro de diálogo **Editor de administración de directivas de grupo**, navegue hasta **Configuración del equipo** > **Directivas** > **Plantillas administrativas** > **Componentes de Windows** > **Windows Hello para empresas**.  

7.  Haga clic con el botón derecho en **Habilitar Windows Hello para empresas** y, a continuación, haga clic en **Editar**.   

8.  Seleccione **Habilitado**, haga clic en **Aplicar**y luego en **Aceptar**.

Ahora puede vincular el objeto de Directiva de grupo que acaba de crear en la ubicación que quiera. Por ejemplo:    

   Una unidad organizativa (UO) específica en AD donde se ubicarán los equipos unidos a dominio de Windows 10.    

   Un grupo de seguridad específico que contiene equipos unidos a un dominio de Windows 10 que se registrarán automáticamente con Azure AD.    

#### <a name="configure-windows-hello-for-business-by-deploying-a-powershell-script-with-configuration-manager"></a>Configuración de Windows Hello para la empresa mediante la implementación de un script de PowerShell con Configuration Manager    
Puede crear e implementar el siguiente script de PowerShell con la administración de aplicaciones de Configuration Manager.    

```    
powershell.exe -ExecutionPolicy Bypass -NoLogo -NoProfile -Command "& {New-ItemProperty "HKLM:\Software\Policies\Microsoft\PassportForWork" -Name "Enabled" -Value 1 -PropertyType "DWord" -Force}"  
```  

Para obtener más información acerca de la administración de la aplicación de Configuration Manager, consulte [Introduction to application management in System Center Configuration Manager](/sccm/apps/understand/introduction-to-application-management) (Introducción a la administración de aplicaciones de System Center Configuration Manager).  

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configuración de un perfil de certificado para inscribir el certificado de inscripción de Windows Hello para empresas en Configuration Manager  
 Si quiere usar el inicio de sesión basado en certificados de Windows Hello para empresas, o Microsoft Hello, configure lo siguiente:  

-   Un perfil de certificado de Configuration Manager  

-   En el perfil de certificado, seleccione una plantilla que usa el EKU de inicio de sesión de tarjeta inteligente.  

 Para obtener más información, consulte [Introduction to certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Introducción a perfiles de certificado en Configuration Manager).  

### <a name="see-also"></a>Consulte también  
 [Protect data and site infrastructure with System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md) (Proteger la infraestructura de datos y del sitio con System Center Configuration Manager)

 [Administrar la verificación de identidad con Windows Hello para empresas](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport).  

