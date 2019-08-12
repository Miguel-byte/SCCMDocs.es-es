---
title: Opciones de rol de sistema de sitio
titleSuffix: Configuration Manager
description: Lea este artículo para obtener detalles sobre los roles de sistema de sitio de Configuration Manager que no son necesariamente explicativos.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 10689b4ae50b06f07516f50041e42a4871fa6bcf
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536578"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Opciones de configuración de roles de sistema de sitio para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La mayoría de las opciones de configuración de los roles de sistema de sitio de Configuration Manager son explicativas o se explican en los cuadros de diálogo o el asistente durante la configuración. En las secciones siguientes se explican los roles de sistema de sitio en los que se necesita información adicional para su configuración.  


## <a name="BKMK_ApplicationCatalog_Website"></a> Punto de sitios web del catálogo de aplicaciones  

> [!Important]
> La experiencia del usuario de Silverlight del catálogo de aplicaciones no se admite a partir de la versión 1806 de la rama actual. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones. En la primera versión de la rama actual después del 31 de octubre de 2019, finalizará el soporte técnico para los roles de catálogo de aplicaciones.  
>
> Vea los siguientes artículos para más información:
>
> - [Configurar el Centro de software](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)
> - [Características eliminadas y en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)  

Para más información sobre cómo configurar el punto de sitios web del catálogo de aplicaciones, vea [Planear y configurar la administración de aplicaciones](/sccm/apps/plan-design/plan-for-and-configure-application-management).  


## <a name="BKMK_ApplicationCatalog_WebService"></a> Punto de servicio web del catálogo de aplicaciones  

> [!Important]
> La experiencia del usuario de Silverlight del catálogo de aplicaciones no se admite a partir de la versión 1806 de la rama actual. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones. En la primera versión de la rama actual después del 31 de octubre de 2019, finalizará el soporte técnico para los roles de catálogo de aplicaciones.  
>
> Vea los siguientes artículos para más información:
>
> - [Configurar el Centro de software](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)
> - [Características eliminadas y en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)  

Para más información sobre cómo configurar el punto de servicio web del catálogo de aplicaciones, vea [Planear y configurar la administración de aplicaciones](/sccm/apps/plan-design/plan-for-and-configure-application-management).  


## <a name="BKMK_CertificateRegistrationPoint"></a> Punto de registro de certificados  

