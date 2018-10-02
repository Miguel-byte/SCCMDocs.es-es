---
title: CMPivot para datos en tiempo real
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo usar CMPivot en Configuration Manager para los clientes de consulta en tiempo real.
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2e0f74790437b34d1c5cd5dc00767ec782a51b45
ms.sourcegitcommit: fe279229a90fdc8cddbb13c7ffdbbb22af0e25ef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47229303"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>CMPivot para datos en tiempo real en Configuration Manager

<!--1358456-->

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager siempre ha proporcionado un gran almacén centralizado de datos de dispositivo, que los clientes utilizan para informes. El sitio normalmente recopila estos datos cada semana. A partir de la versión 1806, CMPivot es una nueva utilidad en la consola que ahora proporciona acceso al estado en tiempo real de los dispositivos del entorno. Esta utilidad ejecuta una consulta inmediatamente en todos los dispositivos conectados actualmente en la colección de destino y devuelve los resultados. Después, puede filtrar y agrupar estos datos en la herramienta. Mediante el suministro de datos en tiempo real de los clientes en línea, puede contestar preguntas empresariales, solucionar problemas y responder a incidentes de seguridad más rápidamente.

Por ejemplo, en la [mitigación de vulnerabilidades de canal lateral de ejecución especulativa](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), uno de los requisitos consiste en actualizar el BIOS del sistema. Puede usar CMPivot para realizar consultas rápidamente sobre la información del BIOS del sistema y buscar clientes que no cumplen los requisitos.



## <a name="prerequisites"></a>Requisitos previos

Los siguientes componentes son necesarios para usar CMPivot:

- Actualice los dispositivos de destino a la última versión del cliente de Configuration Manager.  

