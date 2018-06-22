---
title: Configuración de informes
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo configurar la generación de informes en la jerarquía de Configuration Manager, incluida información sobre SQL Server Reporting Services.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 17b0147e82e2eb9a756bdab69eed7ab86f98a1e0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32344303"
---
# <a name="configuring-reporting-in-system-center-configuration-manager"></a>Configuración de informes en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Para crear, modificar y ejecutar informes en la consola de System Center Configuration Manager, debe realizar varias tareas de configuración. Use las siguientes secciones de este tema como guía para configurar la generación de informes en la jerarquía de Configuration Manager:  

 Antes de proceder con la instalación y la configuración de Reporting Services en la jerarquía, lea los siguientes temas dedicados a la generación de informes de Configuration Manager:  

-   [Introduction to reporting in System Center Configuration Manager (Introducción a la generación de informes en System Center Configuration Manager)](../../../core/servers/manage/introduction-to-reporting.md)  

-   [Planeación de informes en System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md)  

##  <a name="BKMK_SQLReportingServices"></a> SQL Server Reporting Services  
 SQL Server Reporting Services es una plataforma de informes basada en servidor que proporciona exhaustivas funciones de informes para una amplia variedad de orígenes de datos. El punto de servicios de informes de Configuration Manager se comunica con SQL Server Reporting Services para copiar informes de Configuration Manager en una carpeta de informes especificada, para configurar Reporting Services y la seguridad de Reporting Services. Reporting Services se conecta con la base de datos del sitio de Configuration Manager para recuperar datos que se devuelven cuando se ejecutan informes.  

 Para poder instalar el punto de servicios de informes en un sitio de Configuration Manager, debe instalar y configurar SQL Server Reporting Services en el sistema de sitio que hospeda el rol del sistema de sitio del punto de servicios de informes. Para obtener más información acerca de la instalación de Reporting Services, consulte la [biblioteca de TechNet de SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=266389).  

 Utilice el procedimiento siguiente para comprobar que SQL Server Reporting Services está instalado y se ejecuta correctamente.  

#### <a name="to-verify-that-sql-server-reporting-services-is-installed-and-running"></a>Para comprobar que SQL Server Reporting Services está instalado y en ejecución  

1.  En el escritorio, haga clic en **Inicio**, haga clic en **Todos los programas**, en **Microsoft SQL Server 2008 R2**, **Herramientas de configuración**y, a continuación, haga clic en **Reporting Services Configuration Manager**.  

2.  En el cuadro de diálogo **Conexión de configuración de Reporting Services** , especifique el nombre del servidor que hospeda SQL Server Reporting Services. En el menú, seleccione la instancia de SQL Server en la que está instalada SQL Reporting Services y, a continuación, haga clic en **Conectar**. Se abre Reporting Services Configuration Manager.  

3.  En la página **Estado del servidor de informes** , compruebe que **Estado del servidor de informes** está configurado en **Iniciado**. Si no lo está, haga clic en **Iniciar**.  

4.  En la página **Dirección URL del servicio web** , haga clic en la dirección URL de **Direcciones URL del servicio web de del servicio de informes** para probar la conexión con la carpeta de informes. El cuadro de diálogo **Seguridad de Windows** podría abrirse y solicitarle las credenciales de seguridad. De forma predeterminada, se muestra la cuenta de usuario. Escriba la contraseña y haga clic en **Aceptar**. Compruebe que la página web se abre correctamente. Cierre la ventana del explorador.  

5.  En la página **Base de datos** , compruebe que la opción **Modo del servidor de informes** está configurada con **Nativo**.  

6.  En la página **URL de administrador de informes** , haga clic en la dirección URL en **Identificación del sitio del Administrador de informes** para probar la conexión con el directorio virtual para el Administrador de informes. El cuadro de diálogo **Seguridad de Windows** podría abrirse y solicitarle las credenciales de seguridad. De forma predeterminada, se muestra la cuenta de usuario. Escriba la contraseña y haga clic en **Aceptar**. Compruebe que la página web se abre correctamente. Cierre la ventana del explorador.  

    > [!NOTE]  
    >  El Administrador de informes de Reporting Services no es necesario para la generación de informes en Configuration Manager, pero sí si quiere ejecutar informes en un explorador web o usar el Administrador de informes para administrar informes.  

