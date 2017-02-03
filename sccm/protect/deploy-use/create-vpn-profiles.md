---
title: "Cómo crear perfiles de VPN en System Center Configuration Manager | Microsoft Docs"
description: Aprenda a crear perfiles de VPN en System Center Configuration Manager.
ms.custom: 
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: 15
author: nbigman
caps.handback.revision: 0
ms.author: nbigman
ms.manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 8a5dc7361da34f3e6b926acd35c72c0c0767ce70
ms.openlocfilehash: 73b8d28deb6e2c57c92ead2f0fee4d7a2d92f5d4


---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>Cómo crear perfiles de VPN en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los tipos de conexión disponibles para las diferentes plataformas de dispositivos se describen en [Perfiles de VPN en System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  

En el caso de conexiones VPN de terceros, distribuya la aplicación VPN antes de implementar el perfil de VPN. Si no implementa la aplicación, se les pedirá a los usuarios que lo hagan cuando intenten conectarse a la VPN. Para aprender a implementar aplicaciones, consulte [Deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md) (Cómo implementar aplicaciones con System Center Configuration Manager).

### <a name="create-a-vpn-profile"></a>Crear un perfil de VPN   

1.  En la consola de Configuration Manager, pulse **Activos y compatibilidad** > **Configuración de cumplimiento** > **Acceso a los recursos de la compañía** > **Perfiles de VPN**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, pulse **Crear perfil de VPN**.  


1.  Complete la página **General**. y tenga en cuenta lo siguiente:  

    - No use los caracteres \\/:*?<>&#124;, o el carácter de espacio en el nombre de perfil de VPN. Estos caracteres no se admiten en el perfil de VPN de Windows Server.  

     -   Seleccione **Importar un elemento de perfil de VPN existente desde un archivo** para importar información de perfil de VPN que se ha exportado a un archivo XML (solo Windows 8.1 y Windows RT).  

1.  En la página **Conexión**, especifique:  

    -   **Tipo de conexión**: elija el tipo de conexión VPN. Puede elegir entre los tipos de conexión de la tabla siguiente.  

    -   **Lista de servidores**: agregue un nuevo servidor que se usará para la conexión VPN. Según el tipo de conexión, puede agregar uno o más servidores VPN y especificar el servidor predeterminado.  

        > [!NOTE]  
        >  Los dispositivos que ejecutan iOS no admiten el uso de varios servidores VPN. Si configura varios servidores VPN y, a continuación, implementa el perfil de VPN en un dispositivo iOS, solo se utilizará el servidor predeterminado.  

     En esta tabla se proporcionan opciones para los tipos de conexión. Consulte la documentación del servidor VPN para más información.  

    |Opción|Más información|Tipo de conexión|  
    |------------|----------------------|---------------------|  
    |**Dominio Kerberos**|El dominio kerberos de autenticación que quiere usar. Un dominio de autenticación es una agrupación de recursos de autenticación usada por el tipo de conexión Pulse Secure.|Pulse Secure|  
    |**Rol**|El rol de usuario que tiene acceso a esta conexión.|Pulse Secure|  
    |**Dominio o grupo de inicio de sesión**|El nombre del grupo o dominio de inicio de sesión al que quiere conectarse.|Dell SonicWALL Mobile Connect|  
    |**Huella digital**|Una cadena, por ejemplo "Código de huella digital de Contoso", que se usará para comprobar que se puede confiar en el servidor VPN.<br /><br /> Una huella digital se puede:<br /><br /> - Enviar al cliente para que sepa que puede confiar en cualquier servidor que presente esa misma huella digital al conectarse.<br /><br /> - Si el dispositivo todavía no tiene la huella digital, pedirá al usuario que confíe en el servidor VPN al que se está conectando mientras muestra la huella digital (el usuario comprueba la huella digital manualmente y pulsa **Confiar** para conectar).|VPN móvil de punto de comprobación|  
    |**Enviar todo el tráfico de red a través de la conexión VPN**|Si no se selecciona esta opción, puede especificar rutas adicionales para la conexión (para los tipos de conexión **Microsoft SSL [SSTP]**, **Microsoft Automatic**, **IKEv2**, **PPTP** y **L2TP** ), lo que se conoce como túnel dividido o VPN.<br /><br /> Solo las conexiones con la red de la empresa se envían a través de un túnel VPN. El túnel de VPN no se utiliza al conectarse a recursos de Internet.|Todos|  
    |**Sufijo DNS específico de la conexión**|El sufijo del sistema de nombres de dominio (DNS) específico de la conexión para esta.|- <br />                            Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - <br />                            IKEv2<br /><br /> - <br />                            PPTP<br /><br /> - <br />                            L2TP|  
    |**Omitir VPN al conectarse a la red Wi-Fi de empresa**|La conexión VPN no se usará cuando el dispositivo se conecte a la red Wi-Fi de la empresa.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN móvil de punto de comprobación<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - L2TP|  
    |**Omitir VPN al conectarse a la red Wi-Fi doméstica**|La conexión VPN no se usará cuando el dispositivo se conecte a una red Wi-Fi doméstica.|Todos|  
    |**VPN por aplicación (iOS 7 y versiones posteriores, Mac OS X 10.9 y versiones posteriores)**|Asocie esta conexión VPN con una aplicación iOS para que la conexión se abra cuando se ejecute la aplicación. Puede asociar el perfil de VPN con una aplicación al implementarla.|- <br />                        Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN móvil de punto de comprobación|  
    |**XML personalizado (opcional)**|Especifique los comandos XML personalizados que configuran la conexión VPN.<br /><br /> Ejemplos:<br /><br /> Para **Pulse Secure**:<br /><br /> **<pulse-schema><isSingleSignOnCredential\>true</isSingleSignOnCredential\></pulse-schema>**<br /><br /> Para **CheckPoint Mobile VPN**:<br /><br /> **&lt;CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" /\>**<br /><br /> Para **Dell SonicWALL Mobile Connect**:<br /><br /> **<MobileConnect\><Compression\>false</Compression\><debugLogging\>True</debugLogging\><packetCapture\>False</packetCapture\></MobileConnect\>**<br /><br /> Para **F5 Edge Client**:<br /><br /> **&lt;f5-vpn-conf&gt;&lt;single-sign-on-credential /&gt;&lt;/f5-vpn-conf&gt;**<br /><br /> Consulte la documentación de VPN de cada fabricante para más información sobre cómo escribir comandos XML personalizados.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN móvil de punto de comprobación|  

    ###   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Características de VPN de Windows 10 disponibles cuando se usa Configuration Manager con Intune  


    > [!NOTE]  
    > El nombre de un perfil de VPN que usa las características de VPN de Windows 10 no puede estar en formato Unicode ni incluir caracteres especiales.


    |Opción|Más información|Tipo de conexión|  
    |------------|----------------------|---------------------|  
    |**Omitir VPN al conectarse a la red Wi-Fi de empresa**|La conexión VPN no se usará cuando el dispositivo se conecte a la red Wi-Fi de la empresa. Escriba el nombre de red de confianza que se ha usado para determinar si el dispositivo está conectado a la red de la empresa.|Todos|  
    |**Reglas de tráfico de red**|Defina qué protocolos, puertos locales y remotos e intervalos de direcciones se habilitarán para la conexión VPN.<br /><br /> **Nota:** Si no se crea ninguna regla de tráfico de red, se habilitan todos los protocolos, puertos e intervalos de direcciones. Una vez creada una regla, la conexión VPN solo usará los protocolos, puertos e intervalos de direcciones que especifique en esa regla o en reglas adicionales.|Todos|  
    |**Rutas**|Rutas que usará la conexión VPN. Tenga en cuenta que la creación de más de 60 rutas puede producir un error en la directiva. |Todos|  
    |**Servidores DNS**|Qué servidores DNS usa la conexión VPN una vez establecida la conexión.|Todos|  
    |**Aplicaciones que se conectan automáticamente a la VPN**|Puede agregar aplicaciones o importar una lista de aplicaciones que usarán automáticamente la conexión VPN. El tipo de aplicación determinará el identificador de la aplicación. Para una aplicación de escritorio, proporcione la ruta del archivo de la aplicación. Para una aplicación universal, proporcione el nombre de familia de paquete (PFN). Para obtener información sobre cómo buscar el PFN de una aplicación, consulte [Find a package family name for per-app VPN](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md) (Buscar un nombre de familia de paquete para VPN por aplicación). |Todos|

    > [!IMPORTANT]
    > Se recomienda que proteja todas las listas de aplicaciones asociadas que se compilan para su uso en la configuración de VPN por aplicación. Si un usuario no autorizado modifica la lista y usted la importa en la lista de aplicaciones de VPN por aplicación, podría autorizar el acceso a VPN a aplicaciones que no deberían tener acceso. Una forma de proteger las listas de aplicaciones consiste en usar una lista de control de acceso (ACL).


1.  En la página **Método de autenticación** del asistente, especifique:  

    -   **Método de autenticación:** seleccione el método de autenticación que usará la conexión VPN. Métodos disponibles dependiendo del tipo de conexión como se muestra en esta tabla.  

        |Método de autenticación|Tipos de conexión admitidos|  
        |---------------------------|--------------------------------|  
        |**Certificados**<br /><br /> **Nota:** Si el certificado de cliente se usa para autenticar un servidor RADIUS, por ejemplo, un Servidor de directivas de redes, el nombre alternativo del sujeto en el certificado debe configurarse como el nombre principal de usuario.|- <br />                            Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN móvil de punto de comprobación|  
        |**Nombre de usuario y contraseña**|- <br />                            Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN móvil de punto de comprobación|  
        |**Microsoft EAP-TTLS**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - IKEv2<br /><br /> - L2TP|  
        |**EAP (PEAP) protegido de Microsoft**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Contraseña segura de Microsoft (EAP-MSCHAP v2)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Tarjeta inteligente u otro certificado**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**MSCHAP v2**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**RSA SecurID** (solo iOS)|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Usar certificados de máquina**|IKEv2|  

         En función de las opciones que seleccione, se le podría solicitar que especifique más información, como la siguiente:  

        -   **Recordar las credenciales de usuario en cada inicio de sesión**: las credenciales de usuario se recuerdan, de manera que el usuario no tiene que escribirlas cada vez que se conecte.  

        -   **Seleccionar un certificado de cliente para la autenticación de cliente**: seleccione el [certificado SCEP](introduction-to-certificate-profiles.md) de cliente que ha creado previamente y que se usará para autenticar la conexión VPN.   

            > [!NOTE]  
            >  Para dispositivos iOS, el perfil SCEP que seleccione se incrustará en el perfil de VPN. Para otras plataformas, se agrega una regla de aplicabilidad para garantizar que el perfil de VPN no se instala si el certificado no está presente o no es conforme.  
            >   
            >  Si el certificado SCEP que especifique no es compatible o no se implementó, el perfil de VPN no se instalará en el dispositivo.
            >  
            >  Los dispositivos que ejecutan iOS solo admiten RSA SecurID y MSCHAP v2 como métodos de autenticación cuando el tipo de conexión es PPTP. Para evitar errores, implemente un perfil de VPN PPTP independiente en los dispositivos que ejecutan iOS.  

        - **Acceso condicional**
            - Pulse **Habilitar acceso condicional para esta conexión VPN** para asegurarse de que los dispositivos que se conectan a la VPN se prueban para el cumplimiento del acceso condicional antes de la conexión. Las directivas de cumplimiento se describen en [Device compliance policies in System Center Configuration Manager (Directivas de cumplimiento de dispositivos en System Center Configuration Manager)](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md).
            - Pulse **Habilitar inicio de sesión único (SSO) con certificado alternativo** para elegir un certificado diferente al certificado de autenticación de VPN para el cumplimiento del dispositivo. Si elige esta opción, proporcione el **EKU** (lista separada por comas) y el **Hash del emisor** para el certificado correcto que el cliente de VPN debe buscar.

         - **Windows Information Protection**: proporcione la identidad corporativa administrada por la empresa, que normalmente es el dominio principal de la organización, por ejemplo, *contoso.com*. Puede especificar varios dominios que sean propiedad de la organización separándolos con el carácter "|". Por ejemplo, *contoso.com|newcontoso.com*.   
            Para obtener más información sobre Windows Information Protection, consulte [Crear una directiva de Windows Information Protection (WIP) con Microsoft Intune](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune).   

         ![Configurar el acceso condicional para VPN](../media/vpn-conditional-access.png)


        > [!NOTE]  
        >
        >Para algunos métodos de autenticación, puede hacer clic en **Configurar** para abrir el cuadro de diálogo de propiedades de Windows (si la versión de Windows en la que ejecuta la consola de Configuration Manager es compatible con este método de autenticación), donde puede configurar las propiedades del método de autenticación.  


1.  En la página **Configuración de proxy** del **Asistente para crear perfil de VPN**, active la casilla **Configurar configuración de proxy para este perfil de VPN** si su conexión VPN usa un servidor proxy. Después, proporcione la información del servidor proxy. Para obtener más información, consulte la documentación de Windows Server.  

    > [!NOTE]  
    >  En los equipos Windows 8.1, el perfil de VPN no mostrará la información de proxy hasta que se conecte a la VPN con ese equipo.  


2. Configurar opciones de DNS adicionales (si es necesario)  
 En la página **Configurar una conexión VPN automática**, puede configurar las opciones siguientes:  

    -   **Habilitar VPN a petición** Use esta opción si quiere configurar opciones de DNS adicionales para dispositivos Windows Phone 8.1. Esta configuración solo se aplica a dispositivos Windows Phone 8.1 y solo se debe habilitar en los perfiles VPN que se van a implementar en dispositivos Windows Phone 8.1.

    -   Lista de sufijos DNS (solo dispositivos Windows Phone 8.1): configura los dominios que establecerán una conexión VPN. Para cada dominio que especifique, debe agregar el sufijo DNS, la dirección del servidor DNS y una de las siguientes acciones a petición:  

        -   **No establecer nunca**: no se abre nunca una conexión VPN.  

        -   **Establecer si es necesario**: solo se abre una conexión VPN si el dispositivo necesita conectarse a recursos.  

        -   **Establecer siempre**: siempre se abre la conexión VPN.  

    -   **Combinar**: copia todos los sufijos DNS que configuró en la **Lista de redes de confianza**.  

    -   **Lista de redes de confianza** (solo dispositivos Windows Phone 8.1): especifique un sufijo DNS en cada línea. Si el dispositivo se encuentra en una red de confianza, no se abrirá la conexión VPN.  

    -   **Lista de búsqueda de sufijos** (solo dispositivos Windows Phone 8.1): especifique un sufijo DNS en cada línea. Al conectarse a un sitio web mediante un nombre corto, se buscará cada sufijo DNS.  

     Por ejemplo, especifica los sufijos DNS **domain1.contoso.com** y **domain2.contoso.com** y, después, visita la dirección URL **http://mywebsite**. Se buscarán las siguientes direcciones:  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

    > [!NOTE]  
    >  Solo para dispositivos Windows Phone 8.1  
    >   
    >  Si se selecciona la opción **Enviar todo el tráfico de red a través de la conexión VPN** y la conexión VPN usa el túnel completo, la conexión VPN se abrirá automáticamente para el primer perfil aprovisionado en el dispositivo. Si desea que otro perfil abra automáticamente una conexión, debe convertirlo en el perfil predeterminado del dispositivo.  
    >   
    >  Si no se selecciona la opción **Enviar todo el tráfico de red a través de la conexión VPN** y la conexión VPN usa el túnel dividido, puede abrirse automáticamente una conexión VPN si se configuran las rutas o un sufijo DNS específico de la conexión.  


1. En la página **Plataformas admitidas** del **Asistente para crear perfil de VPN**, seleccione los sistemas operativos en los que se instalará el perfil de VPN o haga clic en **Seleccionar todo** para instalar el perfil de VPN en todos los sistemas operativos disponibles.  

2. Complete el asistente. El nuevo perfil de VPN se muestra en el nodo **Perfiles de VPN** en el área de trabajo **Activos y compatibilidad** .  

### <a name="next-steps"></a>Pasos siguientes

- En el caso de conexiones VPN de terceros, distribuya la aplicación VPN antes de implementar el perfil de VPN. Si no implementa la aplicación, se les pedirá a los usuarios que lo hagan cuando intenten conectarse a la VPN. Para aprender a implementar aplicaciones, consulte [Deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md) (Cómo implementar aplicaciones con System Center Configuration Manager).

- Implemente el perfil de VPN tal como se describe en [How to deploy profiles in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md) (Cómo implementar perfiles en System Center Configuration Manager).  



<!--HONumber=Dec16_HO5-->


