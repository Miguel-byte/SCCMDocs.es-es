---
title: Roles de sistema de sitio para clientes
titleSuffix: Configuration Manager
description: Determine roles de sistema de sitio para los clientes en System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eac38757ed2147d664b3bdbf2f7e0eb11947dcac
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334082"
---
# <a name="determine-the-site-system-roles-for-system-center-configuration-manager-clients"></a>Determinar los roles de sistema de sitio para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Este tema puede ayudarle a determinar los roles del sistema de sitio que necesita para implementar clientes de Configuration Manager:  

 Para obtener más información sobre dónde instalar los roles de sistema de sitio necesarios en la jerarquía, consulte [Design a hierarchy of sites for System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md) (Diseñar una jerarquía de sitios para System Center Configuration Manager).  

 Para obtener más información sobre cómo instalar y configurar los roles de sistema de sitio necesarios, consulte [Install site system roles](../../../../core/servers/deploy/configure/install-site-system-roles.md) (Instalar roles de sistema de sitio).  

##  <a name="determine-if-you-need-a-management-point"></a>Determinar si necesita un punto de administración  
 De forma predeterminada, todos los equipos cliente de Windows usan un punto de distribución para instalar el cliente de Configuration Manager y pueden revertir a un punto de administración cuando un punto de distribución no está disponible. Pero puede instalar clientes de Windows en equipos de otro origen mediante la propiedad de línea de comandos de CCMSetup **/source:<ruta\>**. Por ejemplo, podría hacer esto si instala clientes en Internet. Otro escenario es el que se produce cuando intenta evitar el envío de paquetes de red entre el equipo y el punto de administración durante la instalación del cliente, quizás porque un firewall bloquea los puertos necesarios o porque dispone de una conexión de ancho de banda bajo. Pero todos los clientes deben comunicarse con un punto de administración para asignarse a un sitio y para que Configuration Manager los administre.  

 Para obtener más información sobre la propiedad de línea de comandos de CCMSetup **/source:<ruta\>**, consulte [About client installation properties in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md) (Acerca de las propiedades de instalación de clientes en Configuración Manager).  

 Cuando se instala más de un punto de administración de la jerarquía, los clientes se conectan automáticamente a un punto, según su ubicación de red y la pertenencia al bosque. No se puede instalar más de un punto de administración en un sitio secundario.  

 Los clientes de equipos Mac y los clientes de dispositivos móviles inscritos con Configuration Manager siempre requieren un punto de administración para la instalación de cliente. Este punto de administración debe estar en un sitio primario, debe estar configurado para admitir dispositivos móviles y debe aceptar conexiones de clientes desde Internet. Estos clientes no pueden utilizar puntos de administración en sitios secundarios o conectarse a puntos de administración de otros sitios primarios.  

##  <a name="determine-if-you-need-a-fallback-status-point"></a>Determinar si necesita un punto de estado de reserva  
 Puede utilizar un punto de estado de reserva para supervisar la implementación del cliente para equipos de Windows. También puede identificar los clientes de equipos de Windows que no están administrados porque no se pueden comunicar con un punto de administración. Los equipos Mac, los dispositivos móviles inscritos por Configuration Manager y los dispositivos móviles administrados mediante el conector de Exchange Server no usan un punto de estado de reserva.  

 Un punto de estado de reserva no es necesario para supervisar la actividad y el estado del cliente.  

 El punto de estado de reserva siempre se comunica con los clientes mediante HTTP, que utiliza conexiones no autenticadas y envía los datos en texto no cifrado. Esto hace que el punto de estado de reserva sea vulnerable a un ataque, especialmente cuando se utiliza con la administración de clientes basada en Internet. Para reducir la superficie expuesta a ataques, dedique siempre un servidor para ejecutar el punto de estado de reserva y en un entorno de producción no instale otros roles de sistema de sitio en el mismo servidor.  

 Instale un punto de estado de reserva si se cumple todo lo siguiente:  

-   Desea que los errores de comunicación de cliente de los equipos Windows se envíen al sitio, aunque estos equipos cliente no puedan comunicarse con un punto de administración.  

-   Quiere usar los informes de implementación de cliente de Configuration Manager, que muestran los datos que envía el punto de estado de reserva.  

