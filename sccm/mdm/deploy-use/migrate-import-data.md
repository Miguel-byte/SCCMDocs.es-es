---
title: "Importación de datos en Microsoft Intune"
titleSuffix: Configuration Manager
description: 
keywords: 
author: dougeby
manager: dougeby
ms.date: 12/05/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.openlocfilehash: d42a5fd64b5baead8ef87d8c08a99ec659f94633
ms.sourcegitcommit: 8c6e9355846ff6a73c534c079e3cdae09cf13c45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/06/2017
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>Importación de datos de Configuration Manager en Microsoft Intune 

*Se aplica a: System Center Configuration Manager (Rama actual)*    

El primer paso recomendado del proceso de [migrar dispositivos y usuarios de MDM híbrida a Intune independiente](migrate-hybridmdm-to-intunesa.md) en la configuración solo en la nube consiste en utilizar la herramienta Intune Data Importer. Si lo desea, puede omitir esta fase y pasar a la de [preparación de Intune para migrar usuarios](migrate-prepare-intune.md). Sin embargo, esta herramienta realiza las siguientes funciones que pueden ahorrarle mucho tiempo en la fase siguiente: 
1.  Recopila datos sobre los objetos seleccionados de la jerarquía de Configuration Manager. 
2.  Proporciona detalles sobre los objetos que puede seleccionar para la importación, además de información sobre por qué no se pueden importar algunos objetos.
3.  Importa los objetos seleccionados en el inquilino de Microsoft Intune. 

La herramienta Data Importer no cambia su entorno de Configuration Manager. Por lo tanto, puede importar objetos en Intune y validar que todo funciona según lo esperado sin riesgo de dejar los dispositivos de MDM híbrida en un estado de no administrados. 

## <a name="what-objects-can-this-tool-import"></a>¿Qué objetos puede importar esta herramienta?
La herramienta de importación puede recopilar información sobre los siguientes tipos de objetos de Configuration Manager; además, proporciona información sobre si se pueden importar los objetos recopilados: 
- Elementos de configuración
- Perfiles de certificado
- Perfiles de correo electrónico
- Perfiles de VPN
- Perfiles de Wi-Fi
- Directivas de cumplimiento
- Aplicaciones
- Implementaciones

> [!Note]    
> La importación de implementaciones solo es útil para otros tipos de objeto que vaya a importar. Por ejemplo, si importa implementaciones y perfiles de VPN, solo podrá importar las implementaciones de los perfiles de VPN seleccionados. Las implementaciones en Intune se denominan "asignaciones". Si desea importar una implementación de un objeto previamente importado, debe importar ese objeto otra vez o crear manualmente la asignación en Intune en Azure. Por ejemplo, si importa los perfiles de VPN y no las implementaciones, tendrá que volver a ejecutar la herramienta y seleccionar las implementaciones y los perfiles de VPN, o bien crear manualmente la asignación en Intune en Azure.  Si vuelve a ejecutar la herramienta, se pueden crear objetos duplicados que puede eliminar más adelante en Intune en Azure.  

> [!Important]    
> Si la recopilación de una implementación se basa en un grupo de Active Directory que se ha replicado a Azure Active Directory (AAD), la herramienta automáticamente destinará los objetos migrados a los grupos si se selecciona la implementación adecuada al ejecutar la herramienta. Cuando haya recopilaciones más complejas o de pertenencia directa, manualmente, debe volver a crearlos en AAD y destinar las asignaciones de objetos a dichos objetos en Intune en Azure.


