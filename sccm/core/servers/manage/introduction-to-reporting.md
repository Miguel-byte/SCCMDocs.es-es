---
title: Introducción a los informes
titleSuffix: Configuration Manager
description: Obtenga información sobre el conjunto de herramientas y recursos disponibles para administrar los informes en Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 579e9494a4f44f41a411af88bf58df7dcc5e8075
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32340477"
---
# <a name="introduction-to-reporting-in-system-center-configuration-manager"></a>Introducción a los informes en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los informes de System Center Configuration Manager proporcionan un conjunto de herramientas y recursos para usar las avanzadas funcionalidades de informes de SQL Server Reporting Services (SSRS) y la amplia experiencia de creación que ofrece el Generador de informes de Reporting Services. Los informes le permiten reunir, organizar y presentar información sobre los usuarios, inventario de hardware y software, actualizaciones de software, aplicaciones, estado del sitio y otras operaciones de Configuration Manager de la organización. La herramienta de informes le proporciona numerosos informes predefinidos que puede usar sin realizar cambios o bien modificándolos para satisfacer sus necesidades; también puede crear informes personalizados. Use las secciones siguientes para ayudarle a administrar los informes de Configuration Manager.  

##  <a name="BKMK_SQLServerReportingServices"></a> SQL Server Reporting Services  
 SQL Server Reporting Services proporciona una amplia gama de herramientas y servicios listos para su uso que le permitirán crear, implementar y administrar informes para la organización y características de programación con las que podrá ampliar y personalizar las funciones de informes. Reporting Services es una plataforma de informes basada en servidor que proporciona exhaustivas funciones de informes para una amplia variedad de orígenes de datos.  

 Configuration Manager usa SQL Server Reporting Services como solución de informes. La integración con Reporting Services proporciona las siguientes ventajas:  

-   Usa un sistema de informes estándar del sector para consultar la base de datos de Configuration Manager.  

-   Muestra los informes mediante el Visor de informes de Configuration Manager o mediante el Administrador de informes, que es una conexión al informe basada en web.  

-   Proporciona elevadas escalabilidad y disponibilidad y alto rendimiento.  

-   Proporciona suscripciones a informes a los que pueden suscribirse los usuarios; por ejemplo, un administrador puede suscribirse para recibir automáticamente por correo electrónico un informe diario que detalle el estado de implementación de una actualización de software.  

-   Exporta informes que pueden seleccionar los usuarios en una gran variedad de los formatos más usados.  

 Para obtener más información acerca de Reporting Services, consulte [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkID=212032) en Libros en pantalla de SQL Server 2008.  

##  <a name="BKMK_ReportingServicesPoint"></a> Punto de servicios de informes  
 El punto de servicios de informes es un rol de sistema de sitio que está instalado en un servidor que ejecuta Microsoft SQL Server Reporting Services. El punto de servicios de informes copia las definiciones de informes de Configuration Manager en Reporting Services, crea carpetas de informes basadas en categorías de informes y establece una directiva de seguridad sobre los informes y las carpetas de informes que se basa en los permisos basados en roles para los usuarios administrativos de Configuration Manager. En un intervalo de 10 minutos, el punto de servicios de informes se conecta con Reporting Services para volver a aplicar la directiva de seguridad si se cambió, por ejemplo, mediante el Administrador de informes. Para obtener más información acerca de cómo planear e instalar un punto de servicios de informes, consulte la documentación siguiente:  

-   [Planeación de informes en System Center Configuration Manager](planning-for-reporting.md)  

-   [Configuración de informes en System Center Configuration Manager](configuring-reporting.md)  

