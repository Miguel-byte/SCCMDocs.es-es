---
title: "Novedades de la versión 1602 | Microsoft Docs"
description: "Obtenga detalles sobre los cambios y las nuevas funciones introducidas en la versión 1602 de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 4d7b93c95730edde3af254e813c72df279c7285d

---
# <a name="what39s-new-in-version-1602-of-system-center-configuration-manager"></a>Novedades de la versión 1602 de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


La actualización 1602 para System Center Configuration Manager es una actualización que está disponible solo en consola para los sitios instalados previamente que ejecutan la versión 1511. La versión 1511 es la versión de línea base inicial que se usa para instalar sitios nuevos de Configuration Manager.  


> [!TIP]  
>  Más información acerca de:  
>   
>   -   [Instalación de nuevos sitios](/sccm/core/servers/deploy/install) (con una versión de línea base como 1511)  
>   -   [Instalación de actualizaciones en los sitios](/sccm/core/servers/manage/updates) (como la actualización 1602)  

 En las secciones siguientes se proporcionan detalles sobre los cambios y las nuevas funciones introducidas en la versión 1602 de Configuration Manager.  

## <a name="site-infrastructure"></a>Infraestructura del sitio  

###  <a name="a-namebkmkupgradeosa-in-place-upgrade-the-operating-system-of-site-servers-that-run-windows-server-2008-r2"></a><a name="bkmk_UpgradeOS"></a> Actualización inmediata del sistema operativo de los servidores del sitio que ejecutan Windows Server 2008 R2  
 Los sitios de Configuration Manager que ejecutan la versión 1602 o versiones posteriores admiten la actualización inmediata del sistema operativo de los servidores del sitio desde Windows Server 2008 R2 a Windows Server 2012 R2.  

> [!WARNING]  
>  Antes de actualizar a Windows Server 2012 R2, **debe desinstalar WSUS 3.2** del servidor.  
>   
>  Para obtener más información acerca de este paso crítico, consulte la sección Funcionalidad nueva y modificada en [Introducción a Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) en la documentación de Windows Server.  

 Para actualizar un servidor, se usan los procedimientos de actualización de Windows Server 2012 R2 y no es necesario ejecutar una restauración del servidor de sitio de Configuration Manager después de la actualización.  Para conocer los procedimientos de actualización, consulte [Opciones de actualización para Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) en la documentación de Windows Server.  

###  <a name="a-namebkmkaoaga-sql-server-alwayson-availability-groups"></a><a name="bkmk_AOAG"></a> Grupos de disponibilidad AlwaysOn de SQL Server  
 Use grupos de disponibilidad AlwaysOn de SQL Server para hospedar la base de datos de sitio en sitios primarios y el sitio de administración central como una solución de alta disponibilidad y recuperación ante desastres.  

 Para más información, consulte [SQL Server AlwaysOn for a highly available site database for System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) (SQL Server AlwaysOn para una base de datos de sitio de alta disponibilidad para System Center Configuration Manager).  

## <a name="operating-system-deployment"></a>Implementación de sistema operativo  

### <a name="windows-10-servicing"></a>Servicio de actualización de Windows 10  
 Se han agregado las siguientes mejoras para el mantenimiento de Windows 10 en la versión 1602 de Configuration Manager:  

-   Hay nuevas opciones de filtro disponibles para planes de mantenimiento que le permiten filtrar por **idioma**, **carácter obligatorio** y **título**. Solo se agregarán a la implementación asociada las actualizaciones que cumplan con los criterios especificados.  

