---
title: Importación de datos en Microsoft Intune
titleSuffix: Configuration Manager
description: Importación de datos de Configuration Manager en Microsoft Intune
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18c8bab6b072a9df2dea9c9f67d844b8481d314e
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678212"
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>Importación de datos de Configuration Manager en Microsoft Intune 

*Se aplica a: System Center Configuration Manager (Rama actual)*    

El primer paso recomendado del proceso de [migrar dispositivos y usuarios de MDM híbrida a Intune independiente](migrate-hybridmdm-to-intunesa.md) en la configuración solo en la nube consiste en utilizar la herramienta Intune Data Importer. Si lo desea, puede omitir esta fase y pasar a la de [preparación de Intune para migrar usuarios](migrate-prepare-intune.md). Sin embargo, esta herramienta realiza las siguientes funciones que pueden ahorrarle mucho tiempo en la fase siguiente:  

1. Recopila datos sobre los objetos seleccionados de la jerarquía de Configuration Manager.  

2. Proporciona detalles sobre los objetos que puede seleccionar para la importación, además de información sobre por qué no se pueden importar algunos objetos.  

3. Importa los objetos seleccionados en el inquilino de Microsoft Intune.  

La herramienta Data Importer no cambia el entorno de Configuration Manager en modo alguno. Puede importar objetos en Intune y validar que todo funciona según lo esperado sin riesgo de dejar los dispositivos MDM híbrida en un estado no administrado. 


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
> La importación de implementaciones solo es útil para otros tipos de objeto que vaya a importar. Por ejemplo, si importa implementaciones y perfiles de VPN, solo podrá importar las implementaciones de los perfiles de VPN seleccionados. Las implementaciones en Intune se denominan "asignaciones". Si desea importar una implementación de un objeto previamente importado, debe importar ese objeto otra vez o crear manualmente la asignación en Intune en Azure. Por ejemplo, si importa los perfiles de VPN y no las implementaciones, tendrá que volver a ejecutar la herramienta y seleccionar las implementaciones y los perfiles de VPN, o bien crear manualmente la asignación en Intune en Azure. Si vuelve a ejecutar la herramienta, se pueden crear objetos duplicados que puede eliminar más adelante en Intune en Azure.  

> [!Important]  
> Si la colección para una implementación se basa en un grupo de Active Directory que se han replicado en Azure Active Directory (Azure AD), la herramienta tiene como destino automáticamente los objetos migrados a los grupos si se selecciona la implementación adecuada al ejecutar la herramienta. Cuando haya recopilaciones más complejas o recopilaciones de pertenencia directa, que debe volver a crearlas manualmente en Azure AD y de destino manualmente las asignaciones de objetos a ellos en Intune en Azure.  


## <a name="things-to-know-before-you-run-the-tool"></a>Aspectos que debe conocer antes de ejecutar la herramienta

- Ejecutar la herramienta no cambiará su entorno de Configuration Manager en modo alguno.  

- En primer lugar, pruebe el proceso de importación de datos con un inquilino de prueba. Después de confirmar que los datos esperados se ha importado, puede ir a través del mismo proceso con el inquilino de Intune de producción.  

- La herramienta de importación de datos está diseñada para importar solo datos de Configuration Manager una vez. No realiza un seguimiento de los objetos de Configuration Manager o Intune. Sin embargo, si ejecuta el importador de nuevo en el mismo equipo como antes, le indica qué objetos se importaron anteriormente. La herramienta no sabe si el objeto sigue existiendo en Intune o si un objeto ha cambiado. Si importa datos en Intune más de una vez, puede acabar teniendo objetos duplicados.  

- No todas las configuraciones de perfil se pueden importar. Por ejemplo, no se puede importar la configuración de PFX o de modo de pantalla completa.  

- Si tiene una directiva de Configuration Manager con una configuración que no es aplicables a las plataformas seleccionadas, la herramienta podría omitir esta configuración durante la importación. Omitir la configuración ayuda a garantizar que la directiva pueda importarse y que sea compatible con Intune.  

- La herramienta intenta proporcionar un motivo de por qué no se puede importar un objeto. En algunos casos, antes de importar objetos en Intune, puede ir a la consola de Configuration Manager, corregir el problema, iniciar de nuevo el examen de detección de objetos de Configuration Manager y, luego, importar los objetos. A veces, puede que necesite o desee volver a crear estos objetos manualmente en Intune.  

