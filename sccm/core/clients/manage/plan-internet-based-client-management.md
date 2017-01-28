---
title: "Administración de cliente basada en Internet | Microsoft Docs"
description: Cree un plan para administrar los clientes basados en Internet en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 828e2ac9a3f9bcea1571d24145a1021fdf1091f3
ms.openlocfilehash: 82867e77840e14e9b8170801ea3c4a9f399c9890


---
# <a name="plan-for-internet-based-client-management-in-system-center-configuration-manager"></a>Planear la administración de cliente basada en Internet en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La administración de cliente basada en Internet (a veces denominada IBCM) le permite administrar clientes de System Center Configuration Manager cuando no están conectados a la red de su empresa, pero disponen de una conexión de Internet estándar. Esta disposición tiene varias ventajas, entre las que se incluye la reducción de costes al no tener que ejecutar redes privadas virtuales (VPN) ni implementar actualizaciones de software de una manera regular.  

 Debido a los mayores requisitos de seguridad derivados de la administración de equipos cliente en una red pública, la administración de cliente basada en Internet requiere que los clientes y los servidores de sistema de sitio a los que se conectan los clientes usen certificados PKI. Esto garantiza que las conexiones queden autenticadas por una autoridad independiente, y que los datos que se dirigen a estos sistemas de sitio o que proceden de ellos se cifren mediante Capa de sockets seguros (SSL).  

 Utilice las siguientes secciones para planear la administración de cliente basada en Internet.  

##  <a name="a-namebkmkibcmfeaturesnotsupporteda-features-that-are-not-supported-on-the-internet"></a><a name="BKMK_IBCM_FeaturesNotSupported"></a> Características no admitidas en Internet  
 No todas las funciones de administración de cliente son apropiadas para Internet y, por lo tanto, no son compatibles cuando se administran clientes en Internet. Las características que no son compatibles con la administración basada en Internet suelen estar basadas en Servicios de dominio de Active Directory, o no son apropiadas para una red pública; por ejemplo, la detección de redes y Wake on LAN (WOL).  

 No se admiten las siguientes características cuando los clientes se administran en Internet:  

-   Implementación de cliente a través de Internet, como la inserción de cliente y la implementación de cliente basada en actualización de software. Utilice en su lugar la instalación de cliente manual.  

-   Asignación automática de sitio.  

-   Wake on LAN.  

-   Implementación de sistema operativo. Sin embargo, puede implementar secuencias de tareas que no implementan un sistema operativo; Por ejemplo, secuencias de tareas que ejecutan scripts y tareas de mantenimiento en clientes.  

-   Control remoto.  

-   Implementación de software en usuarios, a menos que el punto de administración basado en Internet pueda autenticar al usuario en Servicios de dominio de Active Directory mediante la autenticación de Windows (Kerberos o NTLM). Esto es posible cuando el punto de administración basado en Internet confía en el bosque donde reside la cuenta de usuario.  

 Además, la administración de cliente basada en Internet no admite la movilidad. La movilidad permite a los clientes buscar siempre los puntos de distribución más cercanos para descargar contenido. Los clientes administrados en Internet se comunican con sistemas de sitio desde su sitio asignado cuando estos sistemas de sitio están configurados para usar un FQDN de Internet y los roles de sistema de sitio permiten conexiones de cliente desde Internet. Los clientes seleccionan de manera no determinista uno de los sistemas de sitio basados en Internet, independientemente del ancho de banda o de la ubicación física.  

 Cuando tiene un punto de actualización de software que se ha configurado para aceptar conexiones de Internet, los clientes basados en Internet de Configuration Manager siempre realizan una búsqueda con respecto a este punto de actualización de software para determinar las actualizaciones de software que son necesarias. No obstante, cuando estos clientes se encuentran en Internet, primero intentan descargar las actualizaciones de software de Microsoft Update, en lugar de hacerlo desde un punto de distribución basado en Internet. Solo si se produce un error, intentan descargar las actualizaciones de software necesarias desde un punto de distribución basado en Internet. Los clientes que no están configurados para la administración de cliente basada en Internet nunca intentan descargar las actualizaciones de software desde Microsoft Update; siempre usan los puntos de distribución de Configuration Manager.  

