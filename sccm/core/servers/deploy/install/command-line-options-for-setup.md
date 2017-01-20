---
title: "Opciones de línea de comandos de instalación | System Center Configuration Manager"
description: "Use la información de este artículo para configurar scripts o instalar System Center Configuration Manager desde una línea de comandos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 7d1f55786a42650395fcb66ee4917434feecb630

---
# <a name="command-line-options-for-setup-for-system-center-configuration-manager"></a>Opciones de línea de comandos para la instalación para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


 Use la información de las tablas siguientes al configurar scripts o instalar System Center Configuration Manager desde una línea de comandos.  

##  <a name="a-namebkmksetupa-command-line-options-for-setup"></a><a name="bkmk_setup"></a> Opciones de línea de comandos para la instalación  
 **/DEINSTALL**  
 Desinstala el sitio. Debe ejecutar el programa de instalación desde el equipo servidor del sitio.  

 **/DONTSTARTSITECOMP**  
 Instala un sitio, pero impide que se inicie el servicio Administrador de componentes del sitio. Hasta que se inicie el servicio Administrador de componentes del sitio, el sitio no está activo. El Administrador de componentes del sitio es responsable de instalar e iniciar el servicio SMS_Executive y procesos adicionales en el sitio. Una vez completada la instalación del sitio, cuando se inicia el servicio Administrador de componentes del sitio, a continuación, se instala SMS_Executive y los procesos adicionales necesarios para que el sitio funcione.  

 **/HIDDEN**  
 Oculta la interfaz de usuario durante la instalación. Esta opción debe usarse junto con la opción **/SCRIPT** y el archivo de script desatendido debe proporcionar todas las opciones necesarias. De lo contrario, la instalación producirá un error.  

 **/NOUSERINPUT**  
 Deshabilita la entrada del usuario durante la instalación, pero muestra la interfaz del **Asistente para la instalación** . Esta opción debe usarse junto con la opción **/SCRIPT** y el archivo de script desatendido debe proporcionar todas las opciones necesarias. De lo contrario, la instalación producirá un error.  

 **/RESETSITE**  
 Realiza el restablecimiento de un sitio; restablece las cuentas del servicio y la base de datos para el sitio. Debe ejecutar el programa de instalación desde **&lt;ConfigMgrInstallationPath\>\BIN\X64** en el servidor de sitio. Para más información sobre el restablecimiento del sitio, vea la sección [Run a site reset (Ejecutar un restablecimiento de sitio)](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) del tema [Modify your System Center Configuration Manager infrastructure (Modificar la infraestructura de System Center Configuration Manager)](../../../../core/servers/manage/modify-your-infrastructure.md).  

 **/TESTDBUPGRADE &lt;*NombreInstancia\NombreBasededatos*>**  
 Realiza una prueba en una copia de seguridad de la base de datos del sitio para asegurarse de que es capaz de una actualización. Debe proporcionar el nombre de la instancia y el nombre de la base de datos de la base de datos del sitio. Si especifica solo el nombre de la base de datos, el programa de instalación utiliza el nombre de instancia predeterminado.  

