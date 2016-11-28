---
title: Puertos | System Center Configuration Manager
description: "Obtenga información sobre los puertos necesarios y personalizables que usa System Center Configuration Manager para las conexiones."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2e0ccf8cc419545abe8c87c8d9379618f13f47b1


---
# <a name="ports-used-in-system-center-configuration-manager"></a>Puertos que se usan en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

System Center Configuration Manager es un sistema cliente/servidor distribuido. La naturaleza distribuida de Configuration Manager significa que se pueden establecer conexiones entre servidores de sitio, sistemas de sitio y clientes. Algunas conexiones utilizan puertos que no son configurables, mientras que otras admiten puertos personalizados. Debe comprobar que los puertos necesarios están disponibles si utiliza tecnología de filtro de puertos como firewalls, enrutadores, servidores proxy e IPsec.  

> [!NOTE]  
>  Si tiene compatibilidad con clientes basados en Internet mediante el protocolo de puente SSL, además de requisitos de puerto, es posible que también tenga que permitir que algunos verbos y encabezados HTTP atraviesen el firewall. .  

 Configuration Manager usa los puertos que se indican a continuación y no incluyen información para servicios Windows estándar como la configuración de directiva de grupo para Servicios de dominio de Active Directory y la autenticación Kerberos. Para obtener más información sobre los servicios y los puertos de Windows Server, consulte [Introducción al servicio y requisitos del puerto de red para el sistema Windows Server](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

##  <a name="a-namebkmkconfigurableportsa-ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> Puertos configurables  
 Configuration Manager le permite configurar los puertos para los siguientes tipos de comunicación:  

-   Punto de sitios web del catálogo de aplicaciones a punto de servicio web del catálogo de aplicaciones  

-   Punto de proxy de inscripción a punto de inscripción  

-   Cliente a sistema de sitio que ejecuta IIS  

-   Cliente a Internet (como configuración de servidor proxy)  

-   Punto de actualización de software a Internet (como configuración de servidor proxy)  

-   Punto de actualización de software a servidor WSUS  

-   Servidor de sitio a servidor de base de datos del sitio  

-   Puntos de servicios de informes  

    > [!NOTE]  
    >  Los puertos que se usan para el rol de sistema de sitio de punto de servicios de informes se configuran en SQL Server Reporting Services. Configuration Manager usa estos puertos durante las comunicaciones con el punto de servicios de informes. Asegúrese de revisar estos puertos al definir la información de filtro IP para directivas IPsec o para configurar firewalls.  

De forma predeterminada, el puerto HTTP para la comunicación entre cliente y sistema de sitio es el puerto 80, y el puerto HTTPS predeterminado es 443. Los puertos para la comunicación entre cliente y sistema de sitio a través de HTTP o HTTPS se pueden cambiar durante la ejecución del programa de instalación o en las propiedades del sitio en su sitio de Configuration Manager.  

Los puertos que se usan para el rol de sistema de sitio de punto de servicios de informes se configuran en SQL Server Reporting Services. Configuration Manager usa estos puertos durante las comunicaciones con el punto de servicios de informes. Asegúrese de revisar estos puertos al definir la información de filtro IP para directivas IPsec o para configurar firewalls.  

##  <a name="a-namebkmknonconfigurableportsa-non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> Puertos no configurables  
Configuration Manager no permite configurar puertos para los siguientes tipos de comunicación:  

-   Sitio a sitio  

-   Servidor de sitio a sistema de sitio  

-   Consola de Configuration Manager con el proveedor de SMS  

-   Consola de Configuration Manager a Internet  

-   Conexiones a servicios de nube, como Microsoft Intune y puntos de distribución basados en la nube  

##  <a name="a-namebkmkcommunicationportsa-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Puertos usados por clientes y sistemas de sitio de Configuration Manager  
Las secciones siguientes detallan los puertos utilizados para la comunicación en Configuration Manager. En el título de la sección, las flechas entre los equipos representan la dirección de la comunicación:  

-   -- > indica que un equipo inicia la comunicación y el otro equipo siempre responde  

-   &lt; -- > indica que cualquier equipo puede iniciar la comunicación  

###  <a name="a-namebkmkportsaia-asset-intelligence-synchronization-point----microsoft"></a><a name="BKMK_PortsAI"></a> Punto de sincronización de Asset Intelligence -- > Microsoft  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443|  

###  <a name="a-namebkmkportsai-to-sqla-asset-intelligence-synchronization-point----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a> Punto de sincronización de Asset Intelligence -- > SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 (Véase la nota 2, **Puerto alternativo disponible**)|  

###  <a name="a-namebkmkportsappcatalogservice-sqla-application-catalog-web-service-point----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a> Punto de servicio web del catálogo de aplicaciones -- > SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 (Véase la nota 2, **Puerto alternativo disponible**)|  

###  <a name="a-namebkmkportsappcatalogwebsitepointappcatalogwebservicepointa-application-catalog-website-point----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Punto de sitios web del catálogo de aplicaciones -- > Punto de servicio web del catálogo de aplicaciones  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80 (Véase la nota 2, **Puerto alternativo disponible**)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443 (Véase la nota 2, **Puerto alternativo disponible**)|  

###  <a name="a-namebkmkportsclient-appcatalogwebsitepointa-client----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Cliente -- > Punto de sitios web del catálogo de aplicaciones  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80 (Véase la nota 2, **Puerto alternativo disponible**)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443 (Véase la nota 2, **Puerto alternativo disponible**)|  

###  <a name="a-namebkmkportsclient-clientwakeupa-client----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a> Cliente -- > Cliente  
 Además de los puertos indicados en la tabla siguiente, el proxy de reactivación también utiliza los mensajes de solicitud de eco del Protocolo de mensajes de control de Internet (ICMP) desde un equipo cliente a otro equipo cliente si están configurados para proxy de reactivación. Esta comunicación se utiliza para confirmar si el otro equipo cliente está activo en la red. ICMP se conoce a veces como comandos ping de TCP/IP. ICMP no tiene un número de protocolo UDP o TCP y, por lo tanto, no aparece en la tabla siguiente. Sin embargo, los firewalls basados en host en estos equipos cliente o los dispositivos de red intermedios en la subred deberán permitir el tráfico ICMP para que la comunicación de proxy de reactivación se realice correctamente.  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Wake on LAN|9 (Véase la nota 2, **Puerto alternativo disponible**)|--|  
|Proxy de reactivación|25536 (Véase la nota 2, **Puerto alternativo disponible**)|--|  

###  <a name="a-namebkmkportsclient-policymodulea-client----configuration-manager-policy-module-network-device-enrollment-service"></a><a name="BKMK_PortsClient-PolicyModule"></a> Cliente -- > Módulo de directivas de Configuration Manager (servicio de inscripción de dispositivos de red)  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP)||80|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443|  

###  <a name="a-namebkmkportsclient-clouddpa-client----cloud-based-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a> Cliente -- > Punto de distribución basado en la nube  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443|  

###  <a name="a-namebkmkportsclient-dpa-client----distribution-point"></a><a name="BKMK_PortsClient-DP"></a> Cliente -- > Punto de distribución  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80 (Véase la nota 2, **Puerto alternativo disponible**)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443 (Véase la nota 2, **Puerto alternativo disponible**)|  

###  <a name="a-namebkmkportsclient-dp2a-client----distribution-point-configured-for-multicast"></a><a name="BKMK_PortsClient-DP2"></a> Cliente -- > Punto de distribución configurado para la multidifusión  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Protocolo de multidifusión|63000-64000|--|  

###  <a name="a-namebkmkportsclient-dp3a-client----distribution-point-configured-for-pxe"></a><a name="BKMK_PortsClient-DP3"></a> Cliente -- > Punto de distribución configurado para PXE  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de configuración dinámica de host (DHCP)|67 y 68|--|  
|Protocolo trivial de transferencia de archivos (TFTP)|69 (Véase la nota 4 **Demonio FTP trivial (TFTP)**)|--|  
|Capa de negociación de información de inicio (BINL)|4011|--|  

###  <a name="a-namebkmkportsclient-fspa-client----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a> Cliente -- > Punto de estado de reserva  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80 (Véase la nota 2, **Puerto alternativo disponible**)|  

###  <a name="a-namebkmkportsclient-gcdca-client----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a> Cliente -- > Controlador de dominio del Catálogo global  
 Los clientes de Configuration Manager no contactan con un servidor de catálogo global si son equipos de grupo de trabajo o están configurados para comunicarse solo a través de Internet.  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP de catálogo global|--|3268|  
|SSL de LDAP de catálogo global|--|3269|  

###  <a name="a-namebkmkportsclient-mpa-client----management-point"></a><a name="BKMK_PortsClient-MP"></a> Cliente -- > Punto de administración  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Notificación de cliente (comunicación predeterminada antes de usar HTTP o HTTPS)|--|10123 (Véase la nota 2, **Puerto alternativo disponible**)|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80 (Véase la nota 2, **Puerto alternativo disponible**)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443 (Véase la nota 2, **Puerto alternativo disponible**)|  

###  <a name="a-namebkmkportsclient-supa-client----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a> Cliente -- > Punto de actualización de software  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80 o 8530 (Véase la nota 3, **Windows Server Update Services**)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443 o 8531 (Véase la nota 3, **Windows Server Update Services**)|  

###  <a name="a-namebkmkportsclient-smpa-client----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a> Cliente -- > Punto de migración de estado  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80 (Véase la nota 2, **Puerto alternativo disponible**)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443 (Véase la nota 2, **Puerto alternativo disponible**)|  
|Bloque de mensajes del servidor (SMB)|--|445|  

###  <a name="a-namebkmkportsconsole-clienta-configuration-manager-console----client"></a><a name="BKMK_PortsConsole-Client"></a> Consola de Configuration Manager -- > Cliente  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Control remoto (control)|--|2701|  
|Asistencia remota (RDP y RTC)|--|3389|  

###  <a name="a-namebkmkportsconsole-interneta-configuration-manager-console----internet"></a><a name="BKMK_PortsConsole-Internet"></a> Consola de Configuration Manager -- > Internet  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80|  

###  <a name="a-namebkmkportsconsole-rspa-configuration-manager-console----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a> Consola de Configuration Manager -- > Punto de servicios de informes  

||||  
|-|-|-|  
|Descripción|UDP|TCP|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80 (Véase la nota 2, **Puerto alternativo disponible**)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443 (Véase la nota 2, **Puerto alternativo disponible**)|  

###  <a name="a-namebkmkportsconsole-sitea-configuration-manager-console----site-server"></a><a name="BKMK_PortsConsole-Site"></a> Consola de Configuration Manager -- > Servidor de sitio  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (conexión inicial a WMI para localizar el sistema proveedor)|--|135|  

###  <a name="a-namebkmkportsconsole-providera-configuration-manager-console----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a> Consola de Configuration Manager -- > Proveedor de SMS  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkportscertificateregistationpointpolicymodulea-configuration-manager-policy-module-network-device-enrollment-service----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Módulo de directivas de Configuration Manager (servicio de inscripción de dispositivos de red) -- > Punto de registro del certificado  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443 (Véase la nota 2, **Puerto alternativo disponible**)|  

###  <a name="a-namebkmkportsdistmpa-distribution-point----management-point"></a><a name="BKMK_PortsDist_MP"></a> Punto de distribución -- > Punto de administración  
 Un punto de distribución se comunica con el punto de administración en los siguientes escenarios:  

-   Para informar del estado de contenido preconfigurado  

-   Para informar de los datos de resumen de uso  

-   Para informar de la validación de contenido  

-   Un punto de distribución de extracción informa sobre el estado de descarga del paquete  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80 (Véase la nota 2, **Puerto alternativo disponible**)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443 (Véase la nota 2, **Puerto alternativo disponible**)|  

###  <a name="a-namebkmkportsendpointprotectioninterneta-endpoint-protection-point----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a> Punto de Endpoint Protection -- > Internet  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80|  

###  <a name="a-namebkmkportsep-to-sqla-endpoint-protection-point----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a> Punto de Endpoint Protection -- > SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 (Véase la nota 2, **Puerto alternativo disponible**)|  

###  <a name="a-namebkmkportsenrollmentproxyenrollmentpointa-enrollment-proxy-point----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Punto de proxy de inscripción -- > Punto de inscripción  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443 (Véase la nota 2, **Puerto alternativo disponible**)|  

###  <a name="a-namebkmkportsenrollmentenrollmentsqla-enrollment-point----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Punto de inscripción -- > SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 (Véase la nota 2, **Puerto alternativo disponible**)|  

###  <a name="a-namebkmkportsexchangeconnectorhosteda-exchange-server-connector----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a> Conector de Exchange Server -- > Exchange Online  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Administración remota de Windows a través de HTTPS|--|5986|  

###  <a name="a-namebkmkportsexchangeconnectoronprema-exchange-server-connector----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a> Conector de Exchange Server -- > Exchange Server local  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Administración remota de Windows a través de HTTP|--|5985|  

###  <a name="a-namebkmkportsmacenrollmentproxypointa-mac-computer----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Equipo Mac -- > Punto de proxy de inscripción  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443|  

###  <a name="a-namebkmkportsmp-dca-management-point----domain-controller"></a><a name="BKMK_PortsMP-DC"></a> Punto de administración -- > Controlador de dominio  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo ligero de acceso a directorios (LDAP)|--|389|  
|LDAP (conexión de capa de sockets seguros [SSL])|636|636|  
|LDAP de catálogo global|--|3268|  
|SSL de LDAP de catálogo global|--|3269|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkportsmp-sitea-management-point-lt----site-server"></a><a name="BKMK_PortsMP-Site"></a> Punto de administración &lt; -- > Servidor de sitio  
 (Véase la nota 5, **Comunicación entre el servidor de sitio y los sistemas de sitio**)  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Asignador de extremos de RPC|--|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  
|Bloque de mensajes del servidor (SMB)|--|445|  

###  <a name="a-namebkmkportsmp-sqla-management-point----sql-server"></a><a name="BKMK_PortsMP-SQL"></a> Punto de administración -- > SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 (Véase la nota 2, **Puerto alternativo disponible**)|  

###  <a name="a-namebkmkportsmobiledeviceclient-enrollmentproxypointa-mobile-device----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Dispositivo móvil -- > Punto de proxy de inscripción  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443|  

###  <a name="a-namebkmkportsmobiledeviceclient-windowsintunea-mobile-device----microsoft-intune"></a><a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> Dispositivo móvil -- > Microsoft Intune  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443|  

###  <a name="a-namebkmkportsrsp-sqla-reporting-services-point----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a> Punto de servicios de informes -- > SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 (Véase la nota 2, Puerto alternativo disponible)|  

###  <a name="a-namebkmkportsintuneconnector-windowsintunea-service-connection-point----microsoft-intune"></a><a name="BKMK_PortsIntuneConnector-WindowsIntune"></a> Punto de conexión de servicio -- > Microsoft Intune  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443|
Para obtener más información, consulte [Internet access requirements](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls) (Requisitos del acceso de Internet) para obtener información sobre el punto de conexión de servicio.

###  <a name="a-namebkmkportsappcatalogwebservicepointsiteservera-site-server-lt----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Servidor de sitio &lt; -- > Punto de servicio web del catálogo de aplicaciones  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkportsappcatalogwebsitepointsiteservera-site-server-lt----application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Servidor de sitio &lt; -- > Punto de sitios web del catálogo de aplicaciones  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkportssite-aispa-site-server-lt----asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a> Servidor de sitio &lt; -- > Punto de sincronización de Asset Intelligence  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkportssite-clienta-site-server----client"></a><a name="BKMK_PortsSite-Client"></a> Servidor de sitio -- > Cliente  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Wake on LAN|9 (Véase la nota 2, **Puerto alternativo disponible**)|--|  

###  <a name="a-namebkmkportssiteserver-clouddpa-site-server----cloud-based-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a> Servidor de sitio -- > Punto de distribución basado en la nube  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443|  

###  <a name="a-namebkmkportssite-dpa-site-server----distribution-point"></a><a name="BKMK_PortsSite-DP"></a> Servidor de sitio -- > Punto de distribución  
 (Véase la nota 5, **Comunicación entre el servidor de sitio y los sistemas de sitio**)  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkportssite-dca-site-server----domain-controller"></a><a name="BKMK_PortsSite-DC"></a> Servidor de sitio -- > Controlador de dominio  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo ligero de acceso a directorios (LDAP)|--|389|  
|LDAP (conexión de capa de sockets seguros [SSL])|636|636|  
|LDAP de catálogo global|--|3268|  
|SSL de LDAP de catálogo global|--|3269|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkportscertificateregistrationpointsiteservera-site-server-lt----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Servidor de sitio &lt; -- > Punto de registro del certificado  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkportsendpointprotectionsiteservera-site-server-lt----endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a> Servidor de sitio &lt; -- > Punto de Endpoint Protection  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkenrollmentpointsiteservera-site-server-lt----enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a> Servidor de sitio &lt; -- > Punto de inscripción  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkenrollmentproxypointsiteservera-site-server-lt----enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Servidor de sitio &lt; -- > Punto de proxy de inscripción  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkportssite-fspa-site-server-lt----fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a> Servidor de sitio &lt; -- > Punto de estado de reserva  
 (Véase la nota 5, **Comunicación entre el servidor de sitio y los sistemas de sitio**)  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkportsite-interneta-site-server----internet"></a><a name="BKMK_PortSite-Internet"></a> Servidor de sitio -- > Internet  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80 (Véase la nota 1, **Puerto del servidor proxy**)|  

###  <a name="a-namebkmkportsissuingcasiteservera-site-server-lt----issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a> Servidor de sitio &lt; -- > Entidad de certificación emisora (CA)  
 Esta comunicación se utiliza al implementar perfiles de certificados utilizando el punto de registro del certificado. La comunicación no se utiliza para todos los servidores de sitio en la jerarquía; se utiliza solo para el servidor de sitio en la parte superior de la jerarquía.  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Asignador de extremos de RPC|135|135|  
|RPC (DCOM)|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkportssite-rspa-site-server-lt----reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a> Servidor de sitio &lt; -- > Punto de servicios de informes  
 (Véase la nota 5, **Comunicación entre el servidor de sitio y los sistemas de sitio**)  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkportssite-sitea-site-server-lt----site-server"></a><a name="BKMK_PortsSite-Site"></a> Servidor de sitio &lt; -- > Servidor de sitio  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  

###  <a name="a-namebkmkportssite-sqla-site-server----sql-server"></a><a name="BKMK_PortsSite-SQL"></a> Servidor de sitio -- > SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 (Véase la nota 2, **Puerto alternativo disponible**)|  

 Durante la instalación de un sitio que usará un SQL Server remoto para hospedar la base de datos del sitio, debe abrir los puertos siguientes entre el servidor de sitio y SQL Server:  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkportssite-providera-site-server----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a> Servidor de sitio -- > Proveedor de SMS  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICO (Véase la nota 6, **Puertos dinámicos**)|  

###  <a name="a-namebkmkportssite-supa-site-server-lt----software-update-point"></a><a name="BKMK_PortsSite-SUP"></a> Servidor de sitio &lt; -- > Punto de actualización de software  
 (Véase la nota 5, **Comunicación entre el servidor de sitio y los sistemas de sitio**)  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80 o 8530 (Véase la nota 3, Windows Server Update Services)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443 o 8531 (Véase la nota 3, Windows Server Update Services)|  

###  <a name="a-namebkmkportssite-smpa-site-server-lt----state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a> Servidor de sitio &lt; -- > Punto de migración de estado  
 (Véase la nota 5, **Comunicación entre el servidor de sitio y los sistemas de sitio**)  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  

###  <a name="a-namebkmkportsprovider-sqla-sms-provider----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a> Proveedor de SMS -- > SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 (Véase la nota 2, Puerto alternativo disponible)|  

###  <a name="a-namebkmkportssup-interneta-software-update-point----internet"></a><a name="BKMK_PortsSUP-Internet"></a> Punto de actualización de software -- > Internet  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80 (Véase la nota 1, **Puerto del servidor proxy**)|  

###  <a name="a-namebkmkportssup-wsusa-software-update-point----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a> Punto de actualización de software -- > Servidor WSUS ascendente  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP)|--|80 o 8530 (Véase la nota 3, **Windows Server Update Services**)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS)|--|443 o 8531 (Véase la nota 3, **Windows Server Update Services**)|  

###  <a name="a-namebkmkportssql-sqla-sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server --> SQL Server  
 La replicación de base de datos entre sitios requiere que el SQL Server en un sitio se comunique directamente con el SQL Server de su sitio primario o secundario.  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Servicio de SQL Server|--|1433 (Véase la nota 2, Puerto alternativo disponible)|  
|SQL Server Service Broker|--|4022 (Véase la nota 2, Puerto alternativo disponible)|  

> [!TIP]  
>  Configuration Manager no requiere que el Explorador de SQL Server, que utiliza el puerto UDP 1434.  

###  <a name="a-namebkmkportsstatemigrationpoint-to-sqla-state-migration-point----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> Punto de migración de estado -- > SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 (Véase la nota 2, **Puerto alternativo disponible**)|  



###  <a name="a-namebkmyportnotesa-notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> Notas para los puertos usados por clientes y sistemas de sitio de Configuration Manager  

1.  **Puerto de servidor proxy**: este puerto no se puede configurar, pero puede enrutarse a través de un servidor proxy configurado.  

2.  **Puerto alternativo disponible**: se puede definir un puerto alternativo en Configuration Manager para este valor. Si se definió un puerto personalizado, sustitúyalo cuando defina la información del filtro IP para las directivas IPsec o para configurar firewalls.  

3.  **Windows Server Update Services**:WSUS se puede instalar en el sitio web predeterminado (puerto 80) o en un sitio web personalizado (puerto 8530).  

     Después de la instalación, el puerto se puede cambiar. No es necesario utilizar el mismo número de puerto en toda la jerarquía del sitio.  

    -   Si el puerto HTTP es 80, el puerto HTTPS debe ser 443.  

    -   Si el puerto HTTP es cualquier otro, el puerto HTTPS debe ser 1 valor mayor. Por ejemplo, 8530 y 8531.  

    > [!NOTE]  
    >  Al configurar el punto de actualización de software para usar HTTPS, también debe estar abierto el puerto HTTP. Los datos sin cifrar, como los términos de licencia de las actualizaciones específicas, usan el puerto HTTP.  

4.  **Demonio FTP trivial (TFTP)**: el servicio de sistema Demonio FTP Trivial (TFTP) no requiere un nombre de usuario o una contraseña y es una parte integral de los Servicios de implementación de Windows (WDS). El servicio Demonio FTP Trivial implementa la compatibilidad con el protocolo TFTP definido por las siguientes RFC:  

    -   RFC 350: TFTP  

    -   RFC 2347: extensión de opción  

    -   RFC 2348: opción de tamaño de bloque  

    -   RFC 2349: opciones de tamaño de transferencia e intervalo de tiempo de espera  

     El protocolo trivial de transferencia de archivos está diseñado para admitir entornos de arranque sin disco. Los demonios TFTP escuchan en el puerto UDP 69 pero responden desde un puerto alto asignado dinámicamente. Por lo tanto, la habilitación de este puerto permitirá al servicio TFTP recibir solicitudes TFTP entrantes pero no permitirá al servidor seleccionado responder a dichas solicitudes. El servidor seleccionado no podrá responder a peticiones TFTP de entrada a menos que el servidor TFTP esté configurado para responder desde el puerto 69.  

5.  **Comunicación entre el servidor de sitio y los sistemas de sitio**: de forma predeterminada, la comunicación entre el servidor de sitio y los sistemas de sitio es bidireccional. El servidor de sitio inicia la comunicación para configurar el sistema de sitio y, a continuación, la mayoría de los sistemas de sitio se conectan al servidor de sitio para enviar información de estado. Los puntos de servicios de informes y los puntos de distribución no envían información de estado. Si selecciona **Requerir al servidor de sitio iniciar conexiones a este sistema de sitio** en las propiedades de sistema de sitio, no se iniciará la comunicación con el servidor de sitio después de instalar el sistema de sitio. En vez de ello, el servidor de sitio inicia las conexiones y utiliza la cuenta de instalación del sistema de sitio para la autenticación con el servidor de sistema de sitio.  

6.  **Puertos dinámicos**: estos puertos (también conocidos como puertos efímeros) usan un rango de números de puerto, que se define según la versión del sistema operativo. Para obtener más información acerca de los intervalos de puertos predeterminados, consulte [Introducción al servicio y requisitos del puerto de red para el sistema Windows Server](http://go.microsoft.com/fwlink/p/?LinkId=317965).  

##  <a name="a-namebkmkadditionalportsa-additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a> Listas adicionales de puertos  
 Las secciones siguientes proporcionan información adicional acerca de los puertos utilizados por Configuration Manager.  

###  <a name="a-namebkmkclientsharesa-client-to-server-shares"></a><a name="BKMK_ClientShares"></a> Cliente a recursos compartidos de servidor  
 Los clientes utilizan Bloque de mensajes del servidor (SMB) cada vez que se conectan a recursos compartidos UNC. Por ejemplo:  

-   Instalación manual de cliente que especifica la propiedad de la línea de comandos CCMSetup.exe **/source:** .  

-   Clientes de Endpoint Protection que descargan archivos de definición de una ruta de acceso UNC.  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  

###  <a name="a-namebkmksqlportsa-connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a> Conexiones a Microsoft SQL Server  
 Para la comunicación con el motor de base de datos de SQL Server y para la replicación entre sitios, puede utilizar el puerto de SQL Server predeterminado o especificar puertos personalizados:  

-   Uso de las comunicaciones entre sitios:  

    -   SQL Server Service Broker, que usa de forma predeterminada el puerto TCP 4022.  

    -   SQL Server Service, que usa de forma predeterminada el puerto TCP 1433.  

-   La comunicación entre sitios entre el motor de base de datos de SQL Server y varios roles de sistema de sitio de Configuration Manager tienen el puerto TCP 1433 como predeterminado.  

> [!WARNING]  
>  Configuration Manager no admite los puertos dinámicos. Ya que las instancias con nombre de SQL Server usan de manera predeterminada puertos dinámicos para las conexiones con el motor de base de datos, cuando usa una instancia con nombre deberá configurar manualmente el puerto estático que desea usar para la comunicación entre sitios.  

 Los siguientes roles de sistema de sitio se comunican directamente con la base de datos de SQL Server:  

-   Punto de servicio web del catálogo de aplicaciones  

-   Rol de punto de registro de certificado  

-   Rol de punto de inscripción  

-   Punto de administración  

-   Servidor de sitio  

-   Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.  

-   proveedor de SMS  

-   SQL Server --> SQL Server  

Si un servidor SQL Server hospeda una base de datos de más de un sitio, cada base de datos debe usar una instancia independiente de SQL Server y cada instancia debe estar configurada con un conjunto de puertos único.  

Si tiene un firewall habilitado en el equipo con SQL Server, asegúrese de que está configurado para permitir los puertos utilizados por su implementación en todas las ubicaciones en la red entre los equipos que se comunican con SQL Server.  

Para obtener un ejemplo de cómo configurar SQL Server para usar un puerto específico, consulte [Configurar un servidor para que escuche en un puerto TCP específico (Administrador de configuración de SQL Server)](http://go.microsoft.com/fwlink/p/?LinkID=226349) en la biblioteca de TechNet de SQL Server.  


### <a name="bkmk_discovery"> </a> Detección y publicación
Los siguientes puertos se usan para la detección y la publicación de información de sitios:
 - Protocolo ligero de acceso a directorios (LDAP) - 389
 - LDAP (conexión de capa de sockets seguros [SSL]) - 636


 - LDAP de catálogo global: 3268
 - SSL de LDAP de catálogo global: 3269


 - Asignador de extremos de RPC: 135
 - RPC: puertos TCP altos asignados dinámicamente


 - TCP: 1024 - 5000
 - TCP:  49152 - 65535


###  <a name="a-namebkmkexternala-external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Conexiones externas establecidas por Configuration Manager  
 Los clientes o sistemas de sitio de Configuration Manager pueden establecer las siguientes conexiones externas:  

-   [Punto de sincronización de Asset Intelligence -- &gt; Microsoft](#BKMK_PortsAI)  

-   [Punto de Endpoint Protection -- &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

-   [Cliente -- &gt; Controlador de dominio del Catálogo global](#BKMK_PortsClient-GCDC)  

-   [Consola de Configuration Manager -- &gt; Internet](#BKMK_PortsConsole-Internet)  

-   [Punto de administración -- &gt; Controlador de dominio](#BKMK_PortsMP-DC)  

-   [Servidor de sitio -- &gt; Controlador de dominio](#BKMK_PortsSite-DC)  

-   [Servidor de sitio &lt; -- &gt; Entidad de certificación emisora (CA)](#BKMK_PortsIssuingCA_SiteServer)  

-   [Punto de actualización de software -- &gt; Internet](#BKMK_PortsSUP-Internet)  

-   [Punto de actualización de software -- &gt; Servidor WSUS ascendente](#BKMK_PortsSUP-WSUS)  

-   [Punto de conexión de servicio -- &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

###  <a name="a-namebkmkibcmportsa-installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a> Requisitos de instalación de sistemas de sitio que admiten clientes basados en Internet  
 Los puntos de administración y de distribución que admiten clientes basados en Internet, el punto de actualización de software y el punto de estado de reserva utilizan los siguientes puertos para la instalación y reparación:  

-   Servidor de sitio -- > sistema de sitio: asignador de extremos de RPC con los puertos UDP y TCP 135.  

-   Servidor de sitio -- > sistema de sitio: puertos TCP dinámicos de RPC.  

-   Servidor de sitio &lt; --> sistema de sitio: bloques de mensajes del servidor (SMB) mediante el puerto TCP 445.  

Las instalaciones de aplicación y paquete en puntos de distribución requieren los siguientes puertos RPC:  

-   Servidor de sitio -- > punto de distribución: asignador de extremos de RPC con los puertos UDP y TCP 135.  

-   Servidor de sitio -- > punto de distribución: puertos TCP dinámicos de RPC.  

Utilice IPsec para proteger el tráfico entre el servidor de sitio y los sistemas de sitio. Si debe restringir los puertos dinámicos que usa con RPC, puede usar la herramienta de configuración de RPC de Microsoft (rpccfg.exe) para configurar un conjunto limitado de puertos para estos paquetes RPC. Para obtener más información sobre la herramienta de configuración de RPC, vea [Cómo configurar RPC para usar determinados puertos y cómo asegurar esos puertos con IPsec](http://go.microsoft.com/fwlink/p/?LinkId=124096).  

> [!IMPORTANT]  
>  Antes de instalar estos sistemas de sitio, asegúrese de que el servicio de registro remoto se ejecuta en el servidor de sistema de sitio y que ha especificado una cuenta de instalación del sistema de sitio si el sistema de sitio está en un bosque de Active Directory sin una relación de confianza.  

###  <a name="a-namebkmkportsclientinstalla-ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Puertos usados por la instalación de cliente de Configuration Manager  
Los puertos que se utilizan durante la instalación de cliente dependen del método de implementación de cliente. Consulte **Puertos utilizados durante la implementación de cliente de Configuration Manager** del tema [Firewall de Windows y Configuración de puerto para los clientes en System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md) para ver una lista de puertos para cada método de implementación de clientes. Para obtener información sobre cómo configurar Firewall de Windows en el cliente para la instalación de cliente y la comunicación posterior a la instalación, consulte [Firewall de Windows y Configuración de puerto para los clientes en System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md).  

###  <a name="a-namebkmkmigrationportsa-ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> Puertos usados por la migración  
El servidor de sitio que ejecuta la migración usa varios puertos para conectarse a los sitios que correspondan en la jerarquía de orígenes con el fin de recopilar datos en la base de datos de SQL Server de sitios de origen y compartir puntos de distribución.  

 Para obtener información sobre estos puertos, consulte la sección [Required configurations for migration](../../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) (Configuraciones necesarias para la migración) del tema [Requisitos previos para la migración en System Center Configuration Manager](../../../core/migration/prerequisites-for-migration.md).  

###  <a name="a-namebkmkserverportsa-ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a> Puertos usados por Windows Server  
 En la tabla siguiente se incluyen algunos de los puertos clave que Windows Server utiliza, y sus respectivas funciones. Para obtener una lista completa de los requisitos de puertos de red y servicios de Windows Server, consulte [Introducción al servicio y requisitos del puerto de red para el sistema Windows Server](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Sistema de nombres de dominio (DNS)|53|53|  
|Protocolo de configuración dinámica de host (DHCP)|67 y 68|--|  
|Resolución de nombres NetBIOS|137|--|  
|Servicio de datagramas de NetBIOS|138|--|  
|Servicio de sesión de NetBIOS|--|139|  



<!--HONumber=Nov16_HO1-->


