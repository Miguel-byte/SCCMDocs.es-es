---
title: "Punto de conexión de servicio | Microsoft Docs"
description: "Obtenga información sobre este rol de sistema de sitio de Configuration Manager y comprenda y planee sus diversos usos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
caps.latest.revision: 18
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 8195abd403d94a96d193289ea6e6bf8880d06078
ms.openlocfilehash: aaa9a80a8429ab315a25862a78d6eb8733fd2e89


---
# <a name="about-the-service-connection-point-in-system-center-configuration-manager"></a>Acerca del punto de conexión de servicio en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

El punto de conexión de servicio de System Center Configuration Manager es un rol de sistema de sitio que realiza varias funciones importantes para la jerarquía. Antes de configurar el punto de conexión de servicio, es conveniente conocer y planear sus diversos usos que pueden afectar el modo de configuración de este rol de sistema de sitio:  

-   **Administrar dispositivos móviles con Microsoft Intune**: este rol reemplaza al conector de Windows Intune que se usaba en las versiones anteriores de Configuration Manager y se puede configurar con los detalles de la suscripción de Intune. Vea [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune (Administración híbrida de dispositivos móviles (MDM) con System Center Configuration Manager y Microsoft Intune)](../../../../mdm/understand/hybrid-mobile-device-management.md)  

-   **Administrar dispositivos móviles con MDM local**: este rol proporciona compatibilidad con los dispositivos locales que administra que no se conectan a Internet. Vea [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager (Administrar dispositivos móviles con la infraestructura local en System Center Configuration Manager)](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)  

-   **Cargar datos de uso de la infraestructura de Configuration Manager**: puede controlar el nivel o la cantidad de detalle que se carga. Los datos cargados nos ayudan a:  

    -   Identificar y solucionar problemas de forma proactiva  

    -   Mejorar nuestros productos y servicios  

    -   Identificar las actualizaciones de Configuration Manager que se aplican a la versión de Configuration Manager actualmente en uso  

     Vea [Usage data levels and settings (Niveles de datos de uso y configuración)](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

-   **Descargar las actualizaciones que se aplican a la infraestructura de Configuration Manager**: solo estarán disponibles las actualizaciones apropiadas para la infraestructura, según los datos de uso que se carguen.  

 **Cada jerarquía admite una única instancia de este rol:**  

-   El rol de sistema de sitio solo puede instalarse en el sitio de nivel superior de la jerarquía (es decir, un sitio de administración central o el sitio primario independiente).  

-   Si expande un sitio primario independiente a una jerarquía más grande, debe desinstalar este rol desde el sitio primario y luego puede instalar en el sitio de administración central.  

##  <a name="a-namebkmkmodesa-modes-of-operation"></a><a name="bkmk_modes"></a> Modos de operación  
 El punto de conexión de servicio admite dos modos de funcionamiento:  

-   En el **modo en línea**, el punto de conexión de servicio comprueba automáticamente cada 24 horas si existen actualizaciones y, luego, descarga las nuevas actualizaciones disponibles para la infraestructura y la versión del producto actuales, de manera que estén disponibles en la consola de Configuration Manager.  

-   En el **modo sin conexión**, el punto de conexión de servicio no se conecta al servicio en la nube de Microsoft y es necesario el [Uso de la herramienta de conexión de servicio para System Center Configuration Manager](../../../../core/servers/manage/use-the-service-connection-tool.md) manual para importar las actualizaciones disponibles  

Al cambiar el modo entre en línea o sin conexión después de haber instalado el punto de conexión de servicio, debe reiniciar el subproceso SMS_DMP_DOWNLOADER del servicio SMS_Executive de Configuration Manager para que este cambio sea efectivo.  Para ello, use el Administrador de servicios de Configuration Manager para reiniciar solo el subproceso SMS_DMP_DOWNLOADER del servicio SMS_Executive.  También puede reiniciar el servicio SMS_Executive para Configuration Manager (que reinicia la mayoría de los componentes del sitio) o esperar a que una tarea de programación lo haga en su nombre, como una copia de seguridad de sitio, que detiene y luego reinicia SMS_Executive.  

Para usar el Administrador de servicios de Configuration Manager, en la consola, vaya a **Supervisión** > **Estado del sistema** > **Estado del componente**, haga clic en **Iniciar** y seleccione **Administrador de servicios de Configuration Manager**.  En el Administrador de servicios:  

-   En el panel de navegación, expanda el sitio y los **Componentes** y seleccione el componente que desea reiniciar.  

-   En el panel de detalles, haga clic con el botón derecho en el componente y seleccione **Consultar**.  

-   Una vez que se confirma el estado del componente, haga clic con el botón derecho en el componente y seleccione **Detener**.  

-   **Consulte** el componente de nuevo para confirmar que se ha detenido y, después, haga clic con el botón derecho en el componente una vez más y seleccione **Iniciar**.  

> [!IMPORTANT]  
>  Cuando se agrega una suscripción de Microsoft Intune al punto de conexión de servicio, esta establece automáticamente el rol de sistema de sitio en el modo en línea. El punto de conexión de servicio no admite el modo sin conexión cuando se configura con una suscripción de Intune.  

**Si se instala el rol en un equipo remoto con respecto al servidor de sitio:**  

-   La cuenta de equipo del servidor del sitio debe ser un administrador local del equipo que hospeda una conexión de servicio remoto

-   Debe configurar el servidor de sistema de sitio que hospeda el rol con una cuenta de instalación de sistema de sitio  

-   El administrador de distribución usa dicha cuenta en el servidor de sitio para transferir las actualizaciones desde el punto de conexión de servicio

##  <a name="a-namebkmkurlsa-internet-access-requirements"></a><a name="bkmk_urls"></a> Requisitos de acceso a Internet  
Para permitir la operación, el equipo que hospeda el punto de conexión de servicio y los firewalls entre dicho equipo e Internet deben pasar las comunicaciones a través de **el puerto TCP 443** a las siguientes ubicaciones de Internet. El punto de conexión de servicio también admite el uso de un servidor proxy web (con o sin autenticación) para tener acceso a estas ubicaciones.  

**Actualizaciones y mantenimiento**  

-   *.akamaiedge.net  

-   *.manage.microsoft.com

-   go.microsoft.com

-   blob.core.windows.net  

-   download.microsoft.com  

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

Después de la ejecución de la configuración, o bien si reinstala el rol de sistema de sitio, use el Asistente para **agregar roles de sistema de sitio** o el Asistente para **crear servidor de sistema de sitio** para instalar el sistema de sitio en un servidor en el sitio de nivel superior de la jerarquía (el sitio de administración central o un sitio primario independiente).  Ambos asistentes se encuentran en la pestaña **Inicio** de la consola, en **Administración** > **Configuración de sitio** > **Servidores y roles del sistema de sitios**.



<!--HONumber=Dec16_HO3-->


