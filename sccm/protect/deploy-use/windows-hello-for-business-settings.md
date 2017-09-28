---
title: "Configuración de Windows Hello para empresas | Microsoft Docs"
description: Aprenda a integrar Windows Hello para empresas con System Center Configuration Manager.
ms.custom: na
ms.date: 09/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: "17"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 43586e55f2c0c5cf117b94c61250f26ba4233f53
ms.sourcegitcommit: 4c3906cf9614420cb8527da9e48978eb0b8f0e7a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2017
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Configuración de Windows Hello para empresas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

System Center Configuration Manager le permite integrarse con Windows Hello para empresas (anteriormente Microsoft Passport para Windows), que es un método de inicio de sesión alternativo para dispositivos Windows 10. Hello para empresas utiliza Active Directory o una cuenta de Azure Active Directory para reemplazar una contraseña, una tarjeta inteligente o una tarjeta inteligente virtual.  

Hello para empresas permite usar un **gesto de usuario** al iniciar sesión, en lugar de una contraseña. Un gesto de usuario podría ser un simple PIN, una autenticación biométrica o un dispositivo externo, como un lector de huellas digitales.

[Obtenga más información acerca de Windows Hello para empresas](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)

 Configuration Manager se integra con Windows Hello para empresas de dos maneras:  

-   Puede usar Configuration Manager para controlar cuáles gestos pueden emplear los usuarios para iniciar sesión y cuáles no.  

-   Puede almacenar certificados de autenticación en el proveedor de almacenamiento de claves de Windows Hello para empresas. Para obtener más información, consulte [Introduction to certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Introducción a perfiles de certificado en Configuration Manager).  

- Puede implementar directivas de Windows Hello para empresas para dispositivos de Windows 10 unidos a dominio que ejecutan el cliente de Configuration Manager. Esta configuración se describe en [Configuración de Windows Hello para empresas en dispositivos unidos a dominio de Windows 10](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices), más adelante. Al usar Configuration Manager con Microsoft Intune (híbrido), puede configurar estas opciones en dispositivos con Windows 10 y con Windows 10 Mobile. Consulte [Configure Windows Hello for Business settings (hybrid)](../../mdm/deploy-use/windows-hello-for-business-settings.md) (Configuración de Windows Hello para empresas (híbrido)) para información.

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Configuración de Windows Hello para empresas en dispositivos unidos a dominio de Windows 10
Puede controlar la configuración de Windows Hello para empresas en dispositivos con Windows 10 unidos a un dominio mediante la creación e implementación de un perfil de Windows Hello para empresas. Esta es la opción recomendada.


Si usa la autenticación basada en certificado, también debe implementar un perfil de certificado, como se describe en [Configuración de un perfil de certificado](#configure-a-certificate-profile). Si usa la autenticación basada en claves, no es necesario implementar un perfil de certificado.

## <a name="configure-a-windows-hello-for-business-profile"></a>Configuración de un perfil de Windows Hello para empresas  

En la consola de Configuration Manager, en **Acceso a los recursos de la compañía**, haga clic con el botón derecho en **Perfiles de Windows Hello para empresas** y elija **Nuevo** para iniciar el Asistente para perfiles. Proporcione la configuración solicitada por el asistente, revise y confirme la configuración en la última página y haga clic en **Cerrar**. Este es un ejemplo del aspecto que podría tener la configuración:  

![Configuración de Windows Hello para empresas](../media/Hello-for-Business-settings.png)

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configuración de un perfil de certificado para inscribir el certificado de inscripción de Windows Hello para empresas en Configuration Manager  
 Si quiere usar el inicio de sesión basado en certificados de Windows Hello para empresas, configure lo siguiente:  

-   Un perfil de certificado de Configuration Manager  

-   En el perfil de certificado, seleccione una plantilla que usa el EKU de inicio de sesión de tarjeta inteligente.  

-   Si pretende almacenar perfiles de certificado en el contenedor de claves de Windows Hello para empresas, y el perfil de certificado usa el EKU **Inicio de sesión de tarjeta inteligente**, debe configurar los siguientes permisos para el registro de clave, a fin de asegurarse de que el certificado se valida correctamente.
Primero debe crear el grupo **Administradores clave** y agregar como miembros de dicho grupo a todos los equipos de punto de administración de Configuration Manager.

Algunas configuraciones pueden no requerir la configuración de permisos, o bien pueden requerir otras configuraciones. Consulte la tabla siguiente para obtener más información:

|||||
|-|-|-|-|
|Versión de cliente de Windows|Configuration Manager 1602 o 1606|Configuration Manager 1610|Configuration Manager 1702 o posterior|
|Actualización de aniversario de Windows 10|Ninguna revisión necesaria<br><br>Ningún permiso necesario<br><br>Ninguna actualización de esquema de Windows necesaria|Ninguna revisión necesaria (ver **Advertencia**)<br><br>Ningún permiso necesario<br><br>Ninguna actualización de esquema de Windows necesaria|Configurar permisos<br><br>Aplica el esquema de Windows Server 2016 a Active Directory|
|Windows 10 Creators Update o posterior|No compatible|Instalar [esta revisión](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v)<br><br>Configurar permisos<br><br>Aplica el esquema de Windows Server 2016 a Active Directory|Configurar permisos<br><br>Aplica el esquema de Windows Server 2016 a Active Directory|

> [!WARNING]
> Si bien [la revisión](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v) para Configuration Manager 1610 y la Actualización de aniversario de Windows 10 no es necesaria, puede instalarla.  Si se instala, debe configurar permisos y aplicar el esquema de Windows Server 2016 en Active Directory.

## <a name="to-configure-permissions"></a>Para configurar permisos

1.  Inicie sesión en un controlador de dominio o en estaciones de trabajo de administración con la credencial Administrador de dominio, o bien con credenciales equivalentes.
2.  Abra **Usuarios y equipos de Active Directory**.
3.  En el panel de navegación, haga clic con el botón derecho en el nombre de dominio y después haga clic en **Propiedades**.
4.  En la pestaña **Seguridad** del cuadro de diálogo *<domain name>* **Propiedades**, haga clic en **Opciones avanzadas**. Si la pestaña **Seguridad** no aparece, active **Características avanzadas** en el menú **Ver** de **Usuarios y equipos de Active Directory**.
5.  Haga clic en **Agregar**.
6.  En el cuadro de diálogo **Entrada de permiso para** *<domain name>*, haga clic en **Seleccionar una entidad de seguridad**.
7.  En el cuadro de diálogo **Seleccionar usuario, equipo, cuenta de servicio o grupo**, escriba **Administradores clave** en el cuadro de texto **Escriba el nombre del objeto que desea seleccionar**.  Haga clic en **Aceptar**.
8.  En la lista **Se aplica a**, seleccione **Descendant User objects** (Objetos de usuario descendiente).
9.  Desplácese hasta la parte inferior de la página y haga clic en **Clear all** (Borrar todo).
10. En la sección **Propiedades**, seleccione **Read msDS-KeyCredentialLink** (Leer msDS-KeyCredentialLink).
11. Haga clic en **Aceptar** tres veces para completar la tarea.


## <a name="next-steps"></a>Pasos siguientes

Para obtener más información, consulte [Introduction to certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Introducción a perfiles de certificado en Configuration Manager).  