7.  Haga clic en **Salir** para cerrar el Administrador de configuración de Reporting Services.  

##  <a name="BKMK_ReportBuilder3"></a> Configuración de informes para usar el Generador de informes 3.0  

#### <a name="to-change-the-report-builder-manifest-name-to-report-builder-30"></a>Para cambiar el nombre de manifiesto de Report Builder a Report Builder 3.0  

1.  En el equipo que ejecuta la consola de Configuration Manager, abra el editor del Registro de Windows.  

2.  Navegue a **HKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Microsoft/ConfigMgr10/AdminUI/Reporting**.  

3.  Haga doble clic en la clave **ReportBuilderApplicationManifestName** para editar los datos del valor.  

4.  Cambie **ReportBuilder_2_0_0_0.application** a **ReportBuilder_3_0_0_0.application**y, a continuación, haga clic en **Aceptar**.  

5.  Cierre el editor del Registro de Windows.  

##  <a name="BKMK_InstallReportingServicesPoint"></a> Instalar un punto de servicios de informes  
 Para administrar informes en un sitio, el punto de servicios de informes debe estar instalado en el sitio. El punto de servicios de informes copia las carpetas de informes, notifica a SQL Server Reporting Services, aplica la directiva de seguridad para informes y carpetas, y configura las opciones de Reporting Services. Para que la consola de Configuration Manager muestre informes y poder administrarlos en Configuration Manager, debe configurar el punto de servicios de informes. El punto de servicios de informes es un rol de sistema de sitio que se debe configurar en un servidor que tenga Microsoft SQL Server Reporting Services instalado y en ejecución. Para más información sobre los requisitos previos, vea [Prerequisites for reporting (Requisitos previos para la generación de informes)](prerequisites-for-reporting.md).  

> [!IMPORTANT]  
>  Cuando selecciona un sitio para instalar el punto de servicios de informes, tenga en cuenta que los usuarios que accederán a los informes deben estar en el mismo ámbito de seguridad que el sitio en el se instala el punto de servicios de informes.  

> [!NOTE]  
>  Una vez instalado un punto de servicios de informes en un sistema de sitio, no cambie la dirección URL del servidor de informes. Por ejemplo, si crea el punto de servicios de informes y, luego, en el Administrador de configuración de Reporting Services modifica la dirección URL del servidor de informes, la consola de Configuration Manager seguirá usando la dirección URL anterior y no podrá ejecutar, editar ni crear informes desde la consola. Cuando tenga que cambiar la dirección URL del servidor de informes, quite el punto de servicios de informes, cambie la dirección URL y, a continuación, reinstale el punto de servicios de informes.  

> [!IMPORTANT]    
> Cuando se instala un punto de servicios de informes, debe especificar una cuenta para el punto de servicios de informes. Más adelante, cuando los usuarios de un dominio distinto intenten ejecutar un informe, este dará error a menos que haya una confianza bidireccional establecida entre los dominios.

 Utilice el siguiente procedimiento para instalar el punto de servicios de informes.  

#### <a name="to-install-the-reporting-services-point-on-a-site-system"></a>Para instalar el punto de servicios de informes en un sistema de sitio  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Servidores y roles del sistema de sitios**.  

    > [!TIP]  
    >  Para que aparezcan solo los sistemas de sitio que hospedan el rol de sitio de punto de servicios de informes, haga clic con el botón secundario en **Servidores y roles del sistema de sitios** para seleccionar el **Punto de servicios de informes**.  

3.  Agregue el rol de sistema de sitio del punto de servicios de informes a un servidor de sistema de sitio nuevo o existente mediante el paso asociado:  

    > [!NOTE]  
    >  Para más información sobre la configuración de sistemas de sitio, vea [Agregar roles de sistema de sitio para System Center Configuration Manager](../deploy/configure/add-site-system-roles.md).  

    -   **Nuevo sistema de sitio**: en la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear servidor de sistema de sitio**. Se abre el **Asistente para crear servidor de sistema de sitio** .  

    -   **Sistema de sitio existente**: haga clic en el servidor en el que desea instalar el rol de sistema de sitio del punto de servicios de informes. Al hacer clic en un servidor, se muestra en el panel de resultados una lista de los roles de sistema de sitio que ya están instalados en el servidor.  

         En la pestaña **Inicio** , en el grupo **Servidor** , haga clic en **Agregar rol de sistema de sitio**. Se abre el **Asistente para agregar roles de sistema de sitio** .  

