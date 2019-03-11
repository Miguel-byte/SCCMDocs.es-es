---
title: Novedades de la versión 1810
titleSuffix: Configuration Manager
description: Obtenga detalles sobre los cambios y las nuevas características incorporados en la versión 1810 de la rama actual de Configuration Manager.
ms.date: 03/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d8a3c6c73d30d7d5e8e825cd20baa334214dceb
ms.sourcegitcommit: 33a006204f7f5f9b9acd1f3e84c4bc207362d00a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2019
ms.locfileid: "57305803"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>Novedades de la versión 1810 de la rama actual de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La actualización 1810 para la rama actual de Configuration Manager está disponible como una actualización en consola. Aplique esta actualización a los sitios que ejecuten las versiones 1710, 1802 o 1806. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.--> En este artículo se resumen los cambios y las nuevas características de Configuration Manager, versión 1810.  

Revise siempre la lista de comprobación más reciente para instalar esta actualización. Para obtener más información, vea [Lista de comprobación para la instalación de la actualización 1810](/sccm/core/servers/manage/checklist-for-installing-update-1810). Después de actualizar un sitio, revise también la [lista de comprobación posterior a la actualización](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist).

Para aprovechar las nuevas características de Configuration Manager, primero actualice los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.

> [!Note]  
> En este artículo se indican todas las características importantes de esta versión. Pero no todas las secciones están vinculadas aún a contenido actualizado con información adicional sobre las nuevas características. Vuelva a esta página con regularidad en busca de actualizaciones. Los cambios se indican mediante la etiqueta ***[Actualizado]***. Esta nota se quita una vez que se termina el contenido.  

