---
title: Cambios desde Configuration Manager 2012
description: Identifica los cambios y las nuevas funciones de System Center Configuration Manager con respecto a System Center 2012 Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eb6071e576a12773c0aa5627dad80700db843f43
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496103"
---
# <a name="whats-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>Cambios en System Center Configuration Manager respecto a System Center 2012 Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La rama actual de Configuration Manager presenta cambios importantes de System Center 2012 Configuration Manager. En este artículo se identifican los cambios más importantes y las nuevas funciones de la versión de línea base 1511 de System Center Configuration Manager. Para obtener más información sobre los cambios que se presentan en actualizaciones posteriores para System Center Configuration Manager, vea [Acerca de las versiones incrementales de System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).

La versión de diciembre de 2015 de System Center Configuration Manager (versión 1511) es la versión inicial del producto actual de Configuration Manager de Microsoft. Se conoce habitualmente como la rama actual de System Center Configuration Manager. *Rama actual* indica que esta versión que actualizaciones incrementales para el producto. También proporciona una manera de distinguir entre esta versión y las versiones anteriores de Configuration Manager.  

System Center Configuration Manager:  

- No usa un identificador de producto o de año en el nombre de producto, a diferencia de versiones anteriores como Configuration Manager 2007 o System Center 2012 Configuration Manager.  

- Admite actualizaciones incrementales desde el producto, que también se denominan versiones de actualización. La versión inicial era la 1511. Varias veces al año se publican versiones posteriores como actualizaciones en consola, como la versión 1810.  

- Se instala con una versión de línea base. Aunque 1511 era la versión original de línea de base, las nuevas versiones de línea de base también se publican de vez en cuando, como la 1902. Las versiones de línea base se pueden usar para instalar un nuevo sitio de System Center Configuration Manager y la jerarquía o para actualizar desde una versión compatible de Configuration Manager 2012.  



##  <a name="bkmk_updates"></a> Actualizaciones en consola para Configuration Manager  

System Center Configuration Manager usa un método de servicio en la consola denominado **Actualizaciones y mantenimiento** que facilita la ubicación e instalación de las actualizaciones recomendadas.  

Algunas versiones solo están disponibles como actualizaciones para los sitios existentes (desde la consola de Configuration Manager) y no se pueden usar para instalar nuevos sitios de Configuration Manager. Por ejemplo, la actualización 1810 solo está disponible en la consola de Configuration Manager. Se usa para actualizar un sitio que ya ejecuta una versión de System Center Configuration Manager.

Periódicamente, también se publica una versión de actualización como una nueva versión de línea de base (como la actualización 1902). Este tipo de actualización se puede usar para instalar una nueva jerarquía sin necesidad de comenzar con una versión de línea de base anterior (como 1802) y actualizar a la versión más reciente.


Para más información sobre el uso de actualizaciones, consulte [Updates for Configuration Manager](/sccm/core/servers/manage/updates) (Actualizaciones para Configuration Manager).  
Para más información sobre las versiones de línea base, consulte [Versiones de línea de base y versiones de actualización](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions).



##  <a name="bkmk_servicepoint"></a> Nuevo rol de sistema de sitio: punto de conexión de servicio  

El **conector de Microsoft Intune** se reemplazó por un nuevo rol de sistema de sitio que habilita una funcionalidad adicional, el **punto de conexión de servicio**. El punto de conexión de servicio:  

- Reemplaza el conector de Microsoft Intune cuando Intune se integra con la administración de dispositivos móviles local de System Center Configuration Manager.  

- Se usa como un punto de contacto para los dispositivos que administra.  

- Carga datos de uso sobre la implementación al servicio de nube de Microsoft.  

- Realiza las actualizaciones aplicables a su implementación disponible desde la consola de Configuration Manager.  

Este rol de sistema de sitio admite los modos de funcionamiento en línea y sin conexión. Para obtener más información, consulte [About the service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point) (Sobre el punto de conexión del servicio).  



##  <a name="bkmk_usage"></a> Recopilación de datos de uso  

Configuration Manager recopila datos de uso de los sitios y la infraestructura. Esta información se compila y se envía al servicio de nube de Microsoft mediante el punto de conexión de servicio. Se necesita para permitir que Configuration Manager descargue actualizaciones para su implementación que se aplican a la versión de Configuration Manager que usa. Al configurar el punto de conexión de servicio, puede especificar tanto el nivel de los datos que se recopilan y si los datos se envían de manera automática (modo en línea) o manual (modo sin conexión).  

