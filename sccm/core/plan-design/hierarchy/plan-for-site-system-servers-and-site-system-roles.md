---
title: Planificar roles del sistema de sitio | System Center Configuration Manager
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
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5f8d051a92cd74938f1a5235b37f02ebe0ff542c


---
# <a name="plan-for-site-system-servers-and-site-system-roles-for-system-center-configuration-manager"></a>Planeamiento de servidores y roles de sistema de sitio para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Cada sitio de System Center Configuration Manager que se instala incluye un servidor de sitio que es un **servidor de sistema de sitio**. El sitio también puede incluir servidores de sistema de sitio adicionales en equipos que están alejados del servidor de sitio (equipos remotos).   Los servidores de sistema de sitio (el servidor de sitio o un servidor de sistema de sitio remoto) admiten **roles de sistema de sitio**.


##  <a name="a-namebkmksiteserversa-site-system-servers"></a><a name="bkmk_siteservers"></a> Servidores de sistema de sitio  
 Al instalar un rol de sistema de sitio en un equipo, ese equipo se convierte en un servidor de sistema de sitio. En cada sitio puede instalar a uno o más servidores de sistema de sitio adicionales. También puede elegir no instalar servidores de sistema de sitio adicionales y ejecutar todos los roles de sistema de sitio directamente en el equipo del servidor de sitio.  Cada servidor de sistema de sitio admite uno o varios roles de sistema de sitio y ayuda a ampliar las funcionalidades y la capacidad de un sitio al compartir la carga de procesamiento de la CPU que generan los roles de sistema de sitio en un servidor.  

 Si se plantea la posibilidad de agregar un servidor de sistema de sitio, asegúrese de que cumpla los requisitos previos para el uso previsto y que se encuentre en una ubicación de red con ancho de banda suficiente para comunicarse con los puntos de conexión esperados, lo que incluye el servidor de sitio, los recursos de dominio, la ubicación basada en la nube, los servidores de sistema de sitio y los clientes).  

 Si configura el servidor de sistema de sitio con un servidor proxy para su uso por los roles de sistema de sitio, consulte [Roles de sistema de sitio que pueden utilizar un servidor proxy](#bkmk_proxy)  

##  <a name="a-namebkmkplanrolesa-site-system-roles"></a><a name="bkmk_planroles"></a> Site system roles  
 Los roles de sistema de sitio se instalan en un equipo para proporcionar a este funcionalidades adicionales. Algunos ejemplos son:  

-   Puntos de administración adicionales para que el sitio pueda admitir más dispositivos, hasta alcanzar la capacidad máxima de sitios  

-   Puntos de distribución adicionales para expandir la infraestructura de contenido y mejorar así el rendimiento de las distribuciones de contenido a los usuarios y dispositivos  

-   Uno o varios roles de sistema de sitio de características específicas, como un punto de actualización de software que se usa para administrar las actualizaciones de software de los dispositivos administrados, o un punto de servicios de informes para que pueda ejecutar informes para supervisar y comprender o compartir información acerca de la implementación  


Diferentes sitios de Configuration Manager pueden admitir un conjunto diferente de roles de sistema de sitio. Los roles de sistema de sitio admitidos dependen del tipo de sitio (sitio de administración central, sitio primario o sitio secundario). La topología de la jerarquía puede limitar la colocación de algunos roles en determinados tipos de sitios. Por ejemplo, el punto de conexión de servicio solo se admite en el sitio de nivel superior de la jerarquía, que podría ser un sitio de administración central o un sitio primario independiente. Este rol no se admite en un sitio principal secundario ni en los sitios secundarios.  

Después de que se instala un sitio, puede mover la ubicación de algunos roles de sistema de sitio de su ubicación predeterminada en el servidor de sitio a otro servidor (como el punto de administración o el punto de distribución que se instala de forma predeterminada en un servidor de sitio primario o secundario). También puede instalar instancias adicionales de algunos roles de sistema de sitio para ampliar las funcionalidades del sitio (proporcionar más servicios a los clientes) y para cumplir sus requisitos empresariales. Algunos roles son necesarios, mientras que otros son opcionales:  

-   **Servidor de sitio de Configuration Manager**: este rol identifica el servidor donde se ejecuta el programa de instalación de Configuration Manager para instalar un sitio o el servidor en el que se instala un sitio secundario. Este rol no se puede mover ni desinstalar hasta que se desinstale el sitio.  

-   **Sistema de sitio de Configuration Manager**: este rol se asigna a cualquier equipo donde se instala un sitio o un rol de sistema de sitio.  Este rol no se puede mover ni desinstalar hasta que el último rol de sistema de sitio se quite del equipo.  

-   **Rol de sistema de sitio de componente de Configuration Manager**: este rol identifica un sistema de sitio que ejecuta una instancia del servicio SMS Executive y es necesario para admitir otros roles, como los puntos de administración. Este rol no se puede mover ni desinstalar hasta que el último rol de sistema de sitio aplicable se quite del equipo.  

-   **Servidor de base de datos de sitio de Configuration Manager**: este rol se asigna a los servidores de sistema de sitio que contienen una instancia de la base de datos del sitio para un sitio.  Este rol solo se puede mover a un nuevo servidor modificando el sitio para que use un SQL Server diferente para hospedar la base de datos del sitio.  

-   **Proveedor de SMS**: el rol de proveedor de SMS se asigna a cada equipo que hospeda una instancia del proveedor de SMS, la interfaz entre una consola de Configuration Manager y la base de datos del sitio.  De forma predeterminada, este rol se instala automáticamente en el servidor de sitio de un sitio de administración central y de sitios primarios, y se pueden instalar instancias adicionales en cada sitio para proporcionar a otros usuarios administrativos acceso administrativo a un sitio.  

     A diferencia de la mayoría de los roles de sistema sitio que se instalan dentro de la consola, para instalar proveedores adicionales debe ejecutar el programa de instalación de Configuration Manager para [Administrar el proveedor de SMS](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) y luego instalar proveedores adicionales en otros equipos. Solo puede instalar una instancia del proveedor de SMS en un equipo y dicho equipo debe estar en el mismo dominio que el servidor de sitio.  

-   **Punto de servicio web del catálogo de aplicaciones** : un rol de sistema de sitio que proporciona información de software al sitio web del catálogo de aplicaciones desde la biblioteca de software. Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de él en un sitio o en varios sitios de la misma jerarquía.  

-   **Punto de sitios web del catálogo de aplicaciones** : un rol de sistema de sitio que proporciona a los usuarios una lista del software disponible desde el catálogo de aplicaciones. Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de él en un sitio o en varios sitios de la misma jerarquía.  

     Si el catálogo de aplicaciones admite equipos cliente en Internet, instale, como práctica recomendada de seguridad, el punto de sitios web del catálogo de aplicaciones en una red perimetral y el punto de servicio web del catálogo de aplicaciones en la intranet.  

-   **Punto de sincronización de Asset Intelligence** : un rol de sistema de sitio que se conecta a Microsoft para descargar información del catálogo de Asset Intelligence y para cargar títulos sin categorizar para considerar su futura inclusión en el catálogo.  Una jerarquía admite una sola instancia de este rol, y esa debe estar en el sitio de nivel superior de la jerarquía (un sitio de administración central o el sitio primario independiente). Si expande un sitio primario independiente a una jerarquía más grande, debe desinstalar este rol desde el sitio primario y luego puede instalar en el sitio de administración central.   Para obtener más información, consulte [Asset Intelligence en System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Punto de registro de certificado** : un rol de sistema de sitio que se comunica con un servidor que ejecuta el Servicio de inscripción de dispositivos de red para administrar solicitudes de certificado de dispositivo que usan el Protocolo de inscripción de certificados simple (SCEP).  Este rol solo se admite en los sitios primarios y el sitio de administración central.   Aunque un único punto de registro de certificado puede proporcionar funcionalidad a toda una jerarquía, para ayudar a equilibrar la carga de las solicitudes de certificado puede instalar varias instancias de este rol en un sitio y en varios sitios de la misma jerarquía. Cuando existen varias instancias en una jerarquía, los clientes se asignan aleatoriamente a uno de los puntos de registro de certificado.  

     Cada punto de registro de certificado requiere acceso a una instancia independiente del Servicio de inscripción de dispositivos de red. No se pueden configurar dos o más puntos de registro de certificado para que utilicen el mismo Servicio de inscripción de dispositivos de red. Además, el punto de registro de certificados no debe instalarse en el mismo servidor que ejecuta el Servicio de inscripción de dispositivos de red.  

-   **Punto de distribución** : un rol de sistema de sitio que contiene archivos de origen para que descarguen los clientes, tales como imágenes de arranque, paquetes de software, actualizaciones de software, imágenes del sistema operativo y contenido de la aplicación. De forma predeterminada, este rol se instala en el equipo del servidor de sitio de nuevos sitios primarios y secundarios cuando se instala el sitio, pero no se admite en un sitio de administración central.  Se pueden instalar varias instancias de este rol en un sitio admitido y en varios sitios de la misma jerarquía.  Para obtener más información, consulte [Conceptos básicos de la administración de contenido en System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md), y [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   **Punto de estado de reserva** : un rol de sistema de sitio que le ayuda a supervisar la instalación del cliente e identificar a los clientes sin administrar porque no se pueden comunicar con su punto de administración.  Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de este rol en un sitio y en varios sitios de la misma jerarquía.  Para obtener más información, vea [Escenarios de ubicación de orígenes de contenido](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).


-   **Punto de Endpoint Protection**: Un rol del sistema de sitio que usa Configuration Manager para aceptar los términos de la licencia de Endpoint Protection y configurar la pertenencia predeterminada para Cloud Protection Service (anteriormente conocido como MAPS). Una jerarquía admite una sola instancia de este rol, y esa debe estar en el sitio de nivel superior de la jerarquía (un sitio de administración central o el sitio primario independiente). Si expande un sitio primario independiente a una jerarquía más grande, debe desinstalar este rol desde el sitio primario y luego puede instalar en el sitio de administración central. Para obtener más información, consulte [Endpoint Protection en System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   **Punto de inscripción** : un rol de sistema de sitio que utiliza certificados PKI en Configuration Manager para inscribir dispositivos móviles y equipos Mac. Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de él en un sitio o en varios sitios de la misma jerarquía.  

     Si un usuario inscribe dispositivos móviles mediante Configuration Manager y su cuenta de Active Directory se encuentra en un bosque no es de confianza para el bosque del servidor de sitio, se debe instalar un punto de inscripción en el bosque del usuario para que se pueda autenticar el usuario.  

-   **Punto de proxy de inscripción**: Un rol del sistema de sitio que administra solicitudes de inscripción de Configuration Manager por parte de dispositivos móviles y equipos Mac. Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de él en un sitio o en varios sitios de la misma jerarquía.  

     Como práctica recomendada de seguridad, cuando se admiten dispositivos móviles en Internet, instale el punto de proxy de inscripción en una red perimetral y el punto de inscripción en la intranet.  

-   **Conector de Exchange Server**: para obtener más información, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)  

-   **Punto de administración** : un rol del sistema de sitio que proporciona a los clientes información de ubicación de servicio y de directiva y recibe datos de configuración de los clientes.  
    De forma predeterminada, este rol se instala en el equipo del servidor de sitio de nuevos sitios primarios y secundarios cuando se instala el sitio. Los sitios primarios admiten varias instancias de este rol y los sitios secundarios admiten un único punto de administración para proporcionar un punto de contacto local para que los clientes obtengan directivas de usuario y equipo (un punto de administración en el sitio secundario se conoce como un punto de administración de proxy).  

     Los puntos de administración se pueden configurar para admitir HTTP o HTTPs y para la compatibilidad con dispositivos móviles administrados con la administración local de dispositivos móviles de System Center Configuration Manager. Puede utilizar [Réplicas de bases de datos para puntos de administración de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) para reducir la carga de CPU que los puntos de administración ejercen sobre el servidor de base de datos del sitio mientras atienden las solicitudes de servicio de los clientes.  

-   **Punto de servicios de informes**: rol de sistema de sitio que se integra con SQL Server Reporting Services para crear y administrar informes para Configuration Manager. Este rol se admite en sitios primarios y el sitio de administración central. Puede instalar varias instancias de él en un sitio admitido. Para obtener más información, consulte [Planeamiento de informes en System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md).  

-   **Punto de conexión de servicio**: un rol de sistema de sitio que se usa para administrar dispositivos móviles con Microsoft Intune y MDM local. Este rol también carga los datos de uso del sitio y es necesario para realizar las actualizaciones de Configuration Manager disponibles en la consola de Configuration Manager. Una jerarquía admite una sola instancia de este rol, y esa debe estar en el sitio de nivel superior de la jerarquía (un sitio de administración central o el sitio primario independiente). Si expande un sitio primario independiente a una jerarquía más grande, debe desinstalar este rol desde el sitio primario y luego puede instalar en el sitio de administración central. Para obtener más información, vea [Acerca del punto de conexión de servicio en System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   **Punto de actualización de software**: rol de sistema de sitio que se integra con Windows Server Update Services (WSUS) para proporcionar actualizaciones de software a los clientes de Configuration Manager. Este rol se admite en todos los sitios:  

    -   Instale este sistema de sitio en el sitio de administración central para la sincronización con Windows Server Update Services.  

    -   Configure cada instancia de este rol en sitios primarios secundarios para la sincronización con el sitio de administración central.  

    -   Considere también la posibilidad de instalar un punto de actualización de software en sitios secundarios cuando la transferencia de datos a través de la red sea lenta.  

    Para obtener más información, consulte [Planear las actualizaciones de software en System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

-   **Punto de migración de estado** : un rol de sistema de sitio que almacena datos de estado de usuario cuando se migra un equipo a un nuevo sistema operativo. Este rol se admite en sitios primarios y secundarios, y puede instalar varias instancias de él en un sitio y en varios sitios de la misma jerarquía. Para obtener más información sobre cómo almacenar el estado de usuario al implementar sistemas operativos, consulte [Administrar el estado de usuario en System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   **Punto de Validador de mantenimiento del sistema**: este rol de sistema de sitio ya no se usa con System Center Configuration Manager, aunque permanece visible en la consola de Configuration Manager.  

##  <a name="a-namebkmkproxya-site-system-roles-that-can-use-a-proxy-server"></a><a name="bkmk_proxy"></a> Roles de sistema de sitio que pueden utilizar un servidor proxy  
 Algunos roles de sistema de sitio de Configuration Manager requieren conexiones a Internet y usarán un servidor proxy cuando se configure uno para el servidor de sistema de sitio que hospeda el rol. Normalmente, esta conexión se realiza en el contexto del **sistema** del equipo donde está instalado el rol de sistema de sitio y no puede utilizar una configuración del servidor proxy para las cuentas de usuario habituales. Cuando se requiera un servidor proxy para realizar una conexión a Internet, debe configurar el equipo para ello.  

-   Puede configurar un servidor proxy al instalar un rol de sistema de sitio.  

-   Puede agregar o modificar una configuración de servidor proxy cuando se usa la consola de Configuration Manager.  

-   Todos los roles de sistema de sitio de un servidor de sistema de sitio que pueden usar una configuración de servidor proxy emplean la misma configuración. Si necesita roles de sistema de sitio diferentes para utilizar servidores proxy distintos, debe instalarlos en equipos de servidor de sistema de sitio diferentes.  

-   Si modifica la configuración de servidor proxy o instala un nuevo rol de sistema de sitio en un equipo que ya tiene una, la nueva configuración sobrescribe la configuración original.  


Para ver los procedimientos sobre configuración del servidor proxy para roles de sistema de sitio, consulte el tema [Agregar roles de sistema de sitio para System Center Configuration Manager](../../../core/servers/deploy/configure/add-site-system-roles.md).  

Los siguientes son roles de sistema de sitio que pueden utilizar un servidor proxy:  

-   **Punto de sincronización de Asset Intelligence** : este rol de sistema de sitio se conecta a Microsoft y usará una configuración de servidor proxy en el equipo que hospeda el punto de sincronización de Asset Intelligence.  

-   **Punto de distribución basado en la nube** : cuando use un punto de distribución basado en la nube, el sitio primario que administra el punto de distribución basado en la nube debe poderse conectar a Microsoft Azure para aprovisionar, supervisar y distribuir contenido en el punto de distribución. Si se necesita un servidor proxy para esta conexión, debe configurar el servidor proxy en el servidor del sitio primario. No se puede configurar un servidor proxy en el punto de distribución basado en la nube en Windows Azure.  Para más información, consulte la sección [Configurar parámetros proxy para sitios principales que administran servicios en la nube](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#BKMK_ConfigProxyforCloud) en el tema [Install cloud-based distribution points in Microsoft Azure for System Center Configuration Manager (Instalar puntos de distribución basados en la nube en Microsoft Azure para System Center Configuration Manager)](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).  

-   **Conector de Exchange Server** : este rol de sistema de sitio se conecta a un servidor de Exchange Server y utilizará una configuración de servidor proxy en el equipo que hospeda el conector de Exchange Server.  

-   **Punto de actualización de software** : este rol de sistema de sitio puede requerir conexiones a Microsoft Update para descargar revisiones y sincronizar la información acerca de las actualizaciones. Normalmente, cuando configura el servidor proxy, cada rol de sistema de sitio de ese equipo que admite el uso del servidor proxy usará el servidor proxy sin que requiera configuración adicional. Una excepción a esto es el punto de actualización de software. De forma predeterminada, un punto de actualización de software no utiliza un servidor proxy disponible a menos que también habilite las siguientes opciones cuando se configura el punto de actualización de software:  

    -   **Utilizar un servidor proxy al sincronizar las actualizaciones de software**  

    -   **Utilizar un servidor proxy al descargar contenido mediante reglas de implementación automática**  

    > [!TIP]  
    >  Un servidor proxy debe configurarse en el servidor de sistema del sitio que aloja el punto de actualización de software para poder seleccionar cualquiera de las opciones. Sólo se utiliza el servidor proxy para las opciones específicas que seleccione.  

 Para obtener más información sobre servidores proxy para puntos de actualización de software, consulte la sección Configuración del servidor proxy en el tema [Install a software update point (Instalar un punto de actualización de software)](../../../sum/get-started/install-a-software-update-point.md).  

-   **Punto de conexión de servicio**: cuando se configura para estar en línea (no sin conexión), este rol de sistema de sitio se conecta a Microsoft Intune y al servicio en la nube de Microsoft.  



<!--HONumber=Nov16_HO1-->


