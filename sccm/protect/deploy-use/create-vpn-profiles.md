---
title: "Cómo crear perfiles de VPN en System Center Configuration Manager | Microsoft Docs"
description: Aprenda a crear perfiles de VPN en System Center Configuration Manager.
ms.custom: 
ms.date: 11/18/2016
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
ms.sourcegitcommit: 828e2ac9a3f9bcea1571d24145a1021fdf1091f3
ms.openlocfilehash: f674aa5502e4b3b45d0eda119419863892d72cff


---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>Cómo crear perfiles de VPN en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


> [!NOTE]  
>
> - Para obtener información sobre los tipos de conexión disponibles para las diferentes plataformas de dispositivos, consulte [VPN profiles in System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md) (Perfiles de VPN en System Center Configuration Manager).  
> - En el caso de conexiones VPN de terceros, distribuya la aplicación VPN antes de implementar el perfil de VPN. Si no implementa la aplicación, se les pedirá a los usuarios que lo hagan cuando intenten conectarse a la VPN. Para aprender a implementar aplicaciones, consulte [Deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md) (Cómo implementar aplicaciones con System Center Configuration Manager).

### <a name="start-the-create-vpn-profile-wizard"></a>Iniciar el Asistente para crear perfil de VPN  

1.  En la consola de System Center Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** de la consola de System Center Configuration Manager, expanda **Configuración de cumplimiento**, expanda **Acceso a los recursos de la compañía** y, después, haga clic en **Perfiles de VPN**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear perfil de VPN**.  

### <a name="provide-general-information-about-the-vpn-profile"></a>Proporcionar información general sobre el perfil de VPN  

1.  En la página **General** del **Asistente para crear perfil de VPN**, especifique la información siguiente:  

    -   **Nombre** : escriba un nombre único para el perfil de VPN (hasta 256 caracteres).  

        > [!IMPORTANT]  
        >  No use los caracteres \\/:*?<>&#124; ni el carácter espacio en el nombre del perfil de VPN, ya que no son compatibles con el perfil de VPN de Windows Server.  

    -   **Descripción**: escriba una descripción para que le resulte más fácil encontrar el perfil en la consola de System Center Configuration Manager (hasta 256 caracteres).  

    -   **Import an existing VPN profile item from a file** (Importar un perfil de VPN existente de un archivo): seleccione esta opción para visualizar la página **Importar perfil de VPN**. En esta página puede importar información de perfil de VPN de los sistemas operativos que se ha exportado previamente a un archivo XML (solo sistemas operativos Windows 8.1 y Windows RT).  

### <a name="provide-connection-information-for-the-vpn-profile"></a>Proporcionar información de conexión del perfil de VPN  

