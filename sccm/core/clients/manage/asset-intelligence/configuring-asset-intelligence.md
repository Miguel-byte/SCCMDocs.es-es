---
title: Configurar Asset Intelligence | System Center Configuration Manager
description: Configure Asset Intelligence en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 43e04a447b03885286c6c7201afb4d1b7a10aa91


---
# <a name="configure-asset-intelligence-in-system-center-configuration-manager"></a>Configurar Asset Intelligence en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Para usar Asset Intelligence en System Center Configuration Manager con el fin de inventariar y administrar el uso de licencias de software en la empresa, primero tiene que realizar una serie de pasos de configuración.  

## <a name="steps-to-configure-asset-intelligence"></a>Pasos para configurar Asset Intelligence  
 Para recopilar los datos de inventario necesarios para los informes de Asset Intelligence, el Agente cliente de inventario de hardware debe estar habilitado. Para más información sobre cómo habilitar el Agente cliente de inventario de hardware, vea [Cómo ampliar el inventario de Hardware en Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

|Paso|Detalles|Más información|  
|----------|-------------|----------------------|  
|**Paso 1**: habilitar las clases de informes de inventario de hardware de Asset Intelligence|La recopilación de información de Asset Intelligence no se habilita si Configuration Manager se instala primero. Para habilitar Asset Intelligence, al menos una de las clases de informes de inventario de hardware necesarias de las que dependen los informes de Asset Intelligence debe estar habilitada.|Para más información, consulte el procedimiento siguiente de este tema: [Enable Asset Intelligence hardware inventory reporting classes](#BKMK_EnableAssetIntelligence).|  
|**Paso 2**: instalar un punto de sincronización de Asset Intelligence|El rol de sistema de sitio de punto de sincronización de Asset Intelligence se usa para conectar sitios de Configuration Manager con System Center Online para sincronizar la información del catálogo de Asset Intelligence. El punto de sincronización de Asset Intelligence solo puede instalarse en un sistema de sitio que se encuentre en el sitio de nivel superior de la jerarquía de Configuration Manager y necesita acceso a Internet para sincronizarse con System Center Online mediante el puerto TCP 443.<br /><br /> Además de descargar la nueva información del catálogo Asset Intelligence, el punto de sincronización de Asset Intelligence puede cargar la información de títulos de software personalizado en System Center Online para su categorización. Microsoft trata todos los títulos de software cargados en System Center Online para su categorización como información pública. Por lo tanto, debe asegurarse de que los títulos de software personalizado no contienen información confidencial o de propiedad. Para más información sobre las solicitudes de categorización de títulos de software, vea [Solicitar una actualización del catálogo para títulos de software sin categoría](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).|Para más información, consulte el procedimiento siguiente de este tema: [Install an Asset Intelligence Synchronization Point](#BKMK_InstallAssetIntelligenceSynchronizationPoint).|  
|**Paso 3**: habilitar la auditoría de eventos de inicio de sesión correctos|Cuatro informes de Asset Intelligence muestran información recopilada de los registros de eventos de seguridad de Windows en los equipos cliente. Si la configuración del registro de eventos de seguridad no está establecida para registrar todos los eventos de inicio de sesión correctos, estos informes no contienen datos incluso aunque se haya habilitado la clase de informes de inventario de hardware correspondiente. Para habilitar el Agente cliente de inventario de hardware a fin de inventariar la información necesaria para admitir estos informes, primero se debe modificar la configuración de registro de eventos de seguridad de Windows en los clientes para que registren todos los eventos de inicio de sesión correctos y habiliten la clase de notificación de inventario de hardware **SMS_SystemConsoleUser** .|Para más información, consulte los procedimientos siguientes de este tema: [Enable auditing of success logon events](#BKMK_EnableSuccessLogonEvents).|  
|**Paso 4**: importar información de licencia de software|El Asistente para importar licencias de software se utiliza para importar información de licencias por volumen de Microsoft (MVLS) y declaraciones de licencias generales en el catálogo Asset Intelligence.<br /><br /> La declaración de licencias MVLS contiene información sobre los derechos de licencia o el número de licencias adquiridas de productos de Microsoft.<br /><br /> Una declaración de licencias generales contiene información sobre las licencias adquiridas de cualquier publicador.|Para más información, consulte los procedimientos siguientes de este tema: [Import software license information](#BKMK_ImportSoftwareLicenseInformation).|  
|**Paso 5**: configurar tareas de mantenimiento de Asset Intelligence|Las tareas de mantenimiento siguientes se asocian con Asset Intelligence. De forma predeterminada, las dos tareas de mantenimiento se habilitan y se configuran según una programación predeterminada.<br /><br /> **Comprobar título de la aplicación con información de inventario**: esta tarea de mantenimiento comprueba que el título de software notificado en el inventario de software sea conforme con el título de software del catálogo Asset Intelligence.<br /><br /> **Resumir datos de software instalado**: esta tarea de mantenimiento ofrece la información que se muestra en el área de trabajo **Activos y compatibilidad** del nodo **Software inventariado** en el nodo **Asset Intelligence** . Cuando se ejecuta la tarea, Configuration Manager realiza un recuento de todos los títulos de software inventariado en el sitio primario.|Para más información, consulte los procedimientos siguientes de este tema: [Configure Asset Intelligence maintenance tasks](#BKMK_ConfigureMaintenanceTasks).|  

> [!NOTE]  
>  La tarea de mantenimiento **Resumir datos de software instalado** solo está disponible en los sitios primarios.  

## <a name="supplemental-procedures-for-configuring-asset-intelligence"></a>Procedimientos adicionales para la configuración de Asset Intelligence  
 Utilice la información siguiente en los pasos de la tabla anterior.  

###  <a name="a-namebkmkenableassetintelligencea-enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 Para habilitar Asset Intelligence en sitios de Configuration Manager, debe habilitar una o varias clases de informes de inventario de hardware de Asset Intelligence. Puede habilitar las clases en la página principal de **Asset Intelligence** , o bien en el área de trabajo **Administración** , en el nodo **Configuración de cliente** , en las propiedades de configuración de cliente. Utilice uno de los procedimientos siguientes para habilitar las clases de informes de inventario de hardware de Asset Intelligence.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>Cómo habilitar las clases de informes de inventario de hardware de Asset Intelligence desde la página principal de Asset Intelligence  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Asset Intelligence**.  

3.  En la pestaña **Inicio** , en el grupo **Asset Intelligence** , haga clic en **Editar clases de inventario**. El cuadro de diálogo **Editar clases de inventario** se abre.  

4.  Para habilitar los informes de Asset Intelligence, seleccione **Habilitar solo las clases de informes de Asset Intelligence seleccionadas** o **Habilitar solo las clases de informes de Asset Intelligence seleccionadas**, y seleccione al menos una clase de informes de las que se muestran.  

    > [!NOTE]  
    >  Los informes de Asset Intelligence que dependan de las clases de inventario de hardware que se habiliten mediante este procedimiento no muestran datos hasta que los clientes hayan analizado y devuelto el inventario de hardware.  

5.  Haga clic en **Aceptar** para habilitar las clases de informes de inventario de hardware de Asset Intelligence seleccionadas.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>Cómo habilitar las clases de informes de inventario de hardware de Asset Intelligence desde las propiedades de configuración del cliente  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Configuración de cliente**y después haga clic en **Configuración de Agente de cliente predeterminada**.  

    > [!NOTE]  
    >  Si ha creado una configuración de cliente personalizada, puede seleccionar la configuración de cliente personalizada en lugar de la configuración de cliente predeterminada.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**. El cuadro de diálogo **Propiedades de configuración del cliente** se abre.  

4.  Haga clic en **Inventario de hardware**y luego en **Establecer clases**. El cuadro de diálogo **Clases de inventario de hardware** se abre.  

5.  Haga clic en **Filtrar por categoría**y luego en **Clases de informes de Asset Intelligence**. La lista de clases se actualiza solo con las clases de informes de inventario de hardware de Asset Intelligence.  

6.  Seleccione al menos una clase de informes de la lista de clases de informes de Asset Intelligence.  

    > [!NOTE]  
    >  Los informes de Asset Intelligence que dependan de las clases de inventario de hardware que se habiliten mediante este procedimiento no muestran datos hasta que los clientes hayan analizado y devuelto el inventario de hardware.  

7.  Haga clic en **Aceptar** para habilitar las clases de informes de inventario de hardware de Asset Intelligence seleccionadas.  

###  <a name="a-namebkmkinstallassetintelligencesynchronizationpointa-install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  
 Utilice el siguiente procedimiento para instalar un rol de sistema de sitio de punto de sincronización de Asset Intelligence.  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>Cómo instalar un rol de sistema de sitio de punto de sincronización de Asset Intelligence  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Servidores y roles del sistema de sitios**.  

3.  Agregue el rol de sistema de sitio de punto de sincronización de Asset Intelligence a un servidor de sistema de sitio nuevo o existente mediante el paso asociado:  

    -   **Nuevo servidor de sistema de sitio**: en la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear servidor de sistema de sitio**. Se abre el Asistente para crear servidor de sistema de sitio.  

        > [!NOTE]  
        >  De forma predeterminada, cuando Configuration Manager instala un rol de sistema de sitio, los archivos de instalación se instalan en la primera unidad de disco duro con formato NTFS disponible que tenga más espacio disponible en disco. Para evitar que Configuration Manager se instale en unidades concretas, cree un archivo vacío denominado No_sms_on_drive.sms y cópielo en la carpeta raíz de la unidad antes de instalar el servidor de sistema de sitio.  

    -   **Servidor de sistema de sitio existente**: haga clic en el servidor en el que desea instalar el rol de sistema de sitio de punto de sincronización de Asset Intelligence. Al hacer clic en un servidor, se muestra en el panel de detalles una lista de los roles de sistema de sitio que ya están instalados en el servidor.  

         En la pestaña **Inicio** , en el grupo **Servidor** , haga clic en **Agregar rol de sistema de sitio**. Se abre el Asistente para agregar roles de sistema de sitio.  

4.  En la página **General** , especifique la configuración general para el servidor de sistema de sitio. Cuando agregue el punto de sincronización de Asset Intelligence a un servidor de sistema de sitio existente, compruebe los valores configurados previamente.  

5.  En la página **Selección de rol del sistema** , seleccione **Punto de sincronización de Asset Intelligence** en la lista de roles disponibles y después haga clic en **Siguiente**.  

6.  En la página **Configuración de conexión de punto de sincronización de Asset Intelligence** , haga clic en **Siguiente**.  

     De forma predeterminada, la opción **Usar este punto de sincronización de Asset Intelligence** está seleccionada y no se puede configurar en esta página. System Center Online acepta tráfico de red solo a través del puerto TCP 443 y, por tanto, la opción **Número de puerto SSL** no se puede configurar en esta página del asistente.  

7.  Opcionalmente, puede especificar una ruta de acceso al archivo de certificado de autenticación de System Center Online (.pfx) y luego hacer clic en **siguiente**. Normalmente, no se especifica una ruta de acceso para el certificado porque el certificado de conexión se aprovisiona automáticamente durante la instalación del rol de sitio.  

8.  En la página **Configuración del servidor proxy** , especifique si el punto de sincronización de Asset Intelligence usará un servidor proxy al conectarse a System Center Online para sincronizar el catálogo y si se deben utilizar credenciales para conectarse al servidor proxy y, después, haga clic en **Siguiente**.  

    > [!WARNING]  
    >  Si se requiere un servidor proxy para conectarse a System Center Online, puede que el certificado de conexión también se elimine si expira la contraseña de la cuenta de usuario configurada para la autenticación del servidor proxy.  

9. En la página **Programación de sincronización** , especifique si quiere sincronizar el catálogo Asset Intelligence según una programación. Si se habilita la programación de la sincronización, es posible configurar una programación de sincronización simple o personalizada. Durante la sincronización programada, el punto de sincronización de Asset Intelligence se conecta a System Center Online para recuperar el último catálogo Asset Intelligence. Puede sincronizar manualmente el catálogo de Asset Intelligence desde el nodo Asset Intelligence de la consola de Configuration Manager. Puede consultar los pasos para sincronizar manualmente el catálogo de Asset Intelligence en la sección [Para sincronizar manualmente el catálogo de Asset Intelligence](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) de [Operaciones de Asset Intelligence en Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).  

10. En la página **Resumen** del Asistente de nuevo rol de sitio, revise la configuración especificada para asegurarse de que es correcta antes de continuar. Para realizar cambios en cualquier configuración, haga clic en **Anterior** hasta que regrese a la página adecuada, realice los cambios y vuelva a la página **Resumen** .  

###  <a name="a-namebkmkenablesuccesslogoneventsa-enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 Utilice el procedimiento siguiente para configurar la configuración de inicio de sesión de la directiva de seguridad de equipo a fin de habilitar la auditoría de eventos de inicio de sesión correctos.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>Cómo habilitar el registro de eventos de inicio de sesión correctos mediante una directiva de seguridad local  

1.  En un equipo cliente de Configuration Manager, haga clic en **Inicio**, seleccione **Herramientas administrativas** y luego haga clic en **Directiva de seguridad local**.  

2.  En el cuadro de diálogo **Directiva de seguridad local** , en **Configuración de seguridad**, expanda **Directivas locales**y después haga clic en **Directiva de auditoría**.  

3.  En el panel de resultados, haga doble clic en **Auditar eventos de inicio de sesión**, asegúrese de que la casilla **Correcto** está seleccionada y luego haga clic en **Aceptar**.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>Cómo habilitar el registro de eventos de inicio de sesión correctos mediante una directiva de seguridad de dominio de Active Directory  

1.  En un equipo de controlador de dominio, haga clic en **Inicio**, seleccione **Herramientas administrativas**y luego haga clic en **Directiva de seguridad de dominio**.  

2.  En el cuadro de diálogo **Directiva de seguridad local** , en **Configuración de seguridad**, expanda **Directivas locales**y después haga clic en **Directiva de auditoría**.  

3.  En el panel de resultados, haga doble clic en **Auditar eventos de inicio de sesión**, asegúrese de que la casilla **Correcto** está seleccionada y luego haga clic en **Aceptar**.  

###  <a name="a-namebkmkimportsoftwarelicenseinformationa-import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 En las secciones siguientes se explican los procedimientos necesarios para importar información de licencias de software general y de Microsoft en la base de datos de sitio de Configuration Manager mediante el Asistente para importar licencias de software. Cuando se importa información de licencia de software en la base de datos del sitio a partir de archivos de declaración de licencias, la cuenta de equipo del servidor de sitio requiere permisos de **Control total** del sistema de archivos NTFS del recurso compartido de archivos que se usa para importar información de licencia de software.  

> [!IMPORTANT]  
>  Cuando se importa información de licencia de software en la base de datos del sitio, se sobrescribe la información de licencia de software existente. Asegúrese de que el archivo de información de licencia de software que se utiliza con el Asistente para importar licencias de software contiene una lista completa de toda la información de licencia de software necesaria.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>Cómo importar información de licencia de software en el catálogo Asset Intelligence  

1.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Asset Intelligence**.  

2.  En la pestaña **Inicio** , en el grupo **Asset Intelligence** , haga clic en **Importar licencias de software**. El Asistente para importar licencias de software se abre.  

3.  En la página **principal** , haga clic en **Siguiente**.  

4.  En la página **Importar** , especifique si está importando un archivo de licencias por volumen de Microsoft (MVLS) (.xml o .csv) o un archivo de declaración de licencia general (.csv). Para más información sobre cómo crear un archivo de declaración de licencia general, vea [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) más adelante en este tema.  

    > [!WARNING]  
    >  Para descargar un archivo MVLS en formato .csv que pueda importar en el catálogo Asset Intelligence, consulte [Centro de servicios de licencias por volumen de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=226547). Para acceder a esta información, debe tener una cuenta registrada en el sitio web. Debe ponerse en contacto con su representante de cuenta de Microsoft para recibir información sobre cómo obtener el archivo MVLS en formato .xml.  

5.  Escriba la ruta de acceso UNC al archivo de declaración de licencia o haga clic en **Examinar** para seleccionar un archivo y una carpeta compartidos en la red.  

    > [!NOTE]  
    >  La carpeta compartida debe protegerse correctamente para evitar el acceso no autorizado al archivo de información de licencia y la cuenta del equipo en el que se está ejecutando el asistente debe tener permisos de Control total del recurso compartido que contiene el archivo de importación de licencia.  

6.  En la página **Resumen** , revise la información que ha especificado para asegurarse de que es correcta antes de continuar. Para realizar cambios, haga clic en **Anterior** para volver a la página **Importar** .  

###  <a name="a-namebkmkcreategenerallicensestatementa-create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> Create a general license statement information file for import  
 Una declaración de licencia general también se puede importar en el catálogo Asset Intelligence mediante un archivo de importación de licencia creado manualmente con un formato de archivo delimitado por comas (.csv).  

> [!NOTE]  
>  Aunque solo es necesario que contengan datos los campos **Nombre**, **Publicador**, **Versión**y **EffectiveQuantity** , se deben especificar todos los campos en la primera fila del archivo de importación de licencia. Todos los campos de fecha se deben mostrar en el siguiente formato: mes/día/año; por ejemplo, 08/04/2008.  

 Asset Intelligence coincide con los productos que se especifican en la declaración de licencia general mediante el nombre y la versión del producto, pero no el nombre del publicador. Debe utilizar un nombre de producto en la declaración de licencia general que sea exactamente igual al nombre del producto almacenado en la base de datos del sitio. Asset Intelligence toma el número **EffectiveQuantity** especificado en la declaración de licencia general y lo compara con el número de productos instalados que se encuentra en el inventario de Configuration Manager.  

> [!TIP]  
>  Para obtener una lista completa de los nombres de producto almacenados en la base de datos de sitio de Configuration Manager, puede ejecutar la consulta siguiente en la base de datos de sitio: SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE.  

 Puede especificar versiones exactas de un producto o especificar parte de la versión, como por ejemplo solamente la versión principal. Los ejemplos siguientes proporcionan las coincidencias de versiones resultantes de una entrada de versión de la declaración de licencia general de un producto concreto.  

|Entrada de la declaración de licencia general|Entradas de la base de datos del sitio coincidentes|  
|-------------------------------------|------------------------------------|  
|Name: "MySoftware", ProductVersion0:"2"|ProductName0: "Mysoftware", ProductVersion0: "2.01.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.02.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.10.1234"|  
|Name: "MySoftware", Version "2.05"|ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"|  
|Name: "Mysoftware", Version "2"<br /><br /> Name: "Mysoftware", Version "2.05"|Error durante la importación. Se produce un error en la importación cuando hay más de una entrada que coincide con la misma versión del producto.|  

 En el procedimiento siguiente se describe el proceso que se puede utilizar para crear un archivo de importación de declaración de licencia general mediante Microsoft Excel.  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>Cómo crear un archivo de importación de declaración de licencia general mediante Microsoft Excel  

1.  Abra Microsoft Excel y cree una nueva hoja de cálculo.  

2.  En la primera fila de la nueva hoja de cálculo, escriba los nombres de todos los campos de datos de licencias de software.  

3.  En las filas segunda y posteriores de la hoja de cálculo nueva, escriba la información de licencia de software según sea necesario. Asegúrese de que se especifiquen al menos todos los campos de datos de las licencias de software necesarias en las filas posteriores por cada licencia de software que se quiera importar. El nombre del título de software especificado en la hoja de cálculo debe ser el mismo que el título de software que se muestre en el Explorador de recursos de un equipo cliente después de que se haya ejecutado el inventario de hardware.  

4.  En el menú **Archivo** , haga clic en **Guardar como**y después guarde el archivo en formato .csv.  

5.  Copie el archivo .csv en el recurso compartido de archivos que se use para importar información de licencia de software en el catálogo Asset Intelligence.  

6.  En la consola de Configuration Manager, use el Asistente para importar licencias de software a fin de importar el archivo de información de licencia .csv recién creado.  

7.  Ejecute la **Licencia 15A - Informe de conciliación de licencias generales** de Asset Intelligence para comprobar que la información de licencia se haya importado correctamente en el catálogo Asset Intelligence.  

> [!NOTE]  
>  Para obtener un ejemplo de un archivo de licencia de software general que puede usar para realizar pruebas, vea [Example Asset Intelligence general license import file in System Center Configuration Manager (Ejemplo de archivo de importación de licencia general de Asset Intelligence en System Center Configuration Manager)](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Tabla de ejemplo para describir licencias de software  
 Cuando se crea un archivo de importación de declaración de licencia general, la información de la tabla siguiente puede utilizarse para describir las licencias de software que se importarán en el catálogo Asset Intelligence.  

|Nombre de columna|Tipo de datos|Requerido|Ejemplo|  
|-----------------|---------------|--------------|-------------|  
|Nombre|Hasta 255 caracteres|Sí|Título de software|  
|Publicador|Hasta 255 caracteres|Sí|Publicador de software|  
|Versión|Hasta 255 caracteres|Sí|Versión del título de software|  
|Lenguajes|Hasta 255 caracteres|Sí|Idioma del título de software|  
|EffectiveQuantity|Valor entero|Sí|Número de licencias adquiridas|  
|PONumber|Hasta 255 caracteres|No|Información del pedido de compra|  
|ResellerName|Hasta 255 caracteres|No|Información del distribuidor|  
|DateOfPurchase|Valor de fecha en el siguiente formato: MM/DD/AAAA|No|Informes de adquisición de la licencia|  
|SupportPurchased|Valor de bit|No|0 o 1: escriba 0 para indicar sí; 1 para no|  
|SupportExpirationDate|Valor de fecha en el siguiente formato: MM/DD/AAAA|No|Fecha de finalización del soporte técnico adquirido|  
|Comentarios|Hasta 255 caracteres|No|Comentarios opcionales|  

###  <a name="a-namebkmkconfiguremaintenancetasksa-configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 Las tareas de mantenimiento siguientes están disponibles para Asset Intelligence.  

-   **Comprobar título de la aplicación con información de inventario**: esta tarea de mantenimiento comprueba que el título de software notificado en el inventario de software sea conforme con el título de software del catálogo Asset Intelligence. De forma predeterminada, esta tarea está habilitada y programada para ejecutarse el sábado después de las 12:00 a. m. y antes de las 5:00 a. m. Esta tarea de mantenimiento solo está disponible en el sitio de nivel superior de la jerarquía de Configuration Manager.  

-   **Resumir datos de software instalado**: esta tarea de mantenimiento ofrece la información que se muestra en el área de trabajo **Activos y compatibilidad** del nodo **Software inventariado** en el nodo **Asset Intelligence** . Cuando se ejecuta la tarea, Configuration Manager realiza un recuento de todos los títulos de software inventariado en el sitio primario. De forma predeterminada, esta tarea está habilitada y programada para ejecutarse todos los días después de las 12:00 a. m. y antes de las 5:00 a. m. Esta tarea de mantenimiento solo está disponible en los sitios primarios.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>Cómo configurar tareas de mantenimiento de Asset Intelligence  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.  

3.  Seleccione el sitio en el que quiere configurar la tarea de mantenimiento de Asset Intelligence.  

    > [!NOTE]  
    >  La tarea de mantenimiento **Resumir datos de software instalado** solo está disponible en los sitios primarios.  

4.  En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Mantenimiento del sitio**. Aparece una lista de todas las tareas de mantenimiento de sitio disponibles.  

5.  Seleccione la tarea de mantenimiento deseada y después haga clic en **Editar** para modificar la configuración.  

6.  Habilite y configure la tarea de mantenimiento. Para minimizar las interferencias con la operación del sitio, se recomienda establecer el período de tiempo en horas de poca actividad del sitio. El período de tiempo es el intervalo de tiempo en el que puede ejecutar la tarea. Se define mediante las opciones **Iniciar después de** y **Hora de inicio más tardía** que se especifican en el cuadro de diálogo **Propiedades de la tarea** .  

    > [!WARNING]  
    >  Puede iniciar la tarea inmediatamente si selecciona el día actual y configura la hora de **Iniciar después de** a un par de minutos después de la hora actual.  

7.  Haga clic en **Aceptar** para guardar la configuración. La tarea se ejecuta ahora según la programación.  

    > [!NOTE]  
    >  Si una tarea no se puede ejecutar en el primer intento, Configuration Manager intenta volverla a ejecutar hasta que se ejecuta correctamente o hasta que pasa el período de tiempo en el que la tarea se puede ejecutar.  



<!--HONumber=Nov16_HO1-->


