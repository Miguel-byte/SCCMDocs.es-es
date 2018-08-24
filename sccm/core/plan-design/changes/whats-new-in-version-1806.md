---
title: Novedades de la versión 1806
titleSuffix: Configuration Manager
description: Obtenga detalles sobre los cambios y las nuevas funciones incorporados en la versión 1806 de la rama actual de Configuration Manager.
ms.date: 07/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c6ae28a50f3145420895b295ebe730fb7b2a9a7
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386066"
---
# <a name="whats-new-in-version-1806-of-configuration-manager-current-branch"></a>Novedades de la versión 1806 de la rama actual de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La actualización 1806 para la rama actual de Configuration Manager está disponible como una actualización en la consola. Aplique esta actualización en los sitios que ejecuten las versiones 1706, 1710 o 1802. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

> [!Important]  
> En este artículo se indican todas las características importantes de esta versión. Pero no todas las secciones están vinculadas aún a contenido actualizado con información adicional sobre las nuevas características. Vuelva a esta página con regularidad en busca de actualizaciones. Los cambios se indican mediante la etiqueta ***[Actualizado]***. Esta nota se quita una vez que se termina el contenido.  

<!--
Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in System Center Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4101375).
-->

<!--
The following additional updates to this release are also now available:
- [Update rollup for System Center Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4057517)
-->


En las secciones siguientes se proporcionan detalles sobre los cambios y las nuevas características de la versión 1806 de la rama actual de Configuration Manager.  



<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1806 drops support for the following products:
-->



## <a name="site-infrastructure"></a>Infraestructura del sitio

### <a name="cmpivot"></a>CMPivot
<!--1358456--> Configuration Manager siempre ha proporcionado un gran almacén centralizado de datos de dispositivo, que los clientes utilizan para informes. El sitio normalmente recopila estos datos cada semana. CMPivot es una nueva utilidad en la consola que ahora proporciona acceso al estado en tiempo real de los dispositivos del entorno. Esta utilidad ejecuta una consulta inmediatamente en todos los dispositivos conectados actualmente en la colección de destino y devuelve los resultados. A continuación, puede filtrar y agrupar estos datos en la herramienta. Mediante el suministro de datos en tiempo real de los clientes en línea, puede contestar preguntas empresariales, solucionar problemas y responder a incidentes de seguridad más rápidamente. 

Para obtener más información, vea [CMPivot](/sccm/core/servers/manage/cmpivot).  


### <a name="site-server-high-availability"></a>Alta disponibilidad de servidor de sitio
<!--1128774--> La alta disponibilidad para un rol de servidor de sitio primario independiente es una solución basada en Configuration Manager para instalar un servidor de sitio adicional en modo pasivo. El servidor de sitio en modo pasivo se suma al servidor de sitio existente que está en modo activo. Un servidor de sitio en modo pasivo está disponible para uso inmediato, cuando sea necesario. 

Vea los siguientes artículos para más información: 
- [Alta disponibilidad de servidor de sitio](/sccm/core/servers/deploy/configure/site-server-high-availability) 
- [Diagrama de flujo: configuración de un servidor de sitio en modo pasivo](/sccm/core/servers/deploy/configure/passive-site-server-flowchart)
- [Diagrama de flujo: promoción del servidor de sitio (planificada)](/sccm/core/servers/deploy/configure/promote-site-server-flowchart)
- [Diagrama de flujo: promoción del servidor de sitio (no planificada)](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart)


### <a name="improvements-to-management-insights"></a>Mejoras en la información de administración
Esta versión incluye las siguientes mejoras en la información de administración:  

- Alguna información de administración ahora ofrece la opción de realizar una acción. Esta acción es ir al nodo asociado en la consola o mostrar una vista filtrada basada en una consulta.<!--1357930-->  

- Hay un nuevo grupo de mantenimiento proactivo disponible con seis nuevas reglas, lo que ayuda a resaltar posibles problemas de configuración que se deben evitar mediante un mantenimiento regular.<!--1352184-->  

Para obtener más información, vea [Información de administración](/sccm/core/servers/manage/management-insights).


### <a name="configuration-manager-tools"></a>Herramientas de Configuration Manager
<!--1357145--> Las herramientas de servidor y cliente de Configuration Manager ahora se incluyen en el servidor. Búsquelas en la carpeta `CD.Latest\SMSSETUP\Tools` del servidor de sitio. No se necesita ninguna otra instalación. 

Para obtener más información, vea [Herramientas de Configuration Manager](/sccm/core/support/tools).


### <a name="exclude-active-directory-containers-from-discovery"></a>Exclusión de contenedores de Active Directory de la detección
<!--1358143--> Para reducir el número de objetos detectados, excluya determinados contenedores de la detección de sistemas de Active Directory. 



## <a name="content-management"></a>Administración de contenido

### <a name="configure-a-remote-content-library-for-the-site-server"></a>Configuración de una biblioteca de contenido remoto para el servidor de sitio
<!--1357525--> Para configurar la alta disponibilidad del servidor de sitio o para liberar espacio de disco duro en los servidores de sitio primario o de administración central, reubique la biblioteca de contenido en otra ubicación de almacenamiento. Mueva la biblioteca de contenido a otra unidad del servidor de sitio, un servidor independiente o discos tolerantes a errores de una red de área de almacenamiento (SAN). 

