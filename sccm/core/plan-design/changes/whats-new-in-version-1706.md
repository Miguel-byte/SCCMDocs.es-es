---
title: Nueva versión 1706
titleSuffix: Configuration Manager
description: Conozca en detalle los cambios y las nuevas funciones introducidas en la versión 1706 de System Center Configuration Manager.
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 050122d6a1b799a30bd2c5a83ab261e92aaafabe
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67677215"
---
# <a name="what39s-new-in-version-1706-of-system-center-configuration-manager"></a>Novedades de la versión 1706 de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La actualización 1706 para la rama actual de System Center Configuration Manager está disponible como actualización en consola para sitios instalados previamente que ejecutan la versión 1606, 1610 o 1702.

> [!TIP]  
> Para instalar un sitio nuevo, debe usar una versión de línea base de Configuration Manager.  
>  Más información acerca de:    
>   - [Instalación de nuevos sitios](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Instalación de actualizaciones en los sitios](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Versiones de línea de base y versiones de actualización](/sccm/core/servers/manage/updates#bkmk_Baselines)  

En las secciones siguientes se proporcionan detalles sobre los cambios y las nuevas funciones introducidas en la versión 1706 de Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestructura del sitio

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Compatibilidad con la caché del mismo nivel de cliente para archivos de instalación rápida en Windows 10 y Office 365  
<!-- 1352486 -->
A partir de esta versión, la caché del mismo nivel de cliente admite la distribución de archivos de instalación rápida de contenido para Windows 10, así como de archivos de actualización para Office 365. No se requiere ninguna configuración adicional para admitir este cambio.

### <a name="updates-for-the-data-warehouse"></a>Actualizaciones para el almacenamiento de datos
<!-- 1277922 -->
El almacenamiento de datos ya no es una característica de versión preliminar. También hemos actualizado los requisitos previos para incluir compatibilidad con la base de datos en grupos de disponibilidad AlwaysOn de SQL Server y los clústeres de conmutación por error. Para más información, consulte [Punto de servicio del almacenamiento de datos](/sccm/core/servers/manage/data-warehouse).

### <a name="accessibility-improvements"></a>Mejoras de accesibilidad
<!-- 1253000 -->
Hemos agregado mejoras adicionales de accesibilidad para la consola de Configuration Manager. Para obtener más información, consulte [Características de accesibilidad ](/sccm/core/understand/accessibility-features).

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>Mejoras de los grupos de disponibilidad AlwaysOn de SQL Server
<!-- 1352094 -->
Con esta versión, ahora puede usar réplicas de confirmación asincrónica en los grupos de disponibilidad AlwaysOn de SQL Server que usa con Configuration Manager. Esto significa que puede agregar réplicas adicionales a los grupos de disponibilidad con el fin de usarlas como copias de seguridad externas (remotas) y así utilizarlas en un escenario de recuperación ante desastres.  
  - Configuration Manager admite el uso de la réplica de confirmación asincrónica para recuperar una réplica sincrónica. Vea [las opciones de recuperación de la base de datos de sitio](/sccm/core/servers/manage/recover-sites#site-database-recovery-options) en el tema Copia de seguridad y recuperación para obtener información sobre cómo realizar esta tarea.
  - Esta versión no admite la conmutación por error para usar la réplica de confirmación asincrónica como la base de datos de sitio.
Para obtener más información, consulte [Preparación para usar grupos de disponibilidad AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### <a name="update-reset-tool"></a>Herramienta de restablecimiento de actualizaciones
<!-- 1324589 -->
A partir de la versión 1706, los sitios primarios de Configuration Manager y los sitios de administración central incluyen la Herramienta de restablecimiento de actualizaciones de Configuration Manager, **CMUpdateReset.exe**. Use esta herramienta con cualquier versión de la rama actual que siga teniendo soporte técnico, para solucionar problemas cuando estos surjan al descargar o replicar las actualizaciones en la consola. Para obtener más información, consulte [Update reset tool](/sccm/core/servers/manage/update-reset-tool) (Herramienta de restablecimiento de actualizaciones).

### <a name="high-dpi-console-support"></a>Compatibilidad de la consola con una configuración elevada de ppp  
<!-- 1353476 -->
Con esta versión, los problemas relacionados con el modo en que la consola de Configuration Manager escala y muestra distintas partes de la interfaz de usuario cuando se ven en los dispositivos con una configuración elevada de ppp (como un libro de Surface) deben haberse corregido.

### <a name="improved-boundary-groups-for-software-update-points"></a>Mejoras de los grupos de límites para puntos de actualización de software
<!-- 1324591 -->
Esta versión incluye mejoras para el modo en que los puntos de actualización de software funcionan con grupos de límites. A continuación se resume el nuevo comportamiento de la reserva:
-   La reserva para puntos de actualización de software usa ahora un tiempo configurable para aplicarse en los grupos de límites vecinos.
-   Independientemente de la configuración de la reserva, un cliente intenta alcanzar el último punto de actualización de software que utilizó durante 120 minutos. Tras no conseguir alcanzar ese servidor durante 120 minutos, el cliente consulta su grupo de puntos de actualización de software disponibles para encontrar otro nuevo.
-   Transcurridas dos horas sin conseguir alcanzar su servidor original, el cliente cambia a un ciclo más corto para establecer contacto con un nuevo punto de actualización de software. Esto significa que si un cliente no puede conectar con un nuevo servidor, selecciona rápidamente el siguiente servidor de su grupo de servidores disponibles e intenta ponerse en contacto con él.

Para obtener más información, vea [Puntos de actualización de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) en el tema de Configuración de grupos de límites para la Rama actual.

### <a name="azure-ad-integration-with-configuration-manager"></a>Integración de Azure AD con Configuration Manager
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
Con esta versión, hemos mejorado la integración de Configuration Manager y Azure Active Directory (Azure AD).  Estas mejoras simplifican cómo debe configurar los servicios de Azure que usa con Configuration Manager y lo ayudan a administrar clientes y los usuarios que se autentican a través de Azure AD.

La integración mejorada permite lo siguiente:  
  -   Asistente para servicios de Azure: Este asistente proporciona una experiencia de configuración común que reemplaza los flujos de trabajo individuales para configurar los siguientes servicios de Azure que usa con Configuration Manager.
      - **Administración en la nube** Permita a los clientes autenticarse mediante Azure Active Directory (Azure AD). También puede configurar la detección de usuarios de Azure AD.
      - **Conector de Log Analytics** Conecte con Azure Log Analytics y sincronice los datos de la recopilación.
      - **Upgrade Readiness** Conéctese a Upgrade Readiness y vea los datos de compatibilidad de actualización de cliente.
      - **Tienda Windows para empresas** Conéctese a la tienda en línea para la Tienda Windows para empresas y obtenga aplicaciones para su organización que puede implementar con Configuration Manager.


  Esto se realiza mediante una [aplicación web de servidor de Azure](/azure/app-service/app-service-authentication-overview) para proporcionar la información de suscripción y configuración que, de lo contrario, especificaría cada vez que configurase un nuevo componente o servicio de Configuration Manager con Azure. Para obtener más información, consulte [Azure Services Wizard](/sccm/core/servers/deploy/configure/azure-services-wizard) (Asistente para servicios de Azure).

-   Use Azure AD para autenticar los clientes en Internet para acceder a los sitios de Configuration Manager. Azure AD reemplaza la necesidad de configurar y usar certificados de autenticación del cliente. Esto requiere el rol de sistema de sitio de Cloud Management Gateway. Para más información, vea [Instalación y asignación de clientes de Configuration Manager desde Internet mediante Azure AD con fines de autenticación](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

-   Instale y administre al cliente de Configuration Manager en equipos que se encuentran en Internet. Esto requiere el uso del rol de sistema de Cloud Management Gateway. Para más información, vea [Instalación y asignación de clientes de Configuration Manager desde Internet mediante Azure AD con fines de autenticación](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

-   Configure la detección de usuarios de Azure AD.  Use el Asistente para servicios de Azure para configurar este nuevo método de detección. Este nuevo método consulta a Azure AD los datos de usuario que luego puede usar junto con datos de detección tradicional.  Se admiten tanto la sincronización completa como la sincronización delta.  Para obtener más información, consulte [Detección de usuario de Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

### <a name="peer-cache-improvements"></a>Mejoras de almacenamiento en caché del mismo nivel
<!-- 1252345 -->
La memoria caché del mismo nivel ya no utiliza la cuenta de acceso a la red para autenticar las solicitudes de descarga de elementos del mismo nivel. Hay una limitación cuando los clientes siguen necesitando esta cuenta. Esto sigue siendo un requisito para los clientes que arrancan en WinPE y luego acceden a contenido desde un origen de caché del mismo nivel. Para obtener más información, consulte [Requisitos y consideraciones de la caché del mismo nivel](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements).


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>Configuración de cumplimiento

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>Nuevas opciones de configuración para dispositivos Windows 10 que no están administrados con el cliente de Configuration Manager
<!-- 1354715 -->
En esta versión, hemos agregado nuevas opciones de configuración para dispositivos Windows 10 que están inscritos con Intune o administrados de forma local mediante Configuration Manager. Los parámetros son:

- **Contraseña**
  - Cifrado del dispositivo
- **Dispositivo**
  - Modificación de la configuración regional (solo dispositivos de escritorio)
  - Modificación de la configuración de inicio/apagado y suspensión
  - Modificación de la configuración de idioma
  - Modificación de la hora del sistema
  - Modificación del nombre del dispositivo
- **Tienda**
  - Actualizar automáticamente las aplicaciones de la tienda
  - Usar solo una tienda privada
  - Inicio de aplicaciones de la Tienda
- **Microsoft Edge**
  - Bloquear acceso a about:flags
  - Invalidación de avisos de SmartScreen
  - Invalidación de avisos de SmartScreen para archivos
  - Dirección IP de Localhost para WebRTC
  - Motor de búsqueda predeterminado
  - URL de archivo XML OpenSearch
  - Páginas principales (solo dispositivos de escritorio)

Para detalles de todas las configuraciones de Windows 10, consulte [Cómo crear elementos de configuración para dispositivos de Windows 8.1 y Windows 10 administrados sin el cliente de System Center Configuration Manager](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).

### <a name="new-device-compliance-policy-rules"></a>Nuevas reglas de directiva de cumplimiento de dispositivos

* **Tipo de contraseña requerida**. Especifica si el usuario debe crear una contraseña numérica o alfanumérica. En el caso de las contraseñas alfanuméricas, puede especificar también el número mínimo de juegos de caracteres que debe tener la contraseña. Los conjuntos de cuatro caracteres son los siguientes: letras minúsculas, letras mayúsculas, símbolos y números.

  **Compatible con:**
  * Windows Phone 8+
  * Windows 8.1+
  * iOS 6+
  <br></br>
* **Bloquear depuración USB en el dispositivo**. No es necesario configurar este parámetro porque la depuración USB ya está deshabilitada en los dispositivos Android for Work.

  **Compatible con:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Bloquear aplicaciones de orígenes desconocidos**. Los dispositivos deben impedir la instalación de aplicaciones de orígenes desconocidos. No es necesario configurar este valor, ya que los dispositivos Android for Work siempre restringen la instalación de orígenes desconocidos.

  **Compatible con:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Requerir examen de amenazas en las aplicaciones**. Este valor especifica que la característica Verificar aplicaciones está habilitada en el dispositivo.

  **Compatible con:**
  * Android 4.2 hasta 4.4
  * Samsung KNOX Standard 4.0+

Vea [Crear e implementar una directiva de cumplimiento de dispositivos](https://docs.microsoft.com/sccm/mdm/deploy-use/create-compliance-policy) para probar las nuevas reglas de cumplimiento del dispositivo.

## <a name="application-management"></a>Administración de aplicaciones

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>Ejecución de scripts de PowerShell desde la consola de Configuration Manager
<!-- 1236459 -->

En Configuration Manager, puede implementar scripts en dispositivos de cliente mediante paquetes y programas. En esta versión, hemos agregado nueva funcionalidad que permite realizar las siguientes acciones:

- Importar scripts de PowerShell en Configuration Manager.
- Editar los scripts desde la consola de Configuration Manager (solo para scripts sin firmar).
- Marcar scripts como aprobados o denegados, para mejorar la seguridad.
- Ejecutar scripts en recopilaciones de equipos cliente de Windows y equipos de Windows administrados locales. No se implementan los scripts, sino que se ejecutan casi en tiempo real en los dispositivos cliente.
- Examine los resultados devueltos por el script en la consola de Configuration Manager.

Para obtener más información, consulte [Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).

### <a name="new-mobile-application-management-policy-settings"></a>Configuración de nueva directiva de administración de aplicaciones móviles    
<!--1324760-->
A partir de esta versión, puede usar tres nuevas opciones de configuración para la directiva de Administración de aplicaciones móviles:

- **Bloquear captura de pantalla (solo en dispositivos Android):** Especifica que las funciones de captura de pantalla del dispositivo se bloquean cuando se usa esta aplicación.

Vea [Proteger aplicaciones mediante directivas de administración de aplicaciones móviles en System Center Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para probar la nueva configuración de la directiva de protección de aplicaciones.


## <a name="operating-system-deployment"></a>Implementación de sistema operativo

### <a name="hardware-inventory-collects-secure-boot-information"></a>El inventario de hardware recopila información de arranque seguro
Ahora, el inventario de hardware recopila información sobre si el arranque seguro está habilitado en los clientes. Esta información se almacena en la clase **SMS_Firmware** (introducida en la versión 1702) y se habilita en el inventario de hardware de forma predeterminada. Para obtener más información sobre el inventario de hardware, vea [Cómo configurar el inventario de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

### <a name="collapsible-task-sequence-groups"></a>Grupos de secuencias de tareas contraíbles
Esta versión introduce la capacidad de expandir y contraer los grupos de la secuencia de tareas. Puede expandir o contraer grupos individuales o expandir o contraer todos los grupos a la vez.

### <a name="reload-boot-images-with-current-windows-pe-version"></a>Nueva carga de imágenes de arranque con la versión actual de Windows PE
Al ejecutar **Actualizar puntos de distribución** en una imagen de arranque seleccionada, ahora puede volver a cargar la versión más reciente de Windows PE (desde el directorio de instalación de Windows ADK) en la imagen de arranque. Para obtener más información, vea [Actualización de puntos de distribución con la imagen](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image).

## <a name="software-updates"></a>Actualizaciones de software

### <a name="improvements-to-express-update-download-time"></a>Mejoras en el tiempo de descarga de actualizaciones rápidas
En esta versión, hemos mejorado considerablemente el tiempo de descarga para las actualizaciones rápidas. Para obtener más información, consulte [Administración de archivos de instalación rápida para actualizaciones de Windows 10](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

### <a name="manage-microsoft-surface-driver-updates"></a>Administración de las actualizaciones de controladores de Microsoft Surface
<!-- 1098490 -->
Ahora puede usar Configuration Manager para administrar las actualizaciones de controladores de Microsoft Surface.    


#### <a name="prerequisites"></a>Requisitos previos
- Todos los puntos de actualización de software deben ejecutar Windows Server 2016.    
- Esta es una característica de versión preliminar que debe activar para que esté disponible. Para más información, consulte [Use pre-release features from updates](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease) (Uso de características de la versión preliminar a partir de las actualizaciones).

#### <a name="to-manage-surface-driver-updates"></a>Para administrar actualizaciones de controladores de Surface

1. Habilite la sincronización para controladores de Microsoft Surface. Siga el procedimiento descrito en [Configurar las clasificaciones y los productos que va a sincronizar](/sccm/sum/get-started/configure-classifications-and-products) y seleccione la casilla **Incluir actualizaciones de controladores y firmware de Microsoft Surface** en la pestaña **Clasificaciones** para habilitar los controladores de Surface.
2. [Sincronice los controladores de Microsoft Surface](/sccm/sum/get-started/synchronize-software-updates).
3. [Implemente los controladores de Microsoft Surface sincronizados](/sccm/sum/deploy-use/deploy-software-updates).

### <a name="configure-windows-update-for-business-deferral-policies"></a>Configuración de directivas de aplazamiento de Windows Update para empresas
<!-- 1290890 -->
Ahora puede configurar directivas de aplazamiento para actualizaciones de características de Windows 10 o actualizaciones de calidad para dispositivos con Windows 10 administradas directamente por Windows Update para empresas. Puede administrar las directivas de aplazamiento en el nuevo nodo **Directivas de Windows Update para empresas**, en **Biblioteca de Software** > **Mantenimiento de Windows 10**.

Para detalles, consulte [Integración con Windows Update for Business en Windows 10](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).

### <a name="improved-user-notifications-for-office-365-updates"></a>Mejora en las notificaciones de usuario para las actualizaciones de Office 365
Se han hecho mejoras para aprovechar la experiencia de usuario Hacer clic y ejecutar de Office cuando un cliente instala una actualización de Office 365. Esto incluye notificaciones emergentes y en la aplicación y una experiencia de cuenta atrás. Para obtener más información, consulte [Comportamiento al reiniciar y notificaciones de cliente para las actualizaciones de Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#restart-behavior-and-client-notifications-for-office-365-updates).

## <a name="reporting"></a>Generación de informes

### <a name="use-windows-analytics-with-configuration-manager"></a>Uso de Windows Analytics con Configuration Manager
<!-- 1318608 -->
Windows Analytics es un conjunto de soluciones que permiten hacerse una idea sobre el estado actual de su entorno. Los dispositivos del entorno notifican los datos de telemetría de Windows. Es posible acceder a los datos a través de Azure Portal. En el caso de Upgrade Readiness los datos están directamente disponibles en el nodo de supervisión de la consola de Configuration Manager.

Para obtener más información, consulte [Use Windows Analytics with Configuration Manager](/sccm/core/clients/manage/monitor-windows-analytics).


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Administración de dispositivos móviles

### <a name="updates-to-android-for-work-sharing-configuration"></a>Actualizaciones a Android para la configuración de uso compartido del trabajo
<!-- 1338403 -->
Con esta versión, se han actualizado los valores para la opción de configuración **Permitir uso compartido de datos entre el perfil de trabajo y el perfil personal** del grupo de configuración **Perfil de trabajo**. También hemos agregado una configuración personalizada para bloquear la acción de copiar y pegar entre perfiles de trabajo y personales.

Para obtener más información, consulte [Creación de elementos de configuración para dispositivos Android for Work administrados con Intune](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client).

### <a name="android-and-ios-enrollment-restrictions"></a>Restricciones de inscripción de iOS y Android
<!-- 1290826 -->
Con esta versión, puede especificar que los usuarios no inscriban los dispositivos personales de Android o iOS. Las nuevas opciones de restricción de dispositivos permiten limitar la inscripción de dispositivos Android en dispositivos predeclarados. Para dispositivos iOS, puede bloquear la inscripción de todos los dispositivos excepto los que están inscritos con el Programa de inscripción de dispositivos de Apple, Apple Configurator o la cuenta de administrador de inscripción de dispositivos de Intune.
- Para más información sobre las restricciones de inscripción de Android, vea [Configuración de la administración de dispositivos de Android](/sccm/mdm/deploy-use/enroll-hybrid-android).
- Para más información sobre las restricciones de inscripción de iOS, vea [Configuración de restricciones de inscripción de iOS](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac#configure-enrollment-restrictions).

## <a name="protect-devices"></a>Proteger los dispositivos

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Inclusión de la confianza para determinados archivos y carpetas en una directiva de Device Guard
<!--1324676-->
En esta versión, hemos agregado más funcionalidades para la administración de directivas de Device Guard.

Ahora tiene la posibilidad de agregar confianza para determinados archivos y carpetas en una directiva de Device Guard. Esto le permite:

- Solucionar problemas con los comportamientos de instalador administrado
- Confiar en aplicaciones de línea de negocio que no se pueden implementar con Configuration Manager
- Confiar en aplicaciones que se incluyen en una imagen de implementación de sistema operativo

Para obtener más detalles, consulte [Administración de Device Guard con Configuration Manager](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager).