> [!Tip]  
> Para obtener una notificación cuando se actualice esta página, copie y pegue la siguiente dirección URL en su lector de fuentes RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1810+-+Configuration+Manager%22&locale=en-us`



## <a name="bkmk_deprecated"></a> Características y sistemas operativos en desuso

Obtenga información sobre los cambios de compatibilidad antes de implementarlos en [Elementos eliminados y en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

A partir del 14 de agosto de 2018, la característica de administración híbrida de dispositivos móviles está en desuso. Para más información, vea [¿Qué es la Administración híbrida de dispositivos móviles (MDM)?](/sccm/mdm/understand/hybrid-mobile-device-management). <!--Intune feature 2683117-->  

El soporte técnico para System Center Endpoint Protection (SCEP) para Mac y Linux (todas las versiones) terminará el 31 de diciembre de 2018. La disponibilidad de nuevas definiciones de virus para SCEP para Mac y SCEP para Linux puede interrumpirse tras el fin del soporte técnico. Para obtener más información, vea la [entrada del blog de fin del soporte técnico](https://go.microsoft.com/fwlink/?linkid=870182).

Las implementaciones de servicio clásico de Azure ya están en desuso en Configuration Manager. Empiece a usar implementaciones de Azure Resource Manager para Cloud Management Gateway y el punto de distribución de nube. Para obtener más información, vea [Planear para Cloud Management Gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).
<!--
Version 1810 drops support for the following products:
-->



## <a name="bkmk_infra"></a> Infraestructura del sitio

### <a name="support-for-windows-server-2019"></a>Compatibilidad con Windows Server 2019
<!--1359195--> Configuration Manager ahora admite Windows Server 2019 y Windows Server, versión 1809, como sistemas de sitio. 

Para obtener más información, vea [Sistemas operativos compatibles con servidores de sistema de sitio](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).


### <a name="hierarchy-support-for-site-server-high-availability"></a>Compatibilidad de la jerarquía con la alta disponibilidad de servidor de sitio
<!--1358224--> Los sitios de administración central y los sitios primarios secundarios ahora pueden tener un servidor de sitio adicional en modo pasivo. 

<!--For more information, see [Site server high availability](/sccm/core/servers/deploy/configure/site-server-high-availability).-->


### <a name="improvements-to-setup-prerequisites"></a>Mejoras en los requisitos previos del programa de instalación

Al instalar o actualizar a la versión 1810, el programa de instalación de Configuration Manager ahora incluye o mejora las comprobaciones de requisitos previos siguientes:

- **Reinicio del sistema pendiente**: esta comprobación de requisitos previos ahora es más resistente. Comprueba características de Windows en otras claves del Registro. Para obtener más información, vea [Reinicio del sistema pendiente](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#pending-system-restart). <!--SCCMDocs-pr issue 3010-->  

- **Limpieza del seguimiento de cambios de SQL**: una nueva comprobación de si la base de datos del sitio tiene un trabajo pendiente de datos de seguimiento de cambios de SQL. Para obtener más información, incluido un procedimiento para comprobar y borrar este trabajo pendiente, vea [Limpieza del seguimiento de cambios de SQL](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#bkmk_changetracking). <!--SCCMDocs-pr issue 3023-->  

- **Versión de SQL Native Client**: esta comprobación de requisitos previos se actualiza para las versiones de SQL Native Client que admiten TLS 1.2. La versión mínima es [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402). Para obtener más información, vea [Versión de SQL Native Client](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-native-client). <!--SCCMDocs-pr issue 3094-->  

- **Sistema de sitio en el nodo del clúster de Windows**: El proceso de instalación de Configuration Manager ya no impide la instalación del rol de servidor de sitio en un equipo con el rol de Windows para clústeres de conmutación por error. SQL Always On requiere este rol, por lo que anteriormente no se podía colocar la base de datos del sitio en el servidor de sitio. Con este cambio, puede crear un sitio de alta disponibilidad con menos servidores usando SQL Always On y un servidor de sitio en modo pasivo. Para obtener más información, vea [Clúster de conmutación por error de Windows](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#windows-failover-cluster). <!--1359132-->  




### <a name="new-permission-for-client-notification-actions"></a>Nuevo permiso para acciones de notificación de cliente
<!--SCCMDocs-pr issue #2972--> Las acciones de notificación de cliente ahora requieren el permiso **Notificar al recurso** en la clase SMS_Collection. Los siguientes roles integrados tienen este permiso de forma predeterminada:
- Administrador total  
- Administrador de infraestructuras  

Agregue este permiso a cualquier rol personalizado que deba usar acciones de notificación de cliente. 

Para obtener más información, vea [Notificación de cliente](/sccm/core/clients/manage/client-notification).



## <a name="bkmk_content"></a> Administración de contenido

### <a name="new-boundary-group-options"></a>Nuevas opciones de grupo de límites
<!--1358749--> Los grupos de límites ahora incluyen los siguientes valores de configuración adicionales para ofrecer mayor control sobre la distribución de contenido en el entorno:

- **Preferir puntos de distribución sobre elementos del mismo nivel dentro de la misma subred**: De forma predeterminada, el punto de administración da prioridad a los orígenes de caché del mismo nivel en la parte superior de la lista de ubicaciones de contenido. Esta configuración revierte dicha prioridad para los clientes que están en la misma subred que el origen de caché del mismo nivel.  

- **Preferir puntos de distribución de nube sobre puntos de distribución**: Si tiene una sucursal con un vínculo de Internet más rápido, ahora puede dar prioridad al contenido de la nube.  

Para más información, vea [Opciones de grupo de límites para descargas del mismo nivel](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions).


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>Regla de Información de administración para la versión cliente del origen de caché del mismo nivel
<!-- 1358008 --> El nodo **Información de administración** tiene una nueva regla para identificar a los clientes que actúan como origen de caché del mismo nivel pero que no se han actualizado desde una versión cliente anterior a la 1806. La nueva regla es **Actualizar los orígenes de caché del mismo nivel a la última versión del cliente de Configuration Manager**, y forma parte del nuevo grupo de reglas de **Mantenimiento proactivo**. Los clientes de la versión anterior a la 1806 no pueden usarse como un origen de caché del mismo nivel para clientes que ejecutan la versión 1806 o alguna posterior. Seleccione **Realizar acción** para abrir una vista de dispositivo que muestre la lista de clientes. 

Para obtener más información, vea [Información de administración](/sccm/core/servers/manage/management-insights).



## <a name="bkmk_client"></a> Administración de clientes

### <a name="new-client-notification-action-to-wake-up-device"></a>Nueva acción de notificación de cliente para reactivar el dispositivo
<!--1317364--> Ahora puede reactivar clientes desde la consola de Configuration Manager aunque el cliente no esté en la misma subred que el servidor de sitio. Si necesita realizar tareas de mantenimiento o consultar dispositivos, no se ve limitado por los clientes remotos que están inactivos. El servidor de sitio usa el canal de notificación de cliente para identificar a otro cliente activo en la misma subred remota. El cliente activo envía una activación en la solicitud de la LAN (paquete mágico).

### <a name="new-option-to-perform-client-notification-from-devices-node"></a>Nueva opción para realizar la notificación de cliente desde el nodo Dispositivos
<!--1317364--> Hasta la versión 1810, la opción **Notificación de cliente** solo estaba disponible en el nodo Colección de dispositivos o cuando veía la pertenencia de una colección de dispositivos. Ahora es posible realizar una **notificación de cliente** directamente desde el nodo **Dispositivos**. Ya no es requisito estar dentro de la vista de la pertenencia a una colección. 

Para obtener más información, vea [Notificación de cliente](/sccm/core/clients/manage/client-notification).


### <a name="improvements-to-collection-evaluation"></a>Mejoras en la evaluación de recopilación
<!--1358981--> Los siguientes cambios en el comportamiento de evaluación de recopilación pueden mejorar el rendimiento del sitio:  
 
- Anteriormente, cuando se configuraba una programación de una recopilación basada en consultas, el sitio continuaba con la evaluación de la consulta aunque habilitara o no la configuración de la recopilación como **Programar una actualización completa en esta recopilación**. Para deshabilitar completamente la programación, tenía que cambiar la programación a **Ninguna**. Ahora el sitio elimina la programación cuando se deshabilita esta configuración. Para especificar una programación de evaluación de recopilación, habilite la opción para **Programar una actualización completa en esta recopilación**.  

- No puede deshabilitar la evaluación de las recopilaciones integradas como **Todos los sistemas**, pero ahora puede configurar la programación. Este comportamiento permite personalizar esta acción en el momento en que se cumplen sus requisitos empresariales. 

<!--For more information, see [How to create collections](/sccm/core/clients/manage/collections/create-collections).-->


### <a name="improvement-to-client-installation"></a>Mejora en la instalación del cliente
<!--1358840--> Al instalar el cliente de Configuration Manager, el proceso ccmsetup se pone en contacto con el punto de administración para localizar el contenido necesario. Anteriormente, en este proceso, el punto de administración solo devuelve puntos de distribución en el grupo de límites actual del cliente. Si no hay contenido disponible, el proceso de configuración retrocede para descargar contenido del punto de administración. No existe la opción de retroceder a puntos de distribución de otros grupos de límites que puedan tener el contenido necesario. Ahora el punto de administración devuelve puntos de distribución basados en la configuración del grupo de límites. 

Para obtener más información, vea [Configuración de grupos de límites](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_ccmsetup).


### <a name="improvements-to-internet-based-client-setup"></a>Mejoras en la configuración de cliente basada en Internet
<!--1359181-->
<!--move this under co-management?-->  
Esta versión simplifica aún más el proceso de configuración de cliente de Configuration Manager para clientes en Internet. El sitio publica información adicional de Azure Active Directory (Azure AD) para Cloud Management Gateway (CMG). Un cliente unido a Azure AD obtiene esta información de la instancia de CMG durante el proceso de ccmsetup, mediante el mismo inquilino al que está unido. Este comportamiento simplifica más la inscripción de dispositivos en la administración conjunta de un entorno con más de un inquilino de Azure AD. Ahora las dos únicas propiedades de ccmsetup requeridas son **CCMHOSTNAME** y **SMSSiteCode**.

<!--For more information, see [Prepare Windows 10 devices for co-management](https://docs.microsoft.com/en-us/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).-->



## <a name="bkmk_comgmt"></a> Administración conjunta

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>Directiva de cumplimiento de aplicaciones requerida para dispositivos administrados conjuntamente
<!--1358196--> Define reglas de la directiva de cumplimiento en Configuration Manager sobre las aplicaciones necesarias. Esta evaluación de la aplicación forma parte del estado de cumplimiento general que se envía a Microsoft Intune para los dispositivos administrados conjuntamente.

<!--For more information, see [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview).-->


### <a name="improvement-to-co-management-dashboard"></a>Mejora en el panel de administración conjunta
<!--1358980--> El panel de administración conjunta se ha mejorado con la siguiente información más detallada:  

- El icono **Estado de la inscripción de administración conjunta** incluye otros estados

- Un nuevo icono **Estado de la administración conjunta** con un gráfico de embudo muestra los estados del proceso de inscripción

- Un icono nuevo con recuentos de **Errores de inscripción**

![Captura de pantalla del panel de administración conjunta con los cuatro iconos superiores](media/1358980-comgmt-dashboard.png)

Para obtener más información, vea [Panel de administración conjunta](/sccm/comanage/how-to-monitor#co-management-dashboard).



<!-- ## <a name="bkmk_compliance"></a> Compliance settings -->



## <a name="bkmk_app"></a> Administración de aplicaciones

### <a name="convert-applications-to-msix"></a>Conversión de aplicaciones a MSIX
<!--3607729, fka 1359029-->
 ***[Actualización]*** A partir de la versión 1806, Configuration Manager admite la implementación del nuevo formato de paquete de aplicaciones (.msix) de Windows 10. Ahora puede convertir las aplicaciones existentes de Windows Installer (.msi) al formato MSIX.

Para obtener más información, vea [Creación de aplicaciones Windows](/sccm/apps/get-started/creating-windows-applications#bkmk_msix).  


### <a name="repair-applications"></a>Reparación de aplicaciones
<!--1357866--> Especifique una línea de comandos de reparación para los tipos de implementación de Windows Installer y el instalador de scripts. Si habilita la opción durante la implementación, hay un nuevo botón disponible en el Centro de software para **Reparar** la aplicación. Cuando se configura una aplicación con un programa de reparación, los usuarios pueden iniciar el comando desde el Centro de software. 

Para obtener más información, vea [Crear aplicaciones](/sccm/apps/deploy-use/create-applications#bkmk_dt-content) e [Implementar aplicaciones](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy-settings).


### <a name="approve-application-requests-via-email"></a>Aprobación de solicitudes de aplicaciones a través del correo electrónico
<!--1321550--> Configure notificaciones por correo electrónico para las solicitudes de aprobación de aplicaciones. Recibirá un correo electrónico cuando un usuario solicite una aplicación. Haga clic en los vínculos que aparecen en el correo electrónico para aprobar o denegar la solicitud, sin requerir la consola de Configuration Manager.

Para obtener más información, vea [Aprobar aplicaciones](/sccm/apps/deploy-use/app-approval).


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>Los métodos de detección no cargan perfiles de Windows PowerShell
<!--1359239--> Puede usar scripts de Windows PowerShell para los métodos de detección en aplicaciones y configuración de elementos de configuración. Cuando estos scripts se ejecutan en los clientes, el cliente de Configuration Manager ahora llama a PowerShell con el parámetro `-NoProfile`. Esta opción inicia PowerShell sin perfiles. 

Un perfil de PowerShell es un script que se ejecuta cuando se inicia PowerShell. Puede crear un perfil de PowerShell para personalizar el entorno y para agregar elementos específicos de la sesión a cada sesión de PowerShell que inicie. 

> [!Note]  
> Este cambio de comportamiento no se aplica a [Scripts](/sccm/apps/deploy-use/create-deploy-scripts) ni [CMPivot](/sccm/core/servers/manage/cmpivot). Ambas características ya usan este parámetro de PowerShell.    

<!--For more information, see []().-->


## <a name="bkmk_osd"></a> Implementación del sistema operativo

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>Compatibilidad de la secuencias de tareas de Windows Autopilot con dispositivos existentes
<!--3607717, fka 1358333-->

***[Actualización]*** [Windows Autopilot para los dispositivos existentes](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) ahora está disponible con Windows 10, versión 1809 o posterior. Esta nueva característica permite volver a crear una imagen y aprovisionar un dispositivo de Windows 7 para el [modo controlado por el usuario de Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) mediante una única secuencia de tareas nativa de Configuration Manager. 

Para obtener más información, consulte [Windows Autopilot para dispositivos existentes](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices).


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>Especificación de la unidad para el mantenimiento sin conexión de imágenes de SO  
<!--1358924--> Ahora, especifique la unidad que usa Configuration Manager al agregar actualizaciones de software a imágenes del sistema operativo y paquetes de actualización del sistema operativo. Este proceso puede consumir una gran cantidad de espacio en disco con los archivos temporales, por lo que esta opción le ofrece flexibilidad para seleccionar la unidad que se va a usar. 

Para obtener más información, vea [Administrar imágenes del sistema operativo](/sccm/osd/get-started/manage-operating-system-images#bkmk_servicing-drive) o [Administrar paquetes de actualización del sistema operativo](/sccm/osd/get-started/manage-operating-system-upgrade-packages#bkmk_servicing-drive).


### <a name="task-sequence-support-for-boundary-groups"></a>Compatibilidad de la secuencia de tareas con los grupos de límites
<!--1359025--> Cuando un dispositivo ejecuta una secuencia de tareas y necesita adquirir contenido, ahora usa comportamientos de grupo de límites similares al cliente de Configuration Manager.   

Para obtener más información, consulte [Boundary groups (Grupos de límites)](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgr-osd).


### <a name="improvements-to-driver-maintenance"></a>Mejoras en el mantenimiento de los controladores
<!--3607716, fka 1358270-->
 ***[ACTUALIZACIÓN]*** Ahora, los paquetes de controladores tienen campos de metadatos adicionales para **Fabricante** y **Modelo**. Use estos campos para etiquetar los paquetes de controladores con información para ayudar en el mantenimiento general o para identificar controladores antiguos y duplicados que se pueden eliminar.

Para obtener más información, consulte [Administrar controladores](/sccm/osd/get-started/manage-drivers).


### <a name="new-task-sequence-variable-for-last-action-name"></a>Nueva variable de secuencia de tareas para el nombre de la última acción
<!--SCCMDocs-pr issue #2964--> Junto con la variable de secuencia de tareas _SMSTSLastActionRetCode, la secuencia de tareas también establece una nueva variable **_SMSTSLastActionName**. Además, registra este valor en el archivo smsts.log. Esta nueva variable es beneficiosa al solucionar problemas de una secuencia de tareas. Cuando se produce un error en un paso, un script personalizado puede incluir el nombre del paso junto con el código de retorno.

Para más información, vea [Task sequence variables](/sccm/osd/understand/task-sequence-variables#SMSTSLastActionName) (Variables de secuencia de tareas).



<!-- ## <a name="bkmk_userxp"></a> Software Center -->



## <a name="bkmk_sum"></a> Actualizaciones de software

### <a name="phased-deployment-of-software-updates"></a>Implementación por fases de las actualizaciones de software
<!--1358146--> Cree implementaciones por fases de las actualizaciones de software. Las Implementaciones por fases permiten organizar un lanzamiento de software coordinado y secuencial según criterios y grupos personalizables.

Para más información, vea [Crear implementaciones por fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>Mejoras en las ventanas de mantenimiento para actualizaciones de software
<!--vso2839307--> La siguiente configuración de cliente está incluida en el grupo **Actualizaciones de software** para controlar el comportamiento de instalación de actualizaciones de software en ventanas de mantenimiento: 

**Habilitar la instalación de actualizaciones en la ventana de mantenimiento "Todas las implementaciones" cuando esté disponible la ventana de mantenimiento "Actualización de software"**

De forma predeterminada, esta opción es **No** para mantener la coherencia con el comportamiento existente. Cámbiela a **Sí** para permitir que los clientes usen otras ventanas de mantenimiento disponibles para instalar actualizaciones de software.

<!--For more information, see []().-->

### <a name="improvement-to-software-updates-maintenance"></a>Mejora del mantenimiento de las actualizaciones de software
<!--2839349--> Las tareas de limpieza de WSUS ahora se ejecuta en sitios secundarios. Se ejecuta la limpieza de WSUS para actualizaciones expiradas, mientras que las actualizaciones sustituidas para sitios secundarios se rechazan.

Para obtener más información, vea [WSUS cleanup behavior starting in version 1810](/sccm/sum/deploy-use/software-updates-maintenance#wsus-cleanup-behavior-starting-in-version-1810) (Comportamiento de limpieza de WSUS a partir de la versión 1810).

## <a name="bkmk_report"></a> Generación de informes

### <a name="improvement-to-lifecycle-dashboard"></a>Mejora en el panel de ciclo de vida
<!--1358702--> El panel de ciclo de vida del producto ahora incluye información para **System Center 2012 Configuration Manager y versiones posteriores**. 

También hay un nuevo informe, **Ciclo de vida 05A: panel de ciclo de vida del producto**. Incluye información similar a la del panel en consola.

Para más información sobre este panel, vea [Uso del panel de ciclo de vida del producto](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard).


### <a name="improvement-to-data-warehouse"></a>Mejora en el almacenamiento de datos
<!--1358870--> Ya es posible sincronizar más tablas de la base de datos de sitio en el almacenamiento de datos. Este cambio permite crear más informes según sus requisitos empresariales.

Para obtener más información, vea [Almacenamiento de datos](/sccm/core/servers/manage/data-warehouse).



<!-- ## <a name="bkmk_inv"></a> Inventory -->




<!-- ## <a name="bkmk_protect"></a> Protect devices-->




## <a name="bkmk_admin"></a> Consola de Configuration Manager

### <a name="configuration-manager-administrator-authentication"></a>Autenticación del administrador de Configuration Manager
<!--1357013--> Ahora puede especificar el nivel mínimo de autenticación para que los administradores accedan a sitios de Configuration Manager. Esta característica exige que los administradores inicien sesión en Windows con el nivel requerido. Para configurar esta opción, busque la pestaña **Autenticación** en **Configuración de jerarquía**. 

Para más información, vea [Plan for the SMS Provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth) (Planear el proveedor de SMS).


### <a name="support-center"></a>Support Center
<!--1357489--> Use el Centro de soporte técnico para solucionar los problemas de los clientes, visualizar los registros en tiempo real o capturar el estado de un equipo cliente de Configuration Manager para su posterior análisis. El Centro de soporte técnico es una única herramienta que combina muchas herramientas de solución de problemas de administrador. Puede encontrar el programa de instalación de Support Center en el servidor de sitio en la carpeta **cd.latest\SMSSETUP\Tools\SupportCenter**.

Para obtener más información, vea [Centro de soporte técnico](/sccm/core/support/support-center).


### <a name="management-insights-dashboard"></a>Panel Información de administración
<!--1357979-->

El nodo **Información de administración** ahora incluye un panel gráfico. Este panel muestra información general de los estados de la regla, con lo que le resultará más fácil mostrar el progreso. En el panel se incluyen los iconos siguientes:

- **Índice de Información de administración**: realiza el seguimiento del progreso general en las reglas de información de administración. El índice es un promedio ponderado. Las reglas críticas valen más. Este índice proporciona el menor peso a las reglas opcionales.  

- **Grupos de Información de administración**: muestra el porcentaje de las reglas en cada grupo.  

- **Prioridad de Información de administración**: muestra el porcentaje de las reglas por prioridad.  

- **Toda la información**: una tabla de información, incluida la prioridad y el estado.  

![Captura de pantalla del panel de información de administración](media/1357979-management-insights-dashboard.png)

Para obtener más información, vea [Información de administración](/sccm/core/servers/manage/management-insights).


### <a name="improvements-to-cmpivot"></a>Mejoras en CMPivot
<!--1359068--> CMPivot incluye las siguientes mejoras:

- Guardar consultas **favoritas**  

- En la pestaña Resumen de la consulta, seleccione el número de dispositivos con errores o sin conexión y, a continuación, seleccione la opción **Crear colección**. 

Para obtener más información sobre el rendimiento y las mejoras para solucionar problemas en CMPivot, consulte [Mejoras en los scripts](#bkmk_scripts).

<!--For more information on CMPivot, see [CMPivot](/sccm/core/servers/manage/cmpivot).-->


### <a name="bkmk_scripts"></a> Mejoras para scripts
<!--1358239--> Ahora puede ver una salida de script detallada sin formato o con formato JSON estructurado. Este formato permite leer y analizar la salida de manera más sencilla. 

Las siguientes mejoras de solución de problemas y rendimiento se aplican a CMPivot y scripts:

- Los clientes actualizados devuelven resultados inferiores a 80 KB al sitio a través de un canal de comunicación rápido. Este cambio aumenta el rendimiento de la visualización de resultados del script o la consulta.  

- Otros registros para la solución de problemas  

<!--For more information, see the following articles:  

- [Create and run PowerShell scripts from the Configuration Manager console](/sccm/apps/deploy-use/create-deploy-scripts)  

- [CMPivot](/sccm/core/servers/manage/cmpivot)  -->


### <a name="sms-provider-api"></a>API del proveedor de SMS
<!--1321523--> El proveedor de SMS ahora proporciona acceso de interoperabilidad de solo lectura a la API a WMI a través de HTTPS. El **proveedor de SMS** aparece como un rol con una opción para permitir la comunicación a través de Cloud Management Gateway. El uso actual de este valor es la habilitación de las aprobaciones de aplicaciones a través del correo electrónico desde un dispositivo remoto. Para obtener más información, vea [Aprobación de solicitudes de aplicaciones a través del correo electrónico](#approve-application-requests-via-email).



## <a name="bkmk_opmdm"></a> MDM local

### <a name="an-intune-connection-is-no-longer-required-for-new-on-premises-mdm-deployments"></a>Ya no se necesita una conexión de Intune para las nuevas implementaciones de MDM locales
<!--1359124--> El requisito previo de MDM local para configurar una suscripción de Microsoft Intune ya no es necesario para las nuevas implementaciones. La organización sigue necesitando licencias de Intune para usar esta característica. Actualmente no se puede quitar la conexión de Intune de las implementaciones locales de MDM existentes. Para más información, vea la [entrada del blog de soporte técnico de Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).



## <a name="other-updates"></a>Otras actualizaciones

Además de nuevas características, esta versión también incluye cambios adicionales como, por ejemplo, correcciones de errores. Para obtener más información, vea [Resumen de cambios en la rama actual de Configuration Manager, versión 1810](https://support.microsoft.com/help/4482169).

Para obtener más información sobre los cambios en los cmdlets de Windows PowerShell para Configuration Manager, vea [las notas de la versión de PowerShell 1810](https://docs.microsoft.com/powershell/sccm/1810-release-notes?view=sccm-ps).

El siguiente paquete acumulativo de actualizaciones (4486457) está disponible en la consola a partir del 25 de enero de 2019: [Paquete acumulativo de la rama actual de Configuration Manager, versión 1810](https://support.microsoft.com/help/4486457).


### <a name="hotfixes"></a>Revisiones

Se ofrecen estas revisiones adicionales para solucionar problemas específicos:

| Id. | Título | Fecha | En la consola |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | El certificado del conector de Microsoft Intune no se renueva en Configuration Manager | 18 de enero de 2019 | Sí |
| [4490434](https://support.microsoft.com/help/4490434) | Se crean columnas de detección de usuarios duplicadas en Configuration Manager | 22 de febrero de 2019 | Sí |
| [4490575](https://support.microsoft.com/help/4490575) | Las instalaciones de actualización dejan de responder o nunca muestran la finalización en Configuration Manager, versión 1810 | 22 de febrero de 2019 | Sí |


## <a name="next-steps"></a>Pasos siguientes

Cuando esté listo para instalar esta versión, vea [Instalación de actualizaciones para Configuration Manager](/sccm/core/servers/manage/updates) y [Lista de comprobación para la instalación de la actualización 1810](/sccm/core/servers/manage/checklist-for-installing-update-1810).

> [!TIP]  
> Para instalar un sitio nuevo, use una versión de línea de base de Configuration Manager.  
>
>  Más información acerca de:    
>   - [Instalación de nuevos sitios](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Versiones de línea de base y versiones de actualización](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Para saber los problemas conocidos e importantes, vea las [Notas de la versión](/sccm/core/servers/deploy/install/release-notes).

Después de actualizar un sitio, revise también la [lista de comprobación posterior a la actualización](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist).