Vea los siguientes artículos para más información: 
- [La biblioteca de contenido](/sccm/core/plan-design/hierarchy/the-content-library)
- [Diagrama de flujo: administración de la biblioteca de contenido](/sccm/core/plan-design/hierarchy/manage-content-library-flowchart)


### <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Compatibilidad con puntos de distribución de nube para Azure Resource Manager
<!--1322209--> Al crear un punto de distribución de nube, el asistente ahora proporciona la opción de crear una **implementación de Azure Resource Manager**. Azure Resource Manager es una moderna plataforma para administrar todos los recursos de una solución como una única entidad, denominada grupo de recursos. Al implementar un punto de distribución de nube con Azure Resource Manager, el sitio usa Azure Active Directory para autenticar y crear los recursos de nube necesarios. Esta implementación modernizada no requiere el certificado de administración de Azure clásico. 

La documentación de las características del punto de distribución de nube también se ha revisado y mejorado. Vea los siguientes artículos para más información:
- [Usar un punto de distribución basado en la nube](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)   
- [Instalar puntos de distribución basados en la nube](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)  


### <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Compatibilidad de puntos de distribución de extracción con puntos de distribución de nube como orígenes  
<!--1321554--> Muchos clientes usan puntos de distribución de extracción en sucursales u oficinas remotas que descargan contenido desde un punto de distribución de origen en la WAN. Si las oficinas remotas tienen una mejor conexión a Internet o si quiere reducir la carga en los vínculos a WAN, ahora puede usar como origen un punto de distribución de nube en Microsoft Azure. Cuando se agrega un origen en la pestaña **Punto de distribución de extracción** de las propiedades del punto de distribución, cualquier punto de distribución de nube en el sitio aparece como un punto de distribución disponible. El comportamiento de ambos roles de sistema de sitio sigue siendo el mismo en cualquier caso. 

Para obtener más información, vea [Usar un punto de distribución de extracción](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).


### <a name="enable-distribution-points-to-use-network-congestion-control"></a>Habilitación de los puntos de distribución para usar el control de congestión de red
<!--1358112--> Windows Low Extra Delay Background Transport (LEDBAT) es una característica de Windows Server que ayuda a administrar transferencias de red en segundo plano. En los puntos de distribución que se ejecuten en versiones compatibles de Windows Server, habilite una opción para ayudar a ajustar el tráfico de red. Los clientes solo usan el ancho de banda de red cuando está disponible. 