> [!IMPORTANT]  
>  No se puede ejecutar esta opción de línea de comandos en la base de datos del sitio de producción. Esta acción actualiza la base de datos del sitio y podría inutilizar el sitio.  

 **/UPGRADE**  
 Ejecuta una actualización desatendida de un sitio. Cuando utilice /UPGRADE, también debe especificar la clave del producto, incluidos los guiones (-). Además, debe especificar la ruta de acceso a los archivos de requisitos previos de instalación descargados anteriormente.  

 Ejemplo: **setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx &lt;ruta de acceso a archivos de componentes externos\>**  

 Para más información sobre los archivos de requisitos previos de la instalación, vea  [Descargador del programa de instalación](#bkmk_SetupDownloader) en este tema.  

 **/SCRIPT &lt;*SetupScriptPath*>**  
 Realiza instalaciones desatendidas. Cuando se usa la opción **/SCRIPT** se necesita un archivo de inicialización del programa de instalación. Para más información sobre cómo ejecutar una instalación desatendida, vea [Install sites using a command line (Instalar sitios con una línea de comandos)](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).  

 **/SDKINST &lt;*FQDN*>**  
 Instala el proveedor de SMS en el equipo especificado. Debe proporcionar el FQDN del equipo de proveedor de SMS. Para más información sobre el proveedor de SMS, vea [Plan para el proveedor de SMS de System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

 **/SDKDEINST &lt;*FQDN*>**  
 Desinstala el proveedor de SMS en el equipo especificado. Debe proporcionar el FQDN del equipo de proveedor de SMS.  

 **/MANAGELANGS &lt;*LanguageScriptPath*>**  
 Administra los idiomas que se instalan en un sitio instalado previamente. Para usar esta opción, debe ejecutar el programa de instalación desde **&lt;ConfigMgrInstallationPath\>\BIN\X64** en el servidor de sitio y proporcionar la ubicación del archivo de script de idioma que contiene la configuración del idioma. Para más información sobre las opciones de idioma disponibles en el archivo de script de configuración de idioma, vea [Opciones de línea de comandos para administrar idiomas](#bkmk_Lang) en este tema.  

##  <a name="a-namebkmklanga-command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a> Opciones de línea de comandos para administrar idiomas  
 **Identificación**  

-   **Nombre de clave:** Action  

    -   **Requerido** : sí  

    -   **Valores:** ManageLanguages  

    -   **Detalles:** administra el servidor, el cliente y la compatibilidad con el idioma del cliente móvil en un sitio.  

**Opciones**  

-   **Nombre de clave:** AddServerLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** especifica los idiomas de servidor que estarán disponibles para la consola de Configuration Manager, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada.  

-   **Nombre de clave:** AddClientLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** especifica los idiomas que estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada.  

-   **Nombre de clave:** DeleteServerLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** especifica los idiomas que se van a quitar y que ya no estarán disponibles para la consola de Configuration Manager, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada y no se puede quitar.  

-   **Nombre de clave:** DeleteClientLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** especifica los idiomas que se van a quitar y que ya no estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada y no se puede quitar.  

-   **Nombre de clave:** MobileDeviceLanguage  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si están instalados los idiomas de cliente de dispositivo móvil.  

-   **Nombre de clave:**: PrerequisiteComp  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = descargar  

         1 = ya se ha descargado  

    -   **Detalles** : especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si utiliza un valor de 0, el programa de instalación descarga los archivos.  

-   **Nombre de clave:** PrerequisitePath  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalles** : especifica la ruta de acceso a los archivos de requisitos previos de instalación. Dependiendo del valor **PrerequisiteComp** , el programa de instalación utiliza esta ruta para almacenar los archivos descargados o localizar los archivos descargados previamente.  

##  <a name="a-namebkmkunattendeda-unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a> Claves de archivo de script de instalación desatendida  
 Utilice las siguientes secciones para crear el script para una instalación desatendida. Las tablas enumeran las claves del script de instalación disponibles, sus valores correspondientes, si son necesarias o no, el tipo de instalación para el que se usan y una breve descripción de cada clave.  

### <a name="unattended-install-for-a-central-administration-site"></a>Instalación desatendida de un sitio de administración central  
 Utilice los siguientes datos para instalar un sitio de administración central mediante un archivo de script de instalación desatendida.  

**Identificación**  

-   **Nombre de clave:** Action  

    -   **Requerido** : sí  

    -   **Valores:** InstallCAS  

    -   **Detalles:** instala un sitio de administración central.  

**Opciones**  

-   **Nombre de clave:** ProductID  

    -   **Requerido** : sí  

    -   **Valores:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* o *Eval*  

    -   **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones. Escriba **Eval** para instalar la versión de evaluación de Configuration Manager.  

-   **Nombre de clave:** SiteCode  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*SiteCode*>  

    -   **Detalles:** especifica tres caracteres alfanuméricos que identifican al sitio de forma única en la jerarquía.  

-   **Nombre de clave:** SiteName  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*SiteName*>  

    -   **Detalles:** especifica el nombre de este sitio.  

-   **Nombre de clave:** SMSInstallDir  

    -   **Requerido** : sí  

    -   **Valores:** *ConfigMgrInstallationPath*  

    -   **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.  

-   **Nombre de clave:** SDKServer  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*FQDN del proveedor de SMS*>  

    -   **Detalles** : especifica el FQDN del servidor que hospedará el proveedor de SMS.  
        Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial.  

-   **Nombre de clave:**: PrerequisiteComp  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = descargar  

         1 = ya se ha descargado  

    -   **Detalles** : especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si utiliza un valor de 0, el programa de instalación descargará los archivos.  

-   **Nombre de clave:** PrerequisitePath  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalles** : especifica la ruta de acceso a los archivos de requisitos previos de instalación. Dependiendo del valor PrerequisiteComp, el programa de instalación utiliza esta ruta para almacenar los archivos descargados o localizar los archivos descargados previamente.  

-   **Nombre de clave:** AdminConsole  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si se va a instalar la consola de Configuration Manager.  

-   **Nombre de clave:** JoinCEIP  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no unir  

         1 = unir  

    -   **Detalles** : especifica si se unirá al Programa para la mejora de la experiencia del usuario.  

-   **Nombre de clave:** AddServerLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** especifica los idiomas de servidor que estarán disponibles para la consola de Configuration Manager, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada.  

-   **Nombre de clave:** AddClientLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** especifica los idiomas que estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada.  

-   **Nombre de clave:** DeleteServerLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** modifica un sitio después de instalarlo.  
        Especifica los idiomas que se quitarán y ya no estarán disponibles para la consola, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada y no se puede quitar.  

-   **Nombre de clave:** DeleteClientLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** modifica un sitio después de instalarlo.  
        Especifica los idiomas para quitar que ya no estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada y no se puede quitar.  

-   **Nombre de clave:** MobileDeviceLanguage  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si están instalados los idiomas de cliente de dispositivo móvil.  

**SQLConfigOptions**  

-   **Nombre de clave:** SQLServerName  

    -   **Requerido** : sí  

    -   **Valores:** *SQLServerName*  

    -   **Detalles:** especifica el nombre del servidor, o el nombre de la instancia en clúster, que ejecuta SQL Server. Hospedará la base de datos del sitio.  

-   **Nombre de clave:** DatabaseName  

    -   **Requerido** : sí  

    -   **Valores:** *&lt;SiteDatabaseName\>* o *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **Detalles:**  

         Especifica el nombre de la base de datos de SQL Server que se crea o utiliza para instalar la base de datos del sitio de administración central.  

        > [!IMPORTANT]  
        >  Debe especificar el nombre de instancia y el nombre de la base de datos del sitio si no utiliza la instancia predeterminada.  

-   **Nombre de clave:** SQLSSBPort  

    -   **Requerido** : no  

    -   **Valores:** &lt;*SSBPortNumber*>  

    -   **Detalles:** especifica el puerto de SQL Server Service Broker (SSB) que usa SQL Server. Normalmente, SSB está configurado para utilizar el puerto TCP 4022, pero se admiten otros puertos.  

-   **Nombre de clave:** SQLDataFilePath  

    -   **Requerido** : no  

    -   **Valores:** &lt;*FilePath al archivo .MDB de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .MDB de base de datos.  

-   **Nombre de clave:** SQLLogFilePath  

    -   **Requerido** : no  

    -   **Valores:** &lt;*FilePath al archivo .LDF de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .LDF de base de datos.  

**CloudConnectorOptions**  

-   **Nombre de clave:** CloudConnector  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si instalará un punto de conexión de servicio en este sitio. Dado que el punto de conexión de servicio solo puede instalarse en el sitio de nivel superior de una jerarquía, este valor debe ser 0 para un sitio principal secundario.  

-   **Nombre de clave:** CloudConnectorServer  

    -   **Requerido:** necesario cuando CloudConnector es igual a 1  

    -   **Valores:** &lt;*FQDN del servidor de punto de conexión de servicio*>  

    -   **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio del punto de conexión de servicio.  

-   **Nombre de clave:** UseProxy  

    -   **Requerido:** necesario cuando CloudConnector es igual a 1  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si el punto de conexión de servicio usará un servidor proxy.  

-   **Nombre de clave:** ProxyName  

    -   **Requerido:** necesario cuando UseProxy es igual a 1  

    -   **Valores:** &lt;*FQDN del servidor proxy*>  

    -   **Detalles:** especifica el FQDN del servidor proxy que usará el rol de sistema de sitio del punto de conexión de servicio.  

-   **Nombre de clave:** ProxyPort  

    -   **Requerido:** necesario cuando UseProxy es igual a 1  

    -   **Valores:** &lt;*PortNumber*>  

    -   **Detalles:** especifica el número de puerto que se usará.  

### <a name="unattended-install-for-a-primary-site"></a>Instalación desatendida de un sitio principal  
Utilice los siguientes detalles para instalar un sitio principal mediante un archivo de script de instalación desatendida.  

Utilice los siguientes datos para instalar un sitio de administración central mediante un archivo de script de instalación desatendida.  

**Identificación**  

-   **Nombre de clave:** Action  

    -   **Requerido** : sí  

    -   **Valores:** InstallPrimarySite  

    -   **Detalles:** instala un sitio primario.  

**Opciones**  

-   **Nombre de clave:** ProductID  

    -   **Requerido** : sí  

    -   **Valores:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* o *Eval*  

    -   **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones. Escriba **Eval** para instalar la versión de evaluación de Configuration Manager.  

-   **Nombre de clave:** SiteCode  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*SiteCode*>  

    -   **Detalles:** especifica tres caracteres alfanuméricos que identifican al sitio de forma única en la jerarquía.  

-   **Nombre de clave:** SiteName  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*SiteName*>  

    -   **Detalles:** especifica el nombre de este sitio.  

-   **Nombre de clave:** SMSInstallDir  

    -   **Requerido** : sí  

    -   **Valores:** *ConfigMgrInstallationPath*  

    -   **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.  

-   **Nombre de clave:** SDKServer  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*FQDN del proveedor de SMS*>  

    -   **Detalles** : especifica el FQDN del servidor que hospedará el proveedor de SMS.  
        Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial.  

-   **Nombre de clave:**: PrerequisiteComp  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = descargar  

         1 = ya se ha descargado  

    -   **Detalles** : especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si utiliza un valor de 0, el programa de instalación descargará los archivos.  

-   **Nombre de clave:** PrerequisitePath  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalles** : especifica la ruta de acceso a los archivos de requisitos previos de instalación. Dependiendo del valor **PrerequisiteComp** , el programa de instalación utiliza esta ruta para almacenar los archivos descargados o localizar los archivos descargados previamente.  

-   **Nombre de clave:** AdminConsole  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si se va a instalar la consola de Configuration Manager.  

-   **Nombre de clave:** JoinCEIP  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no unir  

         1 = unir  

    -   **Detalles** : especifica si se unirá al Programa para la mejora de la experiencia del usuario.  

-   **Nombre de clave:** ManagementPoint  

    -   **Requerido** : no  

    -   **Valores:** &lt;*FQDN del servidor de sitio de punto de administración*>  

    -   **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio de punto de administración.  

-   **Nombre de clave:** ManagementPointProtocol  

    -   **Requerido** : no  

    -   **Valores:** HTTPS o HTTP  

    -   **Detalles:** especifica el protocolo que se va a usar para el punto de administración.  

-   **Nombre de clave:** DistributionPoint  

    -   **Requerido** : no  

    -   **Valores:** &lt;*FQDN de servidor de sitio de punto de distribución*>  

    -   **Detalles:** especifica el protocolo que se va a usar para el punto de administración.  

-   **Nombre de clave:** DistributionPointProtocol  

    -   **Requerido** : no  

    -   **Valores:** HTTPS o HTTP  

    -   **Detalles:** especifica el protocolo que se va a usar para el punto de distribución.  

-   **Nombre de clave:** RoleCommunicationProtocol  

    -   **Requerido** : sí  

    -   **Valores:** EnforceHTTPS o HTTPorHTTPS  

    -   **Detalles:** especifica si se van a configurar todos los sistemas de sitio para aceptar solo las comunicaciones HTTPS de los clientes o para el método de comunicación que se configurará para cada rol de sistema de sitio. Al seleccionar **EnforceHTTPS**, el equipo cliente debe tener un certificado PKI válido para la autenticación de cliente.  

-   **Nombre de clave:** ClientsUsePKICertificate  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no usar  

         1 = usar  

    -   **Detalles:** especifica si los clientes van a usar un certificado PKI de cliente para comunicarse con los roles de sistema de sitio.  

-   **Nombre de clave:** AddServerLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** especifica los idiomas de servidor que estarán disponibles para la consola de Configuration Manager, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada.  

-   **Nombre de clave:** AddClientLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** especifica los idiomas que estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada.  

-   **Nombre de clave:** DeleteServerLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** modifica un sitio después de instalarlo.  
        Especifica los idiomas que se quitarán y ya no estarán disponibles para la consola, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada y no se puede quitar.  

-   **Nombre de clave:** DeleteClientLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** modifica un sitio después de instalarlo.  
        Especifica los idiomas para quitar que ya no estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada y no se puede quitar.  

-   **Nombre de clave:** MobileDeviceLanguage  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si están instalados los idiomas de cliente de dispositivo móvil.  

**SQLConfigOptions**  

-   **Nombre de clave:** SQLServerName  

    -   **Requerido** : sí  

    -   **Valores:** *SQLServerName*  

    -   **Detalles:** especifica el nombre del servidor, o el nombre de la instancia en clúster, que ejecuta SQL Server. Hospedará la base de datos del sitio.  

-   **Nombre de clave:** DatabaseName  

    -   **Requerido** : sí  

    -   **Valores:** *&lt;SiteDatabaseName\>* o *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **Detalles:**  

         Especifica el nombre de la base de datos de SQL Server que se crea o utiliza para instalar la base de datos del sitio primario.  

        > [!IMPORTANT]  
        >  Debe especificar el nombre de instancia y el nombre de la base de datos del sitio si no utiliza la instancia predeterminada.  

-   **Nombre de clave:** SQLSSBPort  

    -   **Requerido** : no  

    -   **Valores:** &lt;*SSBPortNumber*>  

    -   **Detalles:** especifica el puerto de SQL Server Service Broker (SSB) que usa SQL Server. Normalmente, SSB está configurado para utilizar el puerto TCP 4022, pero se admiten otros puertos.  

-   **Nombre de clave:** SQLDataFilePath  

    -   **Requerido** : no  

    -   **Valores:** &lt;*FilePath al archivo .MDB de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .MDB de base de datos.  

-   **Nombre de clave:** SQLLogFilePath  

    -   **Requerido** : no  

    -   **Valores:** &lt;*FilePath al archivo .LDF de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .LDF de base de datos.  

**HierarchyExpansionOption**  

-   **Nombre de clave:** CCARSiteServer  

    -   **Requerido** : no  

    -   **Valores:** &lt;*FQDN de sitio de administración central*>  

    -   **Detalles:** especifica el sitio de administración central al que se asociará un sitio primario al unirse a la jerarquía de Configuration Manager. Debe especificar el sitio de administración central mientras se ejecuta el programa de instalación.  

-   **Nombre de clave:** CASRetryInterval  

    -   **Requerido** : no  

    -   **Valores:** &lt;*Interval*>  

    -   **Detalles** : especifica el intervalo de reintento (en minutos) para tratar de establecer una conexión con el sitio de administración central después de que la conexión genera un error. Por ejemplo, si se produce un error en la conexión al sitio de administración central, el sitio primario espera el número de minutos especificado en CASRetryInterval y, a continuación, vuelve a intentar establecer la conexión.  

-   **Nombre de clave:** WaitForCASTimeout  

    -   **Requerido** : no  

    -   **Valores:** &lt;*Timeout*>  

         Un valor de 0 a 100.  

    -   **Detalles:** especifica el valor de tiempo de espera máximo (en minutos) de un sitio primario para conectarse al sitio de administración central. Por ejemplo, si se produce un error de conexión del sitio primario con el sitio de administración central, el sitio primario vuelve a tratar de establecer la conexión conforme al valor especificado para CASRetryInterval hasta que se alcanza el valor de tiempo de WaitForCASTimeout. Puede especificar un valor entre 0 y 100.  

**CloudConnectorOptions**  

-   **Nombre de clave:** CloudConnector  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si instalará un punto de conexión de servicio en este sitio. Dado que el punto de conexión de servicio solo puede instalarse en el sitio de nivel superior de una jerarquía, este valor debe ser 0 para un sitio principal secundario.  

-   **Nombre de clave:** CloudConnectorServer  

    -   **Requerido:** necesario cuando CloudConnector es igual a 1  

    -   **Valores:** &lt;*FQDN del servidor de punto de conexión de servicio*\>  

    -   **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio del punto de conexión de servicio.  

-   **Nombre de clave:** UseProxy  

    -   **Requerido:** necesario cuando CloudConnector es igual a 1  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si el punto de conexión de servicio usará un servidor proxy.  

-   **Nombre de clave:** ProxyName  

    -   **Requerido:** necesario cuando UseProxy es igual a 1  

    -   **Valores:** &lt;*FQDN del servidor proxy*>  

    -   **Detalles:** especifica el FQDN del servidor proxy que usará el rol de sistema de sitio del punto de conexión de servicio.  

-   **Nombre de clave:** ProxyPort  

    -   **Requerido:** necesario cuando UseProxy es igual a 1  

    -   **Valores:** &lt;*PortNumber*>  

    -   **Detalles:** especifica el número de puerto que se usará.  

### <a name="unattended-recovery-for-a-central-administration-site"></a>Recuperación desatendida de un sitio de administración central  
 Use los siguientes detalles para recuperar un sitio de administración central mediante un archivo de script de instalación desatendida.  

**Identificación**  

-   **Nombre de clave:** Action  

    -   **Requerido** : sí  

    -   **Valores** : RecoverCCAR  

    -   **Detalles:** recupera un sitio de administración central.  

**RecoveryOptions**  

-   **Nombre de clave:** ServerRecoveryOptions  

    -   **Requerido** : sí  

    -   **Valores** : 1, 2 o 4  

         1 = servidor de sitio de recuperación y SQL Server.  

         2 = recuperar sólo servidor de sitio.  

         4 = recuperar sólo SQL Server.  

    -   **Detalles** : especifica si el programa de instalación recuperará el servidor de sitio, SQL Server o ambos. Las claves asociadas son necesarias cuando se establece el siguiente valor para la configuración de ServerRecoveryOptions:  

        -   Valor = 1: tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

        -   Valor = 2: tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

        -   Valor = 4: se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se usa para restaurar la base de datos de sitio desde la copia de seguridad.  

-   **Nombre de clave:** DatabaseRecoveryOptions  

    -   **Requerido:** esta clave es necesaria cuando ServerRecoveryOptions tiene un valor de **1** o **4**.  

    -   **Valores:** 10, 20, 40, 80  

         10 = restaurar la base de datos de sitio desde la copia de seguridad.  

         20 = utilizar una base de datos de sitio que se recuperó manualmente mediante otro método.  

         40 = crear una base de datos nueva para el sitio. Utilice esta opción si no hay ninguna copia de seguridad de base de datos de sitio disponible. Los datos globales y de sitio se recuperan mediante la replicación desde otros sitios.  

         80 = omitir recuperación de base de datos.  

    -   **Detalles:** especifica cómo recupera el programa de instalación la base de datos de sitio en SQL Server.  

-   **Nombre de clave:** ReferenceSite  

    -   **Requerido:** esta clave es necesaria cuando **DatabaseRecoveryOptions** tiene un valor de **40**.  

    -   **Valores:** &lt;*ReferenceSiteFQDN*>  

    -   **Detalles** : especifica el sitio primario de referencia que usa el sitio de administración central para recuperar datos globales si la copia de seguridad de la base de datos es anterior al período de retención de seguimiento de cambios, o si se recupera el sitio sin usar una copia de seguridad.  

         Si no especifica ningún sitio de referencia y la copia de seguridad es anterior al período de retención de seguimiento de cambios, todos los sitios primarios se reinicializan con los datos restaurados desde el sitio de administración central.  

         Si no especifica ningún sitio de referencia, y la copia de seguridad pertenece al período de retención de seguimiento de cambios, sólo se replicarán desde los sitios primarios los cambios que tuvieron lugar después de la copia de seguridad. Si existen cambios en conflicto de varios sitios primarios, el sitio de administración central utiliza el primero que recibe.  

-   **Nombre de clave:** SiteServerBackupLocation  

    -   **Requerido** : no  

    -   **Valores:** &lt;*PathToSiteServerBackupSet*>  

    -   **Detalles** : especifica la ruta de acceso al conjunto de copia de seguridad del servidor de sitio. Esta clave es opcional si **ServerRecoveryOptions** tiene un valor de **1** o **2**. Especifique un valor para la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

-   **Nombre de clave:** BackupLocation  

    -   **Requerido:** esta clave es necesaria cuando se configura un valor de **1** o **4** para la clave **ServerRecoveryOptions** y cuando se configura un valor de **10** para la clave **DatabaseRecoveryOptions**.  

    -   **Valores:** &lt;*PathToSiteDatabaseBackupSet*>  

    -   **Detalles** : especifica la ruta de acceso al conjunto de copia de seguridad de base de datos de sitio.  

**Opciones**  

-   **Nombre de clave:** ProductID  

    -   **Requerido** : sí  

    -   **Valores:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* o *Eval*  

    -   **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones. Escriba **Eval** para instalar la versión de evaluación de Configuration Manager.  

-   **Nombre de clave:** SiteCode  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*SiteCode*>  

    -   **Detalles:** especifica tres caracteres alfanuméricos que identifican al sitio de forma única en la jerarquía. Debe especificar el código de sitio que utilizó el sitio antes de que se produjera el error. Para más información sobre las restricciones de código de sitio, consulte la sección [Acerca de los nombres de sitio y los códigos de sitio](#bkmk_codes) en este tema.  

-   **Nombre de clave:** SiteName  

    -   **Requerido** : no  

    -   **Valores:** &lt;*SiteName*>  

    -   **Detalles:** especifica el nombre de este sitio.  

-   **Nombre de clave:** SMSInstallDir  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*ConfigMgrInstallationPath*>  

    -   **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.  

-   **Nombre de clave:** SDKServer  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*FQDN del proveedor de SMS*>  

    -   **Detalles** : especifica el FQDN del servidor que hospedará el proveedor de SMS. Debe especificar el servidor que hospedaba el proveedor de SMS antes de producirse el error.  

         Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial. Para más información sobre el proveedor de SMS, vea [Plan para el proveedor de SMS de System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nombre de clave:**: PrerequisiteComp  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = descargar  

         1 = ya se ha descargado  

    -   **Detalles** : especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si usa un valor de **0**, el programa de instalación descargará los archivos.  

-   **Nombre de clave:** PrerequisitePath  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalles** : especifica la ruta de acceso a los archivos de requisitos previos de instalación. Dependiendo del valor **PrerequisiteComp** , el programa de instalación utiliza esta ruta para almacenar los archivos descargados o localizar los archivos descargados previamente.  

-   **Nombre de clave:** AdminConsole  

    -   **Requerido:** esta clave es necesaria, excepto cuando **ServerRecoveryOptions** tiene un valor de **4**.  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si se va a instalar la consola de Configuration Manager.  

-   **Nombre de clave:** JoinCEIP  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no unir  

         1 = unir  

    -   **Detalles** : especifica si se unirá al Programa para la mejora de la experiencia del usuario.  

**SQLConfigOptions**  

-   **Nombre de clave:** SQLServerName  

    -   **Requerido** : sí  

    -   **Valores:** *SQLServerName*  

    -   **Detalles:** especifica el nombre del servidor o el nombre de la instancia en clúster que ejecuta SQL Server, que hospedará la base de datos de sitio. Debe especificar el mismo servidor que hospedaba la base de datos del sitio antes de producirse el error.  

-   **Nombre de clave:** DatabaseName  

    -   **Requerido** : sí  

    -   **Valores:** *&lt;SiteDatabaseName\>* o *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **Detalles:**  

         Especifica el nombre de la base de datos de SQL Server que se crea o utiliza para instalar la base de datos del sitio de administración central. Debe especificar el mismo nombre de base de datos que se utilizó antes de producirse el error.  

        > [!IMPORTANT]  
        >  Debe especificar el nombre de instancia y el nombre de la base de datos del sitio si no utiliza la instancia predeterminada.  

-   **Nombre de clave:** SQLSSBPort  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*SSBPortNumber*>  

    -   **Detalles:** especifica el puerto de SQL Server Service Broker (SSB) que usa SQL Server. Normalmente, SSB está configurado para usar el puerto TCP 4022. Debe especificar el mismo puerto SSB que se utilizó antes de producirse el error.  

-   **Nombre de clave:** SQLDataFilePath  

    -   **Requerido** : no  

    -   **Valores:** &lt;*FilePath al archivo .MDB de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .MDB de base de datos.  

-   **Nombre de clave:** SQLLogFilePath  

    -   **Requerido** : no  

    -   **Valores:** &lt;*FilePath al archivo .LDF de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .LDF de base de datos.  

**CloudConnectorOptions**  

-   **Nombre de clave:** CloudConnector  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si instalará un punto de conexión de servicio en este sitio. Dado que el punto de conexión de servicio solo puede instalarse en el sitio de nivel superior de una jerarquía, este valor debe ser 0 para un sitio principal secundario.  

-   **Nombre de clave:** CloudConnecorServer  

    -   **Requerido:** necesario cuando CloudConnector es igual a 1  

    -   **Valores:** &lt;*FQDN del servidor de punto de conexión de servicio*>  

    -   **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio del punto de conexión de servicio.  

-   **Nombre de clave:** UseProxy  

    -   **Requerido:** necesario cuando CloudConnector es igual a 1  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si el punto de conexión de servicio usará un servidor proxy.  

-   **Nombre de clave:** ProxyName  

    -   **Requerido:** necesario cuando CloudConnector es igual a 1  

    -   **Valores:** &lt;*FQDN del servidor proxy*>  

    -   **Detalles:** especifica el FQDN del servidor proxy que usará el rol de sistema de sitio del punto de conexión de servicio.  

-   **Nombre de clave:** ProxyPort  

    -   **Requerido:** necesario cuando CloudConnector es igual a 1  

    -   **Valores:** &lt;*PortNumber*>  

    -   **Detalles:** especifica el número de puerto que se usará.  

### <a name="unattended-recovery-for-a-primary-site"></a>Recuperación desatendida de un sitio principal  
 Utilice los siguientes datos para recuperar un sitio principal mediante un archivo de script de instalación desatendida.  

**Identificación**  

-   **Nombre de clave:** Action  

    -   **Requerido** : sí  

    -   **Valores** : RecoverPrimarySite  

    -   **Detalles:** recupera un sitio primario.  

**RecoveryOptions**  

-   **Nombre de clave:** ServerRecoveryOptions  

    -   **Requerido** : sí  

    -   **Valores** : 1, 2 o 4  

         1 = servidor de sitio de recuperación y SQL Server.  

         2 = recuperar sólo servidor de sitio.  

         4 = recuperar sólo SQL Server.  

    -   **Detalles** : especifica si el programa de instalación recuperará el servidor de sitio, SQL Server o ambos. Las claves asociadas son necesarias cuando se establece el siguiente valor para la configuración de ServerRecoveryOptions:  

        -   Valor = 1: tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

        -   Valor = 2: tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

        -   Valor = 4: se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se usa para restaurar la base de datos de sitio desde la copia de seguridad.  

-   **Nombre de clave:** DatabaseRecoveryOptions  

    -   **Requerido:** esta clave es necesaria cuando ServerRecoveryOptions tiene un valor de **1** o **4**.  

    -   **Valores:** 10, 20, 40, 80  

         10 = restaurar la base de datos de sitio desde la copia de seguridad.  

         20 = utilizar una base de datos de sitio que se recuperó manualmente mediante otro método.  

         40 = crear una base de datos nueva para el sitio. Utilice esta opción si no hay ninguna copia de seguridad de base de datos de sitio disponible. Los datos globales y de sitio se recuperan mediante la replicación desde otros sitios.  

         80 = omitir recuperación de base de datos.  

    -   **Detalles:** especifica cómo recupera el programa de instalación la base de datos de sitio en SQL Server.  

-   **Nombre de clave:** SiteServerBackupLocation  

    -   **Requerido** : no  

    -   **Valores:** &lt;*PathToSiteServerBackupSet*>  

    -   **Detalles:**  

         Especifica la ruta de acceso para el conjunto de copia de seguridad del servidor de sitio. Esta clave es opcional si la opción **ServerRecoveryOptions** tiene un valor de **1** o **2**. Especifique un valor para la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

-   **Nombre de clave:** BackupLocation  

    -   **Requerido:** esta clave es necesaria cuando se configura un valor de **1** o **4** para la clave **ServerRecoveryOptions** y cuando se configura un valor de **10** para la clave **DatabaseRecoveryOptions**.  

    -   **Valores:** &lt;*PathToSiteDatabaseBackupSet*>  

    -   **Detalles** : especifica la ruta de acceso al conjunto de copia de seguridad de base de datos de sitio.  

**Opciones**  

-   **Nombre de clave:** ProductID  

    -   **Requerido** : sí  

    -   **Valores:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* o *Eval*  

    -   **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones. Escriba **Eval** para instalar la versión de evaluación de Configuration Manager.  

-   **Nombre de clave:** SiteCode  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*SiteCode*>  

    -   **Detalles:** especifica tres caracteres alfanuméricos que identifican al sitio de forma única en la jerarquía. Debe especificar el código de sitio que utilizó el sitio antes de que se produjera el error. Para más información sobre las restricciones de código de sitio, consulte la sección [Acerca de los nombres de sitio y los códigos de sitio](#bkmk_codes) en este tema.  

-   **Nombre de clave:** SiteName  

    -   **Requerido** : no  

    -   **Valores:** &lt;*SiteName*>  

    -   **Detalles:** especifica el nombre de este sitio.  

-   **Nombre de clave:** SMSInstallDir  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*ConfigMgrInstallationPath*>  

    -   **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.  

-   **Nombre de clave:** SDKServer  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*FQDN del proveedor de SMS*>  

    -   **Detalles** : especifica el FQDN del servidor que hospedará el proveedor de SMS. Debe especificar el servidor que hospedaba el proveedor de SMS antes de producirse el error. Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial. Para más información sobre el proveedor de SMS, vea [Plan para el proveedor de SMS de System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nombre de clave:**: PrerequisiteComp  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = descargar  

         1 = ya se ha descargado  

    -   **Detalles** : especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si usa un valor de **0**, el programa de instalación descargará los archivos.  

-   **Nombre de clave:** PrerequisitePath  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalles** : especifica la ruta de acceso a los archivos de requisitos previos de instalación. Dependiendo del valor **PrerequisiteComp** , el programa de instalación utiliza esta ruta para almacenar los archivos descargados o localizar los archivos descargados previamente.  

-   **Nombre de clave:** AdminConsole  

    -   **Requerido:** esta clave es necesaria, excepto cuando **ServerRecoveryOptions** tiene un valor de **4**.  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si se va a instalar la consola de Configuration Manager.  

-   **Nombre de clave:** JoinCEIP  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no unir  

         1 = unir  

    -   **Detalles** : especifica si se unirá al Programa para la mejora de la experiencia del usuario.  

**SQLConfigOptions**  

-   **Nombre de clave:** SQLServerName  

    -   **Requerido** : sí  

    -   **Valores:** *SQLServerName*  

    -   **Detalles:** especifica el nombre del servidor o el nombre de la instancia en clúster que ejecuta SQL Server, que hospedará la base de datos de sitio. Debe especificar el mismo servidor que hospedaba la base de datos del sitio antes de producirse el error.  

-   **Nombre de clave:** DatabaseName  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*SiteDatabaseName*\> o &lt;*InstanceName*\>\\&lt;*SiteDatabaseName*\>

    -   **Detalles:**  

         Especifica el nombre de la base de datos de SQL Server que se crea o utiliza para instalar la base de datos del sitio de administración central. Debe especificar el mismo nombre de base de datos que se utilizó antes de producirse el error.  

        > [!IMPORTANT]  
        >  Debe especificar el nombre de instancia y el nombre de la base de datos del sitio si no utiliza la instancia predeterminada.  

-   **Nombre de clave:** SQLSSBPort  

    -   **Requerido** : sí  

    -   **Valores:** &lt;*SSBPortNumber*>  

    -   **Detalles:** especifica el puerto de SQL Server Service Broker (SSB) que usa SQL Server. Normalmente, SSB está configurado para usar el puerto TCP 4022. Debe especificar el mismo puerto SSB que se utilizó antes de producirse el error.  

-   **Nombre de clave:** SQLDataFilePath  

    -   **Requerido** : no  

    -   **Valores:** &lt;*FilePath al archivo .MDB de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .MDB de base de datos.  

-   **Nombre de clave:** SQLLogFilePath  

    -   **Requerido** : no  

    -   **Valores:** &lt;*FilePath al archivo .LDF de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .LDF de base de datos.  

**HierarchyExpansionOptions**  

-   **Nombre de clave:** CCARSiteServer  

    -   **Requerido:** ver detalles.  

    -   **Valores:** &lt;*SiteCodeForCentralAdministrationSite*>  

    -   **Detalles:** especifica el sitio de administración central al que se asocia un sitio primario cuando se une a la jerarquía de Configuration Manager. Esta configuración es necesaria si el sitio primario estaba asociado con un sitio de administración central antes de producirse el error. Debe especificar el código del sitio que utilizó el sitio de administración central antes de que se produjera el error.  

-   **Nombre de clave:** CASRetryInterval  

    -   **Requerido** : no  

    -   **Valores:** &lt;*Interval*>  

    -   **Detalles** : especifica el intervalo de reintento (en minutos) para tratar de establecer una conexión con el sitio de administración central después de que la conexión genera un error. Por ejemplo, si se produce un error en la conexión al sitio de administración central, el sitio primario espera el número de minutos especificado en **CASRetryInterval**y, a continuación, vuelve a intentar establecer la conexión.  

-   **Nombre de clave:** WaitForCASTimeout  

    -   **Requerido** : no  

    -   **Valores:** &lt;*Timeout*>  

    -   **Detalles:** especifica el valor de tiempo de espera máximo (en minutos) de un sitio primario para conectarse al sitio de administración central. Por ejemplo, si se produce un error de conexión del sitio primario con el sitio de administración central, el sitio primario vuelve a tratar de establecer la conexión conforme al valor especificado para **CASRetryInterval** hasta que se alcanza el valor de tiempo de **WaitForCASTimeout** . Puede especificar un valor entre 0 y 100.  

**CloudConnectorOptions**  

-   **Nombre de clave:** CloudConnector  

    -   **Requerido** : sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si instalará un punto de conexión de servicio en este sitio. Dado que el punto de conexión de servicio solo puede instalarse en el sitio de nivel superior de una jerarquía, este valor debe ser 0 para un sitio principal secundario.  

-   **Nombre de clave:** CloudConnecorServer  

    -   **Requerido:** necesario cuando CloudConnector es igual a 1  

    -   **Valores:** &lt;*FQDN del servidor de punto de conexión de servicio*>  

    -   **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio del punto de conexión de servicio.  

-   **Nombre de clave:** UseProxy  

    -   **Requerido:** necesario cuando CloudConnector es igual a 1  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si el punto de conexión de servicio usará un servidor proxy.  

-   **Nombre de clave:** ProxyName  

    -   **Requerido:** necesario cuando CloudConnector es igual a 1  

    -   **Valores:** &lt;*FQDN del servidor proxy*>  

    -   **Detalles:** especifica el FQDN del servidor proxy que usará el rol de sistema de sitio del punto de conexión de servicio.  

-   **Nombre de clave:** ProxyPort  

    -   **Requerido:** necesario cuando CloudConnector es igual a 1  

    -   **Valores:** &lt;*PortNumber*>  

    -   **Detalles:** especifica el número de puerto que se usará.  



<!--HONumber=Nov16_HO1-->


