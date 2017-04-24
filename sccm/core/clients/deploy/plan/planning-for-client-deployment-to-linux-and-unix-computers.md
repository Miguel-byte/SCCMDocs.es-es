---
title: "Planeación de la implementación del cliente en equipos Linux y UNIX | Microsoft Docs"
description: "Planee la implementación del cliente en equipos Linux y UNIX con System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
caps.latest.revision: 9
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: dad941d5984fc7e0b43954b14c3966bb2632ad05
ms.lasthandoff: 12/16/2016


---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-system-center-configuration-manager"></a>Planificación de la implementación del cliente en equipos Linux y UNIX con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede instalar el cliente de System Center Configuration Manager en equipos que ejecutan Linux o UNIX. Este cliente está diseñado para servidores que funcionan como un equipo de grupo de trabajo, y no admite la interacción con usuarios que han iniciado sesión. Una vez que se ha instalado el software cliente y el cliente establece comunicación con el sitio de Configuration Manager, el cliente se administra mediante la consola de Configuration Manager y los informes.  

> [!NOTE]  
>  El cliente de Configuration Manager en los equipos UNIX y Linux no admite las siguientes capacidades de administración:  
>   
>  -   Instalación de inserción de cliente  
> -   Implementación de sistema operativo  
> -   Implementación de aplicaciones; en lugar de implementar software mediante paquetes y programas.  
> -   Inventario de software  
> -   Actualizaciones de software  
> -   Configuración de compatibilidad  
> -   Control remoto  
> -   Administración de energía  
> -   Comprobación y corrección de cliente del estado de cliente  
> -   Administración de cliente basada en Internet  

 Para obtener más información sobre las distribuciones de Linux y UNIX admitidas y el hardware necesario para admitir el cliente de Linux y UNIX, consulte [Hardware recomendado para System Center Configuration Manager](../../../../core/plan-design/configs/recommended-hardware.md).  

 Use la información en este artículo para ayudarle a planear la implementación del cliente de Configuration Manager para Linux y UNIX.  

##  <a name="BKMK_ClientDeployPrereqforLnU"></a> Requisitos previos para la implementación del cliente en servidores UNIX y Linux  
 Utilice la siguiente información para determinar los requisitos previos para que debe tener correctamente en su lugar instalación al cliente para Linux y UNIX.  

###  <a name="BKMK_ClientDeployExternalforLnU"></a> Dependencias externas a Configuration Manager:  
 En las tablas siguientes se indican los requisitos de los sistemas operativos UNIX y Linux y las dependencias de los paquetes de software.  

 **Red Hat Enterprise Linux ES versión 4**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas estándar C|2.3.4-2|  
|Openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|0.9.7a-43.1|  
|PAM|Módulos de autenticación conectables|0.77-65.1|  

 **Red Hat Enterprise Linux Server versión 5.1 (Tikanga)**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas estándar C|2.5-12|  
|Openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|0.9.8b-8.3.el5|  
|PAM|Módulos de autenticación conectables|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server versión 6**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas estándar C|2.12-1.7|  
|Openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|1.0.0-4|  
|PAM|Módulos de autenticación conectables|1.1.1-4|  

 **Solaris 9 SPARC**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|Revisión del sistema operativo|Pérdida de memoria de PAM|112960-48|  
|SUNWlibC|libC incluido en compiladores Sun Workshop (sparc)|5.9,REV=2002.03.18|  
|SUNWlibms|Forte Developer libm compartido incluido (sparc)|5.9,REV=2001.12.10|  
|Openssl|SMCosslg (sparc)<br /><br /> Sun no proporciona una versión de OpenSSL para Solaris 9 SPARC. Hay una versión disponible para Sunfreeware.|0.9.7g|  
|PAM|Módulos de autenticación conectables<br /><br /> SUNWcsl, Core Solaris, (compartido Libs) (sparc)|11.9.0,REV=2002.04.06.15.27|  

 **Solaris 10 SPARC**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|Revisión del sistema operativo|Pérdida de memoria de PAM|117463-05|  