1.  En la página **Conexión** del asistente, especifique la información siguiente:  

    -   **tipo de conexión:** en la lista desplegable, seleccione el tipo de conexión de la conexión VPN. Puede elegir entre los tipos de conexión de la tabla siguiente, que muestra las plataformas compatibles.  

        > [!IMPORTANT]  
        >  Para poder usar los perfiles de VPN implementados en un dispositivo, debe instalar las aplicaciones VPN de terceros necesarias. Puede usar la información del tema [How to create applications with System Center Configuration Manager](../../apps/deploy-use/create-applications.md) (Cómo crear aplicaciones con System Center Configuration Manager) como ayuda para implementar la aplicación con System Center Configuration Manager.  

    -   **Lista de servidores:** haga clic en **Agregar** para agregar un nuevo servidor que se usará para la conexión VPN. Según el tipo de conexión, puede agregar uno o varios servidores VPN y especificar el servidor predeterminado.  

        > [!NOTE]  
        >  Los dispositivos que ejecutan iOS no admiten el uso de varios servidores VPN. Si configura varios servidores VPN y, a continuación, implementa el perfil de VPN en un dispositivo iOS, solo se utilizará el servidor predeterminado.  

     Es posible que se muestren más opciones en la tabla siguiente en función del tipo de conexión seleccionado. Consulte la documentación del servidor VPN para más información.  

    |Opción|Más información|Tipo de conexión|  
    |------------|----------------------|---------------------|  
    |**Dominio Kerberos**|Especifique el nombre de dominio de autenticación que quiere usar. Un dominio de autenticación es una agrupación de recursos de autenticación usada por el tipo de conexión Pulse Secure.|Pulse Secure|  
    |**Rol**|Especifique el nombre del rol de usuario que tiene acceso a esta conexión.|Pulse Secure|  
    |**Dominio o grupo de inicio de sesión**|Especifique el nombre del grupo o dominio de inicio de sesión al que quiere conectarse.|Dell SonicWALL Mobile Connect|  
    |**Huella digital**|Especifique una cadena, por ejemplo "Código de huella digital de Contoso" que se utilizará para comprobar que se puede confiar en el servidor VPN.<br /><br /> Una huella digital se puede:<br /><br /> - Enviar al cliente para que sepa que puede confiar en cualquier servidor que presente esa misma huella digital al conectarse.<br /><br /> - Si el dispositivo todavía no tiene la huella digital, pedirá al usuario que confíe en el servidor VPN al que se está conectando mientras muestra la huella digital (el usuario comprueba la huella digital manualmente y hace clic en Confiar para conectar).|VPN móvil de punto de comprobación|  
    |**Enviar todo el tráfico de red a través de la conexión VPN**|Si no se selecciona esta opción, puede especificar rutas adicionales para la conexión (para los tipos de conexión **Microsoft SSL [SSTP]**, **Microsoft Automatic**, **IKEv2**, **PPTP** y **L2TP** ), lo que se conoce como túnel dividido o VPN.<br /><br /> Solo las conexiones con la red de la empresa se envían a través de un túnel VPN. El túnel de VPN no se utiliza al conectarse a recursos de Internet.|Todos|  
    |**Sufijo DNS específico de la conexión**|Opcionalmente, especifique el sufijo del sistema de nombres de dominio (DNS) de la conexión.|- <br />                            Microsoft SSL [SSTP]<br /><br /> - Microsoft Automatic<br /><br /> - <br />                            IKEv2<br /><br /> - <br />                            PPTP<br /><br /> - <br />                            L2TP|  
    |**Omitir VPN al conectarse a la red Wi-Fi de empresa**|Especifica que la conexión VPN no se utilizará cuando el dispositivo se conecte a la red Wi-Fi de la empresa.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN móvil de punto de comprobación<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - L2TP|  
    |**Omitir VPN al conectarse a la red Wi-Fi doméstica**|Especifica que la conexión VPN no se utilizará cuando el dispositivo se conecte a la red Wi-Fi doméstica.|Todos|  
    |**VPN por aplicación (iOS 7 y versiones posteriores, Mac OS X 10.9 y versiones posteriores)**|Seleccione esta opción si quiere asociar esta conexión VPN con una aplicación iOS para que la conexión se abra cuando se ejecute la aplicación. Puede asociar el perfil de VPN con una aplicación al implementarla.|- <br />                        Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN móvil de punto de comprobación|  
    |**XML personalizado (opcional)**|Permite especificar los comandos XML personalizados que configuran la conexión VPN.<br /><br /> Ejemplos:<br /><br /> Para **Pulse Secure**:<br /><br /> **<pulse-schema><isSingleSignOnCredential\>true</isSingleSignOnCredential\></pulse-schema>**<br /><br /> Para **CheckPoint Mobile VPN**:<br /><br /> **&lt;CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" /\>**<br /><br /> Para **Dell SonicWALL Mobile Connect**:<br /><br /> **<MobileConnect\><Compression\>false</Compression\><debugLogging\>True</debugLogging\><packetCapture\>False</packetCapture\></MobileConnect\>**<br /><br /> Para **F5 Edge Client**:<br /><br /> **&lt;f5-vpn-conf&gt;&lt;single-sign-on-credential /&gt;&lt;/f5-vpn-conf&gt;**<br /><br /> Consulte la documentación de VPN de cada fabricante para más información sobre cómo escribir comandos XML personalizados.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN móvil de punto de comprobación|  

####   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Características de VPN de Windows 10 disponibles cuando se usa Configuration Manager con Intune  


> [!NOTE]  
> El nombre de un perfil de VPN que usa las características de VPN de Windows 10 no puede estar en formato Unicode ni incluir caracteres especiales.


