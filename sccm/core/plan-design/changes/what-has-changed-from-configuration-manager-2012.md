---
title: 'Cambios respecto a Configuration Manager 2012 | Microsoft Docs '
description: Identifica los cambios y las nuevas funciones de System Center Configuration Manager con respecto a System Center 2012 Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
caps.latest.revision: 51
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 828e2ac9a3f9bcea1571d24145a1021fdf1091f3
ms.openlocfilehash: 3ede76bd60372dcef2b1b3230577ee3c3f1e2dcd


---
# <a name="what39s-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>Cambios en System Center Configuration Manager respecto a System Center 2012 Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


 La rama actual de System Center Configuration Manager introduce cambios importantes con respecto a System Center 2012 Configuration Manager. En la información de este tema se indican los cambios más importantes y las nuevas funciones de la versión de referencia 1511 de System Center Configuration Manager. Para obtener más información sobre los cambios adicionales que se introducen en actualizaciones posteriores para System Center Configuration Manager, consulte [What's new in System Center Configuration Manager incremental versions](/sccm/core/plan-design/changes/whats-new-incremental-versions) (Novedades de versiones incrementales de System Center Configuration Manager).



 La versión de diciembre de 2015 de System Center Configuration Manager (versión 1511) es la versión de producto más reciente de Configuration Manager de Microsoft.   Se conoce habitualmente como la rama actual de System Center Configuration Manager. *Rama actual* indica que se trata de una versión que admite actualizaciones incrementales del producto y puede suponer una diferencia importante entre esta y versiones anteriores de Configuration Manager.  

 Con esta versión de System Center Configuration Manager:  

-   No use un identificador de producto o de año en el nombre de producto, tal como se hacía en versiones anteriores como Configuration Manager 2007 o System Center 2012 Configuration Manager.

-   Admite actualizaciones incrementales desde el producto, que también se denominan versiones de actualización. La versión inicial es 1511. Las versiones posteriores se publican varias veces al año como las actualizaciones en la consola, como versión 1602 o 1606.




##  <a name="a-namebkmkupdatesa-in-console-updates-for-configuration-manager"></a><a name="bkmk_updates"></a> Actualizaciones en consola para Configuration Manager  
 System Center Configuration Manager usa un método de servicio en la consola denominado **Actualizaciones y mantenimiento** que facilita la ubicación de las actualizaciones recomendadas para Configuration Manager y su posterior instalación.  

 Algunas versiones solo están disponibles como actualizaciones para los sitios existentes (desde la consola de Configuration Manager) y no se pueden usar para instalar nuevos sitios de Configuration Manager.   
Por ejemplo, la actualización 1602 solo está disponible en la consola de Configuration Manager y se usa para actualizar un sitio que ejecuta una versión de referencia 1511 a la versión 1602.  

Periódicamente, también se publicará una versión de actualización como una nueva versión de referencia (como la actualización 1606) que se puede usar para instalar una nueva jerarquía sin necesidad de iniciar con una versión de referencia anterior (como 1511) para actualizar a la versión más reciente.


 Para obtener más información sobre el uso de actualizaciones, consulte [Updates for System Center Configuration Manager](../../../core/servers/manage/updates.md) (Actualizaciones para System Center Configuration Manager).  

##  <a name="a-namebkmkservicepointa-service-connection-point-replaces-microsoft-intune-connector"></a><a name="bkmk_servicepoint"></a> El punto de conexión de servicio reemplaza el conector de Microsoft Intune  
 El **conector de Microsoft Intune** se reemplazó por un nuevo rol de sistema de sitio que habilita una funcionalidad adicional, el **punto de conexión de servicio**. El punto de conexión de servicio:  

-   Reemplaza el conector de Microsoft Intune cuando Intune se integra con la administración de dispositivos móviles local de System Center Configuration Manager  

-   Se utiliza como un punto de contacto para dispositivos administrados con  

-   Carga datos de uso sobre la implementación al servicio de nube de Microsoft  

-   Realiza las actualizaciones aplicables a su implementación disponible desde la consola de Configuration Manager  

Este rol de sistema de sitio admite el modo de funcionamiento tanto en línea como sin conexión que puede afectar a su uso adicional. Para obtener más información, consulte [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md) (Acerca del punto de conexión de servicio en System Center Configuration Manager).  

##  <a name="a-namebkmkusagea-usage-data-collection"></a><a name="bkmk_usage"></a> Recopilación de datos de uso  
 System Center Configuration Manager recopila datos de uso de los sitios y la infraestructura. Esta información se recopila y se envía al servicio en la nube de Microsoft a través del punto de conexión de servicio (un nuevo rol de sistema de sitio) y es necesaria para permitir que Configuration Manager descargue actualizaciones de la implementación que se aplican a la versión de Configuration Manager que se usa. Al configurar el punto de conexión de servicio, puede configurar tanto el nivel de los datos que se recopilan y si estos datos se envía de forma automática (modo en línea) o manual (modo sin conexión).  

 Para obtener más información, consulte [Usage data levels and settings](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage) (Configuración y niveles de datos de uso).  

##  <a name="a-namebkmkamta-support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Compatibilidad para la Tecnología de administración activa (AMT) Intel  
 Con System Center Configuration Manager, se ha quitado la compatibilidad nativa con equipos basados en AMT desde la consola de Configuration Manager.  

-   Los equipos basados en AMT siguen estando totalmente administrados cuando se usa el [complemento Intel SCS para Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html).  

-   El uso del complemento ofrece acceso a las últimas capacidades para administrar AMT a la vez que elimina las limitaciones introducidas hasta que Configuration Manager pudo incorporar esos cambios.  

-   La administración fuera de banda en System Center 2012 Configuration Manager no se ve afectada por este cambio  

La eliminación de AMT integrada para System Center Configuration Manager incluye lo siguiente:  

-   El rol de sistema de sitio del punto de administración fuera de banda ya no se usa ni está disponible.  

##  <a name="a-namebkmkouta-deprecated-functionality"></a><a name="bkmk_out"></a> Característica en desuso  
 Con System Center Configuration Manager, algunas funciones (como los equipos basados en [Compatibilidad con la Tecnología de administración activa (AMT) Intel](#bkmk_AMT) nativa) se quitaron de la consola de Configuration Manager, mientras que otras funciones (como la protección de acceso de red) se quitaron por completo. Además, algunos productos de Microsoft anteriores como Windows Vista, Windows Server 2008 y SQL Server 2008, ya no son compatibles.  

 Para obtener una lista de características en desuso, consulte [Removed and deprecated features for System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md) (Características eliminadas y en desuso de System Center Configuration Manager).  

 Para obtener información detallada sobre productos, sistemas operativos y configuraciones compatibles, consulte [Supported configurations for System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md) (Configuraciones admitidas para System Center Configuration Manager).  

## <a name="client-deployment"></a>Implementación de cliente  
 System Center Configuration Manager presenta una nueva función para probar las nuevas versiones de cliente de Configuration Manager antes de actualizar el resto del sitio con el nuevo software.  Esta nueva función permite configurar una recopilación de preproducción en la que se define un programa piloto de un cliente nuevo. Una vez que esté satisfecho con el nuevo software cliente de la etapa de preproducción, puede promover el cliente para actualizar automáticamente el resto del sitio con la nueva versión.  

 Para obtener más información sobre cómo probar clientes, consulte [How to test client upgrades in a preproduction collection in System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md) (Cómo probar las actualizaciones de cliente en una recopilación de preproducción en System Center Configuration Manager).  

## <a name="operating-system-deployment"></a>Implementación de sistema operativo  

-   El Asistente para crear secuencia de tareas ofrece un nuevo tipo de secuencia de tareas,  **Actualizar un sistema operativo desde el paquete de actualización**, que crea los pasos necesarios para actualizar equipos de Windows 7, Windows 8 o Windows 8.1 a Windows 10.  Para obtener más información, consulte [Upgrade Windows to the latest version with System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) (Actualizar Windows a la versión más reciente con System Center Configuration Manager).  

-   El almacenamiento en caché de Windows PE ya está disponible al implementar sistemas operativos. Los equipos que ejecutan una secuencia de tareas para implementar un sistema operativo pueden usar el almacenamiento en caché del mismo nivel de Windows PE para obtener contenido a partir de un elemento local del mismo nivel (un origen de memoria caché del mismo nivel), en lugar de descargar contenido desde un punto de distribución. Esto ayuda a minimizar el tráfico de red de área extensa (WAN) en escenarios de sucursales donde no hay ningún punto de distribución local. Para obtener más información, consulte [Prepare Windows PE peer cache to reduce WAN traffic in System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic) (Preparar el almacenamiento en caché del mismo nivel de Windows PE para reducir el tráfico WAN en System Center Configuration Manager).  

-   Ahora puede ver el estado de Windows como servicio en su entorno, crear planes de mantenimiento para anillos de implementación de formularios y asegurarse de que los equipos de la rama actual de Windows 10 se mantengan actualizados si se publican nuevas compilaciones. Además, puede ver alertas cuando el servicio de soporte técnico de los clientes de Windows 10 que poseen las compilaciones de Rama actual (CB) o Rama actual para empresas (CBB) está a punto de finalizar. Para obtener más información, consulte [Manage Windows as a service using System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md) (Administración de Windows como servicio mediante System Center Configuration Manager).  

## <a name="application-management"></a>Administración de aplicaciones  

-   System Center Configuration Manager le permite implementar aplicaciones de Plataforma universal de Windows (UWP) para dispositivos que ejecutan Windows 10 y versiones posteriores. Consulte [Creating Windows applications with System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md) (Creación de aplicaciones de Windows con System Center Configuration Manager).  

-   El Centro de software tiene un aspecto nuevo y moderno, y las aplicaciones que antes solo aparecían en el catálogo de aplicaciones (aplicaciones disponibles para el usuario) ahora se incluyen en la pestaña Aplicaciones del Centro de software. De este modo, a los usuarios les resulta más sencillo detectar las implementaciones y ya no tienen que usar el catálogo de aplicaciones. Además, ya no hace falta un explorador habilitado para Silverlight. Consulte [Plan for and configure application management in System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md) (Planear y configurar la administración de aplicaciones en System Center Configuration Manager).  

-   El nuevo tipo de aplicación Windows Installer a través de MDM le permite crear e implementar aplicaciones basadas en Windows Installer para los equipos inscritos que ejecutan Windows 10. Consulte [Creating Windows applications with System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md) (Creación de aplicaciones de Windows con System Center Configuration Manager).  

-   Si crea una aplicación para una aplicación interna de iOS, solo debe especificar el archivo de instalador (.ipa) de la aplicación. Ya no es necesario especificar un archivo de lista de propiedades (.plist) correspondiente. Consulte [Creating iOS applications with System Center Configuration Manager](../../../apps/get-started/creating-ios-applications.md) (Creación de aplicaciones de iOS con System Center Configuration Manager).  

-   En Configuration Manager 2012, para especificar un vínculo a una aplicación de la Tienda Windows, se podía especificar el vínculo directamente o buscar un equipo remoto que tuviese instalada la aplicación. En System Center Configuration Manager, también se puede escribir el vínculo directamente, pero ahora, en lugar de buscar un equipo de referencia, se puede examinar la tienda de la aplicación directamente desde la consola de Configuration Manager.  

## <a name="software-updates"></a>Actualizaciones de software  

-   System Center Configuration Manager ahora puede diferenciar un equipo Windows 10 que se conecta a Windows Update for Business (WUfB) para la administración de actualizaciones de software y los equipos conectados a WSUS para la administración de actualizaciones de software. El atributo **UseWUServer** es nuevo y especifica si el equipo se administra con WUfB. Puede usar esta configuración en una recopilación para quitar estos equipos de la administración de actualizaciones de software. Para obtener más información, consulte [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md) (Integración con Windows Update for Business en Windows 10).  

-   Ya puede programar y ejecutar una tarea de limpieza de WSUS desde la consola de Configuration Manager.  
    Ahora puede ejecutar manualmente la tarea de limpieza de WSUS desde las propiedades del componente de punto de actualización de software. Cuando se seleccione ejecutar la tarea de limpieza de WSUS, se ejecutará en la siguiente sincronización de actualizaciones de software. Las actualizaciones de software expiradas se establecerán en un estado rechazado en el servidor de WSUS y el agente de Windows Update de los equipos ya no las examinará. Para obtener más información, consulte [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md) (Programar y ejecutar la tarea de limpieza de WSUS).  

## <a name="compliance-settings"></a>Configuración de cumplimiento  

-   System Center Configuration Manager incorpora un flujo de trabajo mejorado para crear elementos de configuración. Ahora, cuando cree un elemento de configuración y seleccione las plataformas admitidas, solo están disponible las opciones relevantes para esa plataforma. Consulte [Get started with compliance settings in System Center Configuration Manager](../../../compliance/get-started/get-started-with-compliance-settings.md) (Introducción a la configuración de cumplimiento en System Center Configuration Manager).  

-   El Asistente para crear elemento de configuración ahora facilita la elección del tipo de elemento de configuración que quiere crear. Además, hay elementos de configuración nuevos y actualizados que están disponibles para los siguientes dispositivos:  

    -   Dispositivos Windows 10 administrados con el cliente de Configuration Manager  

    -   Dispositivos Mac OS X administrados con el cliente de Configuration Manager  

    -   Equipos de escritorio y servidores de Windows administrados con el cliente de Configuration Manager  

    -   Dispositivos Windows 8.1 y Windows 10 administrados sin el cliente de Configuration Manager  

    -   Dispositivos Windows Phone administrados sin el cliente de Configuration Manager  

    -   Dispositivos iOS y Mac OS X administrados sin el cliente de Configuration Manager  

    -   Dispositivos Android y Samsung KNOX Standard administrados sin el cliente de Configuration Manager  

     Consulte [How to create configuration items in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items.md) (Cómo crear elementos de configuración en System Center Configuration Manager).  

-   Compatibilidad para administrar la configuración en equipos Mac OS X que están inscritos con Microsoft Intune o administrados mediante el cliente de Configuration Manager. Consulte [How to create configuration items for iOS and Mac OS X devices managed without the System Center Configuration Manager client](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md) (Cómo crear elementos de configuración para dispositivos iOS y Mac OS X administrados sin el cliente de System Center Configuration Manager).  

## <a name="protect-data-and-site-infrastructure"></a>Proteger los datos y la infraestructura del sitio  
-   System Center Configuration Manager permite la integración con Windows Hello para empresas (anteriormente Microsoft Passport for Work), que es un método alternativo de inicio de sesión que usa Active Directory, o una cuenta de Azure Active Directory para reemplazar una contraseña, una tarjeta inteligente o una tarjeta inteligente virtual en dispositivos que ejecutan Windows 10. Consulte [Windows Hello for Business settings in System Center Configuration Manager](../../../protect/deploy-use/windows-hello-for-business-settings.md) (Configuración de Windows Hello para empresas en System Center Configuration Manager).

## <a name="mobile-device-management-with-microsoft-intune"></a>Administración de dispositivos móviles con Microsoft Intune  
 System Center Configuration Manager incorpora mejoras en la experiencia de administración de dispositivos móviles, entre ellas:  

-   limitación del número de dispositivos que puede inscribir un usuario;  

-   especificación de términos y condiciones que los usuarios del portal de empresa deben aceptar para poder inscribir o usar la aplicación;  

-   incorporación de un rol de administrador de inscripción de dispositivos para ayudar a administrar un gran número de dispositivos.  

Para obtener más información sobre las funciones de administración de dispositivos móviles con Configuration Manager e Intune, consulte [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md) (Administración híbrida de dispositivos móviles (MDM) con System Center Configuration Manager y Microsoft Intune).  

## <a name="on-premises-mobile-device-management"></a>Administración local de dispositivos móviles  
 Con System Center Configuration Manager, ahora puede administrar dispositivos móviles con la infraestructura de Configuration Manager local. La totalidad de la administración de dispositivos y los datos de administración se controla localmente y no forma parte de Microsoft Intune u otros servicios en la nube. Este tipo de administración de dispositivos no requiere software cliente ya que las características que Configuration Manager usa para administrar los dispositivos están integradas en los sistemas operativos de los dispositivos.  

 Para obtener más información, consulte [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) (Administrar dispositivos móviles con la infraestructura local en System Center Configuration Manager).



<!--HONumber=Dec16_HO3-->


