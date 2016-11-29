---
title: Technical Preview para System Center Configuration Manager
description: "Obtenga información sobre la versión Technical Preview que le permite probar nuevas funcionalidades y capacidades de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 39a9cde3bd955c84f301d25258b413fecaa4393b
ms.openlocfilehash: 2aa78c20c919d04401f663063860df06c5262048


---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Technical Preview)*

**Le damos la bienvenida a System Center Configuration Manager Technical Preview**. Este tema proporciona detalles acerca de la versión preliminar en evolución que presenta nuevas funcionalidades y capacidades en las que estamos trabajando. Con cada nueva versión preliminar técnica se presentan nuevas características que no se han incluido aún en la rama actual de System Center Configuration Manager cuando se pone a disposición la versión preliminar técnica. Estas características podrían incluirse finalmente en una actualización de la versión actual de la rama, pero antes de finalizarlas y agregarlas, queremos que tenga la oportunidad de probarlas y enviarnos sus comentarios.  

 Puesto que esta es una versión preliminar técnica, los detalles y las funcionalidades están sujetos a cambios.  

 Este tema contiene información que afecta a todas las versiones de Technical Preview y enumera todas las nuevas capacidades (o características), junto con la versión de Technical Preview en la que la capacidad aparece por primera vez, como versión 1512 para diciembre de 2015. Los detalles de estas capacidades se proporcionan en otros temas dedicados a cada versión preliminar.  

 Para obtener más información sobre las novedades en la rama actual de Configuration Manager, consulte [Novedades de System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="a-namebkmkreqsa-requirements-and-limitations-for-the-technical-preview"></a><a name="bkmk_reqs"></a> Requisitos y limitaciones de Technical Preview  

> [!IMPORTANT]  
>  La versión Technical Preview solo tiene licencia para su uso en un entorno de laboratorio.  Es posible que Microsoft no proporcione servicios de soporte técnico y que algunas características no estén disponibles en el software de versión preliminar. Además, es posible que el software de versión preliminar tenga unos estándares de seguridad, privacidad, accesibilidad, disponibilidad y confiabilidad reducidos o diferentes a los del software proporcionado comercialmente.  

 Para la mayoría de requisitos previos del producto, use la información que aparece en [Configuraciones admitidas para System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). Las excepciones siguientes se aplican a las versiones Technical Preview:  

-   Todas las instalaciones permanecen activas durante 90 días y luego cambian a inactivas.  

-   El único idioma admitido es el inglés.  

-   Solo se admite un sitio primario independiente. No se admiten sitios de administración central, varios sitios primarios ni sitios secundarios.  

-   Solo se admiten las siguientes versiones de SQL Server:  

    -   SQL Server 2012 con la actualización acumulativa 2 o posterior  

    -   SQL Server 2014  

-   El sitio admite hasta 10 clientes, que deben ejecutar una de las siguientes opciones:  

    -   Windows 7  

    -   Windows 8  

    -   Windows 8.1  

    -   Windows 10  

-   Solo se admiten los siguientes indicadores de instalación (conmutadores):  

    -   **/silent**  

    -   **/testdbupgrade**  

-   Cuando proceda, se incluyen limitaciones o requisitos adicionales con los detalles de cada versión específica de Technical Preview  

-   No se admite la migración a esta versión preliminar o desde ella.  

-   No se admite la actualización a esta versión preliminar.  

-   No se admite la actualización a una versión de producción (rama actual) desde esta versión preliminar. En cambio, cuando haya actualizaciones disponibles para una versión preliminar, puede buscarlas e instalarlas desde el nodo **Actualizaciones y mantenimiento** de la consola de Configuration Manager. Para ver un vídeo del proceso de actualización en la consola, consulte [Installing ConfigMgr Update Package (Instalación de paquetes de actualización de Configuration Manager)](https://www.youtube.com/embed/KBd_EGFbUT8) en youtube.com.  

##  <a name="a-namebkmkinstalla-install-and-update-the-technical-preview"></a><a name="bkmk_install"></a> Instalar y actualizar la versión Technical Preview  
 System Center Configuration Manager Technical Preview es diferente de la versión actual de System Center Configuration Manager.  

 Para usar la versión preliminar técnica, primero debe instalar una **versión de línea base** de la compilación de dicha versión. Después de instalar una versión de línea base, podrá usar las **actualizaciones en consola** para que la instalación cuente con la versión preliminar más reciente.     Normalmente, las nuevas versiones de Technical Preview están disponibles cada mes.  

> [!TIP]  
>  Cuando se instala una actualización de versión preliminar técnica, la instalación de versión preliminar se actualiza a la nueva versión preliminar técnica.    Una instalación de versión preliminar técnica nunca dispone de una opción para actualizar a una instalación de rama actual ni recibir actualizaciones de la versión de rama actual.  

 **Versiones activas de línea base de Technical Preview:**  
 Puede instalar una versión de línea base hasta 1 año después de su lanzamiento.

-   **Technical Preview 1610**: la versión Configuration Manager Technical Preview 1610 está disponible como actualización en consola para Configuration Manager Technical Preview y como nueva versión de linea base que está disponible en el sitio web [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

-   **Technical Preview 1603** como parte de **System Center Technical Preview 5**: la versión Configuration Manager Technical Preview 1603 está disponible como actualización en consola para Configuration Manager Technical Preview y como nueva versión de linea base incluida con System Center Technical Preview 5.    La versión incluida con System Center Technical Preview 5 es la única que puede utilizarse para una instalación de línea base.  

     Acerca de la versión de línea base de [Configuration Manager Technical Preview de System Center Technical Preview 5](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview):  

    -   La consola de Configuration Manager y el programa de instalación enumeran la versión como System Center Configuration Manager Technical Preview 1603.  

    -   Esta versión de línea base funciona igual que Configuration Manager Technical Preview 1603, incluida la compatibilidad con las actualizaciones en consola.  


##  <a name="a-namebkmktpfeedbacka-providing-feedback"></a><a name="BKMK_TPFeedback"></a> Proporcionar comentarios  
 Deseamos recibir sus comentarios sobre nuestras versiones Technical Preview. Para enviar comentarios sobre las funcionalidades de cada versión preliminar, siga el vínculo a nuestro formulario de comentarios en la página del [programa de comentarios de Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) en el sitio de Microsoft Connect.  

 También puede hablarnos de cualquier característica nueva que le gustaría ver. Para enviar nuevas ideas y votar sobre las ideas enviadas por otros usuarios, [visite nuestra página de voz del usuario](http://configurationmanager.uservoice.com).  

##  <a name="a-namebdmktpknownissuesa-general-changes-introduced-in-technical-previews"></a><a name="bdmk_tpknownissues"></a> Cambios generales introducidos en Technical Preview  

-   **Technical Preview 1603:**  

    -   A partir de Technical Preview 1603, tiene la posibilidad de configurar las implementaciones de actualizaciones de software para que los clientes ejecuten un examen de cumplimiento de las actualizaciones de software inmediatamente después de que un cliente instale las actualizaciones de software y reinicie. Esto permite al cliente comprobar las actualizaciones de software adicionales que entran en vigor después de que el cliente reinicie e instalarlas (para cumplir así los requisitos) durante la misma ventana de mantenimiento.  

         Para configurar esta opción en una implementación, en la página **Experiencia del usuario** del Asistente para implementar actualizaciones de software, seleccione la opción **Si alguna actualización de esta implementación requiere un reinicio del sistema, ejecute el ciclo de evaluación de implementación de actualizaciones tras el reinicio**.  

    -   A partir de Technical Preview 1603, el comportamiento de la variable de secuencia de tareas SMSTSRebootDelay ha cambiado. La variable SMSTSRebootDelay especifica el número de segundos que se debe esperar antes de reiniciar el equipo. Si esta variable no está establecida en 0, el administrador de la secuencia de tareas mostrará un cuadro de diálogo de notificación antes del reinicio.  
        El valor que configure para esta variable se conservará hasta que se configure uno nuevo. El período de demora de los posteriores reinicios del equipo tendrán el mismo valor. En la versión 1602 y anteriores de Configuration Manager, la variable se restablece al valor predeterminado (30 segundos) cuando el equipo se reinicia.   Para más información, vea [Task sequence built-in variables in System Center Configuration Manager](../../osd/understand/task-sequence-built-in-variables.md).

-   **Technical Preview 1602:** a partir de la versión Technical Preview 1602, puede actualizar in situ el sistema operativo de un servidor de sistema de sitio que ejecute de Windows Server 2008 R2 a Windows Server 2012 R2.  Si usa los procedimientos de actualización de Windows Server 2012 R2, no es necesario ejecutar una restauración del servidor de sitio de Configuration Manager después de la actualización.  Para conocer los procedimientos de actualización, consulte [Opciones de actualización para Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx).  

    > [!WARNING]  
    >  Antes de actualizar a Windows Server 2012 R2, **debe desinstalar WSUS 3.2** del servidor.  
    >   
    >  Para obtener más información acerca de este paso crítico, consulte la sección Funcionalidad nueva y modificada en [Introducción a Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) en la documentación de Windows Server.  

-   **Technical Preview 1601:** de forma predeterminada, el punto de conexión de servicio se establece en el modo en línea cuando se instala y no se admite el cambio al modo sin conexión.  





##  <a name="a-namebkmktpcapsa-capabilities-delivered-in-technical-previews"></a><a name="bkmk_tpCaps"></a> Funcionalidades ofrecidas en Technical Preview  
 A continuación se enumeran las capacidades que ofrece cada versión preliminar técnica de Configuration Manager.  Las capacidades que están disponibles a partir de una versión preliminar técnica siguen estando disponibles en versiones posteriores. De igual forma, las capacidades que se han agregado a System Center Configuration Manager Release (rama actual) siguen estando disponibles en las versiones preliminares técnicas posteriores.  Haga clic en el contenido de cada versión preliminar para aprender más acerca de una capacidad específica.  

 |Capacidad|Versión de Technical Preview|Versión de rama actual|  
 |----------------|---------------------|--------------------|
 |Filtrar por tamaño del contenido en las reglas de implementación automática|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|![Sin agregar](media/Red_X.gif)|
 |Funcionalidad mejorada para los cuadros de diálogo de software obligatorios|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|![Sin agregar](media/Red_X.gif)|
 |Rechazar solicitudes de aplicación aprobadas previamente|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|![Sin agregar](media/Red_X.gif)|
 |Excluir a clientes de la actualización automática|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|![Sin agregar](media/Red_X.gif)|
 |Mejoras de Endpoint Protection|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|![Sin agregar](media/Red_X.gif)|
 |Mayor número de dispositivos inscritos|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#increased-number-of-enrolled-devices)|![Sin agregar](media/Red_X.gif)|
 |Opciones adicionales del DEP de Apple|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|![Sin agregar](media/Red_X.gif)|
 |Mejoras en la integración de la Tienda Windows para empresas con Configuration Manager|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|![Sin agregar](media/Red_X.gif)|
 |Nueva configuración de cumplimiento para elementos de configuración|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|![Sin agregar](media/Red_X.gif)|
 |Integración con Upgrade Analytics|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|![Sin agregar](media/Red_X.gif)|
 |Tipos de conexión nativos para perfiles híbridos de VPN de Windows 10|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Sin agregar](media/Red_X.gif)|
 |Mejoras en los grupos de límites|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|![Sin agregar](media/Red_X.gif)|
 |Panel de administración del cliente de Office 365|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|![Sin agregar](media/Red_X.gif)|
 |Implementar aplicaciones de Office 365 en clientes|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#ceploy-office-365-apps-to-clients)|![Sin agregar](media/Red_X.gif)|
 |Mejoras en la conversión de BIOS a UEFI|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-bios-to-uefi-conversion)|![Sin agregar](media/Red_X.gif)|
 |Gráficos de cumplimiento de Intune|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|![Sin agregar](media/Red_X.gif)|
 |Mejoras en el paso Preparar cliente de Configuration Manager para la captura de la secuencia de tareas|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|![Sin agregar](media/Red_X.gif)|
 |Mejoras en el Centro de software|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|![Sin agregar](media/Red_X.gif)|
 |Mejoras en Asset Intelligence|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![Sin agregar](media/Red_X.gif)|
 |Traducción de teclado de control remoto|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![Sin agregar](media/Red_X.gif)|
 |Mejoras en la directiva de actualización de la edición de Windows 10|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|![Sin agregar](media/Red_X.gif)|
 |Cuadros de diálogo personalizables de personalización de marca del Centro de software|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-denter-dialogs)|![Sin agregar](media/Red_X.gif)|  
 |Varios puntos de administración de dispositivos para la administración local de dispositivos móviles|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Versión 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Clasificar automáticamente dispositivos en recopilaciones|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Versión 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Período de gracia de cumplimiento para implementaciones de actualizaciones de software y aplicaciones requeridas|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|![Sin agregar](media/Red_X.gif)|
 |Uso de Configuration Manager como un instalador administrado con protección de dispositivos|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![Sin agregar](media/Red_X.gif)|
 |Servicio de proxy en la nube|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | ![Sin agregar](media/Red_X.gif)|  
 |Administrar al agente cliente de Office 365 en Configuration Manager|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Versión 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |La variable de secuencia de tareas OSDPreserveDriveLetter ha dejado de usarse|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Versión 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Cambios en el nodo de actualizaciones y mantenimiento|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Versión 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |VPN por aplicación para dispositivos Windows 10|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Versión 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Mejoras en la secuencia de tareas Instalar actualizaciones de software|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Versión 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Mejoras en el paso Preparar cliente de Configuration Manager para la captura de la secuencia de tareas |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|![Sin agregar](media/Red_X.gif) |
 |Período de gracia para las implementaciones de aplicaciones necesarias |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|![Sin agregar](media/Red_X.gif)|  
 |Nueva experiencia para acciones del dispositivo remoto |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[Versión 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Tienda Windows para aplicaciones empresariales |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[Versión 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Mejoras generales para aplicaciones adquiridas por volumen|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[Versión 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Protección de datos empresariales (EDP)|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[Versión 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Los usuarios finales pueden instalar aplicaciones desde el Portal de empresa |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|![Sin agregar](media/Red_X.gif)|  
 |Nuevas pestañas para actualizaciones y sistemas operativos en el Centro de software|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[Versión 1606 ](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Dar servicio a un grupo de servidores |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[Versión 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Compatibilidad con el servicio Protección contra amenazas avanzada de Windows Defender |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[Versión 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |Nuevas opciones de reinicio para los clientes de Windows 10 después de la instalación de la actualización del software|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[Versión 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |Atestación de estado del dispositivo local |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[Versión 1606](/sccm/core/servers/manage/health-attestation)|  
 |Declarar previamente dispositivos corporativos con número de serie IMEI o iOS|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[Versión 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  
 |Administración de aplicaciones adquiridas por volumen de la Tienda Windows para empresas| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[Versión 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Mejoras en la administración de Microsoft Passport for Work|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[Versión 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Opción de cambio a un nuevo punto de actualización de software para clientes|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[Versión 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |Configuración de cliente para administrar la Configuración de caché de cliente y la Caché del mismo nivel de clientes |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|[Versión 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)|  
 |Compatibilidad con Passport for Work como KSP |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Versión 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |Atestación de estado del dispositivo local|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Versión 1606](/sccm/core/servers/manage/health-attestation)|  
 |Configuración de SmartLock para dispositivos Android|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Versión 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |Mejoras en el Centro de software|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Versión 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Mejoras en el control remoto|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Versión 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Personalización del tamaño de bloque de TFTP de RamDisk y el tamaño de la ventana de puntos de distribución habilitados con PXE|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Versión 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Mejoras en la administración de dispositivos móviles|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_MDM)|[Versión 1602](/sccm/mdm/deploy-use/manage-ios-activation-lock) |  
 |Mejoras en el Centro de software en la versión 1602|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_SC1601)| [Versión 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#client-management)|  
 |Mejoras en mantenimiento de Windows 10|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_Win10Servicing)|[Versión 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#operating-system-deployment) |  
 |Mejoras en la integración con Microsoft Intune|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_hybrid1)|[Versión 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#conditional-access)|  
 |Estado de conexión de clientes|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_clientStatus)|[Versión 1602](/sccm/core/clients/manage/monitor-clients)|
 |Mejoras en la administración de aplicaciones|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_appmgmt1601)|[Versión 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#application-management)|  
 |Mejoras en la configuración de cumplimiento|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_compliance1601)|[Versión 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#compliance-settings)|  
 |Atestación de estado del dispositivo|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_devicehealth)|[Versión 1602](/sccm/core/servers/manage/health-attestation)|
 |Supervisión en la consola para los términos y condiciones|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_viewterms)|[Versión 1602](/sccm/mdm/deploy-use/terms-and-conditions)|  
 |Mejoras para la configuración de directivas de Endpoint Protection|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_EPpolicy)|[Versión 1602](/sccm/protect/deploy-use/endpoint-antimalware-policies)|  
 |Integración con Windows Update for Business en Windows 10|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_WUfB)|[Versión 1602](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|  
 |Administración de la actualización de cliente de Office 365 ProPlus a través de System Center Configuration Manager|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_Office365ProPlus)|[Versión 1602](/sccm/sum/deploy-use/manage-office-365-proplus-updates)|  
 |Compatibilidad con SQL Server AlwaysOn para bases de datos de alta disponibilidad|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_AlwasyOn)|[Versión 1602](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)|  
 |Servicio de un clúster de servidores|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_ClusterServerUpdates)|[Versión 1606](/sccm/sum/deploy-use/service-a-server-group)|  
## <a name="see-also"></a>Véase también  
[Novedades de System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introducción a System Center Configuration Manager](../../core/understand/introduction.md)



<!--HONumber=Nov16_HO1-->


