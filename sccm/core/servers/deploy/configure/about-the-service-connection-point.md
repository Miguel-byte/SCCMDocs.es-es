---
title: "Punto de conexión de servicio | Microsoft Docs"
description: "Obtenga información sobre este rol de sistema de sitio de Configuration Manager y comprenda y planee sus diversos usos."
ms.custom: na
ms.date: 6/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
caps.latest.revision: "18"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: e3d41dc1bb732e887d722f39ee86deaf0aae3240
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="about-the-service-connection-point-in-system-center-configuration-manager"></a>Acerca del punto de conexión de servicio en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

El punto de conexión de servicio de System Center Configuration Manager es un rol de sistema de sitio que realiza varias funciones importantes para la jerarquía. Antes de configurar el punto de conexión de servicio, le recomendamos que comprenda y planee los diferentes usos que puedan afectar a la forma de configurar este rol de sistema de sitio:  

-   **Administrar dispositivos móviles con Microsoft Intune**: este rol reemplaza al conector de Windows Intune que se usaba en las versiones anteriores de Configuration Manager y se puede configurar con los detalles de la suscripción de Intune. Consulte [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../../mdm/understand/hybrid-mobile-device-management.md) (Administración híbrida de dispositivos móviles (MDM) con System Center Configuration Manager y Microsoft Intune).  

-   **Administrar dispositivos móviles con MDM local**: este rol ofrece compatibilidad con los dispositivos locales que administra y que no se conectan a Internet. Consulte [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) (Administrar dispositivos móviles con la infraestructura local en System Center Configuration Manager).  