4.  En la página **General** , especifique la configuración general para el servidor de sistema de sitio. Cuando se agrega el punto de servicios de informes a un servidor de sistema de sitio existente, compruebe los valores que se habían configurado previamente.  

5.  En la página **Selección de rol del sistema** , seleccione **Punto de servicios de informes** en la lista de roles disponibles y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Punto de servicios de informes** , configure las siguientes opciones:  

    -   **Nombre de servidor de base de datos del sitio**: especifique el nombre del servidor que hospeda la base de datos del sitio de Configuration Manager. Normalmente, el asistente recupera automáticamente el nombre de dominio completo (FQDN) del servidor. Para especificar una instancia de base de datos, use el formato &lt;*Nombre de servidor*>\&lt;*Nombre de instancia*>.  

    -   **Nombre de base de datos**: especifique el nombre de base de datos del sitio de Configuration Manager y, luego, haga clic en **Comprobar** para confirmar que el asistente tiene acceso a la base de datos del sitio.  

        > [!IMPORTANT]  
        >  La cuenta de usuario que crea el punto de servicios de informes debe tener acceso de **lectura** a la base de datos del sitio. Si se produce un error en la prueba de conexión, aparecerá un icono de advertencia rojo. Mueva el cursor sobre este icono para leer los detalles del error. Corrija el error y, a continuación, haga clic en **Prueba** otra vez.  

    -   **Nombre de la carpeta**: especifique el nombre de la carpeta que se crea y se usa para hospedar los informes de Configuration Manager en Reporting Services.  

    -   **Instancia del servidor de Reporting Services**: seleccione en la lista la instancia de SQL Server para Reporting Services. Si hay una sola instancia, aparecerá seleccionada de forma predeterminada. Cuando no se encuentran instancias, compruebe que SQL Server Reporting Services está instalado y configurado, y que se inició el servicio de SQL Server Reporting Services en el sistema de sitio.  

        > [!IMPORTANT]  
        >  Configuration Manager hace una conexión en el contexto del usuario actual con Instrumental de administración de Windows (WMI) en el sistema de sitio seleccionado para recuperar la instancia de SQL Server para Reporting Services. El usuario actual debe tener acceso de **lectura** a WMI en el sistema de sitio; de lo contrario, no se podrán recuperar las instancias de Reporting Services.  

    -   **Cuenta de punto de Reporting Services**: haga clic en **Establecer** y seleccione una cuenta que se use cuando SQL Server Reporting Services en el punto de servicios de informes se conecte con la base de datos del sitio de Configuration Manager para recuperar los datos que se muestran en un informe. Seleccione **Cuenta existente** para especificar una cuenta de usuario de Windows configurada previamente como cuenta de Configuration Manager o seleccione **Nueva cuenta** para especificar una cuenta de usuario de Windows que no esté configurada actualmente como una cuenta de Configuration Manager. Configuration Manager concede automáticamente acceso al usuario especificado a la base de datos del sitio. El usuario se muestra en la subcarpeta **Cuentas** del nodo **Seguridad** en el área de trabajo **Administración** con el nombre de cuenta **Punto de servicios de informes de ConfigMgr** .  

         La cuenta que ejecuta Reporting Services debe pertenecer al grupo de seguridad local de dominio **Grupo de acceso de autorización de Windows**y tener el permiso **Lectura tokenGroupsGlobalAndUniversal** configurado como **Permitir**. Debe existir una relación de confianza bidireccional establecida para los usuarios de un dominio distinto al de la cuenta de punto de Reporting Services para la correcta ejecución de los informes.

         La cuenta de usuario de Windows especificada y la contraseña se cifran, y se almacenan en la base de datos de Reporting Services. Reporting Services recupera los datos de los informes de la base de datos del sitio mediante el uso de esta cuenta y contraseña.  

        > [!IMPORTANT]  
        >  La cuenta que especifique debe tener permisos de **Inicio de sesión local** en el equipo que hospeda la base de datos de Reporting Services.  