##  <a name="a-namebkmkplanforinternetsitesystemsa-considerations-for-client-communications-from-the-internet-or-untrusted-forest"></a><a name="BKMK_PlanforInternetSiteSystems"></a> Consideraciones sobre las comunicaciones de cliente desde Internet o desde un bosque que no es de confianza  
 Los siguientes roles de sistema de sitio instalados en los sitios primarios admiten conexiones provenientes de clientes que se encuentran en ubicaciones que no son de confianza, como Internet o un bosque que no es de confianza (los sitios secundarios no admiten conexiones de cliente desde ubicaciones que no son de confianza):  

-   Punto de sitios web del catálogo de aplicaciones  

-   Módulo de directivas de Configuration Manager  

-   Punto de distribución (los puntos de distribución basados en la nube requieren HTTPS)  

-   Punto de proxy de inscripción  

-   Punto de estado de reserva  

-   Punto de administración  

-   Punto de actualización de software  

 **Sobre los sistemas de sitio con conexión a Internet:**   
Aunque no es necesario tener una relación de confianza entre el bosque de un cliente y el de un servidor de sistema de sitio, cuando el bosque que contiene un sistema de sitio con conexión a Internet confía en el bosque que contiene las cuentas de usuario, esta configuración admite directivas basadas en usuario para los dispositivos en Internet si se habilita la configuración de cliente de **directiva de cliente** **Habilitar solicitudes de directiva de usuario de clientes de Internet**.  

 Por ejemplo, las configuraciones siguientes ilustran cuándo la administración de cliente basada en Internet es compatible con las directivas de usuario para dispositivos de Internet:  

-   El punto de administración basado en Internet se encuentra en la red perimetral, donde se encuentra un controlador de dominio de solo lectura para autenticar al usuario, y el firewall que interviene admite los paquetes de Active Directory.  

-   La cuenta de usuario está en el bosque A (la intranet) y el punto de administración basado en Internet se encuentra en el bosque B (la red perimetral). El bosque B confía en el bosque A y el firewall que interviene admite los paquetes de autenticación.  

-   La cuenta de usuario y el punto de administración basado en Internet están en el bosque A (la intranet). El punto de administración se publica en Internet mediante el uso de un servidor proxy web (como Forefront Threat Management Gateway).  

> [!NOTE]  
>  Si se produce un error en la autenticación Kerberos, a continuación, se intenta automáticamente la autenticación NTLM.  

 Como se muestra en el ejemplo anterior, es posible colocar sistemas de sitio basados en Internet en la intranet cuando están publicados en Internet mediante un servidor proxy web, como ISA Server y Forefront Threat Management Gateway. Estos sistemas de sitio pueden configurarse para conexión de cliente solo desde Internet, o conexiones de cliente desde Internet e intranet. Cuando se utiliza un servidor proxy web, puede configurarlo para protocolo de puente de Capa de sockets seguros (SSL) a SSL (más seguro) o protocolo de túnel SSL:  

-   **Protocolo de puente SSL a SSL:**   
    La configuración recomendada cuando se usan servidores proxy web para la administración de clientes basada en Internet es el protocolo de puente SSL a SSL, que usa la terminación SSL con autenticación. Los equipos cliente deben ser autenticados mediante autenticación de equipo, mientras que los clientes heredados de dispositivos móviles se autentican mediante autenticación de usuario. Los dispositivos móviles inscritos por Configuration Manager no son compatibles con el protocolo de puente SSL.  

     La ventaja de terminación SSL en el servidor proxy web es que los paquetes de Internet están sujetos a inspección antes de que se reenvíen a la red interna. El servidor proxy web autentica la conexión desde el cliente, la termina y, a continuación, abre una nueva conexión autenticada para los sistemas de sitio basados en Internet. Cuando los clientes de Configuration Manager usan un servidor proxy web, la identidad del cliente (GUID de cliente) se incluye de forma segura en la carga de paquete para que el punto de administración no considere como cliente al servidor proxy web. En Configuration Manager no se admite el protocolo de puente con HTTP a HTTPS o de HTTPS a HTTP.  