|Opción|Más información|Tipo de conexión|  
|------------|----------------------|---------------------|  
|**Omitir VPN al conectarse a la red Wi-Fi de empresa**|Especifica que la conexión VPN no se utilizará cuando el dispositivo se conecte a la red Wi-Fi de la empresa. Escriba el nombre de red de confianza, que se utilizará para determinar si el dispositivo está conectado a la red de la empresa.|Todos|  
|**Reglas de tráfico de red**|Defina qué protocolos, puertos locales y remotos e intervalos de direcciones se habilitarán para la conexión VPN.<br /><br /> **Nota:** Si no se crea ninguna regla de tráfico de red, se habilitan todos los protocolos, puertos e intervalos de direcciones. Una vez creada una regla, la conexión VPN solo usará los protocolos, puertos e intervalos de direcciones que especifique en esa regla o en reglas adicionales.|Todos|  
|**Rutas**|Rutas que usará la conexión VPN. Tenga en cuenta que la creación de más de 60 rutas puede producir un error en la directiva. |Todos|  
|**Servidores DNS**|Qué servidores DNS usa la conexión VPN una vez establecida la conexión.|Todos|  
|**Aplicaciones que se conectan automáticamente a la VPN**|Puede agregar aplicaciones o importar una lista de aplicaciones que usarán automáticamente la conexión VPN. El tipo de aplicación determinará el identificador de la aplicación. Para una aplicación de escritorio, proporcione la ruta del archivo de la aplicación. Para una aplicación universal, proporcione el nombre de familia de paquete (PFN). Para obtener información sobre cómo buscar el PFN de una aplicación, consulte [Find a package family name for per-app VPN](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md) (Buscar un nombre de familia de paquete para VPN por aplicación). |Todos|

> [!IMPORTANT]
> Se recomienda que proteja todas las listas de aplicaciones asociadas que se compilan para su uso en la configuración de VPN por aplicación. Si un usuario no autorizado modifica la lista y usted la importa en la lista de aplicaciones de VPN por aplicación, podría autorizar el acceso a VPN a aplicaciones que no deberían tener acceso. Una forma de proteger las listas de aplicaciones consiste en usar una lista de control de acceso (ACL).


### <a name="configure-the-authentication-method-for-the-vpn-profile"></a>Configurar el método de autenticación del perfil de VPN  

1.  En la página **Método de autenticación** del asistente, especifique la información siguiente:  

    -   **Método de autenticación:** en la lista desplegable, seleccione el método de autenticación que la conexión VPN usará. Los elementos de la lista desplegable podrían variar en función del tipo de conexión seleccionado previamente. Los métodos de autenticación disponibles y los tipos de conexión admitidos se indican en la tabla siguiente.  

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

        -   **Recordar las credenciales de usuario en cada inicio de sesión**: Seleccione esta opción para asegurarse de que se recuerdan las credenciales de usuario para que el usuario no tenga que escribirlas cada vez que se establezca una conexión.  

        -   **Seleccionar un certificado de cliente para la autenticación de cliente** : seleccione el certificado SCEP de cliente que creó previamente y que se usará para autenticar la conexión VPN. Para obtener más información sobre cómo usar perfiles de certificado en System Center Configuration Manager, consulte [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Perfiles de certificado en System Center Configuration Manager).  

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
        >Para algunos métodos de autenticación, puede hacer clic en **Configurar** para abrir el cuadro de diálogo de propiedades de Windows (si la versión de Windows en la que ejecuta la consola de System Center Configuration Manager es compatible con este método de autenticación), donde puede configurar las propiedades del método de autenticación.  

### <a name="configure-proxy-settings-for-the-vpn-profile"></a>Establecer la configuración de proxy del perfil de VPN  

1.  En la página **Configuración de proxy** del **Asistente para crear perfil de VPN**, active la casilla **Configurar configuración de proxy para este perfil de VPN** si su conexión VPN usa un servidor proxy.  

2.  Especifique los detalles sobre el servidor proxy y su configuración. Para obtener más información, consulte la documentación de Windows Server.  

