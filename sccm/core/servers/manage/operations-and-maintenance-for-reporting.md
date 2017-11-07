---
title: 'Operaciones y mantenimiento de informes '
titleSuffix: Configuration Manager
description: "Obtenga los detalles sobre la administración de informes y suscripciones a informes en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
caps.latest.revision: "5"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 05a81cdfd46ba2bf0bea17b06bd72f79296b3930
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="operations-and-maintenance-for-reporting-in-system-center-configuration-manager"></a>Operaciones y mantenimiento de informes en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Cuando la infraestructura de generación de informes esté operativa en System Center Configuration Manager, puede ejecutar una serie de operaciones habituales para administrar informes y suscripciones a informes.  

##  <a name="BKMK_ManageReports"></a> Administración de informes de Configuration Manager  
 Configuration Manager ofrece más de 400 informes predefinidos que le ayudan a recopilar, organizar y presentar información sobre usuarios, inventario de hardware y software, actualizaciones de software, aplicaciones, estados de sitio y otras operaciones de Configuration Manager de la organización. Puede utilizar los informes predefinidos tal cual están, o puede modificar un informe para satisfacer sus necesidades. También puede crear informes personalizados basados en SQL y en modelo para satisfacer sus necesidades. Consulte las secciones siguientes para ayudarle a administrar los informes de Configuration Manager.  

###  <a name="BKMK_RunReport"></a> Ejecución de un informe de Configuration Manager  
 En el Administrador de configuración de informes se almacena en SQL Server Reporting Services y los datos representados en el informe se recuperan de la base de datos del sitio de Configuration Manager. Puede obtener acceso a informes en la consola de Configuration Manager o mediante el Administrador de informes, que se obtiene acceso en un explorador web. Puede abrir informes en cualquier equipo que tenga acceso al equipo que ejecuta SQL Server Reporting Services y, además, debe disponer de los derechos suficientes para poder ver los informes. Al ejecutar un informe, el título, la descripción y la categoría del informe se muestran en el idioma del sistema operativo local.  

> [!NOTE]  
>  En algunos idiomas distintos al inglés, es posible que los caracteres no aparezcan correctamente en los informes.  En este caso, los informes se pueden visualizar mediante el Administrador de informes basado en web o a través de la consola de administrador remoto.  

> [!WARNING]  
>  Para ejecutar informes, debe tener derechos de **lectura** para los permisos **Sitio** y **Ejecutar informe** configurados para objetos específicos.  

> [!IMPORTANT]    
> Debe haber una relación de confianza bidireccional establecida para los usuarios de un dominio distinto al de la cuenta para el punto de servicios de informes para una correcta ejecución de los informes.