7.  En la página **Punto de Reporting Services** , haga clic en **Siguiente**.  

8.  En la página **Resumen** , compruebe la configuración y, a continuación, haga clic en **Siguiente** para instalar el punto de servicios de informes.  

     Una vez completado el asistente, se crean las carpetas de informes y los informes de Configuration Manager se copian en las carpetas de informes especificadas.  

    > [!NOTE]  
    >  Cuando se crean las carpetas de informes y los informes se copian en el servidor de informes, Configuration Manager determina el idioma apropiado para los objetos. Si el paquete de idioma asociado está instalado en el sitio, Configuration Manager crea los objetos en el mismo idioma que el sistema operativo que se ejecuta en el servidor de informes del sitio. Si el idioma no está disponible, los informes se crean y se muestran en inglés. Cuando se instala un punto de servicios de informes en un sitio sin paquetes de idioma, los informes se instalan en inglés. Si instala un paquete de idioma tras instalar el punto de servicios de informes, debe desinstalar y reinstalar el punto de servicios de informes para que los informes estén disponibles en el idioma del paquete de idioma apropiado. Para más información sobre los paquetes de idioma, vea [Language Packs in System Center Configuration Manager (Paquetes de idioma en System Center Configuration Manager)](../deploy/install/language-packs.md).  

###  <a name="BKMK_FileInstallationAndSecurity"></a> Derechos de seguridad de carpeta de informes e instalación de archivos  
 Configuration Manager realiza las acciones siguientes para instalar el punto de servicios de informes y configurar Reporting Services:  

> [!IMPORTANT]  
>  Las acciones incluidas en la siguiente lista se realizan mediante las credenciales de la cuenta que está configurada para el servicio SMS_Executive, que suele ser la cuenta de sistema local del servidor de sitio.  

-   Instala el rol de sitio del punto de servicios de informes.  

-   Crea el origen de datos en Reporting Services con las credenciales almacenadas que se especificó en el asistente. Esta es la contraseña y la cuenta de usuario de Windows que utiliza Reporting Services para conectarse con la base de datos del sitio cuando ejecutan informes.  

-   Crea la carpeta raíz de Configuration Manager en Reporting Services.  

-   Agrega los roles de seguridad **Usuarios de informes de Configuration Manager** y **Administradores de informes de Configuration Manager** en Reporting Services.  

-   Crea subcarpetas e implementa informes de Configuration Manager desde %ArchivosDePrograma%\SMS_SRSRP en Reporting Services.  

-   Agrega el rol **Usuarios de informes de Configuration Manager** de Reporting Services a las carpetas raíz para todas las cuentas de usuario de Configuration Manager que tengan derechos de **lectura del sitio**.  

-   Agrega el rol **Administradores de informes de Configuration Manager** de Reporting Services a las carpetas raíz para todas las cuentas de usuario de Configuration Manager que tengan derechos de **modificación del sitio**.  

-   Recupera la asignación entre las carpetas de informes y los tipos de objetos protegidos de Configuration Manager (que se mantienen en la base de datos del sitio de Configuration Manager).  

-   Configura los siguientes derechos para los usuarios administrativos de Configuration Manager en carpetas de informes específicas de Reporting Services:  

    -   Agrega usuarios y asigna el rol **Usuarios de informes de Configuration Manager** a la carpeta de informes asociada para los usuarios administrativos que tengan permisos **Ejecutar informe** para el objeto de Configuration Manager.  

    -   Agrega usuarios y asigna el rol **Administradores de informes de Configuration Manager** a la carpeta de informes asociada para los usuarios administrativos que tengan permisos **Modificar informe** para el objeto de Configuration Manager.  

     Configuration Manager se conecta a Reporting Services y establece los permisos para los usuarios en las carpetas raíz de Configuration Manager y Reporting Services, y en carpetas de informes específicas. Tras la instalación inicial del punto de servicios de informes, Configuration Manager se conecta a Reporting Services en un intervalo de 10 minutos para comprobar que los derechos de usuario configurados en las carpetas de informes son los derechos asociados que están establecidos para los usuarios de Configuration Manager. Cuando se agregan usuarios o se modifican derechos de usuario en la carpeta de informes mediante el uso del Administrador de informes de Reporting Services, Configuration Manager sobrescribe estos cambios por medio del uso de asignaciones basadas en roles almacenadas en la base de datos del sitio. Configuration Manager también quita los usuarios que no tienen derechos de generación de informes en Configuration Manager.  

