---
title: Opciones de roles de sistema de sitio | Microsoft Docs
description: "Lea este artículo para obtener detalles sobre los roles de sistema de sitio de Configuration Manager que no son necesariamente explicativos."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b4db5d86cc0ed020ed176feb2e8f1f9dc51a2280
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="configuration-options-for-site-system-roles-for-system-center-configuration-manager"></a>Opciones de configuración de roles de sistema de sitio para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

La mayoría de las opciones de configuración de los roles de sistema de sitio de System Center Configuration Manager son explicativas o se explican en los cuadros de diálogo o el asistente durante la configuración. En las secciones siguientes se explican los roles de sistema de sitio en los que se necesita información adicional para su configuración.  

##  <a name="BKMK_ApplicationCatalog_Website"></a> Punto de sitios web del catálogo de aplicaciones  
 Para más información sobre cómo configurar el punto de sitios web del catálogo de aplicaciones, vea [Planear y configurar la administración de aplicaciones en Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **Conexiones de cliente**  

 Seleccione **HTTPS** para usar la configuración de conexión más segura y para comprobar si los clientes se conectan desde Internet. Esta opción requiere un certificado PKI en el servidor para la autenticación del servidor en los clientes y para el cifrado de datos mediante capa de sockets seguros (SSL). Para obtener más información sobre los requisitos de certificados, vea [Requisitos de certificados PKI para System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para ver un ejemplo de implementación del certificado de servidor y obtener información sobre cómo configurarlo en Internet Information Services (IIS), vea la sección *Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS* del tema [Ejemplo paso a paso de implementación de los certificados PKI para Configuration Manager: Entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

 **Agregar sitio web del catálogo de aplicaciones a la zona de sitios de confianza**  

 En este mensaje se muestra el valor de la configuración predeterminada de cliente si el parámetro **Agregar sitio web predeterminado del catálogo de aplicaciones a una zona de sitios de confianza de Internet Explorer** se ha establecido actualmente en **Verdadero** o **Falso**. Si ha usado una configuración personalizada de cliente para esta opción, tendrá que comprobar este valor por su cuenta.  

 Si este sistema de sitio está configurado para un nombre de dominio completo (FQDN) y el sitio web no se encuentra en la zona de sitios de confianza de Internet Explorer, se le pedirán las credenciales a los usuarios cuando se conecten al catálogo de aplicaciones.  

 **Nombre de la organización**  

 Escriba el nombre que los usuarios ven en el catálogo de aplicaciones. Esta información de personalización de marca ayuda a los usuarios a identificar este sitio web como una fuente de confianza.  

##  <a name="BKMK_ApplicationCatalog_WebService"></a> Punto de servicio web del catálogo de aplicaciones  
 Para más información sobre cómo configurar el punto de servicio web del catálogo de aplicaciones, vea [Planear y configurar la administración de aplicaciones en Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **HTTPS**  

 Seleccione **HTTPS** para autenticar los puntos de sitios web del catálogo de aplicaciones en este punto de servicio web del catálogo de aplicaciones.  Esta opción necesita un certificado PKI en los servidores que ejecutan el punto de sitios web del catálogo de aplicaciones para la autenticación de servidor y para el cifrado de datos por SSL. Para obtener más información sobre los requisitos de certificados, vea [Requisitos de certificados PKI para System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para ver un ejemplo de implementación del certificado de servidor y obtener información sobre cómo configurarlo en IIS, vea la sección *Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS* del tema [Ejemplo paso a paso de implementación de los certificados PKI para Configuration Manager: Entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_CertificateRegistrationPoint"></a> Punto de registro de certificados  
 Para más información sobre cómo configurar el punto de registro de certificado, vea [Introducción a perfiles de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

##  <a name="BKMK_Distribution_Point"></a> Punto de distribución  
 Para más información sobre cómo configurar el punto de distribución para la distribución de contenido, vea [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Para más información sobre cómo configurar el punto de distribución para las implementaciones de entornos PXE, vea [Usar PXE para implementar Windows a través de la red con System Center Configuration Manager](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Para más información sobre cómo configurar el punto de distribución para las implementaciones de multidifusión, vea [Usar multidifusión para implementar Windows a través de la red con System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 **Instalar y configurar IIS si lo requiere Configuration Manager**  
 Seleccione esta opción para permitir que Configuration Manager instale y configure IIS en el sistema de sitio (si aún no está instalado). IIS debe estar instalado en todos los puntos de distribución, por lo que debe seleccionar esta opción para continuar con el asistente.  

 **Cuenta de instalación de sistema de sitio**  
 Para los puntos de distribución que se instalan en un servidor del sitio, la cuenta de equipo del servidor del sitio se puede usar como la cuenta de instalación de sistema del sitio.  

 **Crear un certificado autofirmado o importar un certificado de cliente PKI**  
 Este certificado tiene dos propósitos:  

1.  Autentica el punto de distribución en un punto de administración antes de que el punto de distribución envíe mensajes de estado.  

2.  Si la opción **Habilitar compatibilidad de PXE para clientes** está seleccionada, el certificado se envía a equipos con arranque PXE para que puedan conectarse a un punto de administración durante la implementación del sistema operativo.  

Cuando todos los puntos de administración del sitio estén configurados para HTTP, cree un certificado autofirmado. Después de configurar los puntos de administración para HTTPS, importe un certificado de cliente PKI.  

Para importar el certificado, busque un archivo Public-Key Cryptography Standards #12 (PKCS #12) que contenga un certificado PKI con los requisitos siguientes para Configuration Manager:  

-   El uso previsto debe incluir autenticación de cliente.  

-   Es necesario configurar la clave privada para su exportación.  

No hay requisitos específicos para el nombre de sujeto del certificado o el nombre alternativo de asunto (SAN), y puede utilizar el mismo certificado para varios puntos de distribución.  

Para obtener más información sobre los requisitos de certificados, vea [Requisitos de certificados PKI para System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md). Para ver una implementación de ejemplo de este certificado, consulte la sección *Implementación del certificado de cliente para puntos de distribución* del tema [Ejemplo paso a paso de implementación de los certificados PKI para System Center Configuration Manager: Entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

**Habilitar este punto de distribución para contenido preconfigurado**  
Active esta casilla para habilitar el punto de distribución para contenido preconfigurado. Cuando esta casilla esté activada, podrá configurar el comportamiento de distribución al distribuir contenido. Puede elegir entre preconfigurar siempre el contenido en el punto de distribución, preconfigurar el contenido inicial para el paquete (pero usar el proceso de distribución de contenido normal cuando hay actualizaciones en el contenido) o usar siempre el proceso de distribución de contenido normal para el contenido en el paquete.  

**Grupos de límites**  
 Puede asociar grupos de límites a un punto de distribución. Durante la distribución de contenido, los clientes deben estar en un grupo de límites que esté asociado con el punto de distribución para utilizarlo como una ubicación de origen para el contenido.
 - **Antes de la versión 1610**, puede activar la casilla **Permitir ubicación de origen de reserva para contenido** para permitir a los clientes que están fuera de estos grupos de límites revertir y usar el punto de distribución como ubicación de origen para el contenido cuando no estén disponibles otros puntos de distribución.
 - **A partir de la versión 1610**, ya no se puede configurar **Permitir ubicación de origen de reserva para contenido**.  En su lugar, configure relaciones entre grupos de límites que determinen cuándo puede un cliente empezar a buscar grupos de límites adicionales para ubicaciones de origen de contenido válidas.

##  <a name="BKMK_Enrollment_Point"></a> Punto de inscripción  
Los puntos de inscripción se usan para instalar equipos Mac y para inscribir dispositivos administrados con la administración de dispositivos móviles local. Para obtener más información, consulte:  

-   [Cómo instalar clientes en equipos Mac en Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md)  

-   [How users enroll devices with On-premises Mobile Device Management in System Center Configuration Manager (Cómo inscriben los usuarios dispositivos con la administración local de dispositivos móviles en System Center Configuration Manager)](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

**Conexiones permitidas**  
 La opción HTTPS está seleccionada automáticamente y necesita un certificado PKI en el servidor para la autenticación de servidor en el punto de proxy de inscripción, para la autenticación de servidor en el punto de servicio fuera de banda y para el cifrado de datos por SSL. Para obtener más información sobre los requisitos de certificados, vea [Requisitos de certificados PKI para System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para ver un ejemplo de implementación del certificado de servidor y obtener información sobre cómo configurarlo en IIS, vea la sección *Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS* del tema [Ejemplo paso a paso de implementación de los certificados PKI para Configuration Manager: Entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_Enrollment_Proxy_Point"></a> Punto de proxy de inscripción  
Para más información sobre cómo configurar un punto de proxy de inscripción para dispositivos móviles, vea [Cómo inscriben dispositivos los usuarios mediante la administración de dispositivos móviles (MDM) local en System Center Configuration Manager](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

**Conexiones de cliente**  
 La opción HTTPS está seleccionada automáticamente y necesita un certificado PKI en el servidor para la autenticación de servidor en dispositivos móviles y en equipos Mac inscritos por Configuration Manager, y para el cifrado de datos por SSL (capa de sockets seguros). Para obtener más información sobre los requisitos de certificados, vea [Requisitos de certificados PKI para System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para ver un ejemplo de implementación del certificado de servidor y obtener información sobre cómo configurarlo en IIS, vea la sección *Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS* del tema [Ejemplo paso a paso de implementación de los certificados PKI para Configuration Manager: Entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_Fallback_Status_Point"></a> Punto de estado de reserva  
**Número de mensajes de estado** e **Intervalo de limitación (en segundos)**  
Aunque la configuración predeterminada para estas opciones (10.000 mensajes de estado y 3.600 segundos para el intervalo de limitación) son suficientes para la mayoría de las circunstancias, es posible que tenga que cambiarla cuando se cumplen las condiciones siguientes:  

-   El punto de estado de reserva sólo acepta conexiones desde la intranet.  

-   Se usa el punto de estado de reserva durante una ejecución de la implementación de cliente en muchos equipos.  

En este escenario, un flujo continuo de mensajes de estado podría crear una acumulación de mensajes de estado que provoque un uso elevado de la unidad central de procesamiento (CPU) en el servidor de sitio durante un período de tiempo prolongado. Además, puede que no vea la información actualizada sobre la implementación de cliente en la consola de Configuration Manager y en los informes de implementación de cliente.  

Esta configuración de punto de estado de reserva se ha diseñado para que se configure para mensajes de estado generados durante una implementación de cliente. La configuración no se ha diseñado para configurarla para problemas de comunicación de clientes (por ejemplo, cuando los clientes de Internet no se pueden conectar a su punto de administración basado en Internet). Debido a que el punto de estado de reserva no puede aplicar esta configuración solo a los mensajes de estado generados durante la implementación de cliente, no aplique esta configuración cuando el punto de estado de reserva acepte conexiones de Internet.  

Cada equipo que instala correctamente el cliente de System Center 2012 Configuration Manager envía los cuatro mensajes de estado siguientes al punto de estado de reserva:  

-   Implementación de cliente iniciada  

-   Implementación de cliente con éxito  

-   Se inició la asignación de cliente  

-   Asignación de cliente con éxito  

Los equipos que no se puedan instalar (o que asignen el cliente de Configuration Manager) envían mensajes de estado adicionales.  

Por ejemplo, si implementa el cliente de Configuration Manager en 20.000 equipos, la implementación podría crear 80.000 mensajes de estado enviados al punto de estado de reserva. Como la configuración de límite predeterminada permite el envío de 10.000 mensajes de estado al punto de estado de reserva cada 3600 segundos (1 hora), puede que los mensajes de estado se acumulen en el punto de estado de reserva. También necesita tener en cuenta el ancho de banda de red disponible entre el punto de estado de reserva y el servidor de sitio, así como la capacidad de procesamiento del servidor de sitio para procesar una gran cantidad de mensajes de estado.  

Para evitar estos problemas, puede aumentar el número de mensajes de estado y reducir el intervalo de limitación.  

Restablezca los valores de limitación para el punto de estado de reserva si se cumple alguna de las siguientes condiciones:  

-   Calcula que los valores de limitación actuales son más altos de lo necesario para procesar mensajes de estado desde el punto de estado de reserva.  

-   Detecta que la configuración de limitación actual crea un uso intensivo de la CPU en el servidor del sitio.  

No cambie la configuración de limitación de punto de estado de reserva a menos que entienda las consecuencias. Por ejemplo, si aumenta demasiado la configuración de limitación, el uso de CPU en el servidor de sitio puede aumentar también en exceso, lo cual ralentiza todas las operaciones del sitio.  
