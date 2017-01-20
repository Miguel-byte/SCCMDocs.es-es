---
title: Migrar objetos | System Center Configuration Manager
description: "Obtenga información sobre cómo planear la migración de objetos entre jerarquías en un entorno de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 243b1eeac2536e3e63e9f8cbe132d36ea2aba39a


---
# <a name="planning-for-the-migration-of-configuration-manager-objects-to-system-center-configuration-manager"></a>Planear la migración de objetos de Configuration Manager a System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Con System Center Configuration Manager, puede migrar muchos de los distintos objetos que están asociados con diferentes características que se encuentran en un sitio de origen. Utilice las secciones siguientes como ayuda para planear la migración de objetos entre jerarquías.  

-   [Planeación de la migración de actualizaciones de software](#Plan_migrate_Software_updates)  

-   [Planeación de la migración de contenido](#Plan_Migrate_content)  

-   [Planeación de la migración de recopilaciones](#BKMK_MigrateCollections)  

-   [Planeación de la migración de implementaciones de sistema operativo](#Plan_migrate_OSD)  

-   [Planeación de la migración de administración de configuración deseada](#Plan_Migrate_Compliance_settings)  

-   [Planeación de migración de límites](#Plan_migrate_Boundaries)  

-   [Planeación de la migración de informes](#Plan_Migrate_reports)  

-   [Planeación de la migración de carpetas organizativas y de búsqueda](#Plan_Migrate_Org_Folders)  

-   [Planeación de la migración de personalizaciones de Asset Intelligence](#Plan_Migrate_AI)  

-   [Planeación de la migración de personalizaciones de reglas de disponibilidad de software](#Plan_Migrate_SWM_Rules)  

##  <a name="a-nameplanmigratesoftwareupdatesa-planning-to-migrate-software-updates"></a><a name="Plan_migrate_Software_updates"></a> Planeación de la migración de actualizaciones de software  
 Puede migrar objetos de actualización de software, como paquetes de actualización de software e implementaciones de actualización de software.  

 Para migrar satisfactoriamente objetos de actualización de software, primero debe configurar la jerarquía de destino con configuraciones que coincidan con su entorno de jerarquía de origen. Esto requiere las siguientes acciones:  

-   Implementar un punto de actualización de software activo en la jerarquía de destino.  

-   Configurar el catálogo de productos e idiomas para que coincida con la configuración de la jerarquía de origen.  

-   Sincronizar el punto de actualización de software en la jerarquía de destino con Windows Server Update Services (WSUS).  

A la hora de migrar actualizaciones de software, tenga en cuenta lo siguiente:  

-   Se puede producir un error en la migración de objetos de la actualización de software si no se ha sincronizado la información en la jerarquía de destino para que coincida con la configuración de la jerarquía de origen.  

    > [!WARNING]  
    >  No se puede utilizar la herramienta WSUSutil para sincronizar datos entre una jerarquía de origen y una de destino.  

-   No se pueden migrar actualizaciones personalizadas publicadas mediante System Center Updates Publisher. En su lugar, las actualizaciones personalizadas se deben volver a publicar en la jerarquía de destino.  

Cuando migre desde una jerarquía de origen de Configuration Manager 2007, el proceso de migración modificará algunos objetos de actualizaciones de software al formato en uso en la jerarquía de destino. Utilice la tabla siguiente como ayuda para planear la migración de objetos de actualización de software de Configuration Manager 2007.  

|Objeto de Configuration Manager 2007|Nombre del objeto después de la migración|  
|-----------------------------------|---------------------------------|  
|Listas de actualizaciones de software|Las listas de actualizaciones de software se convierten en grupos de actualizaciones de software.|  
|Implementaciones de actualización de software|Las implementaciones de actualización de software se convierten en grupos de implementaciones y actualizaciones.<br /><br /> Después de migrar la implementación de una actualización de software desde Configuration Manager 2007, debe habilitarla en la jerarquía de destino para implementarla.|  
|Paquetes de actualización de software|Los paquetes de actualización de software continúan siendo paquetes de actualización de software.|  
|Plantillas de actualización de software|Las plantillas de actualización de software continúan siendo plantillas de actualización de software.<br /><br /> El valor **Duración** de las plantillas de implementación de Configuration Manager 2007 no se migra.|  

Al migrar objetos desde una jerarquía de origen de System Center 2012 Configuration Manager o System Center Configuration Manager, los objetos de las actualizaciones de software no se modifican.  

##  <a name="a-nameplanmigratecontenta-planning-to-migrate-content"></a><a name="Plan_Migrate_content"></a> Planeación de la migración de contenido  
 Puede migrar contenido de una jerarquía de origen compatible a la jerarquía de destino. Para una jerarquía de origen de Configuration Manager 2007, este contenido incluye paquetes y programas de distribución de software y aplicaciones virtuales, tales como Microsoft Application Virtualization (App-V). Para las jerarquías de origen de System Center 2012 Configuration Manager y System Center Configuration Manager, este contenido incluye aplicaciones y aplicaciones virtuales de App-V. Cuando se migra contenido entre jerarquías, son los archivos de origen comprimidos los que se migran a la jerarquía de destino.  

### <a name="packages-and-programs"></a>Paquetes y programas  
 Cuando se migran paquetes y programas, no se modifican por la migración. Sin embargo, antes de migrarlos, debe configurar cada paquete para utilizar una ruta de acceso de convención de nomenclatura universal (UNC) para su ubicación de archivo de origen. Como parte de la configuración para migrar paquetes y programas, es necesario asignar un sitio en la jerarquía de destino para administrar este contenido. El contenido no se migra desde el sitio asignado; sin embargo, después de la migración, el sitio asignado tiene acceso a la ubicación del archivo de origen original mediante la asignación de UNC.  

 Una vez migrados el paquete y el programa a la jerarquía de destino, y mientras la migración de la jerarquía de origen permanece activa, puede poner el contenido a disposición de los clientes en esa jerarquía mediante un punto de distribución compartido. Para utilizar un punto de distribución compartido, el contenido debe permanecer accesible en el punto de distribución del sitio de origen. Para obtener información sobre los puntos de distribución compartidos, consulte la sección [Share distribution points between source and destination hierarchies](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) (Compartir puntos de distribución entre jerarquías de origen y de destino) del tema [Planning a content deployment migration strategy in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md) (Planear una estrategia de migración de implementación de contenido en System Center Configuration Manager).  

 En cuanto al contenido migrado, si la versión del contenido cambia en la jerarquía de origen o en la de destino, los clientes ya no podrán tener acceso al mismo desde el punto de distribución compartido en la jerarquía de destino. En este escenario, debe volver a migrar el contenido para restaurar una versión coherente del paquete entre la jerarquía de origen y la jerarquía de destino. Esta información se sincroniza durante el ciclo de recopilación de datos.  

> [!TIP]  
>  Por cada paquete que vaya a migrar, actualice el paquete en la jerarquía de destino. Esto puede evitar problemas al implementar el paquete en puntos de distribución en la jerarquía de destino. Sin embargo, cuando se actualiza un paquete en el punto de distribución en la jerarquía de destino, los clientes de dicha jerarquía ya no podrán adquirir ese paquete desde un punto de distribución compartido. Para actualizar un paquete en la jerarquía de destino, en la consola de Configuration Manager, vaya a la biblioteca de software, haga clic con el botón secundario en el paquete y, luego, seleccione **Actualizar puntos de distribución**. Realice esta acción por cada paquete que haya migrado.  

> [!TIP]  
>  Puede usar el administrador de conversión de paquetes de Microsoft System Center Configuration Manager para convertir paquetes y programas en aplicaciones de System Center Configuration Manager. Descargar Package Conversion Manager desde el sitio del [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=212950) . Para obtener más información, consulte [Configuration Manager Package Conversion Manager](http://go.microsoft.com/fwlink/p/?LinkId=247245).  

### <a name="virtual-applications"></a>Aplicaciones virtuales  
Si migra paquetes App-V desde un sitio compatible con Configuration Manager 2007, el proceso de migración los convierte en aplicaciones en la jerarquía de destino. Además, de acuerdo con los anuncios existentes para el paquete App-V, los siguientes tipos de implementación se crean en la jerarquía de destino:  

-   Si no hay ningún anuncio, se crea un tipo de implementación que utiliza la configuración predeterminada del tipo de implementación.  

-   Si existe un anuncio, se crea un tipo de implementación que utiliza la misma configuración que la del anuncio de Configuration Manager 2007.  

-   Si existen varios anuncios, se crea un tipo de implementación para cada anuncio de Configuration Manager 2007, con la misma configuración que la del anuncio.  

> [!IMPORTANT]  
>  Si migra un App-V de Configuration Manager 2007 previamente migrado, se produce un error en la migración porque los paquetes de aplicaciones virtuales no admiten el comportamiento de sobrescritura de migración. En este escenario debe eliminar el paquete de la aplicación virtual migrado de la jerarquía de destino y, a continuación, crear un nuevo trabajo de migración para migrar la aplicación virtual.  

> [!NOTE]  
>  Una vez migrado el paquete de App-V, puede utilizar el Asistente para actualizar contenido para cambiar la ruta de origen de los tipos de implementación de App-V. Para obtener información sobre cómo actualizar el contenido relativo a un tipo de implementación, consulte la sección *How to manage deployment types* (Cómo administrar tipos de implementación) en el tema [Management tasks for System Center Configuration Manager applications](../../apps/deploy-use/management-tasks-applications.md) (Tareas de administración para aplicaciones de System Center Configuration Manager).  

Si migra desde una jerarquía de origen de System Center 2012 Configuration Manager o System Center Configuration Manager, además de las aplicaciones y los tipos de implementación de App-V, puede migrar objetos para el entorno virtual de App-V. Para obtener información sobre los entornos de App-V, consulte [Deploying App-V virtual applications with System Center Configuration Manager](../../apps/get-started/deploying-app-v-virtual-applications.md) (Implementación de aplicaciones virtuales de App-V con System Center Configuration Manager).  

### <a name="advertisements"></a>Anuncios  
Puede migrar anuncios desde un sitio de origen compatible con Configuration Manager 2007 a la jerarquía de destino mediante migración basada en recopilación. Si actualiza un cliente, éste conservará el historial de anuncios previamente ejecutados para evitar que el cliente vuelva a ejecutar los anuncios migrados.  

> [!NOTE]  
>  No puede migrar los anuncios de paquetes virtuales. Se trata de una excepción de la migración de anuncios.  

### <a name="applications"></a>Aplicaciones  
 Puede migrar las aplicaciones a una jerarquía de destino desde una jerarquía de origen de System Center 2012 Configuration Manager o de System Center Configuration Manager que sea compatible. Si reasigna a un cliente de la jerarquía de origen a la jerarquía de destino, el cliente conserva el historial de las aplicaciones previamente instaladas para impedir que vuelva a ejecutar una aplicación migrada.  

##  <a name="a-namebkmkmigratecollectionsa-planning-to-migrate-collections"></a><a name="BKMK_MigrateCollections"></a> Planeación de la migración de recopilaciones  
 Puede migrar los criterios de las recopilaciones de una jerarquía de origen compatible de System Center 2012 Configuration Manager o System Center Configuration Manager. Para ello, utilice una tarea de migración basada en objetos. Cuando se migra una recopilación, se migran las reglas de la misma y no la información acerca de los miembros de la recopilación ni la información o los objetos relacionados con los miembros de la recopilación.  

 La migración de objetos de recopilación no se admite si se migra desde una jerarquía de origen de Configuration Manager 2007.  

##  <a name="a-nameplanmigrateosda-planning-to-migrate-operating-system-deployments"></a><a name="Plan_migrate_OSD"></a> Planeación de la migración de implementaciones de sistema operativo  
Puede migrar los siguientes objetos de implementación de sistema operativo de una jerarquía de origen compatible:  

-   Imágenes y paquetes de sistema operativo. La ruta de origen de imágenes de arranque se actualiza en la ubicación de la imagen predeterminada para Windows Administrative Installation Kit (Windows AIK) en el sitio de destino. Los siguientes son los requisitos y las limitaciones de la migración de imágenes y paquetes de sistema operativo:  

    -   Para migrar satisfactoriamente archivos de imagen, la cuenta de equipo del servidor del proveedor de SMS para el sitio de alto nivel de las jerarquías de destino debe tener permisos de **Lectura** y **Escritura** de los archivos de origen de la imagen de la ubicación Windows AIK de los sitios de origen.  

    -   Cuando migre un paquete de instalación de sistema operativo, asegúrese de que la configuración del paquete en el sitio de origen indica la carpeta que contiene el archivo WIM, y no el archivo WIM mismo. Si el paquete de instalación indica el archivo WIM, se producirá un error en la migración del paquete de instalación.  

    -   Cuando se migra un paquete de imagen de arranque desde un sitio de origen de Configuration Manager 2007, el identificador del paquete no se mantiene en el sitio de destino. El resultado es que los clientes de la jerarquía de destino no pueden utilizar paquetes de imagen de arranque disponibles en los puntos de distribución compartidos.  

-   Secuencias de tareas. Cuando se migra una secuencia de tareas que contiene una referencia a un paquete de instalación de cliente, la referencia se sustituye por una referencia al paquete de instalación del cliente de la jerarquía de destino.  

    > [!NOTE]  
    >  Si migra una secuencia de tareas, es posible que Configuration Manager migre objetos no necesarios en la jerarquía de destino. Entre estos objetos se incluyen imágenes de arranque y paquetes de instalación de cliente de Configuration Manager 2007.  

-   Controladores y paquetes de controladores.  

##  <a name="a-nameplanmigratecompliancesettingsa-planning-to-migrate-desired-configuration-management"></a><a name="Plan_Migrate_Compliance_settings"></a> Planeación de la migración de administración de configuración deseada  
Puede migrar elementos de configuración y líneas de base de configuración.  

> [!NOTE]  
>  Los elementos de configuración no interpretados de jerarquías de origen de Configuration Manager 2007 no se admiten para la migración. No puede migrar o importar estos elementos de configuración a la jerarquía de destino. Para obtener información sobre los elementos de configuración no interpretados, consulte la sección "Uninterpreted Configuration Item" (Elemento de configuración no interpretado) del tema [About Configuration Items in Desired Configuration Management](http://go.microsoft.com/fwlink/?LinkId=103846) (Acerca de los elementos de configuración en la administración de configuración deseada) de la biblioteca de documentación de Configuration Manager 2007.  

Puede importar paquetes de configuración de Configuration Manager 2007. El proceso de importación convierte automáticamente el paquete de configuración para que sea compatible con System Center Configuration Manager.  

##  <a name="a-nameplanmigrateboundariesa-planning-to-migrate-boundaries"></a><a name="Plan_migrate_Boundaries"></a> Planeación de migración de límites  
 Puede migrar los límites entre las jerarquías. Al migrar límites de Configuration Manager 2007, cada límite del sitio de origen se migra al mismo tiempo y se agrega a un nuevo grupo de límites que se crea en la jerarquía de destino. Cuando se migran límites de una jerarquía de System Center 2012 Configuration Manager o System Center Configuration Manager, cada límite seleccionado se agrega a un nuevo grupo de límites en la jerarquía de destino.  

 Cada grupo de límites creado automáticamente está habilitado para la ubicación de contenido pero no para la asignación de sitios. De esta manera se evita la superposición de límites para la asignación de sitios entre las jerarquías de origen y de destino. Migrar de un sitio de origen de Configuration Manager 2007 contribuye a evitar que los nuevos clientes de Configuration Manager 2007 instalados se asignen incorrectamente a la jerarquía de destino. De forma predeterminada, los clientes de System Center Configuration Manager no se asignan automáticamente a los sitios de Configuration Manager 2007.  

 Durante la migración, si comparte un punto de distribución con la jerarquía de destino, los límites que estén asociados con el punto de distribución automáticamente se migran a la jerarquía de destino. En la jerarquía de destino, la migración crea un nuevo grupo de límites de solo lectura para cada punto de distribución compartido. Si cambia los límites del punto de distribución en la jerarquía de origen, el grupo de límites en la jerarquía de destino se actualiza con estos cambios durante el siguiente ciclo de obtención de datos.  

##  <a name="a-nameplanmigratereportsa-planning-to-migrate-reports"></a><a name="Plan_Migrate_reports"></a> Planeación de la migración de informes  
Configuration Manager no admite la migración de informes. En vez de ello, utilice el generador de informes de SQL Server Reporting Services para exportar informes de la jerarquía de origen y, a continuación, impórtelos a la jerarquía de destino.  

> [!NOTE]  
>  Como hay cambios de esquemas en los informes entre Configuration Manager 2007 y System Center Configuration Manager, debe probar todos los informes que importe desde una jerarquía de Configuration Manager 2007 para asegurarse de que funciona según lo esperado.  

Para obtener más información sobre la generación de informes, consulte [Generación de informes en System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="a-nameplanmigrateorgfoldersa-planning-to-migrate-organizational-and-search-folders"></a><a name="Plan_Migrate_Org_Folders"></a> Planeación de la migración de carpetas organizativas y de búsqueda  
 Puede migrar las carpetas organizativas y las carpetas de búsqueda de una jerarquía de origen admitida a una jerarquía de destino. Además, desde una jerarquía de origen de System Center 2012 Configuration Manager o de System Center Configuration Manager, puede migrar los criterios de una búsqueda guardada a una jerarquía de destino.  

 De forma predeterminada, el proceso de migración conserva las estructuras de carpeta administrativa y de búsqueda de objetos y recopilaciones al migrar. Sin embargo, en el Asistente para crear nuevo trabajo de migración, en la página **Configuración** , puede configurar un trabajo de migración para que no migre la estructura organizativa de objetos mediante la desactivación de la casilla correspondiente. Las estructuras organizativas de las recopilaciones siempre se conservan.  

 Las carpetas de búsqueda que contienen aplicaciones virtuales son una excepción a esta regla. Cuando se migra un paquete de App-V, el paquete de App-V se transforma en una aplicación en System Center Configuration Manager. Después de la migración de la carpeta de búsqueda solo se encuentran los paquetes restantes. La carpeta de búsqueda no puede encontrar un paquete de App-V debido a la conversión en aplicación cuando migra.  

 Cuando se migra una búsqueda guardada de la jerarquía de origen de System Center 2012 Configuration Manager o System Center Configuration Manager, se migran los criterios de búsqueda y no la información del resultado de esta. La migración de una búsqueda guardada no es aplicable desde un sitio de origen de Configuration Manager 2007.  

##  <a name="a-nameplanmigrateaia-planning-to-migrate-asset-intelligence-customizations"></a><a name="Plan_Migrate_AI"></a> Planeación de la migración de personalizaciones de Asset Intelligence  
 Puede migrar las personalizaciones de Asset Intelligence de una jerarquía de origen admitida a una jerarquía de destino. No hay cambios significativos en la estructura de las personalizaciones de Asset Intelligence entre Configuration Manager 2007 y System Center Configuration Manager.  

> [!NOTE]  
>  System Center Configuration Manager no admite la migración de objetos de Asset Intelligence de un sitio de Configuration Manager 2007 que usa Asset Intelligence Service 2.0 (AIS 2.0).  

##  <a name="a-nameplanmigrateswmrulesa-planning-to-migrate-software-metering-rules-customizations"></a><a name="Plan_Migrate_SWM_Rules"></a> Planeación de la migración de personalizaciones de reglas de disponibilidad de software  
 No hay ningún cambio significativo en la medición de software entre Configuration Manager 2007 y System Center Configuration Manager. Puede migrar las reglas de disponibilidad de software de una jerarquía de origen admitida a una jerarquía de destino.  

 De manera predeterminada, las reglas de disponibilidad de software que se migran a una jerarquía de destino no están asociadas a un sitio en la jerarquía de destino, sino que se aplican a todos los clientes en la jerarquía. Para aplicar una regla de disponibilidad de software a clientes de un determinado sitio, debe editar la regla de disponibilidad después de su migración.  



<!--HONumber=Nov16_HO1-->


