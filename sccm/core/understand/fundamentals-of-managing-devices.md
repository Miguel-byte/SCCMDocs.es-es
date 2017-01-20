---
title: "Aspectos básicos de la administración de dispositivos | System Center Configuration Manager"
description: "Obtenga información sobre cómo usar System Center Configuration Manager para administrar dispositivos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: 6
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f4d39f31723711a7f5ec2b1aa39e81d3a3188029


---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>Fundamentos de la administración de dispositivos con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

System Center Configuration Manager puede administrar dos amplias categorías de dispositivos.

La primera, los **clientes**, son dispositivos tales como estaciones de trabajo, equipos portátiles, servidores y dispositivos móviles, que tienen el software cliente de Configuration Manager instalado para que los pueda administrar.   

La segunda, los **dispositivos administrados**, pueden incluir clientes, pero normalmente hace referencia a dispositivos móviles que no instalan el software cliente de Configuration Manager y que se administran mediante Microsoft Intune o a través de la administración local integrada de dispositivos móviles de Configuration Manager.

Además de administrar dispositivos con o sin el cliente de Configuration Manager, puede usar una administración centrada en el usuario para ayudar a agrupar e identificar los dispositivos administrados.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Administración de dispositivos con el cliente de Configuration Manager

 La administración de clientes incluye operaciones como recopilación del inventario de hardware o software de los dispositivos, instalación de nuevo software en un dispositivo, definición de la configuración que informa del cumplimiento o la aplicación de cumplimiento a una determinada configuración. Algunas funciones de administración, como el inventario de hardware, requieren que el dispositivo ejecute el software cliente de Configuration Manager. Otras operaciones, como la instalación (implementación) de software en un dispositivo, se admiten en todos los dispositivos administrados.  

 Para administrar un dispositivo mediante el software cliente de Configuration Manager, tiene que detectar el dispositivo en la red y luego implementar (instalar) el software cliente en ese dispositivo, o bien instalar manualmente el software cliente en un nuevo equipo y hacer que ese equipo se una a su sitio cuando se una a la red. Para detectar dispositivos que aún no tienen instalado software cliente, ejecute uno o varios de los métodos de detección integrados. Después de que se detecta un dispositivo, puede usar varios métodos para instalar el software cliente. Para obtener información sobre la detección, consulte [Ejecutar la detección para System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

 Después de detectar los dispositivos que pueden ejecutar el software cliente de Configuration Manager, puede usar varios métodos para instalarlo. Cuando se haya instalado el software y se haya asignado el cliente a un sitio principal, puede comenzar a administrar el dispositivo.  Los métodos de instalación comunes son: instalación de inserción de cliente, instalación basada en una actualización de software mediante directiva de grupo, instalación manual en un equipo o incorporación del cliente como parte de una imagen del sistema operativo que se implemente.  

 Después de instalar el cliente, puede simplificar las tareas de administración de dispositivos mediante el uso de colecciones. Las recopilaciones son grupos lógicos de dispositivos o usuarios que se crean para poder realizar las tareas de administración en varios dispositivos que comparten un conjunto común de criterios. Por ejemplo, es posible que quiera instalar una aplicación de dispositivo móvil en todos los dispositivos móviles inscritos por Configuration Manager. Si es así, podría utilizar la recopilación **Todos los dispositivos móviles** , que excluye automáticamente los equipos. Puede crear sus propias recopilaciones para agrupar de forma lógica los dispositivos que administra, según sus requisitos empresariales.  

 Para más información, consulte los temas siguientes:  

-   [Elegir una solución de administración de dispositivos para System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  

-   [Métodos de instalación de cliente en System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [Introducción a las recopilaciones en System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Configuración de cliente  
 Cuando instala Configuration Manager por primera vez, todos los clientes de la jerarquía se configuran mediante la configuración de cliente predeterminada, que se puede cambiar. Esta configuración de cliente incluye opciones de configuración, como la frecuencia de comunicación de los dispositivos con el sitio, la posibilidad de habilitar o no al cliente para las actualizaciones de software y otras operaciones de administración y la inscripción por parte de los usuarios de sus dispositivos móviles para que sean administrados por Configuration Manager.  

 Si necesita una configuración de cliente diferente para grupos de usuarios o dispositivos, puede crear una configuración de cliente personalizada y después asignarlos a las recopilaciones.  Los miembros de la recopilación están configurados para tener los valores personalizados y puede crear varias configuraciones de cliente personalizadas que se apliquen en el orden especificado (por orden numérico).  En caso de conflicto, la configuración que tenga el número de orden más bajo invalida al resto de configuraciones.  

 En el diagrama siguiente se muestra un ejemplo de creación y aplicación de una configuración de cliente personalizada.  

 ![Configuración de cliente](media/ClientSettings.gif)  

 Para más información sobre la configuración de cliente, consulte  
                [Cómo configurar el cliente en System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) y [Acerca de la configuración de cliente en System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>Administración de dispositivos sin el cliente de Configuration Manager  
 Configuration Manager admite la administración de algunos dispositivos que no tienen instalado el software cliente y que no están administrados mediante la interacción con Microsoft Intune. Para obtener más información, consulte [Administrar dispositivos móviles con la infraestructura local en System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) y [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-centric-management"></a>Administración centrada en el usuario  
 Además de las recopilaciones para dispositivos, también existen recopilaciones de usuarios que contienen usuarios de Servicios de dominio de Active Directory. Cuando se utiliza una recopilación de usuarios, puede instalar software en todos los equipos en los que los miembros de la recopilación inicien sesión y configurar la **afinidad entre usuario y dispositivo** de forma que el software que implemente se instale únicamente en los dispositivos especificados como dispositivo principal de un usuario. Estos dispositivos principales se denominan dispositivos primarios. Un usuario puede tener uno o más dispositivos principales.  

 Uno de los métodos que pueden usar los usuarios para controlar su experiencia de implementación de software es mediante el uso de la interfaz de cliente de equipo, **Centro de software**. Centro de software se instala automáticamente en los equipos cliente y su acceso se obtiene desde el menú de inicio de los usuarios. Centro de software permite que los usuarios administren su propio software, así como realizar las siguiente operaciones:  

-   Instalar software  

-   Programar software para su instalación automática fuera del horario laboral  

-   Configurar cuándo puede instalar Configuration Manager software en su dispositivo  

-   Configurar opciones de acceso para el control remoto si este está habilitado en Configuration Manager  

-   Configurar opciones de administración de energía, si un usuario administrativo lo ha habilitado  

 A través de un vínculo en el Centro de software, los usuarios pueden conectarse al **Catálogo de aplicaciones**, donde pueden buscar, instalar y solicitar software. Además, el catálogo de aplicaciones permite a los usuarios configurar algunas opciones de preferencia, borrar sus dispositivos móviles y (si se permite esta configuración) especificar sus propios dispositivos principales para la afinidad entre usuario y dispositivo. Entre otros métodos de configuración de la información de afinidad entre usuario y dispositivo se incluyen la importación de la información desde un archivo y la generación automática de datos de uso.  

 Dado que el catálogo de aplicaciones es un sitio web hospedado en IIS, los usuarios también pueden tener acceso a él directamente desde un explorador, desde la intranet o desde Internet.  



<!--HONumber=Nov16_HO1-->