##  <a name="BKMK_SecurityRoles"></a> Roles de seguridad de Reporting Services para Configuration Manager  
 Cuando Configuration Manager instala el punto de servicios de informes, se agregan los siguientes roles de seguridad en Reporting Services:  

-   **Usuarios de informes de Configuration Manager**: los usuarios a los que se les asigna este rol de seguridad solo pueden ejecutar informes de Configuration Manager.  

-   **Administradores de informes de Configuration Manager**: los usuarios a los que se les asigna este rol de seguridad pueden realizar todas las tareas relacionadas con la generación de informes en Configuration Manager.  

##  <a name="BKMK_VerifyReportingServicesPointInstallation"></a> Comprobación de la instalación del punto de Reporting Services  
 Tras agregar el rol de sitio de punto de servicios de informes, puede comprobar la instalación mediante la visualización de entradas del archivo de registro y mensajes de estado específicos. Utilice el siguiente procedimiento para comprobar que la instalación del punto de servicios de informes se realizó correctamente.  

> [!WARNING]  
>  Puede omitir este procedimiento si los informes se muestran en la subcarpeta **Informes** del nodo **Informes** del área de trabajo **Supervisión** de la consola de Configuration Manager.  

#### <a name="to-verify-the-reporting-services-point-installation"></a>Para comprobar la instalación del punto de servicios de informes  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Estado del sistema**y, a continuación, haga clic en **Estado del componente**.  

3.  Haga clic en **SMS_SRS_REPORTING_POINT** en la lista de componentes.  

4.  En la pestaña **Inicio** , en el grupo **Componente** , haga clic en **Mostrar mensajes**y, a continuación, haga clic en **Todos**.  

5.  Especifique una fecha y una hora para un período anterior a la instalación del punto de servicios de informes y, a continuación, haga clic en **Aceptar**.  

6.  Compruebe que aparece el identificador de mensaje de estado 1015, que indica que el punto de servicios de informes se instaló correctamente. Si quiere, puede abrir el archivo Srsrp.log, que se encuentra en &lt;*Ruta de instalación de ConfigMgr*>\Logs, y buscar **Se completó la instalación**.  

     En el Explorador de Windows, vaya a &lt;*Ruta de instalación de ConfigMgr*>\Logs.  

7.  Abra Srsrp.log y lea el archivo de registro a partir de la hora en la que se instaló correctamente el punto de servicios de informes. Compruebe que se crearon las carpetas de informes, se implementaron los informes, y se confirmó la directiva de seguridad en todas las carpetas. Busque **Se comprobó correctamente que el servicio SRS es correcto en el servidor** después de la última línea de las confirmaciones de la directiva de seguridad.  

##  <a name="BKMK_Certificate"></a> Configuración de un certificado autofirmado para los equipos de la consola de Configuration Manager  
 Existen muchas opciones para crear informes de SQL Server Reporting Services. Cuando se crean o editan informes en la consola de Configuration Manager, Configuration Manager abre el Generador de informes para usarlo como entorno de creación. Independientemente de cómo cree los informes de Configuration Manager, un certificado autofirmado es necesario para la autenticación del servidor en el servidor de base de datos del sitio. Configuration Manager instala automáticamente el certificado en el servidor de sitio y los equipos con el proveedor de SMS instalado. Por lo tanto, puede crear o modificar informes desde la consola de Configuration Manager cuando esta se ejecuta desde uno de estos equipos. Pero cuando sea crean o modifican informes desde una consola de Configuration Manager que está instalada en un equipo distinto, debe exportar el certificado del servidor del sitio y, luego, agregarlo al almacén de certificados **Personas de confianza** en el equipo que ejecuta la consola de Configuration Manager.  