> [!NOTE]  
>  En los equipos Windows 8.1, el perfil de VPN no mostrará la información de proxy hasta que se conecte a la VPN con ese equipo.  


### <a name="configure-further-dns-settings-if-required"></a>Configurar opciones de DNS adicionales (si es necesario)  
 En la página **Configurar una conexión VPN automática** del asistente, puede configurar las opciones siguientes:  

-   **Habilitar VPN a petición**: seleccione esta opción si quiere configurar opciones de DNS adicionales en esta página del asistente para dispositivos Windows Phone 8.1.

> [!Note]  
> Esta configuración solo se aplica a dispositivos Windows Phone 8.1 y solo se debe habilitar en los perfiles VPN que se van a implementar en dispositivos Windows Phone 8.1.


-   Lista de sufijos DNS (solo para dispositivos Windows Phone 8.1): configura los dominios que establecerán una conexión VPN. Para cada dominio que especifique, debe agregar el sufijo DNS, la dirección del servidor DNS y una de las siguientes acciones a petición:  

    -   **No establecer nunca**: no se abre nunca una conexión VPN.  

    -   **Establecer si es necesario**: solo se abre una conexión VPN si el dispositivo necesita conectarse a recursos.  

    -   **Establecer siempre**: siempre se abre la conexión VPN.  

-   **Combinar**: copia todos los sufijos DNS que configuró en la **Lista de redes de confianza**.  

-   **Lista de redes de confianza** (solo para dispositivos Windows Phone 8.1): especifique un sufijo DNS en cada línea. Si el dispositivo se encuentra en una red de confianza, no se abrirá la conexión VPN.  

-   **Lista de búsqueda de sufijos** (solo para dispositivos Windows Phone 8.1): especifique un sufijo DNS en cada línea. Al conectarse a un sitio web mediante un nombre corto, se buscará cada sufijo DNS que especifique.  

     Por ejemplo, especifica los sufijos DNS **domain1.contoso.com** y **domain2.contoso.com** y, después, visita la dirección URL **http://mywebsite**. Se buscarán las siguientes direcciones:  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

> [!NOTE]  
>  Solo para dispositivos Windows Phone 8.1  
>   
>  Si se selecciona la opción **Enviar todo el tráfico de red a través de la conexión VPN** y la conexión VPN usa el túnel completo, la conexión VPN se abrirá automáticamente para el primer perfil aprovisionado en el dispositivo. Si desea que otro perfil abra automáticamente una conexión, debe convertirlo en el perfil predeterminado del dispositivo.  
>   
>  Si no se selecciona la opción **Enviar todo el tráfico de red a través de la conexión VPN** y la conexión VPN usa el túnel dividido, puede abrirse automáticamente una conexión VPN si se configuran las rutas o un sufijo DNS específico de la conexión.  


### <a name="configure-supported-platforms-for-the-vpn-profile"></a>Configurar plataformas admitidas del perfil de VPN  
 Las plataformas admitidas son los sistemas operativos en los que se instalará el perfil de VPN.  

En la página **Plataformas admitidas** del **Asistente para crear perfil de VPN**, seleccione los sistemas operativos en los que se instalará el perfil de VPN o haga clic en **Seleccionar todo** para instalar el perfil de VPN en todos los sistemas operativos disponibles.  

### <a name="complete-the-wizard"></a>Completar el asistente  
 En la página **Resumen** del asistente, revise las acciones que se realizarán y, después, elija **Finalizar**. El nuevo perfil de VPN se muestra en el nodo **Perfiles de VPN** en el área de trabajo **Activos y compatibilidad** .  

### <a name="next-steps"></a>Pasos siguientes

- En el caso de conexiones VPN de terceros, distribuya la aplicación VPN antes de implementar el perfil de VPN. Si no implementa la aplicación, se les pedirá a los usuarios que lo hagan cuando intenten conectarse a la VPN. Para aprender a implementar aplicaciones, consulte [Deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md) (Cómo implementar aplicaciones con System Center Configuration Manager).

- Implemente el perfil de VPN tal como se describe en [How to deploy profiles in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md) (Cómo implementar perfiles en System Center Configuration Manager).  



<!--HONumber=Dec16_HO3-->


