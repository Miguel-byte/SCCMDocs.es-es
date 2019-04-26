---
title: Perfiles de VPN
titleSuffix: Configuration Manager
description: Obtenga más información sobre los perfiles de VPN en dispositivos móviles en Configuration Manager.
ms.date: 06/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7accfe4c329b61c7791bc4b82028d48fdc81931
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62256598"
---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>Perfiles de VPN en dispositivos móviles en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use perfiles de VPN en Configuration Manager para implementar la configuración de VPN para los usuarios de dispositivos móviles de la organización. Mediante la implementación de esta configuración, se minimiza la intervención del usuario final necesaria para conectarse a los recursos de la red de la empresa.  

Por ejemplo, quiere configurar todos los dispositivos iOS para conectarse a un recurso compartido de archivos de la red corporativa. Cree un perfil de VPN con la configuración de conexión necesaria. Luego implemente este perfil para todos los usuarios con dispositivos iOS. Esos usuarios ven la conexión VPN en la lista de redes disponibles y pueden conectarse a esta red sin apenas esfuerzo.  

Cuando se crea un perfil de VPN, puede incluir una amplia gama de opciones de seguridad. Por ejemplo, puede especificar certificados para la validación de servidor y la autenticación de cliente que se han configurado mediante perfiles de certificado de Configuration Manager. Para obtener más información, consulte [Introduction to certificate profiles in System Center Configuration Manager](../../protect/deploy-use/introduction-to-certificate-profiles.md) (Introducción a perfiles de certificado en Configuration Manager).  



## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Perfiles de VPN en Configuration Manager con Intune

Para implementar perfiles en dispositivos iOS, Android, Windows Phone y Windows 8.1, estos deben estar inscritos en Microsoft Intune. También se pueden inscribir en Intune dispositivos de otras plataformas. Para obtener información sobre cómo realizar la inscripción, vea [Enroll devices in Microsoft Intune](/intune/device-enrollment) (Inscribir dispositivos en Microsoft Intune). 

En esta tabla se muestra qué tipo de conexión se admite para cada plataforma de dispositivo:  

 |Tipo de conexión|iOS y macOS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop y Mobile|  
 |---------------|---------------|-------|-----------|----------|--------------|-----------------|-----------------------------|  
 |Cisco AnyConnect|Sí<sup>1</sup>|Sí|No|No|No|No|No|
 |Cisco (IPsec)|Solo iOS|No|No|No|No|No|No|  
 |Pulse Secure|Sí|Sí|Sí|No|Sí|Sí|Sí|  
 |F5 Edge Client|Sí|Sí|Sí|No|Sí|Sí|Sí|  
 |Dell SonicWALL Mobile Connect|Sí|Sí|Sí|No|Sí|Sí|Sí|  
 |VPN móvil de punto de comprobación|Sí|Sí|Sí|No|Sí|Sí|Sí|  
 |Microsoft SSL (SSTP)|No|No|Sí|Sí|Sí|No|No|  
 |Microsoft Automatic|No|No|Sí|Sí|Sí|No|Sí|  
 |IKEv2|Sí (directiva personalizada, iOS 9 y versiones posteriores)|No|Sí|Sí|Sí|Sí|Sí|  
 |PPTP|Sí|No|Sí|Sí|Sí|No|Sí|  
 |L2TP|Sí|No|Sí|Sí|Sí|No|Sí (OMA-URI)|  