Para obtener más información, vea [Windows LEDBAT](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#windows-ledbat).


### <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Compatibilidad de descarga parcial en la memoria caché del mismo nivel de cliente para reducir la utilización de la WAN
<!--1357346--> Los orígenes de la caché del mismo nivel de cliente ahora pueden dividir el contenido en partes. Estas partes reducen al mínimo la transferencia de red para usar menos WAN. El punto de administración proporciona un seguimiento más detallado de las partes de contenido e intenta eliminar más de una descarga del mismo contenido por grupo de límites. 

Para obtener más información, vea [Partial download support](/sccm/core/plan-design/hierarchy/client-peer-cache#bkmk_parts) (Compatibilidad con la descarga parcial). 


### <a name="boundary-group-options-for-peer-downloads"></a>Opciones de grupo de límites para descargas del mismo nivel
<!--1356193--> Los grupos de límites ahora incluyen valores de configuración adicionales para ofrecerle mayor control sobre la distribución de contenido en su entorno. Esta versión agrega las siguientes opciones:  

- **Permitir descargas del mismo nivel en este grupo de límites**: esta opción está habilitada de forma predeterminada. El punto de administración proporciona a los clientes una lista de ubicaciones de contenido que incluye orígenes del mismo nivel. Este valor afecta también a la aplicación de los identificadores de grupo para la optimización de entrega.  

- **Durante las descargas del mismo nivel, solo use elementos del mismo nivel en la misma subred**: esta configuración depende de la anterior. Si habilita esta opción, el punto de administración solo se incluye en los orígenes del mismo nivel de la lista de ubicaciones de contenido que se encuentran en la misma subred que el cliente.  



<!-- ## Migration  -->



## <a name="client-management"></a>Administración de cliente

### <a name="improvement-to-client-push-security"></a>Mejora de seguridad de inserción de cliente
<!--1358204--> Cuando se usa el método de inserción de cliente para la instalación del cliente de Configuration Manager, el sitio ahora puede requerir autenticación mutua Kerberos. Esta mejora ayuda a proteger la comunicación entre el servidor y el cliente. 

Para obtener más información, vea [Cómo instalar clientes con inserción de cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).


### <a name="bkmk_ehttp"></a> Sistema de sitios HTTP mejorado
<!--1356889,1358228--> Es recomendable utilizar la comunicación HTTPS para todas las vías de comunicación de Configuration Manager, pero puede ser un reto para algunos clientes debido a la sobrecarga de administración de certificados PKI. La introducción de la integración de Azure Active Directory (Azure AD) reduce algunos requisitos de certificado, pero no todos. 

Esta versión incluye mejoras en la forma en que los clientes se comunican con los sistemas de sitio. En las propiedades del sitio, pestaña **Comunicación de equipo cliente**, seleccione la opción **HTTPS o HTTP** y habilite la nueva opción **Use Configuration Manager-generated certificates for HTTP site systems** (Usar certificados generados por Configuration Manager para sistemas de sitio HTTP). Esta es una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features).

Esta opción es compatible con los siguientes escenarios primarios:  

- **Punto de administración Cliente a HTTP**<!--1356889-->: los [dispositivos unidos a Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) pueden comunicarse a través de una instancia de Cloud Management Gateway (CMG) con un punto de administración configurado para HTTP. El servidor de sitio genera un certificado para el punto de administración para que pueda comunicarse a través de un canal seguro.   

- **Punto de distribución Cliente a HTTP**<!--1358228-->: un grupo de trabajo o un cliente unido a Azure AD puede descargar contenido a través de un canal seguro desde un punto de distribución configurado para HTTP.   


### <a name="azure-ad-device-identity"></a>Identidad del dispositivo de Azure AD 
<!--1358460--> Un [dispositivo unido a Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) o un [dispositivo de Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices) sin un usuario de Azure AD con sesión iniciada puede comunicarse de forma segura con su sitio asignado. La identidad del dispositivo basado en la nube ahora es suficiente para autenticarse con el punto de administración y CMG.  


### <a name="cmtrace-installed-with-client"></a>Herramienta CMTrace instalada con el cliente
<!--1357971--> La herramienta de visualización del registro CMTrace ahora se instala automáticamente junto con el cliente de Configuration Manager. Se agrega al directorio de instalación del cliente, que de forma predeterminada es `%WinDir%\ccm\cmtrace.exe`. 

Para obtener más información, vea [CMTrace](/sccm/core/support/cmtrace).


### <a name="cloud-management-dashboard"></a>Panel de administración en la nube
<!--1358461--> El nuevo panel de administración en la nube proporciona una vista centralizada para el uso de Cloud Management Gateway (CMG). Cuando el sitio está incorporado con Azure AD, también muestra los datos sobre los usuarios en la nube y los dispositivos. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**. Seleccione el nodo **Administración en la nube** y vea los iconos del panel.  

Esta característica también incluye el **analizador de conexión de CMG** para la comprobación en tiempo real que ayuda a solucionar problemas. La utilidad en la consola comprueba el estado actual del servicio y el canal de comunicación a través del punto de conexión de CMG a todos los puntos de administración que permiten el tráfico CMG. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Cloud Services** y seleccione **Cloud Management Gateway**. Seleccione la instancia de CMG de destino y luego haga clic en **Analizador de conexión** en la cinta de opciones.


### <a name="improvements-to-cloud-management-gateway"></a>Mejoras en Cloud Management Gateway

La versión 1806 incluye las mejoras siguientes en Cloud Management Gateway (CMG):

#### <a name="simplified-client-bootstrap-command-line"></a>Línea de comandos de arranque de cliente simplificada
<!--1358215--> Al instalar el cliente de Configuration Manager en Internet a través de CMG, la línea de comandos ahora necesita menos propiedades. Esta mejora reduce el tamaño de la línea de comandos usada en Microsoft Intune al prepararse para la administración conjunta. 

Las siguientes propiedades de línea de comandos son necesarias en todos los escenarios:
  - CCMHOSTNAME  
  - SMSSITECODE  

Las propiedades siguientes son necesarias al usar Azure AD para la autenticación de cliente en lugar de certificados de autenticación de cliente basada en PKI:
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

La siguiente propiedad es obligatoria si el cliente volverá a la intranet:
  - SMSMP  

En el ejemplo siguiente se incluyen todas las propiedades anteriores:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

<!--For more information, see [Client installation properties](/sccm/core/clients/deploy/about-client-installation-properties).-->

#### <a name="download-content-from-a-cmg"></a>Descargar contenido desde un CMG
<!--1358651--> Anteriormente, era necesario implementar un punto de distribución de nube y CMG como roles independientes. Una instancia de CMG ahora también puede servir contenido a los clientes. Esta funcionalidad reduce los certificados necesarios y el costo de máquinas virtuales de Azure. Para activar esta característica, habilite la nueva opción **Allow CMG to function as a cloud distribution point and serve content from Azure storage** (Permitir que CMG funcione como un punto de distribución de nube y servir el contenido desde el almacenamiento de Azure) en la pestaña **Settings** (Configuración) de las propiedades de CMG. 

#### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>El certificado raíz de confianza no es necesario con Azure AD
<!--503899--> Para crear una instancia de CMG ya no es necesario proporcionar un [certificado raíz de confianza](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-trusted-root-certificate-to-clients) en la página Configuración. Este certificado no es necesario cuando se usa Azure Active Directory (Azure AD) para la autenticación de cliente, pero solía ser necesario en el asistente. Si usa certificados de autenticación de cliente PKI, entonces todavía debe agregar un certificado raíz de confianza a la CMG.



## <a name="co-management"></a>Administración conjunta

### <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Sincronizar directiva MDM desde Microsoft Intune para un dispositivo administrado conjuntamente
<!--1357377--> Al cambiar una carga de trabajo de administración conjunta, los dispositivos administrados conjuntamente sincronizan automáticamente la directiva de MDM de Microsoft Intune. Esta sincronización también se produce al iniciar la acción **Descargar directiva de equipo** desde Notificaciones de cliente en la consola de Configuration Manager. 

Para obtener más información, vea [Cambiar las cargas de trabajo de Configuration Manager a Intune](/sccm/core/clients/manage/co-management-switch-workloads).


### <a name="transition-new-workloads-to-intune-using-co-management"></a>Transición de nuevas cargas de trabajo a Intune mediante la administración conjunta
Las siguientes cargas de trabajo ahora pueden pasar de Configuration Manager a Intune después de habilitar la administración conjunta:  

- **Configuración del dispositivo**<!--1357903-->: esta carga de trabajo permite usar Intune para implementar directivas de MDM y seguir usando Configuration Manager para la implementación de aplicaciones.  

- **Office 365**<!--1357841-->: los dispositivos no instalan implementaciones de Office 365 desde Configuration Manager.  

- **Aplicaciones móviles**<!--1357892-->: las aplicaciones disponibles implementadas desde Intune están disponibles en el Portal de empresa. Las aplicaciones implementadas desde Configuration Manager están disponibles en el Centro de software. Esta es una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features).  

