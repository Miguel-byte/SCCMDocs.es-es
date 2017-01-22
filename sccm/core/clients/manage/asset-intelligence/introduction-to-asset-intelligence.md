---
title: "Introducción a Asset Intelligence | Microsoft Docs"
description: "Obtenga una introducción a Asset Intelligence en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 6a851ddfeee78574fbb0b1eff0c7cc518a7bb598


---
# <a name="introduction-to-asset-intelligence-in-system-center-configuration-manager"></a>Introducción a Asset Intelligence en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Asset Intelligence en System Center Configuration Manager le permite inventariar y administrar el uso de licencias de software en toda la empresa mediante el catálogo Asset Intelligence. Muchas clases de Instrumental de administración de Windows (WMI) de inventario de hardware mejoran la amplitud de información que se recopila sobre el hardware y los títulos de software que se utilizan. Más de 60 informes presentan esta información con un formato fácil de usar. Muchos de estos informes vinculan a otros más específicos, en los que puede consultar información general y profundizar para obtener información más detallada. Puede agregar información personalizada al catálogo Asset Intelligence, como categorías de software personalizado, familias de software, etiquetas de software y requisitos de hardware. También puede conectarse a System Center Online para actualizar dinámicamente el catálogo Asset Intelligence con la información más reciente disponible. Los clientes de Microsoft pueden equilibrar el uso de licencias de software empresarial con las licencias de software adquiridas que se están usando mediante la importación de información de licencias de software en la base de datos del sitio de Configuration Manager.  

##  <a name="a-namebkmkassetintelligencecataloga-asset-intelligence-catalog"></a><a name="BKMK_AssetIntelligenceCatalog"></a> Catálogo Asset Intelligence  

 El catálogo Asset Intelligence de Configuration Manager es un conjunto de tablas de base de datos almacenadas en la base de datos del sitio que contiene información de categorización e identificación de más de 300 000 títulos y versiones de software. Estas tablas de base de datos también se utilizan para administrar requisitos de hardware de títulos de software concretos.  

 El catálogo Asset Intelligence ofrece información de licencias de software de títulos de software que se utilicen, tanto de Microsoft como de otros fabricantes. Hay disponible un conjunto predefinido de requisitos de hardware de títulos de software en el catálogo Asset Intelligence y puede crear nueva información de requisitos de hardware definida por el usuario para cumplir requisitos personalizados. Además, puede personalizar la información en el catálogo Asset Intelligence y puede cargar información de títulos de software en System Center Online para su categorización.  

 Las actualizaciones del catálogo Asset Intelligence que contienen software de reciente publicación están disponibles para su descarga periódicamente a fin de realizar actualizaciones masivas del catálogo. O bien, el catálogo se puede actualizar dinámicamente mediante el uso del rol de sistema de sitio de punto de sincronización de Asset Intelligence.  

