---
title: Usar Azure AD para la administración conjunta
titleSuffix: Configuration Manager
description: Con Azure AD que puede aprovechar mejora la productividad para los usuarios y seguridad para los recursos, en entornos de nube y locales
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3b773c0bfe8cd0f8253a67ac96f5a0113b7206c0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755596"
---
# <a name="use-azure-ad-for-co-management"></a>Usar Azure AD para la administración conjunta

En la nube, la identidad es el nuevo plano de control. Azure Active Directory (Azure AD) permite vincular los usuarios, dispositivos y aplicaciones en entornos de nube y locales. Registrar sus dispositivos a Azure AD le permite mejorar la productividad de los usuarios y seguridad para los recursos. Tener dispositivos en Azure AD es la base para la administración conjunta y acceso condicional basado en el dispositivo. 

Para obtener más información sobre el acceso condicional basado en dispositivos, consulte [How To: Requerir que los dispositivos administrados para el acceso a la aplicación en la nube con acceso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)

En el siguiente vídeo, director de programas senior Sandeep Deo y productos de marketing manager Adam Harbour discutir y demostración de Azure AD para la administración conjunta:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD proporciona dos opciones para dispositivos de empresa satisfacer las necesidades de su organización:  

- **Dispositivo unido a AD Azure**: Unir sus dispositivos Windows 10 a Azure AD sin necesidad de conectarse a ellas en su Active Directory local  

    - Es compatible con Windows 10

    - Configurar sin necesidad de ninguna configuración adicional para los entornos locales  

    - Al habilitar algunas opciones de configuración de Azure AD, se pueden permitir que los usuarios unir dispositivos a Azure AD a través de la experiencia de instalación de Windows (OOBE)  

    - Para obtener más información consulte el tema [How to: Planee la implementación de Azure AD join](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  

- **Híbrida de dispositivos Unidos a AD Azure**: Unir los dispositivos Unidos a un dominio existentes a Azure AD  

    - Es compatible con Windows 10, Windows 8.1 y Windows 7

    - Configurar el uso de notificaciones de AD FS o Azure AD Connect  

    - Para Windows 10 la combinación tiene lugar en el contexto del equipo, por lo que los usuarios no tienen que realizar pasos adicionales  

    - Para obtener más información, vea [cómo planear su implementación híbrida de la unión de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)  

Ambas opciones ofrecen una funcionalidad similar para los usuarios. Es flexible, puede elegir cualquiera de ellos según sus necesidades. Por ejemplo, puede [acceder a los recursos locales](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso) desde equipos unidos a AD de Azure, aunque no estén unidos a Active Directory. 

Se pueden unir dispositivos a Azure AD en diversos entornos, sin importar su [método de autenticación](https://docs.microsoft.com/azure/security/azure-ad-choose-authn). Por ejemplo, la autenticación federada o autenticación en la nube. 

Si ya tiene un Active Directory local, la configuración de cualquiera de las opciones es sencillo. 



## <a name="benefits"></a>Ventajas

Al unir dispositivos a Azure AD proporciona las siguientes ventajas a su organización:

#### <a name="single-sign-on-to-cloud-resources"></a>Inicio de sesión único a los recursos de nube
En los dispositivos Unidos a Azure AD, obtendrá una experiencia integrada de acceso a los recursos en la nube o local. Una vez que inicie sesión en una máquina de Windows que está unida a Azure AD, obtendrá un inicio de sesión único para todas las aplicaciones sin las peticiones de inicio de sesión adicionales.  

#### <a name="windows-hello-for-business"></a>Windows Hello para empresas
Windows Hello para empresas ofrece una autenticación sin contraseña segura a Windows 10. Mediante la combinación de los dispositivos a Azure AD, puede habilitar Windows Hello para empresas en la base para los recursos en la nube y locales de usuarios. Windows Hello para empresas elimina el problema de tener que recordar contraseñas complejas o exponer por accidente en ellos. Su proceso de inicio de sesión es sencilla y segura. 

Para obtener más información, vea [Windows Hello para empresas](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

#### <a name="device-based-conditional-access"></a>Acceso condicional basado en dispositivos
Habilitar el acceso condicional basado en el estado del dispositivo para proteger mejor los datos de su organización. Acceso condicional basado en dispositivo requiere un dispositivo administrado. Este dispositivo debe ser un dispositivo compatible o un dispositivo unido a AD Azure híbrido. Para dispositivos Unidos a AD Azure, necesita Intune para marcar el dispositivo como compatible. Pero Azure híbrido dispositivos Unidos a AD, el estado del dispositivo se usa para evaluar el acceso condicional. Administración conjunta le proporciona la ventaja adicional de la evaluación de cumplimiento a través de Intune de Azure híbrido dispositivos Unidos a AD. Esta característica garantiza que la configuración del dispositivo está intacta. 

Para obtener más información sobre el acceso condicional basado en dispositivos, consulte [How To: Requerir que los dispositivos administrados para el acceso a la aplicación en la nube con acceso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

#### <a name="automatic-device-licensing"></a>Licencias de dispositivo automático
Todos los dispositivos Windows 10 Unidos a Azure AD que se vaya a través de la comprobación de licencia. Estas comprobaciones le permiten les actualizar automáticamente Pro a Enterprise a través de la nube de Microsoft. Cuando se quita la suscripción correspondiente al usuario, el dispositivo degrada automáticamente su licencia. Esta característica proporciona un único panel de control para la administración de licencias de Windows, sin los complicados procesos o sistemas locales.

#### <a name="self-service-functionality"></a>Funcionalidad de autoservicio
Funcionalidad de autoservicio incluye el restablecimiento de contraseña de autoservicio y la clave de recuperación de BitLocker. Azure AD también proporciona opciones directas para restablecer la contraseña o tener acceso a las claves de recuperación de BitLocker. Puede usar Azure AD para restablecer su contraseña directamente desde la pantalla de bloqueo de Windows, en lugar de desde un explorador web. Estas características reducen la fricción para los usuarios y ayudar a reducir los costos del departamento de soporte técnico para su organización.  

Para obtener más información, consulte [inicio rápido: Restablecimiento de contraseña de autoservicio](https://docs.microsoft.com/azure/active-directory/authentication/quickstart-sspr).

#### <a name="enterprise-state-roaming"></a>De Enterprise state roaming
Todos los dispositivos Unidos a Azure AD pueden sincronizar su configuración en la nube. Todos los dispositivos a la que un usuario inicia sesión en las sincronizaciones toda su configuración de una experiencia más productiva.  



## <a name="value-proposition"></a>Propuesta de valor

Unir los dispositivos a Azure AD a través de cualquiera de estos métodos acelera su transformación digital. Amplía la funcionalidad proporcionada por Microsoft 365. Tendrá una experiencia mejorada y tendrá mayor seguridad para los datos. 

Azure AD proporciona varias opciones para facilitar el trabajo de carga, por ejemplo:

- Administrar todas las identidades de dispositivo de su organización desde un único lugar  

- Reduzca sus costos del departamento de soporte técnico habilitando el restablecimiento de contraseña de autoservicio. A continuación, los usuarios puede restablecer la contraseña de la pantalla de bloqueo de Windows 10 en el dispositivo en cualquier momento.  



## <a name="configure"></a>Configurar

Si ya tiene un entorno de Active Directory local y quiere unir sus dispositivos Unidos a Azure AD, configure hybrid Azure dispositivos Unidos a AD. Para obtener más información, [cómo planear su implementación híbrida de la unión de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan). 

Configuration Manager tiene un configuración de cliente para [registrar automáticamente nuevos dispositivos de Windows 10 Unidos a un dominio con Azure AD](/sccm/core/clients/deploy/about-client-settings#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). Para obtener más información sobre cómo configurar la configuración de cliente, consulte [cómo configurar el cliente](/sccm/core/clients/deploy/configure-client-settings).

Si desea configurar Azure AD-join para sus dispositivos sin unirlos también a su dominio local, revise las consideraciones para Azure AD-join en su entorno. Una vez decidido ir con unión a Azure AD, tiene muchas opciones para implementar según las necesidades de su organización. Vea los siguientes artículos para más información:
- [Cómo: Planee la implementación de Azure AD join](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  
- [Descripción de las opciones de aprovisionamiento](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  