Para realizar la transición de estas cargas de trabajo, vaya a la página de propiedades de administración conjunta y mueva la barra deslizante de la carga de trabajo de Configuration Manager a **Piloto** o a **Todo**. 

Para más información, vea [Administración conjunta para dispositivos de Windows 10](/sccm/core/clients/manage/co-management-overview).


### <a name="support-for-multiple-hierarchies-to-one-intune-tenant"></a>Compatibilidad con varias jerarquías para un inquilino de Intune
<!--1357944--> Algunos clientes tienen varias jerarquías de Configuration Manager y quieren consolidar en el futuro en un único inquilino para Azure Active Directory y Microsoft Intune. Ahora la administración conjunta permite conectar más de un entorno de Configuration Manager al mismo inquilino de Intune.

Para obtener más información, vea [Preparar dispositivos de Windows 10 para la administración conjunta](/sccm/core/clients/manage/co-management-prepare).
 


## <a name="compliance-settings"></a>Configuración de cumplimiento

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Configurar SmartScreen de Windows Defender para Microsoft Edge
<!--1353701--> La directiva de configuración de cumplimiento del explorador Microsoft Edge agrega las tres configuraciones siguientes para SmartScreen de Windows Defender: 
- Permitir SmartScreen
- Los usuarios pueden invalidar los avisos de SmartScreen de los sitios
- Los usuarios pueden invalidar los avisos de SmartScreen para los archivos

Para obtener más información, vea [Configuración de las opciones de Microsoft Edge](/sccm/compliance/deploy-use/browser-profiles).


### <a name="scap-extensions"></a>Extensiones SCAP
<!--1357552--> Convierta el contenido de Security Content Automation Protocol (SCAP) en líneas de base de configuración de cumplimiento y genere informes SCAP mediante una extensión de consola. Esta característica además incluye un nuevo panel para visualizar el cumplimiento del cliente, así como el cumplimiento de reglas de XCCDF. 

Para obtener más información, vea [Extensiones de Security Content Automation Protocol (SCAP)](/sccm/compliance/plan-design/scap/about-scap).



## <a name="application-management"></a>Administración de aplicaciones

### <a name="phased-deployment-of-applications"></a>Implementación de aplicaciones por fases
<!--1358147--> Cree una implementación por fases para una aplicación. Las Implementaciones por fases permiten organizar un lanzamiento de software coordinado y secuencial según criterios y grupos personalizables. Por ejemplo, implemente la aplicación en una colección piloto y luego continúe automáticamente con la implementación según los criterios de éxito. 

Vea los siguientes artículos para más información:  