##  <a name="BKMK_ConfigurationManagerReports"></a> Informes de Configuration Manager  
 Configuration Manager proporciona definiciones de informes para más de 400 informes en más de 50 carpetas de informes, que se copian a la carpeta de informes raíz en SQL Server Reporting Services durante el proceso de instalación del punto de servicios de informes. Los informes se muestran en la consola de Configuration Manager y se organizan en subcarpetas según la categoría del informe. Los informes no se propagan hacia arriba ni hacia abajo en la jerarquía de Configuration Manager; solo se ejecutan contra la base de datos del sitio en el que se han creado. En cambio, debido a que Configuration Manager replica los datos globales por toda la jerarquía, tendrá acceso a la información de toda ella. Cuando un informe recupera datos de la base de datos de un sitio, obtiene acceso a los datos del sitio tanto para el sitio actual como para los secundarios, y a los datos globales para todos los sitios de la jerarquía. Al igual que otros objetos de Configuration Manager, los usuarios administrativos deben tener los permisos adecuados para ejecutar o modificar informes. Para ejecutar un informe, un usuario administrativo debe tener el permiso **Ejecutar informe** para el objeto. Para crear o modificar un informe, un usuario administrativo debe tener el permiso **Modificar informe** para el objeto.  

###  <a name="BKMK_CreatingReports"></a> Creación y modificación de informes  
 Configuration Manager usa el Generador de informes de Microsoft SQL Server como herramienta exclusiva de creación y edición para los informes basados en modelos y basados en SQL. Al crear o editar un informe en la consola de Configuration Manager, se abrirá el Generador de informes. Para obtener más información sobre los informes de administración, consulte [Operaciones y mantenimiento de informes en System Center Configuration Manager](operations-and-maintenance-for-reporting.md).  

###  <a name="BKMK_RunningReports"></a> Ejecución de informes  
 Si ejecuta un informe en la consola de Configuration Manager, el Visor de informes se abre y se conecta a Reporting Services. Una vez que especifique los parámetros de informes requerido, Reporting Services recuperará los datos y mostrará los resultados en el visor. También puede conectarse a SQL Server Reporting Services, conectarse al origen de datos para el sitio y ejecutar informes.  

###  <a name="BKMK_ReportPrompts"></a> Mensajes de informes  
 Un mensaje de informe o un parámetro de informe en Configuration Manager es una propiedad de informe que puede configurar cuando se crea o modifica un informe. Los mensajes de informes se crean para limitar o dirigir los datos que recupera un informe. Un informe puede contener más de un mensaje, siempre que los nombres de los mensajes sean exclusivos y solo contengan caracteres alfanuméricos que cumplan las normas de SQL Server para los identificadores.  

 Cuando se ejecuta un informe, el mensaje solicitará un valor para un parámetro necesario y, en función del valor, recuperará los datos del informe. Por ejemplo, el informe **Información de un equipo específico** recupera la información de un equipo específico y solicita al usuario administrativo un nombre de equipo. Reporting Services pasa el valor especificado a una variable definida en la instrucción SQL para el informe.  

###  <a name="BKMK_ReportLinks"></a> Vínculos de informes  
 Los vínculos de informes en Configuration Manager se usan en un informe de origen para proporcionar a los usuarios administrativos un acceso sencillo a datos adicionales, como información más detallada sobre cada uno de los elementos del informe de origen. Si el informe de destino requiere uno o más mensajes para su ejecución, el informe de origen deberá contener una columna con los valores adecuados para cada mensaje. Deberá especificar el número de columna que proporciona el valor para el mensaje. Por ejemplo, puede vincular un informe que muestre los equipos descubiertos recientemente con otro informe que muestra los últimos mensajes recibidos en un equipo específico. Cuando se cree el vínculo, podría especificar que la columna 2 del informe de origen contiene nombres de equipo, que es un mensaje requerido para el informe de destino. Cuando se ejecute el informe de origen, aparecerán iconos de vínculos a la izquierda de cada fila de datos. Cuando haga clic en el icono de una fila, el Visor de informes pasará el valor de la columna especificada para dicha fila como valor de mensaje que se requiere para mostrar el informe de destino. Se puede configurar un informe con un solo vínculo, y ese vínculo solo puede conectarse a un único recurso de destino.  

> [!WARNING]  
>  Si mueve un informe de destino a otra carpeta de informes, cambiará la ubicación para el informe de destino. El vínculo del informe de origen no se actualiza automáticamente con la nueva ubicación y no funcionará en el informe de origen.  

