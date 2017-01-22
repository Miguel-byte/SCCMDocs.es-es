---
title: Configurar los certificados | Microsoft Docs | MDM local
description: "Configure certificados de comunicaciones de confianza para la administración local de dispositivos móviles en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
caps.latest.revision: 27
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0d6479bcc134103e6005159a8ea295a5f359a436
ms.openlocfilehash: d7aaad9298308b588f1bc13027082bf07066a3c2


---
# <a name="set-up-certificates-for-trusted-communications-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

La administración local de dispositivos móviles de System Center Configuration Manager requiere que los roles de sistema de sitio del punto de inscripción, el punto de proxy de inscripción, el punto de distribución y el punto de administración de dispositivos estén configurados para comunicaciones de confianza con los dispositivos administrados. Cualquier servidor de sistema de sitio que hospeda uno o varios de esos roles debe tener un certificado PKI exclusivo enlazado al servidor web en el sistema. También, un certificado con la misma raíz que el certificado de los servidores se debe almacenar en los dispositivos administrados con el fin de establecer comunicaciones de confianza con ellos.  

 Para dispositivos unidos a un dominio, los Servicios de certificados de Active Directory instalan automáticamente el certificado necesario con la raíz de confianza en todos los dispositivos. Para los dispositivos no unidos a un dominio, debe obtener un certificado válido con una raíz de confianza por otros medios. Si utiliza la entidad de certificación (CA) del sitio como raíz de confianza (que es la misma que usa Active Directory para los dispositivos unidos a un dominio), los servidores de sistema de sitio del punto de inscripción y el punto de proxy de inscripción deben tener enlazado un certificado emitido por esa CA.  

 Cada dispositivo que se administre deberá tener también instalado un certificado con la misma raíz para admitir comunicaciones de confianza con los roles de sistema de sitio. Para dispositivos inscritos de forma masiva, puede incluir el certificado en el paquete de inscripción que se agrega al dispositivo para inscribirlo cuando un usuario lo inicia por primera vez. Para dispositivos inscritos por el usuario, debe agregar el certificado mediante correo electrónico, descarga web o algún otro método.  

 Otra alternativa para dispositivos no unidos a un dominio, es usar la raíz de una entidad de certificación pública conocida (como Verisign o GoDaddy) para emitir el certificado de servidor. Con ello, se evita tener que instalar manualmente un certificado en el dispositivo, porque la mayoría de los dispositivos confían de forma nativa en las conexiones a los servidores que usan la misma raíz de la entidad de certificación pública. Es una alternativa útil para dispositivos inscritos por el usuario en los que no resulta factible instalar los certificados de confianza a través de la entidad de certificación del sitio en cada dispositivo.  

