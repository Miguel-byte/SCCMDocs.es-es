---
title: "Novedades de la versión 1602 de System Center Configuration Manager | Microsoft Docs"
description: "Obtenga detalles sobre los cambios y las nuevas funciones introducidas en la versión 1602 de System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 9a548f43625a907173e7b967d26356bd80f1c5d9
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017

---
# <a name="what39s-new-in-version-1602-of-system-center-configuration-manager"></a>Novedades de la versión 1602 de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


La actualización 1602 para System Center Configuration Manager solo está disponible como una actualización en consola para sitios instalados previamente que ejecutan la versión 1511. La versión 1511 es la versión de línea base inicial que se usa para instalar sitios nuevos de Configuration Manager.  


> [!TIP]  
>  Más información acerca de:  
>   
>   -   [Instalación de nuevos sitios](/sccm/core/servers/deploy/install) (con una versión de línea base como 1511)  
>   -   [Instalación de actualizaciones en los sitios](/sccm/core/servers/manage/updates) (como la actualización 1602)  

 En las secciones siguientes se proporcionan detalles sobre los cambios y las nuevas funciones introducidas en la versión 1602 de Configuration Manager.  

## <a name="site-infrastructure"></a>Infraestructura del sitio  

###  <a name="bkmk_UpgradeOS"></a> Actualización inmediata del sistema operativo de los servidores del sitio que ejecutan Windows Server 2008 R2  
 Los sitios de Configuration Manager que ejecutan la versión 1602 o versiones posteriores admiten la actualización inmediata del sistema operativo de los servidores del sitio desde Windows Server 2008 R2 a Windows Server 2012 R2.  

> [!WARNING]  
>  Antes de actualizar a Windows Server 2012 R2, debe desinstalar WSUS 3.2 del servidor.  
>   
>  Para obtener más información sobre este paso crítico, vea la sección "Funcionalidad nueva y modificada" en [Introducción a Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) en la documentación de Windows Server.  

 Para actualizar un servidor, use los procedimientos de actualización de Windows Server 2012 R2. No es necesario ejecutar una restauración del servidor de sitio de Configuration Manager después de la actualización. Para conocer los procedimientos de actualización, consulte [Opciones de actualización para Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) en la documentación de Windows Server.  