Para más información sobre cómo configurar el punto de registro de certificado, vea [Introducción a perfiles de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  


## <a name="BKMK_Distribution_Point"></a> Punto de distribución  

Para más información sobre cómo configurar el punto de distribución para la distribución de contenido, vea [Administración del contenido y de la infraestructura de contenido](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

Para más información sobre cómo configurar el punto de distribución para las implementaciones de entornos PXE, vea [Usar PXE para implementar Windows a través de la red](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  

Para más información sobre cómo configurar el punto de distribución para implementaciones de multidifusión, vea [Usar multidifusión para implementar Windows a través de la red](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).  

### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>Instalar y configurar IIS si lo requiere Configuration Manager

Seleccione esta opción para permitir que Configuration Manager instale y configure IIS en el sistema de sitio (si aún no está instalado). IIS debe estar instalado en todos los puntos de distribución, por lo que debe seleccionar esta opción para continuar con el asistente.  

### <a name="site-system-installation-account"></a>Cuenta de instalación del sistema de sitio

Para los puntos de distribución que se instalan en un servidor del sitio, la cuenta de equipo del servidor del sitio se puede usar como la cuenta de instalación del sistema del sitio. Para más información, vea [Cuentas](/sccm/core/plan-design/hierarchy/accounts#site-system-installation-account).  


## <a name="BKMK_Enrollment_Point"></a> Punto de inscripción  

Los puntos de inscripción se usan para instalar equipos macOS y para inscribir dispositivos administrados con la administración de dispositivos móviles local. Vea los siguientes artículos para más información:  

- [Cómo implementar clientes en equipos Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)  

- [Cómo los usuarios inscriben dispositivos con la MDM local](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm)  

### <a name="allowed-connections"></a>Conexiones permitidas

La opción HTTPS está seleccionada automáticamente y necesita un certificado PKI en el servidor para la autenticación de servidor en el punto de proxy de inscripción, para la autenticación de servidor en el punto de servicio fuera de banda y para el cifrado de datos por SSL. Para obtener más información, vea [Requisitos de certificados PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

Para ver un ejemplo de implementación del certificado de servidor y obtener información sobre cómo configurarlo en IIS, vea [Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  


## <a name="BKMK_Enrollment_Proxy_Point"></a> Punto de proxy de inscripción  

Para más información sobre cómo configurar un punto de proxy de inscripción para dispositivos móviles, vea [Cómo inscriben dispositivos los usuarios mediante la administración de dispositivos móviles (MDM) local](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm).  

### <a name="client-connections"></a>Conexiones de cliente

La opción HTTPS se selecciona automáticamente. Requiere los siguientes certificados PKI en el servidor:

- Para la autenticación de servidor en dispositivos móviles y equipos Mac que inscribe con Configuration Manager
- Para el cifrado de datos a través de la Capa de sockets seguros (SSL)

Para obtener más información sobre los requisitos de certificado, vea [Requisitos de certificados PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

Para ver un ejemplo de implementación del certificado de servidor y obtener información sobre cómo configurarlo en IIS, vea [Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  


## <a name="BKMK_Fallback_Status_Point"></a> Punto de estado de reserva  

### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>Número de mensajes de estado e Intervalo de limitación (en segundos)

La configuración predeterminada para estas opciones es 10 000 mensajes de estado y 3 600 segundos para el intervalo de limitación. Aunque estas opciones son suficientes para la mayoría de los casos, es posible que deba cambiarlas cuando se cumplan las condiciones siguientes:  

- El punto de estado de reserva sólo acepta conexiones desde la intranet.  

- Se usa el punto de estado de reserva durante una ejecución de la implementación de cliente en muchos equipos.  

En este escenario, un flujo continuo de mensajes de estado podría crear una acumulación de mensajes de estado que provoque un uso elevado del procesador en el servidor de sitio durante un período de tiempo prolongado. Además, puede que no vea la información actualizada sobre la implementación de cliente en la consola de Configuration Manager y en los informes de implementación de cliente.  

Esta configuración de punto de estado de reserva se ha diseñado para que se configure para mensajes de estado generados durante una implementación de cliente. La configuración no se ha diseñado para configurarla para problemas de comunicación de clientes (por ejemplo, cuando los clientes de Internet no se pueden conectar a su punto de administración basado en Internet). Debido a que el punto de estado de reserva no puede aplicar esta configuración solo a los mensajes de estado generados durante la implementación de cliente, no aplique esta configuración cuando el punto de estado de reserva acepte conexiones de Internet.  

Cada equipo que instala correctamente el cliente de Configuration Manager envía los cuatro mensajes de estado siguientes al punto de estado de reserva:  

- Implementación de cliente iniciada  

- Implementación de cliente con éxito  

- Se inició la asignación de cliente  

- Asignación de cliente con éxito  

Los equipos que no se puedan instalar (o que asignen el cliente de Configuration Manager) envían mensajes de estado adicionales.  

Por ejemplo, si implementa el cliente de Configuration Manager en 20.000 equipos, la implementación podría crear 80.000 mensajes de estado enviados al punto de estado de reserva. Como la configuración de límite predeterminada permite el envío de 10.000 mensajes de estado al punto de estado de reserva cada 3600 segundos (1 hora), puede que los mensajes de estado se acumulen en el punto de estado de reserva. Debe tener en cuenta el ancho de banda de red disponible entre el punto de estado de reserva y el servidor de sitio, así como la capacidad de procesamiento del servidor de sitio para procesar una gran cantidad de mensajes de estado.  

Para evitar estos problemas, puede aumentar el número de mensajes de estado y reducir el intervalo de limitación.  

Restablezca los valores de limitación para el punto de estado de reserva si se cumple alguna de las siguientes condiciones:  

- Calcula que los valores de limitación actuales son más altos de lo necesario para procesar mensajes de estado desde el punto de estado de reserva.  

- Detecta que la configuración de limitación actual crea un uso intensivo del procesador en el servidor del sitio.  

No cambie la configuración de limitación de punto de estado de reserva a menos que entienda las consecuencias. Por ejemplo, si aumenta demasiado la configuración de limitación, el uso del procesador en el servidor de sitio puede aumentar también en exceso, lo cual ralentiza todas las operaciones del sitio.  
