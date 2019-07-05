---
title: CMPivot para datos en tiempo real
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo usar CMPivot en Configuration Manager para realizar consultas en clientes en tiempo real.
ms.date: 05/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3626514d4cd7f2d26e3c198931eb6fad49123dd2
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67551305"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>CMPivot para datos en tiempo real en Configuration Manager

<!--1358456-->

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager siempre ha proporcionado un gran almacén centralizado de datos de dispositivo, que los clientes utilizan para informes. El sitio normalmente recopila estos datos cada semana. A partir de la versión 1806, CMPivot es una nueva utilidad en la consola que ahora proporciona acceso al estado en tiempo real de los dispositivos del entorno. Esta utilidad ejecuta una consulta inmediatamente en todos los dispositivos conectados actualmente en la colección de destino y devuelve los resultados. Después, puede filtrar y agrupar estos datos en la herramienta. Mediante el suministro de datos en tiempo real de los clientes en línea, puede contestar preguntas empresariales, solucionar problemas y responder a incidentes de seguridad más rápidamente.

Por ejemplo, en la [mitigación de vulnerabilidades de canal lateral de ejecución especulativa](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), uno de los requisitos consiste en actualizar el BIOS del sistema. Puede usar CMPivot para realizar consultas rápidamente sobre la información del BIOS del sistema y buscar clientes que no cumplen los requisitos.

 > [!Tip]  
 > Algunos programas de seguridad podrían bloquear los scripts que se ejecutan desde c:\windows\ccm\scriptstore. Esto puede impedir la correcta ejecución de las consultas de CMPivot. Otros programas de software de seguridad también podrían generar alertas o eventos de auditoría al ejecutar PowerShell para CMPivot.


## <a name="prerequisites"></a>Requisitos previos

Los siguientes componentes son necesarios para usar CMPivot:

- Actualice los dispositivos de destino a la última versión del cliente de Configuration Manager.  

- Permisos para CMPivot:
  - Permiso de **L¡lectura** en el objeto **Scripts SMS**
  - Permiso para **ejecutar scripts** en la **colección**
  - Permiso de **lectura** en los **informes de inventario**
  - Ámbito predeterminado. 

- Los clientes de destino requieren como mínimo PowerShell versión 4.

- Para recopilar datos para las siguientes entidades, los clientes de destino requieren la versión 5.0 de PowerShell:  
  - Administradores
  - Conexión
  - IPConfig
  - SMBConfig

 
## <a name="limitations"></a>Limitaciones