Para obtener más información, vea [Diagnósticos y datos de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  



##  <a name="bkmk_AMT"></a> Compatibilidad para la Tecnología de administración activa (AMT) Intel  

La rama actual de Configuration Manager quita la compatibilidad nativa con equipos basados en AMT desde la consola de Configuration Manager. Los equipos basados en AMT siguen estando totalmente administrados cuando se usa el [complemento Intel SCS para Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). El complemento permite el acceso a las funciones más recientes para administrar AMT, a la vez que elimina las limitaciones introducidas hasta que Configuration Manager pudo incorporar esos cambios.  

La eliminación de AMT integrada para Configuration Manager incluye la administración fuera de banda. El rol de sistema de sitio del punto de administración fuera de banda ya no está disponible.  

> [!Note]   
> La administración fuera de banda en System Center 2012 Configuration Manager no se ve afectada por este cambio.  



##  <a name="bkmk_out"></a> Característica en desuso  

Algunas características, como los equipos nativos basados en la [Compatibilidad con la Tecnología de administración activa (AMT) de Intel](#bkmk_AMT), se quitan de la consola de Configuration Manager. Otras características, como la Protección de acceso a redes, se quitan completamente. Además, algunos productos de Microsoft anteriores como Windows Vista, Windows Server 2008 y SQL Server 2008, ya no son compatibles.  

Para una lista de las características en desuso, consulte el artículo [Elementos eliminados y en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).  

Para información detallada sobre productos, sistemas operativos y configuraciones compatibles, consulte [Configuraciones admitidas](/sccm/core/plan-design/configs/supported-configurations).  



## <a name="client-deployment"></a>Implementación de cliente  

Configuration Manager presenta una nueva característica para probar las nuevas versiones de cliente de Configuration Manager antes de actualizar el resto del sitio con el nuevo software. Puede configurar una recopilación de preproducción en la que realizar un piloto en un cliente nuevo. Una vez que esté satisfecho con el nuevo software cliente de preproducción, puede promover el cliente para actualizar automáticamente el resto del sitio con la nueva versión.  

Para más información sobre cómo probar los clientes, consulte [Cómo probar las actualizaciones de cliente en una recopilación de preproducción](/sccm/core/clients/manage/upgrade/test-client-upgrades).  



## <a name="os-deployment"></a>Implementación del sistema operativo  

Tenga en cuenta los siguientes cambios en la implementación del sistema operativo:

- En el Asistente para crear secuencia de tareas, hay disponible un nuevo tipo de secuencia de tareas: **Actualización de un sistema operativo desde un paquete de actualización**. Crea los pasos para actualizar equipos de Windows 7, Windows 8 o Windows 8.1 a Windows 10. Para más información, consulte [Actualizar Windows a la versión más reciente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version).  

- El almacenamiento en caché de Windows PE ya está disponible al implementar sistemas operativos. Los equipos que ejecutan una secuencia de tareas para implementar un sistema operativo pueden usar el almacenamiento en caché del mismo nivel de Windows PE para obtener contenido a partir de un origen de caché del mismo nivel, en lugar de descargar contenido desde un punto de distribución. Este comportamiento minimiza el tráfico WAN en escenarios de sucursales donde no existe un punto de distribución local. Para obtener más información, consulte [Preparar el almacenamiento en caché del mismo nivel de Windows PE para reducir el tráfico WAN](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).  

- Ahora puede ver el estado de Windows como un servicio de su entorno. También puede crear planes de mantenimiento para formar anillos de implementación y garantizar que los equipos de la rama actual de Windows 10 se mantengan actualizados cuando se presenten nuevas compilaciones. Además, puede ver alertas cuando los clientes de Windows 10 estén cerca del final del soporte técnico de su compilación. Para obtener más información, consulte [Manage Windows as a service](/sccm/osd/deploy-use/manage-windows-as-a-service) (Administrar Windows como servicio).  



## <a name="application-management"></a>Administración de aplicaciones  

Tenga en cuenta los siguientes cambios en la administración de aplicaciones:

- Configuration Manager le permite implementar aplicaciones de Plataforma universal de Windows (UWP) para dispositivos que ejecutan Windows 10 y versiones posteriores. Para más información, consulte [Creación de aplicaciones Windows](/sccm/apps/get-started/creating-windows-applications).  

- El Centro de software tiene un aspecto renovado y moderno. Las aplicaciones disponibles para el usuario que antes solo aparecían en el catálogo de aplicaciones ahora se incluyen en la pestaña Aplicaciones del Centro de software. Este comportamiento hace que estas implementaciones sean más reconocibles y que los usuarios no necesiten consultar el catálogo de aplicaciones. Además, ya no hace falta un explorador habilitado para Silverlight. Para obtener más información, consulte [Planear y configurar la administración de aplicaciones en Configuration Manager](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

- El nuevo tipo de aplicación Windows Installer a través de MDM le permite crear e implementar aplicaciones basadas en Windows Installer para los equipos inscritos que ejecutan Windows 10. Para más información, consulte [Creación de aplicaciones Windows](/sccm/apps/get-started/creating-windows-applications).  

- Si crea una aplicación para una aplicación interna de iOS, solo debe especificar el archivo de instalador (.ipa) de la aplicación. Ya no es necesario especificar un archivo de lista de propiedades (.plist) correspondiente. Consulte [Creación de aplicaciones iOS](/sccm/apps/get-started/creating-ios-applications).  

- En Configuration Manager 2012, para especificar un vínculo a una aplicación de la Tienda Windows, se podía especificar el vínculo directamente o buscar un equipo remoto que tuviese instalada la aplicación. En la rama actual de Configuration Manager, también se puede escribir el vínculo directamente, pero ahora, en lugar de buscar un equipo de referencia, puede examinar la tienda de la aplicación directamente desde la consola de Configuration Manager.  



## <a name="software-updates"></a>Actualizaciones de software  

Tenga en cuenta los siguientes cambios en las actualizaciones de software:

- Configuration Manager ahora puede detectar la diferencia entre los métodos de administración de actualización de software en los equipos. Concretamente, puede diferenciar entre un equipo Windows 10 que se conecta a Windows Update for Business (WUfB) y un equipo conectado a WSUS. El atributo **UseWUServer** es nuevo y especifica si el equipo se administra con WUfB. Puede usar esta configuración en una recopilación para quitar estos equipos de la administración de actualizaciones de software. Para obtener más información, consulte [Integration with Windows Update for Business in Windows 10](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10) (Integración con Windows Update for Business en Windows 10).  

- Ahora ya puede programar y ejecutar la tarea de limpieza de WSUS desde la consola de Configuration Manager. En las propiedades **Componente de punto de actualización de software**, cuando seleccione ejecutar la tarea de limpieza de WSUS, se ejecutará en la siguiente sincronización de actualizaciones de software. Las actualizaciones de software expiradas se establecen en un estado rechazado en el servidor de WSUS y el agente de Windows Update de los equipos ya no las examinará. Para obtener más información, consulte [Schedule and run the WSUS clean up task](/sccm/sum/deploy-use/software-updates-maintenance) (Programar y ejecutar la tarea de limpieza de WSUS).  



## <a name="compliance-settings"></a>Configuración de cumplimiento  

Tenga en cuenta los siguientes cambios en la configuración de cumplimiento:

- Configuration Manager mejora el flujo de trabajo para crear elementos de configuración. Ahora, cuando cree un elemento de configuración y seleccione las plataformas admitidas, solo están disponible las opciones relevantes para esa plataforma. Consulte [Introducción a la configuración de cumplimiento](/sccm/compliance/get-started/get-started-with-compliance-settings).  

- El Asistente para **crear elemento de configuración** ahora facilita la elección del tipo de elemento de configuración que quiere crear. Además, hay elementos de configuración nuevos y actualizados que están disponibles para los siguientes dispositivos:  

    - Dispositivos Windows 10 administrados con el cliente de Configuration Manager  

    - Dispositivos Mac OS X administrados con el cliente de Configuration Manager  

    - Equipos de escritorio y servidores de Windows administrados con el cliente de Configuration Manager  

    - Dispositivos Windows 8.1 y Windows 10 administrados sin el cliente de Configuration Manager  

    - Dispositivos Windows Phone administrados sin el cliente de Configuration Manager  

    - Dispositivos iOS y Mac OS X administrados sin el cliente de Configuration Manager  

    - Dispositivos Android y Samsung KNOX Standard administrados sin el cliente de Configuration Manager  
  
    Para más información, consulte [Cómo crear elementos de configuración](/sccm/compliance/deploy-use/create-configuration-items).  

- Compatibilidad para administrar la configuración en equipos Mac OS X que están inscritos con Microsoft Intune o administrados con el cliente de Configuration Manager. Consulte [Cómo crear elementos de configuración para dispositivos iOS y Mac OS X administrados sin el cliente de Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client).  



## <a name="on-premises-mobile-device-management"></a>Administración local de dispositivos móviles  

Ahora puede administrar dispositivos móviles con la infraestructura local de Configuration Manager. La totalidad de los dispositivos y los datos de administración se controla localmente y no forma parte de Microsoft Intune ni de otros servicios en la nube. Este tipo de administración de dispositivos no necesita software cliente. Configuration Manager administra los dispositivos con una funcionalidad integrada en el sistema operativo del dispositivo.  

Para obtener más información, consulte [Administrar dispositivos móviles con la infraestructura local](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).
