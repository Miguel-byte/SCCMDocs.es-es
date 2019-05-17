---
title: Punto de conexión de servicio
titleSuffix: Configuration Manager
description: Obtenga información sobre este rol de sistema de sitio de Configuration Manager y comprenda y planee sus diversos usos.
ms.date: 08/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f1173a8bec0ab05c3519d04430adddab129389b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499122"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>Acerca del punto de conexión de servicio en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

El punto de conexión de servicio es un rol de sistema de sitio que realiza varias funciones importantes para la jerarquía. Antes de configurar el punto de conexión de servicio, es conveniente conocer y planear sus posibilidades de uso. La planificación del uso podría afectar su forma de configurar este rol de sistema de sitio:  

- **Administrar dispositivos móviles con Microsoft Intune**: este rol reemplaza al conector de Windows Intune que se usaba en las versiones anteriores de Configuration Manager y se puede configurar con los detalles de la suscripción de Intune. Para obtener más información, vea [Administración de dispositivos móviles (MDM) híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).  

- **Administrar dispositivos móviles con MDM local**: este rol ofrece compatibilidad con los dispositivos locales que administra y que no se conectan a Internet. Para obtener más información, consulte [Administrar dispositivos móviles con la infraestructura local](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  

- **Cargar datos de uso desde la infraestructura de Configuration Manager**: puede controlar el nivel o la cantidad de detalle que se carga. Los datos cargados nos ayudan a:  

    - Identificar y solucionar problemas de forma proactiva  

    - Mejorar nuestros productos y servicios  

    - Identificar las actualizaciones de Configuration Manager válidas para la versión de Configuration Manager que use  

    Para obtener más información sobre los datos que recopila cada nivel y sobre cómo cambiar el nivel de recopilación después de instalar el rol, vea [Diagnósticos y datos de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data). Después, siga el vínculo para la versión de Configuration Manager que utilice.  

    Para obtener más información, vea [Configuración y niveles de datos de uso](/sccm/core/servers/deploy/install/setup-reference#bkmk_usage).  

- **Descargar las actualizaciones que se aplican a la infraestructura de Configuration Manager**: solo se ponen a disposición las actualizaciones apropiadas para la infraestructura, según los datos de uso que se carguen.  

- **Cada jerarquía admite una única instancia de este rol**:  

    - El rol de sistema de sitio solo se puede instalar en el sitio de nivel superior de la jerarquía (es decir, un sitio de administración central o un sitio primario independiente).  

    - Si expande un sitio primario independiente a una jerarquía más grande, tendrá que desinstalar este rol desde el sitio primario para instalarlo en el sitio de administración central.  


##  <a name="bkmk_modes"></a> Modos de operación  
El punto de conexión de servicio admite dos modos de funcionamiento:  

- En el **modo en línea**, el punto de conexión de servicio comprueba si existen actualizaciones automáticamente cada 24 horas. Descarga automáticamente las nuevas actualizaciones disponibles para la infraestructura y la versión del producto actuales para que estén disponibles en la consola de Configuration Manager.  

- En el **modo sin conexión**, el punto de conexión de servicio no se conecta al servicio en la nube de Microsoft. Para importar manualmente las actualizaciones disponibles, puede usar la [herramienta de conexión de servicio](/sccm/core/servers/manage/use-the-service-connection-tool).  

Al cambiar entre los modos con conexión o sin conexión después de instalar el punto de conexión de servicio, tendrá que reiniciar el subproceso SMS_DMP_DOWNLOADER del servicio SMS_Executive de Configuration Manager para que se aplique el cambio. Puede usar el Administrador de servicios de Configuration Manager para reiniciar solo el subproceso SMS_DMP_DOWNLOADER del servicio SMS_Executive. También puede reiniciar el servicio SMS_Executive para Configuration Manager, con lo que se reinician la mayoría de componentes del sitio. Como alternativa, puede esperar que una tarea programada, como una copia de seguridad del sitio, detenga y después reinicie el servicio SMS_Executive.  

Para usar el Administrador de servicios de Configuration Manager, en la consola, vaya a **Supervisión** > **Estado del sistema** > **Estado del componente**, haga clic en **Iniciar** y, después, seleccione **Administrador de servicios de Configuration Manager**. En el Administrador de servicios:  

- En el panel de navegación, expanda el sitio, expanda **Componentes** y, después, seleccione el componente que quiera reiniciar.  

- En el panel de detalles, haga clic con el botón derecho en el componente y, después, seleccione **Consulta**.  

- Cuando se confirme el estado del componente, haga clic con el botón derecho en el componente y seleccione **Detener**.  

- **Consulte** el componente de nuevo para confirmar que se ha detenido. Haga clic en el componente una vez más y después elija **Iniciar**.  

> [!IMPORTANT]  
> El proceso que agrega una suscripción de Microsoft Intune al punto de conexión de servicio establece automáticamente el rol de sistema de sitio en el modo con conexión. El punto de conexión de servicio no admite el modo sin conexión cuando se configura con una suscripción de Intune.  

**Si se instala el rol en un equipo remoto con respecto al servidor de sitio:**  

- La cuenta de equipo del servidor de sitio tiene que ser un administrador local del equipo que hospeda una conexión de servicio remoto.

- Necesita configurar el servidor de sistema de sitio que hospeda el rol con una cuenta de instalación de sistema de sitio.  

- El administrador de distribución del servidor de sitio usa la cuenta de instalación de sistema de sitio para transferir las actualizaciones desde el punto de conexión de servicio.

##  <a name="bkmk_urls"></a> Requisitos de acceso a Internet  
Para permitir la operación, el equipo que hospeda el punto de conexión de servicio y los firewalls entre dicho equipo e Internet deben pasar las comunicaciones a través del puerto de salida **TCP 443** para HTTPS y el puerto de salida **TCP 80** para HTTP a las siguientes ubicaciones de Internet. El punto de conexión de servicio también admite el uso de un servidor proxy web (con o sin autenticación) para acceder a estas ubicaciones. Si necesita configurar una cuenta de proxy web, vea [Compatibilidad con servidores proxy](/sccm/core/plan-design/network/proxy-server-support).

> [!TIP]  
> El punto de conexión de servicio usa el servicio de Microsoft Intune cuando se conecta a go.microsoft.com o manage.Microsoft.com. Hay un problema conocido por el que el conector de Intune experimenta problemas de conectividad si no está instalado el certificado raíz de Baltimore CyberTrust, si ha expirado o si está dañado en el punto de conexión de servicio. Para obtener más información, vea [Service connection point doesn't download updates](https://support.microsoft.com/help/3187516) (El punto de conexión de servicio no descarga las actualizaciones).  

#### <a name="updates-and-servicing"></a>Actualizaciones y mantenimiento

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

#### <a name="microsoft-intune"></a>Microsoft Intune

- `*manage.microsoft.com`  

- `https://bspmts.mp.microsoft.com/V`  

- `https://login.microsoftonline.com/{TenantID}`  

#### <a name="windows-10-servicing"></a>Servicio de actualización de Windows 10

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

#### <a name="azure-services"></a>Servicios de Azure

- `management.azure.com`  

## <a name="install-the-service-connection-point"></a>Instalar el punto de conexión de servicio
Cuando ejecute **Configurar** para instalar el sitio de nivel superior de una jerarquía, tendrá la opción de instalar el punto de conexión de servicio.

Después de ejecutar el programa de instalación o de reinstalar el rol de sistema de sitio, use el **Asistente para agregar roles de sistema de sitio** o el **Asistente para crear servidor de sistema de sitio** para instalar el sistema de sitio en un servidor en el sitio de nivel superior de la jerarquía (es decir, el sitio de administración central o un sitio primario independiente). Los dos asistentes se encuentran en la pestaña **Inicio** de la consola, en **Administración** > **Configuración de sitio** > **Servidores y roles del sistema de sitios**.



## <a name="log-files-used-by-the-service-connection-point"></a>Archivos de registro usados por el punto de conexión de servicio
Para consultar información sobre las cargas en Microsoft, vea **Dmpuploader.log** en el equipo en que se ejecuta el punto de conexión de servicio.  Para las descargas, incluido el progreso de descarga de las actualizaciones, vea **Dmpdownloader.log**. Para obtener la lista completa de registros relacionados con el punto de conexión de servicio, consulte [Punto de conexión de servicio](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog) en el artículo de archivos de registro de Configuration Manager.

También puede utilizar los diagramas de flujo siguientes para conocer el flujo del proceso y las entradas del registro de claves para descargas de actualización y replicación de actualizaciones en otros sitios:
- [Diagrama de flujo: descargar actualizaciones](/sccm/core/servers/manage/download-updates-flowchart)
- [Diagrama de flujo: replicación de actualización](/sccm/core/servers/manage/update-replication-flowchart)