- En una jerarquía, conecte la consola de Configuration Manager a un *sitio primario* para ejecutar CMPivot. La acción **Iniciar CMPivot** no aparece en la consola cuando se conecta a un sitio de administración central (CAS).
  - A partir de Configuration Manager versión 1902, puede ejecutar CMPivot desde un CAS. En algunos entornos, se necesitan permisos adicionales. Para obtener más información, vea [CMPivot a partir de la versión 1902](#bkmk_cmpivot1902).

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

     - Los vínculos de **Table Operators** (Operadores de tabla), **Aggregation Functions** (Funciones de agregación) y **Funciones escalares** abren la documentación de referencia del lenguaje en el explorador web. CMPivot usa el [lenguaje de consulta de Kusto (KQL)](https://docs.microsoft.com/azure/kusto/query/).  

3. Mantenga la ventana CMPivot abierta para ver los resultados de los clientes. Cuando cierre la ventana CMPivot, la sesión se completará.  

    > [!Note]  
    > Si se ha enviado la consulta, los clientes todavía envían un mensaje de estado de respuesta al servidor.  



## <a name="how-to-use-cmpivot"></a>Cómo usar CMPivot

![Ejemplo de ventana CMPivot](media/1358456-cmpivot-sample.png)

La ventana CMPivot contiene los elementos siguientes:  

1. La colección que CMPivot actualmente tiene como destino se encuentra en la barra de título en la parte superior y la barra de estado en la parte inferior de la ventana. Por ejemplo, "PM_Team_Machines" en la captura de pantalla anterior.  

2. El panel de la izquierda muestra las **Entidades** que están disponibles en los clientes. Algunas entidades usan WMI, mientras que otras usan PowerShell para obtener datos de los clientes.   

    - Haga clic con el botón derecho en una entidad para realizar las siguientes acciones:  

       - **Insertar**: agregue la entidad a la consulta en la posición actual del cursor. La consulta no se ejecuta automáticamente. Esta acción es el valor predeterminado cuando se hace doble clic en una entidad. Use esta acción cuando cree una consulta.  

       - **Consultar todos**: ejecute una consulta para esta entidad incluyendo todas las propiedades. Use esta acción para realizar consultas de una sola entidad rápidamente.  

       - **Consultar por dispositivo**: ejecute una consulta para esta entidad y agrupe los resultados. Por ejemplo, `Disk | summarize dcount( Device ) by Name`.  

    - Expanda una entidad para ver las propiedades específicas disponibles para cada entidad. Haga doble clic en una propiedad para agregarla a la consulta en la posición actual del cursor.  

3. La pestaña **Inicio** muestra información general sobre CMPivot, incluidos los vínculos a las consultas de ejemplo y documentación complementaria.  

4. La pestaña **Consulta** muestra el panel de consultas, el panel de resultados y la barra de estado. En la captura de pantalla de ejemplo anterior se seleccionó la pestaña de consulta.  

5. El panel de consulta es donde se crea o se escribe una consulta que se ejecuta en los clientes de la colección.  

    - CMPivot usa un subconjunto del [lenguaje de consulta de Kusto (KQL)](https://docs.microsoft.com/azure/kusto/query/).  

    - Corte, copie o pegue contenido en el panel de consulta.  
    <!-- markdownlint-disable MD038 -->
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

      - **Ejecutar script**: inicie el Asistente para la ejecución de scripts para ejecutar un script de PowerShell existente en este dispositivo. Para obtener más información, vea [Ejecutar un script](/sccm/apps/deploy-use/create-deploy-scripts#run-a-script).  

      - **Control remoto**: inicie una sesión de Control remoto de Configuration Manager en este dispositivo. Para obtener más información, vea [Cómo administrar de forma remota un equipo cliente de Windows](/sccm/core/clients/manage/remote-control/remotely-administer-a-windows-client-computer).  

      - **Explorador de recursos**: inicie el Explorador de recursos de Configuration Manager para este dispositivo. Para obtener más información, vea [Ver el inventario de hardware](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory) o [Ver el inventario de software](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory).  

   - Haga clic con el botón derecho en una casilla que no sea de dispositivo para realizar las siguientes acciones adicionales:  

     - **Copiar**: copie el texto de la celda en el Portapapeles.  

     - **Mostrar los dispositivos con**: consulte los dispositivos con este valor para esta propiedad. Por ejemplo, de los resultados de la consulta `OS`, seleccione esta opción en una celda en la fila Versión: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Mostrar los dispositivos sin**: consulte los dispositivos sin este valor para esta propiedad. Por ejemplo, de los resultados de la consulta `OS`, seleccione esta opción en una celda en la fila Versión: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Buscarlo con Bing**: inicie el explorador web predeterminado en www.bing.com con este valor como la cadena de consulta.  

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


### <a name="example-1-stop-a-running-service"></a>Ejemplo 1: Detección de un servicio en ejecución

El Administrador de seguridad le pide que detenga y deshabilite el servicio Examinador de equipos tan pronto como sea posible en todos los dispositivos en el departamento de contabilidad. Inicie CMPivot en una colección de todos los dispositivos de contabilidad y seleccione **Consultar todos** en la entidad **Servicio**. 

`Service`

Conforme aparezcan los resultados, haga clic con el botón derecho en la columna **Nombre** y seleccione **Agrupar por**. 

`Service | summarize dcount( Device ) by Name`

En la fila del servicio **Explorador**, haga clic en el número de un hipervínculo en la columna **dcount_** . 

`Service | where (Name == 'Browser') | summarize count() by Device`

Realice una selección múltiple de todos los dispositivos, haga clic con el botón derecho en la selección y elija **Ejecutar script**. Esta acción inicia el asistente Ejecutar script, desde el que se ejecuta un script existente para detener y deshabilitar un servicio. Con CMPivot responde rápidamente a los incidentes de seguridad para todos los equipos activos, y puede ver los resultados en el asistente Ejecutar script. Luego realiza un seguimiento para crear una referencia de configuración para corregir otros equipos de la colección a medida que se activen en el futuro. 

![Ejemplo de CMPivot para el servicio Explorador y la acción Ejecutar script](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>Ejemplo 2: Resolución proactiva de errores de aplicación  

Para ser proactivo con el mantenimiento, ejecute una vez por semana CMPivot en una colección de servidores que administra y seleccione **Consultar todos** en la entidad **AppCrash**. Haga clic con el botón derecho en la columna **FileName** y seleccione **Orden ascendente**. Un dispositivo devuelve siete resultados sqlsqm.exe con una marca de tiempo aproximadamente a las 3:00 cada día. Seleccione el nombre de archivo en una de las filas, haga clic con el botón derecho en él y seleccione **Buscarlo con Bing**. Examine los resultados de búsqueda en el explorador web para encontrar un artículo de soporte técnico de Microsoft para resolver este problema con más información y la resolución. 


### <a name="example-3-bios-version"></a>Ejemplo 3: Versión del BIOS

Para [mitigar la ejecución especulativa de vulnerabilidades de canal lateral](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), uno de los requisitos consiste en actualizar el BIOS del sistema. Comience con una consulta para la entidad **BIOS**. Después, seleccione **Agrupar por** la propiedad **Versión**. Después, haga clic con el botón derecho en un valor específico, como "LENOVO - 1140", y seleccione **Mostrar dispositivos con**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Ejemplo 4: Espacio libre en disco

Necesita almacenar temporalmente un archivo grande en un servidor de archivos de red, pero no está seguro de cuál de ellos tiene suficiente capacidad. Inicie CMPivot en una colección de servidores de archivos y consulte la entidad **Disco**. Modifique la consulta para que CMPivot devuelva rápidamente una lista de servidores activos con los datos de almacenamiento en tiempo real:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="bkmk_cmpivot"></a> CMPivot a partir de la versión 1810
<!--1359068, 3607759-->

A partir de la versión 1810 de Configuration Manager, CMPivot incluye las mejoras siguientes:

- [Utilidad y rendimiento de CMPivot](#bkmk_cmpivot-perf)
- [Funciones escalares](#bkmk_cmpivot-functions)  
- [Visualizaciones de representación](#bkmk_cmpivot-charts)  
- [Inventario de hardware](#bkmk_cmpivot-hinv)  
- [Operadores escalares](#bkmk_cmpivot-operators)  
- [Resumen de consulta](#bkmk_cmpivot-summary)  
- [Mensajes de estado de auditoría](#cmpivot-audit-status-messages)

### <a name="bkmk_cmpivot-perf"></a> Utilidad y rendimiento de CMPivot

- CMPivot devolverá hasta 100 000 celdas, en lugar de 20 000 filas.
  - Si la entidad tiene 5 propiedades, lo que significa 5 columnas, se mostrarán hasta 20 000 filas.
  - Para una entidad con 10 propiedades, se mostrarán hasta 10 000 filas.
  - El total de los datos que se muestran es menor o igual que 100 000 celdas.
- En la pestaña Resumen de la consulta, seleccione el número de dispositivos con errores o sin conexión y, a continuación, seleccione la opción **Crear colección**. Esta opción hace que sea más fácil establecer el destino de dichos dispositivos con una implementación de la corrección.
- Para guardar las consultas **favoritas**, haga clic en el icono de carpeta.
   ![Ejemplo de cómo guardar una consulta favorita en CMPivot](media/cmpivot-favorite.png)

- Los clientes actualizados a la versión 1810 devuelven resultados inferiores a 80 KB al sitio a través de un canal de comunicación rápido.
  - Este cambio aumenta el rendimiento de la visualización de resultados del script o la consulta.
  - Si el resultado del script o la consulta es mayor que 80 KB, el cliente envía los datos a través de un mensaje de estado.
  - Si el cliente no se actualiza a la versión de cliente 1810, sigue usando los mensajes de estado.

### <a name="bkmk_cmpivot-functions"></a> Funciones escalares
CMPivot admite estas funciones escalares:
- **ago()** : resta el intervalo de tiempo dado de la hora UTC actual.  
- **datetime_diff()** : calcula la diferencia de calendario entre dos valores de fecha y hora.  
- **now()** : devuelve la hora de reloj UTC actual.  
- **bin()** : redondea valores a la baja a un número entero múltiplo del tamaño de una ubicación determinada.  

> [!Note]  
> El tipo de datos de fecha y hora representa un instante de tiempo, normalmente expresado como una fecha y hora del día. Los valores de tiempo se miden en unidades de 1 segundo. Siempre es un valor de fecha y hora en la zona horaria UTC. Siempre expresa literales de fecha y hora en formato ISO 8601, como por ejemplo, `yyyy-mm-dd HH:MM:ss`  

#### <a name="examples"></a>Ejemplos
- `datetime(2015-12-31 23:59:59.9)`: literal de fecha y hora específicas.   
- `now()`: hora actual.  
- `ago(1d)`: hora actual menos un día.  


### <a name="bkmk_cmpivot-charts"></a> Visualizaciones de representación

CMPivot ahora incluye compatibilidad básica para el [operador de representación](https://docs.microsoft.com/azure/kusto/query/renderoperator) de KQL. Esta compatibilidad incluye estos tipos:  
- **barchart**: la primera columna es el eje X y puede ser texto, fecha y hora o un valor numérico. La segunda columna debe ser numérica y se muestra como una banda horizontal.  
- **columnchart**: como barchart, con bandas verticales en lugar de bandas horizontales.  
- **piechart**: la primera columna es el eje de color y la segunda columna es numérica.  
- **timechart**: gráfico de líneas. La primera columna es el eje x y debe ser la fecha y hora. La segunda columna es el eje y.  

#### <a name="example-bar-chart"></a>Ejemplo: gráfico de barras
En esta consulta se representan las aplicaciones más usadas recientemente como un gráfico de barras:

```
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```
![Ejemplo de visualización de gráfico de barras de CMPivot](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>Ejemplo: gráfico de tiempo
Para representar gráficos de tiempo, use el nuevo operador **bin()** para agrupar eventos en el tiempo. En esta consulta se muestra cuándo se han iniciado los dispositivos en los últimos siete días:

``` 
OperatingSystem 
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```
![Ejemplo de visualización de gráfico de tiempo de CMPivot](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>Ejemplo: gráfico circular
En esta consulta se muestran todas las versiones de sistema operativo en un gráfico circular:

```
OperatingSystem 
| summarize count() by Caption
| render piechart
```
![Ejemplo de visualización de gráfico circular de CMPivot](media/1359068-cmpivot-piechart.png)


### <a name="bkmk_cmpivot-hinv"></a> Inventario de hardware
Use CMPivot para consultar cualquier clase de inventario de hardware. Estas clases incluyen cualquier extensión personalizada que realice en el inventario de hardware. CMPivot devuelve inmediatamente los resultados almacenados en caché desde el último examen de inventario de hardware almacenado en la base de datos del sitio. Al mismo tiempo, actualiza los resultados si es necesario con datos dinámicos de cualquier cliente en línea.

La saturación de color de los datos en la tabla de resultados o el gráfico indica si los datos se han transmitido en directo o se han almacenado en caché. Por ejemplo, el azul oscuro indica que los datos son en tiempo real desde un cliente en línea. El azul claro indica que los datos están almacenados en caché.

#### <a name="example"></a>Ejemplo
```
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```
![Ejemplo de consulta de inventario de CMPivot con visualización de gráfico de columnas](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>Limitaciones
- No se admiten estas entidades de inventario de hardware:  
    - Propiedades de la matriz, como por ejemplo, la dirección IP  
    - Real32/Real64 <!--example?-->  
    - Propiedades de objetos incrustados <!--example?-->  
- Los nombres de entidad de inventario deben empezar con un carácter
- No se pueden sobrescribir las entidades integradas mediante la creación de una entidad de inventario con el mismo nombre  


### <a name="bkmk_cmpivot-operators"></a> Operadores escalares
CMPivot incluye estos operadores escalares:  

> [!Note]  
> - LHS: cadena a la izquierda del operador  
> - RHS: cadena a la derecha del operador  


|Operador|Descripción|Ejemplo (da como resultado true)|
|--------|-----------|---------------------|
|==|Igual a|`"aBc" == "aBc"`|
|!=|No es igual a|`"abc" != "ABC"`|
|like|LHS contiene una coincidencia para RHS|`"FabriKam" like "%Brik%"`|
|!like|LHS no contiene ninguna coincidencia para RHS|`"Fabrikam" !like "%xyz%"`|
|contiene|RHS ocurre como una subsecuencia de LHS|`"FabriKam" contains "BRik"`|
|!contains|RHS no se produce en LHS|`"Fabrikam" !contains "xyz"`|
|startswith|RHS es una subsecuencia inicial de LHS|`"Fabrikam" startswith "fab"`|
|!startswith|RHS no es una subsecuencia inicial de LHS|`"Fabrikam" !startswith "kam"`|
|endswith|RHS es una subsecuencia de cierre de LHS|`"Fabrikam" endswith "Kam"`|
|!endswith|RHS no es una subsecuencia de cierre de LHS|`"Fabrikam" !endswith "brik"`|


### <a name="bkmk_cmpivot-summary"></a> Resumen de consulta

Seleccione la pestaña **Resumen de consulta** en la parte inferior de la ventana de CMPivot. Con este estado es más fácil identificar los clientes que están sin conexión o solucionar los errores que puedan producirse. Seleccione un valor en la columna Recuento para abrir una lista de dispositivos específicos con ese estado. 

Por ejemplo, seleccione el número de dispositivos con un estado de error. Vea el mensaje de error específico y exporte una lista de estos dispositivos. Si el error indica que no se reconoce un cmdlet específico, cree una colección de la lista de dispositivos exportados para implementar una actualización de Windows PowerShell.  

### <a name="cmpivot-audit-status-messages"></a>Mensajes de estado de auditoría de CMPivot

A partir de la versión 1810, al ejecutar CMPivot, se crea un mensaje de estado de auditoría con el **MessageID 40805**. Para ver los mensajes de estado, vaya a **Supervisión** < **Estado del sistema** < **Consultas de mensaje de estado**. Puede ejecutar **Todos los mensajes de estado de auditoría de un usuario específico** o **All Audit status Messages for a Specific Site** (Todos los mensajes de estado de auditoria de un sitio específico), o bien crear su propia consulta de mensaje de estado.

Se usa el formato siguiente para el mensaje:

MessageID 40805: El usuario &lt;nombre de usuario> ejecutó el script &lt;GUID de script> con el hash &lt;hash de script> en la colección &lt;id. de colección>.

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 es el GUID de script para CMPivot.
- El hash de script puede verse en el archivo scripts.log del cliente.
- También puede ver el hash almacenado en la puntuación del script de cliente. El nombre de archivo del cliente es &lt;GUID de script>_&lt;hash de script>.
    - Ejemplo de nombre de archivo: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123.ps
   

![Ejemplo de mensaje de estado de auditoría de CMPivot](media/cmpivot-audit-status-message.png)

## <a name="bkmk_cmpivot1902"></a> CMPivot a partir de la versión 1902
<!--3610960-->
A partir de Configuration Manager versión 1902, puede ejecutar CMPivot desde el sitio de administración central (CAS) en una jerarquía. El sitio primario sigue controlando la comunicación con el cliente. Al ejecutar CMPivot desde el sitio de administración central, se comunica con el sitio primario a través del canal de suscripción de mensajes de alta velocidad. Esta comunicación no depende de la replicación SQL estándar entre sitios.

Para ejecutar CMPivot en el CAS, se requieren permisos adicionales cuando SQL o el proveedor no están en el mismo equipo o en el caso de la configuración Always On de SQL. Con estas configuraciones remotas, tiene un "escenario de salto doble" para CMPivot.

Para que CMPivot funcione en el CAS con dicho "escenario de salto doble", puede definir una delegación restringida. Lea el artículo [Información general de la delegación restringida de Kerberos](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview) para entender las implicaciones de seguridad de esta configuración. Si tiene más de una configuración remota, como el proveedor de SCCM o SQL junto con el CAS, es posible que necesite una combinación de opciones de permisos. A continuación se muestran los pasos que debe realizar:

### <a name="cas-has-a-remote-sql-server"></a>El CAS tiene un servidor SQL remoto

1. Vaya al servidor SQL Server de cada sitio principal.
   1. Agregue el servidor SQL Server remoto del CAS y el servidor de sitio del CAS al grupo [Configmgr_DviewAccess](/sccm/core/plan-design/hierarchy/accounts#configmgr_dviewaccess).
   ![Grupo Configmgr_DviewAccess en el servidor SQL Server de un sitio principal](media/cmpivot-dviewaccess-group.png)
1. Vaya a Usuarios y equipos de Active Directory.
   1. Para cada servidor de sitio principal, haga clic con el botón derecho y seleccione **Propiedades**.
      1. En la pestaña Delegación, seleccione la tercera opción: **Confiar en este equipo para la delegación solo a los servicios especificados**. 
      1. Seleccione **Usar solamente Kerberos**.
      1. Agregue el servicio de SQL Server del CAS con el puerto y la instancia.
      1. Asegúrese de que estos cambios se ajustan a la directiva de seguridad de su empresa.
   1. Para el sitio del CAS, haga clic con el botón derecho y seleccione **Propiedades**.
      1. En la pestaña Delegación, seleccione la tercera opción: **Confiar en este equipo para la delegación solo a los servicios especificados**. 
      1. Seleccione **Usar solamente Kerberos**.
      1. Agregue el servicio de SQL Server de cada sitio principal con el puerto y la instancia.
      1. Asegúrese de que estos cambios se ajustan a la directiva de seguridad de su empresa.

   ![Ejemplo de delegación de AD de CMPivot para saltos dobles](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>El CAS tiene un proveedor remoto

1. Vaya al servidor SQL Server de cada sitio principal.
   1. Agregue la cuenta del equipo del proveedor del CAS y el servidor de sitio del CAS al grupo [Configmgr_DviewAccess](/sccm/core/plan-design/hierarchy/accounts#configmgr_dviewaccess).
1. Vaya a Usuarios y equipos de Active Directory.
   1. Seleccione el equipo del proveedor del CAS, haga clic con el botón derecho y seleccione **Propiedades**.
      1. En la pestaña Delegación, seleccione la tercera opción: **Confiar en este equipo para la delegación solo a los servicios especificados**. 
      1. Seleccione **Usar solamente Kerberos**.
      1. Agregue el servicio de SQL Server de cada sitio principal con el puerto y la instancia.
      1. Asegúrese de que estos cambios se ajustan a la directiva de seguridad de su empresa.
   1. Seleccione el servidor de sitio del CAS, haga clic con el botón derecho y seleccione **Propiedades**.
      1. En la pestaña Delegación, seleccione la tercera opción: **Confiar en este equipo para la delegación solo a los servicios especificados**. 
      1. Seleccione **Usar solamente Kerberos**.
      1. Agregue el servicio de SQL Server de cada sitio principal con el puerto y la instancia.
      1. Asegúrese de que estos cambios se ajustan a la directiva de seguridad de su empresa.
1. Reinicie el equipo del proveedor remoto del CAS.

### <a name="sql-always-on"></a>Always On de SQL

1. Vaya al servidor SQL Server de cada sitio principal.
   1. Agregue el servidor de sitio del CAS al grupo [Configmgr_DviewAccess](/sccm/core/plan-design/hierarchy/accounts#configmgr_dviewaccess).
1. Vaya a Usuarios y equipos de Active Directory.
   1. Para cada servidor de sitio principal, haga clic con el botón derecho y seleccione **Propiedades**.
      1. En la pestaña Delegación, seleccione la tercera opción: **Confiar en este equipo para la delegación solo a los servicios especificados**. 
      1. Seleccione **Usar solamente Kerberos**.
      1. Agregue las cuentas de servicio del servidor SQL Server del CAS para los nodos de SQL con el puerto y la instancia.
      1. Asegúrese de que estos cambios se ajustan a la directiva de seguridad de su empresa.
   1. Seleccione el servidor de sitio del CAS, haga clic con el botón derecho y seleccione **Propiedades**.
      1. En la pestaña Delegación, seleccione la tercera opción: **Confiar en este equipo para la delegación solo a los servicios especificados**. 
      1. Seleccione **Usar solamente Kerberos**.
      1. Agregue el servicio de SQL Server de cada sitio principal con el puerto y la instancia.
      1. Asegúrese de que estos cambios se ajustan a la directiva de seguridad de su empresa.
1. Asegúrese de que el [SPN se publique](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs) para el nombre del cliente de escucha de SQL del CAS y para cada nombre del cliente de escucha de SQL principal.
1. Reinicie los servidores principales de SQL Server.
1. Reinicie el servidor de sitio del CAS y los servidores SQL Server del CAS.


## <a name="inside-cmpivot"></a>Dentro de CMPivot

CMPivot envía consultas a los clientes que usan el "canal rápido" de Configuration Manager. Otras características como las acciones de notificación de cliente, el estado de cliente y Endpoint Protection también utilizan este canal de comunicación del servidor al cliente. Los clientes devuelven resultados mediante el sistema de mensajes de estado que es igual de rápido. Los mensajes de estado se almacenan temporalmente en la base de datos. Para obtener más información sobre los puertos usados para la notificación de cliente, vea el artículo [Puertos](/sccm/core/plan-design/hierarchy/ports#BKMK_PortsClient-MP).

Las consultas y los resultados son todo texto. Las entidades **InstallSoftware** y **Proceso** devuelven algunos de los conjuntos de resultados más grandes. Durante las pruebas de rendimiento, el tamaño de archivo de mensaje de estado más grande de equipo cliente para estas consultas era menor de **1 KB**. Escalada a un entorno grande con 50 000 clientes activos, esta consulta única generaría menos de 50 MB de datos a través de la red. Todos los elementos subrayados en la página principal devolverán menos de 1 KB de información por cliente.

![Ejemplo de entidades subrayadas de CMPivot](media/cmpivot-underlined-entities.png)

A partir de Configuration Manager 1810, CMPivot puede consultar datos de inventario de hardware, incluidas las clases de inventario ampliado de hardware. Estas nuevas entidades (que no están subrayadas en la página principal) pueden devolver conjuntos de datos mucho mayores, en función de la cantidad de datos que se haya definido para una propiedad determinada de inventario de hardware. Por ejemplo, la entidad "InstalledExecutable" podría devolver varios megabytes de datos por cliente, según los datos específicos sobre los que se realice la consulta. Tenga en cuenta el rendimiento y la escalabilidad de los sistemas cuando se devuelvan grandes conjuntos de datos de inventario de hardware procedentes de colecciones más grandes mediante el uso de CMPivot.

Una consulta agota el tiempo de espera después de una hora. Por ejemplo, una colección tiene 500 dispositivos y 450 de los clientes están actualmente en línea. Los dispositivos activos reciben la consulta y devuelven los resultados casi de inmediato. Si deja la ventana CMPivot abierta, a medida que los 50 clientes restantes se conecten, también recibirán la consulta y devolverán resultados. 

## <a name="log-files"></a>Archivos de registro

 Las interacciones de CMPivot se registran en los archivos de registro siguientes:

**Servidor:**
- SmsProv.log
- BgbServer.log
- StateSys.log

**Cliente:**
 - CCMNotificationAgent.log
 - Scripts.log
 - StateMessage.log

Para obtener más información, vea [Archivos de registro](/sccm/core/plan-design/hierarchy/log-files) y [Solución de problemas de CMPivot](/sccm/core/servers/manage/cmpivot-tsg).

## <a name="next-steps"></a>Pasos siguientes
 
[Solución de problemas de CMPivot](/sccm/core/servers/manage/cmpivot-tsg)

[Crear y ejecutar scripts de PowerShell](/sccm/apps/deploy-use/create-deploy-scripts)


