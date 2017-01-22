---
title: Implementar clientes Mac | Microsoft Docs
description: "Obtenga información sobre cómo implementar clientes en equipos Mac en System Center Configuration Manager."
ms.custom: na
ms.date: 11/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: 12
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 66071227fd10a43f7cd4e64508494d485392ffcd
ms.openlocfilehash: 6cbddd623767522a0026e0736b1f647fddbecfb6


---
# <a name="how-to-deploy-clients-to-macs-in-system-center-configuration-manager"></a>How to deploy clients to Macs in System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este tema se describe cómo instalar el cliente de Configuration Manager en equipos Mac.

## <a name="prerequisites-and-preparatory-steps"></a>Requisitos previos y pasos de preparación

### <a name="mac-prerequisites"></a>Requisitos previos de Mac

Antes de instalar el cliente, debe asegurarse de que los equipos Mac cumplan los requisitos previos, tal como se describe en [Sistemas operativos compatibles con equipos Mac](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

### <a name="certificate-requirements"></a>Requisitos de certificados
Para la instalación y la administración de clientes para equipos Mac se necesitan certificados de infraestructura de clave pública (PKI). Los certificados PKI protegen la comunicación entre los equipos Mac y el sitio de Configuration Manager mediante transferencias de datos cifrados y autenticación mutua. Configuration Manager puede solicitar e instalar un certificado de cliente mediante los Servicios de certificados de Microsoft con una entidad de certificación empresarial (CA) y los roles del sistema de sitio del punto de proxy de inscripción y del punto de inscripción de Configuration Manager. También puede solicitar e instalar un certificado de equipo sin la intervención de Configuration Manager, si el certificado cumple los requisitos para Configuration Manager.   
  
Los clientes Mac de Configuration Manager siempre realizan una comprobación de revocación de certificado. Al contrario que con los clientes de Configuration Manager que se ejecutan en Windows, no se puede deshabilitar la función de comprobación de la lista de revocación de certificados (CRL).  
  
Si los clientes Mac no pueden confirmar el estado de revocación de certificado para un certificado de servidor porque no encuentran la CRL, no podrán conectarse correctamente a sistemas de sitio de Configuration Manager, como los puntos de administración y los puntos de distribución. Compruebe, especialmente para clientes Mac que no están en el mismo bosque que la entidad de certificación emisora, el diseño de la CRL para asegurarse de que los clientes Mac pueden encontrar un punto de distribución CRL (CDP), y conectarse a él, para poder conectarse a servidores de sistema de sitio.  

Antes de instalar el cliente de Configuration Manager en un equipo Mac, decida cómo va a instalar el certificado de cliente:  

-   Usar la inscripción de Configuration Manager mediante la herramienta CMEnroll. Para esta opción, siga los pasos indicados en la siguiente sección de este tema. El proceso de inscripción no admite la renovación automática de certificados por lo que debe volver a inscribir los equipos Mac antes de que expire el certificado instalado.  

-   Usar una solicitud de certificado y un método de instalación independiente de Configuration Manager. Para saber más sobre este método de instalación, consulte la sección [Use a certificate request and installation method that is independent from Configuration Manager](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager) en este tema.  

Para obtener más información sobre los requisitos de certificado de cliente Mac y otros certificados PKI necesarios para admitir equipos Mac, consulte [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md) (Requisitos de certificados PKI para System Center Configuration Manager).  

Los clientes Mac se asignan automáticamente al sitio de Configuration Manager que los administra. Los clientes Mac se instalan como clientes de solo Internet, incluso si la comunicación está restringida a la intranet. La configuración de cliente implica que se comunicarán con los roles de sistema de sitio (puntos de administración y puntos de distribución) del sitio al que están asignados cuando se configuren estos roles para permitir conexiones de cliente desde Internet. Los equipos Mac no se comunican con roles de sistema de sitio fuera del sitio al que están asignados.  

> [!IMPORTANT]  
>  El cliente Mac de Configuration Manager no se puede usar para conectarse con un punto de administración que está configurado para usar una [réplica de base de datos](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  


### <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Implementar un certificado de servidor web en servidores de sistema de sitio  
Si estos sistemas de sitio no tienen un certificado de servidor web, debe implementarlo en los equipos que tengan estos roles de sistema de sitio:  

-   Punto de administración  

-   Punto de distribución  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

El certificado de servidor web debe contener el FQDN de Internet que se especifica en las propiedades del sistema de sitio. No es necesario que el servidor sea accesible desde Internet para admitir equipos Mac. Si no requiere administración de cliente basada en Internet, puede especificar el FQDN de la intranet para el FQDN de Internet.  

Especifique el FQDN de Internet del sistema de sitio en el certificado de servidor web para el punto de administración, el punto de distribución y el punto de proxy de inscripción. 

Para ver una implementación de ejemplo en la que se crea y se instala este certificado de servidor web, consulte [Deploying the Web Server Certificate for Site Systems that Run IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012) (Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS).  

 

### <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Implementar un certificado de autenticación de cliente en servidores de sistema de sitio  
 Si estos sistemas de sitio no tienen un certificado de autenticación de cliente, impleméntelo en los equipos que tengan los siguientes roles de sistema de sitio:  

-   Punto de administración  

-   Punto de distribución  

 Para ver una implementación de ejemplo en la que se crea y se instala el certificado de cliente para puntos de administración, consulte [Deploying the Client Certificate for Windows Computers](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012) (Implementación del certificado de cliente para equipos Windows).  

 Para ver una implementación de ejemplo en la que se crea y se instala el certificado de cliente para puntos de distribución, consulte [Deploying the Client Certificate for Distribution Points](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012) (Implementación del certificado de cliente para puntos de distribución).  

### <a name="prepare-the-client-certificate-template-for-macs"></a>Preparar la plantilla de certificado de cliente para equipos Mac  

> [!NOTE]  
>  Para ejecutar la herramienta de inscripción de Configuration Manager, debe tener una cuenta de usuario de Active Directory.  

 La plantilla de certificado debe tener permisos de **lectura** e **inscripción** para la cuenta de usuario que inscriba el certificado en el equipo Mac.  

 Consulte [Deploying the Client Certificate for Mac Computers](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1) (Implementación del certificado de cliente para equipos Mac).  

### <a name="configure-the-management-point-and-distribution-point"></a>Configurar el punto de administración y el punto de distribución  
 Configure los puntos de administración para las siguientes opciones:  

-   HTTPS  

-   Allow client connections from the Internet (Permitir conexiones de cliente desde Internet). Este valor de configuración es necesario para administrar equipos Mac. Sin embargo, eso no significa que los servidores del sistema de sitios deben ser accesibles desde Internet.  

-   Permitir a los dispositivos móviles y equipos Mac usar este punto de administración  

 Aunque no se requieren puntos de distribución para instalar el cliente, debe configurar puntos de distribución para permitir conexiones de cliente desde Internet si quiere implementar software en estos equipos una vez instalado el cliente.  

 
##### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Para configurar puntos de administración y puntos distribución para admitir equipos Mac  

Antes de iniciar este procedimiento, asegúrese de que el servidor de sistema de sitio que ejecuta el punto de administración y el punto de distribución está configurado con un FQDN de Internet. Si estos servidores no admiten la administración de cliente basada en Internet, puede especificar el FQDN de intranet como FQDN de Internet. 

Los roles de sistema de sitio deben estar en un sitio primario.  


1.  En la consola de Configuration Manager, seleccione **Administración** > **Configuración del sitio** > **Servidores y roles del sistema de sitios** y, después, seleccione el servidor que tenga los roles de sistema de sitio correctos.  

3.  En el panel de detalles, haga clic con el botón derecho en **Punto de administración**, seleccione **Propiedades de rol** y, en el cuadro de diálogo **Propiedades de punto de administración**, configure estas opciones:  

    1.  Elija **HTTPS**.  

    2.  Seleccione **Permitir solo conexiones de Internet a los clientes** o **Allow intranet and Internet client connections** (Permitir conexiones de intranet e Internet a los clientes). Estas opciones requieren un FQDN de Internet o de intranet.  

    3.  Seleccione **Permitir a los dispositivos móviles y equipos Mac usar este punto de administración**.  

4.  En el panel de detalles, haga clic con el botón derecho en **Punto de distribución**, seleccione **Propiedades de rol** y, en el cuadro de diálogo **Propiedades de punto de distribución**, configure estas opciones:  

    -   Elija **HTTPS**.  

    -   Seleccione **Permitir solo conexiones de Internet a los clientes** o **Allow intranet and Internet client connections** (Permitir conexiones de intranet e Internet a los clientes). Estas opciones requieren un FQDN de Internet o de intranet.  

    -   Seleccione **Importar certificado**, busque el archivo del certificado del punto de distribución de cliente exportado y, después, especifique la contraseña.  

5.  Repita los pasos del 2 al 4 para todos los puntos de administración y puntos de distribución de los sitios primarios que va a usar con equipos Mac.  

### <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configurar el punto de proxy de inscripción y el punto de inscripción  
 Debe instalar estos dos roles de sistema de sitio en el mismo sitio, pero no es necesario instalarlos en el mismo servidor de sistema de sitio, ni en el mismo bosque de Active Directory.  

 Para obtener más información sobre los distintos roles de sistema de sitio, consulte [Site system roles](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) (Roles de sistema de sitio) en [Plan for site system servers and site system roles for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md) (Planeamiento de servidores y roles de sistema de sitio para System Center Configuration Manager).  

 Estos procedimientos configuran los roles de sistema de sitio para admitir equipos Mac. Elija el procedimiento adecuado en función de si va a instalar un servidor de sistema de sitio nuevo para inscripción de equipos Mac, o va a utilizar un servidor de sistema de sitio existente:  

-   [Nuevo servidor de sistema de sitio](#new-site-system-server)  

-   [Servidor de sistema de sitio existente](#existing-site-system-server)  

####  <a name="new-site-system-server"></a>nuevo servidor de sistema de sitio  

1.  En la consola de Configuration Manager, elija **Administración** >  **Configuración de sitio** > **Servidores y roles del sistema de sitios**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, elija **Crear servidor del sistema de sitio**.  

4.  En la página **General**, especifique la configuración general para el sistema de sitio.  Asegúrese de especificar un valor para el FQDN de Internet. Si el servidor no va a ser accesible desde Internet, use el FQDN de intranet.  

5.  En la página **Selección de rol del sistema**, seleccione **Punto de proxy de inscripción** y **Punto de inscripción** en la lista de roles disponibles.  

6.  En la página **Punto de proxy de inscripción**, revise la configuración y haga los cambios necesarios.  

7.  En la página de configuración de **Punto de inscripción**, revise la configuración y haga los cambios necesarios. Después, finalice el asistente.  

#### <a name="existing-site-system-server"></a>servidor de sistema de sitio existente  

1.  En la consola de Configuration Manager, seleccione **Administración** >  **Configuración del sitio** > **Servidores y roles del sistema de sitios** y, después, seleccione el servidor que quiere usar para admitir equipos Mac.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, elija **Agregar roles del sistema de sitio**.  

4.  En la página **General** , especifique la configuración general del sistema de sitio y, a continuación, haga clic en **Siguiente**. Asegúrese de especificar un valor para el FQDN de Internet. Si el servidor no va a ser accesible desde Internet, use el FQDN de intranet.   

5.  En la página **Selección de rol del sistema**, seleccione **Punto de proxy de inscripción** y **Punto de inscripción** en la lista de roles disponibles.  

6.  En la página **Punto de proxy de inscripción**, revise la configuración y haga los cambios necesarios.  

7.  En la página de configuración de **Punto de inscripción**, revise la configuración y haga los cambios necesarios. Después, finalice el asistente.  

### <a name="optional-install-the-reporting-services-point"></a>Opcional: instalar el punto de servicios de informes  
 Instale el punto de servicios de informes si quiere ejecutar informes para equipos Mac.  

 Para obtener más información sobre cómo instalar y configurar el punto de servicios de informes, consulte [Configuring reporting in System Center Configuration Manager](../../../core/servers/manage/configuring-reporting.md) (Configuración de informes en System Center Configuration Manager).  


##  <a name="install-and-configure-the-client-for-macs"></a>Instalar y configurar el cliente para equipos Mac  


### <a name="configure-client-settings-for-enrollment"></a>Configurar las opciones del cliente para la inscripción  
 Debe utilizar la configuración predeterminada para configurar la inscripción para equipos Mac; no puede utilizar una configuración de cliente personalizada.  

 Para obtener más información sobre la configuración de cliente, consulte [About client settings in System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md) (Acerca de la configuración de cliente en System Center Configuration Manager).  

 Esto es necesario para que Configuration Manager solicite e instale el certificado en el equipo Mac.  

#### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>Para configurar las opciones de cliente predeterminadas para que Configuration Manager inscriba los certificados para los equipos Mac  

1.  En la consola de Configuration Manager, elija **Administración** >  **Configuración de cliente** > **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

5.  Seleccione la sección **Inscripción** y, después, configure estas opciones:  

    1.  **Permitir a los usuarios inscribir dispositivos móviles y equipos Mac: Sí**  

    2.  **Perfil de inscripción:** seleccione **Establecer perfil**.  

6.  En el cuadro de diálogo **Perfil de inscripción de dispositivo móvil**, seleccione **Crear**.  

7.  En el cuadro de diálogo **Crear perfil de inscripción** , escriba un nombre para este perfil de inscripción y, a continuación, configure el **Código del sitio de administración**. Seleccione el sitio primario de Configuration Manager que contiene los puntos de administración que administrarán los equipos Mac.  

    > [!NOTE]  
    >  Si no puede seleccionar el sitio, compruebe que como mínimo un punto de administración en el sitio está configurado para admitir dispositivos móviles.  

8.  Seleccione **Agregar**.  

9. En el cuadro de diálogo **Agregar entidad de certificación para dispositivos móviles**, seleccione el servidor de la entidad de certificación (CA) que emitirá certificados a equipos Mac.  

10. En el cuadro de diálogo **Crear perfil de inscripción**, seleccione la plantilla de certificado del equipo Mac que ha creado en el paso 3.  

11. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Perfil de inscripción** y el cuadro de diálogo **Configuración de cliente predeterminada**.  

    > [!TIP]  
    >  Si desea cambiar el intervalo de directivas de cliente, utilice la configuración de cliente en **Intervalo de sondeo de directiva de cliente** en el grupo de configuración de cliente **Directiva de cliente** .  

 Todos los usuarios se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, consulte [Initiate Policy Retrieval for a Configuration Manager Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) (Iniciar la recuperación de directivas para un cliente de Configuration Manager).  

 Además de la configuración de cliente de inscripción, asegúrese de que configuró la siguiente configuración de dispositivo de cliente de Configuration Manager:  

-   **Inventario de hardware**: habilite y configure esta opción si quiere recopilar el inventario de hardware de los equipos cliente Mac y Windows. Para obtener más información, consulte [How to extend hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md) (Cómo ampliar el inventario de hardware en System Center Configuration Manager).  

-   **Configuración de cumplimiento**: habilite y configure esta opción si quiere evaluar y corregir la configuración de los equipos cliente Mac y Windows. Para obtener más información, consulte [Plan for and configure compliance settings](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) (Planear y configurar la configuración de cumplimiento).  

> [!NOTE]  
>  Para obtener más información sobre la configuración de cliente de Configuration Manager, consulte [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md) (Cómo configurar el cliente en System Center Configuration Manager).  

### <a name="download-the-client-source-files-for-macs"></a>Descargar los archivos de origen de cliente para equipos Mac  
 Debe descargar e instalar los siguientes programas para poder instalar y administrar el cliente de Configuration Manager en equipos Mac:  

-   **Ccmsetup**: use esta aplicación para instalar el cliente de Configuration Manager en los equipos Mac.  

-   **CMDiagnostics**: use esta herramienta para recopilar información de diagnóstico relacionada con el cliente de Configuration Manager en los equipos Mac.  

-   **CMUninstall**: use esta herramienta para desinstalar el cliente de Configuration Manager de los equipos Mac.  

-   **CMAppUtil**: use esta herramienta para convertir paquetes de aplicaciones de Apple en un formato que se pueda implementar como una aplicación de Configuration Manager.  

-   **CMEnroll**: use esta herramienta para solicitar e instalar el certificado de cliente para un equipo Mac, de modo que pueda instalar después el cliente de Configuration Manager.  

> [!IMPORTANT]  
>  Cuando instale un nuevo cliente para equipos Mac, es posible que tenga que instalar también actualizaciones de Configuration Manager para reflejar la nueva información de cliente en la consola de Configuration Manager.  

##### <a name="to-download-and-install-the-mac-os-x-client-files"></a>Para descargar e instalar los archivos de cliente de Mac OS X  

1.  Descargue el paquete de archivos de cliente de Mac OS X **ConfigmgrMacClient.msi**y guárdelo en un equipo donde se ejecute Windows.  

     Este archivo no se incluye en los medios de instalación de Configuration Manager. Puede descargar este archivo desde el [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

2.  En el equipo Windows, ejecute el archivo **ConfigmgrMacClient.msi** que acaba de descargar para extraer el paquete de cliente Mac, Macclient.dmg, en una carpeta del disco local (de manera predeterminada **C:\Archivos de programa (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**).  

3.  Copie el archivo Macclient.dmg en una carpeta del equipo Mac.  

4.  En el equipo Mac, ejecute el archivo Macclient.dmg para extraer los archivos en una carpeta del disco local.  

5.  En la carpeta, asegúrese de que se extraen los archivos Ccmsetup y CMClient.pkg, y que se creó una carpeta denominada Tools que contiene las herramientas CMDiagnostics, CMUninstall, CMAppUtil y CMEnroll.  

### <a name="install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>Instalar el cliente e inscribir el certificado de cliente en el equipo Mac  
 Este procedimiento instala el cliente y, luego, usa la herramienta CMEnroll para solicitar e instalar el certificado de cliente para un equipo Mac, de tal forma que pueda administrar después este equipo mediante Configuration Manager.  

 Puede inscribir el cliente mediante el Asistente para inscripción de equipos Mac sin necesidad de usar la herramienta CMEnroll, como se describe en [Inscribir el cliente mediante el Asistente para inscripción de equipos Mac](#enroll-the-client-by-using-the-mac-computer-enrollment-wizard).  

#### <a name="to-install-the-client-and-enroll-the-certificate-by-using-the-cmenroll-tool"></a>Para instalar el cliente e inscribir el certificado mediante la herramienta CMEnroll  

1.  En el equipo Mac, vaya a la carpeta en la que ha extraído el contenido del archivo Macclient.dmg file.  

2.  Escriba la siguiente línea de comandos: **sudo ./ccmsetup**  

3.  Espere hasta que vea el mensaje de **instalación completada** . Aunque el instalador muestra un mensaje que indica que debe reiniciar ahora, no lo haga y continúe con el paso siguiente.  

4.  En la carpeta de herramientas en el equipo Mac, escriba lo siguiente: **sudo ./CMEnroll -s &lt;nombre_de_servidor_proxy_de_inscripción> -ignorecertchainvalidation -u &lt;nombre de usuario'>**  

    Una vez instalado del cliente, se abrirá el asistente para inscripción de equipos Mac que lo ayudará a inscribir el equipo Mac. Para inscribir el cliente mediante este método, consulte [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) en este tema.  

5. Escriba la contraseña de la cuenta de usuario de Active Directory.  Cuando escriba este comando, se le pedirán dos contraseñas: la primera solicitud es para que la cuenta de superusuario ejecute el comando. La segunda es para la cuenta de usuario de Active Directory. Los mensajes de solicitud son idénticos, así que asegúrese de especificar las credenciales en la secuencia correcta.  

    El nombre de usuario puede adoptar los siguientes formatos:  

    -   'dominio\nombre'. Por ejemplo: 'contoso\mnorth'  

    -   'user@domain'. Por ejemplo: 'mnorth@contoso.com'  

     El nombre de usuario y la contraseña correspondiente deben coincidir con una cuenta de usuario de Active Directory a la que se haya concedido permisos de lectura e inscripción en la plantilla de certificado de cliente de Mac.  

     Ejemplo: si el servidor de punto de proxy de inscripción se denomina **server02.contoso.com** y se concedieron permisos para la plantilla de certificado de cliente Mac a un nombre de usuario de **contoso\mnorth**, escriba lo siguiente: **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!NOTE]  
    >  La inscripción no se llevará a cabo si el nombre de usuario contiene cualquiera de los siguientes caracteres: **&lt;>"+=,**. Para solucionar este problema, obtenga un certificado de fuera de banda con un nombre de usuario que no contenga estos caracteres.  
    >  
    >  Para lograr una perfecta experiencia de usuario, puede crear scripts con los comandos y pasos de la instalación para que los usuarios solo tengan que proporcionar su nombre de usuario y contraseña.  

5.  Espere hasta que vea el mensaje de **inscripción correcta** .  

6.  Para limitar el certificado inscrito a Configuration Manager, en el equipo Mac, abra una ventana de terminal y realice los cambios siguientes:  

    a.  Escriba el comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  En el cuadro de diálogo **Keychain Access** (Acceso a cadenas de claves), en la sección **Keychains** (Cadenas de claves), seleccione **Sistema** y, después, en la sección **Categoría**, seleccione **Claves**.  

    c.  Expanda los llaveros para ver los certificados de cliente. Una vez identificado el certificado con la clave privada que acaba de instalar, haga doble clic en dicha clave.  

    d.  En la pestaña **Control de acceso**, seleccione **Confirm before allowing access** (Confirmar antes de permitir el acceso).  

    e.  Vaya a **/Library/Application Support/Microsoft/MCC**, elija **CCMClient** y, después, seleccione **Agregar**.  

    f.  Seleccione **Guardar cambios** y cierre el cuadro de diálogo **Keychain Access** (Acceso a cadenas de claves).  

7.  Reinicie el equipo Mac.  

 Compruebe que la instalación de cliente se realizó correctamente. Para ello, abra el elemento **Configuration Manager** en **Preferencias del sistema** en el equipo Mac. También puede actualizar y ver la recopilación **Todos los sistemas** para confirmar que el equipo Mac ahora aparece en esta recopilación como un cliente administrado.  

> [!TIP]  
>  Para resolver cualquier problema con el cliente Mac, puede usar el programa CMDiagnostics que se incluye con el paquete de cliente Mac OS X para recopilar la siguiente información de diagnóstico:  
>   
>  -   Una lista de procesos en ejecución  
> -   La versión del sistema operativo Mac OS X  
> -   Informes de bloqueo de Mac OS X relacionados con el cliente de Configuration Manager, incluidos **CCM\*.crash** y **System Preference.crash**.  
> -   El archivo de lista de materiales (L. Mat) y el archivo de lista de propiedades (.plist) creados por la instalación de cliente de Configuration Manager.  
> -   El contenido de la carpeta /Library/Application Support/Microsoft/CCM/Logs.  
>   
>  La información recopilada por CmDiagnostics se agrega a un archivo ZIP que se guarda en el escritorio del equipo con el nombre cmdiag-*<nombre de host\>***-***<fecha y hora\>*.zip.  

####  <a name="enroll-the-client-by-using-the-mac-computer-enrollment-wizard"></a>Inscribir el cliente mediante el Asistente para inscripción de equipos Mac  

1.  Cuando la instalación del cliente finaliza, se abre el Asistente para inscripción de equipos. Si el asistente no se inicia, o si cierra el asistente involuntariamente, haga clic en **Inscribir** en la página de preferencias de **Configuration Manager** para abrirlo.  

2.  En la segunda página del asistente, especifique la siguiente información:  

    -   **Nombre de usuario** : el nombre de usuario puede adoptar los siguientes formatos:  

        -   'dominio\nombre'. Por ejemplo: 'contoso\mnorth'  

        -   'user@domain'. Por ejemplo: 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  Si usa una dirección de correo electrónico para rellenar el campo **Nombre de usuario**, Configuration Manager automáticamente usa el nombre de dominio de la dirección de correo electrónico y el nombre predeterminado del servidor de punto de proxy de inscripción para rellenar el campo **Nombre de servidor**. Si el nombre de dominio y el nombre de servidor no coinciden con el nombre del servidor de punto de proxy de inscripción, deberá notificar a los usuarios el nombre correcto que deben usar, para que puedan escribirlo al realizar la inscripción de equipos Mac.  

         El nombre de usuario y la contraseña correspondiente deben coincidir con una cuenta de usuario de Active Directory a la que se haya concedido permisos de lectura e inscripción en la plantilla de certificado de cliente de Mac.  

    -   **Contraseña**: escriba la contraseña correspondiente del nombre de usuario especificado.  

    -   **Nombre de servidor**: escriba el nombre del servidor de punto de proxy de inscripción.  

3.  Haga clic en **Siguiente** para continuar y, a continuación, complete el asistente.  

## <a name="maintenance-tasks-for-mac-clients"></a>Tareas de mantenimiento para clientes Mac

###  <a name="uninstalling-the-mac-client"></a>Desinstalar el cliente Mac  

1.  En un equipo Mac, abra una ventana de terminal y desplácese hasta la carpeta en la que ha extraído el contenido del archivo macclient.dmg que ha descargado.  

2.  Navegue hasta la carpeta Tools, y escriba la siguiente línea de comandos:  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  La propiedad **-c** indica a la desinstalación de cliente que también quite los registros de bloqueo y los archivos de registro del cliente. Aunque es opcional, es una práctica recomendada para evitar confusiones si más adelante vuelve a instalar al cliente.  

3.  Si es necesario, revoque o elimine manualmente el certificado de autenticación de cliente usado por Configuration Manager. CMUnistall no quita ni revoca este certificado.  

###  <a name="renewing-the-mac-client-certificate"></a>Renovación del certificado de cliente Mac  
 Utilice uno de los métodos siguientes para renovar el certificado de cliente Mac:  

-   [Asistente para renovar certificado](#renew-certificate-wizard)  

-   [Renovar el certificado manualmente](#renew-certificate-manually)  

####  <a name="renew-certificate-wizard"></a>Asistente para renovar certificado  

1.  Configure los valores siguientes como *cadenas* en el archivo ccmclient.plist que controla la apertura del Asistente para renovar certificado:  

    -   **RenewalPeriod1**: especifica, en segundos, el primer período de renovación en el que los usuarios pueden renovar el certificado. El valor predeterminado es 3.888.000 segundos (45 días). No configure un valor inferior a 300, ya que el período volverá al valor predeterminado. 


    -   **RenewalPeriod2**: especifica, en segundos, el segundo período de renovación en el que los usuarios pueden renovar el certificado. El valor predeterminado es 259.200 segundos (3 días). Si este valor se configura y es mayor o igual que 300 segundos y menor o igual que **RenewalPeriod1**, se usará el valor. Si **RenewalPeriod1** es mayor que 3 días, se usará un valor de 3 días para **RenewalPeriod2**.  Si **RenewalPeriod1** es menor que 3 días, **RenewalPeriod2** se establecerá en el mismo valor que **RenewalPeriod1**.  

    -   **RenewalReminderInterval1**: especifica, en segundos, la frecuencia con la que se mostrará el Asistente para renovación de certificados a los usuarios durante el primer período de renovación. El valor predeterminado es 86.400 segundos (1 día). Si **RenewalReminderInterval1** es mayor que 300 segundos y menor que el valor configurado para **RenewalPeriod1**, se usará el valor configurado. De lo contrario, se utilizará el valor predeterminado de 1 día.  

    -   **RenewalReminderInterval2**: especifica, en segundos, la frecuencia con la que se mostrará el Asistente para renovación de certificados a los usuarios durante el segundo período de renovación. El valor predeterminado es 28.800 segundos (8 horas). Si **RenewalReminderInterval2** es mayor que 300 segundos y menor o igual que **RenewalReminderInterval1** , y menor o igual que **RenewalPeriod2**, se usará el valor configurado. De lo contrario, se usará un valor de 8 horas.  

     **Ejemplo** : si se mantienen los valores predeterminados, 45 días antes de que expire el certificado, el asistente se abrirá cada 24 horas.  A los 3 días de que expire el certificado, el asistente se abrirá cada 8 horas.  

     **Ejemplo** : use la siguiente línea de comandos, o un script, para establecer el valor del primer período de renovación en 20 días.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  Habitualmente, cuando el Asistente para renovar certificado se inicia, los campos **Nombre de usuario** y **Nombre de servidor** se rellenan automáticamente y el usuario solo deberá escribir la contraseña para renovar el certificado.  

    > [!NOTE]  
    >  Si el asistente no se inicia, o si cierra el asistente involuntariamente, haga clic en **Renovar** en la página de preferencias de **Configuration Manager** para iniciarlo.  

####  <a name="renewing-the-mac-client-certificate-manually"></a>Renovación manual del certificado de cliente Mac  
 El período de validez normal de un certificado de cliente de Mac es 1 año Configuration Manager no renueva automáticamente el certificado de usuario que solicita durante la inscripción, por lo que deberá realizar el siguiente procedimiento para renovarlo manualmente.  

> [!IMPORTANT]  
>  Si el certificado expira, debe desinstalarlo, reinstalarlo y, a continuación, volver a inscribir el cliente Mac.  

 Este procedimiento quita el SMSID, lo cual es necesario para solicitar un nuevo certificado para el mismo equipo Mac. Cuando quita y reemplaza el SMSID del cliente, todo el historial del cliente almacenado, como el inventario, se elimina después de eliminar el cliente de la consola de Configuration Manager.  

1.  Cree y rellene una recopilación de dispositivos para los equipos Mac que deben renovar los certificados de usuario.  

    > [!WARNING]  
    >  Configuration Manager no supervisa el periodo de validez del certificado que inscribe para los equipos Mac. Debe supervisarlo independientemente de Configuration Manager para identificar los equipos Mac que se van a agregar a esta recopilación.  

2.  En el área de trabajo **Activos y compatibilidad** , inicie el **Asistente para crear elemento de configuración**.  

3.  En la página **General** del asistente, especifique la siguiente información:  

    -   **NombreQuitar SMSID para Mac**:  

    -   **TipoMac OS X**:  

4.  En la página **Plataformas admitidas** del asistente, asegúrese de que se seleccionan todas las versiones de Mac OS X.  

5.  En la página **Configuración** del asistente, seleccione **Nueva** y, después, en el cuadro de diálogo **Crear configuración**, especifique la información siguiente:  

    -   **NombreQuitar SMSID para Mac**:  

    -   **Tipo de configuraciónscript**:  

    -   **Tipo de datoscadena**:  

6.  En el cuadro de diálogo **Crear configuración**, en **Script de detección**, seleccione **Agregar script** para especificar un script que detecta equipos Mac con el SMSID configurado.  

7.  En el cuadro de diálogo **Editar script de detección** , escriba el siguiente script de shell:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Seleccione **Aceptar** para cerrar el cuadro de diálogo **Editar script de detección**.  

9. En el cuadro de diálogo **Crear configuración**, en **Script de corrección (opcional)**, seleccione **Agregar script** para especificar un script que quita el SMSID cuando se encuentra en equipos Mac.  

10. En el cuadro de diálogo **Crear script de corrección** , escriba el siguiente script de shell:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Crear script de corrección**.  

12. En la página **Reglas de compatibilidad** del asistente, haga clic en **Nueva**y, a continuación, en el cuadro de diálogo **Crear regla** , especifique la información siguiente:  

    -   **NombreQuitar SMSID para Mac**:  

    -   **Configuración seleccionada**: seleccione **Examinar** y, luego, seleccione el script de detección especificado previamente.  

    -   En el campo **los siguientes valores** escriba **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Habilite la opción **Ejecutar el script de corrección especificado cuando esta configuración no sea compatible**.  

13. Complete el Asistente para crear elemento de configuración.  

14. Cree una línea base de configuración que contenga el elemento de configuración que acaba de crear e impleméntela en la recopilación de dispositivos que ha creado en el paso 1.  

     Para obtener más información sobre cómo crear e implementar líneas de base de configuración, consulte [How to create configuration baselines in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) (Cómo crear líneas base de configuración en System Center Configuration Manager) y [How to deploy configuration baselines in System Center Configuration Manager](../../../compliance/deploy-use/deploy-configuration-baselines.md) (Cómo implementar líneas base de configuración en System Center Configuration Manager).  

15. En equipos Mac que tienen el SMSID quitado, ejecute el comando siguiente para instalar un certificado nuevo:  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Cuando se le solicite, proporcione la contraseña de la cuenta de superusuario para ejecutar el comando y, a continuación, la contraseña de la cuenta de usuario de Active Directory.  

16. Para limitar el certificado inscrito a Configuration Manager, en el equipo Mac, abra una ventana de terminal y realice los cambios siguientes:  

    a.  Escriba el comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  En el cuadro de diálogo **Keychain Access** (Acceso a cadenas de claves), en la sección **Keychains** (Cadenas de claves), seleccione **Sistema** y, después, en la sección **Categoría**, seleccione **Claves**.  

    c.  Expanda los llaveros para ver los certificados de cliente. Una vez identificado el certificado con la clave privada que acaba de instalar, haga doble clic en dicha clave.  

    d.  En la pestaña **Control de acceso**, seleccione **Confirm before allowing access** (Confirmar antes de permitir el acceso).  

    e.  Vaya a **/Library/Application Support/Microsoft/MCC**, elija **CCMClient** y, después, seleccione **Agregar**.  

    f.  Seleccione **Guardar cambios** y cierre el cuadro de diálogo **Keychain Access** (Acceso a cadenas de claves).  

17. Reinicie el equipo Mac.  

##  <a name="use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a>Utilizar una solicitud de certificado y un método de instalación independiente de Configuration Manager  
 Cuando no use la inscripción de Configuration Manager, sino que solicite e instale el certificado de cliente independientemente de Configuration Manager, los pasos de configuración son ligeramente distintos.

Empiece realizando *solo* estos pasos:

a. [Implementar un certificado de servidor web en servidores del sistema de sitio](#deploy-a-web-server-certificate-to-site-system-servers)

b. [Implementar un certificado de autenticación de cliente en servidores del sistema de sitio](#deploy-a-client-authentication-certificate-to-site-system-servers)

c. [Configurar el punto de administración y el punto de distribución](#configure-the-management-point-and-distribution-point)

d. [Opcional: instalar el punto de servicios de informes](#optional:-install-the-reporting-services-point)

e. [Descargar los archivos de origen de cliente para equipos Mac](#download-the-client-source-files-forMacs)  
  

#### <a name="to-install-the-client-certificate-independently-from-configuration-manager-and-install-the-client"></a>Para instalar el certificado de cliente independientemente de Configuration Manager e instalar el cliente  

1.  Para instalar el certificado de cliente independientemente de Configuration Manager, siga las instrucciones que acompañan al método de implementación del certificado elegido para solicitar e instalar el certificado de cliente en el equipo Mac.  

2.  Navegue a la carpeta en la que extrajo el contenido del archivo macclient.dmg que descargó desde el Centro de descarga de Microsoft.  

3.  Escriba la siguiente línea de comandos: **sudo ./ccmsetup -MP <FQDN de Internet del punto de administración\> -SubjectName <valor de asunto del certificado\>**.  El valor de asunto del certificado distingue mayúsculas de minúsculas, por tanto escríbalo tal como aparece en los detalles del certificado.  

     Ejemplo: si en las propiedades del sistema de sitio el valor de FQDN de Internet es **server03.contoso.com** y el certificado de cliente de Mac tiene el FQDN de **mac12.contoso.com** como nombre común en el asunto del certificado, escriba: **sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**.  

4.  Espere hasta que vea el mensaje de que se **completó la instalación** y, a continuación, reinicie el equipo Mac.  

5.  Para asegurarse de que Configuration Manager tiene acceso a este certificado, en el equipo Mac, abra una ventana de terminal y realice estos cambios:  

    a.  Escriba el comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  En el cuadro de diálogo **Keychain Access** (Acceso a cadenas de claves), en la sección **Keychains** (Cadenas de claves), seleccione **Sistema** y, después, en la sección **Categoría**, seleccione **Claves**.  

    c.  Expanda los llaveros para ver los certificados de cliente. Una vez identificado el certificado con la clave privada que acaba de instalar, haga doble clic en dicha clave.  

    d.  En la pestaña **Control de acceso**, seleccione **Confirm before allowing access** (Confirmar antes de permitir el acceso).  

    e.  Vaya a **/Library/Application Support/Microsoft/MCC**, elija **CCMClient** y, después, seleccione **Agregar**.  

    f.  Seleccione **Guardar cambios** y cierre el cuadro de diálogo **Keychain Access** (Acceso a cadenas de claves).  

6.  Si tiene más de un certificado que contiene el mismo asunto, debe especificar el número de serie de certificado para identificar el certificado que quiere usar para el cliente de Configuration Manager. Para ello, use el siguiente comando: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<número de serie\>"**.  

     Por ejemplo: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 Compruebe que la instalación de cliente se ha realizado correctamente. Para ello, abra el elemento **Configuration Manager** en **Preferencias del sistema** en el equipo Mac. También puede actualizar y ver la recopilación **Todos los sistemas** para confirmar que el equipo Mac aparece en esta recopilación como un cliente administrado.  

### <a name="renewing-the-mac-client-certificate"></a>Renovación del certificado de cliente Mac  
 Utilice el siguiente procedimiento antes de renovar el certificado de equipo en los equipos Mac.  

 Este procedimiento quita el SMSID, lo cual es necesario para que el cliente utilice un certificado nuevo o renovado en el equipo Mac.  

> [!IMPORTANT]  
>  Cuando quita y reemplaza el SMSID del cliente, todo el historial del cliente almacenado, como el inventario, se elimina después de eliminar el cliente de la consola de Configuration Manager.  

#### <a name="to-renew-the-mac-client-certificate"></a>Para renovar el certificado de cliente Mac  

1.  Cree y rellene una recopilación de dispositivos para los equipos Mac que deben renovar los certificados de equipo.  

2.  En el área de trabajo **Activos y compatibilidad** , inicie el **Asistente para crear elemento de configuración**.  

3.  En la página **General** del asistente, especifique la siguiente información:  

    -   **NombreQuitar SMSID para Mac**:  

    -   **TipoMac OS X**:  

4.  En la página **Plataformas admitidas** del asistente, asegúrese de que se seleccionan todas las versiones de Mac OS X.  

5.  En la página **Configuración** del asistente, haga clic en **Nueva** y, a continuación, en el cuadro de diálogo **Crear configuración** , especifique la información siguiente:  

    -   **NombreQuitar SMSID para Mac**:  

    -   **Tipo de configuraciónscript**:  

    -   **Tipo de datoscadena**:  

6.  En el cuadro de diálogo **Crear configuración** , en **Script de detección**, haga clic en **Agregar script** para especificar un script que detecta equipos Mac con el SMSID configurado.  

7.  En el cuadro de diálogo **Editar script de detección** , escriba el siguiente script de shell:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Seleccione **Aceptar** para cerrar el cuadro de diálogo **Editar script de detección**.  

9. En el cuadro de diálogo **Crear configuración**, en **Script de corrección (opcional)**, seleccione **Agregar script** para especificar un script que quita el SMSID cuando se encuentra en equipos Mac.  

10. En el cuadro de diálogo **Crear script de corrección** , escriba el siguiente script de shell:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Crear script de corrección**.  

12. En la página **Reglas de compatibilidad** del asistente, seleccione **Nueva** y, después, en el cuadro de diálogo **Crear regla**, especifique la información siguiente:  

    -   **NombreQuitar SMSID para Mac**:  

    -   **Configuración seleccionada**: seleccione **Examinar** y, luego, seleccione el script de detección especificado previamente.  

    -   En el campo **los siguientes valores** escriba **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Habilite la opción **Ejecutar el script de corrección especificado cuando esta configuración no sea compatible**.  

13. Complete el Asistente para crear elemento de configuración.  

14. Cree una línea de base de configuración que contenga el elemento de configuración que acaba de crear e impleméntela en la recopilación de dispositivos que creó en el paso 1.  

     Para obtener más información sobre cómo crear e implementar líneas de base de configuración, consulte [How to create configuration baselines in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) (Cómo crear líneas base de configuración en System Center Configuration Manager).  

15. Después de instalar un nuevo certificado en los equipos Mac a los que se ha quitado el SMSID, ejecute el siguiente comando para configurar el cliente para usar el nuevo certificado:  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. Si tiene más de un certificado que contiene el mismo asunto, debe especificar el número de serie de certificado para identificar el certificado que quiere usar para el cliente de Configuration Manager. Para ello, use el siguiente comando: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<número de serie\>"**.  

     Por ejemplo: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. Reinicie el equipo Mac.  



<!--HONumber=Dec16_HO3-->