-   **Protocolo de túnel**:   
    Si su servidor proxy web no puede admitir los requisitos del protocolo de puente SSL o si quiere configurar la compatibilidad con Internet para dispositivos móviles inscritos por Configuration Manager, también se admite el protocolo de túnel SSL. Esto es una opción menos segura porque los paquetes SSL de Internet se reenvían a los sistemas de sitio sin terminación SSL, por lo que no se puede comprobar si incluyen contenido malintencionado. Cuando se utiliza el protocolo de túnel SSL, no hay ningún requisito de certificado para el servidor proxy web.  

##  <a name="a-namebkmkplanforinternetclientsa-planning-for-internet-based-clients"></a><a name="BKMK_PlanforInternetClients"></a> Planeamiento de clientes basados en Internet  
 Debe decidir si los equipos cliente que se administrarán a través de Internet van a configurarse para administración en la intranet e Internet, o solamente para administración de cliente basada en Internet. Solo se puede configurar la opción de administración de cliente durante la instalación de un equipo cliente. Si cambia de opinión más adelante, debe volver a instalar al cliente.  

> [!NOTE]  
>  Si se configura un punto de administración compatible con Internet, los clientes que se conectan al punto de administración serán compatibles con Internet la próxima vez que actualicen su lista de puntos de administración disponibles.  

> [!TIP]  
>  No es necesario restringir la configuración de administración de cliente solamente a Internet, sino que también puede usarla en la intranet.  

 Los clientes que están configurados para la administración de cliente basada únicamente en Internet sólo se comunican con los sistemas de sitio que están configurados para conexiones de cliente de Internet. Esta configuración sería apropiada para equipos que sabe que nunca se conectan a la intranet de su empresa, por ejemplo, equipos para puntos de venta en ubicaciones remotas. También podría ser apropiada si se desea restringir la comunicación de cliente a HTTPS solamente (por ejemplo, para admitir firewall y directivas de seguridad restringidas), y cuando se instalan sistemas de sitio basados en Internet en una red perimetral y se quiere administrar estos servidores mediante el cliente de Configuration Manager.  

 Si desea administrar clientes de grupo de trabajo en Internet, debe instalarlos como solo de Internet.  

> [!NOTE]  
>  Los clientes de dispositivos móviles se configuran automáticamente como solo de Internet cuando están configurados para utilizar un punto de administración basado en Internet.  

 Otros equipos cliente pueden configurarse para la administración de clientes de Internet e intranet. Estos equipos pueden cambiar automáticamente entre administración de cliente basada en Internet y administración de cliente de intranet cuando detectan un cambio de red. Si estos clientes pueden encontrar y conectarse a un punto de administración configurado para conexiones de cliente en la intranet, se administrarán como clientes de intranet con funcionalidad de administración de Configuration Manager completa. Si los clientes no pueden encontrar o conectarse a un punto de administración configurado para conexiones de cliente en la intranet, intentarán conectarse a un punto de administración basado en Internet. Si la conexión se realiza correctamente, estos clientes pasarán entonces a ser administrados por los sistemas de sitio basados en Internet en su sitio asignado.  

 La ventaja de poder cambiar de forma automática entre administración de cliente basada en Internet y administración de cliente de intranet es que los equipos cliente pueden usar automáticamente todas las características de Configuration Manager cada vez que estén conectados a la intranet, a la vez que continúan siendo administrados para funciones de administración esenciales cuando están en Internet. Además, una descarga que haya comenzado en Internet se puede reanudar sin problemas en la intranet y viceversa.  

##  <a name="a-namebkmkprerequisitsforinternetclientmgmta-prerequisites-for-internet-based-client-management"></a><a name="BKMK_PrerequisitsForInternetClientMgmt"></a> Requisitos previos para la administración de cliente basada en Internet  
 La administración de cliente basada en Internet de Configuration Manager presenta las siguientes dependencias externas:  

