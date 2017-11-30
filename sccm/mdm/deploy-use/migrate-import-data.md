---
title: "Importación de datos en Microsoft Intune"
titleSuffix: Configuration Manager
description: 
keywords: 
author: dougeby
manager: dougeby
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.openlocfilehash: 4b5f788a611b9df7c12f788099d82fadbf1e4af9
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>Importación de datos de Configuration Manager en Microsoft Intune 

*Se aplica a: System Center Configuration Manager (Rama actual)*    

El primer paso recomendado del proceso de [migrar dispositivos y usuarios de MDM híbrida a Intune independiente](migrate-hybridmdm-to-intunesa.md) en la configuración solo en la nube consiste en utilizar la herramienta Intune Data Importer. Si lo desea, puede omitir esta fase y pasar a la de [preparación de Intune para migrar usuarios](migrate-prepare-intune.md). Sin embargo, esta herramienta realiza las siguientes funciones que pueden ahorrarle mucho tiempo en la fase siguiente: 
1.  Recopila datos sobre los objetos seleccionados de la jerarquía de Configuration Manager. 
2.  Proporciona detalles sobre los objetos que puede seleccionar para la importación, además de información sobre por qué no se puede importar un objeto.
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
- Hay algunos perfiles que dependen de otros objetos. Si desea importar un perfil que depende de otro objeto, como uno de correo electrónico que depende de un certificado, debe importar ambos objetos al mismo tiempo.
- Después de ejecutar la herramienta, deberá realizar algunos pasos manuales más. Por ejemplo, destinar aplicaciones y directivas a grupos de AAD. 

## <a name="prerequisites"></a>Requisitos previos
- Versión 1610 de Configuration Manager o una posterior: se recomienda especificar el sitio de nivel superior y ejecutar la herramienta con un usuario que tenga acceso a todos los objetos de la jerarquía del sitio. La herramienta solo detecta los objetos a los que puede acceder el usuario que ejecuta la herramienta. 
- Debe ejecutar la herramienta desde un equipo con acceso al proveedor de SMS (para recopilar datos de Configuration Manager) y a Internet (para importar objetos en Intune).
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