-   Cuando se selecciona la clasificación **Actualizar** para la sincronización de las actualizaciones de software, se muestra un cuadro de diálogo de advertencia para informarle de que la [revisión 3095113](https://support.microsoft.com/kb/3095113) de WSUS 4.0 es necesaria para sincronizar correctamente las actualizaciones de software y para que el mantenimiento de Windows 10 se realice correctamente. Desde el cuadro de diálogo, puede ir al artículo de Knowledge Base correspondiente.  

-   Ahora las actualizaciones de Windows 10 disponibles solo se muestran en el nodo **Mantenimiento de Windows 10** \ **Todas las actualizaciones de Windows 10** de la consola de Configuration Manager. Estas actualizaciones ya no se mostrarán en el nodo **Actualizaciones de Software** \ **Todas las actualizaciones de software** de la consola.  

-   Un plan de mantenimiento se considera una implementación de alto riesgo, y la ventana **Seleccionar recopilación** muestra solo las recopilaciones personalizadas que cumplen con la configuración de comprobación de implementación que está configurada en las propiedades del sitio. Para obtener más información, consulte [Settings to manage high-risk deployments for System Center Configuration Manager](../../../protect/understand/settings-to-manage-high-risk-deployments.md) (Configuración para administrar implementaciones de alto riesgo para System Center Configuration Manager).  

-   Se mostrará a los usuarios finales que inicien un paquete de actualización de Windows 10 un cuadro de diálogo para notificarles que van a actualizar su sistema operativo.  

## <a name="application-management"></a>Administración de aplicaciones  

### <a name="ios-app-configuration-policies"></a>Directivas de configuración de aplicaciones de iOS  
 Use las directivas de configuración de aplicaciones de Configuration Manager para proporcionar la configuración que puede ser necesaria cuando el usuario ejecuta una aplicación de iOS. Por ejemplo, una aplicación puede requerir al usuario que especifique un número de puerto personalizado, idioma, seguridad o configuración de marca, como un logotipo de empresa.   
Si el usuario ha introducido esta configuración incorrectamente, puede aumentar la carga del servicio de asistencia técnica y ralentizar la adopción de nuevas aplicaciones.  

 Las directivas de configuración de aplicaciones pueden ayudarle a eliminar estos problemas al permitirle implementar esta configuración para los usuarios en una directiva antes de ejecutar la aplicación. A continuación, la configuración se proporciona de forma automática y el usuario tiene que realizar ninguna acción.  

 Para obtener más información, consulte [Configure iOS apps with app configuration policies in System Center Configuration Manager](../../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md) (Configurar aplicaciones de iOS con directivas de configuración de aplicaciones en System Center Configuration Manager).  

### <a name="manage-volume-purchased-ios-apps"></a>Manage volume-purchased iOS apps  
 Configuration Manager puede ayudarle a implementar y administrar aplicaciones que ha adquirido por volumen desde el Programa de Compras por Volumen (PCV) de Apple importando la información de licencia desde App Store y supervisando la cantidad de licencias que se han utilizado.  

 Para obtener más información, consulte [Administración de aplicaciones iOS adquiridas por volumen con System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).  

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
 Se agregaron nuevas opciones para el elemento de configuración de **Windows 8.1 y Windows 10** que le ayudarán a ejecutar los dispositivos que ejecutan Windows 10 Team, como un dispositivo con Surface Hub.  

 Para obtener más información, consulte [How to create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client](../../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md) (Creación de elementos de configuración para dispositivos de Windows 8.1 y Windows 10 administrados sin el cliente de System Center Configuration Manager).  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Configuración de pantalla completa para dispositivos Android Samsung KNOX Standard  
 El modo de quiosco permite bloquear un dispositivo para permitir que solo funcionen determinadas características. Por ejemplo, puede permitir que un dispositivo ejecute solo una aplicación administrada que especifique, o puede deshabilitar los botones de volumen de un dispositivo. Esta configuración podría utilizarse para un modelo de demostración de un dispositivo o para un dispositivo que está dedicado a realizar solo una función, como un dispositivo de punto de venta. En Configuration Manager, ahora puede especificar la configuración de pantalla completa para dispositivos Samsung KNOX Standard.  

 Para obtener más información, consulte [Crear elementos de configuración para dispositivos Android y Samsung KNOX Standard administrados sin el cliente de System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).  

## <a name="conditional-access"></a>Acceso condicional  

### <a name="conditional-access-for-pcs-managed-by-system-center-configuration-manager"></a>Acceso condicional para equipos administrados por System Center Configuration Manager  
 Antes de esta versión, para configurar el acceso condicional para un equipo, dicho equipo debía estar inscrito en Intune o unido a dominio. A partir de la actualización 1602, se admite el acceso condicional para equipos administrados por System Center Configuration Manager. Para los equipos administrados por System Center Configuration Manager, puede restringir el acceso a Exchange Online y SharePoint Online a los dispositivos que cumplan con las directivas que se configuren.  

 Para obtener más información, consulte [Manage access to O365 services for PCs managed by System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md) (Administración del acceso a servicios de O365 para equipos administrados por System Center Configuration Manager).  

### <a name="restricting-access-based-on-device-health-attestation-status"></a>Restricción del acceso según el estado de la atestación de estado del dispositivo  
 Ahora puede restringir el acceso a los servicios de correo electrónico y 0365 según el estado de los dispositivos notificado por el servicio de atestación de estado. Además, los dispositivos administrados por Intune se incluyen en los informes de estado de dispositivos.  

 Se ha agregado una nueva regla de cumplimiento a la consola de Configuration Manager que permite especificar si debe permitir o bloquear el acceso de los dispositivos en función de su estado de mantenimiento.   Para obtener más información sobre el servicio de atestación de estado y cómo se notifica el estado de los dispositivos en Intune, consulte [Health attestation for System Center Configuration Manager](../../../core/servers/manage/health-attestation.md) (Atestación de estado para System Center Configuration Manager).  

### <a name="new-compliance-policy-rules"></a>Nuevas reglas de directivas de cumplimiento  
 Se agregaron nuevas reglas de directivas de cumplimiento, como actualizaciones automáticas y una contraseña para desbloquear dispositivos, para admitir mejores requisitos de seguridad.  


 Para obtener más información, consulte [Device compliance policies in System Center Configuration Manager](../../../protect/deploy-use/device-compliance-policies.md) (Directivas de cumplimiento de dispositivos en System Center Configuration Manager).  

### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Comprobación de que los dispositivos inscritos y conformes siempre tengan acceso a Exchange local.  
 **Sustitución de la regla predeterminada: permitir siempre que los dispositivos inscritos y compatibles tengan acceso a Exchange local:** si se selecciona esta opción, los dispositivos inscritos en Intune y que cumplen con las directivas establecidas pueden tener acceso a Exchange local. Esta regla invalida la Regla predeterminada, lo que significa que aunque configure dicha regla y la establezca en Cuarentena o Bloquear el acceso, aquellos dispositivos inscritos y que cumplen con las directivas seguirán teniendo acceso a Exchange local. Use esta opción cuando quiera que los dispositivos inscritos y conformes a las directivas siempre tengan acceso a correo electrónico a través de Exchange local.  

 Esta regla está disponible en la **página General** del **Asistente de configuración de directivas de acceso condicional** para Exchange local.  

 Para obtener un tutorial detallado, consulte [Manage email access in System Center Configuration Manager](../../../protect/deploy-use/manage-email-access.md) (Administración del acceso a correo electrónico en System Center Configuration Manager).  

## <a name="client-management"></a>Administración de cliente  

### <a name="client-online-status"></a>Estado de conexión de clientes  
 Hay un nuevo estado disponible para los clientes para supervisar si un equipo está conectado o no. Un equipo se considera en línea si está conectado a su punto de administración asignado. Para indicar que el equipo está en línea, el cliente envía mensajes similares a ping al punto de administración. Si el punto de administración no recibe un mensaje después de 5 minutos, el cliente se considera sin conexión.  

 Para obtener más información, consulte [How to monitor clients in System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md) (Supervisión de clientes en System Center Configuration Manager).  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Actualizar la directiva de usuario y máquina desde el Centro de software  
 Se ha agregado una nueva opción, **Directiva de sincronización**, a la página **Opciones** > **Mantenimiento del equipo** del Centro de software que hace que el equipo actualice su directiva de usuario y máquina de Configuration Manager.  

### <a name="software-center-branding-changes"></a>Personalización del Centro de software  
 Puede cambiar el color, el nombre de la organización y el icono que aparece en el Centro de software. Esta configuración se aplicará según las reglas siguientes:  

1.  Si no está instalado el rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones, el Centro de software mostrará el nombre de organización especificado en el cliente **Agente de equipo** que establece el **Nombre de organización mostrado en el Centro de software**.  

2.  Si está instalado el rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones, el Centro de software mostrará el nombre de la organización y el color especificados en las propiedades del rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones.  

3.  Si una suscripción de Microsoft Intune está configurada y conectada al entorno de Configuration Manager, el Centro de software mostrará el nombre de la organización, el color y el logotipo de la empresa especificados en las propiedades de la suscripción de Intune.  

### <a name="health-attestation"></a>Atestación de estado  
 Los administradores pueden ver el estado de la atestación de estado de los dispositivos de Windows 10 en la consola de Configuration Manager.  Esta funcionalidad está disponible para Configuration Manager y Configuration Manager con Microsoft Intune. La atestación de estado del dispositivo permite al administrador garantizar que los equipos cliente tienen habilitadas las siguientes configuraciones BIOS, TPM y de software de arranque de confianza:  

-   Antimalware de inicio temprano  

-   BitLocker  

-   Arranque seguro  

-   Integridad de código  

Para obtener más información, consulte [Health attestation for System Center Configuration Manager](../../../core/servers/manage/health-attestation.md) (Atestación de estado para System Center Configuration Manager).  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Mejoras en la configuración antimalware de Endpoint Protection  
 1602 agrega las nuevas opciones de configuración siguientes a la directiva antimalware de Endpoint Protection para Windows Defender:  

-   Protección en tiempo real: bloquear aplicaciones potencialmente no deseadas en la descarga y antes de la instalación  

-   Configuración de exploración: examinar unidades de red asignadas al ejecutar un examen completo  

-   Configuración de envío automático de archivo de ejemplo:  

     El motor de antimalware puede solicitar ejemplos de archivo que se enviarán a Microsoft para un análisis más profundo. De forma predeterminada, siempre se le preguntará antes de enviar dichos ejemplos. Los administradores pueden administrar ahora las siguientes opciones para configurar este comportamiento:  

    -   Avanzado: habilitar el envío automático de archivos de ejemplo para ayudar a Microsoft a averiguar si ciertos elementos encontrados son malintencionados  

    -   Avanzado: permitir a los usuarios modificar la configuración de envío automático de archivos de ejemplo  

    Además, la configuración **Excluir archivos y carpetas** existente en la sección "Configuración de exclusión" de la directiva antimalware de Endpoint Protection se ha mejorado para permitir exclusiones del dispositivo.  

Para obtener más información, consulte [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-antimalware-policies.md) (Creación e implementación de directivas antimalware para Endpoint Protection en System Center Configuration Manager).  

## <a name="mobile-device-management"></a>Administración de dispositivos móviles  

### <a name="ios-activation-lock"></a>Bloqueo de activación de iOS  
 Configuration Manager puede ayudarle a administrar el bloqueo de activación de iOS, una característica de la aplicación Buscar mi iPhone disponible en iOS 7.1 y en dispositivos más modernos. El bloqueo de activación se habilita automáticamente cuando se usa la aplicación Buscar mi iPhone en un dispositivo. Tras su activación, se debe escribir el identificador y la contraseña de Apple del usuario para poder:  

-   Desactivar Buscar mi iPhone  

-   Borrar el dispositivo  

-   Reactivar el dispositivo  

Configuration Manager puede solicitar el estado de bloqueo de activación de los dispositivos supervisados y no supervisados que ejecutan iOS 7.1 y versiones posteriores. Para los dispositivos supervisados, Configuration Manager puede recuperar el código de omisión de bloqueo de activación y emitirlo directamente al dispositivo.  

 Para obtener más información, consulte [Help protect iOS devices with Activation Lock bypass in System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock) (Ayudar a proteger dispositivos iOS con omisión del bloqueo de activación en System Center Configuration Manager).  

### <a name="monitor-terms-and-conditions-deployments"></a>Supervisión de las implementaciones de términos y condiciones  
 Puede supervisar las implementaciones de términos y condiciones en la consola de Configuration Manager.  

 Seleccione la implementación de términos y condiciones en la lista de implementaciones. El área de resumen muestra las estadísticas siguientes:  

-   **Conforme** : los usuarios han aceptado la versión más reciente de los términos y condiciones  

-   **Error**  

-   **No conforme** : los usuarios han aceptado una versión de los términos y condiciones, pero no la más reciente  

-   **Desconocido** : los usuarios no han aceptado nunca los términos y condiciones, incluidos aquellos sin un dispositivo inscrito  



<!--HONumber=Dec16_HO3-->


