---
title: 'Cómo crear perfiles de VPN '
titleSuffix: Configuration Manager
description: Aprenda a crear perfiles de VPN en System Center Configuration Manager.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 677a3ef2086f20d94bd0ee6fca983a2cc429d329
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65494844"
---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>Cómo crear perfiles de VPN en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los tipos de conexión disponibles para las diferentes plataformas de dispositivos se describen en [Perfiles de VPN en System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  

En el caso de conexiones VPN de terceros, distribuya la aplicación VPN antes de implementar el perfil de VPN. Si no implementa la aplicación, se les pedirá a los usuarios que lo hagan cuando intenten conectarse a la VPN. Para aprender a implementar aplicaciones, consulte [Deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md) (Cómo implementar aplicaciones con System Center Configuration Manager).

### <a name="create-a-vpn-profile"></a>Crear un perfil de VPN   

1. En la consola de Configuration Manager, pulse **Activos y compatibilidad** > **Configuración de cumplimiento** > **Acceso a los recursos de la compañía** > **Perfiles de VPN**.  

2. En la pestaña **Inicio**, en el grupo **Crear**, pulse **Crear perfil de VPN**.  


3. Complete la página **General**. Tenga en cuenta lo siguiente:  

   - Seleccione la **plataforma** adecuada.

      - Si selecciona la plataforma Windows 8.1, tiene la opción de elegir **Import an existing VPN profile item from a file** (Importar un perfil de VPN existente de un archivo) para importar información de perfil de VPN que se ha exportado a un archivo XML.

   - No use los caracteres \\/:*?&lt;>&#124;, o el carácter de espacio en el nombre de perfil de VPN. Estos caracteres no se admiten en el perfil de VPN de Windows Server.  


4. En la página **Conexión**, especifique:  

   - **Tipo de conexión**: elija el tipo de conexión VPN. Puede elegir entre los tipos de conexión de la tabla siguiente.  

   - **Lista de servidores**: agregue un nuevo servidor que se usará para la conexión VPN. Según el tipo de conexión, puede agregar uno o más servidores VPN y especificar el servidor predeterminado.  

     > [!NOTE]  
     >  Los dispositivos que ejecutan iOS no admiten el uso de varios servidores VPN. Si configura varios servidores VPN y, a continuación, implementa el perfil de VPN en un dispositivo iOS, solo se utilizará el servidor predeterminado.  

     En esta tabla se proporcionan opciones para los tipos de conexión. Consulte la documentación del servidor VPN para más información.

| &nbsp;&nbsp;Opción&nbsp;&nbsp; | Más información | &nbsp;&nbsp;Conexión&nbsp;tipo&nbsp;&nbsp; |  
|----------------|----------------------|---------------------|  
|**Dominio Kerberos**     |El dominio kerberos de autenticación que quiere usar. Un dominio de autenticación es una agrupación de recursos de autenticación usada por el tipo de conexión Pulse Secure.|Pulse Secure|    
|**Rol**        |El rol de usuario que tiene acceso a esta conexión. |Pulse Secure|  
|**Dominio o grupo de inicio de sesión** |El nombre del grupo o dominio de inicio de sesión al que quiere conectarse.|Dell SonicWALL Mobile Connect|  
|**Huella digital**  |Una cadena, por ejemplo "Código de huella digital de Contoso", que se usará para comprobar que se puede confiar en el servidor VPN.<br /><br /> Una huella digital se puede:<br /><br /> - Enviar al cliente para que sepa que puede confiar en cualquier servidor que presente esa misma huella digital al conectarse.<br /><br /> - Si el dispositivo todavía no tiene la huella digital, pedirá al usuario que confíe en el servidor VPN al que se está conectando mientras muestra la huella digital (el usuario comprueba la huella digital manualmente y pulsa **Confiar** para conectar).|VPN móvil de punto de comprobación|  
|**Enviar todo el tráfico de red a través de la conexión VPN** |Si no se selecciona esta opción, puede especificar rutas adicionales para la conexión (para los tipos de conexión **Microsoft SSL [SSTP]**, **Microsoft Automatic**, **IKEv2**, **PPTP** y **L2TP** ), lo que se conoce como túnel dividido o VPN.<br /><br /> Solo las conexiones con la red de la empresa se envían a través de un túnel VPN. El túnel de VPN no se utiliza al conectarse a recursos de Internet. |Todos|  
|**Sufijo DNS específico de la conexión** |El sufijo del sistema de nombres de dominio (DNS) específico de la conexión para esta.|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
|**Omitir VPN al conectarse a la red Wi-Fi de empresa**  |La conexión VPN no se usará cuando el dispositivo se conecte a la red Wi-Fi de la empresa.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN móvil de punto de comprobación<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - L2TP|  
|**Omitir VPN al conectarse a la red Wi-Fi doméstica**  |La conexión VPN no se usará cuando el dispositivo se conecte a una red Wi-Fi doméstica.|Todos|  
|**VPN por aplicación (iOS 7 y versiones posteriores, Mac OS X 10.9 y versiones posteriores)** |Asocie esta conexión VPN con una aplicación iOS para que la conexión se abra cuando se ejecute la aplicación. Puede asociar el perfil de VPN con una aplicación al implementarla.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN móvil de punto de comprobación|  
|**XML personalizado (opcional)** |Especifique los comandos XML personalizados que configuran la conexión VPN.<br /><br /> Ejemplo:<br /><br /> Para **Pulse Secure**:<br /><br /> **&lt;pulse-schema><br /> &nbsp; &lt;isSingleSignOnCredential>true&lt;/isSingleSignOnCredential\><br />&lt;/pulse-schema>**<br /><br /> Para **CheckPoint Mobile VPN**:<br /><br /> **&lt;CheckPointVPN <br /> &nbsp; port="443" name="CheckPointSelfhost" <br /> &nbsp; sso="true" <br /> &nbsp; debug="3"<br />/>**<br /><br /> Para **Dell SonicWALL Mobile Connect**:<br /><br /> **&lt;MobileConnect\><br />&nbsp; &nbsp; &lt;Compression\>false&lt;/Compression\><br />&nbsp; &nbsp; &lt;debugLogging\>True&lt;/debugLogging\><br />&nbsp; &nbsp; &lt;packetCapture\>False&lt;/packetCapture\><br />&lt;/MobileConnect\>**<br /><br /> Para **F5 Edge Client**:<br /><br /> **&lt;f5-vpn-conf>&lt;single-sign-on-credential>&lt;/f5-vpn-conf>**<br /><br /> Consulte la documentación de VPN de cada fabricante para más información sobre cómo escribir comandos XML personalizados.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN móvil de punto de comprobación|  

> [!NOTE]  
>  Para información específica para crear perfiles de VPN para dispositivos móviles, consulte [Create VPN Profiles](../../mdm/deploy-use/create-vpn-profiles.md) (Crear perfiles de VPN).  

Complete el asistente. El nuevo perfil de VPN se muestra en el nodo **Perfiles de VPN** en el área de trabajo **Activos y compatibilidad** .

### <a name="next-steps"></a>Pasos siguientes

- En el caso de conexiones VPN de terceros, distribuya la aplicación VPN antes de implementar el perfil de VPN. Si no implementa la aplicación, se les pedirá a los usuarios que lo hagan cuando intenten conectarse a la VPN. Para aprender a implementar aplicaciones, consulte [Deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md) (Cómo implementar aplicaciones con System Center Configuration Manager).

- Implemente el perfil de VPN tal como se describe en [How to deploy profiles in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md) (Cómo implementar perfiles en System Center Configuration Manager).  