###  <a name="bkmk_AOAG"></a> Grupos de disponibilidad AlwaysOn de SQL Server  
 Use grupos de disponibilidad AlwaysOn de SQL Server para hospedar la base de datos de sitio en sitios primarios y el sitio de administración central como una solución de alta disponibilidad y recuperación ante desastres.  

 Para obtener más información, vea [SQL Server AlwaysOn para una base de datos de sitio de alta disponibilidad para System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

## <a name="operating-system-deployment"></a>Implementación de sistema operativo  

### <a name="windows-10-servicing"></a>Servicio de actualización de Windows 10  
 Se han agregado las siguientes mejoras para el mantenimiento de Windows 10 en la versión 1602 de Configuration Manager:  

-   Hay nuevas opciones de filtro disponibles para planes de mantenimiento que le permiten filtrar por **idioma**, **carácter obligatorio** y **título**. Solo se agregarán a la implementación asociada las actualizaciones que cumplan con los criterios especificados.  

-   Cuando selecciona la clasificación **Actualizaciones** para la sincronización de actualizaciones de software, se muestra una advertencia. Esta advertencia le permite conocer que se necesita la [revisión 3095113](https://support.microsoft.com/kb/3095113) para Windows Server Update Services (WSUS) 4.0 antes de que pueda sincronizar correctamente las actualizaciones de software, y para que el mantenimiento de Windows 10 funcione correctamente. Desde el mensaje de advertencia, puede ir al artículo de Knowledge Base correspondiente.  

-   Ahora las actualizaciones de Windows 10 disponibles solo se muestran en el nodo **Mantenimiento de Windows 10** \ **Todas las actualizaciones de Windows 10** de la consola de Configuration Manager. Estas actualizaciones ya no se mostrarán en el nodo **Actualizaciones de Software** \ **Todas las actualizaciones de software** de la consola.  

-   Un plan de mantenimiento se considera una implementación de alto riesgo, y la ventana **Seleccionar recopilación** muestra solo las recopilaciones personalizadas que cumplen con la configuración de comprobación de implementación que está configurada en las propiedades del sitio. Para obtener más información, consulte [Settings to manage high-risk deployments for System Center Configuration Manager](../../../protect/understand/settings-to-manage-high-risk-deployments.md) (Configuración para administrar implementaciones de alto riesgo para System Center Configuration Manager).  

-   Los usuarios que inician un paquete de actualizaciones de Windows 10 ahora reciben un mensaje de que se actualizará su sistema operativo.  

## <a name="application-management"></a>Administración de aplicaciones  

### <a name="ios-app-configuration-policies"></a>Directivas de configuración de aplicaciones de iOS  
 Use las directivas de configuración de aplicaciones de Configuration Manager para proporcionar la configuración que puede ser necesaria cuando el usuario ejecuta una aplicación de iOS. Por ejemplo, una aplicación puede requerir que el usuario especifique un número de puerto personalizado, idioma, configuración de seguridad o configuración de marca (como un logotipo de empresa). Si se ha especificado esta configuración incorrectamente, puede aumentar la carga del departamento de soporte técnico y ralentizar la adopción de nuevas aplicaciones.  

 Las directivas de configuración de aplicaciones pueden ayudarle a eliminar estos problemas al permitirle implementar esta configuración para los usuarios en una directiva, antes de que ejecuten la aplicación. Después, la configuración se proporciona de manera automática y el usuario no necesita realizar ninguna acción. Para obtener más información, consulte [Configure iOS apps with app configuration policies in System Center Configuration Manager](../../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md) (Configurar aplicaciones de iOS con directivas de configuración de aplicaciones en System Center Configuration Manager).  

### <a name="manage-volume-purchased-ios-apps"></a>Manage volume-purchased iOS apps  
 Configuration Manager puede ayudarle a implementar y administrar aplicaciones que ha adquirido en volumen desde el Programa de Compras por Volumen de Apple (VPP). Configuration Manager importa la información de licencia desde la tienda de aplicaciones y realiza un seguimiento de cuántas licencias ha usado.  

 Para obtener más información, consulte [Manage volume-purchased iOS apps with System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md) (Administrar aplicaciones de iOS compradas por volumen con System Center Configuration Manager).  

### <a name="automatic-creation-of-office-mobile-apps"></a>Creación automática de aplicaciones móviles de Office  
 Cuando se actualiza a la versión 1602 desde 1511, Configuration Manager crea automáticamente las siguientes aplicaciones móviles de Microsoft Office para iOS y Android:  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (solo iOS)  

-   Microsoft Outlook  

Encontrará estas aplicaciones en el nodo **Aplicaciones** de la consola de Configuration Manager.  

 Para obtener más información sobre cómo implementar aplicaciones, consulte [How to deploy applications with System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md) (Implementación de aplicaciones con System Center Configuration Manager).  

## <a name="software-updates"></a>Actualizaciones de software  

### <a name="manage-office-365-client-updates"></a>Administración de las actualizaciones de cliente de Office 365  
 System Center Configuration Manager tiene la capacidad de administrar las actualizaciones del cliente de Office 365 mediante el flujo de trabajo de administración de actualizaciones de software. Para más información, consulte [Manage Office 365 ProPlus updates with System Center Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates) (Administración de actualizaciones de Office 365 ProPlus con System Center Configuration Manager).  

## <a name="compliance-settings"></a>Configuración de cumplimiento  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Configuración de cumplimiento para dispositivos que ejecutan Windows 10 Team  
 Se han agregado opciones de configuración nuevas al elemento de configuración de **Windows 8.1 y Windows 10**. Estas opciones de configuración le ayudan a controlar dispositivos que ejecutan Windows 10 Team, como un dispositivo de Surface Hub.  

 Para obtener más información, consulte [How to create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client](../../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md) (Creación de elementos de configuración para dispositivos de Windows 8.1 y Windows 10 administrados sin el cliente de System Center Configuration Manager).  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Configuración de pantalla completa para dispositivos Android Samsung KNOX Standard  
 El modo de pantalla completa le permite bloquear un dispositivo para que solo funcionen determinadas características. Por ejemplo, puede permitir que un dispositivo ejecute solo una aplicación administrada que especifique, o puede deshabilitar los botones de volumen de un dispositivo. Esta configuración podría usarse para un modelo de demostración de un dispositivo o para un dispositivo que está dedicado a realizar solo una función, como un dispositivo de punto de venta. En Configuration Manager, ahora puede especificar la configuración de pantalla completa para dispositivos Samsung KNOX Standard.  

 Para obtener más información, consulte [Crear elementos de configuración para dispositivos Android y Samsung KNOX Standard administrados sin el cliente de System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).  

## <a name="conditional-access"></a>Acceso condicional  

### <a name="conditional-access-for-pcs-managed-by-system-center-configuration-manager"></a>Acceso condicional para equipos administrados por System Center Configuration Manager  
 Antes de esta versión, para configurar el acceso condicional para un equipo, dicho equipo debía estar inscrito en Intune o ser un equipo unido a un dominio. A partir de la actualización 1602, se admite el acceso condicional para equipos administrados por System Center Configuration Manager. Para los equipos administrados por System Center Configuration Manager, puede restringir el acceso a Exchange Online y SharePoint Online solo para los dispositivos que sean conformes con las directivas de cumplimiento que configure.  

 Para obtener más información, consulte [Manage access to O365 services for PCs managed by System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md) (Administración del acceso a servicios de O365 para equipos administrados por System Center Configuration Manager).  

### <a name="restricting-access-based-on-the-health-of-devices"></a>Restringir el acceso basándose en el estado de los dispositivos  
 Ahora puede restringir el acceso a los servicios de correo electrónico y Office 365 según el estado de los dispositivos, como ha notificado el Servicio de atestación de estado. Además, los dispositivos administrados por Intune se incluyen en los informes de estado de dispositivos.  

 La consola de Configuration Manager presenta una nueva regla de cumplimiento que le permite especificar si debe permitir o bloquear el acceso de los dispositivos en función de su estado de mantenimiento. Para obtener más información sobre el servicio de atestación de estado y cómo se notifica el estado de los dispositivos en Intune, vea [Atestación de estado para System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="new-compliance-policy-rules"></a>Nuevas reglas de directivas de cumplimiento  
 Se han agregado nuevas reglas de directivas de cumplimiento, como actualizaciones automáticas y pedir una contraseña para desbloquear dispositivos, para admitir mejores requisitos de seguridad.

 Para obtener más información, consulte [Device compliance policies in System Center Configuration Manager](../../../protect/deploy-use/device-compliance-policies.md) (Directivas de cumplimiento de dispositivos en System Center Configuration Manager).  

### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Comprobación de que los dispositivos inscritos y conformes siempre tengan acceso a Exchange local  
 Cuando activa la siguiente opción, los dispositivos que están inscritos en Intune, y son conformes con las directivas de cumplimiento, pueden acceder a Exchange local: **Sustitución de la regla predeterminada: permitir siempre que los dispositivos inscritos y conformes de Intune tengan acceso a Exchange local:**. Esta regla está disponible en la **página General** del **Asistente de configuración de directivas de acceso condicional** para Exchange local.

 Esta regla invalida la regla predeterminada, lo que significa que aunque establezca dicha regla en Cuarentena o Bloquear el acceso, los dispositivos inscritos y conformes seguirán teniendo acceso a Exchange local. Use esta opción cuando quiera que los dispositivos inscritos y conformes a las directivas siempre tengan acceso a correo electrónico a través de Exchange local.   

 Para obtener un tutorial detallado, consulte [Manage email access in System Center Configuration Manager](../../../protect/deploy-use/manage-email-access.md) (Administración del acceso a correo electrónico en System Center Configuration Manager).  

## <a name="client-management"></a>Administración de cliente  

### <a name="client-online-status"></a>Estado de conexión de clientes  
 Hay un nuevo estado disponible para los clientes para supervisar si un equipo está conectado o no. Un equipo se considera en línea si está conectado a su punto de administración asignado. Para indicar que el equipo está en línea, el cliente envía mensajes similares a Ping al punto de administración. Si el punto de administración no recibe un mensaje después de 5 minutos, el cliente se considera sin conexión.  

 Para obtener más información, consulte [How to monitor clients in System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md) (Supervisión de clientes en System Center Configuration Manager).  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Actualizar la directiva de usuario y máquina desde el Centro de software  
 Se ha agregado una nueva opción, **Directiva de sincronización**, a la página **Opciones** > **Mantenimiento del equipo** del Centro de software que hace que el equipo actualice su directiva de usuario y máquina de Configuration Manager.  

### <a name="software-center-branding-changes"></a>Personalización del Centro de software  
 Puede cambiar el color, el nombre de la organización y el icono que aparece en el Centro de software. Esta configuración se aplica según las reglas siguientes:  

- Si no está instalado el rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones, el Centro de software mostrará el nombre de organización especificado en la configuración cliente **Agente de equipo** denominada **Nombre de organización mostrado en el Centro de software**.  

- Si está instalado el rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones, el Centro de software mostrará el nombre de la organización y el color especificados en las propiedades del rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones.  

- Si una suscripción de Microsoft Intune está configurada y conectada al entorno de Configuration Manager, el Centro de software mostrará el nombre de la organización, el color y el logotipo de la empresa especificados en las propiedades de la suscripción de Intune.  

### <a name="health-attestation"></a>Atestación de estado  
 Los administradores pueden ver el estado de la atestación de estado de los dispositivos de Windows 10 en la consola de Configuration Manager. Está disponible para Configuration Manager, así como para Configuration Manager con Microsoft Intune. La atestación de estado del dispositivo permite al administrador garantizar que los equipos cliente tienen habilitadas las siguientes configuraciones BIOS, TPM y de software de arranque de confianza:  

-   Antimalware de inicio temprano  

-   BitLocker  

-   Arranque seguro  

-   Integridad de código  

Para obtener más información, consulte [Health attestation for System Center Configuration Manager](../../../core/servers/manage/health-attestation.md) (Atestación de estado para System Center Configuration Manager).  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Mejoras en la configuración antimalware de Endpoint Protection  
 1602 agrega las nuevas opciones de configuración siguientes a la directiva antimalware de Endpoint Protection para Windows Defender:  

-   Protección en tiempo real: bloquear aplicaciones potencialmente no deseadas en la descarga, antes de la instalación.  

-   Configuración de exploración: examinar unidades de red asignadas durante un examen completo  

-   Configuración de envío automático de archivos de ejemplo:  

     El motor de antimalware puede solicitar ejemplos de archivo que se enviarán a Microsoft para un análisis más profundo. De forma predeterminada, siempre se le preguntará antes de enviar dichos ejemplos. Los administradores pueden administrar ahora las siguientes opciones para configurar este comportamiento:  

    -   Avanzado: habilitar el envío automático de archivos de ejemplo para ayudar a Microsoft a averiguar si ciertos elementos encontrados son malintencionados.  

    -   Avanzado: permitir a los usuarios modificar la configuración de envío automático de archivos de ejemplo.  

    Además, en la sección "Configuración de exclusión" de la directiva antimalware de Endpoint Protection, la configuración **Excluir archivos y carpetas** existente ahora permite exclusiones del dispositivo.  

Para obtener más información, consulte [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-antimalware-policies.md) (Creación e implementación de directivas antimalware para Endpoint Protection en System Center Configuration Manager).  

## <a name="mobile-device-management"></a>Administración de dispositivos móviles  

### <a name="ios-activation-lock"></a>Bloqueo de activación de iOS  
 Configuration Manager puede ayudarle a administrar el bloqueo de activación de iOS, una característica de la aplicación Buscar mi iPhone disponible en iOS 7.1 y en dispositivos más modernos. El bloqueo de activación se habilita automáticamente cuando se usa la aplicación Buscar mi iPhone en un dispositivo. Tras su activación, se debe escribir el identificador y la contraseña de Apple del usuario para poder:  

-   Desactivar Buscar mi iPhone.  

-   Borrar el dispositivo.  

-   Reactivar el dispositivo.  

Configuration Manager puede solicitar el estado de bloqueo de activación de los dispositivos supervisados y no supervisados que ejecutan iOS 7.1 y versiones posteriores. Para los dispositivos supervisados, Configuration Manager puede recuperar el código de omisión de bloqueo de activación y emitirlo directamente al dispositivo.  

 Para obtener más información, consulte [Help protect iOS devices with Activation Lock bypass in System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock) (Ayudar a proteger dispositivos iOS con omisión del bloqueo de activación en System Center Configuration Manager).  

### <a name="monitor-terms-and-conditions-deployments"></a>Supervisión de las implementaciones de términos y condiciones  
 Puede supervisar las implementaciones de términos y condiciones en la consola de Configuration Manager.  

 Seleccione la implementación de términos y condiciones de la lista de implementaciones. El área de resumen muestra las estadísticas siguientes:  

-   **Conforme**: los usuarios han aceptado la versión más reciente de los términos y condiciones.  

-   **Error**  

-   **No conforme**: los usuarios han aceptado una versión de los términos y condiciones, pero no la más reciente.  

-   **Desconocido**: los usuarios no han aceptado nunca los términos y condiciones, incluidos aquellos sin un dispositivo inscrito.  

