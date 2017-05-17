---
title: Planear roles del sistema de sitio | Microsoft Docs
description: "Tenga en cuenta los servidores y roles de sistema de sitio cuando planifique la jerarquía de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
caps.latest.revision: 11
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: a93ea730c39cce9dc46036f5aa6ece4a62679d0f
ms.openlocfilehash: 0d16d362b798c194645f987088ba8a95a7be3f19
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017


---
# <a name="plan-for-site-system-servers-and-site-system-roles-for-system-center-configuration-manager"></a>Planeamiento de servidores y roles de sistema de sitio para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Cada sitio de System Center Configuration Manager que se instala incluye un servidor de sitio que es un **servidor de sistema de sitio**. El sitio también puede incluir servidores de sistema de sitio adicionales en equipos que están alejados del servidor de sitio (equipos remotos). Los servidores de sistema de sitio (el servidor de sitio o un servidor de sistema de sitio remoto) admiten **roles de sistema de sitio**.


##  <a name="bkmk_siteservers"></a> Servidores de sistema de sitio  
 Al instalar un rol de sistema de sitio en un equipo, ese equipo se convierte en un servidor de sistema de sitio. En cada sitio puede instalar a uno o más servidores de sistema de sitio adicionales. También puede elegir no instalar servidores de sistema de sitio adicionales y ejecutar todos los roles de sistema de sitio directamente en el equipo del servidor de sitio. Cada sistema de sitio hospeda uno o varios roles de sistema de sitio. Servidores adicionales pueden contribuir a ampliar las funcionalidades y la capacidad de un sitio al compartir la carga de procesamiento de la CPU que generan los roles de sistema de sitio en un servidor.  

 Al plantearse la incorporación de un servidor de sistema de sitio, asegúrese de que el servidor cumple los requisitos previos para el uso previsto. También conviene agregarlo en una ubicación de red con ancho de banda suficiente para comunicarse con los puntos de conexión esperados, como el servidor de sitio, los recursos de dominio, una ubicación en la nube, los servidores de sistema de sitio y los clientes).  

 Si configura el servidor de sistema de sitio con un servidor proxy para su uso por los roles de sistema de sitio, vea [Roles de sistema de sitio que pueden utilizar un servidor proxy](#bkmk_proxy).  

##  <a name="bkmk_planroles"></a> Roles de sistema de sitio  
 Los roles de sistema de sitio se instalan en un equipo para proporcionar a este funcionalidades adicionales. Algunos ejemplos son:  

-   Puntos de administración adicionales para que el sitio pueda admitir más dispositivos, hasta alcanzar su capacidad máxima.  

-   Puntos de distribución adicionales para expandir la infraestructura de contenido y mejorar así el rendimiento de las distribuciones de contenido a los usuarios y dispositivos.  

-   Uno o varios roles de sistema de sitio específicos de la característica. Por ejemplo, un punto de actualización de software que le permite administrar las actualizaciones de software de los dispositivos administrados o un punto de servicios de informes que le permite ejecutar informes para supervisar y comprender la implementación o compartir información relacionada.  


Diferentes sitios de Configuration Manager pueden admitir distintos conjuntos de roles de sistema de sitio. Los roles de sistema de sitio admitidos dependen del tipo de sitio (sitio de administración central, sitio primario o sitio secundario). La topología de la jerarquía puede limitar la colocación de algunos roles en determinados tipos de sitios. Por ejemplo, el punto de conexión de servicio solo se admite en el sitio de nivel superior de la jerarquía, que podría ser un sitio de administración central o un sitio primario independiente. Este rol no se admite en un sitio principal secundario ni en los sitios secundarios.  

Una vez instalado un sitio, se puede mover la ubicación de algunos roles de sistema de sitio de su ubicación predeterminada en el servidor de sitio a otro servidor. Por ejemplo, este es el caso del punto de administración o el punto de distribución, que se instalan de manera predeterminada en un servidor de sitio primario o secundario. También puede instalar instancias adicionales de algunos roles de sistema de sitio para ampliar las funcionalidades del sitio (ofrecer más servicios a los clientes) y para cumplir sus requisitos empresariales. Algunos roles son necesarios, mientras que otros son opcionales.  

-   **Servidor de sitio de Configuration Manager.** Este rol identifica el servidor donde se ejecuta el programa de instalación de Configuration Manager para instalar un sitio o el servidor en el que se instala un sitio secundario. Este rol no se puede mover ni desinstalar hasta que se desinstale el sitio.  

-   **Sistema de sitio de Configuration Manager.** Este rol se asigna a cualquier equipo en el que se instale un sitio o un rol de sistema de sitio. Este rol no se puede mover ni desinstalar hasta que el último rol de sistema de sitio se quite del equipo.  

-   **Rol de sistema de sitio de componente de Configuration Manager.** Este rol identifica un sistema de sitio que ejecuta una instancia del servicio SMS Executive y es necesario para admitir otros roles, como los puntos de administración. Este rol no se puede mover ni desinstalar hasta que el último rol de sistema de sitio aplicable se quite del equipo.  

-   **Servidor de base de datos del sitio de Configuration Manager.** Este rol se asigna a los servidores de sistema de sitio que contienen una instancia de la base de datos del sitio en un sitio. Este rol solo se puede mover a un nuevo servidor modificando el sitio para que use otra instancia de SQL Server para hospedar la base de datos del sitio.  

-   **Proveedor de SMS.** El rol de proveedor de SMS se asigna a cada equipo que hospeda una instancia del proveedor de SMS, la interfaz entre una consola de Configuration Manager y la base de datos del sitio. De forma predeterminada, este rol se instala automáticamente en el servidor de sitio de un sitio de administración central y en sitios primarios. Puede instalar instancias adicionales para proporcionar acceso a otros usuarios administrativos.  

     Para instalar proveedores de SMS adicionales, debe ejecutar el programa de instalación de Configuration Manager en el servidor del sitio para [administrar el proveedor de SMS](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Luego puede instalar proveedores adicionales en otros equipos. Solo puede instalar una instancia de proveedor de SMS en un equipo y dicho equipo debe estar en el mismo dominio que el servidor de sitio.  

-   **Punto de servicio web del catálogo de aplicaciones.** Rol del sistema de sitio que proporciona información de software al sitio web del catálogo de aplicaciones desde la biblioteca de software. Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de él en un sitio o en varios sitios de la misma jerarquía.  

-   **Punto de sitio web del catálogo de aplicaciones.** Rol del sistema de sitio que proporciona a los usuarios una lista de software disponible desde el catálogo de aplicaciones. Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de él en un sitio o en varios sitios de la misma jerarquía.  

     Si el catálogo de aplicaciones admite equipos cliente en Internet, instale, como práctica recomendada de seguridad, el punto de sitio web del catálogo de aplicaciones en una red perimetral de seguridad y el punto de servicio web del catálogo de aplicaciones en la intranet.  

-   **Punto de sincronización de Asset Intelligence.** Rol de sistema de sitio que se conecta a Microsoft para descargar información del catálogo de Asset Intelligence. Este rol también carga títulos sin clasificar, para que se puedan tener en cuenta para su futura inclusión en el catálogo. Una jerarquía admite una sola instancia de este rol, y esa debe estar en el sitio de nivel superior de la jerarquía (un sitio de administración central o el sitio primario independiente). Si expande un sitio primario independiente a una jerarquía más grande, debe desinstalar este rol desde el sitio primario y luego instalarlo en el sitio de administración central.   Para obtener más información, consulte [Asset Intelligence en System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Punto de registro del certificados.** Rol de sistema que se comunica con un servidor que ejecute el Servicio de inscripción de dispositivos de red. Este rol administra las solicitudes de certificado de dispositivo que usan el Protocolo de inscripción de certificados simple (SCEP). Este rol solo se admite en los sitios primarios y el sitio de administración central.

     Aunque un único punto de registro de certificados puede proporcionar funcionalidad a toda una jerarquía, tal vez prefiera instalar varias instancias de este rol en un sitio y en varios sitios de la misma jerarquía. Esto puede ayudar con equilibrio de carga. Cuando existen varias instancias en una jerarquía, los clientes se asignan aleatoriamente a uno de los puntos de registro de certificado.  

     Cada punto de registro de certificado requiere acceso a una instancia independiente del Servicio de inscripción de dispositivos de red. No se pueden configurar dos o más puntos de registro de certificado para que utilicen el mismo Servicio de inscripción de dispositivos de red. Además, el punto de registro de certificados no debe instalarse en el mismo servidor que ejecuta el Servicio de inscripción de dispositivos de red.  

- **Punto de conexión de puerta de enlace de administración en la nube.** Rol de sistema de sitio para comunicarse con la [puerta de enlace de administración en la nube](/sccm/core/clients/manage/setup-cloud-management-gateway).

-   **Punto de distribución.** Rol de sistema de sitio que contiene archivos de origen para que descarguen los clientes, tales como imágenes de arranque, paquetes de software, actualizaciones de software, imágenes del sistema operativo y contenido de la aplicación. De forma predeterminada, este rol se instala en el equipo del servidor de sitio de nuevos sitios primarios y secundarios cuando se instala el sitio. Este rol no se admite en un sitio de administración central. Se pueden instalar varias instancias de este rol en un sitio admitido y en varios sitios de la misma jerarquía. Para obtener más información, consulte [Conceptos básicos de la administración de contenido en System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md), y [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   **Punto de estado de reserva.** Rol de sistema de sitio que le ayuda a supervisar la instalación del cliente e identificar a los clientes que no están administrados porque no se pueden comunicar con su punto de administración. Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de este rol en un sitio y en varios sitios de la misma jerarquía. Para obtener más información, vea [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) (Escenarios de ubicación de origen del contenido).


-   **Punto de Endpoint Protection.** Rol del sistema de sitio que Configuration Manager utiliza para aceptar los términos de la licencia de Endpoint Protection y configurar la pertenencia predeterminada a Microsoft Active Protection Service. Una jerarquía admite una sola instancia de este rol, y esa debe estar en el sitio de nivel superior de la jerarquía (un sitio de administración central o el sitio primario independiente). Si expande un sitio primario independiente a una jerarquía más grande, debe desinstalar este rol desde el sitio primario y luego instalarlo en el sitio de administración central. Para obtener más información, vea [Endpoint Protection en System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   **Punto de inscripción.** Rol de sistema de sitio que utiliza certificados PKI en Configuration Manager para inscribir dispositivos móviles y equipos Mac. Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de él en un sitio o en varios sitios de la misma jerarquía.  

     Si un usuario inscribe dispositivos móviles mediante Configuration Manager y su cuenta de Active Directory se encuentra en un bosque que no es de confianza para el bosque del servidor de sitio, debe instalarse un punto de inscripción en el bosque del usuario. Después puede autenticarse el usuario.  

-   **Punto de proxy de inscripción.** Rol del sistema de sitio que administra solicitudes de inscripción de Configuration Manager por parte de dispositivos móviles y equipos Mac. Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de él en un sitio o en varios sitios de la misma jerarquía.  

     Cuando admita dispositivos móviles en Internet, instale el punto de proxy de inscripción en una red perimetral de seguridad y el punto de inscripción en la intranet.  

-   **Conector de Exchange Server.** Para obtener información sobre este rol, vea [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

-   **Punto de administración.** Rol del sistema de sitio que proporciona a los clientes información de ubicación de servicio y de directiva y recibe datos de configuración de los clientes.  

    De forma predeterminada, este rol se instala en el equipo del servidor de sitio de nuevos sitios primarios y secundarios cuando se instala el sitio. Los sitios primarios admiten varias instancias de este rol. Los sitios secundarios admiten un único punto de administración para proporcionar un punto de contacto local para que los clientes obtengan directivas de usuario y equipo (un punto de administración en un sitio secundario se conoce como un punto de administración de proxy).  

     Los puntos de administración se pueden configurar para admitir HTTP o HTTPs, así como compatibilidad con dispositivos móviles que se administren con la administración local de dispositivos móviles de System Center Configuration Manager. Puede utilizar [Réplicas de bases de datos para puntos de administración de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) para reducir la carga de CPU que los puntos de administración ejercen sobre el servidor de base de datos del sitio mientras atienden las solicitudes de servicio de los clientes.  

-   **Punto de servicios de informes.** Rol de sistema de sitio que se integra con SQL Server Reporting Services para crear y administrar informes para Configuration Manager. Este rol se admite en sitios primarios y en el sitio de administración central. Se pueden instalar varias instancias de él en un sitio admitido. Para obtener más información, consulte [Planeamiento de informes en System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md).  

-   **Punto de conexión de servicio.** Rol de sistema de sitio que se usa para administrar dispositivos móviles con Microsoft Intune y MDM local. Este rol también carga los datos de uso del sitio y es necesario para realizar las actualizaciones de Configuration Manager disponibles en la consola de Configuration Manager. Una jerarquía admite una sola instancia de este rol, y esa debe estar en el sitio de nivel superior de la jerarquía (un sitio de administración central o el sitio primario independiente). Si expande un sitio primario independiente a una jerarquía más grande, debe desinstalar este rol desde el sitio primario y luego instalarlo en el sitio de administración central. Para obtener más información, consulte [Acerca del punto de conexión de servicio en System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   **Punto de actualización de software.** Rol de sistema de sitio que se integra con Windows Server Update Services (WSUS) para proporcionar actualizaciones de software a los clientes de Configuration Manager. Este rol se admite en todos los sitios:  

    -   Instale este sistema de sitio en el sitio de administración central para la sincronización con WSUS.  

    -   Configure cada instancia de este rol en sitios primarios secundarios para la sincronización con el sitio de administración central.  

    -   Considere también la posibilidad de instalar un punto de actualización de software en sitios secundarios cuando la transferencia de datos a través de la red sea lenta.  

    Para obtener más información, consulte [Planear las actualizaciones de software en System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

-   **Punto de migración de estado.** Rol de sistema de sitio que almacena datos de estado de usuario cuando se migra un equipo a un nuevo sistema operativo. Este rol se admite en sitios primarios y sitios secundarios. Se pueden instalar varias instancias de este rol en un sitio y en varios sitios de la misma jerarquía. Para obtener más información sobre cómo almacenar el estado de usuario al implementar sistemas operativos, consulte [Administrar el estado de usuario en System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   **Punto de Validador de mantenimiento del sistema.** Aunque este rol de sistema de sitio permanece visible en la consola de Configuration Manager,ya no se utiliza.  

###  <a name="bkmk_proxy"></a> Roles de sistema de sitio que pueden utilizar un servidor proxy  
 Algunos roles de sistema de sitio de Configuration Manager requieren conexiones a Internet y usarán un servidor proxy cuando se configure uno para el servidor de sistema de sitio que hospeda el rol. Normalmente, esta conexión se realiza en el contexto del **sistema** del equipo donde está instalado el rol de sistema de sitio. La conexión no puede utilizar una configuración de proxy para cuentas de usuario habituales. Cuando se requiera un servidor proxy para realizar una conexión a Internet, debe configurar el equipo para ello:  

-   Puede configurar un servidor proxy al instalar un rol de sistema de sitio.  

-   Puede agregar o modificar una configuración de servidor proxy cuando use la consola de Configuration Manager.  

-   Se usa la misma configuración de servidor proxy para todos los roles de sistema de sitio en un servidor de sistema de sitio que pueda usar una configuración de este tipo. Si necesita roles de sistema de sitio diferentes para utilizar servidores proxy distintos, debe instalar los roles de sistema de sitio en equipos de servidor de sistema de sitio diferentes.  

-   Si modifica la configuración de servidor proxy o instala un nuevo rol de sistema de sitio en un equipo que ya tiene una, la nueva configuración sobrescribe la configuración original.  


Para obtener los procedimientos sobre configuración del servidor proxy para roles de sistema de sitio, vea el tema [Agregar roles de sistema de sitio para System Center Configuration Manager](../../../core/servers/deploy/configure/add-site-system-roles.md).  

Los siguientes son roles de sistema de sitio que pueden utilizar un servidor proxy:  

-   **Punto de sincronización de Asset Intelligence.** Este rol de sistema de sitio se conecta a Microsoft y usa una configuración de servidor proxy en el equipo que hospeda el punto de sincronización de Asset Intelligence.  

-   **punto de distribución basado en la nube.** Cuando use un punto de distribución basado en la nube, el sitio primario que administra el punto de distribución basado en la nube debe poder conectarse a Microsoft Azure para aprovisionar, supervisar y distribuir contenido en el punto de distribución. Si se necesita un servidor proxy para esta conexión, debe configurar el servidor proxy en el servidor del sitio primario. No se puede configurar un servidor proxy en el punto de distribución basado en la nube de Azure. Para obtener más información, vea la sección [Configurar parámetros proxy para sitios primarios que administran servicios en la nube](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#BKMK_ConfigProxyforCloud) en el tema [Instalar puntos de distribución basados en la nube en Microsoft Azure para System Center Configuration Manager](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).  

-   **Conector de Exchange Server.** Este rol de sistema de sitio se conecta a Exchange Server y usa una configuración de servidor proxy en el equipo que hospeda el conector de Exchange Server.  

-   **Punto de actualización de software.** Este rol de sistema de sitio puede requerir conexiones a Microsoft Update para descargar revisiones y sincronizar la información sobre las actualizaciones. Normalmente, cuando se configura el servidor proxy, cada rol de sistema de sitio en ese equipo que admite el uso del servidor proxy utiliza el servidor proxy. No se requiere ninguna configuración adicional. Una excepción a esto es el punto de actualización de software. De forma predeterminada, un punto de actualización de software no utiliza un servidor proxy disponible a menos que también se habiliten las siguientes opciones al configurar el punto de actualización de software:  

    -   **Utilizar un servidor proxy al sincronizar las actualizaciones de software**  

    -   **Utilizar un servidor proxy al descargar contenido mediante reglas de implementación automática**  

    > [!TIP]  
    >  Para poder seleccionar una de las opciones, debe configurarse un servidor proxy en el servidor de sistema de sitio que hospeda el punto de actualización de software. Sólo se utiliza el servidor proxy para las opciones específicas que seleccione.  

 Para obtener más información sobre servidores proxy para puntos de actualización de software, vea la sección "Configuración de servidor proxy" en el tema [Instalar y configurar un punto de actualización de software](../../../sum/get-started/install-a-software-update-point.md).  

-   **Punto de conexión de servicio.** Cuando se configura para estar en línea (no sin conexión), este rol de sistema de sitio se conecta a Microsoft Intune y al servicio en la nube de Microsoft.  