> [!IMPORTANT]  
>  Existen muchas formas de configurar los certificados para permitir comunicaciones de confianza entre los dispositivos y los servidores de sistema de sitio para la administración local de dispositivos móviles. La información proporcionada en este artículo se facilita como ejemplo de una manera de hacerlo. Para utilizar este método se debe estar ejecutando un servidor en el sitio que tenga instalados el rol Servicios de certificado de Active Directory y los servicios de rol Entidad de certificación e Inscripción web de entidad de certificación. Consulte [Servicios de certificados de Active Directory](http://go.microsoft.com/fwlink/p/?LinkId=115018) para más información e instrucciones sobre este rol de Windows Server.  

 Para configurar el sitio de Configuration Manager para las comunicaciones SSL necesarias para la administración local de dispositivos móviles, siga estos pasos generales:  

-   [Configurar la entidad de certificación (CA) para la publicación de CRL](#bkmk_configCa)  

-   [Crear la plantilla de certificado de servidor web en la entidad de certificación](#bkmk_certTempl)  

-   [Solicitar el certificado de servidor web para cada rol de sistema de sitio](#bkmk_requestCert)  

-   [Enlazar el certificado al servidor web](#bkmk_bindCert)  

-   [Exportar el certificado con la misma raíz que el certificado de servidor web](#bkmk_exportCert)  

##  <a name="a-namebkmkconfigcaa-configure-the-certification-authority-ca-for-crl-publishing"></a><a name="bkmk_configCa"></a> Configurar la entidad de certificación (CA) para la publicación de CRL  
 De forma predeterminada, la entidad de certificación (CA) utiliza listas de revocación de certificados (CRL) basadas en LDAP que permiten conexiones para los dispositivos unidos a un dominio. Deberá agregar listas CRL basadas en HTTP a la entidad de certificación para que se pueda confiar en los dispositivos no unidos a un dominio con certificados emitidos por dicha entidad. Estos certificados son necesarios para las comunicaciones SSL entre los servidores que hospedan los roles de sistema de sitio de Configuration Manager y los dispositivos inscritos para la administración local de dispositivos móviles.  

 Siga los pasos que se describen a continuación para configurar la entidad de certificación para la publicación automática de información de CRL para la emisión de certificados que permitan conexiones de confianza en dispositivos unidos y no unidos a un dominio:  

1.  En el servidor en el que se ejecuta la entidad de certificación de su sitio, haga clic en **Iniciar** > ** Herramientas administrativas** > ** Entidad de certificación**.  

2.  En la consola de la entidad de certificación, haga clic en **CertificateAuthority** y luego en **Propiedades**.  

3.  En las propiedades de CertificateAuthority, haga clic en la pestaña **Extensiones** y asegúrese de que **Seleccionar extensión** está establecido en **Puntos de distribución CRL (CDP)**  

4.  Seleccione **http://<ServerDNSName\>/CertEnroll/<CAName\><CRLNameSuffix\><DeltaCRLAllowed\>.crl**. Y las tres opciones siguientes:  

    -   **Incluir en las CRL. Usada para encontrar la ubicación de diferencias CRL.**  

    -   **Incluir en la extensión CDP de los certificados emitidos.**  

    -   **Incluir en la extensión IDP de CRL emitidas**  

5.  Haga clic en la pestaña **Módulo de salida**, en **Propiedades...** y luego seleccione **Permitir que se publiquen los certificados en el sistema de archivos**.  

6.  Cuando se le notifique que los Servicios de certificados de Active Directory se deben reiniciar, haga clic en **Aceptar**.  

7.  Haga clic en **Certificados revocados**, en **Todas las tareas** y, luego, en **Publicar**.  

8.  En el cuadro de diálogo Publicar CRL, seleccione **Solo diferencias entre listas CRL** y, luego, haga clic en **Aceptar**.  

##  <a name="a-namebkmkcerttempla-create-the-web-server-certificate-template-on-the-ca"></a><a name="bkmk_certTempl"></a> Crear la plantilla de certificado de servidor web en la entidad de certificación  
 Después de publicar la nueva lista de revocación de certificados en la entidad de certificación, el siguiente paso es crear una plantilla de certificado de servidor web. Esta plantilla es necesaria para emitir certificados para los servidores que hospedan los roles de sistema de sitio de punto de inscripción, punto de proxy de inscripción, punto de distribución y punto de administración de dispositivos. Estos servidores serán puntos de conexión de SSL para comunicaciones de confianza entre los roles de sistema de sitio y los dispositivos inscritos.    Siga los pasos que se describen a continuación para crear la plantilla de certificado:  

1.  Cree un grupo de seguridad denominado **ConfigMgr MDM Servers** que contenga los servidores que ejecutan los sistemas de sitio que requieren comunicaciones de confianza con los dispositivos inscritos.  

2.  En la consola de la entidad de certificación, haga clic con el botón derecho en **Plantillas de certificado** y haga clic en **Administrar** para cargar la Consola de plantillas de certificado.  

3.  En el panel de resultados, haga clic con el botón secundario en la entrada que muestra **Servidor web** en la columna **Nombre para mostrar plantilla**y, a continuación, haga clic en **Duplicar plantilla**.  

4.  En el cuadro de diálogo **Duplicar plantilla** , asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, a continuación, haga clic en **Aceptar**.  

    > [!IMPORTANT]  
    >  No seleccione **Windows 2008 Server, Enterprise Edition**. Configuration Manager no admite plantillas de certificados de Windows Server 2008 para comunicaciones de confianza mediante HTTPS.  

    > [!NOTE]  
    >  Si la entidad de certificación que utiliza está en Windows Server 2012, no se le solicitará la versión de la plantilla de certificado al hacer clic en **Duplicar plantilla**. En su lugar, especifíquela en la ficha **Compatibilidad** de las propiedades de la plantilla, de la siguiente manera:  
    >   
    >  **Entidad de certificación**: **Windows Server 2003**  
    >   
    >  **Destinatario del certificado**: **Windows XP / Server 2003**  

5.  En el cuadro de diálogo **Propiedades de plantilla nueva**, en la pestaña **General**, escriba el nombre de la plantilla para generar los certificados web que se utilizarán en los sistemas de sitio de Configuration Manager, como por ejemplo **Servidor web MDM ConfigMgr**.  

6.  Haga clic en la pestaña **Nombre de sujeto**, seleccione **Build from Active Directory information** (Compilado a partir de la información de Active Directory) y, para el formato de nombre de sujeto, especifique **Nombre DNS**. Si **Nombre principal del usuario (UPN)** está seleccionado, desactive la casilla del nombre de sujeto alternativo.  

7.  Haga clic en la pestaña **Seguridad** y elimine el permiso **Inscribir** de los grupos de seguridad **Admins. del dominio** y **Administradores de organización**.  

8.  Haga clic en **Agregar**, escriba **ConfigMgr MDM Servers** en el cuadro de texto y, a continuación, haga clic en **Aceptar**.  

9. Seleccione el permiso **Inscribir** para este grupo y no desactive el permiso **Leer** .  

10. Haga clic en **Aceptar** y cierre la consola de Plantillas de certificado.  

11. En la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**, haga clic en **Nueva**y, a continuación, haga clic en **Plantilla de certificado que se va a emitir**.  

12. En el cuadro de diálogo **Habilitar plantillas de certificados**, seleccione la nueva plantilla que acaba de crear, **Servidor web MDM ConfigMgr** y luego haga clic en **Aceptar**.  

##  <a name="a-namebkmkrequestcerta-request-the-web-server-certificate-for-each-site-system-role"></a><a name="bkmk_requestCert"></a> Solicitar el certificado de servidor web para cada rol de sistema de sitio  
 Los dispositivos inscritos para la administración local de dispositivos móviles tienen que confiar en los puntos de conexión SSL que hospedan el punto de inscripción, el punto de proxy de inscripción, el punto de distribución y el punto de administración de dispositivos.  En los pasos siguientes se describe cómo solicitar el certificado de servidor web para IIS. Tiene que realizar este procedimiento para cada servidor (punto de conexión SSL) que hospede uno de los roles de sistema de sitio requeridos para la administración local de dispositivos móviles.  

1.  En el servidor de sitio primario, abra un símbolo del sistema con permisos de administrador, escriba **MMC** y presione **Entrar**.  

2.  En MMC, haga clic en **Archivo** > ** Agregar o quitar complemento**.  

3.  En el complemento Certificados, seleccione **Certificados**, haga clic en **Agregar**, seleccione **Cuenta de equipo**, haga clic en **Siguiente**, haga clic en **Finalizar** y, finalmente, en **Aceptar** para salir de la ventana Agregar o quitar complemento.  

4.  Haga clic en **Personal** y, a continuación, en **Todas las tareas** > ** Solicitar un nuevo certificado**.  

5.  En el asistente de Inscripción de certificados, haga clic en **Siguiente**, seleccione **Directiva de inscripción de Active Directory** y haga clic en **Siguiente**.  

6.  Seleccione la casilla al lado del certificado de servidor web (**Servidor web MDM ConfigMgr**) y, a continuación, haga clic en **Inscribir**.  

7.  Cuando el certificado esté inscrito, haga clic en **Finalizar**.  

 Dado que cada servidor necesitará un certificado de servidor web único, tendrá que repetir este proceso con cada servidor que hospede uno de los roles de sistema de sitio necesarios para la administración local de dispositivos móviles.  Si un servidor hospeda todos los roles de sistema de sitio, solo será necesario solicitar un certificado de servidor web.  

##  <a name="a-namebkmkbindcerta-bind-the-certificate-to-the-web-server"></a><a name="bkmk_bindCert"></a> Enlazar el certificado al servidor web  
 Ahora, el nuevo certificado debe enlazarse al servidor web de cada servidor de sistema de sitio que hospede los roles de sistema de sitio necesarios para la administración local de dispositivos móviles. Siga estos pasos con cada servidor que hospeda los roles de sistema de sitio de punto de inscripción y punto de proxy de inscripción. Si un servidor hospeda todos los roles de sistema de sitio, solo deberá seguir estos pasos una vez. No es necesario realizar esta tarea para los roles de sistema de sitio de punto de distribución y punto de administración de dispositivos, dado que reciben automáticamente el certificado necesario durante la inscripción.  

1.  En el servidor que hospeda el punto de inscripción, el punto de proxy de inscripción, el punto de distribución o el punto de administración de dispositivos, haga clic en **Iniciar ** > ** Herramientas administrativas ** > ** Administrador de IIS**.  

2.  En Conexiones, vaya a **Sitio web predeterminado**, haga clic con el botón derecho y luego haga clic en **Modificar enlaces...**  

3.  En el cuadro de diálogo Enlaces de sitios, haga clic en **https** y luego en **Editar… **  

4.  En el cuadro de diálogo Modificar enlace de sitio, seleccione el certificado que acaba de inscribir como **certificado SSL**, haga clic en **Aceptar** y, luego, en **Cerrar**.  

5.  En la consola del Administrador de IIS, en Conexiones, seleccione el servidor web y, en el panel Acciones derecho, haga clic en **Reiniciar**.  

##  <a name="a-namebkmkexportcerta-export-the-certificate-with-the-same-root-as-the-web-server-certificate"></a><a name="bkmk_exportCert"></a> Exportar el certificado con la misma raíz que el certificado de servidor web  
 Los Servicios de certificados de Active Directory normalmente instalan el certificado requerido de la entidad de certificación en todos los dispositivos unidos a un dominio. Pero los dispositivos no unidos a un dominio no podrán comunicarse con los roles de sistema de sitio sin un certificado de la entidad de certificación raíz. Para obtener el certificado que necesitan los dispositivos para comunicarse con los roles de sistema de sitio, puede exportarlo desde el certificado enlazado al servidor web.  

 Siga estos pasos para exportar el certificado raíz del certificado del servidor web.  

1.  En el Administrador de IIS, haga clic en **Sitio web predeterminado** y luego, en el panel Acciones de la derecha, haga clic en **Enlaces...**  

2.  En el cuadro de diálogo Enlaces de sitios, haga clic en **https** y luego en **Editar…**  

3.  Asegúrese de que está seleccionado el certificado de servidor web y haga clic en **Ver...**  

4.  En las propiedades del certificado de servidor web, haga clic en **Ruta de certificación**, en la raíz en la parte superior de la ruta de certificación y luego en **Ver certificado**.  

5.  En las propiedades del certificado raíz, haga clic en **Detalles** y luego en **Copiar a archivo...**  

6.  En el Asistente para exportación de certificados, haga clic en **Siguiente**.  

7.  Asegúrese de que el formato seleccionado sea **DER binario codificado X.509 (. CER)** y haga clic en **Siguiente**.  

8.  Para el nombre de archivo, haga clic en **Examinar…**, elija una ubicación en la que guardar el archivo de certificado, asigne un nombre al archivo y haga clic en **Guardar**.  

     Los dispositivos que se van a inscribir deben tener acceso a este archivo para importar el certificado raíz, así que elija una ubicación común a la que puedan acceder la mayoría de los dispositivos, o bien puede guardarlo ahora en una ubicación conveniente (como la unidad C) y moverlo más tarde a una ubicación común.  

     Haga clic en **Siguiente**.  

9. Revise la configuración y haga clic en **Finalizar**.  



<!--HONumber=Dec16_HO3-->


