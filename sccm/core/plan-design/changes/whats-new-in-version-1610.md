---
title: "Novedades de la versión 1610 | Microsoft Docs"
description: "Conozca en detalle los cambios y las nuevas funciones introducidas en la versión 1610 de System Center Configuration Manager."
ms.custom: na
ms.date: 
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
caps.latest.revision: 40
author: Brenduns
ms.author: brenduns
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: 828e2ac9a3f9bcea1571d24145a1021fdf1091f3
ms.openlocfilehash: 5121073a335f6722ea1e6cf7669edbf13ba3f9db

---
# <a name="what39s-new-in-version-1610-of-system-center-configuration-manager"></a>Novedades de la versión 1610 de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La actualización 1610 para la Rama actual de System Center Configuration Manager es una actualización disponible como actualización en consola para sitios instalados previamente que ejecutan la versión 1511, 1602 o 1606.


> [!TIP]  
> Para instalar un sitio nuevo, debe usar una versión de línea base de Configuration Manager.  
>  Más información acerca de:    
>  -   [Instalación de nuevos sitios](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [Instalación de actualizaciones en los sitios](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [Versiones de línea de base y versiones de actualización](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

En las secciones siguientes se proporcionan detalles sobre los cambios y las nuevas funciones introducidas en la versión 1610 de Configuration Manager.  


## <a name="in-console-monitoring-of-update-installation-status"></a>Supervisión en la consola del estado de la instalación de actualización  
A partir de la versión 1610, cuando instale un paquete de actualizaciones y supervise la instalación en la consola, hay una fase nueva: **Postinstalación**. En esta fase se incluye el estado de las tareas como el reinicio de los servicios clave y la inicialización de la supervisión de replicación. (Esta fase no está disponible en la consola hasta que el sitio se actualice a la versión 1610). Para obtener más información sobre el estado de la instalación de actualización, consulte [Install in-console updates (Instalación de actualizaciones en la consola)](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).


## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir a clientes de la actualización automática
Puede excluir clientes de Windows de la actualización con las versiones nuevas del software cliente. Para hacer esto, incluya los equipos cliente en una colección que sea específica para excluirse de la actualización. El cliente de la colección excluida ignora las solicitudes para actualizar el software cliente.  Para obtener más información, consulte [Exclude Windows clients from upgrades (Excluir clientes Windows de las actualizaciones)](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Mejoras en los grupos de límites
La versión 1610 presenta cambios importantes en los grupos de límites y en su funcionamiento con los puntos de distribución. Estos cambios pueden simplificar el diseño de la infraestructura de contenido al proporcionarle más control sobre cómo y cuándo usan la reserva los clientes para buscar puntos de distribución adicionales como ubicaciones de origen de contenido. Esto incluye tanto puntos de distribución locales como basados en la nube.
Estas mejoras reemplazan conceptos y comportamientos con los que puede que esté familiarizado (como la configuración de puntos de distribución como rápidos o lentos) por un nuevo modelo que debería ser más fácil de configurar y mantener. Estos cambios también constituyen la base para futuros cambios que mejorarán otros roles de sistema de sitio que asocia a los grupos de límites.

Cuando actualiza a la versión 1610, la actualización convierte las configuraciones de los grupos de límites actuales para ajustarse al nuevo modelo, de modo que estos cambios no afecten a las configuraciones de distribución de contenido existentes.

Para obtener más información, consulte [Boundary groups (Grupos de límites)](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-groups).


## <a name="peer-cache-for-content-distribution-to-clients"></a>Almacenamiento en caché del mismo nivel para la distribución de contenido en los clientes
A partir de la versión 1610, el **almacenamiento en caché del mismo nivel** de cliente le ayuda a administrar la implementación de contenido en los clientes en ubicaciones remotas. Caché del mismo nivel es una solución integrada de Configuration Manager para que los clientes compartan contenido con otros clientes directamente desde su caché local.

Después de implementar la configuración de cliente que habilita el almacenamiento en caché del mismo nivel en una colección, los miembros de esa colección pueden actuar como origen de contenido del mismo nivel para otros clientes en el mismo grupo de límites.

También puede usar el nuevo panel **Orígenes de datos de cliente** para entender el uso de los orígenes de contenido del almacenamiento en caché del mismo nivel en su entorno.

> [!TIP]  
> Con la versión 1610, el panel de orígenes de datos de cliente y la caché del mismo nivel son funciones de la versión preliminar. Para habilitarlos, vea [Uso de características de la versión preliminar a partir de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

Para obtener más información, consulte [Peer Cache for Configuration Manager clients (Almacenamiento en caché del mismo nivel para clientes de Configuration Manager)](/sccm/core/plan-design/hierarchy/client-peer-cache) y [Client Data Sources dashboard (Panel de orígenes de datos de cliente)](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrar varios puntos de distribución compartidos al mismo tiempo
Ahora puede usar la opción **Reasignar punto de distribución** para que Configuration Manager procese en paralelo la reasignación de un máximo de 50 puntos de distribución compartidos al mismo tiempo. Antes de esta versión, los puntos de distribución reasignados se procesaban de uno en uno. Para obtener más información, consulte [Migrate multiple shared distribution points at the same time (Migrar varios puntos de distribución compartidos al mismo tiempo)](/sccm/core/migration/planning-a-content-deployment-migration-strategy#migrate-multiple-shared-distribution-points-at-the-same-time).

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Puerta de enlace de administración en la nube para administrar los clientes basados en Internet

La puerta de enlace de administración en la nube proporciona una manera sencilla de administrar clientes de Configuration Manager en Internet. El servicio de puerta de enlace de administración en la nube, que se implementa en Microsoft Azure y exige una suscripción de Azure, se conecta a la infraestructura local de Configuration Manager con un nuevo rol denominado punto de conexión de la puerta de enlace de administración en la nube. Una vez implementado y configurado por completo, los clientes pueden comunicarse con los roles del sistema de sitio local de Configuration Manager y con los puntos de distribución basados en la nube independientemente de si están conectados en la red privada interna o en Internet. Para obtener más información y ver cómo la puerta de enlace de administración en la nube se compara con la administración de cliente basada en Internet, consulte [Manage clients on the Internet (Administrar clientes en Internet)](/sccm/core/clients/manage/manage-clients-internet).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Mejoras en la directiva de actualización de la edición de Windows 10
En esta versión se han realizado las siguientes mejoras en este tipo de directiva:

- Ahora puede usar la directiva de actualización de la edición con equipos Windows 10 que ejecuten el cliente de Configuration Manager además de con equipos Windows 10 inscritos en Microsoft Intune.
- Puede actualizar desde Windows 10 Professional a cualquiera de las plataformas del asistente compatibles con el hardware.

## <a name="manage-hardware-identifiers"></a>Administrar identificadores de hardware
Ahora puede proporcionar una lista de identificadores de hardware que Configuration Manager omitirá en el registro de clientes y el arranque PXE. Esto ayuda a resolver dos problemas comunes.

1. Muchos dispositivos nuevos, como Surface Pro 3, no incluyen un puerto Ethernet integrado. Generalmente se usa un adaptador de USB a Ethernet para establecer una conexión con cable para la implementación del sistema operativo, pero suele tratarse de adaptadores compartidos debido a su costo y su facilidad de uso general. Dado que la dirección MAC de este adaptador se usa para identificar el dispositivo, resulta problemático volver a usar el adaptador si no se realizan acciones de administrador adicionales entre cada implementación. Ahora, en la versión 1610 de rama actual de Configuration Manager, puede excluir la dirección MAC de este adaptador para que se pueda volver a usar fácilmente en este escenario.
2. A pesar de que se supone que el identificador de SMBIOS es un identificador de hardware único, algunos dispositivos de hardware especiales se crean con identificadores duplicados. Aunque esto no es tan común como el anterior escenario de adaptador de USB a Ethernet, también se puede usar la lista de identificadores de hardware para solucionar este problema.

Para obtener más información, consulte [Manage duplicate hardware identifiers (Administrar identificadores de hardware duplicados)](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Mejoras en la integración de la Tienda Windows para empresas con Configuration Manager
Cambios de esta versión:
- Anteriormente, solo se podían implementar aplicaciones gratuitas de la Tienda Windows para empresas. Configuration Manager ahora además admite la implementación de aplicaciones con licencia en línea de pago (solo para dispositivos inscritos en Intune).
- Ahora puede iniciar una sincronización inmediata entre la Tienda Windows para empresas y Configuration Manager.
- Ahora puede modificar la clave secreta de cliente que ha obtenido de Azure Active Directory.
- Puede eliminar una suscripción de la tienda

Para obtener más información, consulte [Manage apps from the Windows Store for Business with System Center Configuration Manager (Administración de aplicaciones desde la Tienda Windows para empresas con System Center Configuration Manager)](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Sincronización de directivas para dispositivos inscritos en Intune
Ahora puede solicitar una sincronización de directivas en un dispositivo inscrito con Intune desde la consola de Configuration Manager, en lugar de solicitar una sincronización desde la aplicación de portal de empresa en el propio dispositivo. La información del estado de la solicitud de sincronización está disponible como una nueva columna en las vistas del dispositivo denominada **Remote Sync State (Estado de la sincronización remota)**, así como en la sección de datos de detección del cuadro de diálogo **Propiedades** de cada dispositivo.
Para obtener más información, consulte [Remotely synchronize policy on Intune-enrolled devices from the Configuration Manager console (Sincronizar directivas en dispositivos inscritos con Intune de manera remota desde la consola de Configuration Manager)](/sccm/mdm/deploy-use/sync-intune-device).


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Usar la configuración de cumplimiento para configurar las opciones de Windows Defender
Ahora puede establecer la configuración de cliente de Windows Defender en equipos Windows 10 inscritos en Intune mediante elementos de configuración de la consola de Configuration Manager.
Para obtener más información, vea la sección **Windows Defender** de [Create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client (Creación de elementos de configuración para dispositivos de Windows 8.1 y Windows 10 administrados sin el cliente de System Center Configuration Manager)](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).



## <a name="general-improvements-to-software-center"></a>Mejoras generales en el Centro de software
- Ahora los usuarios pueden solicitar aplicaciones del Centro de software, así como del catálogo de aplicaciones.
- Mejoras para ayudar a los usuarios a comprender qué software es nuevo y relevante.

## <a name="new-columns-in-device-collection-views"></a>Columnas nuevas en las vistas de colección de dispositivos
Ahora puede mostrar columnas para **IMEI** y **Número de serie** (para dispositivos iOS) en las vistas de colección de dispositivos.
Para obtener más información, consulte [Predeclare devices with IMEI or iOS serial numbers](https://docs.microsoft.com/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id) (Declaración previa de dispositivos con IMEI o números de serie de iOS).

## <a name="customizable-branding-for-software-center-dialogs"></a>Cuadros de diálogo personalizables de personalización de marca del Centro de software
La personalización de marca del Centro de software se presentó en la versión 1602 de Configuration Manager. En la versión 1610, esa marca se ha ampliado ahora a todos los cuadros de diálogo asociados para proporcionar una experiencia más coherente a los usuarios del Centro de software.

La personalización de marca del Centro de software se aplica conforme a las siguientes reglas:

1. Si no está instalado el rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones, el Centro de software mostrará el nombre de organización especificado en el cliente **Agente de equipo** que establece el **Nombre de organización mostrado en el Centro de software**. Para obtener instrucciones, vea [Cómo establecer la configuración del cliente](../../clients/deploy/configure-client-settings.md).

2. Si está instalado el rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones, el Centro de software mostrará el nombre de la organización y el color especificados en las propiedades del rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones. Para más información, vea [Configuration options for Application Catalog website point (Opciones de configuración del punto de sitios web del catálogo de aplicaciones)](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#Application-Catalog-website-point).

3. Si una suscripción de Microsoft Intune está configurada y conectada al entorno de Configuration Manager, el Centro de software mostrará el nombre de la organización, el color y el logotipo de la empresa especificados en las propiedades de la suscripción de Intune. Para más información, vea [Configuring the Microsoft Intune subscription (Configuración de la suscripción de Microsoft Intune)](/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Período de gracia de cumplimiento para implementaciones de actualizaciones de software y aplicaciones requeridas
En algunos casos, es posible que quiera dar más tiempo a los usuarios para instalar las implementaciones de aplicaciones o las actualizaciones de software necesarias más allá de los plazos que ha establecido. Normalmente esto es necesario cuando un equipo ha estado apagado durante un largo período de tiempo y tiene que instalar muchas implementaciones de aplicaciones o actualizaciones. Por ejemplo, si un usuario final acaba de volver de vacaciones, es posible que tenga que esperar bastante mientras se instalan las implementaciones de aplicaciones vencidas. Para solucionar este problema, puede definir un período de gracia de cumplimiento mediante la implementación de la configuración de cliente de Configuration Manager en una colección.

Para configurar el período de gracia, haga lo siguiente:
1.      En la página **Agente de equipo** de la configuración de cliente, configure la nueva propiedad **Período de gracia para el cumplimiento tras la fecha límite de la implementación (horas)** con un valor entre **1** y **120** horas.
2.      En una nueva implementación de aplicación obligatoria o en las propiedades de una implementación existente, en la página **Programación**, active la casilla **Retrasar el cumplimiento de esta implementación de acuerdo con las preferencias del usuario hasta el período de gracia definido en la configuración del cliente**. Todas las implementaciones que tienen activada esta casilla y que están destinadas a dispositivos en los que también ha implementado la configuración de cliente usarán el período de gracia de cumplimiento.

Si configura un período de gracia de cumplimiento y activa la casilla de verificación, una vez que se llegue a la fecha límite de instalación de la aplicación, esta se instalará en la primera ventana que no sea de empresa configurada por el usuario hasta ese período de gracia. No obstante, el usuario puede abrir el Centro de software e instalar la aplicación en cualquier momento que quiera. Una vez que expira el período de gracia, el cumplimiento vuelve al comportamiento normal para implementaciones vencidas. Se han agregado opciones similares al asistente para la implementación de actualizaciones de software, al asistente para reglas de implementación automática y a las páginas de propiedades.



## <a name="improved-functionality-for-required-software-dialogs"></a>Funcionalidad mejorada para los cuadros de diálogo de software obligatorios
Cuando un usuario recibe software obligatorio, desde el valor **Posponer y volver a recordármelo en:**, puede seleccionar las siguientes opciones en la lista desplegable:
- Más adelante: especifica que las notificaciones se programan según la configuración de notificación establecida en Configuración de agente de cliente.
- Hora fija: especifica que la notificación se programará para mostrarse de nuevo después de la hora seleccionada. Por ejemplo, si un usuario selecciona 30 minutos, la notificación se mostrará de nuevo en 30 minutos.

![Página Agente de equipo de Configuración de agente de cliente](media/client-notification-settings.png)

El tiempo máximo que se puede posponer siempre se basa en los valores de notificación configurados en Configuración de agente de cliente en cada momento a lo largo de la escala de tiempo de implementación. Por ejemplo, si la opción **La fecha límite de la implementación es de más de 24 horas. Recordar al usuario cada (horas)** de la página Agente de equipo se configura para 10 horas y pasan más de 24 horas antes de la fecha límite cuando se inicia el cuadro de diálogo, el usuario vería un conjunto de opciones para posponer de hasta 10 horas, pero nunca de más de esas 10 horas. Cuando se acerca la fecha límite, el cuadro de diálogo muestra menos opciones, en consonancia con la configuración de agente de cliente correspondiente a cada componente de la escala de tiempo de implementación.

Además, en una implementación de alto riesgo, como una secuencia de tareas que implementa un sistema operativo, la experiencia de notificación del usuario final es ahora más intrusiva. En lugar de una notificación transitoria en la barra de tareas, cada vez que se notifica al usuario que se necesita mantenimiento de software crítico, aparece un cuadro de diálogo como el siguiente en el equipo del usuario:

![Cuadro de diálogo Software requerido](media/client-toast-notification.png)


Para obtener más información:
- [Settings to manage high-risk deployments (Configuración para administrar implementaciones de alto riesgo)](../../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Cómo configurar el cliente](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Panel de actualizaciones de software
Puede usar el nuevo panel de actualizaciones de software para ver el estado de cumplimiento actual de los dispositivos de la organización y analizar rápidamente los datos para ver los dispositivos que están en riesgo. Para ver el panel, vaya a **Supervisión** > **Información general** > **Seguridad** > **Software Updates Dashboard (Panel de actualizaciones de software)**.

Para obtener detalles, vea [Monitor software updates (Supervisar actualizaciones de software)](/sccm/sum/deploy-use/monitor-software-updates).


## <a name="improvements-to-the-application-request-process"></a>Mejoras en el proceso de solicitud de aplicaciones
Después de aprobar una aplicación para la instalación, puede denegar la solicitud. Para ello, haga clic en **Denegar** en la consola de Configuration Manager (antes, este botón aparecía atenuado tras la aprobación).
Esta acción no provoca que la aplicación se desinstale de ningún dispositivo. En cambio, impide que los usuarios instalen copias nuevas de la aplicación desde el Centro de software.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar por tamaño del contenido en las reglas de implementación automática
Ahora se puede filtrar por el tamaño del contenido de las actualizaciones de software en las reglas de implementación automática. Por ejemplo, puede establecer el filtro **Tamaño del contenido (KB)** en **< 2048** para descargar solo las actualizaciones de software que tengan menos de 2 MB. Con este filtro evita que las actualizaciones de software de gran tamaño se descarguen automáticamente con el fin de ofrecer un mantenimiento simplificado de nivel inferior de Windows cuando el ancho de banda de red es limitado. Para obtener más información, vea:
- [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems (Configuration Manager y mantenimiento simplificado de Windows en sistemas operativos de nivel inferior)](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).
- [Implementar actualizaciones de software automáticamente](/sccm/sum/deploy-use/automatically-deploy-software-updates)

#### <a name="to-configure-the-content-size-field"></a>Para configurar el campo Tamaño del contenido
Para configurar el campo **Tamaño del contenido (KB)**, vaya a la página **Actualizaciones de software** del Asistente para crear regla de implementación automática cuando cree una ADR o vaya a la pestaña **Actualizaciones de software** en las propiedades de una ADR existente.

## <a name="office-365-client-management-dashboard"></a>Panel de administración de clientes de Office 365
El panel de administración de clientes de Office 365 ahora está disponible en la consola de Configuration Manager. Para ver el panel, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365**.

El panel muestra gráficos para lo siguiente:

- Número de clientes de Office 365
- Versiones de cliente de Office 365
- Idiomas de cliente de Office 365
- Canales de cliente de Office 365     

Para obtener información, consulte [Manage Office 365 ProPlus updates (Administrar las actualizaciones de Office 365 ProPlus)](/sccm/sum/deploy-use/manage-office-365-proplus-updates).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Pasos de la secuencia de tareas para administrar la conversión de BIOS a UEFI
Ahora puede personalizar una secuencia de tareas de implementación de sistema operativo con una nueva variable, TSUEFIDrive, para que el paso **Reiniciar el equipo** prepare una partición FAT32 en la unidad de disco duro para la transición a UEFI. En el procedimiento siguiente se proporciona un ejemplo de cómo crear pasos de secuencia de tareas para preparar la unidad de disco duro para la conversión de BIOS en UEFI. Para obtener más información, consulte [Task sequence steps to manage BIOS to UEFI conversion (Pasos de la secuencia de tareas para administrar la conversión de BIOS a UEFI)](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion).

##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>Mejoras en el paso Preparar cliente de Configuration Manager para la captura de la secuencia de tareas  
El paso Preparar el cliente de Configuration Manager quitará por completo el cliente de Configuration Manager en lugar de quitar solo la información de clave. Cuando la secuencia de tareas implementa la imagen capturada del sistema operativo, se instala un nuevo cliente de Configuration Manager cada vez. Para obtener más información, consulte [Task sequence steps (Pasos de la secuencia de tareas)](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Gráficos de directivas cumplimiento de Intune
Ahora puede obtener una vista rápida del cumplimiento general de los dispositivos y de las principales razones del incumplimiento con los nuevos gráficos del área de trabajo **Supervisión** de la consola de Configuration Manager. Puede hacer clic en una sección del gráfico para explorar en profundidad una lista de los dispositivos de esa categoría. Para obtener más información, consulte [Monitor the compliance policy (Supervisar la directiva de cumplimiento)](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy).


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Integración de Lookout en las implementaciones híbridas para proteger los dispositivos iOS y Android
Microsoft se está integrando en la solución de protección de amenazas móviles de Lookout para proteger los dispositivos móviles iOS y Android mediante la detección de malware y aplicaciones de riesgo, entre otros, en los dispositivos. La solución de Lookout le ayuda a determinar el nivel de amenaza, que es configurable. Puede crear una regla de directivas de cumplimiento en System Center Configuration Manager para determinar el cumplimiento de dispositivo basándose en la evaluación de riesgos mediante Lookout. Con las directivas de acceso condicional, puede permitir o bloquear el acceso a los recursos empresariales basándose en el estado de cumplimiento del dispositivo. Para obtener más información sobre la integración y su funcionamiento, consulte [Manage access based on device, network, and application risk (Administrar el acceso a los recursos de la empresa según el dispositivo, la red y el riesgo de aplicación)](/sccm/protect/deploy-use/manage-access-based-on-device-network-app-risk).

A los usuarios finales de los dispositivos iOS no compatibles se les solicitará que se inscriban; necesitarán instalar la aplicación Lookout for Work en sus dispositivos, activar la aplicación y corregir las amenazas que se mencionan en la aplicación Lookout for Work para obtener acceso a los datos de la empresa. Obtenga información sobre cómo [Configure and deploy Lookout for Work apps (Configurar e implementar aplicaciones Lookout for Work)](/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps).



## <a name="new-compliance-settings-for-configuration-items"></a>Nueva configuración de cumplimiento para elementos de configuración
Se han agregado muchas opciones nuevas que se pueden usar en los elementos de configuración de varias plataformas de dispositivo. Son opciones que existían con anterioridad en Microsoft Intune en una configuración independiente y que ahora están disponibles al usar Intune con Configuration Manager.
Para obtener más información, consulte [Configuration items for devices managed without the System Center Configuration Manager client (Elementos de configuración para dispositivos administrados sin el cliente de System Center Configuration Manager)](/sccm/compliance/deploy-use/configuration-items-for-devices-managed-without-the-client).

### <a name="new-settings-for-android-devices"></a>Nuevas opciones para dispositivos Android
#### <a name="password-settings"></a>Configuración de contraseña
- **Recordar el historial de contraseñas**
- **Permitir desbloqueo mediante huellas digitales**

#### <a name="security-settings"></a>Configuración de seguridad
- **Requerir cifrado en tarjetas de almacenamiento**
- **Permitir captura de pantalla**
- **Permitir el envío de datos de diagnóstico**

#### <a name="browser-settings"></a>Configuración del explorador
- **Permitir explorador web**
- **Permitir autorrelleno**
- **Permitir bloqueador de elementos emergentes**
- **Permitir cookies**
- **Permitir Active scripting**

#### <a name="app-settings"></a>Configuración de aplicaciones
- **Permitir Google Play Store**

#### <a name="device-capability-settings"></a>Configuración de las capacidades de los dispositivos
- **Permitir almacenamiento extraíble**
- **Permitir tethering Wi-Fi**
- **Permitir geolocalización**
- **Permitir NFC**
- **Permitir Bluetooth**
- **Permitir itinerancia de voz**
- **Permitir itinerancia de datos**
- **Permitir mensajería SMS/MMS**
- **Permitir asistente de voz**
- **Permitir marcación por voz**
- **Permitir copiar y pegar**

### <a name="new-settings-for-ios-devices"></a>Nuevas opciones para dispositivos iOS
#### <a name="password-settings"></a>Configuración de contraseña
- **Número de caracteres complejos necesarios en la contraseña**
- **Permitir contraseñas sencillas**
- **Minutos de inactividad antes de que se requiera la contraseña**
- **Recordar el historial de contraseñas**

### <a name="new-settings-for-mac-os-x-devices"></a>Nuevas opciones para dispositivos Mac OS X
#### <a name="password-settings"></a>Configuración de contraseña
- **Número de caracteres complejos necesarios en la contraseña**
- **Permitir contraseñas sencillas**
- **Recordar el historial de contraseñas**
- **Minutos de inactividad antes de que se active el protector de pantalla**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Nuevas opciones para dispositivos Windows 10 Escritorio y Mobile
#### <a name="password-settings"></a>Configuración de contraseña
- **Número mínimo de conjuntos de caracteres**
- **Recordar el historial de contraseñas**
- **Requerir una contraseña cuando el dispositivo vuelva de un estado de inactividad**

#### <a name="security-settings"></a>Configuración de seguridad
- **Requerir cifrado en el dispositivo móvil**
- **Permitir cancelar suscripción manualmente**

#### <a name="device-capability-settings"></a>Configuración de las capacidades de los dispositivos
- **Permitir VPN sobre móvil**
- **Permitir itinerancia de VPN sobre móvil**
- **Permitir restablecer teléfono**
- **Permitir conexión USB**
- **Permitir a Cortana**
- **Permitir notificaciones del centro de actividades**

### <a name="new-settings-for-windows-10-team-devices"></a>Nuevas opciones para dispositivos Windows 10 Team
#### <a name="device-settings"></a>Configuración del dispositivo
- **Habilitar Visión operativa de Azure**
- **Habilitar proyección inalámbrica de Miracast**
- **Seleccione la información sobre la reunión que se muestra en la pantalla de inicio de sesión**
- **URL de imagen de fondo de pantalla de bloqueo**

### <a name="new-settings-for-windows-81-devices"></a>Nuevas opciones para dispositivos Windows 8.1
#### <a name="applicability-settings"></a>Configuración de la aplicación
- **Aplicar todas las configuraciones a Windows 10**

#### <a name="password-settings"></a>Configuración de contraseña
- **Tipo de contraseña requerida**
- **Número mínimo de conjuntos de caracteres**
- **Longitud mínima de la contraseña**
- **Número de errores de inicio de sesión consecutivos permitidos antes de que se borre el dispositivo**
- **Minutos de inactividad antes de que se apague la pantalla**
- **Expiración de la contraseña (días)**
- **Recordar el historial de contraseñas**
- **Impedir la reutilización de contraseñas anteriores**
- **Permitir contraseña de imagen y PIN**

#### <a name="browser-settings"></a>Configuración del explorador
- **Permitir la detección automática de redes de intranet**

### <a name="new-settings-for-windows-phone-81-devices"></a>Nuevas opciones para dispositivos Windows Phone 8.1
#### <a name="applicability-settings"></a>Configuración de la aplicación
- **Aplicar todas las configuraciones a Windows 10**

#### <a name="password-settings"></a>Configuración de contraseña
- **Número mínimo de conjuntos de caracteres**
- **Permitir contraseñas sencillas**
- **Recordar el historial de contraseñas**

#### <a name="device-capability-settings"></a>Configuración de las capacidades de los dispositivos
- **Permitir conexión automática a zonas Wi-Fi gratuitas**



<!--HONumber=Dec16_HO3-->