- Hay algunos perfiles que dependen de otros objetos. Si desea importar un perfil que depende de otro objeto, como uno de correo electrónico que depende de un certificado, debe importar ambos objetos al mismo tiempo a menos que haya importado previamente el otro objeto desde el mismo equipo con el mismo usuario.  

- Después de ejecutar la herramienta, deberá realizar algunos pasos manuales más. Por ejemplo, destinar aplicaciones y directivas a grupos de Azure AD.  

- Si las aplicaciones web (a veces denominadas webclips) se han asignado a los usuarios, debe quitar esas aplicaciones web antes de migrar los usuarios. A continuación, volver a asignar las aplicaciones web una vez completada la migración. Si no hace esta acción, los clips web será imposible de administrar después de la migración.  


## <a name="prerequisites"></a>Requisitos previos

- Especifique el sitio de nivel superior y ejecutar la herramienta con un usuario que tenga acceso a todos los objetos de la jerarquía de sitios. La herramienta solo detecta los objetos a los que puede acceder el usuario que ejecuta la herramienta.  

- Un administrador Global debe ejecutar la herramienta Data Importer la primera vez que se usa el parámetro - GlobalConsent. A continuación, un administrador Global o administrador de Intune puede ejecutar la herramienta. 

- Ejecute la herramienta Data Importer en Windows 10 o Windows Server 2016.


<!-- ## Objects that cannot be imported
There are some Configuration Manager objects that the importer tool cannot import to Intune. You must manually create these objects in Intune. 
- Collections based on direct membership or that are based on a query. The only collections that are imported are based on a single AD group. For all other collections, you must create the assignment in Intune and add the assignment to the appropriate objects. 
- Profiles <list what we cannot import>
- Policies <??>
- Etc.
-->



## <a name="download-the-data-importer-tool"></a>Descarga de la herramienta Data Importer

Descargue la herramienta Data Importer desde el **ConfigMgrTools/Intune-Data-Importer** repositorio de GitHub. Use el procedimiento siguiente para descargar la herramienta.