-   Dispone de un servidor dedicado para este rol de sistema de sitio y de medidas de seguridad adicionales para ayudar a proteger el servidor contra los ataques.  

-   Las ventajas de utilizar un punto de estado de reserva son mayores que los riesgos de seguridad asociados con conexiones no autenticadas y transferencias de texto no cifrado sobre tráfico HTTP.  

 No instale un punto de estado de reserva si los riesgos de seguridad de la ejecución de un sitio web con conexiones no autenticadas y transferencias de texto no cifrado superan a las ventajas de identificar problemas de comunicación de clientes.  

##  <a name="determine-whether-you-need-a-reporting-services-point"></a>Determinar si necesita un punto de servicios de informes  
 Configuration Manager proporciona muchos informes para ayudarle a supervisar la instalación, asignación y administración de clientes en la consola de Configuration Manager. Algunos de los informes de implementación de cliente requieren que los clientes se asignen a un punto de estado de reserva.  

 Aunque los informes no son necesarios para implementar clientes y es posible ver parte de la información de implementación en la consola de Configuration Manager o usar los archivos de registro de cliente para obtener información detallada, los informes de cliente proporcionan información valiosa para ayudarle a supervisar y solucionar problemas relacionados con la implementación de clientes.  

##  <a name="determine-if-you-need-an-enrollment-point-and-an-enrollment-proxy-point"></a>Determinar si necesita un punto de inscripción y un punto de proxy de inscripción  
 Configuration Manager requiere el punto de inscripción y el punto de proxy de inscripción para inscribir dispositivos móviles y certificados para equipos Mac. Estos roles de sistema de sitio no son necesarios si va a administrar dispositivos móviles mediante el conector de Exchange Server, o si instala el cliente heredado de dispositivo móvil (por ejemplo, para Windows CE) o solicita e instala el certificado de cliente en equipos Mac independientemente de Configuration Manager.  

##  <a name="determine-if-you-need-a-distribution-point"></a>Determinar si necesita un punto de distribución  
 No es necesario un punto de distribución para instalar clientes de Configuration Manager en equipos de Windows. Sin embargo, de forma predeterminada, Configuration Manager usa de forma predeterminada un punto de distribución para instalar los archivos de origen de cliente en equipos Windows, pero puede revertir para descargar estos archivos desde un punto de administración. Los puntos de distribución no se usan para instalar clientes de dispositivos móviles inscritos por Configuration Manager, pero se usan para instalar el cliente heredado de dispositivo móvil. Si instala el cliente de Configuration Manager como parte de una implementación de sistema operativo, la imagen del sistema operativo se almacena y recupera desde un punto de distribución.  

 Aunque es posible que no sean necesarios puntos de distribución para instalar la mayoría de los clientes de Configuration Manager, serán necesarios para instalar software como aplicaciones y actualizaciones de software en los clientes.  

##  <a name="determine-if-you-need-an-application-catalog-website-point-and-an-application-catalog-web-services-point"></a>Determinar si necesita un punto de sitios web del catálogo de aplicaciones y un punto de servicios web del catálogo de aplicaciones  
 El punto de sitios web del catálogo de aplicaciones y el punto de servicios web del catálogo de aplicaciones no son necesarios para la implementación del cliente. Pero es posible que quiera instalarlos como parte de su proceso de implementación de cliente para que los usuarios puedan realizar las acciones siguientes tan pronto como el cliente de Configuration Manager se instale en los equipos Windows:  

-   Borrar sus dispositivos móviles.  

-   Buscar e instalar aplicaciones desde el catálogo de aplicaciones.  

-   Implemente las aplicaciones en los usuarios y los dispositivos con un propósito de implementación **Disponible**.  

##  <a name="determine-whether-you-require-a-cloud-management-gateway-connector-point"></a>Determinar si necesita un punto del conector de puerta de enlace de administración en la nube 

Necesita un punto de conector de puerta de enlace de administración en la nube si está configurando una [puerta de enlace de administración en la nube](/sccm/core/clients/manage/setup-cloud-management-gateway) para [administrar clientes en Internet](/sccm/core/clients/manage/manage-clients-internet).


 