##  <a name="BKMK_ReportFolders"></a> Carpetas de informes  
 Las carpetas de informes de System Center Configuration Manager proporcionan un método para ordenar y filtrar los informes almacenados en Reporting Services. Las carpetas de informes son particularmente útiles si tiene muchos informes que administrar. Si instala un punto de servicios de informes, los informes se copiarán a Reporting Services y se organizarán en más de 50 carpetas de informes. Las carpetas de informes son de sólo lectura. No se pueden modificar en la consola de Configuration Manager.  

##  <a name="BKMK_ReportSubscriptions"></a> Suscripciones a informes  
 Una suscripción de informe en Reporting Services es una solicitud recurrente para entregar un informe a una hora específica o en respuesta a un evento y en un formato de archivo de solicitud que especifique en la suscripción. Las suscripciones proporcionan una alternativa a ejecutar un informe a petición. Los informes a petición requieren que seleccione activamente el informe cada vez que desee verlo. Por el contrario, las suscripciones se pueden utilizar para programar y, a continuación, automatizar la entrega de un informe.  

 Puede administrar suscripciones a informes en la consola de Configuration Manager. Se procesan en el servidor de informes. Las suscripciones se distribuyen mediante el uso de las extensiones de entrega que están implementadas en el servidor. De forma predeterminada, puede crear suscripciones que envíen informes a una carpeta compartida o a una dirección de correo electrónico. Para obtener más información sobre las suscripciones de informes de administración, consulte [Operaciones y mantenimiento de informes en System Center Configuration Manager](operations-and-maintenance-for-reporting.md).  

##  <a name="BKMK_ReportBuilder"></a> Generador de informes  
 Configuration Manager usa el Generador de informes de Microsoft SQL Server Reporting Services como herramienta exclusiva de creación y edición de informes tanto basados en modelo como basados en SQL. Cuando inicia la acción para crear o editar un informe en la consola de Configuration Manager, se abre el Generador de informes. Al crear o modificar un informe por primera vez, el Generador de informes se instalará automáticamente. La versión del Generador de informes asociada con la versión instalada de SQL Server se abre cuando se ejecutan o editan informes.  

 La instalación del Generador de informes agrega compatibilidad para más de 20 idiomas. Cuando se ejecuta el Generador de informes, muestra los datos en el idioma del sistema operativo que está en ejecución en el equipo local. Si el Generador de informes no es compatible con el idioma, los datos se mostrarán en inglés. El Generador de informes es compatible con todas las funciones de SQL Server 2008 Reporting Services, que incluyen las siguientes capacidades:  

-   Ofrece un entorno de creación de informes intuitivo, con un aspecto similar a Microsoft Office.  

-   Ofrece el flexible diseño de informes del lenguaje RDL (Report Definition Language) de SQL Server 2008.  

-   Proporciona diversas formas de visualización de datos, incluidos gráficos e indicadores.  

-   Proporciona cuadros de texto con formato enriquecido.  

-   Exporta a formato de Microsoft Word.  

 También puede abrir el Generador de informes desde SQL Server Reporting Services.  

##  <a name="BKMK_ReportModels"></a> Modelos de informes en SQL Server Reporting Services  
 SQL Reporting Services en Configuration Manager usa modelos de informes para permitir a los usuarios administrativos seleccionar elementos de la base de datos e incluirlos en informes basados en modelos. Para el usuario administrativo que genera el informe, los modelos de informes solo exponen las vistas y elementos especificados para elegir entre ellos. Para crear informes basados en modelos, al menos un modelo de informes debe estar disponible. Los modelos de informes tienen las siguientes características:  

-   Puede dar a los campos y las vistas de la base de datos nombres empresariales lógicos para facilitar la producción de informes. No se requieren conocimientos de estructuras de bases de datos para producir informes.  

-   Puede agrupar los elementos lógicamente.  

-   Puede definir relaciones entre elementos.  

-   Puede proteger los elementos del modelo para que los usuarios administrativos solo puedan ver los datos que tienen permiso para ver.  

 Aunque Configuration Manager proporciona modelos de informes de ejemplo, también puede definir modelos de informes para satisfacer los requisitos empresariales. Para obtener más información sobre cómo crear modelos de informes, consulte [Creación de modelos de informes personalizados para System Center Configuration Manager en SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).  

## <a name="next-steps"></a>Pasos siguientes
[Planeación de informes](planning-for-reporting.md)
