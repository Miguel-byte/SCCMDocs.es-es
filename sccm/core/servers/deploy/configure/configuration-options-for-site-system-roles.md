---
title: Opciones de roles de sistema de sitio | System Center Configuration Manager
description: "Lea este artículo para obtener detalles sobre los roles de sistema de sitio de Configuration Manager que no son necesariamente explicativos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a3c370dedc23e2eda38bd942b1d5bed91bdc3876

---
# <a name="configuration-options-for-site-system-roles-for-system-center-configuration-manager"></a>Opciones de configuración de roles de sistema de sitio para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

La mayoría de las opciones de configuración de los roles de sistema de sitio de System Center Configuration Manager son explicativas o se explican en los cuadros de diálogo o el asistente durante la configuración.  Las secciones siguientes contienen detalles de los roles de sistema de sitio que tienen opciones que exigen información adicional.  

##  <a name="a-namebkmkapplicationcatalogwebsitea-application-catalog-website-point"></a><a name="BKMK_ApplicationCatalog_Website"></a> Punto de sitios web del catálogo de aplicaciones  
 Para más información sobre la configuración del punto de sitios web del catálogo de aplicaciones, vea [Planear y configurar la administración de aplicaciones en Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **Conexiones de cliente**  

 Seleccione **HTTPS** para conectarse mediante la opción más segura y para determinar si los clientes se conectan desde Internet. Esta opción requiere un certificado PKI en el servidor para la autenticación del servidor en los clientes y para el cifrado de datos mediante capa de sockets seguros (SSL). Para más información sobre los requisitos de certificados, vea [Requisitos de certificados PKI para Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para ver un ejemplo de implementación del certificado de servidor y obtener información sobre cómo configurarlo en Internet Information Services (IIS), vea la sección *Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS* del tema [Ejemplo paso a paso de implementación de los certificados PKI para Configuration Manager: Entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

 **Agregar sitio web del catálogo de aplicaciones a la zona de sitios de confianza**  

 Este mensaje muestra el valor de la configuración de cliente predeterminada si el parámetro **Agregar sitio web predeterminado del catálogo de aplicaciones a una zona de sitios de confianza de Internet Explorer** está establecido actualmente en **VERDADERO** o **FALSO**. Si ha configurado este parámetro mediante configuración de cliente personalizada, deberá comprobar este valor.  

 Si este sistema de sitio está configurado para un FQDN y el sitio web no se encuentra en la zona de sitios de confianza de Internet Explorer, se le solicitará a los usuarios credenciales cuando se conecten al catálogo de aplicaciones.  

 **Nombre de la organización**  

 Escriba el nombre que los usuarios ven en el catálogo de aplicaciones. Esta información de personalización ayuda a los usuarios identificar este sitio web como una fuente de confianza.  

##  <a name="a-namebkmkapplicationcatalogwebservicea-application-catalog-web-service-point"></a><a name="BKMK_ApplicationCatalog_WebService"></a> Punto de servicio web del catálogo de aplicaciones  
 Para más información sobre la configuración del punto de servicio web del catálogo de aplicaciones, vea [Planear y configurar la administración de aplicaciones en Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **HTTPS**  

 Seleccione **HTTPS** para autenticar los puntos de sitios web del catálogo de aplicaciones en este punto de servicio web del catálogo de aplicaciones.  Esta opción requiere un certificado PKI en los servidores que ejecutan el punto de sitios web del catálogo de aplicaciones para la autenticación de servidor y para el cifrado de datos a través de SSL. Para más información sobre los requisitos de certificados, vea [Requisitos de certificados PKI para Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para ver un ejemplo de implementación del certificado de servidor y obtener información sobre cómo configurarlo en IIS, vea la sección *Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS* del tema [Ejemplo paso a paso de implementación de los certificados PKI para Configuration Manager: Entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="a-namebkmkcertificateregistrationpointa-certificate-registration-point"></a><a name="BKMK_CertificateRegistrationPoint"></a> Punto de registro de certificado  
 Para más información sobre cómo configurar el punto de registro de certificados, vea [Introducción a perfiles de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

##  <a name="a-namebkmkdistributionpointa-distribution-point"></a><a name="BKMK_Distribution_Point"></a> Punto de distribución  
 Para más información sobre cómo configurar el punto de distribución para la implementación de contenido, vea [Manage content and content infrastructure for System Center Configuration Manager (Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager)](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Para más información sobre cómo configurar el punto de distribución para las implementaciones de PXE, vea [Use PXE to deploy Windows over the network with System Center Configuration Manager (Usar PXE para implementar Windows a través de la red con System Center Configuration Manager)](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Para más información sobre cómo configurar el punto de distribución para las implementaciones de multidifusión, vea [Use multicast to deploy Windows over the network with System Center Configuration Manager (Usar multidifusión para implementar Windows a través de la red con System Center Configuration Manager)](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 **Instalar y configurar IIS si lo requiere Configuration Manager**  

 Seleccione esta opción para permitir que Configuration Manager instale y configure IIS en el sistema de sitio, si aún no está instalado. IIS debe estar instalado en todos los puntos de distribución, por lo que debe seleccionar esta opción para continuar con el asistente.  

 **Cuenta de instalación de sistema de sitio**  

 Para los puntos de distribución que se instalan en un servidor del sitio, la cuenta de equipo del servidor del sitio se puede usar como la cuenta de instalación de sistema del sitio.  

 **Crear un certificado autofirmado o importar un certificado de cliente PKI**  

 Este certificado tiene dos propósitos:  

1.  Autentica el punto de distribución en un punto de administración antes de que el punto de distribución envíe mensajes de estado.  

2.  Cuando se ha seleccionado **Habilitar compatibilidad de PXE para clientes**, el certificado se envía a equipos con arranque PXE para que puedan conectarse a un punto de administración durante la implementación del sistema operativo.  

Cuando se configuran todos los puntos de administración del sitio para HTTP, debe crear un certificado autofirmado. Cuando se configuran los puntos de administración para HTTPS, debe importar un certificado de cliente PKI.  

Para importar el certificado, busque un archivo Public-Key Cryptography Standards #12 (PKCS #12) que contenga un certificado PKI con los requisitos siguientes para Configuration Manager:  

-   El uso previsto debe incluir autenticación de cliente.  

-   La clave privada debe configurarse para ser exportada.  

No hay requisitos específicos para el nombre de sujeto del certificado o el nombre alternativo de asunto (SAN), y puede utilizar el mismo certificado para varios puntos de distribución.  

Para más información sobre los requisitos de certificados, vea [Requisitos de certificados PKI para Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md). Para ver una implementación de ejemplo de este certificado, vea la sección *Implementación del certificado de cliente para puntos de distribución* del tema [Ejemplo paso a paso de implementación de los certificados PKI para Configuration Manager: Entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

**Habilitar este punto de distribución para contenido preconfigurado**  

Active esta casilla de verificación para habilitar el punto de distribución para contenido preconfigurado. Cuando se selecciona esta casilla de verificación, puede configurar el comportamiento de distribución a la hora de distribuir contenido. Puede elegir entre preconfigurar siempre el contenido en el punto de distribución, preconfigurar el contenido inicial para el paquete, pero usar el proceso de distribución de contenido normal cuando hay actualizaciones en el contenido, o usar siempre el proceso de distribución de contenido normal para el contenido en el paquete.  

**Grupos de límites**  

 Puede asociar grupos de límites a un punto de distribución. Durante la distribución de contenido, los clientes deben estar en un grupo de límites que esté asociado con el punto de distribución para utilizarlo como una ubicación de origen para el contenido. Puede seleccionar la casilla **Permitir ubicación de origen de reserva para contenido** para permitir a los clientes que están fuera de estos grupos de límites que reviertan y usen el punto de distribución como una ubicación de origen para el contenido cuando no estén disponibles otros puntos de distribución.  

##  <a name="a-namebkmkenrollmentpointa-enrollment-point"></a><a name="BKMK_Enrollment_Point"></a> Punto de inscripción  
Los puntos de inscripción se usan para instalar equipos Mac e inscribir dispositivos administrados por medio de la administración local de dispositivos móviles. Para obtener más información, consulte:  

-   [Cómo instalar clientes en equipos Mac en Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md)  

-   [How users enroll devices with On-premises Mobile Device Management in System Center Configuration Manager (Cómo inscriben los usuarios dispositivos con la administración local de dispositivos móviles en System Center Configuration Manager)](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

**Conexiones permitidas**  

 La opción HTTPS se selecciona automáticamente y requiere un certificado PKI en el servidor para la autenticación de servidor en el punto proxy de inscripción y el punto de servicio de fuera de banda, y para el cifrado de datos mediante SSL. Para más información sobre los requisitos de certificados, vea [Requisitos de certificados PKI para Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para ver un ejemplo de implementación del certificado de servidor y obtener información sobre cómo configurarlo en IIS, vea la sección *Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS* del tema [Ejemplo paso a paso de implementación de los certificados PKI para Configuration Manager: Entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="a-namebkmkenrollmentproxypointa-enrollment-proxy-point"></a><a name="BKMK_Enrollment_Proxy_Point"></a> Punto de proxy de inscripción  
Para más información sobre cómo configurar un punto de proxy de inscripción para dispositivos móviles, vea [How users enroll devices with On-premises Mobile Device Management in System Center Configuration Manager (Cómo inscriben los usuarios dispositivos con la administración local de dispositivos móviles en System Center Configuration Manager)](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

**Conexiones de cliente**  

 La opción HTTPS se selecciona automáticamente y necesita un certificado PKI en el servidor para la autenticación de servidor en dispositivos móviles y equipos Mac inscritos por Configuration Manager, y para el cifrado de datos a través de capa de sockets seguros (SSL). Para más información sobre los requisitos de certificados, vea [Requisitos de certificados PKI para Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para ver un ejemplo de implementación del certificado de servidor y obtener información sobre cómo configurarlo en IIS, vea la sección *Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS* del tema [Ejemplo paso a paso de implementación de los certificados PKI para Configuration Manager: Entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="a-namebkmkfallbackstatuspointa-fallback-status-point"></a><a name="BKMK_Fallback_Status_Point"></a> Punto de estado de reserva  
**Número de mensajes de estado** e **Intervalo de limitación (en segundos)**  

Aunque la configuración predeterminada para estas opciones (10.000 mensajes de estado y 3.600 segundos para el intervalo de limitación) son suficientes para la mayoría de las circunstancias, es posible que tenga que cambiarla cuando se cumplen las condiciones siguientes:  

-   El punto de estado de reserva sólo acepta conexiones desde la intranet.  

-   Se usa el punto de estado de reserva durante una ejecución de la implementación de cliente en muchos equipos.  

En este escenario, un flujo continuo de mensajes de estado puede crear una acumulación de mensajes de estado que provoque un uso elevado de la unidad central de procesamiento  (CPU) en el servidor de sitio durante un periodo de tiempo prolongado. Además, puede que no vea la información actualizada sobre la implementación de cliente en la consola de Configuration Manager y en los informes de implementación de cliente.  

Esta configuración de punto de estado de reserva está diseñada para ser configurada para mensajes de estado que se generan durante la implementación de cliente. La configuración no está diseñada para ser configurada para problemas de comunicación del cliente, por ejemplo, cuando los clientes de Internet no se pueden conectar a su punto de administración basado en Internet. Debido a que el punto de estado de reserva no puede aplicar esta configuración solo a los mensajes de estado generados durante la implementación de cliente, no aplique esta configuración cuando el punto de estado de reserva acepte conexiones de Internet.  

Cada equipo que instala correctamente el cliente de System Center 2012 Configuration Manager envía los cuatro mensajes de estado siguientes al punto de estado de reserva:  

-   Implementación de cliente iniciada  

-   Implementación de cliente con éxito  

-   Se inició la asignación de cliente  

-   Asignación de cliente con éxito  

Los equipos que no se puedan instalar o no puedan asignar el cliente de Configuration Manager envían mensajes de estado adicionales.  

Por ejemplo, si implementa el cliente de Configuration Manager en 20.000 equipos, la implementación podría crear 80.000 mensajes de estado enviados al punto de estado de reserva. Como la configuración de limitación predeterminada permite el envío de 10.000 mensajes de estado al punto de estado de reserva cada 3.600 segundos (1 hora), es posible que los mensajes de estado se acumulen en el punto de estado de reserva debido a la configuración de limitación. También debe considerar el ancho de red disponible entre el punto de estado de reserva y el servidor de sitio, y la capacidad de procesamiento del servidor de sitio para procesar muchos mensajes de estado.  

Para intentar evitar estos problemas, considere la posibilidad de aumentar el número de mensajes de estado y disminuir el intervalo de limitación.  

Restablezca los valores de limitación para el punto de estado de reserva si se cumple alguna de las siguientes condiciones:  

-   Calcula que los valores de limitación actuales son más altos de lo necesario para procesar mensajes de estado desde el punto de estado de reserva.  

-   Detecta que la configuración de limitación actual crea un uso intensivo de la CPU en el servidor del sitio.  

No cambie la configuración de limitación de punto de estado de reserva a menos que entienda las consecuencias. Por ejemplo, si aumenta demasiado la configuración de limitación, el uso de CPU en el servidor de sitio puede aumentar también en exceso, lo cual ralentiza todas las operaciones del sitio.  



<!--HONumber=Nov16_HO1-->