## <a name="things-to-know-before-you-run-the-tool"></a>Aspectos que debe conocer antes de ejecutar la herramienta
- Al ejecutar la herramienta, no se modificará el entorno de Configuration Manager.
- Le recomendamos que primero pruebe el proceso de importación de datos con un inquilino de prueba. Después de confirmar que se han importado los datos que esperaba, puede realizar el mismo proceso con el inquilino de Intune de producción.
- La herramienta de importación de datos está diseñada para importar solo datos de Configuration Manager una vez. No realiza un seguimiento de los objetos de Configuration Manager o Intune. Sin embargo, si ejecuta el importador de nuevo en el mismo equipo de antes, le indicará qué objetos se importaron anteriormente. La herramienta no podrá saber si el objeto sigue existiendo en Intune o si uno ha cambiado. Si importa datos en Intune más de una vez, puede acabar teniendo objetos duplicados.
- No todas las configuraciones de perfil se pueden importar. Por ejemplo, no se puede importar el modo de pantalla completa o la configuración de PFX. 
- Si tiene una directiva de Configuration Manager con una configuración que no se corresponde con las plataformas seleccionadas, la herramienta podría omitir esta configuración durante la importación. Omitir la configuración ayuda a garantizar que la directiva pueda importarse y que sea compatible con Intune. 
- La herramienta tratará de proporcionar un motivo por el cual no se puede importar un objeto. En algunos casos, antes de importar objetos en Intune, puede ir a la consola de Configuration Manager, corregir el problema, iniciar de nuevo el examen de detección de objetos de Configuration Manager y, luego, importar los objetos. A veces, puede que necesite o desee volver a crear estos objetos manualmente en Intune.
- Hay algunos perfiles que dependen de otros objetos. Si desea importar un perfil que depende de otro objeto, como uno de correo electrónico que depende de un certificado, debe importar ambos objetos al mismo tiempo a menos que haya importado previamente el otro objeto desde el mismo equipo con el mismo usuario.  
- Después de ejecutar la herramienta, deberá realizar algunos pasos manuales más. Por ejemplo, destinar aplicaciones y directivas a grupos de AAD. 

## <a name="prerequisites"></a>Requisitos previos
- Versión 1610 de Configuration Manager o una posterior: se recomienda especificar el sitio de nivel superior y ejecutar la herramienta con un usuario que tenga acceso a todos los objetos de la jerarquía del sitio. La herramienta solo detecta los objetos a los que puede acceder el usuario que ejecuta la herramienta. 
- Un administrador global debe ejecutar la herramienta Data Importer la primera vez con el siguiente parámetro: ***intunedataimporter.exe -GlobalConsent***. Después, un administrador global o de Intune puede ejecutar la herramienta.  


<!-- ## Objects that cannot be imported
There are some Configuration Manager objects that the importer tool cannot import to Intune. You must manually create these objects in Intune. 
- Collections based on direct membership or that are based on a query. The only collections that are imported are based on a single AD group. For all other collections, you must create the assignment in Intune and add the assignment to the appropriate objects. 
- Profiles <list what we cannot import>
- Policies <??>
- Etc.
-->

## <a name="download-the-data-importer-tool"></a>Descarga de la herramienta Data Importer
La herramienta Data Importer está disponible para descargarse en el repositorio ConfigMgrTools/Intune-Data-Importer de GitHub. Use el procedimiento siguiente para descargar la herramienta.