- [Creación de una implementación por fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Administración y supervisión de implementaciones por fases](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  


### <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Aprovisionar los paquetes de aplicación de Windows para todos los usuarios en un dispositivo
<!--1358310--> Aprovisione una aplicación con un paquete de aplicación de Windows para todos los usuarios del dispositivo. Un ejemplo común de este escenario es el aprovisionamiento de una aplicación de Microsoft Store para empresas y educación —por ejemplo, Minecraft: Education Edition— en todos los dispositivos usados por los alumnos en una escuela. Anteriormente, Configuration Manager solo admitía la instalación de estas aplicaciones por usuario. Tras iniciar sesión en un dispositivo nuevo, un estudiante tendría que esperar para obtener acceso a una aplicación. Ahora, al aprovisionarse la aplicación en el dispositivo para todos los usuarios, estos pueden empezar a trabajar más rápidamente. 

Para obtener más información, vea [Creación de aplicaciones Windows](/sccm/apps/get-started/creating-windows-applications#bkmk_provision).


### <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integración de la Herramienta de personalización de Office en el instalador de Office 365
<!--1358149--> La Herramienta de personalización de Office está ahora integrada con el programa de instalación de Office 365 en la consola de Configuration Manager. Al crear una implementación de Office 365, configure de manera dinámica la capacidad de administración más reciente de Office. Microsoft actualiza la Herramienta de personalización de Office cuando publica nuevas compilaciones de Office 365. Esta integración permite aprovechar la nueva capacidad de administración de Office 365 en cuanto está disponible. 

Para obtener más información, consulte [Implementación de aplicaciones de Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).


### <a name="support-for-new-windows-app-package-formats"></a>Compatibilidad con nuevos formatos de paquete de aplicaciones de Windows
<!--1357427--> Configuration Manager admite ahora la implementación de nuevos formatos de paquete de aplicaciones (.msix) y lote de aplicaciones (.msixbundle) de Windows 10. 

Para obtener más información, vea [Creación de aplicaciones Windows](/sccm/apps/get-started/creating-windows-applications#bkmk_general).


### <a name="uninstall-application-on-approval-revocation"></a>Desinstalación de aplicaciones al revocarse la aprobación
<!--1357891--> El comportamiento de revocación de la aprobación de una aplicación ha cambiado. Ahora cuando se deniega la solicitud de la aplicación, el cliente desinstala la aplicación del dispositivo del usuario. Este comportamiento exige que se habilite la [característica opcional](https://docs.microsoft.com/en-us/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Aprobación de solicitudes de aplicación para los usuarios por dispositivo**. 

Para obtener más información, consulte [Deploy applications](/sccm/apps/deploy-use/deploy-applications#bkmk_approval) (Implementar aplicaciones).


### <a name="package-conversion-manager"></a>Administrador de conversión de paquetes 
<!--1357861--> El Administrador de conversión de paquetes es ahora una herramienta integrada que permite convertir paquetes de Configuration Manager 2007 heredados en aplicaciones de la rama actual de Configuration Manager. Luego, pueden usarse las características de aplicaciones como dependencias, reglas de requisitos y afinidad entre usuario y dispositivo.

Comience con las siguientes acciones desde el nodo **Paquetes** de la consola de Configuration Manager:  

   - **Analyze Package** (Analizar paquete): iniciar el proceso de conversión con el análisis del paquete.  

   - **Convert Package** (Convertir paquete): algunos paquetes pueden convertirse fácilmente en las aplicaciones con esta acción.  

   - **Fix and Convert** (Corregir y convertir): algunos paquetes requieren que se corrijan los problemas antes de su conversión en aplicaciones.  

Luego vaya al panel **Estado de conversión del paquete** del área de trabajo **Supervisión**. Este nuevo panel muestra el análisis general y el estado de conversión de los paquetes del sitio. Esta es una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features).



## <a name="os-deployment"></a>Implementación del sistema operativo

### <a name="improvements-to-phased-deployments"></a>Mejoras en las implementaciones por fases

Esta versión incluye las siguientes mejoras en las implementaciones por fases:  

#### <a name="create-a-phased-deployment-with-manually-configured-phases"></a>Creación de una implementación por fases con fases configuradas manualmente
<!--1358148--> En una secuencia de tareas, ahora puede configurar manualmente cuando cree una implementación por fases. Agregue un máximo de diez fases adicionales desde la pestaña **Fases** del asistente Crear una implementación por fases. Puede seguir creando automáticamente una implementación predeterminada de dos fases. 

Para obtener más información, vea [Creación de implementaciones por fases para una secuencia de tareas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence#bkmk_manual).

#### <a name="phased-deployment-status"></a>Estado de implementación por fases
<!--1358577--> Las implementaciones por fases ahora tienen una experiencia de supervisión nativa. En el nodo **Implementaciones** del área de trabajo **Supervisión**, seleccione una implementación por fases y luego haga clic en **Estado de implementación por fases** en la cinta de opciones. 

Para obtener más información, vea [Administración y supervisión de implementaciones por fases](/sccm/osd/deploy-use/manage-monitor-phased-deployments).  

#### <a name="gradual-rollout-during-phased-deployments"></a>Lanzamiento gradual durante las implementaciones por fases
<!--1358578--> Durante una implementación por fases, el lanzamiento de cada fase ahora puede realizarse de forma gradual. Este comportamiento ayuda a mitigar el riesgo de problemas de implementación y disminuye la carga en la red provocada por la distribución de contenido a los clientes. El sitio puede habilitar la disponibilidad del software de forma gradual en función de la configuración de cada fase. Cada cliente de una fase tiene una fecha límite en relación con el tiempo de disponibilidad del software. La ventana de tiempo entre el tiempo disponible y la fecha límite es la misma para todos los clientes de una fase. 

Para obtener más información, vea [Configuración de fase](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence#bkmk_settings).  


### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Mejoras en la secuencia de tareas de actualización en contexto de Windows 10
<!--1358500--> La plantilla de secuencia de tareas predeterminada para la actualización local de Windows 10 ahora incluye otro grupo nuevo con las acciones recomendadas que se deben agregar en caso de error del proceso de actualización. Estas acciones facilitan la solución de problemas. Una de estas herramientas es Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). Es una herramienta de diagnóstico independiente para obtener detalles sobre el motivo de que una actualización de Windows 10 se haya realizado incorrectamente. 

Para obtener más información, vea [Crear una secuencia de tareas para actualizar un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-on-failure).


### <a name="improvements-to-pxe-enabled-distribution-points"></a>Mejoras en los puntos de distribución habilitados con PXE
<!--1357580--> En la pestaña **PXE** de las propiedades del punto de distribución, active **Enable a PXE responder without Windows Deployment Service** (Habilitar un respondedor PXE sin Servicios de implementación de Windows). Esta nueva opción habilita un respondedor PXE en el punto de distribución que no requiere Servicios de implementación de Windows (WDS). Dado que WDS no es necesario, el punto de distribución habilitado con PXE puede ser un sistema operativo de cliente o servidor, incluido Windows Server Core. Este nuevo servicio de respondedor PXE es compatible con IPv6 y además mejora la flexibilidad de los puntos de distribución habilitados con PXE en oficinas remotas. 

Para obtener más información, vea [habilitar PXE en el punto de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).


### <a name="network-access-account-not-required-for-some-scenarios"></a>La cuenta de acceso a la red no es necesaria para algunos escenarios
<!--1358278,1358279--> La característica [Sistema de sitios HTTP mejorado](#bkmk_ehttp) también elimina algunas dependencias en la cuenta de acceso a la red. Cuando se habilita en el sitio nuevo la opción **Use Configuration Manager-generated certificates for HTTP site systems** (Usar certificados generados por Configuration Manager para sistemas de sitios HTTP), los escenarios siguientes no requieren una cuenta de acceso de red al descargar contenido desde un punto de distribución:  

- Secuencias de tareas que se ejecutan desde un entorno PXE o medios de arranque
- Secuencias de tareas que se ejecutan desde el Centro de software  

Estas secuencias de tareas pueden ser para la implementación del sistema operativo o ser personalizadas. También se admite en los equipos de grupos de trabajo.


### <a name="other-improvements-to-os-deployment"></a>Otras mejoras en la implementación del sistema operativo

#### <a name="mask-sensitive-data-stored-in-task-sequence-variables"></a>Enmascaramiento de la información confidencial almacenada en variables de secuencia de tareas
<!--1358330--> En el paso [Configurar variable de secuencia de tareas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable), seleccione la nueva opción **Do not display this value** (No mostrar este valor). Por ejemplo, al especificar una contraseña. 

#### <a name="mask-program-name-during-run-command-step-of-a-task-sequence"></a>Enmascaramiento del nombre del programa durante el paso Ejecutar comando de una secuencia de tareas
<!--1358493--> Para evitar la visualización o el registro de información posiblemente confidencial, establezca la variable de secuencia de tareas **OSDDoNotLogCommand** en `TRUE`. Esta variable enmascara el nombre del programa en el archivo smsts.log durante un paso de secuencia de tareas [Ejecutar línea de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine).   

#### <a name="task-sequence-variable-for-dism-parameters-when-installing-drivers"></a>Variable de secuencia de tareas para parámetros de DISM al instalar controladores
<!--516679--> Para especificar otros parámetros de línea de comandos para DISM, use la nueva variable de secuencia de tareas **OSDInstallDriversAdditionalOptions**. Habilite el paso [Aplicar paquete de controladores](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage) al establecer en **Install driver package via running DISM with recurse option** (Instalar paquete de controladores mediante la ejecución de DISM con la opción de recursividad). 

#### <a name="option-to-use-full-disk-encryption"></a>Opción para usar cifrado de disco completo
<!--SCCMDocs-pr issue 2671--> Los pasos [Habilitar BitLocker](/sccm/osd/understand/task-sequence-steps#BKMK_EnableBitLocker) y [Tener en servicio BitLocker](/sccm/osd/understand/task-sequence-steps#BKMK_PreProvisionBitLocker) ahora incluyen una opción para **usar cifrado de disco completo**. De forma predeterminada, estos pasos cifran el espacio usado en la unidad. Este comportamiento predeterminado es el recomendado, ya que es más rápido y eficaz. Si la organización necesita cifrar toda la unidad durante la instalación, habilite esta opción. El programa de instalación de Windows espera a que se cifre toda la unidad, lo que tarda mucho tiempo, especialmente en unidades de gran tamaño. 



## <a name="software-center"></a>Centro de software

### <a name="software-center-infrastructure-improvements"></a>Mejoras de la infraestructura del Centro de software
<!--1358309--> Los roles del catálogo de aplicaciones ya no son necesarios para mostrar las aplicaciones disponibles para el usuario en el Centro de software. Este cambio ayuda a reducir la infraestructura de servidor necesaria para entregar las aplicaciones a los usuarios. El Centro de software se basa ahora en el punto de administración para obtener esta información, lo que facilita el escalado de los entornos de mayor tamaño al asignarlos a [grupos de límites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).

> [!Note]  
> Los roles Punto de sitios web y Punto de servicio web del catálogo de aplicaciones ya no son *necesarios* en la versión 1806, aunque todavía son *compatibles*. 
> 
> La **experiencia de usuario de Silverlight** del punto de sitios web del catálogo de aplicaciones ya no se admite. Para más información, consulte [Características en desuso y eliminadas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  


### <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Especificación de la visibilidad del vínculo al sitio web del catálogo de aplicaciones en el Centro de software
<!--1358214--> Use la configuración de cliente para controlar si el vínculo para **abrir el sitio web del catálogo de aplicaciones** aparece en el nodo **Estado de la instalación** del Centro de software.  

Para obtener más información, vea [Acerca de la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#software-center).

> [!Note]  
> La **experiencia de usuario de Silverlight** del punto de sitios web del catálogo de aplicaciones ya no se admite. Para más información, consulte [Características en desuso y eliminadas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  


### <a name="custom-tab-for-webpage-in-software-center"></a>Pestaña personalizada de la página web en el Centro de software
<!--1358132--> Use la configuración de cliente para crear una pestaña personalizada para abrir una página web en el Centro de software. Esta característica permite mostrar contenido a los usuarios finales de una manera coherente y confiable. En esta lista se incluyen algunos ejemplos:  

- Contactar con TI: información sobre cómo ponerse en contacto con el departamento de TI de la organización  

- Centro de soporte técnico de TI: acciones de autoservicio de TI, como buscar una base de conocimientos o abrir una incidencia de soporte técnico.  

- Documentación de usuario final: artículos para los usuarios de la organización sobre diversos temas de TI como, por ejemplo, el uso de aplicaciones o la actualización a Windows 10.  

Para obtener más información, vea [Acerca de la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#software-center) y [Manual del usuario del Centro de software](/sccm/core/understand/software-center).


### <a name="maintenance-windows-in-software-center"></a>Ventanas de mantenimiento en el Centro de software
<!--1358131--> El Centro de software ahora muestra la siguiente ventana de mantenimiento programado. En la pestaña Estado de la instalación, cambie la vista de Todas a Próximas. Muestra el intervalo de tiempo y la lista de implementaciones que están programadas. Si no hay ninguna ventana de mantenimiento futuro, la lista está vacía. 

Para obtener más información, vea [Cómo usar ventanas de mantenimiento](/sccm/core/clients/manage/collections/use-maintenance-windows) y [Manual del usuario del Centro de software](/sccm/core/understand/software-center).



## <a name="software-updates"></a>Actualizaciones de software

### <a name="third-party-software-updates"></a>Actualizaciones de software de terceros
<!--1357605, 1352101, 1358714--> Las actualizaciones de software de terceros permiten suscribirse a catálogos de asociados en la consola de Configuration Manager y publicar las actualizaciones en WSUS. Luego se pueden implementar esas actualizaciones mediante el proceso de administración de actualizaciones de software existente. 

Para obtener más información, vea [Habilitar actualizaciones de terceros](/sccm/sum/deploy-use/third-party-software-updates).


### <a name="deploy-software-updates-without-content"></a>Implementar actualizaciones de software sin contenido
<!--1357933--> Implemente actualizaciones de software en dispositivos sin antes descargar ni distribuir el contenido a los puntos de distribución. Esta característica es útil cuando se trabaja con contenido de actualización extremadamente grande, o cuando se quiere que los clientes obtengan siempre el contenido desde el servicio de nube de Microsoft Update. En este escenario, los clientes también pueden descargar el contenido desde los equipos del mismo nivel que ya tienen el contenido necesario. El cliente de Configuration Manager sigue administrando la descarga del contenido, por lo que puede usar la característica de caché del mismo nivel de Configuration Manager u otras tecnologías como, por ejemplo, Optimización de distribución. Esta característica es compatible con cualquier tipo de actualización admitida por la administración de actualizaciones de software de Configuration Manager, incluidas las actualizaciones de Windows y Office. 

Para obtener más información, vea la opción **Ningún paquete de implementación** al [Implementar actualizaciones de software manualmente](/sccm/sum/deploy-use/manually-deploy-software-updates) o [Implementar actualizaciones de software automáticamente](/sccm/sum/deploy-use/automatically-deploy-software-updates).


### <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrado de las reglas de implementación automáticas por arquitectura de actualización de software
 <!--1322266--> Ahora puede filtrar las reglas de implementación automática (ADR) para excluir arquitecturas como Itanium y ARM64. En la página **Actualizaciones de software** del Asistente para crear regla de implementación automática, el filtro de propiedad **Arquitectura** ya está disponible. 

Para más información, vea [Implementar actualizaciones de software automáticamente](/sccm/sum/deploy-use/automatically-deploy-software-updates).


### <a name="improved-wsus-maintenance"></a>Mantenimiento de WSUS mejorado 
<!--1357898--> El asistente de limpieza WSUS rechaza ahora las actualizaciones que hayan expirado, de acuerdo con las reglas de sustitución definidas en las propiedades de componente de punto de actualización de software. 

Para obtener más información, vea [Mantenimiento de las actualizaciones de software](/sccm/sum/deploy-use/software-updates-maintenance).



## <a name="reporting"></a>Generación de informes

### <a name="new-software-updates-compliance-report"></a>Nuevo informe de cumplimiento de actualizaciones de software
<!--1357775--> La visualización de informes de cumplimiento de actualizaciones de software suele incluir datos de clientes que no han contactado recientemente con el sitio. Un nuevo informe, **Cumplimiento 9 - Mantenimiento general y cumplimiento**, permite filtrar los resultados de cumplimiento de un grupo específico de actualizaciones de software por clientes "correctos". Este informe muestra el estado de cumplimiento más realista de los clientes activos del entorno. 

Para obtener más información, vea [Informes de actualizaciones de software](/sccm/sum/deploy-use/monitor-software-updates#BKMK_SUReports).



## <a name="inventory"></a>Inventario

### <a name="bkmk_bigint"></a> Mejora en el inventario de hardware para valores enteros grandes
<!--1357880--> El inventario de hardware anteriormente tenía un límite para los enteros mayores que 4 294 967 296 (2^32). Este límite se podía alcanzar en atributos como tamaños de unidades de disco duro en bytes. El punto de administración no procesaba los valores enteros por encima de este límite, por lo que no se almacenaba ningún valor en la base de datos. Ahora, en esta versión, se ha aumentado el límite hasta 18 446 744 073 709 551 616 (2^64). 

Para obtener más información, vea [Cómo usar el Explorador de recursos para ver el inventario de hardware](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory#bkmk_bigint).


### <a name="hardware-inventory-default-unit-revision"></a>Revisión de unidad predeterminada de inventario de hardware
<!--514442--> En [Configuration Manager versión 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#site-infrastructure), la unidad predeterminada usada en la mayoría de las vistas de informes se cambió de megabytes (MB) a gigabytes (GB). Debido a las [mejoras en el inventario de hardware para los valores enteros grandes](#bkmk_bigint), y en base a los comentarios de los clientes, esta unidad predeterminada vuelve a ser MB.



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## <a name="configuration-manager-console"></a>Consola de Configuration Manager

### <a name="product-lifecycle-dashboard"></a>Panel de ciclo de vida del producto
<!--1319632--> El panel de ciclo de vida del producto muestra el estado de la directiva de ciclo de vida de los productos de Microsoft instalados en los dispositivos administrados con Configuration Manager. Además proporciona información sobre los productos de Microsoft del entorno, el estado de compatibilidad y la fechas de finalización del soporte técnico. Use el panel para conocer la disponibilidad del soporte técnico para cada producto. Esta información le ayuda a planear cuándo actualizar los productos de Microsoft que usa antes de que llegue el fin del soporte actual.   

Para obtener más información, vea [Uso del panel de ciclo de vida del producto](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard).


### <a name="copy-asset-details-from-monitoring-views"></a>Copiado de detalles de recursos desde vistas de supervisión
<!--1357856--> Las siguientes secciones del área de trabajo **Supervisión** ahora permiten copiar texto:  

- En el nodo **Implementaciones**, seleccione una implementación y haga clic en **Ver estado**. En el panel **Detalles del activo** de la vista Estado de implementación, seleccione uno o varios dispositivos.  

- Expanda el nodo **Estado de distribución** y seleccione **Estado de contenido**. Seleccione un componente de software y haga clic en **Ver estado**. En el panel **Detalles del activo** de la vista Estado de contenido, seleccione uno o varios puntos de distribución. 

Haga clic con el botón derecho en el recurso y seleccione **Copiar**. Esta acción copia los recursos seleccionados como una lista delimitada por comas que incluye todos los detalles. El método abreviado de teclado **CTRL** + **C** también funciona en estas vistas. 

Para obtener más información, vea [Console improvements in version 1806](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806) (Mejoras en la consola en la versión 1806).


### <a name="improvements-to-the-surface-dashboard"></a>Mejoras en el panel de Surface
<!--1358654--> Esta versión incluye las siguientes mejoras en el panel de Surface:  

- Ahora, en el panel de Surface se muestra una lista de los dispositivos correspondientes al seleccionar secciones concretas de un gráfico:  

   - Al hacer clic en el mosaico **Porcentaje de dispositivos Surface**, se abre una lista de dispositivos de Surface.  

   - Al hacer clic en una barra del mosaico **Cinco versiones principales de firmware**, se abre una lista de los dispositivos de Surface que cuentan con esa versión concreta de firmware.  

- Al visualizar estas listas de dispositivos en el panel de Surface, se puede hacer clic con el botón derecho en un dispositivo para llevar a cabo acciones comunes.  

Para obtener más información, vea [Panel de dispositivos Surface](/sccm/core/clients/manage/surface-device-dashboard).


### <a name="view-the-currently-signed-on-user-for-a-device"></a>Visualización del usuario con sesión iniciada en un dispositivo
<!--1358202--> Ahora, de forma predeterminada, el nodo **Dispositivos** del área de trabajo **Activos y compatibilidad** muestra una columna para el **usuario con sesión iniciada**. También se muestra para cualquier lista de dispositivos específicos de una colección. Este valor es tan actual como el [estado de cliente](/sccm/core/clients/manage/monitor-clients#bkmk_indStatus). Cuando el usuario cierra la sesión, el cliente borra este valor. Si ningún usuario ha iniciado sesión, el valor está en blanco. 

Para obtener más información, vea [Console improvements in version 1806](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806) (Mejoras en la consola en la versión 1806).


### <a name="submit-feedback-from-the-configuration-manager-console"></a>Envío de comentarios desde la consola de Configuration Manager  
<!--1357542-->

Enviar una sonrisa Ahora puede contar directamente al equipo de Configuration Manager sus experiencias. Enviar comentarios es fácil desde la consola de Configuration Manager. Nos gustaría recibir todos sus comentarios: sugerencias, problemas y elogios. En la consola de Configuration Manager, haga clic en el botón de sonrisa en la esquina superior derecha encima de la cinta de opciones. Esta información va directamente al equipo de producto de Microsoft de Configuration Manager. Si bien aún se admite el uso del centro de opiniones de Windows 10, le recomendamos que use el mecanismo de comentarios incluido en la consola.  

Para obtener más información, vea [Console improvements in version 1806](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806) (Mejoras en la consola en la versión 1806) y [Buscar ayuda para Configuration Manager](/sccm/core/understand/find-help#BKMK_1806Feedback).



## <a name="next-steps"></a>Pasos siguientes

Cuando esté listo para instalar esta versión, vea [Actualizaciones para System Center Configuration Manager](/sccm/core/servers/manage/updates).

> [!TIP]  
> Para instalar un sitio nuevo, use una versión de línea de base de Configuration Manager.  
>
>  Más información acerca de:    
>   - [Instalación de nuevos sitios](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Versiones de línea de base y versiones de actualización](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Para saber los problemas conocidos e importantes, vea las [Notas de la versión](/sccm/core/servers/deploy/install/release-notes).