-   Los clientes que van a administrarse en Internet deben tener una conexión a Internet.  

     Configuration Manager usa conexiones de proveedor de servicios de Internet (ISP) a Internet existentes, que pueden ser permanentes o temporales. Los dispositivos móviles de cliente deben tener una conexión directa a Internet, pero los equipos cliente pueden tener una conexión directa a Internet o conectarse mediante un servidor proxy web.  

-   Los sistemas de sitios que admiten administración de cliente basada en Internet deben tener conectividad a Internet y deben estar en un dominio de Active Directory.  

     Los sistemas de sitio basados en Internet no requieren una relación de confianza con el bosque de Active Directory del servidor del sitio. Sin embargo, cuando el punto de administración basado en Internet puede autenticar al usuario mediante la autenticación de Windows, se admiten las directivas de usuario. Si se produce un error en la autenticación de Windows, se admiten solo las directivas de equipo.  

    > [!NOTE]  
    >  Para admitir las directivas de usuario, también se debe establecer como **VERDADERO** las dos configuraciones de cliente de **Directiva de cliente** :  
    >   
    >  -   **Habilitar sondeo de directiva de usuario en clientes**  
    > -   **Habilitar solicitudes de directiva de usuario de clientes de Internet**  

     Un punto de sitio web del catálogo de aplicaciones basado en Internet también requiere autenticación de Windows para autenticar usuarios cuando su equipo se encuentra en Internet. Este requisito es independiente de las directivas de usuario.  

-   Es necesario disponer de una infraestructura de clave pública (PKI) compatible que pueda implementar y administrar los certificados que los clientes requieren y que se administran en Internet y en los servidores de sistema de sitio basados en Internet.  

     Para obtener más información sobre los certificados PKI, consulte [Requisitos de certificados PKI para System Center Configuration Manager](/sccm/core/plan-design/network/pki-certificate-requirements).  

-   El nombre de dominio completo (FQDN) de Internet de los sistemas de sitio que admiten administración de cliente basada en Internet debe registrarse como entradas de host en servidores DNS públicos.  

-   Los firewalls o servidores proxy que intervienen deben permitir la comunicación de cliente que está asociada a los sistemas de sitio basados en Internet.  

     Requisitos de comunicación de cliente:  

    -   Compatibilidad con HTTP 1.1  

    -   Permitir tipo de contenido HTTP de datos adjuntos de MIME de varias partes (multipart/mixed y application/octet-stream)  

    -   Permitir los siguientes verbos para el punto de administración basado en Internet:  

        -   HEAD  

        -   CCM_POST  

        -   BITS_POST  

        -   GET  

        -   PROPFIND  

    -   Permitir los siguientes verbos para el punto de distribución basado en Internet:  

        -   HEAD  

        -   GET  

        -   PROPFIND  

    -   Permitir los siguientes verbos para el punto de estado de reserva basado en Internet:  

        -   POST  

    -   Permitir los siguientes verbos para el punto de sitio web del catálogo de aplicaciones basado en Internet:  

        -   POST  

        -   GET  

    -   Permitir los siguientes encabezados de HTTP para el punto de administración basado en Internet:  

        -   Intervalo:  

        -   CCMClientID:  

        -   CCMClientIDSignature:  

        -   CCMClientTimestamp:  

        -   CCMClientTimestampsSignature:  

    -   Permitir el siguiente encabezado de HTTP para el punto de administración basado en Internet:  

        -   Intervalo:  

     Para obtener información de configuración compatible con estos requisitos, consulte la documentación del firewall o del servidor proxy.  

     Para obtener información sobre requisitos de comunicación similares cuando se utiliza el punto de actualización de software para conexiones de cliente de Internet, consulte la documentación de Windows Server Update Services (WSUS). Por ejemplo, para WSUS en Windows Server 2003, consulte [Apéndice D: Configuración de seguridad](http://go.microsoft.com/fwlink/p/?LinkId=143368), el apéndice de implementación para la configuración de seguridad.



<!--HONumber=Dec16_HO3-->