1. Vaya a la página de [versiones de GitHub para Intune Data Importer](https://github.com/ConfigMgrTools/Intune-Data-Importer/releases).
2. Para la versión más reciente, haga clic en **Microsoft.Intune.Data.Importer.exe**.
3. Guarde y ejecute (o simplemente ejecute) el archivo .exe y luego elija una carpeta de destino para extraer la herramienta Intune Data Importer.

## <a name="run-the-data-importer-tool"></a>Ejecución de la herramienta Data Importer
Los pasos principales del Asistente para la herramienta Data Importer se pueden dividir en tres. En esta sección se proporciona información para ayudarlo a completar cada sección del asistente y a importar correctamente los datos de Configuration Manager en Intune. Cada paso continúa donde termina el anterior.

### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>Concesión de permiso a la herramienta Data Importer para acceder a los recursos
Antes de poder ejecutar la herramienta Data Importer, debe utilizar una cuenta de administrador global para conceder permiso en Azure a la herramienta Data Importer con el fin de que pueda acceder a los recursos. Después, puede ejecutar la herramienta con una cuenta de administrador global o de administrador de Intune.   

1.  Un administrador global debe ejecutar la herramienta la primera vez con el siguiente parámetro: ***intunedataimporter.exe -GlobalConsent***. 
2. Cuando se inicia la herramienta, se muestra una pantalla de inicio de sesión donde debe iniciar sesión con una cuenta con el rol de administrador global de Azure. 
3. Haga clic en **Accept** (Aceptar) para crear una aplicación en Azure con los derechos adecuados en Microsoft Graph. La herramienta Data Importer necesita estos derechos para importar objetos en Microsoft Intune.   

   > [!Important]
   > Al hacer clic en **Accept** (Aceptar), conceda permiso a la herramienta para hacer lo siguiente:
   > - Leer todos los grupos
   > - Iniciar sesión y leer el perfil de usuario
   > - Leer y escribir las directivas y la configuración de dispositivos de Intune
   > - Leer y escribir aplicaciones de Intune
   > - Leer y escribir las directivas de control de administración basada en roles de Intune
   > - Leer y escribir en dispositivos de Intune
   > - Leer y escribir la configuración de Intune
1. Después de aceptar el consentimiento, cualquier otro administrador global o de Intune puede ejecutar la herramienta para importar datos de Configuration Manager en Intune en Azure.    
        
    > [!Note]
    > Si antes un administrador global no ha dado el consentimiento, la herramienta puede mostrar el mensaje **You can't access this application** (No puede acceder a esta aplicación) después de que un administrador de Intune ejecute la herramienta Data Importer e inicie sesión en la suscripción de Intune.

### <a name="manually-map-collections-to-azure-ad-groups"></a>Asignación manual de recopilaciones a grupos de Azure AD
Al ejecutar la herramienta Data Importer, se extrae el nombre del grupo de AD de las recopilaciones con una única regla que tiene como destino un único grupo de AD. Cuando las asignaciones se crean en Intune, Data Importer busca un grupo de Azure AD con el mismo nombre que el grupo de AD y, si existe, se asigna el objeto importado a ese grupo de Azure AD. Puede invalidar el nombre del grupo de AD que Data Importer busca para una recopilación y proporcionar uno o varios grupos de Azure AD que se utilizarán para esa colección. El uso del archivo de asignación de la recopilación proporciona una manera de asignar recopilaciones que normalmente no se importan con Data Importer a grupos de Azure AD.
#### <a name="find-the-collections-that-cannot-be-imported"></a>Búsqueda de recopilaciones que no se pueden importar
Puede obtener una lista de todas las colecciones que no se pueden importar de forma que pueda agregarlas al archivo .csv de asignación de colecciones. 
1. Ejecute la herramienta Data Importer y seleccione los objetos que desea importar. Utilice los procedimientos que se describen en [Fase 1: Detectar objetos de Configuration Manager y recopilar datos](#phase-1:-discover-configuration-manager-objects-and-collect-data) y [Fase 2: Resolver problemas y seleccionar los objetos que se van a importar](#phase-2:-resolve-issues-and-select-the-objects-to-import) para detectar y elegir los objetos. Después, en la página **Summary (Resumen)**, elija **Export details (Exportar detalles)** para crear un archivo .csv con detalles de todo lo seleccionado para importar, incluidos los objetos que no se pueden importar y las implementaciones. 
2. Abra el archivo .csv en Microsoft Excel y filtre los datos en función de **Deployment** (Implementación) para la columna **Type** (Tipo) y **No** para la columna **Importable**. La columna del nombre de la recopilación muestra todas las recopilaciones que deben agregarse a un archivo de asignación de recopilaciones para que las implementaciones se puedan importar.

#### <a name="create-the-collection-mapping-file"></a>Creación del archivo de asignación de recopilaciones
El archivo de asignación de recopilaciones es un archivo de valores separados por comas (CSV), donde la primera columna es el nombre de la recopilación de Configuration Manager y la segunda columna es el nombre del grupo de Azure AD que se utilizará para esa recopilación. Para especificar más de un grupo de Azure AD para una sola recopilación de Configuration Manager, cree varias filas en el archivo CSV con ese nombre de archivo de asignación de recopilaciones. El ejemplo siguiente es un archivo CSV que contiene dos recopilaciones. La primera recopilación está asignada a un solo grupo de Azure AD y la segunda recopilación está asignada a dos grupos de Azure AD.

![Ejemplo de archivo csv de asignación de recopilaciones](..\media\migrate-collectionmapping.png)

#### <a name="start-the-data-importer-tool-using-collection-mapping"></a>Inicie la herramienta Data Importer mediante la asignación de recopilaciones
Para usar un archivo de asignación de recopilaciones, debe iniciar la herramienta Data Importer utilizando el parámetro de línea de comandos *-CollectionMappingFile* y la ruta de acceso completa al archivo .csv de asignación de recopilaciones que crea. Por ejemplo:

```IntuneDataImporter.exe -CollectionMappingFile c:\Users\myuser\Documents\collectionmapping.csv```

> [!Note]
> Data Importer no muestra nada en ninguna página de asistente para indicar que el archivo de asignación de recopilaciones se cargó. Sin embargo, la herramienta muestra los errores encontrados al leer el archivo .csv. Además, en la página **Summary** (Resumen) del asistente puede revisar los tipos **Deployment** (Implementación). La herramienta muestra **Yes** (Sí) en la columna Importable y enumera los grupos de Azure AD que asignará a los objetos de la columna **Notes** (Notas).

### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>Fase 1: Detectar objetos de Configuration Manager y recopilar datos
En la fase 1, seleccione los objetos para detectar e indique a la herramienta que recopile información sobre los objetos seleccionados. 
1. Abra la herramienta y haga clic en **Start** (Iniciar).  
2. Lea la información y, luego, haga clic en **Next** (Siguiente). 
3. Elija si desea importar un conjunto de datos exportado previamente o seleccione los tipos de objeto que desea importar:
   - **Importar conjunto de datos exportado previamente**: elija **Import data set exported from a previous run of Intune Data Importer** (Importar conjunto de datos exportado desde una ejecución anterior de Intune Data Importer) y haga clic en **Browse** (Examinar) para **Exported data folder** (Carpeta de datos exportados) para seleccionar un conjunto de datos que haya exportado previamente con la herramienta Data Importer. El usuario que importa el conjunto de datos debe ser el mismo usuario que exportó los datos. Después de importar los datos, se muestra un resumen de los objetos en la página **Summary** (Resumen) del asistente. Si el resumen es correcto, vaya a [Fase 3: Importar objeto seleccionado a Intune](phase-3:-import-selected-object-to-intune).
 
      > [!Note]
      > Después de detectar y seleccionar los objetos en el sitio para importar, puede exportar los objetos a un conjunto de datos en la página **Sign-in to Intune** (Iniciar sesión en Intune). Después, puede importar el conjunto de datos en esta página. El conjunto de datos se cifra mediante las credenciales de usuario de Windows del usuario que ha iniciado sesión, por lo que solo el usuario que exportó el conjunto de datos puede importar dicho conjunto de datos en la herramienta. 
   - **Seleccionar tipos de objetos para importar**: elija **Select object types to import** (Seleccionar tipos de objeto para importar) para seleccionar los tipos de objetos para importar y detectar objetos en su entorno. Proporcione la siguiente información sobre el sitio y los objetos que desea importar.
      - **Site server name** (Nombre del servidor de sitio): proporcione el nombre de dominio completo del servidor de sitio para importar objetos. La herramienta solo detecta los objetos a los que puede acceder el usuario que ejecuta la herramienta. Normalmente, tendrá que especificar el sitio de nivel superior y ejecutar la herramienta con un usuario que tenga acceso a todos los objetos de la jerarquía del sitio.
      - **Site code** (Código de sitio): proporcione el código de sitio del servidor de sitio. Puede encontrar el código de tres letras en la parte superior de la consola de Configuration Manager.
      - **Object types to import** (Tipos de objeto para importar): elija los objetos que desea que la herramienta recopile. Puede elegir **Select all** (Seleccionar todo) para elegir todos los objetos o tipos de objeto concretos. 
4.  Haga clic en **Next** (Siguiente) para iniciar la detección de los objetos en el sitio. La herramienta muestra el progreso de cada uno de los tipos de objeto. 
    - Cuando la herramienta no detecta ningún dato de un tipo de objeto seleccionado, la barra de progreso se muestra inmediatamente como completada en ese tipo de objeto.
    - Los objetos que no se seleccionaron no se muestran en la página de datos **Collect** (Recopilar). 
    - Puede volver a ejecutar la herramienta para los objetos que no se recopilaron o que canceló durante el proceso de recopilación.

### <a name="phase-2-resolve-issues-and-select-the-objects-to-import"></a>Fase 2: Resolver problemas y seleccionar los objetos que se van a importar  
En la fase 2, revise los objetos que detectó la herramienta, resuelva los problemas que impiden que el objeto se importe en Intune y elija los objetos que se van a importar. Si soluciona los problemas, vuelva a la página **Discover environment** (Entorno de detección) del Asistente para volver a detectar objetos. 
5.  Haga clic en **Next** (Siguiente) para revisar los objetos recopilados. Hay disponible una página de selección de elementos para cada tipo de objeto recopilado. 
 <!--   > [!Tip]     
    > On each item selection page, you can create a filter to help you find the objects that you want to import. However, take note of the following:
    > - When you are on an item selection page and the view is filtered, the Select all checkboxes only apply to the displayed items. Any hidden objects because of a filter are not included when using the checkboxes.
    > - Objects are always grouped under their parent item even when you sort or filter the objects.
-->
6.  En cada página de selección de elementos, ordene los objetos por la columna Importable y revise los objetos que no se pueden importar. La información de la columna Notes (Notas) proporciona detalles sobre por qué la herramienta no puede importar el objeto. 
7.  Ahora debe decidir si desea corregir alguno de los problemas de los objetos que no se pueden importar. Si corrige uno o varios problemas, haga clic en Previous (Anterior) hasta que llegue a la página Select data from Configuration Manager (Seleccionar datos de Configuration Manager) y recopile los datos de nuevo para ver si se ha resuelto el problema. Puede seguir corrigiendo problemas hasta que esté satisfecho con los objetos que se pueden importar. 
8.  En cada página de selección de elementos, seleccione los objetos que se van a importar. Se muestran las siguientes columnas:
    - **Name** (Nombre): el nombre del objeto de Configuration Manager. 
    - **Importable**: especifica si se puede importar un objeto. Solo puede elegir objetos que tengan Yes (Sí) en la columna Importable. 
    - **Plataform** (Plataforma): especifica la plataforma que admite el objeto.
    - **Already imported** (Ya importados): especifica si el objeto ya se ha importado con la herramienta en este equipo. 
    - **Is superseded** (Se reemplazó): especifica si la aplicación ha sido reemplazada por otra aplicación. Debe activar la casilla **Show superseded apps** (Mostrar aplicaciones reemplazadas) en la parte superior de la página para que se muestren las aplicaciones reemplazadas.
    - **Notes** (Notas): proporciona información sobre por qué no se puede importar un objeto. La columna **Notes** (Notas) también muestra información sobre la configuración que se omitió (para algunos tipos de objetos), pero el objeto todavía se puede importar sin esa configuración.
    - **Configuration baselines** (Líneas base de configuración) (para los elementos de configuración): especifica las líneas base de configuración que están asociadas a un elemento de configuración.
    - **Required certificate** (Certificado necesario) (para los perfiles y las directivas): especifica si un certificado está asociado con el objeto. Cuando lo está, debe importar también certificado.
9.  Después de elegir los objetos que se van a importar, aparecen en la página Summary (Resumen). Están disponibles las siguientes acciones: 
    - **Export details** (Exportar detalles): crea un archivo .csv que contiene la información que aparece en la pantalla. También muestra los objetos que no se pueden importar y el motivo por el que no se pueden importar. Puede mantener este archivo para tenerlos como referencia. 
    - **Export error data** (Exportar datos de errores): exporta un archivo comprimido que contiene información sobre los datos que la herramienta no pudo convertir ni importar. 

### <a name="phase-3-import-selected-objects-to-intune"></a>Fase 3: Importar objeto seleccionado a Intune
En la fase 3, podrá iniciar sesión en Intune e importar los objetos seleccionados. 
10. Haga clic en **Next** (Siguiente) y, después, en **Sign in to Intune** (Iniciar sesión en Intune) con el objetivo de iniciar sesión en el inquilino de Intune para importar los datos o elija exportar los datos.

    - **Export** (Exportar): después de detectar y seleccionar los objetos en el sitio para importar, puede exportar los objetos a un conjunto de datos. Esto le permite detectar objetos desde un equipo que no tiene acceso a Internet, exportar los datos y luego importar dichos datos desde un equipo que tenga acceso a Internet. El conjunto de datos se cifra mediante las credenciales de usuario de Windows del usuario que ha iniciado sesión, por lo que solo el usuario que exportó el conjunto de datos puede importar dicho conjunto de datos en la herramienta. Cuando elija esta opción, elija la ruta de acceso a los datos exportados. 
      1. Haga clic en **Export** (Exportar) en la página **Sign in to Intune** (Iniciar sesión en Intune). 
      2. Haga clic en **Browse** (Examinar) para seleccionar la carpeta de destino para la exportación. La carpeta debe estar vacía. 
      3. Haga clic en **Start**  (Iniciar) para exportar los datos y, cuando finalice la exportación, haga clic en **Close** (Cerrar) para completar el asistente y cerrar Data Importer.
      4. Inicie Data Importer desde otro equipo con acceso a Internet utilizando las mismas credenciales y seleccione **Import previously exported data set** (Importar conjunto de datos previamente exportado) en la segunda página del asistente. Una vez importados los datos, el asistente le llevará a la página **Sign in to Intune** (Iniciar sesión en Intune). 
    - **Iniciar sesión en Intune** (Iniciar sesión en Intune): debe iniciar sesión con una cuenta de administrador global o de administrador de Intune. Después de iniciar la sesión, se inicia el proceso de importación.
    
      > [!Important]
      > Le recomendamos que primero pruebe el proceso de importación de datos con un inquilino de prueba. Después de confirmar que se han importado los datos que esperaba, puede realizar el mismo proceso con el inquilino de Intune de producción.
12. La página Progress (Progreso) muestra el progreso de la importación de los objetos. Haga clic en **Next** (Siguiente) cuando finalice la importación. 
13. En la página Completion (Finalización), se enumeran los objetos importados. Compruebe el estado de todos los objetos en los que se detectó un error durante el proceso de importación. Están disponibles las siguientes acciones: 
    - **Export details** (Exportar detalles): crea un archivo .csv que contiene la información que aparece en pantalla. Puede mantener este archivo para tenerlos como referencia. 
    - **Export error data** (Exportar datos de errores): exporta un archivo comprimido que contiene información sobre los datos que la herramienta no pudo convertir ni importar.

## <a name="next-steps"></a>Pasos siguientes
Después de importar los datos en Intune, debe realizar los pasos de [preparación de Intune para la migración de usuarios](migrate-prepare-intune.md). 