> [!NOTE]  
>  Para obtener más información acerca de otros entornos de creación de informes para SQL Server Reporting Services, consulte [Comparar los entornos de creación de informes](http://go.microsoft.com/fwlink/p/?LinkId=242805) en Libros en pantalla de SQL Server 2008.  

 Use el siguiente procedimiento como ejemplo de cómo transferir una copia del certificado autofirmado desde el servidor del sitio a otro equipo que ejecuta la consola de Configuration Manager cuando ambos equipos usan Windows Server 2008 R2. Si no puede seguir este procedimiento porque tiene una versión de sistema operativo diferente, consulte la documentación de su sistema operativo para ver el procedimiento equivalente.  

#### <a name="to-transfer-a-copy-of-self-signed-certificate-from-the-site-server-to-another-computer"></a>Para transferir una copia de un certificado autofirmado desde el servidor del sitio a otro equipo  

1.  Realice los siguientes pasos en el servidor del sitio para exportar el certificado autofirmado:  

    1.  Haga clic en **Inicio**y en **Ejecutar**, y escriba **mmc.exe**. En la consola vacía, haga clic en **Archivo**y, a continuación, haga clic en **Agregar o quitar complemento**.  

    2.  En el cuadro de diálogo **Agregar o quitar complementos** , seleccione **Certificados** en la lista de **Complementos disponibles**y, a continuación, haga clic en **Agregar**.  

    3.  En el cuadro de diálogo **Complemento Certificado** , seleccione **Cuenta de equipo**y, a continuación, haga clic en **Siguiente**.  

    4.  En el cuadro de diálogo **Seleccionar equipo** , asegúrese de que está seleccionado **Equipo local: (el equipo en el que se está ejecutando esta consola)** y, a continuación, haga clic en **Finalizar**.  

    5.  En el cuadro de diálogo **Agregar o quitar complementos** , haga clic en **Aceptar**.  

    6.  En la consola, expanda **Certificados (equipo local)**, expanda **Personas de confianza**y seleccione **Certificados**.  

    7.  Haga clic con el botón derecho en el certificado con el nombre descriptivo de &lt;*FQDN del servidor del sitio*>, haga clic en **Todas las tareas** y luego seleccione **Exportar**.  

    8.  Complete el **Asistente para exportación de certificados** con las opciones predeterminadas y guarde el certificado con la extensión de nombre de archivo **.cer** .  

2.  Realice los siguientes pasos en el equipo que ejecuta la consola de Configuration Manager para agregar el certificado autofirmado al almacén de certificados Personas de confianza:  

    1.  Repita que los pasos anteriores del 1.a al 1.e para configurar el MMC del complemento **Certificado** en el equipo de punto de administración.  

    2.  En la consola, expanda **Certificados (equipo local)**, expanda **Personas de confianza**, haga clic con el botón secundario en **Certificados**, seleccione **Todas las tareas**y, a continuación, seleccione **Importar** para iniciar el **Asistente para importación de certificados**.  

    3.  En la página **Archivo para importar** , seleccione el certificado que guardó en el paso 1.h y, a continuación, haga clic en **Siguiente**.  

    4.  En la página **Almacén de certificados** , seleccione **Colocar todos los certificados en el siguiente almacén**, con el **Almacén de certificados** establecido en **Personas de confianza**y, a continuación, haga clic en **Siguiente**.  

    5.  Haga clic en **Finalizar** para cerrar el asistente y finalizar la configuración del certificado en el equipo.  

##  <a name="BKMK_ModifyReportingServicesPoint"></a> Modificación de la configuración del punto de servicios de informes  
 Una vez instalado el punto de servicios de informes, puede modificar la conexión de base de datos del sitio y la configuración de autenticación en las propiedades del punto de servicios de informes. Utilice el siguiente procedimiento para modificar la configuración del punto de servicios de informes.  

#### <a name="to-modify-reporting-services-point-settings"></a>Para modificar la configuración del punto de servicios de informes  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Servidores y roles del sistema de sitios** para que aparezcan los sistemas de sitio.  

    > [!TIP]  
    >  Para que aparezcan solo los sistemas de sitio que hospedan el rol de sitio de punto de servicios de informes, haga clic con el botón secundario en **Servidores y roles del sistema de sitios** para seleccionar el **Punto de servicios de informes**.  

3.  Seleccione el sistema de sitio que hospeda el punto de servicios de informes en el que desea modificar la configuración y, a continuación, seleccione **Punto de servicios de informes** en **Roles del sistema de sitios**.  

4.  En la pestaña **Rol del sitio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5.  En el cuadro de diálogo **Propiedades de punto de servicios de informes** , puede modificar las siguientes opciones:  

    -   **Nombre de servidor de base de datos del sitio**: especifique el nombre del servidor que hospeda la base de datos del sitio de Configuration Manager. Normalmente, el asistente recupera automáticamente el nombre de dominio completo (FQDN) del servidor. Para especificar una instancia de base de datos, use el formato &lt;*Nombre de servidor*>\&lt;*Nombre de instancia*>.  

    -   **Nombre de base de datos**: especifique el nombre de base de datos del sitio de System Center 2012 Configuration Manager y, luego, haga clic en **Comprobar** para confirmar que el asistente tiene acceso a la base de datos del sitio.  

        > [!IMPORTANT]  
        >  La cuenta de usuario que crea el punto de servicios de informes debe tener acceso de lectura a la base de datos del sitio. Si se produce un error en la prueba de conexión, aparecerá un icono de advertencia rojo. Mueva el cursor sobre este icono para leer los detalles del error. Corrija el error y, a continuación, haga clic en **Prueba** otra vez.  

    -   **Cuenta de usuario**: haga clic en **Establecer** y luego seleccione una cuenta que se use cuando SQL Server Reporting Services en el punto de servicios de informes se conecte con la base de datos del sitio de Configuration Manager para recuperar los datos que se muestran en un informe. Seleccione **Cuenta existente** para especificar una cuenta de usuario de Windows con derechos de Configuration Manager existentes o seleccione **Nueva cuenta** para especificar una cuenta de usuario de Windows actualmente sin derechos en Configuration Manager. Configuration Manager concede automáticamente acceso a la cuenta de usuario especificada a la base de datos del sitio. La cuenta se muestra como la cuenta del **Punto de informes de SRS de Configuration Manager** en la subcarpeta **Cuentas** del nodo **Seguridad** en el área de trabajo **Administración** .  

         La cuenta de usuario de Windows especificada y la contraseña se cifran, y se almacenan en la base de datos de Reporting Services. Reporting Services recupera los datos de los informes de la base de datos del sitio mediante el uso de esta cuenta y contraseña.  

        > [!IMPORTANT]  
        >  Cuando la base de datos del sitio se encuentra en un sistema de sitio remoto, la cuenta que especifica debe tener el permiso **Inicio de sesión local** para el equipo.  

6.  Haga clic en **Aceptar** para guardar los cambios y salir del cuadro de diálogo.  

## <a name="upgrading-sql-server"></a>Actualización de SQL Server  
 Tras actualizar SQL Server, y el servicio SQL Server Reporting Services que se usa como el origen de datos de un punto de servicios de informes, podría experimentar errores al ejecutar o editar informes desde la consola de Configuration Manager. Para que la generación de informes funcione correctamente en la consola de Configuration Manager, debe eliminar el rol de sistema de sitio de punto de servicios de informes para el sitio y volver a instalarlo. Sin embargo, tras la actualización puede continuar con la ejecución y edición de informes desde un explorador de Internet.  

##  <a name="BKMK_ConfigureReportOptions"></a> Configuración de las opciones de informes  
 Use las opciones de informes de un sitio de Configuration Manager para seleccionar el punto de servicios de informes predeterminado que se usa para administrar los informes. Aunque puede haber más de un punto de servicios de informes en un sitio, solo el servidor de informes predeterminado seleccionado en Opciones de informes se utiliza para administrar los informes. Utilice el siguiente procedimiento para configurar las opciones de informes para su sitio.  

#### <a name="to-configure-report-options"></a>Para configurar las opciones de informes  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Generación de informes**y, a continuación, haga clic en **Informes**.  

3.  En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Opciones de informes**.  

4.  Seleccione el servidor de informes predeterminado en la lista y, a continuación, haga clic en **Aceptar**. Si no aparecen puntos de servicios de informes en la lista, compruebe que tiene un punto de servicios de informes correctamente instalado y configurado en el sitio.  

## <a name="next-steps"></a>Pasos siguientes
[Operaciones y mantenimiento de informes](operations-and-maintenance-for-reporting.md)