> [!NOTE]  
>  El Administrador de informes es una herramienta de acceso y administración de informes basada en web que se usa para administrar una única instancia de servidor de informes en una ubicación remota a través de una conexión HTTP. Puede utilizar el Administrador de informes para las tareas operativas, por ejemplo, para ver los informes, modificar las propiedades de los informes y administrar suscripciones a informes asociados. En este tema se describen los pasos que cabe seguir para ver un informe y modificar sus propiedades en el Administrador de informes; no obstante, si desea obtener más información acerca de las demás opciones disponibles en el Administrador de informes, consulte [Administrador de informes](http://go.microsoft.com/fwlink/p/?LinkId=224916) en los Libros en pantalla de SQL Server 2008.  

 Utilice los procedimientos siguientes para ejecutar un informe de Configuration Manager.  

##### <a name="to-run-a-report-in-the-configuration-manager-console"></a>Para ejecutar un informe en la consola de Configuration Manager  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Generación de informes**y, a continuación, haga clic en **Informes** para ver los informes disponibles.  

    > [!IMPORTANT]  
    >  En esta versión de Configuration Manager, **Todo el contenido** solo muestra los paquetes, no las aplicaciones.  

    > [!TIP]  
    >  Si no aparece ningún informe, compruebe que el punto de servicios de informes está instalado y configurado. Para obtener más información, vea [Configuración de informes](configuring-reporting.md).  

3.  Seleccione el informe que desee ejecutar y, a continuación, en la pestaña **Inicio** de la sección **Grupo de informes** , haga clic en **Ejecutar** para abrir el informe.  

4.  Si se necesitan parámetros, especifíquelos y, a continuación, haga clic en **Ver informe**.  

#### <a name="to-run-a-report-in-a-web-browser"></a>Para ejecutar un informe en un explorador web  

1.  En el explorador web, escriba la dirección URL del Administrador de informes, por ejemplo, **http:\/\/Server1\/Reports**. Puede determinar la dirección URL del Administrador de informes en el **Report Manager URL** página en el Administrador de configuración de Reporting Services.  

2.  En el Administrador de informes, haga clic en la carpeta de informes de Configuration Manager, por ejemplo, **ConfigMgr\_CAS**.  

    > [!TIP]  
    >  Si no aparece ningún informe, compruebe que el punto de servicios de informes está instalado y configurado. Para obtener más información, vea [Configuración de informes](configuring-reporting.md).  

3.  Haga clic en la categoría de informe del informe que desea ejecutar y, a continuación, haga clic en el vínculo del informe. El informe se abre en el Administrador de informes.  

4.  Si se necesitan parámetros, especifíquelos y, a continuación, haga clic en **Ver informe**.  

###  <a name="BKMK_ModifyReportProperties"></a> Modificación de las propiedades de un informe de Configuration Manager  
 En la consola de Configuration Manager, puede ver las propiedades de un informe, como el nombre y la descripción, pero debe usar el Administrador de informes para poder modificar las propiedades. Use el siguiente procedimiento para modificar las propiedades de un informe de Configuration Manager.  

#### <a name="to-modify-report-properties-in-report-manager"></a>Para modificar las propiedades de informes en el Administrador de informes  

1.  En el explorador web, escriba la dirección URL del Administrador de informes, por ejemplo, **http:\/\/Server1\/Reports**. Puede determinar la dirección URL del Administrador de informes en el **Report Manager URL** página en el Administrador de configuración de Reporting Services.  

2.  En el Administrador de informes, haga clic en la carpeta de informes de Configuration Manager, por ejemplo, **ConfigMgr\_CAS**.  

    > [!TIP]  
    >  Si no aparece ningún informe, compruebe que el punto de servicios de informes está instalado y configurado. Para obtener más información, vea [Configuración de informes](configuring-reporting.md)  

3.  Haga clic en la categoría de informe del informe cuyas propiedades desea modificar y, a continuación, haga clic en el vínculo del informe. El informe se abre en el Administrador de informes.  

4.  Haga clic en la pestaña **Propiedades** . Puede modificar el nombre y la descripción del informe.  

5.  Cuando haya terminado, haga clic en **Aplicar**. Las propiedades del informe se guardan en el servidor de informes, y la consola de Configuration Manager recupera las propiedades actualizadas del informe.  

###  <a name="BKMK_EditReport"></a> Edición de un informe de Configuration Manager  
 Cuando un informe existente de Configuration Manager no recupera la información de la que debe disponer o no presenta el diseño deseado, puede editar el informe en el Generador de informes.  

> [!NOTE]  
>  También puede clonar un informe existente: ábralo para edición y haga clic en **Guardar como** para guardarlo como un nuevo informe.  

> [!IMPORTANT]  
>  La cuenta de usuario debe tener el permiso de **modificación del sitio** y los permisos **Modificar informe** en los objetos específicos asociados con el informe que desea modificar.  

> [!IMPORTANT]  
>  Cuando Configuration Manager se actualiza a una versión más reciente, los nuevos informes sobrescriben los informes predefinidos. Si modifica un informe predefinido, debe realizar una copia de seguridad del informe antes de instalar la nueva versión y, a continuación, restaurar el informe en Reporting Services. Si va a realizar cambios importantes en un informe predefinido, considere la posibilidad de crear un nuevo informe en su lugar. No se sobrescriben los nuevos informes creados antes de actualizar un sitio.  

 Use el siguiente procedimiento para editar las propiedades de un informe de Configuration Manager.  

#### <a name="to-edit-report-properties"></a>Para editar las propiedades de informes  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Generación de informes**y, a continuación, haga clic en **Informes** para ver los informes disponibles.  

3.  Seleccione el informe que desee modificar y, a continuación, en la pestaña **Inicio** , en la sección **Grupo de informes** , haga clic en **Editar**. Escriba la cuenta de usuario y contraseña si se le solicitan y, a continuación, haga clic en **Aceptar**. Si el Generador de informes no está instalado en el equipo, se le solicitará que lo instale. Haga clic en **Ejecutar** para instalar el Generador de informes, una aplicación que resulta necesaria para modificar y crear informes.  

4.  En el Generador de informes, modifique la configuración del informe según corresponda y, a continuación, haga clic en **Guardar** para guardar el informe en el servidor de informes.  

###  <a name="BKMK_CreateModelBasedReport"></a> Creación de un informe\-basado en modelo  
 Un informe basado en modelo le permite seleccionar de forma interactiva los elementos que desea incluir en el informe. Para más información sobre la creación de modelos de informes, vea [Creación de modelos de informes personalizados para System Center Configuration Manager en SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).  

> [!IMPORTANT]  
>  La cuenta de usuario debe tener el permiso de **modificación del sitio** para crear un informe nuevo. El usuario sólo puede crear un informe en las carpetas para las que el usuario tiene permisos de **modificación de informes** .  

 Use los procedimientos siguientes para ejecutar un informe de Configuration Manager basado en modelo.  

#### <a name="to-create-a-model-based-report"></a>Para crear un informe basado en modelo  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Generación de informes** y, a continuación, haga clic en **Informes**.  

3.  En la pestaña **Inicio** , en la sección **Crear** , haga clic en **Crear informe** para iniciar el **Asistente para crear informes**.  

4.  En la página **Información** , configure las siguientes opciones:  

    -   **Tipo:** seleccione **Informe basado en modelo** para crear un informe en el Generador de informes con la utilización del modelo de Reporting Services.  

    -   **Nombre**: especifique un nombre para el informe.  

    -   **Descripción**: especifique una descripción para el informe.  

    -   **Servidor**: muestra el nombre del servidor de informes en el que va a crear este informe.  

    -   **Ruta de acceso**: haga clic en **Examinar** para especificar una carpeta en la que desea almacenar el informe.  

     Haga clic en **Siguiente**.  

5.  En la página **Selección de modelo** , seleccione un modelo disponible en la lista que desee utilizar para crear este informe. Al seleccionar el modelo de informe, en la sección **Vista previa** se muestran las entidades y las vistas de SQL Server que estarán disponibles con el modelo de informe seleccionado.  

6.  En la página **Resumen** , revise la configuración. Haga clic en **Anterior** para cambiar la configuración o haga clic en **Siguiente** para crear el informe en Configuration Manager.  

7.  En la página **Confirmación** , haga clic en **Cerrar** para salir del asistente y, a continuación, abra el Generador de informes para configurar las opciones del informe. Escriba la cuenta de usuario y contraseña si se le solicitan y, a continuación, haga clic en **Aceptar**. Si el Generador de informes no está instalado en el equipo, se le solicitará que lo instale. Haga clic en **Ejecutar** para instalar el Generador de informes, una aplicación que resulta necesaria para modificar y crear informes.  

8.  En el Generador de informes de Microsoft, cree el diseño del informe, seleccione los datos en las vistas de SQL Server disponibles, agregue parámetros al informe y así sucesivamente. Para obtener más información acerca de cómo utilizar el Generador de informes para crear un informe nuevo, consulte la Ayuda del Generador de informes.  

9. Haga clic en **Ejecutar** para ejecutar el informe. Compruebe que el informe proporciona la información esperada. Haga clic en **Diseño** para volver a la vista de diseño para modificar el informe, si es necesario.  

10. Haga clic en **Guardar** para guardar el informe en el servidor de informes. Puede ejecutar y modificar el nuevo informe en el nodo **Informes** en el área de trabajo **Supervisión** .  

###  <a name="BKMK_CreateSQLBasedReport"></a> Creación de un informe\-basado en SQL  
 Un informe basado en SQL le permite recuperar los datos basados en una instrucción SQL del informe.  

> [!IMPORTANT]  
>  Al crear una instrucción SQL para un informe personalizado, no haga referencia directamente a las tablas de SQL Server. En su lugar, haga referencia a las vistas de SQL Server \(nombres de vista que empiezan por v\_\) de la base de datos de sitio. También puede hacer referencia a procedimientos públicos almacenados \(nombres de procedimientos almacenados que empiezan con sp\_\) de la base de datos de sitio.  

> [!IMPORTANT]  
>  La cuenta de usuario debe tener el permiso de **modificación del sitio** para crear un informe nuevo. El usuario sólo puede crear un informe en las carpetas para las que el usuario tiene permisos de **modificación de informes** .  

 Use los procedimientos siguientes para ejecutar un informe de Configuration Manager basado en SQL.  

#### <a name="to-create-a-sql-based-report"></a>Para crear un informe basado en SQL  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Generación de informes**y, a continuación, haga clic en **Informes**.  

3.  En la pestaña **Inicio** , en la sección **Crear** , haga clic en **Crear informe** para iniciar el **Asistente para crear informes**.  

4.  En la página **Información** , configure las siguientes opciones:  

    -   **Tipo**: seleccione **Informe basado en SQL** para crear un informe en el Generador de informes con la utilización de una instrucción SQL.  

    -   **Nombre**: especifique un nombre para el informe.  

    -   **Descripción**: especifique una descripción para el informe.  

    -   **Servidor**: muestra el nombre del servidor de informes en el que va a crear este informe.  

    -   **Ruta de acceso**: haga clic en **Examinar** para especificar una carpeta en la que desea almacenar el informe.  

     Haga clic en **Siguiente**.  

5.  En la página **Resumen** , revise la configuración. Haga clic en **Anterior** para cambiar la configuración o haga clic en **Siguiente** para crear el informe en Configuration Manager.  

6.  En la página **Confirmación** , haga clic en **Cerrar** para salir del asistente y, a continuación, abra el Generador de informes para configurar las opciones del informe. Escriba la cuenta de usuario y contraseña si se le solicitan y, a continuación, haga clic en **Aceptar**. Si el Generador de informes no está instalado en el equipo, se le solicitará que lo instale. Haga clic en **Ejecutar** para instalar el Generador de informes, una aplicación que resulta necesaria para modificar y crear informes.  

7.  En el Generador de informes de Microsoft, proporcione la instrucción SQL para el informe o compile la instrucción SQL con la utilización de las columnas de las vistas de SQL Server disponibles, agregue parámetros al informe y así sucesivamente.  

8.  Haga clic en **Ejecutar** para ejecutar el informe. Compruebe que el informe proporciona la información esperada. Haga clic en **Diseño** para volver a la vista de diseño para modificar el informe, si es necesario.  

9. Haga clic en **Guardar** para guardar el informe en el servidor de informes. Puede ejecutar el nuevo informe en el nodo **Informes** en el área de trabajo **Supervisión** .  

##  <a name="BKMK_ManageReportSubscriptions"></a> Administrar suscripciones a informes  
 Las suscripciones a informes en SQL Server Reporting Services permiten configurar la entrega automática de determinados informes a través de correo electrónico o de un recurso compartido de archivos en intervalos programados. Use el **Asistente para crear suscripciones** en System Center 2012 Configuration Manager para configurar las suscripciones a informes.  

###  <a name="BKMK_ReportSubscriptionFileShare"></a> Creación de una suscripción de informe para la entrega de un informe a un recurso compartido de archivos  
 Cuando se crea una suscripción de informe para la entrega de un informe a un recurso compartido de archivos, el informe se copia en el formato especificado en el recurso compartido de archivo seleccionado. Solo puede realizar la suscripción y la solicitud de entrega de un único informe a la vez.  

 A diferencia de los informes hospedados y administrados por un servidor de informes, los informes que se entregan en una carpeta compartida son archivos estáticos. Las características interactivas definidas para el informe no funcionan en informes que se almacenan como archivos en el sistema de archivos. Las funciones de interacción se representan como elementos estáticos. Si el informe incluye gráficos, se utiliza la presentación predeterminada. Si el informe se vincula a otro informe, el vínculo se representa como texto estático. Si desea conservar las características interactivas en un informe entregado, utilice la entrega a través de correo electrónico. Para obtener más información sobre la entrega de correo electrónico, vea la sección [Creación de una suscripción de informe para la entrega de un informe a través del correo electrónico](#BKMK_ReportSubscriptionEmail) posteriormente en este tema.  

 Cuando se crea una suscripción que usa la entrega a través de recurso compartido de archivos, debe especificar una carpeta existente como carpeta de destino. El servidor de informes no crea las carpetas en el sistema de archivos. La carpeta que especifique debe ser accesible a través de una conexión de red. Cuando se especifica la carpeta de destino en una suscripción, utilice una ruta de acceso UNC y no incluya barras diagonales inversas en la ruta de carpeta. Por ejemplo, una ruta de acceso UNC válida para la carpeta de destino podría ser: \\\\&lt;nombre de servidor\>\\reportfiles\\operations\\2011.  

 Los informes se pueden representar en varios formatos de archivo, como MHTML o Excel. Para guardar el informe en un determinado formato de archivo, seleccione el formato de representación al crear la suscripción. Por ejemplo, la selección de Excel guarda el informe como un archivo de Microsoft Excel. Aunque es posible seleccionar cualquier formato de representación admitido, la representación de archivos funciona mejor en algunos formatos que en otros.  

 Utilice el procedimiento siguiente para crear una suscripción de informe para entregar un informe a un recurso compartido de archivos.  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Para crear una suscripción de informe para entregar un informe a un recurso compartido de archivos  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Informes** y, a continuación, haga clic en **Informes** para visualizar los informes disponibles. Puede seleccionar una carpeta de informes para mostrar solo los informes que están asociados con la carpeta.  

3.  Seleccione el informe que desee agregar a la suscripción y, a continuación, en la pestaña **Inicio** , en la sección **Grupo de informes** , haga clic en **Crear suscripción** para abrir el **Asistente para crear suscripciones**.  

4.  En la página **Entrega de suscripción** , configure las siguientes opciones:  

    -   Informe entregado por: Seleccione **Recurso compartido de archivos** para entregar el informe a un recurso compartido de archivos.  

    -   **Nombre de archivo**: Especifique el nombre de archivo del informe. De forma predeterminada, el archivo de informe no incluye una extensión de nombre de archivo. Seleccione **Agregar extensión de archivo al crearse** para agregar automáticamente una extensión de nombre de archivo a este informe en función del formato de representación.  

    -   **Ruta de acceso**: especifique una ruta de acceso UNC a una carpeta existente en la que quiere que se entregue el informe \(por ejemplo, \\\\&lt;nombre de servidor\>\\&lt;nombre de recurso compartido de servidor\>\\&lt;carpeta de informes\>\).  

        > [!NOTE]  
        >  El nombre de usuario especificado posteriormente en esta página debe tener acceso a este recurso compartido de servidor y tener permisos de escritura en la carpeta de destino.  

    -   **Formato de representación**: Seleccione uno de los formatos siguientes para el archivo de informe:  

        -   **Archivo XML con datos del informe**: Guarda el informe en formato de lenguaje de marcado extensible.  

        -   **CSV \(delimitado por comas\)**: Guarda el informe en formato de valores separados por comas.  

        -   **Archivo TIFF**: Guarda el informe en formato Tagged Image File.  

        -   **Archivo de Acrobat \(PDF\)**: Guarda el informe en formato Acrobat Portable Document.  

        -   **HTML 4.0**: Guarda el informe como una página web que se puede visualizar solo en exploradores que admiten HTML 4.0. Internet Explorer 5 y las versiones posteriores admiten HTML 4.0.  

            > [!NOTE]  
            >  Si tiene imágenes en el informe, el formato HTML 4.0 no las incluye en el archivo.  

        -   **MHTML \(archivo web\)**: Guarda el informe en formato MIME HTML \(mhtml\), que se puede visualizar en muchos exploradores web.  

        -   **Representador de RPL**: Guarda el informe en formato Report Page Layout \(RPL\).  

        -   **Excel**: Guarda el informe como una hoja de cálculo de Microsoft Excel.  

        -   **Word**: Guarda el informe como un documento de Microsoft Word.  

    -   **Nombre de usuario**: Especifique una cuenta de usuario de Windows con permisos para tener acceso al recurso compartido y la carpeta del servidor de destino. La cuenta de usuario debe tener acceso a este recurso compartido de servidor y tener permiso de escritura en la carpeta de destino.  

    -   **Contraseña**: Especifique la contraseña de la cuenta de usuario de Windows. En **Confirmar contraseña**, vuelva a escribir la contraseña.  

    -   Seleccione una de las siguientes opciones para configurar el comportamiento si ya existe un archivo con el mismo nombre en la carpeta de destino:  

        -   **Sobrescribir archivos existentes con nuevas versiones**: Especifica que si el archivo de informe ya existe, la nueva versión lo sobrescribe.  

        -   **No sobrescribir archivos existentes**: Especifica que si el archivo de informe ya existe, no se realiza ninguna acción.  

        -   **Incrementar nombres de archivo al agregarse nuevas versiones**: Especifica que si ya existe el archivo de informe, se agrega un número al nuevo informe en el nombre de archivo para distinguirlo de otras versiones.  

    -   **Descripción**: Especifica la descripción de la suscripción de informe.  

     Haga clic en **Siguiente**.  

5.  En la página **Programación de suscripción** , seleccione una de las siguientes opciones de programación de entrega para la suscripción de informe:  

    -   **Usar programación compartida**: Una programación compartida es una programación definida previamente que puede ser utilizada por otras suscripciones de informes. Active esta casilla y, a continuación, seleccione una programación compartida en la lista si se ha especificado alguna.  

    -   **Crear nueva programación**: Configure la programación en la que se ejecuta este informe, incluidos el intervalo, la hora y fecha de inicio y la fecha de finalización de esta suscripción.  

6.  En página **Parámetros de suscripción** , especifique los parámetros de este informe que se utilizan cuando se ejecuta sin supervisión. Si no hay ningún parámetro para el informe, no se muestra esta página.  

7.  En la página **Resumen** , revise la configuración de la suscripción de informe. Haga clic en **Anterior** para cambiar la configuración o haga clic en **Siguiente** para crear la suscripción de informe.  

8.  En la página **Finalización** , haga clic en **Cerrar** para salir del asistente. Compruebe que la suscripción de informe se creó correctamente. Puede ver y modificar suscripciones de informes en el nodo **Suscripciones** , en **Informes** , en el área de trabajo **Supervisión** .  

###  <a name="BKMK_ReportSubscriptionEmail"></a> Creación de una suscripción de informe para la entrega de un informe a través del correo electrónico  
 Cuando crea una suscripción de informe para entregar un informe mediante el correo electrónico, se envía un correo electrónico a los destinatarios configurados y el informe se incluye como datos adjuntos. El servidor de informes no valida las direcciones de correo electrónico ni obtiene direcciones de correo electrónico de un servidor de correo electrónico. Debe saber de antemano las direcciones de correo electrónico que desea usar. De forma predeterminada, puede enviar informes a través del correo electrónico a cualquier cuenta de correo electrónico válida dentro o fuera de su organización. Puede seleccionar las dos opciones de entrega de correo electrónico siguientes:  

-   Enviar una notificación y un hipervínculo al informe generado.  

-   Enviar un informe adjunto o incrustado. El formato de representación y el explorador determinan si el informe se incrusta o adjunta. Si su explorador es compatible con HTML 4.0 y MHTML y se selecciona el formato de representación MHTML \(archivo web\), el informe se incrusta como parte del mensaje. Todos los demás formatos de representación \(CSV, PDF, Word, etc.\) proporcionan informes como datos adjuntos. Reporting Services no comprueba el tamaño de los datos adjuntos o del mensaje antes de enviar el informe. Si los datos adjuntos o el mensaje superan el límite máximo permitido por su servidor de correo electrónico, el informe no se entregará.  

> [!IMPORTANT]  
>  Debe establecer la configuración de correo electrónico en Reporting Services para que la opción de entrega **Correo electrónico** esté disponible. Para obtener más información sobre la configuración de opciones de correo electrónico en Reporting Services, consulte [Configurar un servidor de informes para la entrega por correo electrónico](http://go.microsoft.com/fwlink/p/?LinkId=226668) en Libros en pantalla de SQL Server.  

 Utilice el procedimiento siguiente para crear una suscripción de informe para entregar un informe a través de correo electrónico.  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-by-email"></a>Para crear una suscripción de informe para entregar un informe por correo electrónico  

-   En la consola de Configuration Manager, haga clic en **Supervisión**.  

-   En el área de trabajo **Supervisión** , expanda **Informes** y, a continuación, haga clic en **Informes** para visualizar los informes disponibles. Puede seleccionar una carpeta de informes para mostrar solo los informes que están asociados con la carpeta.  

-   Seleccione el informe que desee agregar a la suscripción y, a continuación, en la pestaña **Inicio** , en la sección **Grupo de informes** , haga clic en **Crear suscripción** para abrir el **Asistente para crear suscripciones**.  

-   En la página **Entrega de suscripción** , configure las siguientes opciones:  

    -   **Informe entregado por**: Seleccione **Correo electrónico** para entregar el informe como datos adjuntos en un mensaje de correo electrónico.  

    -   **A**: Especifique una dirección de correo electrónico válida a la que enviar este informe.  

        > [!NOTE]  
        >  Puede especificar varios destinatarios de correo electrónico mediante la separación de cada dirección de correo electrónico con un punto y coma.  

    -   **CC**: Si lo desea, especifique una dirección de correo electrónico a la que desea enviar una copia de este informe.  

    -   **CCO**: Opcionalmente, especifique una dirección de correo electrónico a la que desea enviar una copia oculta de este informe.  

    -   **Responder a**: Especifique la dirección de respuesta que se utilizará si el destinatario responde al mensaje de correo electrónico.  

    -   **Tema**: Especifique una línea de tema del mensaje de correo electrónico de suscripción.  

    -   **Prioridad**: Seleccione la marca de prioridad del mensaje de correo electrónico. Seleccione **Baja**, **Normal**o **Alta**. Microsoft Exchange usa la configuración de prioridad para establecer una marca que indica la importancia del mensaje de correo electrónico.  

    -   **Comentario**: Especifique el texto que se agregará al cuerpo del mensaje de correo electrónico de suscripción.  

    -   **Descripción**: Especifica la descripción de la suscripción de informe.  

    -   **Incluir vínculo**: Incluye la dirección URL del informe suscrito en el cuerpo del mensaje de correo electrónico.  

    -   **Incluir informe**: Especifica que el informe se adjunta al mensaje de correo electrónico. El formato en el que se adjuntará el informe se especifica en la lista **Formato de representación** .  

    -   **Formato de representación**: Seleccione uno de los siguientes formatos para el informe adjunto:  

        -   **Archivo XML con datos del informe**: Guarda el informe en formato de lenguaje de marcado extensible.  

        -   **CSV \(delimitado por comas\)**: Guarda el informe en formato de valores separados por comas.  

        -   **Archivo TIFF**: Guarda el informe en formato Tagged Image File.  

        -   **Archivo de Acrobat \(PDF\)**: Guarda el informe en formato Acrobat Portable Document.  

        -   **MHTML \(archivo web\)**: Guarda el informe en formato MIME HTML \(mhtml\), que se puede visualizar en muchos exploradores web.  

        -   **Excel**: Guarda el informe como una hoja de cálculo de Microsoft Excel.  

        -   **Word**: Guarda el informe como un documento de Microsoft Word.  

-   En la página **Programación de suscripción** , seleccione una de las siguientes opciones de programación de entrega para la suscripción de informe:  

    -   **Usar programación compartida**: Una programación compartida es una programación definida previamente que puede ser utilizada por otras suscripciones de informes. Active esta casilla y, a continuación, seleccione una programación compartida en la lista si se ha especificado alguna.  

    -   **Crear nueva programación**: Configure la programación en la que se ejecutará este informe, incluidos el intervalo, la hora y fecha de inicio y la fecha de finalización de esta suscripción.  

-   En página **Parámetros de suscripción** , especifique los parámetros de este informe que se utilizan cuando se ejecuta sin supervisión. Si no hay ningún parámetro para el informe, no se muestra esta página.  

-   En la página **Resumen** , revise la configuración de la suscripción de informe. Haga clic en **Anterior** para cambiar la configuración o haga clic en **Siguiente** para crear la suscripción de informe.  

-   En la página **Finalización** , haga clic en **Cerrar** para salir del asistente. Compruebe que la suscripción de informe se creó correctamente. Puede ver y modificar suscripciones de informes en el nodo **Suscripciones** , en **Informes** , en el área de trabajo **Supervisión** .  
