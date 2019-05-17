---
title: Opciones de rol de sistema de sitio
titleSuffix: Configuration Manager
description: Lea este artículo para obtener detalles sobre los roles de sistema de sitio de Configuration Manager que no son necesariamente explicativos.
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a5fb9a553efa634dad314da58298611cdf0bbb58
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65498978"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Opciones de configuración de roles de sistema de sitio para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La mayoría de las opciones de configuración de los roles de sistema de sitio de Configuration Manager son explicativas o se explican en los cuadros de diálogo o el asistente durante la configuración. En las secciones siguientes se explican los roles de sistema de sitio en los que se necesita información adicional para su configuración.  



##  <a name="BKMK_ApplicationCatalog_Website"></a> Punto de sitios web del catálogo de aplicaciones  

> [!Note]  
> A partir de la versión 1806, el punto de sitios web del catálogo de aplicaciones ya no es *necesario* en la versión 1806, pero todavía es *compatible*. Para obtener más información, consulte [Configurar el centro de software](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex).  
> 
> La **experiencia de usuario de Silverlight** del punto de sitios web del catálogo de aplicaciones ya no se admite. Para más información, consulte [Características en desuso y eliminadas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

 Para más información sobre cómo configurar el punto de sitios web del catálogo de aplicaciones, vea [Planear y configurar la administración de aplicaciones](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

 #### <a name="client-connections"></a>Conexiones de cliente
 Seleccione **HTTPS** para usar la configuración de conexión más segura y para comprobar si los clientes se conectan desde Internet. Esta opción requiere un certificado PKI en el servidor para la autenticación del servidor en los clientes y para el cifrado de datos mediante capa de sockets seguros (SSL). Para obtener más información, vea [Requisitos de certificados PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Para ver un ejemplo de implementación del certificado de servidor y obtener información y obtener información sobre cómo configurarlo en Internet Information Services (IIS), consulte [Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  

 #### <a name="add-application-catalog-website-to-trusted-sites-zone"></a>Agregar sitio web del catálogo de aplicaciones a la zona de sitios de confianza  
 En este mensaje se muestra el valor de la configuración predeterminada de cliente si el parámetro **Agregar sitio web predeterminado del catálogo de aplicaciones a una zona de sitios de confianza de Internet Explorer** se ha establecido actualmente en **Verdadero** o **Falso**. Si ha usado una configuración personalizada de cliente para esta opción, habilítela.  

 Si este sistema de sitio está configurado para un nombre de dominio completo (FQDN) y el sitio web no se encuentra en la zona de sitios de confianza de Internet Explorer, se le pedirán las credenciales a los usuarios cuando se conecten al catálogo de aplicaciones.  

 #### <a name="organization-name"></a>Nombre de la organización  

 Escriba el nombre que los usuarios ven en el catálogo de aplicaciones. Esta información de personalización de marca ayuda a los usuarios a identificar este sitio web como una fuente de confianza.  



##  <a name="BKMK_ApplicationCatalog_WebService"></a> Punto de servicio web del catálogo de aplicaciones  

> [!Note]  
> A partir de la versión 1806, el punto de servicio web del catálogo de aplicaciones ya no es *necesario*, pero todavía es un *compatible*. Para obtener más información, consulte [Configurar el centro de software](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex).  

 Para más información sobre cómo configurar el punto de servicio web del catálogo de aplicaciones, vea [Planear y configurar la administración de aplicaciones](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

 #### <a name="https"></a>HTTPS

 Seleccione **HTTPS** para autenticar los puntos de sitios web del catálogo de aplicaciones en este punto de servicio web del catálogo de aplicaciones. Esta opción necesita un certificado PKI en los servidores que ejecutan el punto de sitios web del catálogo de aplicaciones para la autenticación de servidor y para el cifrado de datos por SSL. Para obtener más información, vea [Requisitos de certificados PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Para ver un ejemplo de implementación del certificado de servidor y obtener información y obtener información sobre cómo configurarlo en Internet Information Services (IIS), consulte [Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_CertificateRegistrationPoint"></a> Punto de registro de certificados  

 Para más información sobre cómo configurar el punto de registro de certificado, vea [Introducción a perfiles de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  



##  <a name="BKMK_Distribution_Point"></a> Punto de distribución  

 Para más información sobre cómo configurar el punto de distribución para la distribución de contenido, vea [Administración del contenido y de la infraestructura de contenido](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

 Para más información sobre cómo configurar el punto de distribución para las implementaciones de entornos PXE, vea [Usar PXE para implementar Windows a través de la red](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  

 Para más información sobre cómo configurar el punto de distribución para implementaciones de multidifusión, vea [Usar multidifusión para implementar Windows a través de la red](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).  

 #### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>Instalar y configurar IIS si lo requiere Configuration Manager
 Seleccione esta opción para permitir que Configuration Manager instale y configure IIS en el sistema de sitio (si aún no está instalado). IIS debe estar instalado en todos los puntos de distribución, por lo que debe seleccionar esta opción para continuar con el asistente.  

 #### <a name="site-system-installation-account"></a>Cuenta de instalación del sistema de sitio
 Para los puntos de distribución que se instalan en un servidor del sitio, la cuenta de equipo del servidor del sitio se puede usar como la cuenta de instalación de sistema del sitio. Para más información, vea [Cuentas](/sccm/core/plan-design/hierarchy/accounts#site-system-installation-account).  

 #### <a name="create-a-self-signed-certificate-or-import-a-pki-client-certificate"></a>Crear un certificado autofirmado o importar un certificado de cliente PKI
 Este certificado tiene dos propósitos:  

1.  Autentica el punto de distribución en un punto de administración antes de que el punto de distribución envíe mensajes de estado.  

2.  Cuando se selecciona **Habilitar compatibilidad de PXE para clientes**, el certificado se envía a los equipos para el arranque PXE. Estos usan el certificado para conectarse a un punto de administración durante la implementación del sistema operativo.  

Cuando todos los puntos de administración del sitio estén configurados para HTTP, cree un certificado autofirmado. Después de configurar los puntos de administración para HTTPS, importe un certificado de cliente PKI.  

Para importar el certificado, busque un archivo Public-Key Cryptography Standards #12 (PKCS #12) que contenga un certificado PKI con los requisitos siguientes para Configuration Manager:  

-   El uso previsto debe incluir autenticación de cliente.  

-   Es necesario configurar la clave privada para su exportación.  

No existen requisitos específicos para el nombre de sujeto del certificado ni el nombre alternativo del firmante (SAN). Puede utilizar el mismo certificado para varios puntos de distribución.  

Para obtener más información sobre los requisitos de certificado, vea [Requisitos de certificados PKI](/sccm/core/plan-design/network/pki-certificate-requirements). 

Para obtener un ejemplo de implementación de este certificado, vea [Implementar el certificado de cliente para puntos de distribución](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012).  

#### <a name="enable-this-distribution-point-for-prestaged-content"></a>Habilitar este punto de distribución para contenido preconfigurado
Active esta casilla de verificación para habilitar el punto de distribución para contenido preconfigurado. Cuando habilite esta opción, podrá configurar el comportamiento de distribución al distribuir contenido. Puede elegir entre preconfigurar siempre el contenido en el punto de distribución, preconfigurar el contenido inicial para el paquete (pero usar el proceso de distribución de contenido normal cuando hay actualizaciones en el contenido) o usar siempre el proceso de distribución de contenido normal para el contenido en el paquete. Para obtener más información, vea [Contenido preconfigurado](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).  

#### <a name="boundary-groups"></a>Grupos de límites
 Puede asociar grupos de límites a un punto de distribución. Durante la distribución de contenido, los clientes deben estar en un grupo de límites que esté asociado con el punto de distribución para utilizarlo como una ubicación de origen para el contenido. Configure relaciones entre grupos de límites que determinen cuándo puede un cliente empezar a buscar grupos de límites adicionales para ubicaciones de origen de contenido válidas. Para obtener más información, consulte [Boundary groups (Grupos de límites)](/sccm/core/servers/deploy/configure/boundary-groups).



##  <a name="BKMK_Enrollment_Point"></a> Punto de inscripción  

Los puntos de inscripción se usan para instalar equipos macOS y para inscribir dispositivos administrados con la administración de dispositivos móviles local. Vea los siguientes artículos para más información:  

-   [Cómo implementar clientes en equipos Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)  

-   [Cómo los usuarios inscriben dispositivos con la MDM local](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm)  

#### <a name="allowed-connections"></a>Conexiones permitidas
 La opción HTTPS está seleccionada automáticamente y necesita un certificado PKI en el servidor para la autenticación de servidor en el punto de proxy de inscripción, para la autenticación de servidor en el punto de servicio fuera de banda y para el cifrado de datos por SSL. Para obtener más información, vea [Requisitos de certificados PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Para ver un ejemplo de implementación del certificado de servidor y obtener información sobre cómo configurarlo en IIS, vea [Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_Enrollment_Proxy_Point"></a> Punto de proxy de inscripción  

Para más información sobre cómo configurar un punto de proxy de inscripción para dispositivos móviles, vea [Cómo inscriben dispositivos los usuarios mediante la administración de dispositivos móviles (MDM) local](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm).  

#### <a name="client-connections"></a>Conexiones de cliente
 La opción HTTPS se selecciona automáticamente. Requiere los siguientes certificados PKI en el servidor: 
- Para la autenticación de servidor en dispositivos móviles y equipos Mac que inscribe con Configuration Manager 
- Para el cifrado de datos a través de la Capa de sockets seguros (SSL)

Para obtener más información sobre los requisitos de certificado, vea [Requisitos de certificados PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Para ver un ejemplo de implementación del certificado de servidor y obtener información sobre cómo configurarlo en IIS, vea [Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_Fallback_Status_Point"></a> Punto de estado de reserva  

#### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>Número de mensajes de estado e Intervalo de limitación (en segundos)
La configuración predeterminada para estas opciones es 10 000 mensajes de estado y 3 600 segundos para el intervalo de limitación. Aunque estas opciones son suficientes para la mayoría de los casos, es posible que deba cambiarlas cuando se cumplan las condiciones siguientes:  

-   El punto de estado de reserva sólo acepta conexiones desde la intranet.  

-   Se usa el punto de estado de reserva durante una ejecución de la implementación de cliente en muchos equipos.  

En este escenario, un flujo continuo de mensajes de estado podría crear una acumulación de mensajes de estado que provoque un uso elevado del procesador en el servidor de sitio durante un período de tiempo prolongado. Además, puede que no vea la información actualizada sobre la implementación de cliente en la consola de Configuration Manager y en los informes de implementación de cliente.  

Esta configuración de punto de estado de reserva se ha diseñado para que se configure para mensajes de estado generados durante una implementación de cliente. La configuración no se ha diseñado para configurarla para problemas de comunicación de clientes (por ejemplo, cuando los clientes de Internet no se pueden conectar a su punto de administración basado en Internet). Debido a que el punto de estado de reserva no puede aplicar esta configuración solo a los mensajes de estado generados durante la implementación de cliente, no aplique esta configuración cuando el punto de estado de reserva acepte conexiones de Internet.  

Cada equipo que instala correctamente el cliente de Configuration Manager envía los cuatro mensajes de estado siguientes al punto de estado de reserva:  

-   Implementación de cliente iniciada  

-   Implementación de cliente con éxito  

-   Se inició la asignación de cliente  

-   Asignación de cliente con éxito  

Los equipos que no se puedan instalar (o que asignen el cliente de Configuration Manager) envían mensajes de estado adicionales.  

Por ejemplo, si implementa el cliente de Configuration Manager en 20.000 equipos, la implementación podría crear 80.000 mensajes de estado enviados al punto de estado de reserva. Como la configuración de límite predeterminada permite el envío de 10.000 mensajes de estado al punto de estado de reserva cada 3600 segundos (1 hora), puede que los mensajes de estado se acumulen en el punto de estado de reserva. Debe tener en cuenta el ancho de banda de red disponible entre el punto de estado de reserva y el servidor de sitio, así como la capacidad de procesamiento del servidor de sitio para procesar una gran cantidad de mensajes de estado.  

Para evitar estos problemas, puede aumentar el número de mensajes de estado y reducir el intervalo de limitación.  

Restablezca los valores de limitación para el punto de estado de reserva si se cumple alguna de las siguientes condiciones:  

-   Calcula que los valores de limitación actuales son más altos de lo necesario para procesar mensajes de estado desde el punto de estado de reserva.  

-   Detecta que la configuración de limitación actual crea un uso intensivo del procesador en el servidor del sitio.  

No cambie la configuración de limitación de punto de estado de reserva a menos que entienda las consecuencias. Por ejemplo, si aumenta demasiado la configuración de limitación, el uso del procesador en el servidor de sitio puede aumentar también en exceso, lo cual ralentiza todas las operaciones del sitio.  