1. Vaya a la página [Intune Data Importer en GitHub](https://go.microsoft.com/fwlink/?linkid=858194).
2. Haga clic en **Clone or download** (Clonar o descargar), en **Download ZIP** (Descargar ZIP) y guarde el archivo ZIP comprimido. 
3. Extraiga el contenido del archivo ZIP.

## <a name="run-the-data-importer-tool"></a>Ejecución de la herramienta Data Importer
Antes de poder ejecutar la herramienta Data Importer, debe utilizar una cuenta de administrador global para conceder permiso en Azure a la herramienta Data Importer con el fin de que pueda acceder a los recursos. Después, puede ejecutar la herramienta con una cuenta de administrador global o de administrador de Intune.     

Los pasos principales del Asistente para la herramienta Data Importer se pueden dividir en tres. En esta sección se proporciona información para ayudarlo a completar cada sección del asistente y a importar correctamente los datos de Configuration Manager en Intune. Cada paso continúa donde termina el anterior.

### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>Concesión de permiso a la herramienta Data Importer para acceder a los recursos
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

### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>Fase 1: Detectar objetos de Configuration Manager y recopilar datos
En la fase 1, seleccione los objetos para detectar e indique a la herramienta que recopile información sobre los objetos seleccionados. 
1. Abra la herramienta y haga clic en **Start** (Iniciar).  
2. Lea la información y, luego, haga clic en **Next** (Siguiente). 
3. Proporcione la siguiente información sobre su sitio y los objetos en el sitio que va a importar. 
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

    > [!Tip]     
    > En cada página de selección de elementos, puede crear un filtro que lo ayude a encontrar los objetos que se van a importar. Sin embargo, tenga en cuenta lo siguiente:
    > - Cuando se encuentra en una página de selección de elementos y la vista está filtrada, la casilla de verificación Select all (Seleccionar todo) solo se aplica a los elementos mostrados. No se incluyen los objetos ocultos por un filtro al usar las casillas de verificación.
    > - Los objetos siempre se agrupan bajo su elemento primario, incluso al ordenar o filtrar los objetos.


6.  En cada página de selección de elementos, ordene los objetos por la columna Importable y revise los objetos que no se pueden importar. La información de la columna Notes (Notas) proporciona detalles sobre por qué la herramienta no puede importar el objeto. 
7.  Ahora debe decidir si desea corregir alguno de los problemas de los objetos que no se pueden importar. Si corrige uno o varios problemas, haga clic en Previous (Anterior) hasta que llegue a la página Select data from Configuration Manager (Seleccionar datos de Configuration Manager) y recopile los datos de nuevo para ver si se ha resuelto el problema. Puede seguir corrigiendo problemas hasta que esté satisfecho con los objetos que se pueden importar. 
8.  En cada página de selección de elementos, seleccione los objetos que se van a importar. Se muestran las siguientes columnas:
    - **Name** (Nombre): el nombre del objeto de Configuration Manager. 
    - **Importable**: especifica si se puede importar un objeto. Solo puede elegir objetos que tengan Yes (Sí) en la columna Importable. 
    - **Plataform** (Plataforma): especifica la plataforma que admite el objeto.
    - **Already imported** (Ya importados): especifica si el objeto ya se ha importado con la herramienta en este equipo. 
    - **Notes** (Notas): proporciona información sobre por qué no se puede importar un objeto.
    - **Configuration baselines** (Líneas base de configuración) (para los elementos de configuración): especifica las líneas base de configuración que están asociadas a un elemento de configuración.
    - **Required certificate** (Certificado necesario) (para los perfiles y las directivas): especifica si un certificado está asociado con el objeto. Cuando lo está, debe importar también certificado.
9.  Después de elegir los objetos que se van a importar, aparecen en la página Summary (Resumen). Están disponibles las siguientes acciones: 
    - **Export details** (Exportar detalles): crea un archivo .csv que contiene la información que aparece en pantalla. Puede mantener este archivo para tenerlos como referencia. 
    - **Export error data** (Exportar datos de errores): exporta un archivo comprimido que contiene información sobre los datos que la herramienta no pudo convertir ni importar. 

### <a name="phase-3-import-selected-object-to-intune"></a>Fase 3: Importar el objeto seleccionado en Intune
En la fase 3, podrá iniciar sesión en Intune e importar los objetos seleccionados. 
10. Haga clic en **Next** (Siguiente) y, después, en **Sign in to Intune** (Iniciar sesión en Intune) con el objetivo de iniciar sesión en el inquilino de Intune para importar los datos. Debe iniciar sesión con una cuenta de administrador global o de administrador de Intune. Después de iniciar la sesión, se inicia el proceso de importación.

    > [!Important]
    > Le recomendamos que primero pruebe el proceso de importación de datos con un inquilino de prueba. Después de confirmar que se han importado los datos que esperaba, puede realizar el mismo proceso con el inquilino de Intune de producción.

12. La página Progress (Progreso) muestra el progreso de la importación de los objetos. Haga clic en **Next** (Siguiente) cuando finalice la importación. 
13. En la página Completion (Finalización), se enumeran los objetos importados. Compruebe el estado de todos los objetos en los que se detectó un error durante el proceso de importación. Están disponibles las siguientes acciones: 
    - **Export details** (Exportar detalles): crea un archivo .csv que contiene la información que aparece en pantalla. Puede mantener este archivo para tenerlos como referencia. 
    - **Export error data** (Exportar datos de errores): exporta un archivo comprimido que contiene información sobre los datos que la herramienta no pudo convertir ni importar.

## <a name="next-steps"></a>Pasos siguientes
Después de importar los datos en Intune, debe realizar los pasos de [preparación de Intune para la migración de usuarios](migrate-prepare-intune.md). 