---
title: Configuración de opciones de la línea de comandos
titleSuffix: Configuration Manager
description: Cree scripts de automatización para instalar System Center Configuration Manager desde una línea de comandos.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
caps.latest.revision: 3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fede359c884ef8b4027935b2e3fb48a5b7543d26
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2018
---
# <a name="command-line-options-for-setup-in-system-center-configuration-manager"></a>Opciones de la línea de comandos para la instalación en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


 Use la información siguiente para configurar scripts o instalar System Center Configuration Manager desde una línea de comandos.  

##  <a name="bkmk_setup"></a> Opciones de la línea de comandos para la instalación  
 **/DEINSTALL**  
 Desinstala el sitio. Ejecute el programa de instalación desde el equipo de servidor de sitio.  

 **/DONTSTARTSITECOMP**  
 Instala un sitio, pero impide que se inicie el servicio Administrador de componentes de sitio. Hasta que se inicie el servicio Administrador de componentes del sitio, el sitio no está activo. El Administrador de componentes de sitio es responsable de instalar e iniciar el servicio SMS_Executive y de procesos adicionales en el sitio. Una vez completada la instalación del sitio, cuando se inicia el servicio Administrador de componentes de sitio, instala el servicio SMS_Executive y los procesos adicionales necesarios para que el sitio funcione.  

 **/HIDDEN**  
 Oculta la interfaz de usuario durante la instalación. Use esta opción solamente en combinación con la opción **/SCRIPT**. El archivo de script desatendido debe proporcionar todas las opciones necesarias o se produce un error en la instalación.  

 **/NOUSERINPUT**  
 Deshabilita la entrada del usuario durante la instalación, pero muestra el Asistente para la instalación. Use esta opción solamente en combinación con la opción **/SCRIPT**. El archivo de script desatendido debe proporcionar todas las opciones necesarias o se produce un error en la instalación.  

 **/RESETSITE**  
 Realiza el restablecimiento de un sitio; restablece las cuentas del servicio y la base de datos para el sitio. Ejecute el programa de instalación desde **<*ruta de instalación de Configuration Manager*>\BIN\X64** en el servidor de sitio. Para más información sobre el restablecimiento del sitio, vea la sección [Ejecutar un restablecimiento de sitio](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) en [Modificar la infraestructura de System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).  

 **/TESTDBUPGRADE <*nombre de instancia*>\\<*nombre de base de datos*>**  
 Realiza una prueba en una copia de seguridad de la base de datos del sitio para asegurarse de que la base de datos es capaz de una actualización. Proporcione el nombre de instancia y el nombre de base de datos de la base de datos del sitio. Si solo se especifica el nombre de base de datos, el programa de instalación usa el nombre de instancia predeterminado.  