<sup>1</sup> a partir de la versión 1802, el uso del tipo de conexión de Cisco AnyConnect varía.<!--1357393-->  
   - Use la opción **Cisco Legacy AnyConnect** para perfiles de VPN en las siguientes versiones:
       - iOS con Cisco AnyConnect versión 4.0.5 o anteriores
       - macOS con cualquier versión de Cisco AnyConnect
   - Use la opción **Cisco AnyConnect** para perfiles de VPN en las siguientes versiones:
       - iOS con Cisco AnyConnect versión 4.0.7 o posteriores

     > [!Tip]  
     > Cisco AnyConnect 4.0.07x y versiones posteriores para iOS se introdujeron primero en la versión 1802 como una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). A partir de la [actualización 4163547](https://support.microsoft.com/help/4163547) de la versión 1802, ya no es una característica de versión preliminar.  
  
  
> [!Note]  
> Las versiones 3.0 y posteriores de F5 Access para iOS no son compatibles para los perfiles de VPN en la administración híbrida de dispositivos móviles. A este producto también se le conoce como F5 Access 2018. Si necesita crear perfiles de VPN para este cliente VPN, use Intune independiente. Las futuras versiones de iOS, incluida la versión 12, no admiten las versiones 2.1 o anteriores de F5 Access. Para más información, vea el [blog del equipo de soporte técnico de Microsoft Intune](https://aka.ms/iOS12_and_VPN).


## <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Características de VPN de Windows 10 disponibles cuando se usa Configuration Manager con Intune  

Las siguientes opciones están disponibles para todos los tipos de conexión en Windows 10:

- **Omitir VPN al conectarse a la red Wi-Fi de empresa**: La conexión VPN no se usa cuando el dispositivo está conectado a la red Wi-Fi de empresa. Escriba el nombre de red de confianza que se ha usado para determinar si el dispositivo está conectado a la red de la empresa.  

- **Las reglas de tráfico de red**: Establecer los protocolos, puerto local, puerto remoto y los intervalos de direcciones para habilitar para la conexión VPN.  

     > [!Note]  
     > Si no se crea ninguna regla de tráfico de red, se habilitan todos los protocolos, puertos e intervalos de direcciones. Una vez creada una regla, la conexión VPN solo usa los protocolos, puertos e intervalos de direcciones que especifique en esa regla o en reglas adicionales.  
  
- **Las rutas**: Rutas que usen la conexión VPN. La creación de más de 60 rutas puede producir un error en la directiva.  

- **Servidores DNS**: Servidores DNS que usa la conexión VPN una vez establecida la conexión.  

- **Las aplicaciones que se conectan automáticamente a la VPN**: Puede agregar aplicaciones o importar una lista de aplicaciones que usarán automáticamente la conexión VPN. El tipo de aplicación determina el identificador de la aplicación. Para una aplicación de escritorio, proporcione la ruta del archivo de la aplicación. Para una aplicación universal, proporcione el nombre de familia de paquete (PFN). Para obtener información sobre cómo buscar el PFN de una aplicación, consulte [Find a package family name for per-app VPN](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md) (Buscar un nombre de familia de paquete para VPN por aplicación).  

     > [!IMPORTANT]  
     > Proteja todas las listas de aplicaciones asociadas que se compilan para su uso en la configuración de VPN por aplicación. Si un usuario no autorizado modifica la lista y usted la importa a la lista de aplicaciones de VPN por aplicación, podría autorizar el acceso a VPN a aplicaciones que no deberían tener acceso. Una forma de proteger las listas de aplicaciones consiste en usar una lista de control de acceso (ACL).  



## <a name="create-vpn-profiles"></a>Crear perfiles de VPN


1. En el área de trabajo **Activos y compatibilidad** de la consola de Configuration Manager, expanda **Configuración de cumplimiento**, expanda **Acceso a los recursos de la compañía** y seleccione **Perfiles de VPN**. 

2. Haga clic en **Crear perfil de VPN** en la cinta de opciones.  

3. En la página **General**, especifique un **Nombre** y luego seleccione el **Tipo de perfil de VPN**.   
     > [!NOTE]  
     > El nombre de un perfil de VPN que usa las características de VPN de Windows 10 no puede estar en formato Unicode ni incluir caracteres especiales.


4. Si la página **Plataformas compatibles** está disponible, seleccione las versiones de sistema operativo para el tipo de perfil de VPN especificado anteriormente. Elija **Seleccionar todo** para instalar el perfil de VPN en todas las versiones de sistema operativo disponibles.  

5. Configure la conexión VPN en la página **Conexión**. Para obtener más información sobre estas opciones, vea el paso sobre la página Conexión en [Crear un perfil de VPN](/sccm/protect/deploy-use/create-vpn-profiles#create-a-vpn-profile).  

6. En la página **Método de autenticación**, especifique la configuración siguiente:  

   - **Método de autenticación**: Seleccione el método de autenticación que usa la conexión VPN. Métodos disponibles dependiendo del tipo de conexión como se muestra en esta tabla.  

     |Método de autenticación|Tipos de &nbsp;conexión&nbsp; admitidos|  
     |---------------------------|--------------------------------|  
     |**Certificados**<br /><br /> **Notas:**<ul><li>Si el certificado de cliente se autentica en un servidor RADIUS, como un Servidor de directivas de redes, establezca el nombre alternativo del firmante del certificado en el nombre principal de usuario.</li><li>En el caso de las implementaciones de Android, seleccione el identificador EKU y el valor de hash de huella digital del emisor de certificados. De lo contrario, los usuarios deben seleccionar manualmente el certificado adecuado.</li></ul>  |<ul><li>Cisco AnyConnect</li><li>Cisco Legacy AnyConnect</li><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> VPN móvil de punto de comprobación</li></ul>|  
     |**Nombre de usuario y contraseña**|<ul><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> VPN móvil de punto de comprobación</li></ul>|  
     |**Microsoft EAP-TTLS**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>IKEv2</li><li>L2TP</li></ul>|  
     |**EAP (PEAP) protegido de Microsoft**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Contraseña segura de Microsoft (EAP-MSCHAP v2)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Tarjeta inteligente u otro certificado**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**MSCHAP v2**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**RSA SecurID** (solo iOS)|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Usar certificados de máquina**|<ul><li>IKEv2</li></ul>|  

      En función de las opciones que seleccione, se le podría solicitar que especifique más información, como la siguiente:  

     - **Recordar las credenciales de usuario en cada inicio de sesión**: Se recuerdan las credenciales de usuario para que los usuarios no tengan que escribirlas cada vez que se conectan.  

     - **Seleccionar un certificado de cliente para autenticación de cliente**: Seleccione el cliente que ha creado anteriormente [certificado SCEP](create-pfx-certificate-profiles.md) que se usa para autenticar la conexión VPN.   

       > [!NOTE]  
       >  Para dispositivos iOS, el perfil SCEP que seleccione se incrusta en el perfil de VPN. Para otras plataformas, se agrega una regla de aplicabilidad para garantizar que el perfil de VPN no se instala si el certificado no está presente o no es conforme.  
       >   
       >  Si el certificado SCEP que especifique no es conforme o no se ha implementado, el perfil de VPN no se instala en el dispositivo.
       >  
       >  Los dispositivos que ejecutan iOS solo admiten RSA SecurID y MSCHAP v2 como métodos de autenticación cuando el tipo de conexión es PPTP. Para evitar errores, implemente un perfil de VPN PPTP independiente en los dispositivos que ejecutan iOS.   

     - **Acceso condicional**  
         - Pulse **Habilitar acceso condicional para esta conexión VPN** para asegurarse de que los dispositivos que se conectan a la VPN se prueban para el cumplimiento del acceso condicional antes de la conexión. Para obtener más información, vea [Directivas de cumplimiento de dispositivos](/sccm/protect/deploy-use/device-compliance-policies).  

         - Seleccione **Habilitar inicio de sesión único (SSO) con certificado alternativo** para elegir un certificado diferente al certificado de autenticación de VPN para el cumplimiento del dispositivo. Si elige esta opción, proporcione el **EKU** (lista separada por comas) y el **Hash del emisor** para el certificado correcto que el cliente de VPN debe buscar.  

       - Para **Windows Information Protection**, proporcione la identidad corporativa administrada por la empresa, que normalmente es el dominio principal de la organización, por ejemplo, *contoso.com*. Puede especificar varios dominios que sean propiedad de la organización si los separa con el carácter "|". Por ejemplo, *contoso.com|newcontoso.com*. Para obtener más información, vea [Creación e implementación de una directiva de protección de aplicaciones de Windows Information Protection (WIP) con Intune](/intune/windows-information-protection-policy-create).   

       ![Asistente para crear perfil de VPN, página Método de autenticación](media/vpn-conditional-access.png)

       Si la versión del cliente Windows lo admite, la opción de **Configurar** el método de autenticación está disponible. Esta opción abre el cuadro de diálogo de propiedades de Windows para configurar el método de autenticación. Si **Configurar** está deshabilitado, utilice medios alternativos para configurar las propiedades del método de autenticación.  

7. En la página **Configuración de proxy** del **Asistente para crear perfil de VPN**, active la casilla **Configurar configuración de proxy para este perfil de VPN** si su conexión VPN usa un servidor proxy. Después, proporcione la información del servidor proxy. Para obtener más información, consulte la documentación de Windows Server.  

   > [!NOTE]  
   >  En los equipos Windows 8.1, el perfil de VPN no mostrará la información de proxy hasta que se conecte a la VPN con ese equipo.  


8. Configure opciones de DNS adicionales si fuera necesario.  

9. Finalice el asistente. El nuevo perfil de VPN se muestra en el nodo **Perfiles de VPN** en el área de trabajo **Activos y compatibilidad** .  



## <a name="next-steps"></a>Pasos siguientes  
Para obtener más información sobre cómo implementar perfiles de VPN, vea [Implementación de perfiles de Wi-Fi, VPN, correo electrónico y certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

 Use los artículos siguientes para planear, configurar, operar y mantener perfiles de VPN:  

-   [Requisitos previos de los perfiles de VPN](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Seguridad y privacidad de los perfiles de VPN](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