###  <a name="a-namebkmksoftwarecategoriesa-software-categories"></a><a name="BKMK_SoftwareCategories"></a> Categorías de software  
 Las categorías de software de Asset Intelligence se usan para categorizar en líneas generales los títulos de software inventariado y también como agrupaciones de alto nivel de familias de software más específicas. Por ejemplo, una categoría de software podría ser empresas de energía, y una familia de software dentro de esa categoría de software podría ser petróleo y gas o hidroeléctrica. Existen muchas categorías de software predefinidas en el catálogo Asset Intelligence y se pueden crear categorías definidas por el usuario para concretar adicionalmente el software inventariado. El estado de validación de todas las categorías de software predefinido es siempre **Validado**, mientras que el de la información de categorías de software personalizado que se hayan agregado al catálogo Asset Intelligence es **Definido por el usuario**. Para obtener más información sobre cómo administrar las categorías de software, consulte [Configuración de Asset Intelligence en System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  La información de categorías de software predefinido que se almacena en el catálogo Asset Intelligence es de solo lectura y no se puede cambiar ni eliminar. Los usuarios administrativos pueden agregar, modificar o eliminar categorías de software definidas por el usuario.  

###  <a name="a-namebkmksoftwarefamiliesa-software-families"></a><a name="BKMK_SoftwareFamilies"></a> Familias de software  
 Las familias de software de Asset Intelligence se usan para definir los títulos de software inventariado dentro de las categorías de software. Existen muchas familias de software predefinidas en el catálogo Asset Intelligence y se pueden crear categorías definidas por el usuario para concretar adicionalmente el software inventariado. El estado de validación de todas las familias de software predefinido es siempre **Validado**, mientras que el de la información de familias de software personalizado que se hayan agregado al catálogo Asset Intelligence es **Definido por el usuario**. Para obtener más información sobre cómo administrar las familias de software, consulte [Configuración de Asset Intelligence en System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  La información de la familia software predefinido es de solo lectura y no se puede cambiar. Los usuarios administrativos pueden agregar, modificar o eliminar familias de software definidas por el usuario.  

###  <a name="a-namebkmkcustomlabelsa-software-labels"></a><a name="BKMK_CustomLabels"></a> Etiquetas de software  
 Las etiquetas de software personalizado de Asset Intelligence le permiten crear filtros que puede utilizar para agrupar los títulos de software y para verlos mediante informes de Asset Intelligence. Puede utilizar etiquetas de software para crear grupos definidos por el usuario de títulos de software que compartan un atributo común. Por ejemplo, podría crear una etiqueta de software denominada Shareware, asociar dicha etiqueta con títulos de shareware inventariados y ejecutar un informe para mostrar todos los títulos de software con la etiqueta de software Shareware asociada. Las etiquetas de software no están predefinidas. El estado de validación de las etiquetas de software siempre es **Definido por el usuario**. Para obtener más información sobre cómo administrar las etiquetas de software, consulte [Configuración de Asset Intelligence en System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

###  <a name="a-namebkmkhardwarerequirementsa-hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a> Requisitos de hardware  
 Puede usar la información de requisitos de hardware para comprobar que los equipos cumplan los requisitos de hardware de los títulos de software antes de que se destinen a implementaciones de software. Puede administrar los requisitos de hardware de títulos de software en el área de trabajo **Activos y compatibilidad** , en el nodo **Requisitos de hardware** , en el nodo **Asset Intelligence** . Muchos de los requisitos de hardware están predefinidos en el catálogo Asset Intelligence, y puede crear nueva información de requisitos de hardware definida por el usuario para cumplir requisitos personalizados. El estado de validación de todos los requisitos de hardware predefinidos siempre es **Validado**, mientras que el de la información de los requisitos de hardware que se hayan agregado al catálogo Asset Intelligence es **Definido por el usuario**. Para obtener más información sobre cómo administrar los requisitos de hardware, consulte [Configuración de Asset Intelligence en System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  Los requisitos de hardware que se muestran en la consola de Configuration Manager se recuperan desde el catálogo Asset Intelligence y no se basan en información de títulos de software inventariado de clientes System Center 2012 Configuration Manager. La información de requisitos de hardware no se actualiza como parte del proceso de sincronización con System Center Online. Puede crear requisitos de hardware definidos por el usuario para software inventariado que no tenga requisitos de hardware asociados.  

 De forma predeterminada, se muestra la siguiente información por cada requisito de hardware de la lista:  

-   **Título de software**: especifica el título de software asociado con el requisito de hardware.  

-   **CPU mínima (MHz)**: especifica la velocidad del procesador mínima, en megahercios (MHz), que requiere el título de software.  

-   **RAM mínima (KB)**: especifica la memoria RAM mínima, en kilobytes (KB), que requiere el título de software.  

-   **Espacio en disco mínimo (KB)**: especifica el espacio disponible en disco duro mínimo, en KB, que requiere el título de software.  

-   **Tamaño del disco mínimo (KB)**: especifica el tamaño del disco duro mínimo, en KB, que requiere el título de software.  

-   **Estado de validación**: especifica el estado de validación del requisito de hardware.  

 Los requisitos de hardware predefinidos almacenados en el catálogo Asset Intelligence son de solo lectura y no se pueden eliminar.  Los usuarios administrativos pueden agregar, modificar o eliminar requisitos de hardware definidos por el usuario de títulos de software que no se almacenan en el catálogo Asset Intelligence.  

##  <a name="a-namebkmkinventoriedsoftwaretitlesa-inventoried-software-titles"></a><a name="BKMK_InventoriedSoftwareTitles"></a> Títulos de software inventariado  
 Puede ver la información de títulos de software inventariado en el área de trabajo **Activos y compatibilidad** del nodo **Software inventariado** en el nodo **Asset Intelligence** . El Agente cliente de inventario de hardware recopila la información de software inventariado de clientes de Configuration Manager basada en los títulos de software que se almacenan en el catálogo Asset Intelligence.  

> [!WARNING]  
>  El Agente cliente de inventario de hardware recopila inventario basándose en las clases de informes de inventario de hardware de Asset Intelligence que habilite. Para obtener más información sobre cómo habilitar las clases de informes, consulte [Configuración de Asset Intelligence en System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 De forma predeterminada, se muestra la siguiente información por cada título de software inventariado:  

-   **Nombre**: especifica el nombre del título de software inventariado.  

-   **Proveedor**: especifica el nombre del proveedor que desarrolló el título de software inventariado.  

-   **Versión**: especifica la versión de producto del título de software inventariado.  

-   **Categoría**: especifica la categoría de software que está asignada actualmente al título de software inventariado.  

-   **Familia**: especifica la familia de software que está asignada actualmente al título de software inventariado.  

-   **Etiqueta** [**1**, **2**y **3**]: especifica las etiquetas personalizadas que están asociadas con el título de software. Los títulos de software inventariado pueden tener hasta tres etiquetas personalizadas asociadas a ellos.  

-   **Recuento**: especifica el número de clientes de Configuration Manager que han inventariado el título de software.  

-   **Estado**: especifica el estado de validación del título de software inventariado.  

> [!NOTE]  
>  Puede cambiar la información de categorización (nombre de producto, proveedor, categoría de software y familia de software) del software inventariado únicamente en el sitio de nivel superior de la jerarquía. Después de modificar la información de categorización de software predefinido, el estado de validación del software cambia de **Validado** a **Definido por el usuario**.  

##  <a name="a-nameassetintelligencesycnronizationpointa-asset-intelligence-synchronization-point"></a><a name="AssetIntelligenceSycnronizationPoint"></a> Punto de sincronización de Asset Intelligence  
 El punto de sincronización de Asset Intelligence es un rol de sistema de sitio de Configuration Manager que se usa para conectarse a System Center Online (mediante el puerto TCP 443) para administrar actualizaciones dinámicas de información del catálogo Asset Intelligence. Este rol de sitio solo puede instalarse en el sitio de nivel superior de la jerarquía. Debe configurar todas las personalizaciones del catálogo Asset Intelligence mediante una consola de Configuration Manager conectada al sitio de nivel superior. Aunque todas las actualizaciones se deben configurar en el sitio de nivel superior, la información del catálogo Asset Intelligence se replica en los demás sitios de la jerarquía. El rol de sitio del punto de sincronización de Asset Intelligence le permite solicitar sincronización del catálogo a petición con System Center Online o programar una sincronización del catálogo automática. Además de descargar la nueva información del catálogo Asset Intelligence, el punto de sincronización de Asset Intelligence puede cargar la información de títulos de software personalizado en System Center Online para su categorización. Microsoft trata todos los títulos de software cargados en System Center Online para su categorización como información pública. Por lo tanto, debe asegurarse de que los títulos de software personalizado no contienen información confidencial o de propiedad.  

> [!NOTE]  
>  Después de enviar un título de software sin categoría y cuando haya al menos 4 solicitudes de categorización de clientes para el mismo título de software, los investigadores de System Center Online identifican, categorizan y ponen la información de categorización del título a disposición de todos los clientes que usen el servicio en línea. Los títulos de software que tengan la mayoría de solicitudes de categorización reciben la mayor prioridad para la categorización. El software personalizado y las aplicaciones de línea de negocio no suelen recibir una categoría y, como práctica recomendada, no se deberían enviar estos títulos de software a Microsoft para su categorización.  

> [!NOTE]  
>  Un rol de sistema de sitio de punto de sincronización de Asset Intelligence es necesario para conectarse a System Center Online. Para obtener información sobre cómo instalar un punto de sincronización de Asset Intelligence, consulte [Configuración de Asset Intelligence en System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

##  <a name="a-namebkmkassetintelligencehomepagea-asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a> Página principal de Asset Intelligence  
 El nodo **Asset Intelligence** del área de trabajo **Activos y compatibilidad** es la página principal de Asset Intelligence en Configuration Manager. En la página principal de **Asset Intelligence** se muestra una vista de panel de resumen para obtener información sobre el catálogo Asset Intelligence.  

> [!NOTE]  
>  La página principal de **Asset Intelligence** no se actualiza automáticamente mientras se está visualizando.  

 La página principal de **Asset Intelligence** contiene las siguientes secciones:  

-   **Sincronización del catálogo**: ofrece información sobre si Asset Intelligence está habilitada y sobre el estado actual del punto de sincronización de Asset Intelligence. Esta sección también facilita la programación de sincronización, si se importó el informe de licencia del cliente, cuándo se actualizó por última vez el estado y la hora de la siguiente actualización programada, y el número de cambios que se produjeron después de que se instalara el sistema de sitio del punto de sincronización de Asset Intelligence.  

    > [!NOTE]  
    >  La sección de sincronización del catálogo Asset Intelligence de la página principal de **Asset Intelligence** aparece únicamente si se instaló un rol de sistema de sitio del punto de sincronización de Asset Intelligence.  

-   **Estado de software inventariado**: ofrece el recuento y porcentaje de software inventariado, categorías de software y familias de software que identifica Microsoft o un administrador, están pendientes de identificación en línea, o no tienen identificación y no están pendientes de ella. En la información que se representa en formato de tabla se muestra el recuento de cada uno y en la información del gráfico se muestra el porcentaje.  

##  <a name="a-namebkmkassetintelligencereportsa-asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a> Informes de Asset Intelligence  
 Los informes de Asset Intelligence se encuentran en la consola de Configuration Manager, en el área de trabajo **Supervisión**, en el nodo **Informes** de la carpeta Asset Intelligence. Los informes ofrecen información sobre el hardware, la administración de licencias y el software. Para obtener más información sobre informes en Configuration Manager, consulte [Generación de informes en System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

> [!NOTE]  
>  La precisión de la cantidad títulos de software instalados y la información de licencias que se muestra en los informes de Asset Intelligence puede diferir del número real de títulos de software instalados o licencias que se utilizan en el entorno. Esta diferencia se debe a las complejas dependencias y limitaciones relacionadas con la información de licencia de software de los títulos de software que están instalados en entornos empresariales. No utilice los informes de Asset Intelligence como el único origen para determinar la compatibilidad de las licencias de software adquiridas.  

###  <a name="a-namebkmkhardwarereportsa-asset-intelligence-hardware-reports"></a><a name="BKMK_HardwareReports"></a> Informes de hardware de Asset Intelligence  
 Los informes de hardware de Asset Intelligence ofrecen información sobre los recursos de hardware de la organización. Gracias a la información de inventario de hardware, como la velocidad, la memoria, los dispositivos periféricos, etc., los informes de hardware de Asset Intelligence pueden presentar información sobre dispositivos USB, sobre hardware que debe actualizarse e incluso sobre los equipos que no estén preparados para una actualización de software concreta.  

> [!NOTE]  
>  Algunos datos de usuario de los informes de hardware de Asset Intelligence se recopilan del registro de eventos de seguridad de sistema. Para conseguir una mayor precisión en los informes, se recomienda que borre este registro cuando se reasigne un equipo a un nuevo usuario.  

###  <a name="a-namebkmklicensemanagementreportsa-asset-intelligence-license-management-reports"></a><a name="BKMK_LicenseManagementReports"></a> Informes de administración de licencias de Asset Intelligence  
 Los informes de administración de licencias de Asset Intelligence ofrecen datos sobre las licencias que se están utilizando. En el informe de contabilidad de licencias se muestra una lista de las aplicaciones de Microsoft instaladas en un formato coherente con la Declaración de licencias de Microsoft (MLS). Esto ofrece un método práctico para hacer coincidir licencias adquiridas con licencias utilizadas. Otros informes de administración de licencias ofrecen información sobre los equipos que actúan como servidores que ejecutan el Servicio de administración de claves (KMS) para las estadísticas de activaciones de sistemas operativos.  

> [!IMPORTANT]  
>  Varios de los informes de administración de licencias de Asset Intelligence presentan información sobre la función de KMS, un método de administración de licencias por volumen. Si no se ha implementado un servidor KMS, es posible que algunos informes no devuelvan datos. Para más información sobre KMS, busque KMS en [Microsoft TechNet](http://go.microsoft.com/fwlink/?linkid=3225).  

###  <a name="a-namebkmksoftwarereportsa-asset-intelligence-software-reports"></a><a name="BKMK_SoftwareReports"></a> Informes de software de Asset Intelligence  
 Los informes de software de Asset Intelligence ofrecen información sobre familias de software, categorías y títulos de software concretos que están instalados en equipos de la organización. Los informes de software presentan información sobre los objetos auxiliares del explorador, el software que se inicia automáticamente y más. Estos informes se pueden utilizar para identificar adware, spyware u otro malware, e identificar redundancia de software para ayudar a agilizar el soporte y la adquisición de software.  

###  <a name="a-namebkmksoftwareidtagreportsa-asset-intelligence-software-identification-tag-reports"></a><a name="BKMK_SoftwareIdTagReports"></a> Informes de etiquetas de identificación de software de Asset Intelligence  
 Los informes de etiquetas de identificación de software de Asset Intelligence ofrecen información sobre software que contiene una etiqueta de identificación de software que es compatible con ISO/IEC 19770-2. Las etiquetas de identificación de software ofrecen información autoritativa que se utiliza para identificar el software instalado. Si habilita la clase de informes de inventario de hardware SMS_SoftwareTag, Configuration Manager recopila información sobre el software con etiquetas de identificación de software. En los informes siguientes se ofrece información sobre el software:  

-   **Software 14A - Búsqueda de software con etiqueta de identificación de software habilitada**: en este informe se ofrece el recuento de software instalado con una etiqueta de identificación de software habilitada.  

-   **Software 14B - Equipos con etiqueta de identificación de software específica habilitada instalada**: en este informe se muestran todos los equipos que tienen instalado software con una etiqueta de identificación de software concreta habilitada.  

-   **Software 14C - Software instalado con etiqueta de identificación de software habilitada en un equipo específico**: en este informe se muestra una lista de todo el software instalado con una etiqueta de identificación de software concreta habilitada en un equipo determinado.  

###  <a name="a-namebkmkreportinglimitationsa-asset-intelligence-reporting-limitations"></a><a name="BKMK_ReportingLImitations"></a> Limitaciones de los informes de Asset Intelligence  
 Los informes de Asset Intelligence pueden ofrecer una gran cantidad de información sobre los títulos de software instalados y las licencias de software adquiridas que se están utilizando. Sin embargo, no debe usar esta información como el único origen para determinar el cumplimiento de las licencias de software adquiridas.  

####  <a name="a-namebkmkexampledependenciesa-example-dependencies"></a><a name="BKMK_ExampleDependencies"></a> Dependencias de ejemplo  
 La precisión de la cantidad mostrada en los informes de Asset Intelligence sobre los títulos de software instalados y la información de licencias puede variar de las cifras reales que se utilicen actualmente. Esta diferencia se debe a las complejas dependencias relacionadas con la información de licencia de software de los títulos de software que se usan en entornos empresariales. En los ejemplos siguientes se muestran las dependencias relacionadas con el inventario del software instalado en la empresa mediante el uso de Asset Intelligence que podrían afectar a la precisión de los informes de Asset Intelligence:  

 **Dependencias del inventario de hardware del cliente**  
 Los informes del software instalado de Asset Intelligence se basan en datos que se recopilan de clientes de Configuration Manager mediante la ampliación del inventario de hardware para habilitar los informes de Asset Intelligence. Debido a esta dependencia de los informes de inventario de hardware, los informes de Asset Intelligence reflejan solo los datos de clientes de Configuration Manager que completen correctamente los procesos de inventario de hardware con las clases de informes de WMI de Asset Intelligence habilitadas. Además, como los clientes de Configuration Manager realizan procesos de inventario de hardware según una programación definida por el usuario administrativo, puede producirse un retraso en los informes de datos que afecte a la precisión de los informes de Asset Intelligence. Por ejemplo, un título de software con licencia inventariado podría desinstalarse después de que el cliente finalice un ciclo de inventario de hardware correcto. En cambio, el título del software se mostrará como instalado en los informes de Asset Intelligence hasta el siguiente ciclo de informes de inventario de hardware del cliente programado.  

 **Dependencias de paquetes de software**  
 Como los informes de Asset Intelligence se basan en datos de títulos de software instalados que se recopilan mediante procesos estándares de inventario de hardware de cliente de Configuration Manager, es posible que parte de los datos de los títulos de software no se recopilen correctamente. Por ejemplo, las instalaciones de software que no cumplen con los procesos de instalación estándares o las que se cambiaron antes de la instalación podrían provocar informes de Asset Intelligence imprecisos.  

####  <a name="a-namebkmklegallimitationsa-legal-limitations"></a><a name="BKMK_LegalLimitations"></a> Limitaciones legales  
 La información que se muestra en los informes de Asset Intelligence está sujeta a muchas limitaciones y dicha información no representa asesoramiento profesional legal, de contabilidad ni de ningún otro tipo. La información que ofrece Asset Intelligence es solo informativa y no debe utilizarse como el único origen de información para determinar el cumplimiento de uso de licencias de software.  

 A continuación se muestran ejemplos de limitaciones relacionadas con el inventario del software instalado y el uso de licencias en la empresa mediante el uso de Asset Intelligence que podría afectar a la precisión de los informes de Asset Intelligence:  

 **Limitaciones de cantidad de usos de las licencias de Microsoft**  
 -   La cantidad de licencias de software de Microsoft adquiridas se basa en la información que facilitan los administradores y se debe revisar con cuidado para asegurarse de que se ofrece el número correcto de licencias de software.  

-   La cantidad de licencias de software de Microsoft que se muestra en el informe solo contiene información sobre licencias de software de Microsoft adquiridas a través de programas de licencias por volumen y no refleja la información de licencias de software adquiridas a través de minoristas, OEM u otros canales de ventas de licencias de software.  

-   Las licencias de software adquiridas en los últimos 45 días podrían no incluirse en la cantidad de licencias de software de Microsoft que se muestra en el informe, debido a las programaciones y los requisitos de informes de los distribuidores de software.  

-   Las transferencias de licencias de software de las fusiones o adquisiciones entre compañías podrían no reflejarse en las cantidades de licencias de software de Microsoft.  

-   Los términos y condiciones no estándares de un acuerdo de licencias por volumen de Microsoft (MVLS) podrían afectar al número de licencias de software que aparecen en el informe y, por tanto, podría ser necesario que un representante de Microsoft realizara revisiones adicionales.  

 **Limitaciones de cantidades de títulos de software instalados**  
 Los clientes de Configuration Manager deben completar correctamente los ciclos de informes de inventario de hardware de los informes de Asset Intelligence para notificar con exactitud la cantidad de títulos de software instalados. Además, podría producirse un retraso entre la instalación o desinstalación de un título de software con licencia, después de un ciclo de informes de inventario de hardware correcto que no se refleje en los informes de Asset Intelligence que se ejecutaron antes de que el cliente informe del siguiente inventario de hardware programado.  

 **Limitaciones de conciliación de licencias**  
 El equilibrio entre la cantidad de títulos de software instalados con respecto a la cantidad de licencias de software adquiridas se calcula mediante una comparación entre la cantidad de licencias que especifica el administrador y el número de títulos de software instalados, recopilados de los inventarios de hardware de los clientes de Configuration Manager, según la programación establecida por el administrador. Esta comparación no representa una conclusión final de Microsoft sobre las situaciones de las licencias. La situación real de las licencias depende de las licencias de los títulos de software concretos y los derechos de uso que conceden los términos de licencia.  

##  <a name="a-namebkmkvalidationstatesa-asset-intelligence-validation-states"></a><a name="BKMK_ValidationStates"></a> Estados de validación de Asset Intelligence  
 Los estados de validación de Asset Intelligence representan el estado de validación actual y el original de la información del catálogo Asset Intelligence. En la tabla siguiente se muestran los posibles estados de validación de Asset Intelligence y las acciones de administrador que pueden provocarlos.  

|**Estado**|**Definición**|**Acción de administrador**|**Comentario**|  
|---------------|--------------------|------------------------------|-----------------|  
|**Validado**|Los investigadores de System Center Online definieron el elemento del catálogo.|Ninguna.|Mejor estado.|  
|**Definido por el usuario**|Los investigadores de System Center Online aún no han definido el elemento del catálogo.|Se personalizó la información del catálogo local.|Este estado se muestra en los informes de Asset Intelligence.|  
|**Pendiente**|Los investigadores de System Center Online no definieron el elemento del catálogo, pero el elemento se envió a System Center Online para su categorización.|Categorización de System Center Online solicitada.|El elemento del catálogo permanece en este estado hasta que los investigadores de System Center Online categoricen el elemento y se sincronice el catálogo Asset Intelligence.|  
|**Actualizable**|System Center Online ha categorizado de forma diferente un elemento de catálogo definido por el usuario durante una sincronización del catálogo posterior.|Se personalizó el catálogo Asset Intelligence local para categorizar un elemento como definido por el usuario.|Puede usar la acción Resolver conflicto para decidir si quiere usar la nueva información de categorización o el valor definido por el usuario anterior. Para obtener más información sobre cómo resolver conflictos, consulte [Operaciones de Asset Intelligence en System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).|  
|**Sin categoría**|Los investigadores de System Center Online no han definido el elemento del catálogo, el elemento no se ha enviado a System Center Online para su categorización y el administrador no ha asignado un valor de categorización definido por el usuario.|Ninguna.|Solicitar categorización o personalizar la información del catálogo local.<br /><br /> Para obtener más información sobre cómo solicitar la categorización, consulte [Operaciones de Asset Intelligence en System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).<br /><br /> Para obtener más información sobre cómo cambiar la categoría del título de software, consulte [Operaciones de Asset Intelligence en System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).|  

> [!NOTE]  
>  Los elementos del catálogo enviados a System Center Online para su categorización tienen un estado de validación **Pendiente** en un sitio de administración central, pero se siguen mostrando con un estado de validación **Sin categoría** en los sitios primarios secundarios.  

> [!NOTE]  
>  Después de resolver un conflicto de categorización, el elemento no se valida de nuevo como en conflicto a menos que haya actualizaciones de categorización posteriores que introduzcan nueva información sobre el elemento.  

 Para obtener ejemplos de cuándo puede pasar un estado de validación de un estado a otro, consulte [Example validation state transitions for Asset Intelligence in System Center Configuration Manager (Transiciones de estado de validación de ejemplo para Asset Intelligence en System Center Configuration Manager)](../../../../core/clients/manage/asset-intelligence/example-validation-state-transitions-for-asset-intelligence.md).  



<!--HONumber=Dec16_HO3-->