- El administrador de Configuration Manager necesita el permiso **lectura** en el objeto **Scripts SMS** y el permiso **Ejecutar scripts** en el objeto **Colección**. El rol **Ejecutor de scripts** tiene estos permisos. Para más información, consulte [Crear roles de seguridad para scripts](/sccm/apps/deploy-use/create-deploy-scripts#bkmk_ScriptRoles).  

- Para recopilar datos para las siguientes entidades, los clientes de destino requieren la versión 5.0 de PowerShell:  
    - Administradores
    - Conexión
    - IPConfig
    - SMBConfig 



## <a name="limitations"></a>Limitaciones

- En una jerarquía, conecte la consola de Configuration Manager a un *sitio primario* para ejecutar CMPivot. La acción **Iniciar CMPivot** no aparece en la consola cuando se conecta a un sitio de administración central.  

- CMPivot solo devuelve datos para los clientes conectados al sitio actual.  

- Si una colección contiene dispositivos de otro sitio, los resultados de CMPivot son solo desde dispositivos en el sitio actual.  

- No se pueden personalizar las propiedades de entidad, las columnas de resultados o las acciones en dispositivos.  

- Solo se puede ejecutar una instancia de CMPivot al mismo tiempo en un equipo que ejecuta la consola de Configuration Manager.  

- En la versión 1806, la consulta para la entidad **Administrators** solo funciona si el grupo se denomina "Administrators". No funciona si se localiza el nombre del grupo. Por ejemplo, "Administrateurs" en francés.<!--SCCMDocs issue 759-->  



## <a name="start-cmpivot"></a>Iniciar CMPivot

1. En la consola de Configuration Manager, conéctese al sitio primario. Vaya al área de trabajo **Activos y compatibilidad** y seleccione el nodo **Recopilaciones de dispositivos**. Seleccione una recopilación de destino y haga clic en **Iniciar CMPivot** en la cinta para iniciar la herramienta.  

    > [!Tip]  
    > Si no ve esta opción, consulte las siguientes configuraciones:  
    > 
    > - Confirme con un administrador del sitio que la cuenta tiene los permisos necesarios. Para obtener más información, consulte [Requisitos previos](#prerequisites).  
    > 
    > - Conecte la consola a un *sitio primario*.  

2. La interfaz proporciona más información sobre el uso de la herramienta.  

     - Especifique cadenas de consulta manualmente en la parte superior o haga clic en los vínculos en la documentación en línea.  

     - Haga clic en una de las opciones de **Entidades** para agregarla a la cadena de consulta.  

     - Los vínculos de **Table Operators** (Operadores de tabla), **Aggregation Functions** (Funciones de agregación) y **Funciones escalares** abren la documentación de referencia del lenguaje en el explorador web. CMPivot utiliza el mismo lenguaje de consulta que [Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/).  

3. Mantenga la ventana CMPivot abierta para ver los resultados de los clientes. Cuando cierre la ventana CMPivot, la sesión se completará.  

    > [!Note]  
    > Si se ha enviado la consulta, los clientes todavía envían un mensaje de estado de respuesta al servidor.  



## <a name="how-to-use-cmpivot"></a>Cómo usar CMPivot

![Ejemplo de ventana CMPivot](media/1358456-cmpivot-sample.png)

La ventana CMPivot contiene los elementos siguientes:  

1. La colección que CMPivot actualmente tiene como destino se encuentra en la barra de título en la parte superior y la barra de estado en la parte inferior de la ventana. Por ejemplo, **Todos los sistemas** en la captura de pantalla anterior.  

2. El panel de la izquierda muestra las **Entidades** que están disponibles en los clientes. Algunas entidades usan WMI, mientras que otras usan PowerShell para obtener datos de los clientes.   

    - Haga clic con el botón derecho en una entidad para realizar las siguientes acciones:  

       - **Insertar**: agregue la entidad a la consulta en la posición actual del cursor. La consulta no se ejecuta automáticamente. Esta acción es el valor predeterminado cuando se hace doble clic en una entidad. Use esta acción cuando cree una consulta.  

       - **Consultar todos**: ejecute una consulta para esta entidad incluyendo todas las propiedades. Use esta acción para realizar consultas de una sola entidad rápidamente.  

       - **Consultar por dispositivo**: ejecute una consulta para esta entidad y agrupe los resultados. Por ejemplo, `Disk | summarize dcount( Device ) by Name`.  

    - Expanda una entidad para ver las propiedades específicas disponibles para cada entidad. Haga doble clic en una propiedad para agregarla a la consulta en la posición actual del cursor.  

3. La pestaña **Inicio** muestra información general sobre CMPivot, incluidos los vínculos a las consultas de ejemplo y documentación complementaria.  

4. La pestaña **Consulta** muestra el panel de consultas, el panel de resultados y la barra de estado. En la captura de pantalla de ejemplo anterior se seleccionó la pestaña de consulta.  

5. El panel de consulta es donde se crea o se escribe una consulta que se ejecuta en los clientes de la colección.  

    - CMPivot utiliza un subconjunto del mismo lenguaje de consulta que [Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/).  

    - Corte, copie o pegue contenido en el panel de consulta.  

    - De forma predeterminada, este panel usa IntelliSense. Por ejemplo, si comienza a escribir `D`, IntelliSense sugiere todas las entidades que comienzan con esa letra. Seleccione una opción y presione la tecla TAB para insertarla. Escriba un carácter de canalización y un espacio `| ` y después IntelliSense sugiere todos los operadores de la tabla. Inserte `summarize`, escriba un espacio e IntelliSense sugerirá todas las funciones de agregación. Para obtener más información sobre estos operadores y funciones, haga clic en la pestaña **Inicio** en CMPivot.  

    - El panel de consulta también proporciona las siguientes opciones:  

        - Ejecutar la consulta.  

        - Avanzar y retroceder en la lista del historial de consultas.  

        - Crear una colección de pertenencia directa.  

        - Exportar los resultados de consulta a CSV o al Portapapeles.  

6. El panel de resultados muestra los datos devueltos por los clientes activos de la consulta.  

    - Las columnas disponibles varían en función de la entidad y la consulta.  

    - Haga clic en un nombre de columna para ordenar los resultados por esa propiedad.  

    - Haga clic con el botón derecho en cualquier nombre de columna para agrupar los resultados por la misma información en esa columna u ordenarlos.  

    - Haga clic con el botón derecho en un nombre de dispositivo para realizar las siguientes acciones adicionales en el dispositivo:  

       - **Pasar a**: consulte otra entidad en este dispositivo.  

       - **Ejecutar Script**: inicie el asistente Ejecuta script para ejecutar un script de PowerShell existente en este dispositivo. Para obtener más información, vea [Ejecutar un script](/sccm/apps/deploy-use/create-deploy-scripts#run-a-script).  

       - **Control remoto**: inicie una sesión de Control remoto de Configuration Manager en este dispositivo. Para obtener más información, vea [Cómo administrar de forma remota un equipo cliente de Windows](/sccm/core/clients/manage/remote-control/remotely-administer-a-windows-client-computer).  

       - **Explorador de recursos**: inicie el Explorador de recursos de Configuration Manager para este dispositivo. Para obtener más información, vea [Ver el inventario de hardware](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory) o [Ver el inventario de software](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory).  

    - Haga clic con el botón derecho en una casilla que no sea de dispositivo para realizar las siguientes acciones adicionales:  

       - **Copiar**: copie el texto de la celda en el Portapapeles.  

       - **Mostrar los dispositivos con**: consulte los dispositivos con este valor para esta propiedad. Por ejemplo, de los resultados de la consulta `OS`, seleccione esta opción en una celda en la fila Versión: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

       - **Mostrar los dispositivos sin**: consulte los dispositivos sin este valor para esta propiedad. Por ejemplo, de los resultados de la consulta `OS`, seleccione esta opción en una celda en la fila Versión: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

       - **Buscarlo con Bing**: inicie el explorador web predeterminado en www.bing.com con este valor como cadena de consulta.  

    - Haga clic en cualquier texto con hipervínculo para fijar la vista en esa información específica.  

    - El panel de resultados no muestra más de 20 000 filas. Puede ajustar la consulta para filtrar aún más los datos o reiniciar CMPivot en una colección más pequeña.  

7. La barra de estado muestra la siguiente información (de izquierda a derecha):  

    - El estado de la consulta actual a la colección de destino. Este estado incluye:  
        - El número de clientes activos que completaron la consulta (3)  
        - El número de clientes total (5)  
        - El número de clientes sin conexión (2)  
        - Los clientes que devolvieron un error (0)  

        Por ejemplo: `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

    - El identificador de la operación del cliente. Por ejemplo: `id(16780221)`  

    - La colección actual. Por ejemplo: `PM_Team_Machines`  

    - El número total de filas en el panel de resultados. Por ejemplo, `1 objects`.  



## <a name="example-scenarios"></a>Escenarios de ejemplo

Las secciones siguientes proporcionan ejemplos de cómo puede usar CMPivot en su entorno:


### <a name="example-1-stop-a-running-service"></a>Ejemplo 1: Detenga un servicio en ejecución

El Administrador de seguridad le pide que detenga y deshabilite el servicio Examinador de equipos tan pronto como sea posible en todos los dispositivos en el departamento de contabilidad. Inicie CMPivot en una colección de todos los dispositivos de contabilidad y seleccione **Consultar todos** en la entidad **Servicio**. 

`Service`

Conforme aparezcan los resultados, haga clic con el botón derecho en la columna **Nombre** y seleccione **Agrupar por**. 

`Service | summarize dcount( Device ) by Name`

En la fila del servicio **Explorador**, haga clic en el número de un hipervínculo en la columna **dcount_**. 

`Service | where (Name == 'Browser') | summarize count() by Device`

Realice una selección múltiple de todos los dispositivos, haga clic con el botón derecho en la selección y elija **Ejecutar script**. Esta acción inicia el asistente Ejecutar script, desde el que se ejecuta un script existente para detener y deshabilitar un servicio. Con CMPivot responde rápidamente a los incidentes de seguridad para todos los equipos activos, y puede ver los resultados en el asistente Ejecutar script. Luego realiza un seguimiento para crear una referencia de configuración para corregir otros equipos de la colección a medida que se activen en el futuro. 

![Ejemplo de CMPivot para el servicio Explorador y la acción Ejecutar script](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>Ejemplo 2: Resolver proactivamente errores de aplicación  

Para ser proactivo con el mantenimiento, ejecute una vez por semana CMPivot en una colección de servidores que administra y seleccione **Consultar todos** en la entidad **AppCrash**. Haga clic con el botón derecho en la columna **FileName** y seleccione **Orden ascendente**. Un dispositivo devuelve siete resultados sqlsqm.exe con una marca de tiempo aproximadamente a las 3:00 cada día. Seleccione el nombre de archivo en una de las filas, haga clic con el botón derecho en él y seleccione **Buscarlo con Bing**. Examine los resultados de búsqueda en el explorador web para encontrar un artículo de soporte técnico de Microsoft para resolver este problema con más información y la resolución. 


### <a name="example-3-bios-version"></a>Ejemplo 3: Versión del BIOS

Para [mitigar la ejecución especulativa de vulnerabilidades de canal lateral](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), uno de los requisitos consiste en actualizar el BIOS del sistema. Comience con una consulta para la entidad **BIOS**. Después, seleccione **Agrupar por** la propiedad **Versión**. Después, haga clic con el botón derecho en un valor específico, como "LENOVO - 1140", y seleccione **Mostrar dispositivos con**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Ejemplo 4: Liberar espacio en disco

Necesita almacenar temporalmente un archivo grande en un servidor de archivos de red, pero no está seguro de cuál de ellos tiene suficiente capacidad. Inicia CMPivot en una colección de servidores de archivos y consulta la entidad **Disco**. Modifica la consulta para que CMPivot devuelva rápidamente una lista de servidores activos con los datos de almacenamiento en tiempo real:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`



## <a name="inside-cmpivot"></a>Dentro de CMPivot

CMPivot envía consultas a los clientes que usan el "canal rápido" de Configuration Manager. Otras características como las acciones de notificación de cliente, el estado de cliente y Endpoint Protection también utilizan este canal de comunicación del servidor al cliente. Los clientes devuelven resultados mediante el sistema de mensajes de estado que es igual de rápido. Los mensajes de estado se almacenan temporalmente en la base de datos. 

Las consultas y los resultados son todo texto. Las entidades **InstallSoftware** y **Proceso** devuelven algunos de los conjuntos de resultados más grandes. Durante las pruebas de rendimiento, el tamaño de archivo de mensaje de estado más grande de equipo cliente para estas consultas era menor de **1 KB**. Escalada a un entorno grande con 50 000 clientes activos, esta consulta única generaría menos de 50 MB de datos a través de la red.  

Una consulta agota el tiempo de espera después de una hora. Por ejemplo, una colección tiene 500 dispositivos y 450 de los clientes están actualmente en línea. Los dispositivos activos reciben la consulta y devuelven los resultados casi de inmediato. Si deja la ventana CMPivot abierta, a medida que los 50 clientes restantes se conecten, también recibirán la consulta y devolverán resultados. 

>[!TIP]
> Las interacciones de CMPivot se registran en los archivos de registro siguientes:
>
> **Servidor:**
> - SmsProv.log
> - bgbServer.log
> - StateSys.log
>
> **Cliente:**
> - CCMNotificationAgent.log
> - Scripts.log
> - StateMessage.log
>
> Para obtener más información, vea [Archivos de registro](/sccm/core/plan-design/hierarchy/log-files).


## <a name="see-also"></a>Consulte también
[Crear y ejecutar scripts de PowerShell](/sccm/apps/deploy-use/create-deploy-scripts)