> [!IMPORTANT]  
>  No ejecute esta opción de línea de comandos en la base de datos del sitio de producción. Ejecutar esta opción de línea de comandos en la base de datos del sitio de producción actualiza la base de datos del sitio y podría inutilizar el sitio.  

 **/UPGRADE**  
 Ejecuta una actualización desatendida de un sitio. Cuando use **/UPGRADE**, también debe especificar la clave del producto, incluidos los guiones (-). Además, se debe especificar la ruta de acceso a los archivos de requisitos previos de instalación descargados anteriormente.  

 Ejemplo: `setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

 Para obtener más información sobre los archivos de requisitos previos de la instalación, vea [Descargador del programa de instalación](setup-downloader.md).  

 **/SCRIPT <*ruta de acceso del script de instalación*>**  
 Realiza instalaciones desatendidas. Es necesario un archivo de inicialización del programa de instalación cuando se usa la opción **/SCRIPT**. Para obtener más información sobre cómo ejecutar una instalación desatendida, vea [Usar una línea de comandos para instalar sitios de System Center Configuration Manager](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).  

 **/SDKINST <*FQDN del proveedor de SMS*>**  
 Instala el proveedor de SMS en el equipo especificado. Proporcione el nombre de dominio completo (FQDN) para el equipo del proveedor de SMS. Para obtener más información sobre el proveedor de SMS, vea [Plan para el proveedor de SMS](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

 **/SDKDEINST <*FQDN del proveedor de SMS*>**  
 Desinstala el proveedor de SMS en el equipo especificado. Proporcione el FQDN del equipo de proveedor de SMS.  

 **/MANAGELANGS <*ruta del acceso del script de idioma*>**  
 Administra los idiomas que se instalan en un sitio instalado previamente. Para usar esta opción, ejecute el programa de instalación desde **<*ruta de instalación de Configuration Manager*>\BIN\X64** en el servidor de sitio. Proporcione la ubicación del archivo de script de idioma que contiene la configuración de idioma. Para obtener más información sobre las opciones de idioma disponibles en el archivo de script de configuración de idioma, vea la sección [Opciones de la línea de comandos para administrar idiomas](#bkmk_Lang).  

##  <a name="bkmk_Lang"></a> Opciones de línea de comandos para administrar idiomas  
 **Identificación**  

-   **Nombre de clave:** Action  

    -   **Requerido**: sí  

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

    -   **Detalles:** especifica los idiomas que se quitarán y que ya no estarán disponibles para la consola, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada y no se puede quitar.  

-   **Nombre de clave:** DeleteClientLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** especifica los idiomas para quitar y cuáles ya no estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada y no se puede quitar.  

-   **Nombre de clave:** MobileDeviceLanguage  

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si están instalados los idiomas de cliente de dispositivo móvil.  

-   **Nombre de clave:**: PrerequisiteComp  

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = descargar  

         1 = ya se ha descargado  

    -   **Detalles:** especifica si ya se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si usa un valor de **0**, el programa de instalación descarga los archivos.  

-   **Nombre de clave:** PrerequisitePath  

    -   **Requerido**: sí  

    -   **Valores:** <*ruta de acceso a los archivos de requisitos previos de instalación*>  

    -   **Detalles:** especifica la ruta de acceso a los archivos de requisitos previos de instalación. En función del valor **PrerequisiteComp**, el programa de instalación usa esta ruta de acceso para almacenar los archivos descargados o localizar los archivos descargados previamente.  

##  <a name="bkmk_Unattended"></a> Claves de archivo de scripts de instalación desatendida  
 Use las secciones siguientes para crear el script para la instalación desatendida. En la lista se muestran las claves del script de instalación disponibles, sus valores correspondientes, si son necesarias o no, el tipo de instalación para el que se usan y una breve descripción de cada clave.  

### <a name="unattended-install-for-a-central-administration-site"></a>Instalación desatendida de un sitio de administración central  
 Use los datos siguientes para instalar un sitio de administración central mediante un archivo de script de instalación desatendida.  

**Identificación**  

-   **Nombre de clave:** Action  

    -   **Requerido**: sí  

    -   **Valores:** InstallCAS  

    -   **Detalles:** instala un sitio de administración central.  

-   **Nombre de clave:** CDLatest  

    -   **Necesario:** sí, solo cuando se utilizan medios de la carpeta CD.Latest.    

    -   **Valores:** 1 si el valor es distinto de 1, se considera que no se usa CD.Latest.

    -   **Detalles:** el script debe incluir esta clave y valor al ejecutar el programa de instalación desde medios de una carpeta CD.Latest, con el fin de instalar un sitio de administración central o principal, o bien para recuperar estos sitios. Este valor indica al programa de instalación que se están usando medios de la carpeta CD.Latest.

**Opciones**  

-   **Nombre de clave:** ProductID  

    -   **Requerido**: sí  

    -   **Valores:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *o* Eval  

    -   **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones. Escriba **Eval** para instalar la versión de evaluación de Configuration Manager.  

-   **Nombre de clave:** SiteCode  

    -   **Requerido**: sí  

    -   **Valores:** <*código de sitio*>  

    -   **Detalles:** especifica tres caracteres alfanuméricos que identifican al sitio de forma única en la jerarquía.  

-   **Nombre de clave:** nombre del sitio  

    -   **Requerido**: sí  

    -   **Valores:** <*nombre de sitio*>  

    -   **Detalles:** especifica el nombre de este sitio.  

-   **Nombre de clave:** SMSInstallDir  

    -   **Requerido**: sí  

    -   **Valores:** <*ruta de instalación de Configuration Manager*>  

    -   **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.  

-   **Nombre de clave:** SDKServer  

    -   **Requerido**: sí  

    -   **Valores:** <*FQDN del proveedor de SMS*>  

    -   **Detalles** : especifica el FQDN del servidor que hospedará el proveedor de SMS. Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial.  

-   **Nombre de clave:**: PrerequisiteComp  

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = descargar  

         1 = ya se ha descargado  

    -   **Detalles:** especifica si ya se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si usa un valor de **0**, el programa de instalación descarga los archivos.  

-   **Nombre de clave:** PrerequisitePath  

    -   **Requerido**: sí  

    -   **Valores:** <*ruta de acceso a los archivos de requisitos previos de instalación*>  

    -   **Detalles:** especifica la ruta de acceso a los archivos de requisitos previos de instalación. En función del valor **PrerequisiteComp**, el programa de instalación usa esta ruta de acceso para almacenar los archivos descargados o localizar los archivos descargados previamente.  

-   **Nombre de clave:** AdminConsole  

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si se va a instalar la consola de Configuration Manager.  

-   **Nombre de clave:** JoinCEIP  
    > [!Note]  
    > A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto.

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = no unir  

         1 = unir  

    -   **Detalles:** especifica si se unirá al Programa para la mejora de la experiencia del usuario (CEIP).  

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

    -   **Detalles:** modifica un sitio después de instalarlo. Especifica los idiomas que se quitarán y que ya no estarán disponibles para la consola, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada y no se puede quitar.  

-   **Nombre de clave:** DeleteClientLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** modifica un sitio después de instalarlo. Especifica los idiomas para quitar y cuáles ya no estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada y no se puede quitar.  

-   **Nombre de clave:** MobileDeviceLanguage  

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si están instalados los idiomas de cliente de dispositivo móvil.  

**SQLConfigOptions**  

-   **Nombre de clave:** SQLServerName  

    -   **Requerido**: sí  

    -   **Valores:** <*nombre de servidor SQL*>  

    -   **Detalles:** especifica el nombre del servidor o de la instancia en clúster que ejecuta SQL Server, y cuál hospedará la base de datos de sitio.  

-   **Nombre de clave:** DatabaseName  

    -   **Requerido**: sí  

    -   **Valores:** <*nombre de base de datos de sitio*> o <*nombre de instancia*>\\<*nombre de base de datos de sitio*>  

    -   **Detalles:** especifica el nombre de la base de datos de SQL Server que se va a crear o usar cuando el programa de instalación instala la base de datos del sitio de administración central.  

        > [!IMPORTANT]  
        >  Si no se usa la instancia predeterminada, se debe especificar el nombre de instancia y el nombre de la base de datos del sitio.  

-   **Nombre de clave:** SQLSSBPort  

    -   **Requerido** : no  

    -   **Valores:** <*número de puerto SSB*>  

    -   **Detalles:** especifica el puerto de SQL Server Service Broker (SSB) que usa SQL Server. Normalmente, SSB está configurado para usar el puerto TCP 4022, pero se puede usar otro puerto.  

-   **Nombre de clave:** SQLDataFilePath  

    -   **Requerido** : no  

    -   **Valores:** <*ruta de acceso al archivo .mdb de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .mdb de base de datos.  

-   **Nombre de clave:** SQLLogFilePath  

    -   **Requerido** : no  

    -   **Valores:** <*ruta de acceso al archivo .ldf de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .ldf de base de datos.  

**CloudConnectorOptions**  

-   **Nombre de clave:** CloudConnector  

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si se instala un punto de conexión de servicio en este sitio. Dado que el punto de conexión de servicio solo puede instalarse en el sitio de nivel superior de una jerarquía, este valor debe ser **0** para un sitio principal secundario.  

-   **Nombre de clave:** CloudConnectorServer  

    -   **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1  

    -   **Valores:** <*FQDN del servidor de punto de conexión de servicio*>  

    -   **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio del punto de conexión de servicio.  

-   **Nombre de clave:** UseProxy  

    -   **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si el punto de conexión de servicio usa un servidor proxy.  

-   **Nombre de clave:** ProxyName  

    -   **Obligatorio:** obligatorio cuando **UseProxy** es igual a 1  

    -   **Valores:** <*FQDN del servidor proxy*>  

    -   **Detalles:** especifica el FQDN del servidor proxy que usa el punto de conexión de servicio.  

-   **Nombre de clave:** ProxyPort  

    -   **Obligatorio:** obligatorio cuando **UseProxy** es igual a 1  

    -   **Valores:** <*número de puerto*>  

    -   **Detalles:** especifica el número de puerto que se usará para el puerto de proxy.  

### <a name="unattended-install-for-a-primary-site"></a>Instalación desatendida de un sitio principal  
Use los detalles siguientes para instalar un sitio primario mediante un archivo de script de instalación desatendida.  

**Identificación**  

-   **Nombre de clave:** Action  

    -   **Requerido**: sí  

    -   **Valores:** InstallPrimarySite  

    -   **Detalles:** instala un sitio primario.  

-   **Nombre de clave:** CDLatest  

    -   **Necesario:** sí, solo cuando se utilizan medios de la carpeta CD.Latest.    

    -   **Valores:** 1 si el valor es distinto de 1, se considera que no se usa CD.Latest.

    -   **Detalles:** el script debe incluir esta clave y valor al ejecutar el programa de instalación desde medios de una carpeta CD.Latest, con el fin de instalar un sitio de administración central o principal, o bien para recuperar estos sitios. Este valor indica al programa de instalación que se están usando medios de la carpeta CD.Latest.

**Opciones**  

-   **Nombre de clave:** ProductID  

    -   **Requerido**: sí  

    -   **Valores:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *o* Eval  

    -   **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones. Escriba **Eval** para instalar la versión de evaluación de Configuration Manager.  

-   **Nombre de clave:** SiteCode  

    -   **Requerido**: sí  

    -   **Valores:** <*código de sitio*>  

    -   **Detalles:** especifica tres caracteres alfanuméricos que identifican al sitio de forma única en la jerarquía.  

-   **Nombre de clave:** SiteName  

    -   **Requerido**: sí  

    -   **Valores:** <*nombre de sitio*>  

    -   **Detalles:** especifica el nombre de este sitio.  

-   **Nombre de clave:** SMSInstallDir  

    -   **Requerido**: sí  

    -   **Valores:** <*ruta de instalación de Configuration Manager*>

    -   **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.  

-   **Nombre de clave:** SDKServer  

    -   **Requerido**: sí  

    -   **Valores:** <*FQDN del proveedor de SMS*>  

    -   **Detalles** : especifica el FQDN del servidor que hospedará el proveedor de SMS. Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial.  

-   **Nombre de clave:**: PrerequisiteComp  

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = descargar  

         1 = ya se ha descargado  

    -   **Detalles:** especifica si ya se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si usa un valor de **0**, el programa de instalación descarga los archivos.  

-   **Nombre de clave:** PrerequisitePath  

    -   **Requerido**: sí  

    -   **Valores:** <*ruta de acceso a los archivos de requisitos previos de instalación*>  

    -   **Detalles:** especifica la ruta de acceso a los archivos de requisitos previos de instalación. En función del valor **PrerequisiteComp**, el programa de instalación usa esta ruta de acceso para almacenar los archivos descargados o localizar los archivos descargados previamente.  

-   **Nombre de clave:** AdminConsole  

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si se va a instalar la consola de Configuration Manager.  

-   **Nombre de clave:** JoinCEIP  
    > [!Note]  
    > A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto.

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = no unir  

         1 = unir  

    -   **Detalles:**: especifica si se unirá al CEIP.  

-   **Nombre de clave:** ManagementPoint  

    -   **Requerido** : no  

    -   **Valores:** <*FQDN del servidor de sitio de punto de administración*>  

    -   **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio de punto de administración.  

-   **Nombre de clave:** ManagementPointProtocol  

    -   **Requerido** : no  

    -   **Valores:** HTTPS *o* HTTP  

    -   **Detalles:** especifica el protocolo que se va a usar para el punto de administración.  

-   **Nombre de clave:** DistributionPoint  

    -   **Requerido** : no  

    -   **Valores:** <*FQDN del servidor de sitio de punto de distribución*>  

    -   **Detalles:** especifica el protocolo que se va a usar para el punto de distribución.  

-   **Nombre de clave:** DistributionPointProtocol  

    -   **Requerido** : no  

    -   **Valores:** HTTPS *o* HTTP  

    -   **Detalles:** especifica el protocolo que se va a usar para el punto de distribución.  

-   **Nombre de clave:** RoleCommunicationProtocol  

    -   **Requerido**: sí  

    -   **Valores:** EnforceHTTPS *o* HTTPorHTTPS  

    -   **Detalles:** especifica si se van a configurar todos los sistemas de sitio para aceptar solo las comunicaciones HTTPS de los clientes o que el método de comunicación se configure para cada rol de sistema de sitio. Al seleccionar **EnforceHTTPS**, el equipo cliente debe tener un certificado de infraestructura de clave pública (PKI) válido para la autenticación de cliente.  

-   **Nombre de clave:** ClientsUsePKICertificate  

    -   **Requerido**: sí  

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

    -   **Detalles:** modifica un sitio después de instalarlo. Especifica los idiomas que se quitarán y que ya no estarán disponibles para la consola, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada y no se puede quitar.  

-   **Nombre de clave:** DeleteClientLanguages  

    -   **Requerido** : no  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Detalles:** modifica un sitio después de instalarlo. Especifica los idiomas para quitar y cuáles ya no estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada y no se puede quitar.  

-   **Nombre de clave:** MobileDeviceLanguage  

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si están instalados los idiomas de cliente de dispositivo móvil.  

**SQLConfigOptions**  

-   **Nombre de clave:** SQLServerName  

    -   **Requerido**: sí  

    -   **Valores:** <*nombre de servidor SQL*>  

    -   **Detalles:** especifica el nombre del servidor o de la instancia en clúster que ejecuta SQL Server, y cuál hospedará la base de datos de sitio.  

-   **Nombre de clave:** DatabaseName  

    -   **Requerido**: sí  

    -   **Valores:** <*nombre de base de datos de sitio*> o <*nombre de instancia*>\\<*nombre de base de datos de sitio*>  

    -   **Detalles:** especifica el nombre de la base de datos de SQL Server que se crea o usa para instalar la base de datos del sitio primario.  

        > [!IMPORTANT]  
        >  Si no se usa la instancia predeterminada, se debe especificar el nombre de instancia y el nombre de la base de datos del sitio.  

-   **Nombre de clave:** SQLSSBPort  

    -   **Requerido** : no  

    -   **Valores:** <*número de puerto SSB*>  

    -   **Detalles:** especifica el puerto SSB que usa SQL Server. Normalmente, SSB está configurado para usar el puerto TCP 4022, pero se puede usar otro puerto.  

-   **Nombre de clave:** SQLDataFilePath  

    -   **Requerido** : no  

    -   **Valores:** <*ruta de acceso al archivo .mdb de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .mdb de base de datos.  

-   **Nombre de clave:** SQLLogFilePath  

    -   **Requerido** : no  

    -   **Valores:** <*ruta de acceso al archivo .ldf de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .ldf de base de datos.  

**HierarchyExpansionOption**  

-   **Nombre de clave:** CCARSiteServer  

    -   **Requerido** : no  

    -   **Valores:** <*FQDN del sitio de administración central*>  

    -   **Detalles:** especifica el sitio de administración central al que se asocia un sitio primario al unirse a la jerarquía de Configuration Manager. Especifique el sitio de administración central durante el programa de instalación.  

-   **Nombre de clave:** CASRetryInterval  

    -   **Requerido** : no  

    -   **Valores:** <*Interval*>  

    -   **Detalles** : especifica el intervalo de reintento (en minutos) para tratar de establecer una conexión con el sitio de administración central después de que la conexión genera un error. Por ejemplo, si se produce un error en la conexión al sitio de administración central, el sitio primario espera el número de minutos especificado para el valor **CASRetryInterval** y, después, vuelve a intentar la conexión.  

-   **Nombre de clave:** WaitForCASTimeout  

    -   **Requerido** : no  

    -   **Valores:** <*Tiempo de espera*>  

         Un valor de **0** a **100**  

    -   **Detalles** : especifica el valor de tiempo de espera máximo (en minutos) de un sitio primario para conectarse al sitio de administración central. Por ejemplo, si se produce un error de conexión del sitio primario con el sitio de administración central, el sitio primario vuelve a tratar de establecer la conexión conforme al valor **CASRetryInterval** hasta que se alcanza el valor de tiempo de **WaitForCASTimeout**. Puede especificar un valor de **0** a **100**.  

**CloudConnectorOptions**  

-   **Nombre de clave:** CloudConnector  

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si se instala un punto de conexión de servicio en este sitio. Dado que el punto de conexión de servicio solo puede instalarse en el sitio de nivel superior de una jerarquía, este valor debe ser **0** para un sitio principal secundario.  

-   **Nombre de clave:** CloudConnectorServer  

    -   **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1  

    -   **Valores:** <*FQDN del servidor de punto de conexión de servicio*\>  

    -   **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio del punto de conexión de servicio.  

-   **Nombre de clave:** UseProxy  

    -   **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si el punto de conexión de servicio usa un servidor proxy.  

-   **Nombre de clave:** ProxyName  

    -   **Obligatorio:** obligatorio cuando **UseProxy** es igual a 1  

    -   **Valores:** <*FQDN del servidor proxy*>  

    -   **Detalles:** especifica el FQDN del servidor proxy que usa el punto de conexión de servicio.  

-   **Nombre de clave:** ProxyPort  

    -   **Obligatorio:** obligatorio cuando **UseProxy** es igual a 1  

    -   **Valores:** <*número de puerto*>  

    -   **Detalles:** especifica el número de puerto que se usará para el puerto de proxy.  

### <a name="unattended-recovery-for-a-central-administration-site"></a>Recuperación desatendida de un sitio de administración central  
 Use los detalles siguientes para recuperar un sitio de administración central mediante un archivo de script de instalación desatendida.  

**Identificación**  

-   **Nombre de clave:** Action  

    -   **Requerido**: sí  

    -   **Valores** : RecoverCCAR  

    -   **Detalles:** recupera un sitio de administración central.  

-   **Nombre de clave:** CDLatest  

    -   **Necesario:** sí, solo cuando se utilizan medios de la carpeta CD.Latest.    

    -   **Valores:** 1 si el valor es distinto de 1, se considera que no se usa CD.Latest.

    -   **Detalles:** el script debe incluir esta clave y valor al ejecutar el programa de instalación desde medios de una carpeta CD.Latest, con el fin de instalar un sitio de administración central o principal, o bien para recuperar estos sitios. Este valor indica al programa de instalación que se están usando medios de la carpeta CD.Latest.

**RecoveryOptions**  

-   **Nombre de clave:** ServerRecoveryOptions  

    -   **Requerido**: sí  

    -   **Valores** : 1, 2 o 4  

         1 = servidor de sitio de recuperación y SQL Server.  

         2 = recuperar sólo servidor de sitio.  

         4 = recuperar sólo SQL Server.  

    -   **Detalles**: especifica si el programa de instalación recupera el servidor de sitio, SQL Server o ambos. Las claves asociadas son necesarias cuando se establece el siguiente valor para el valor **ServerRecoveryOptions**:  

        -   Valor = 1: tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

        -   Valor = 2: tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

        -   Valor = 4: se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se usa para restaurar la base de datos de sitio desde la copia de seguridad.  

-   **Nombre de clave:** DatabaseRecoveryOptions  

    -   **Obligatorio:** esta clave es obligatoria cuando **ServerRecoveryOptions** tiene un valor de **1** o **4**.  

    -   **Valores:** 10, 20, 40 o 80  

         10 = restaurar la base de datos de sitio desde la copia de seguridad.  

         20 = utilizar una base de datos de sitio que se recuperó manualmente mediante otro método.  

         40 = crear una base de datos nueva para el sitio. Utilice esta opción si no hay ninguna copia de seguridad de base de datos de sitio disponible. Los datos globales y de sitio se recuperan mediante la replicación desde otros sitios.  

         80 = omitir recuperación de base de datos.  

    -   **Detalles:** especifica cómo recupera el programa de instalación la base de datos de sitio en SQL Server.  

-   **Nombre de clave:** ReferenceSite  

    -   **Requerido:** esta clave es necesaria cuando **DatabaseRecoveryOptions** tiene un valor de **40**.  

    -   **Valores:** <*FQDN del sitio de referencia*>  

    -   **Detalles:** especifica el sitio primario de referencia que usa el sitio de administración central para recuperar datos globales si la copia de seguridad de la base de datos es anterior al período de retención de seguimiento de cambios, o si se recupera el sitio sin usar una copia de seguridad.  

         Si no especifica ningún sitio de referencia y la copia de seguridad es anterior al período de retención de seguimiento de cambios, todos los sitios primarios se reinicializan con los datos restaurados desde el sitio de administración central.  

         Si no especifica ningún sitio de referencia y la copia de seguridad pertenece al período de retención de seguimiento de cambios, solo se replicarán desde los sitios primarios los cambios que tuvieron lugar después de la copia de seguridad. Si existen cambios en conflicto de varios sitios primarios, el sitio de administración central utiliza el primero que recibe.  

-   **Nombre de clave:** SiteServerBackupLocation  

    -   **Requerido** : no  

    -   **Valores:** <*ruta de acceso al conjunto de copia de seguridad de servidor de sitio*>  

    -   **Detalles** : especifica la ruta de acceso al conjunto de copia de seguridad del servidor de sitio. Esta clave es opcional si **ServerRecoveryOptions** tiene un valor de **1** o **2**. Especifique un valor para la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

-   **Nombre de clave:** BackupLocation  

    -   **Obligatorio:** esta clave es obligatoria cuando se configura un valor de **1** o **4** para la clave **ServerRecoveryOptions** y cuando se configura un valor de **10** para la clave **DatabaseRecoveryOptions**.  

    -   **Valores:** <*ruta de acceso al conjunto de copia de seguridad de sitio*>  

    -   **Detalles** : especifica la ruta de acceso al conjunto de copia de seguridad de base de datos de sitio.  

**Opciones**  

-   **Nombre de clave:** ProductID  

    -   **Requerido**: sí  

    -   **Valores:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *o* Eval  

    -   **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones. Escriba **Eval** para instalar la versión de evaluación de Configuration Manager.  

-   **Nombre de clave:** SiteCode  

    -   **Requerido**: sí  

    -   **Valores:** <*código de sitio*>  

    -   **Detalles:** especifica tres caracteres alfanuméricos que identifican al sitio de forma única en la jerarquía. Especifique el código de sitio que usó el sitio antes de producirse el error.

-   **Nombre de clave:** SiteName  

    -   **Requerido** : no  

    -   **Valores:** <*nombre de sitio*>  

    -   **Detalles:** especifica el nombre de este sitio.  

-   **Nombre de clave:** SMSInstallDir  

    -   **Requerido**: sí  

    -   **Valores:** <*ruta de instalación de Configuration Manager*>  

    -   **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.  

-   **Nombre de clave:** SDKServer  

    -   **Requerido**: sí  

    -   **Valores:** <*FQDN del proveedor de SMS*>  

    -   **Detalles:** especifica el FQDN del servidor que hospeda el proveedor de SMS. Especifique el servidor que hospedaba el proveedor de SMS antes de producirse el error.  

         Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial. Para más información sobre el proveedor de SMS, vea [Plan para el proveedor de SMS de System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nombre de clave:**: PrerequisiteComp  

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = descargar  

         1 = ya se ha descargado  

    -   **Detalles:** especifica si ya se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si usa un valor de **0**, el programa de instalación descarga los archivos.  

-   **Nombre de clave:** PrerequisitePath  

    -   **Requerido**: sí  

    -   **Valores:** <*ruta de acceso a los archivos de requisitos previos de instalación*>  

    -   **Detalles:** especifica la ruta de acceso a los archivos de requisitos previos de instalación. En función del valor **PrerequisiteComp**, el programa de instalación usa esta ruta de acceso para almacenar los archivos descargados o localizar los archivos descargados previamente.  

-   **Nombre de clave:** AdminConsole  

    -   **Requerido:** esta clave es necesaria, excepto cuando **ServerRecoveryOptions** tiene un valor de **4**.  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si se va a instalar la consola de Configuration Manager.  

-   **Nombre de clave:** JoinCEIP  
    > [!Note]  
    > A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto.

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = no unir  

         1 = unir  

    -   **Detalles:**: especifica si se unirá al CEIP.  

**SQLConfigOptions**  

-   **Nombre de clave:** SQLServerName  

    -   **Requerido**: sí  

    -   **Valores:** <*nombre de servidor SQL*>  

    -   **Detalles:** especifica el nombre del servidor o de la instancia en clúster que ejecuta SQL Server, y cuál hospeda la base de datos del sitio. Especifique el mismo servidor que hospedaba la base de datos del sitio antes de producirse el error.  

-   **Nombre de clave:** DatabaseName  

    -   **Requerido**: sí  

    -   **Valores:** <*nombre de base de datos de sitio*> o <*nombre de instancia*>\\<*nombre de base de datos de sitio*>  

    -   **Detalles:** especifica el nombre de la base de datos de SQL Server que se crea o se usa para instalar la base de datos del sitio de administración central. Especifique el mismo nombre de base de datos que se usó antes de producirse el error.  

        > [!IMPORTANT]  
        >  Si no se usa la instancia predeterminada, se debe especificar el nombre de instancia y el nombre de la base de datos del sitio.  

-   **Nombre de clave:** SQLSSBPort  

    -   **Requerido**: sí  

    -   **Valores:** <*número de puerto SSB*>  

    -   **Detalles:** especifica el puerto SSB que usa SQL Server. Normalmente, SSB está configurado para usar el puerto TCP 4022. Especifique el mismo puerto SSB que se usó antes de producirse el error.  

-   **Nombre de clave:** SQLDataFilePath  

    -   **Requerido** : no  

    -   **Valores:** <*ruta de acceso al archivo .mdb de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .mdb de base de datos.  

-   **Nombre de clave:** SQLLogFilePath  

    -   **Requerido** : no  

    -   **Valores:** <*ruta de acceso al archivo .ldf de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .ldf de base de datos.  

**CloudConnectorOptions**  

-   **Nombre de clave:** CloudConnector  

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si se instala un punto de conexión de servicio en este sitio. Dado que el punto de conexión de servicio solo puede instalarse en el sitio de nivel superior de una jerarquía, este valor debe ser **0** para un sitio principal secundario.  

-   **Nombre de clave:** CloudConnectorServer  

    -   **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1  

    -   **Valores:** <*FQDN del servidor de punto de conexión de servicio*>  

    -   **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio del punto de conexión de servicio.  

-   **Nombre de clave:** UseProxy  

    -   **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si el punto de conexión de servicio usa un servidor proxy.  

-   **Nombre de clave:** ProxyName  

    -   **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1  

    -   **Valores:** <*FQDN del servidor proxy*>  

    -   **Detalles:** especifica el FQDN del servidor proxy que usa el punto de conexión de servicio.  

-   **Nombre de clave:** ProxyPort  

    -   **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1  

    -   **Valores:** <*número de puerto*>  

    -   **Detalles:** especifica el número de puerto que se usará para el puerto de proxy.  

### <a name="unattended-recovery-for-a-primary-site"></a>Recuperación desatendida de un sitio principal  
 Use los datos siguientes para recuperar un sitio primario mediante un archivo de script de instalación desatendida.  

**Identificación**  

-   **Nombre de clave:** Action  

    -   **Requerido**: sí  

    -   **Valores:** <*RecoverPrimarySite*>  

    -   **Detalles:** recupera un sitio primario.  

-   **Nombre de clave:** CDLatest  

    -   **Necesario:** sí, solo cuando se utilizan medios de la carpeta CD.Latest.    

    -   **Valores:** 1 si el valor es distinto de 1, se considera que no se usa CD.Latest.

    -   **Detalles:** el script debe incluir esta clave y valor al ejecutar el programa de instalación desde medios de una carpeta CD.Latest, con el fin de instalar un sitio de administración central o principal, o bien para recuperar estos sitios. Este valor indica al programa de instalación que se están usando medios de la carpeta CD.Latest.    

**RecoveryOptions**  

-   **Nombre de clave:** ServerRecoveryOptions  

    -   **Requerido**: sí  

    -   **Valores** : 1, 2 o 4  

         1 = servidor de sitio de recuperación y SQL Server.  

         2 = recuperar sólo servidor de sitio.  

         4 = recuperar sólo SQL Server.  

    -   **Detalles**: especifica si el programa de instalación recupera el servidor de sitio, SQL Server o ambos. Las claves asociadas son necesarias cuando se establece el siguiente valor para el valor **ServerRecoveryOptions**:  

        -   Valor = 1: tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

        -   Valor = 2: tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

        -   Valor = 4: se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se usa para restaurar la base de datos de sitio desde la copia de seguridad.  

-   **Nombre de clave:** DatabaseRecoveryOptions  

    -   **Obligatorio:** esta clave es obligatoria cuando **ServerRecoveryOptions** tiene un valor de **1** o **4**.  

    -   **Valores:** 10, 20, 40 o 80  

         10 = restaurar la base de datos de sitio desde la copia de seguridad.  

         20 = utilizar una base de datos de sitio que se recuperó manualmente mediante otro método.  

         40 = crear una base de datos nueva para el sitio. Utilice esta opción si no hay ninguna copia de seguridad de base de datos de sitio disponible. Los datos globales y de sitio se recuperan mediante la replicación desde otros sitios.  

         80 = omitir recuperación de base de datos.  

    -   **Detalles:** especifica cómo recupera el programa de instalación la base de datos de sitio en SQL Server.  

-   **Nombre de clave:** SiteServerBackupLocation  

    -   **Requerido** : no  

    -   **Valores:** <*ruta de acceso al conjunto de copia de seguridad de servidor de sitio*>  

    -   **Detalles:**  

         Especifica la ruta de acceso para el conjunto de copia de seguridad del servidor de sitio. Esta clave es opcional si la opción **ServerRecoveryOptions** tiene un valor de **1** o **2**. Especifique un valor para la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

-   **Nombre de clave:** BackupLocation  

    -   **Requerido:** esta clave es necesaria cuando se configura un valor de **1** o **4** para la clave **ServerRecoveryOptions** y cuando se configura un valor de **10** para la clave **DatabaseRecoveryOptions**.  

    -   **Valores:** <*ruta de acceso al conjunto de copia de seguridad de sitio*>  

    -   **Detalles** : especifica la ruta de acceso al conjunto de copia de seguridad de base de datos de sitio.  

**Opciones**  

-   **Nombre de clave:** ProductID  

    -   **Requerido**: sí  

    -   **Valores:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* o *Eval*  

    -   **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones. Escriba **Eval** para instalar la versión de evaluación de Configuration Manager.  

-   **Nombre de clave:** SiteCode  

    -   **Requerido**: sí  

    -   **Valores:** <*código de sitio*>  

    -   **Detalles:** especifica tres caracteres alfanuméricos que identifican al sitio de forma única en la jerarquía. Especifique el código de sitio que usó el sitio antes de producirse el error.

-   **Nombre de clave:** SiteName  

    -   **Requerido** : no  

    -   **Valores:** <*nombre de sitio*>  

    -   **Detalles:** especifica el nombre de este sitio.  

-   **Nombre de clave:** SMSInstallDir  

    -   **Requerido**: sí  

    -   **Valores:** <*ruta de instalación de Configuration Manager*>  

    -   **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.  

-   **Nombre de clave:** SDKServer  

    -   **Requerido**: sí  

    -   **Valores:** <*FQDN del proveedor de SMS*>  

    -   **Detalles:** especifica el FQDN del servidor que hospeda el proveedor de SMS. Especifique el servidor que hospedaba el proveedor de SMS antes de producirse el error. Configure proveedores de SMS adicionales para el sitio después de la instalación inicial. Para obtener más información sobre el proveedor de SMS, vea [Plan para el proveedor de SMS](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nombre de clave:**: PrerequisiteComp  

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = descargar  

         1 = ya se ha descargado  

    -   **Detalles:** especifica si ya se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si usa un valor de **0**, el programa de instalación descarga los archivos.  

-   **Nombre de clave:** PrerequisitePath  

    -   **Requerido**: sí  

    -   **Valores:** <*ruta de acceso a los archivos de requisitos previos de instalación*>  

    -   **Detalles:** especifica la ruta de acceso a los archivos de requisitos previos de instalación. En función del valor **PrerequisiteComp**, el programa de instalación usa esta ruta de acceso para almacenar los archivos descargados o localizar los archivos descargados previamente.  

-   **Nombre de clave:** AdminConsole  

    -   **Requerido:** esta clave es necesaria, excepto cuando **ServerRecoveryOptions** tiene un valor de **4**.  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si se va a instalar la consola de Configuration Manager.  

-   **Nombre de clave:** JoinCEIP  
    > [!Note]  
    > A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto.

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = no unir  

         1 = unir  

    -   **Detalles:**: especifica si se unirá al CEIP.  

**SQLConfigOptions**  

-   **Nombre de clave:** SQLServerName  

    -   **Requerido**: sí  

    -   **Valores:** <*nombre de servidor SQL*>  

    -   **Detalles:** especifica el nombre del servidor o de la instancia en clúster que ejecuta SQL Server, y cuál hospeda la base de datos del sitio. Especifique el mismo servidor que hospedaba la base de datos del sitio antes de producirse el error.  

-   **Nombre de clave:** DatabaseName  

    -   **Requerido**: sí  

    -   **Valores:** <*nombre de base de datos de sitio*> o <*nombre de instancia*>\\<*nombre de base de datos de sitio*>

    -   **Detalles:**  

         especifica el nombre de la base de datos de SQL Server que se crea o se usa para instalar la base de datos del sitio de administración central. Especifique el mismo nombre de base de datos que se usó antes de producirse el error.  

        > [!IMPORTANT]  
        >  Si no se usa la instancia predeterminada, se debe especificar el nombre de instancia y el nombre de la base de datos del sitio.  

-   **Nombre de clave:** SQLSSBPort  

    -   **Requerido**: sí  

    -   **Valores:** <*número de puerto SSB*>  

    -   **Detalles:** especifica el puerto SSB que usa SQL Server. Normalmente, SSB está configurado para usar el puerto TCP 4022. Especifique el mismo puerto SSB que se usó antes de producirse el error.  

-   **Nombre de clave:** SQLDataFilePath  

    -   **Requerido** : no  

    -   **Valores:** <*ruta de acceso al archivo .mdb de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .mdb de base de datos.  

-   **Nombre de clave:** SQLLogFilePath  

    -   **Requerido** : no  

    -   **Valores:** <*ruta de acceso al archivo .ldf de base de datos*>  

    -   **Detalles:** especifica una ubicación alternativa para crear el archivo .ldf de base de datos.  

**HierarchyExpansionOptions**  

-   **Nombre de clave:** CCARSiteServer  

    -   **Requerido:** ver detalles.  

    -   **Valores:** <*código de sitio para el sitio de administración central*>  

    -   **Detalles:** especifica el sitio de administración central al que se asocia un sitio primario cuando se une a la jerarquía de Configuration Manager. Esta configuración es necesaria si el sitio primario estaba asociado con un sitio de administración central antes de producirse el error. Especifique el código de sitio que se usó para el sitio de administración central antes de que se produjera el error.  

-   **Nombre de clave:** CASRetryInterval  

    -   **Requerido** : no  

    -   **Valores:** <*Interval*>  

    -   **Detalles** : especifica el intervalo de reintento (en minutos) para tratar de establecer una conexión con el sitio de administración central después de que la conexión genera un error. Por ejemplo, si se produce un error en la conexión al sitio de administración central, el sitio primario espera el número de minutos especificado para el valor **CASRetryInterval** y, después, vuelve a intentar la conexión.  

-   **Nombre de clave:** WaitForCASTimeout  

    -   **Requerido** : no  

    -   **Valores:** <*Tiempo de espera*>  

    -   **Detalles** : especifica el valor de tiempo de espera máximo (en minutos) de un sitio primario para conectarse al sitio de administración central. Por ejemplo, si se produce un error de conexión del sitio primario con el sitio de administración central, el sitio primario vuelve a tratar de establecer la conexión conforme al valor **CASRetryInterval** hasta que se alcanza el valor de tiempo de **WaitForCASTimeout**. Puede especificar un valor de **0** a **100**.  

**CloudConnectorOptions**  

-   **Nombre de clave:** CloudConnector  

    -   **Requerido**: sí  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si se instala un punto de conexión de servicio en este sitio. Dado que el punto de conexión de servicio solo puede instalarse en el sitio de nivel superior de una jerarquía, este valor debe ser **0** para un sitio principal secundario.  

-   **Nombre de clave:** CloudConnectorServer  

    -   **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1  

    -   **Valores:** <*FQDN del servidor de punto de conexión de servicio*>  

    -   **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio del punto de conexión de servicio.  

-   **Nombre de clave:** UseProxy  

    -   **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1  

    -   **Valores** : 0 o 1  

         0 = no instalar  

         1 = instalar  

    -   **Detalles:** especifica si el punto de conexión de servicio usa un servidor proxy.  

-   **Nombre de clave:** ProxyName  

    -   **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1  

    -   **Valores:** <*FQDN del servidor proxy*>  

    -   **Detalles:** especifica el FQDN del servidor proxy que usa el punto de conexión de servicio.  

-   **Nombre de clave:** ProxyPort  

    -   **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1  

    -   **Valores:** <*número de puerto*>  

    -   **Detalles:** especifica el número de puerto que se usará para el puerto de proxy.  
