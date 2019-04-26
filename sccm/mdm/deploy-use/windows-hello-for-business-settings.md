---
title: Configuración de Windows Hello para empresas
titleSuffix: Configuration Manager
description: Aprenda a integrar Windows Hello para empresas con Configuration Manager.
ms.date: 12/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c0593c07-5dd7-4d23-a0d8-d30165f49ef7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 71f853034133e2ec73a4d8e606c2e0c0c94841a4
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62227590"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager-hybrid"></a>Windows Hello para empresas en Configuration Manager (híbrido)

*Se aplica a: System Center Configuration Manager (Rama actual)*

Administrador de configuración permite la integración con Windows Hello para empresas (anteriormente Microsoft Passport para Windows), que es un método de inicio de sesión alternativo para dispositivos Windows 10. Hello para empresas utiliza Active Directory o una cuenta de Azure Active Directory para reemplazar una contraseña, una tarjeta inteligente o una tarjeta inteligente virtual. Hello para empresas permite usar un **gesto de usuario** al iniciar sesión, en lugar de una contraseña. Un gesto de usuario podría ser un simple PIN, una autenticación biométrica o un dispositivo externo, como un lector de huellas digitales.  

> [!Important]  
> A partir de diciembre de 2017, Windows Hello para empresas en Configuration Manager es un [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Implementación de Windows Server 2016 Active Directory Federation Services autoridad de registro (ADFS RA) es más sencillo, proporciona una mejor experiencia de usuario y tiene una experiencia de inscripción de certificados más determinista. Para obtener más información, vea [Windows Hello para empresas](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification).  


Configuration Manager se integra con Windows Hello para empresas de dos maneras:  

- Puede usar Configuration Manager para controlar cuáles gestos pueden emplear los usuarios para iniciar sesión y cuáles no.  

- Puede almacenar certificados de autenticación en el proveedor de almacenamiento de claves de Windows Hello para empresas. Para obtener más información, consulte [Introduction to certificate profiles in System Center Configuration Manager](create-pfx-certificate-profiles.md) (Introducción a perfiles de certificado en Configuration Manager).  

- Puede implementar directivas de Windows Hello para empresas para dispositivos de Windows 10 unidos a dominio que ejecutan el cliente de Configuration Manager. Esta configuración se describe en [Configuración de Windows Hello para empresas en dispositivos unidos a dominio de Windows 10](/sccm/protect/deploy-use/windows-hello-for-business-settings#configure-windows-hello-for-business-on-domain-joined-windows-10-devices). Cuando se usa Configuration Manager con Intune (híbrido), puede configurar estas opciones en Windows 10 y dispositivos Windows 10 Mobile, pero no en dispositivos unidos a dominio que ejecutan al cliente de Configuration Manager.   

Para obtener información general acerca de cómo configurar Windows Hello para empresas, consulte [Windows Hello para empresas en Configuration Manager](/sccm/protect/deploy-use/windows-hello-for-business-settings).



## <a name="configure-windows-hello-for-business-settings-hybrid"></a>Configuración de Windows Hello para empresas (híbrido)  

1. En la consola de Configuration Manager, haga clic en **Administración** > **Servicios de nube** > **Suscripciones a Microsoft Intune**.  

2. En la lista, seleccione su suscripción de Microsoft Intune y, luego, en la pestaña **Inicio** , en el grupo **Suscripción** , haga clic en **Configurar plataformas** > **Windows (MDM)**.  

3. En la pestaña **Windows Hello para empresas** del cuadro de diálogo **Propiedades de suscripción de Microsoft Intune** , elija entre los siguientes valores que afectarán a todos los dispositivos de Windows 10 y Windows 10 Mobile inscritos:  

   - **Deshabilitar Windows Hello para empresas para los dispositivos inscritos** o **Habilitar Windows Hello para empresas para los dispositivos inscritos** : habilita o deshabilita el uso de Windows Hello para empresas en todos los dispositivos Windows 10 y Windows 10 Mobile inscritos.  

   - **Usar un Módulo de plataforma segura (TPM)** : un chip de Módulo de plataforma segura (TPM) ofrece una capa adicional de seguridad de datos. Elija uno de los siguientes valores:  

     -   **Requerido** (valor predeterminado): solo los dispositivos con un TPM accesible pueden aprovisionar Windows Hello para empresas.  

     -   **Preferido** : los dispositivos intentan primero usar un TPM. Si no está disponible, pueden usar el cifrado de software.  

   - **Requerir una longitud mínima para el PIN** : especifique el número mínimo de caracteres necesarios para el PIN de Windows Hello para empresas. Debe usar al menos 4 caracteres (el valor predeterminado es 6 caracteres).  

   - **Requerir una longitud máxima para el PIN** : especifique el número máximo de caracteres necesarios para el PIN de Windows Hello para empresas. Puede usar hasta 127 caracteres.  

   - **Requerir minúsculas en el PIN** : especifica si se deben usar minúsculas en el PIN de Windows Hello para empresas. Elija de entre las siguientes opciones:  

     -   **Permitido** : los usuarios pueden usar minúsculas en su PIN.  

     -   **Requerido** : los usuarios deben incluir al menos un carácter en minúscula en su PIN.  

     -   **No permitido** (valor predeterminado): los usuarios no deben usar caracteres en minúsculas en su PIN.  

   - **Requerir mayúsculas en el PIN** : especifica si se deben usar mayúsculas en el PIN de Windows Hello para empresas. Elija de entre las siguientes opciones:  

     -   **Permitido** : los usuarios pueden usar mayúsculas en su PIN.  

     -   **Requerido** : los usuarios deben incluir al menos un carácter en mayúscula en su PIN.  

     -   **No permitido** (valor predeterminado): los usuarios no deben usar caracteres en mayúsculas en su PIN.  

   - **Requerir caracteres especiales** : especifica el uso de caracteres especiales en el PIN. Elija de entre las siguientes opciones:  

     - **Permitido** : los usuarios pueden usar caracteres especiales en su PIN.  

     - **Requerido** : los usuarios deben incluir al menos un carácter especial en su PIN.  

     - **No permitido** (valor predeterminado): los usuarios no deben usar caracteres especiales en su PIN (este es el comportamiento si no se ha definido la configuración).  

       Entre los caracteres especiales se incluyen: **! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**.  

   - **Requerir expiración del PIN (días)**: especifica el número de días antes de que se deba cambiar el PIN del dispositivo. El valor predeterminado es 41 días.  

   - **Evitar la reutilización de los PIN anteriores** : use esta opción para restringir la reutilización de los PIN usados anteriormente. El valor predeterminado es que no se pueden usar los 5 últimos PIN.  

   - **Habilitar los gestos biométricos** : habilita la autenticación biométrica como el reconocimiento facial o la huella digital como alternativa a un PIN para Windows Hello para empresas. Los usuarios todavía deben configurar un PIN de trabajo por si produce un error en la autenticación biométrica.  

      Si establece en **Habilitado**, Windows Hello para empresas permite la autenticación biométrica.  Si establece la opción en **Deshabilitado**, Windows Hello para empresas impide la autenticación biométrica (para todos los tipos de cuenta).  

   - **Usar la protección mejorada contra suplantación de identidad cuando esté disponible** : configura si la protección mejorada contra suplantación de identidad se usa en dispositivos que la admiten.  

      Si establece en **Habilitado**, Windows requiere que todos los usuarios usen el anti-spoofing para características faciales cuando se admitan.  

   - **Usar Passport remoto** : si esta opción se establece en **Habilitado**, los usuarios pueden usar una cuenta de Hello para empresas para que actúe como dispositivo complementario portátil para la autenticación del equipo de escritorio. El equipo de escritorio debe estar unido a Azure Active Directory y el dispositivo complementario debe configurarse con un PIN de Windows Hello para empresas.  

4. Cuando termine, haga clic en **Aceptar**.  



## <a name="see-also"></a>Consulte también  

[Proteger la infraestructura de datos y del sitio](/sccm/protect/understand/protect-data-and-site-infrastructure)

[Windows Hello para empresas](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)  