-   **Cargar datos de uso desde la infraestructura de Configuration Manager**: puede controlar el nivel o la cantidad de detalle que se sube. Los datos cargados nos ayudan a:  

    -   Identificar y solucionar problemas de forma proactiva  

    -   Mejorar nuestros productos y servicios  

    -   Identificar las actualizaciones de Configuration Manager válidas para la versión de Configuration Manager que use  

  Para más información sobre los datos que recopila cada nivel y sobre cómo cambiar el nivel de recopilación después de instalar el rol, vea [Diagnósticos y datos de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data) y, después, siga el vínculo de la versión de Configuration Manager que use.  

  Para obtener más información, consulte [Configuración y niveles de datos de uso](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

-   **Descargar las actualizaciones válidas para la infraestructura de Configuration Manager**: solo estarán disponibles las actualizaciones apropiadas para la infraestructura, según los datos de uso que suba.  

- **Cada jerarquía admite una única instancia de este rol:**  

 -   El rol de sistema de sitio solo se puede instalar en el sitio de nivel superior de la jerarquía (es decir, un sitio de administración central o un sitio primario independiente).  

  -   Si expande un sitio primario independiente a una jerarquía más grande, tendrá que desinstalar este rol desde el sitio primario para instalarlo en el sitio de administración central.  


##  <a name="bkmk_modes"></a> Modos de operación  
 El punto de conexión de servicio admite dos modos de funcionamiento:  

-   En el **modo con conexión**, el punto de conexión de servicio comprueba automáticamente cada 24 horas si existen actualizaciones y, después, descarga las nuevas actualizaciones disponibles para la infraestructura y la versión del producto actuales para que estén disponibles en la consola de Configuration Manager.  

-   En el **modo sin conexión**, el punto de conexión de servicio no se conecta al servicio en la nube de Microsoft y tendrá que usar de forma manual la [herramienta de conexión de servicio para System Center Configuration Manager](../../../../core/servers/manage/use-the-service-connection-tool.md) para importar las actualizaciones disponibles.  

Al cambiar entre los modos con conexión o sin conexión después de instalar el punto de conexión de servicio, tendrá que reiniciar el subproceso SMS_DMP_DOWNLOADER del servicio SMS_Executive de Configuration Manager para que se aplique el cambio. Para ello, use el Administrador de servicios de Configuration Manager para reiniciar solo el subproceso SMS_DMP_DOWNLOADER del servicio SMS_Executive. También puede reiniciar el servicio SMS_Executive para Configuration Manager (que reinicia la mayoría de los componentes de sitio) o puede esperar hasta que se ejecute una tarea programada (como una copia de seguridad de sitio, que detiene y, después, reinicia automáticamente el servicio SMS_Executive).  

Para usar el Administrador de servicios de Configuration Manager, en la consola, vaya a **Supervisión** > **Estado del sistema** > **Estado del componente**, haga clic en **Iniciar** y, después, seleccione **Administrador de servicios de Configuration Manager**. En el Administrador de servicios:  

-   En el panel de navegación, expanda el sitio, expanda **Componentes** y, después, seleccione el componente que quiera reiniciar.  

-   En el panel de detalles, haga clic con el botón derecho en el componente y, después, seleccione **Consulta**.  

-   Cuando se confirme el estado del componente, haga clic con el botón derecho en el componente y seleccione **Detener**.  

-   Vuelva a **consultar** el componente para confirmar que se ha detenido, vuelva a hacer clic con el botón derecho en el componente y, después, seleccione **Iniciar**.  

> [!IMPORTANT]  
>  El proceso que agrega una suscripción de Microsoft Intune al punto de conexión de servicio establece automáticamente el rol de sistema de sitio en el modo con conexión. El punto de conexión de servicio no admite el modo sin conexión cuando se configura con una suscripción de Intune.  

**Si se instala el rol en un equipo remoto con respecto al servidor de sitio:**  

-   La cuenta de equipo del servidor de sitio tiene que ser un administrador local del equipo que hospeda una conexión de servicio remoto.

-   Necesita configurar el servidor de sistema de sitio que hospeda el rol con una cuenta de instalación de sistema de sitio.  

-   El administrador de distribución del servidor de sitio usa la cuenta de instalación de sistema de sitio para transferir las actualizaciones desde el punto de conexión de servicio.

##  <a name="bkmk_urls"></a> Requisitos de acceso a Internet  
Para permitir la operación, el equipo que hospeda el punto de conexión de servicio y los firewalls entre dicho equipo e Internet deben pasar las comunicaciones a través de **el puerto TCP 443** y el **puerto TCP 443** a las siguientes ubicaciones de Internet. El punto de conexión de servicio también admite el uso de un servidor proxy web (con o sin autenticación) para acceder a estas ubicaciones.  Si necesita configurar una cuenta de proxy web, consulte [Compatibilidad de servidor proxy en System Center Configuration Manager](/sccm/core/plan-design/network/proxy-server-support).

**Actualizaciones y mantenimiento**  

-   *.akamaiedge.net  

-   *.akamaitechnologies.com 

-   *.manage.microsoft.com

-   go.microsoft.com

-   blob.core.windows.net  

-   download.microsoft.com  

-   download.windowsupdate.com

-   sccmconnected-a01.cloudapp.net  

**Microsoft Intune**  

-   *manage.microsoft.com  
-   https://bspmts.mp.microsoft.com/V
-   https://login.microsoftonline.com/{TenantID}


**Mantenimiento de Windows 10**  

-   download.microsoft.com  

-   https://go.microsoft.com/fwlink/?LinkID=619849  

## <a name="install-the-service-connection-point"></a>Instalar el punto de conexión de servicio
Cuando ejecute **Configurar** para instalar el sitio de nivel superior de una jerarquía, tendrá la opción de instalar el punto de conexión de servicio.

Después de ejecutar el programa de instalación o de reinstalar el rol de sistema de sitio, use el **Asistente para agregar roles de sistema de sitio** o el **Asistente para crear servidor de sistema de sitio** para instalar el sistema de sitio en un servidor en el sitio de nivel superior de la jerarquía (es decir, el sitio de administración central o un sitio primario independiente). Los dos asistentes se encuentran en la pestaña **Inicio** de la consola, en **Administración** > **Configuración de sitio** > **Servidores y roles del sistema de sitios**.

## <a name="log-files-used-by-the-service-connection-point"></a>Archivos de registro usados por el punto de conexión de servicio
Para consultar información sobre las cargas en Microsoft, vea **Dmpuploader.log** en el equipo en que se ejecuta el punto de conexión de servicio.  Para las descargas, incluido el progreso de descarga de las actualizaciones, vea **Dmpdownloader.log**. Para obtener la lista completa de registros relacionados con el punto de conexión de servicio, vea [Punto de conexión de servicio](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog) en el tema de archivos de registro de Configuration Manager.

También puede utilizar los diagramas de flujo siguientes para conocer el flujo del proceso y las entradas del registro de claves para descargas de actualización y replicación de actualizaciones en otros sitios:
 - [Diagrama de flujo: descargar actualizaciones](/sccm/core/servers/manage/download-updates-flowchart)
 - [Diagrama de flujo: replicación de actualización](/sccm/core/servers/manage/update-replication-flowchart)