|SUNWlibC|libC incluido en compiladores Sun Workshop (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Bibliotecas de Math & Microtasking (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Bibliotecas de Math & Microtasking (raíz) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Bibliotecas de Core Solaris (raíz) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Bibliotecas de Core Solaris (raíz) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|Openssl|Bibliotecas de SUNopenssl (Usr)<br /><br /> Sun proporciona las bibliotecas OpenSSL para Solaris 10 SPARC. Están incluidas en el sistema operativo.|11.10.0,REV=2005.01.21.15.53|  
|PAM|Módulos de autenticación conectables<br /><br /> SUNWcsr, Core Solaris, (raíz) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|Revisión del sistema operativo|Pérdida de memoria de PAM|117464-04|  
|SUNWlibC|Sun Workshop libc incluido en compiladores (i386)|5.10,REV=2004.12.20|  
|SUNWlibmsr|Bibliotecas de Math & Microtasking (raíz) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Core Solaris, (bibliotecas compartidas) (i386)|11.10.0,REV=2005.01.21.16.34|  
|SUNWcslr|Bibliotecas de Core Solaris (raíz) (i386)|11.10.0, REV=2005.01.21.16.34|  
|Openssl|Bibliotecas de SUNWopenssl; Bibliotecas OpenSSL (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Módulos de autenticación conectables<br /><br /> SUNWcsr Core Solaris, (Root)(i386)|11.10.0,REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|libC incluido en compiladores Sun Workshop|5.11, REV=2011.04.11|  
|SUNWlibmsr|Bibliotecas de Math y Microtasking (raíz)|5.11, REV=2011.04.11|  
|SUNWcslr|Bibliotecas de Core Solaris (raíz)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (bibliotecas compartidas)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (raíz)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|Bibliotecas OpenSSL (Usr)|11.11.0,REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------|-----------|---------------|  
|SUNWlibC|libC incluido en compiladores Sun Workshop|5.11, REV=2011.04.11|  
|SUNWlibmsr|Bibliotecas de Math y Microtasking (raíz)|5.11, REV=2011.04.11|  
|SUNWcslr|Bibliotecas de Core Solaris (raíz)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (bibliotecas compartidas)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (raíz)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|Bibliotecas OpenSSL (Usr)|11.11.0,REV=2010.05.25.01.00|  

 **SUSE Linux Enterprise Server 9 (i586)**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|Service Pack 4|SUSE Linux Enterprise Server 9||  
|gcc-41.rpm de revisión de SO|Biblioteca compartida estándar|41-4.1.2_20070115-0.6|  
|lib stdc++-41.rpm de revisión de SO|Biblioteca compartida estándar|41-4.1.2_20070115-0.6|  
|Openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|0.9.7d-15.35|  
|PAM|Módulos de autenticación conectables|0.77-221-11|  

 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|glibc-2,4-31,30|Biblioteca compartida estándar C|2.4-31.30|  
|Openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|0.9.8a-18,15|  
|PAM|Módulos de autenticación conectables|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|Biblioteca compartida estándar C|2.9-13.2|  
|PAM|Módulos de autenticación conectables|pam-1.0.2-20.1|  

 **Universal Linux (Debian package) Debian, Ubuntu Server**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|libc6|Biblioteca compartida estándar C|2.3.6|  
|Openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|0.9.8 o 1.0|  
|PAM|Módulos de autenticación conectables|0.79-3|  

 **Universal Linux (RPM package) CentOS, Oracle Linux**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Biblioteca compartida estándar C|2.5-12|  
|Openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|0.9.8 o 1.0|  
|PAM|Módulos de autenticación conectables|0.99.6.2-3.14|  

 **IBM AIX 5L 5.3**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|Versión de SO|Versión de sistema operativo|AIX 5.3, Technology Level 6, Service Pack 5|  
|xlC.rte|Tiempo de ejecución en XL C/C++|9.0.0.2|  
|openssl.base|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|0.9.8.4|  

 **IBM AIX 6.1**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|Versión de SO|Versión de sistema operativo|AIX 6.1, cualquier nivel de tecnología y Service Pack|  
|xlC.rte|Tiempo de ejecución en XL C/C++|9.0.0.5|  
|OpenSSL/openssl.base|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|Versión de SO|Versión de sistema operativo|AIX 7.1, cualquier nivel de tecnología y Service Pack|  
|xlC.rte|Tiempo de ejecución en XL C/C++||  
|OpenSSL/openssl.base|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras||  

 **HP-UX 11i v2 IA 64**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|HPUXBaseOS|SO básico|B.11.23|  
|HPUXBaseAux|Auxiliar de SO HP-UX básico|B.11.23.0706|  
|HPUXBaseAux.openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|A.00.09.07l.003|  
|PAM|Módulos de autenticación conectables|En HP-UX, PAM forma parte de los principales componentes del sistema operativo. No hay otras dependencias.|  

 **HP-UX 11i v2 PA-RISC**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|Entorno operativo HP-UX Foundation|B.11.23.0706|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Bibliotecas de herramientas de desarrollo compatibles|B.11.23|  
|HPUXBaseAux|Auxiliar de SO HP-UX básico|B.11.23.0706|  
|HPUXBaseAux.openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|A.00.09.071.003|  
|PAM|Módulos de autenticación conectables|En HP-UX, PAM forma parte de los principales componentes del sistema operativo. No hay otras dependencias.|  

 **HP-UX 11i v3 PA-RISC**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|Entorno operativo HP-UX Foundation|B.11.31.0709|  
|OS-Core.MinimumRuntime.CORE2-SHLIBS|Bibliotecas de emulador de IA específico|B.11.31|  
|openssl/Openssl.openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|A.00.09.08d.002|  
|PAM|Módulos de autenticación conectables|En HP-UX, PAM forma parte de los principales componentes del sistema operativo. No hay otras dependencias.|  

 **HP-UX 11i v3 IA64**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|Entorno operativo HP-UX Foundation|B.11.31.0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Bibliotecas de desarrollo de IA específico|B.11.31|  
|SysMgmtMin|Herramientas de implementación de software mínimo|B.11.31.0709|  
|SysMgmtMin.openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|A.00.09.08d.002|  
|PAM|Módulos de autenticación conectables|En HP-UX, PAM forma parte de los principales componentes del sistema operativo. No hay otras dependencias.|  

 **Dependencias de Configuration Manager:** La tabla siguiente enumera los roles de sistema de sitio que admiten clientes Linux y UNIX. Para obtener más información sobre estos roles de sistema de sitio, consulte [Determinar los roles de sistema de sitio para System Center Configuration Manager](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|Sistema de sitio de Configuration Manager|Más información|  
|---------------------------------------|----------------------|  
|Punto de administración|Si bien no es necesario un punto de administración para instalar el cliente de Configuration Manager para Linux y UNIX, debe tener un punto de administración para transferir información entre equipos cliente y servidores de Configuration Manager. Sin un punto de administración, no puede administrar los equipos cliente.|  
|Punto de distribución|El punto de distribución no tiene que instalar un cliente de Configuration Manager para Linux y UNIX. Sin embargo, la función de sistema de sitio es necesaria si implementa software en servidores Linux y UNIX.<br /><br /> Dado que el cliente de Configuration Manager para Linux y UNIX no es compatible con las comunicaciones que usan SMB, los puntos de distribución que se usan con el cliente deben admitir la comunicación HTTP o HTTPS.|  
|Punto de estado de reserva|El punto de estado de reserva no tiene que instalar un cliente de Configuration Manager para Linux y UNIX. Pero el punto de estado de reserva permite a los equipos en el sitio de Configuration Manager que envíen mensajes de estado cuando no se puedan comunicar con un punto de administración. Cliente también puede enviar su estado de instalación en el punto de estado de reserva.|  

 **Requisitos de firewall**: Asegúrese de que los servidores de seguridad no bloquean las comunicaciones a través de los puertos que especifique como puertos de solicitud de cliente. El cliente para Linux y UNIX se comunica directamente con los puntos de administración, los puntos de distribución y los puntos de estado de reserva.  

 Para obtener información sobre los puertos de solicitud y comunicación del cliente, consulte [Configurar al cliente para Linux y UNIX buscar puntos de administración](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="BKMK_PlanningforCommunicationsforLnU"></a> Planeamiento para la comunicación a través de confianzas de bosque para servidores Linux y UNIX  
 Los servidores Linux y UNIX que administre con Configuration Manager funcionan como clientes de grupo de trabajo y requieren configuraciones similares como clientes basados en Windows que se encuentran en un grupo de trabajo. Para obtener más información sobre las comunicaciones de los equipos que están en grupos de trabajo, consulte la sección [Comunicaciones entre bosques de Active Directory](../../../../core/plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest) en el tema [Comunicaciones entre puntos de conexión en System Center Configuration Manager](../../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

###  <a name="BKMK_ServiceLocationforLnU"></a> Ubicación del servicio por el cliente para Linux y UNIX  
 La tarea de localizar un servidor de sistema de sitio que proporciona servicio a los clientes se conoce como ubicación del servicio. A diferencia de un cliente basado en Windows, el cliente para Linux y UNIX no utiliza Active Directory para la ubicación del servicio. Además, el cliente de Configuration Manager para Linux y UNIX no admite una propiedad del cliente que especifique el sufijo de dominio de un punto de administración. En su lugar, el cliente obtiene información acerca de los servidores de sistema de sitio adicionales que proporcionan servicios a los clientes desde un punto de administración conocidos que al instalar el software cliente se asigna.  

 Para obtener más información sobre la ubicación del servicio, consulte la sección [Ubicación del servicio y cómo los clientes averiguan su punto de administración asignado](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location) en el tema [Comprender cómo los clientes buscan servicios y recursos de sitio para System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

##  <a name="BKMK_SecurityforLnU"></a> Planeamiento de seguridad y certificados para servidores Linux y UNIX  
 Para las comunicaciones autenticadas y seguras con los sitios de Configuration Manager, el cliente de Configuration Manager para Linux y UNIX usa el mismo modelo de comunicación que el cliente para Windows.  

 Cuando se instala el cliente Linux y UNIX, puede asignar al cliente un certificado PKI que le permite usar HTTPS para comunicarse con los sitios de Configuration Manager. Si no asigna un certificado PKI, el cliente crea un certificado autofirmado y se comunica sólo HTTP.  

 Los clientes que se proporcionan un certificado PKI cuando instala usan HTTPS para comunicarse con los puntos de administración. Cuando un cliente no puede localizar un punto de administración que admite HTTPS, se derivará para utilizar HTTP con el certificado PKI proporcionado.  

 Cuando un cliente Linux o UNIX utiliza un certificado PKI no debe aprobarlas. Cuando un cliente usa un certificado autofirmado, revise la configuración de la jerarquía de aprobación de cliente en la consola de Configuration Manager. Si el método de aprobación de cliente no es **Aprobar automáticamente todos los equipos (no recomendados)**, el cliente debe aprobar manualmente.  

 Para obtener más información sobre cómo aprobar manualmente el cliente, consulte la sección [Administrar clientes desde el nodo Dispositivos](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) en el tema [Cómo administrar clientes en System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

 Para obtener más información sobre el uso de certificados en Configuration Manager, consulte [Requisitos de certificados PKI para System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

###  <a name="BKMK_AboutCertsforLnU"></a> Acerca de los certificados para su uso por servidores Linux y UNIX  
 El cliente de Configuration Manager para Linux y UNIX usa un certificado autofirmado o un certificado de PKI X.509 igual que los clientes basados en Windows. No hay ningún cambio en los requisitos de la PKI para los sistemas de sitio de Configuration Manager para administrar los clientes de UNIX y Linux.  

 Los certificados que usa para los clientes de UNIX y Linux que se comunican con los sistemas de sitio de Configuration Manager deben tener un formato Public Key Certificate Standard (PKCS #12) y debe conocerse la contraseña para que pueda especificársela al cliente cuando se especifica el certificado PKI.  

 El cliente de Configuration Manager para Linux y UNIX es compatible con un solo certificado PKI y no admite varios certificados. Por lo tanto, no se aplican los criterios de selección de certificado que configure para un sitio de Configuration Manager.  

###  <a name="BKMK_ConfigCertsforLnU"></a> Configurar certificados para servidores Linux y UNIX  
 Para configurar un cliente de Configuration Manager para servidores Linux y UNIX para que use las comunicaciones HTTPS, debe configurar el cliente para que use un certificado PKI en el momento de instalar el cliente. No se puede aprovisionar un certificado antes de la instalación del software cliente.  

 Cuando se instala un cliente que utiliza un certificado PKI, utilice el parámetro de línea de comandos **- /usepkicert** para especificar la ubicación y el nombre de un archivo PKCS #12 que contiene el certificado PKI. Además debe utilizar el parámetro de línea de comandos **- certpw** para especificar la contraseña para el certificado.  

 Si no se especifica **- /usepkicert**, el cliente genera un certificado autofirmado e intenta comunicarse con servidores de sistema de sitio solo mediante HTTP.  

##  <a name="BKMK_NoSHA-256"></a> Acerca de los sistemas operativos Linux y UNIX que no admiten SHA-256  
 Los siguientes sistemas operativos Linux y UNIX que se admiten como clientes para Configuration Manager se publicaron con versiones de OpenSSL que no admiten SHA-256:  

-   Versión de Red Hat Enterprise Linux 4 (x 86 o x 64)  

-   Versión de Solaris 9 (SPARC) y la versión de Solaris 10 (SPARC y x 86)  

-   SUSE Linux Enterprise Server versión 9 (x 86)  

-   Versión de HP-UX 11iv2 (PA-RISH/IA64)  

 Para administrar estos sistemas operativos con Configuration Manager, debe instalar el cliente de Configuration Manager para Linux y UNIX con un conmutador de línea de comandos que indique al cliente que omita la validación de SHA-256. Los clientes de Configuration Manager que se ejecutan en estas versiones de sistema operativo funcionan en un modo menos seguro que los clientes que admiten SHA-256. Este modo de operación menos seguro tiene el siguiente comportamiento:  

-   Los clientes no validan la firma de servidor del sitio asociada con la directiva que se solicitan desde un punto de administración.  

-   Los clientes no validan el hash para los paquetes que se descargan desde un punto de distribución.  

> [!IMPORTANT]  
>  El **ignoreSHA256validation** opción le permite ejecutar el cliente para equipos UNIX y Linux en un modo menos seguro. Esto está pensado para su uso en plataformas anteriores que no incluía compatibilidad con SHA-256. Esto es un reemplazo de seguridad y no se recomienda por Microsoft, pero se puede usar en un entorno de centro de datos segura y de confianza.  

 Cuando se instala el cliente de Configuration Manager para Linux y UNIX, la secuencia de comandos de instalación comprueba la versión del sistema operativo. De forma predeterminada, si la versión del sistema operativo se identifica como que se ha publicado sin una versión de OpenSSL que admita SHA-256, la instalación del cliente de Configuration Manager produce un error.  

 Para instalar el cliente de Configuration Manager en los sistemas operativos Linux y UNIX que no se hayan publicado con una versión de OpenSSL que admita SHA-256, debe usar el conmutador de instalación de la línea de comandos **ignoreSHA256validation**. Cuando se usa esta opción de línea de comandos en un sistema operativo Linux o UNIX aplicable, el cliente de Configuration Manager omitirá la validación de SHA-256 y, después de la instalación, el cliente no usará SHA-256 para firmar los datos que envía a los sistemas de sitio mediante HTTP. Para obtener información sobre cómo configurar los clientes de Linux y UNIX para usar certificados, consulte [Planning for Security and Certificates for Linux and UNIX Servers](#BKMK_SecurityforLnU) en este tema. Para obtener más información sobre el requisito SHA-256, consulte la sección [Configurar la firma y el cifrado](../../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption) en el tema [Configurar la seguridad en System Center Configuration Manager](../../../../core/plan-design/security/configure-security.md).  

> [!NOTE]  
>  La opción de línea de comandos **ignoreSHA256validation** se ignora en los equipos que ejecutan una versión de Linux y UNIX que se publicaron con versiones de OpenSSL que admiten SHA-256.  