1. Vaya a la página de [versiones de GitHub para Intune Data Importer](https://github.com/ConfigMgrTools/Intune-Data-Importer/releases).  

2. Para la versión más reciente, haga clic en **Microsoft.Intune.Data.Importer.exe**.  

3. Guarde y ejecute el archivo ejecutable. A continuación, elija una carpeta de destino para extraer la herramienta Intune Data Importer.  



## <a name="run-the-data-importer-tool"></a>Ejecución de la herramienta Data Importer

Los pasos principales del Asistente para la herramienta Data Importer se pueden dividir en tres. En esta sección se proporciona información para ayudarlo a completar cada sección del asistente y a importar correctamente los datos de Configuration Manager en Intune. Cada paso continúa donde termina el anterior.


### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>Concesión de permiso a la herramienta Data Importer para acceder a los recursos

Antes de poder ejecutar la herramienta Data Importer, debe utilizar una cuenta de administrador global para conceder permiso en Azure a la herramienta Data Importer con el fin de que pueda acceder a los recursos. A continuación, puede ejecutar la herramienta con una cuenta de administrador Global o administrador de Intune.   

1. Un administrador Global debe ejecutar la herramienta de la primera vez mediante el siguiente parámetro: `IntuneDataImporter.exe -GlobalConsent`  

2. Cuando se inicia la herramienta, inicie sesión con una cuenta con el rol de administrador Global en Azure.  

3. Seleccione **Accept** para crear una aplicación en Azure con los derechos adecuados en Microsoft Graph. La herramienta Data Importer necesita estos derechos para importar objetos en Microsoft Intune.  

    > [!Important]  
    > Al aceptar este aviso, asigne el permiso de la herramienta para realizar las siguientes acciones:  
    > - Leer todos los grupos  
    > - Iniciar sesión y leer el perfil de usuario  
    > - Leer y escribir las directivas y la configuración de dispositivos de Intune  
    > - Leer y escribir aplicaciones de Intune  
    > - Leer y escribir las directivas de control de administración basada en roles de Intune  
    > - Leer y escribir en dispositivos de Intune  
    > - Leer y escribir la configuración de Intune  

4. Después de aceptar el consentimiento, cualquier otro administrador global o de Intune puede ejecutar la herramienta para importar datos de Configuration Manager en Intune en Azure.  

> [!Note]  
> Si un administrador Global no ha aceptado primero su consentimiento, la herramienta puede mostrar el siguiente error para un administrador de Intune: **No se puede acceder a esta aplicación**.  


### <a name="manually-map-collections-to-azure-ad-groups"></a>Asignación manual de recopilaciones a grupos de Azure AD

Al ejecutar la herramienta Data Importer, extrae el nombre del grupo de Active Directory de colecciones con una única regla que tenga como destino un único grupo de Active Directory. Cuando las asignaciones se crean en Intune, Data Importer busca un grupo de Azure AD con el mismo nombre que el grupo de Active Directory. Si existe, la herramienta asigna el objeto importado a ese grupo de Azure AD. 

Puede invalidar el nombre del grupo de Active Directory que Data Importer busca para una recopilación y proporcionar uno o varios grupos de Azure AD que se usará para esa colección. El uso del archivo de asignación de la recopilación proporciona una manera de asignar recopilaciones que normalmente no se importan con Data Importer a grupos de Azure AD. 

#### <a name="find-the-collections-that-cant-be-imported"></a>Búsqueda de recopilaciones que no se puede importar
Puede obtener una lista de todas las colecciones que no se pueden importar de forma que pueda agregarlas al archivo .csv de asignación de colecciones. 

1. Ejecute la herramienta Data Importer y seleccione los objetos que desea importar. Utilice los procedimientos de [fase 1: Detectar objetos de Configuration Manager y recopilar datos](#phase-1-discover-configuration-manager-objects-and-collect-data) y [fase 2: Resolver problemas y seleccionar los objetos que se va a importar](#phase-2-resolve-issues-and-select-the-objects-to-import) para detectar y elegir los objetos. Después, en la página **Summary (Resumen)** , elija **Export details (Exportar detalles)** para crear un archivo .csv con detalles de todo lo seleccionado para importar, incluidos los objetos que no se pueden importar y las implementaciones.  

2. Abra el archivo .csv en Microsoft Excel y filtre los datos en función de **Deployment** (Implementación) para la columna **Type** (Tipo) y **No** para la columna **Importable**. La columna del nombre de la recopilación muestra todas las recopilaciones que deben agregarse a un archivo de asignación de recopilaciones para que las implementaciones se puedan importar.  

#### <a name="create-the-collection-mapping-file"></a>Creación del archivo de asignación de recopilaciones
El archivo de asignación de recopilaciones es un archivo de valores separados por comas (CSV), donde la primera columna es el nombre de la recopilación de Configuration Manager y la segunda columna es el nombre del grupo de Azure AD que se utilizará para esa recopilación. Para especificar más de un grupo de Azure AD para una sola recopilación de Configuration Manager, cree varias filas en el archivo CSV con ese nombre de archivo de asignación de recopilaciones. El ejemplo siguiente es un archivo CSV que contiene dos recopilaciones. La primera recopilación está asignada a un solo grupo de Azure AD y la segunda recopilación está asignada a dos grupos de Azure AD.

![Ejemplo de archivo csv de asignación de recopilaciones](../media/migrate-collectionmapping.png)

#### <a name="start-the-data-importer-tool-using-collection-mapping"></a>Inicie la herramienta Data Importer mediante la asignación de recopilaciones
Para usar un archivo de asignación de recopilaciones, debe iniciar la herramienta Data Importer utilizando el parámetro de línea de comandos **-CollectionMappingFile** y la ruta de acceso completa al archivo .csv de asignación de recopilaciones que crea. Por ejemplo:

```IntuneDataImporter.exe -CollectionMappingFile c:\Users\myuser\Documents\collectionmapping.csv```

> [!Note]  
> Data Importer no muestra nada en cualquier página del Asistente para indicar que se ha cargado el archivo de asignación de la colección. Sin embargo, la herramienta muestra los errores encontrados al leer el archivo .csv. 
> 
> Además, en la página **Summary** (Resumen) del asistente puede revisar los tipos **Deployment** (Implementación). La herramienta muestra **Yes** (Sí) en la columna Importable y enumera los grupos de Azure AD que asignará a los objetos de la columna **Notes** (Notas).  


### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>Fase 1: Detectar objetos de Configuration Manager y recopilar datos

En la fase 1, seleccione los objetos para detectar e indique a la herramienta que recopile información sobre los objetos seleccionados. 

1. Abra la herramienta y seleccionar **iniciar**.  

2. Lea la información y, a continuación, seleccione **siguiente**.  

3. Elija si desea importar un conjunto de datos exportado previamente o seleccione los tipos de objeto que desea importar:  

    - **Exporta el conjunto de datos de importación de una ejecución anterior de Intune Data Importer**: Seleccione **examinar** para **carpeta de datos exportado**. Seleccione un conjunto de datos que exportó anteriormente mediante la herramienta Importador de datos. El usuario que importa el conjunto de datos debe ser el mismo usuario que exportó los datos. Después de importar los datos, se muestra un resumen de los objetos en la página **Summary** (Resumen) del asistente. Si el resumen es correcto, vaya a la [fase 3: Importar objeto seleccionado a Intune](#phase-3-import-selected-objects-to-intune).  

        > [!Note]  
        > Después de detectar y seleccionar los objetos en el sitio para importar, puede exportar los objetos a un conjunto de datos en la página **Sign-in to Intune** (Iniciar sesión en Intune). Después, puede importar el conjunto de datos en esta página. El conjunto de datos se cifra mediante las credenciales de usuario de Windows del usuario con sesión iniciada por lo que solo el usuario que exportó el conjunto de datos puede importar el conjunto de datos en la herramienta.  

    - **Seleccionar tipos de objeto para importar**: Proporcione la siguiente información sobre su sitio y los objetos que van a importar:  

        - **Nombre del servidor de sitio**: Proporcione el nombre de dominio completo del servidor de sitio para importar objetos. La herramienta solo detecta los objetos a los que puede acceder el usuario que ejecuta la herramienta. Normalmente, tendrá que especificar el sitio de nivel superior y ejecutar la herramienta con un usuario que tenga acceso a todos los objetos de la jerarquía del sitio.  

        - **Código de sitio**: Proporcionar el código de sitio para el servidor de sitio. Puede encontrar el código de tres letras en la parte superior de la consola de Configuration Manager.  

        - **Para importar los tipos de objetos**: Elija los objetos que desea que la herramienta para recopilar. Puede elegir **Select all** (Seleccionar todo) para elegir todos los objetos o tipos de objeto concretos.  

4. Seleccione **siguiente** para iniciar la detección de los objetos en el sitio. La herramienta muestra el progreso de cada uno de los tipos de objeto.  

    - Cuando la herramienta no detecta ningún dato de un tipo de objeto seleccionado, la barra de progreso se muestra inmediatamente como completada en ese tipo de objeto.  

    - No mostrar los objetos que no ha seleccionado en el **recopilar** página de datos.  

    - Puede ejecutar la herramienta de nuevo para los objetos que no se han recopilado o que canceló durante el proceso de recopilación.  


### <a name="phase-2-resolve-issues-and-select-the-objects-to-import"></a>Fase 2: Resolver problemas y seleccionar los objetos que se va a importar  

En la fase 2, revise los objetos que detectó la herramienta, resuelva los problemas que impiden que el objeto se importe en Intune y elija los objetos que se van a importar. Si soluciona los problemas, volver a la **Discover entorno** página del Asistente para volver a detectar los objetos. 

1. Haga clic en **Next** (Siguiente) para revisar los objetos recopilados. Hay disponible una página de selección de elementos para cada tipo de objeto recopilado.  
   <!--   > [!Tip]     
   > On each item selection page, you can create a filter to help you find the objects that you want to import. However, take note of the following:
   > - When you are on an item selection page and the view is filtered, the Select all checkboxes only apply to the displayed items. Any hidden objects because of a filter are not included when using the checkboxes.
   > - Objects are always grouped under their parent item even when you sort or filter the objects.
   -->
2. En cada página de selección de elementos, ordenar objetos por la **Importable** columna y revise los objetos que no son importables. La información de la **notas** columna proporciona detalles sobre por qué la herramienta no puede importar el objeto.  

3. Decida si desea corregir alguno de los problemas de los objetos que no se puede importar. Si soluciona los problemas de uno o más, seleccione **anterior** hasta llegar a los datos que seleccione en la página Administrador de configuración. A continuación, recopilar los datos de nuevo para ver si se ha resuelto el problema. Puede seguir corrigiendo problemas hasta que esté satisfecho con los objetos que se pueden importables.  

4. En cada página de selección de elementos, seleccione los objetos que se van a importar. Se muestran las siguientes columnas:  

    - **Nombre**: Nombre del objeto de Configuration Manager.  

    - **Importable**: Especifica si se puede importar un objeto. Solo puede elegir objetos que tengan Yes (Sí) en la columna Importable.  

    - **Plataforma**: Especifica la plataforma admitida por el objeto.  

    - **Ya se importó**: Especifica si el objeto ya se ha importado con la herramienta en este equipo.  

    - **Se ha sustituido** (para aplicaciones): Especifica si la aplicación se ha reemplazado por otra aplicación. Seleccione el **Show sustituido aplicaciones** opción en la parte superior de la página para las aplicaciones reemplazadas mostrar.  

    - **Notas de la**: Proporciona información sobre por qué no se puede importar un objeto. La columna **Notes** (Notas) también muestra información sobre la configuración que se omitió (para algunos tipos de objetos), pero el objeto todavía se puede importar sin esa configuración.  

    - **Líneas base de configuración** (para elementos de configuración): Especifica las líneas de base de configuración que están asociados con un elemento de configuración.  

    - **Certificado necesario** (para los perfiles y directivas): Especifica si un certificado está asociado con el objeto. Cuando lo está, debe importar también certificado.  

5. Después de elegir los objetos que se va a importar, aparecen en la página de resumen. Están disponibles las siguientes acciones:  

    - **Exportar detalles**: Crea un archivo .csv que contiene la información que aparece en la pantalla. También muestra los objetos que no puede importables y el motivo por qué no se pueden importar. Puede mantener este archivo para tenerlos como referencia.  

    - **Exportar datos de error**: Exporta un archivo comprimido que contiene información sobre los datos que la herramienta no pudo convertir ni importar.  


### <a name="phase-3-import-selected-objects-to-intune"></a>Fase 3: Importar objeto seleccionado a Intune

En la fase 3, inicie sesión en Intune e importar los objetos seleccionados. 

1. Seleccione **siguiente**y, a continuación, seleccione una de las siguientes opciones:  

    - **Exportar**: Después de detectar y seleccionar los objetos en el sitio para importar, puede exportar los objetos a un conjunto de datos. Esto le permite detectar objetos desde un equipo que no tiene acceso a internet, exportar los datos y, a continuación, importar los datos desde un equipo que tenga acceso a internet. El conjunto de datos se cifra mediante las credenciales de usuario de Windows del usuario con sesión iniciada por lo que solo el usuario que exportó el conjunto de datos puede importar el conjunto de datos en la herramienta. Cuando elija esta opción, elija la ruta de acceso a los datos exportados.  

        1. Seleccione **exportar** en el **iniciar sesión en Intune** página.  

        2. Seleccione **examinar** para seleccionar la carpeta de destino para la exportación. La carpeta debe estar vacía.  

        3. Seleccione **iniciar** para exportar los datos. Cuando finalice la exportación, seleccione **cerrar** para completar el asistente y cerrar Data Importer.  

        4. Inicie Data Importer desde otro equipo con acceso a internet con las mismas credenciales. Seleccione **importación exportado previamente el conjunto de datos** en la segunda página del asistente. Una vez importados los datos, el asistente le llevará a la página **Sign in to Intune** (Iniciar sesión en Intune).  

    - **Inicie sesión en Intune**: Inicie sesión con una cuenta de administrador Global o administrador de Intune. Después de iniciar la sesión, se inicia el proceso de importación.  

        > [!Important]  
        > En primer lugar, pruebe el proceso de importación de datos con un inquilino de prueba. Después de confirmar que los datos esperados se ha importado, puede ir a través del mismo proceso con el inquilino de Intune de producción.  

2. La página Progress (Progreso) muestra el progreso de la importación de los objetos. Haga clic en **Next** (Siguiente) cuando finalice la importación.  

3. En la página Completion (Finalización), se enumeran los objetos importados. Compruebe el estado de todos los objetos en los que se detectó un error durante el proceso de importación. Están disponibles las siguientes acciones:  

    - **Exportar detalles**: Crea un archivo .csv que contiene la información mostrada en pantalla. Puede mantener este archivo para tenerlos como referencia.  

    - **Exportar datos de error**: Exporta un archivo comprimido que contiene información sobre los datos que la herramienta no pudo convertir ni importar.  



## <a name="next-steps"></a>Pasos siguientes

Después de importar los datos en Intune, [preparar Intune para la migración de usuarios](migrate-prepare-intune.md). 
