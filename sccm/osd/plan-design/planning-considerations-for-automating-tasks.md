---
title: "Planeamiento de consideraciones para la automatización de tareas | Configuration Manager"
description: Planee antes de automatizar tareas en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
caps.latest.revision: 13
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a439d847adb129a341b33be8e1a1674c72184e77


---
# <a name="planning-considerations-for-automating-tasks-in-system-center-configuration-manager"></a>Planeación de consideraciones para la automatización de tareas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede crear secuencias de tareas para automatizar tareas en su entorno de System Center Configuration Manager. Estas tareas van desde la captura de un sistema operativo en un equipo de referencia hasta la implementación del sistema operativo en uno o varios equipos de destino. Las acciones de la secuencia de tareas se definen en los pasos individuales de la secuencia. Cuando se ejecuta la secuencia de tareas, se realizan las acciones de cada etapa en el nivel de la línea de comandos en el contexto del sistema local sin necesidad de intervención del usuario. Use las secciones siguientes como ayuda para planear la automatización de tareas en Configuration Manager.

##  <a name="a-namebkmktsstepsactionsa-task-sequence-steps-and-actions"></a><a name="BKMK_TSStepsActions"></a> Acciones y etapas de una secuencia de tareas  
 Los pasos son los componentes básicos de una secuencia de tareas. Pueden contener comandos que configuran y capturan el sistema operativo de un equipo de referencia, o pueden contener comandos que instalan el sistema operativo, controladores, el cliente de Configuration Manager y software en el equipo de destino. Los comandos de un paso de la secuencia de tareas se definen mediante las acciones del paso. Existen dos tipos de acciones. Una acción definida mediante una cadena de línea de comandos se conoce como una acción personalizada. Una acción predefinida por Configuration Manager se conoce como una acción integrada. Una secuencia de tareas puede realizar cualquier combinación de acciones personalizadas e integradas.  

 Los pasos de la secuencia de tareas también pueden incluir condiciones que controlan cómo se comporta el paso, como detener la secuencia de tareas o continuar la secuencia de tareas si se produce un error. Las condiciones se agregan al paso mediante la inclusión de una variable de secuencia de tareas para el paso. Por ejemplo, puede utilizar la variable **SMSTSLastActionRetCode** para probar la condición del paso anterior. Las variables pueden agregarse a un solo paso o a un grupo de pasos.  

 Los pasos de la secuencia de tareas se procesan secuencialmente, lo que incluye la acción del paso y todas las condiciones asignadas al paso. Cuando Configuration Manager comienza a procesar un paso de la secuencia de tareas, el paso siguiente no se inicia hasta que haya finalizado la acción anterior. Una secuencia de tareas se considera completada cuando se completan todos los pasos o cuando un paso con errores hace que Configuration Manager deje de ejecutar la secuencia de tareas antes de completar todos sus pasos. Por ejemplo, si el paso de una secuencia de tareas no puede encontrar una imagen o un paquete a los que se hace referencia en un punto de distribución, la secuencia de tareas contiene una referencia errónea y Configuration Manager deja de ejecutar la secuencia de tareas en ese momento, a menos que el paso con errores tenga una condición que especifique que continúe cuando se produce un error.  

> [!IMPORTANT]  
>  De forma predeterminada, una secuencia de tareas produce un error después de que un paso o una acción produzcan un error. Si quiere que la secuencia de tareas continúe incluso cuando un paso produce error, edite la secuencia de tarea, haga clic en la pestaña **Opciones** y luego seleccione **Continuar después del error**.  

 Para obtener más información sobre los pasos que se pueden agregar a una secuencia de tareas, consulte [Pasos de la secuencia de tareas](../understand/task-sequence-steps.md).  

##  <a name="a-namebkmktsgroupsa-task-sequence-groups"></a><a name="BKMK_TSGroups"></a> Grupos de secuencias de tareas  
 Los **Grupos** son varios pasos dentro de una secuencia de tareas. Un grupo de secuencia de tareas consta de un nombre, una descripción opciones y cualquier condición opcional evaluada como una unidad antes de que la secuencia de tareas siga con el paso siguiente. Los grupos pueden anidarse dentro de otros; un grupo puede contener una combinación de pasos y subgrupos. Los grupos son útiles para la combinación de varios pasos que comparten una condición común.  

> [!IMPORTANT]  
>  De forma predeterminada, se produce un error de un grupo de secuencia de tareas cuando se produce un error en cualquier paso o grupo integrado dentro del grupo. Si quiere que la secuencia de tareas continúe cuando un paso o un grupo integrado produzca error, edite la secuencia de tareas, haga clic en la pestaña **Opciones** y luego seleccione **Continuar después del error**.  

 La tabla siguiente muestra cómo funciona la opción **Continuar después de un error** cuando se agrupan pasos.  

 En este ejemplo, hay dos grupos que contienen tres pasos de secuencia de tareas cada uno.  

|Grupo o paso de secuencia de tareas|Valor Continuar después de un error|  
|---------------------------------|-------------------------------|  
|**Grupo de secuencia de tareas 1**|**Continuar después de un error** seleccionado.|  
|Paso de secuencia de tareas 1|**Continuar después de un error** seleccionado.|  
|Paso de secuencia de tareas 2|No establecido.|  
|Paso de secuencia de tareas 3|No establecido.|  
|**Grupo de secuencia de tareas 2**|No establecido.|  
|Paso de secuencia de tareas 4|No establecido.|  
|Paso de secuencia de tareas 5|No establecido.|  
|Paso de secuencia de tareas 6|No establecido.|  

-   Si se produce un error en el paso de la secuencia de tareas 1, la secuencia de tareas continúa con el paso 2.  

-   Si se produce un error en el paso de secuencia de tareas 2, la secuencia de tareas no ejecuta el paso 3, pero ejecuta los pasos 4 y 5, que se encuentran en un grupo diferente.  

-   Si se produce un error en el paso de secuencia de tareas 4, no se ejecuta ningún paso más y la secuencia de tareas produce un error porque el valor **Continuar después de un error** no se configuró para el grupo de secuencia de tareas 2.  

 Debe asignar un nombre a los grupos de secuencias de tareas, aunque el nombre del grupo no tiene que ser único. También puede proporcionar una descripción opcional para el grupo de secuencia de tareas.  

##  <a name="a-namebkmktsvariablesa-task-sequence-variables"></a><a name="BKMK_TSVariables"></a> Variables de secuencias de tareas  
 Las variables de secuencia de tareas son un conjunto de pares de nombre y valor que proporcionan valores de configuración y de implementación del sistema operativo para tareas de configuración del estado del usuario, equipo y sistema operativo en un equipo cliente de Configuration Manager. Las variables de secuencia de tareas proporcionan un mecanismo para configurar y personalizar los pasos en una secuencia de tareas.  

 Cuando se ejecuta una secuencia de tareas, muchos de los valores de configuración de la secuencia de tareas se almacenan como variables de entorno. Puede acceder a los valores de variables de secuencia de tareas integradas, o cambiarlos, y puede crear nuevas variables de secuencia de tareas para personalizar la forma en que una secuencia de tareas se ejecuta en un equipo de destino.  

 Puede utilizar variables de secuencia tareas en el entorno de la secuencia de tareas para realizar las siguientes acciones:  

-   Configurar las opciones de una acción de la secuencia de tareas  

-   Proporcionar argumentos de la línea de comandos para un paso de la secuencia de tareas  

-   Evaluar una condición que determina si se ejecuta un paso o un grupo de la secuencia de tareas  

-   Proporcionar valores para scripts personalizados usados en una secuencia de tareas  

 Por ejemplo, podría tener una secuencia de tareas que incluyera un paso de secuencia de tareas **Unirse a dominio o grupo de trabajo**. La secuencia de tareas podría implementarse en diferentes recopilaciones, donde la pertenencia de la recopilación viene determinada por la pertenencia al dominio. En ese caso, puede especificar una variable de secuencia de tareas por recopilación para cada nombre de dominio de recopilación y, después, usar esa variable de secuencia de tareas para proporcionar el nombre de dominio apropiado en la secuencia de tareas.  

###  <a name="a-namebkmktscreatevariablesa-create-task-sequence-variables"></a><a name="BKMK_TSCreateVariables"></a> Creación de variables de secuencias de tareas  
 Puede agregar nuevas variables de secuencia de tareas para personalizar y controlar los pasos en una secuencia de tareas. Por ejemplo, puede crear una variable de secuencia de tareas para reemplazar un valor de configuración de un paso de secuencia de tareas integrado. También puede crear una variable de secuencia de tareas personalizada para usar con condiciones, líneas de comando o pasos personalizados en la secuencia de tareas. Cuando cree una variable de secuencia de tareas, la variable y el valor asociado se mantendrán dentro del entorno de la secuencia de tareas, incluso cuando la secuencia reinicie el equipo de destino. La variable y su valor pueden utilizarse dentro de la secuencia de tareas en entornos de sistema operativo diferentes. Por ejemplo, puede usarse en un sistema operativo de Windows completo y en el entorno de Windows PE.  

 La tabla siguiente describe los métodos para crear una variable de secuencia de tareas e información de uso adicional.  

|Método de creación|Uso|  
|-------------------|-----------|  
|Configurar los campos en los pasos de la secuencia de tareas mediante el Editor de secuencia de tareas|Especifica los valores predeterminados para el paso de la secuencia de tareas. La variable y su valor son accesibles solo cuando el paso se ejecuta en la secuencia de tareas. No forman parte del entorno de la secuencia general y no son accesibles para otros pasos de la secuencia de tareas.<br /><br /> Para obtener una lista de las variables integradas y sus acciones asociadas, consulte [Variables de acción de secuencias de tareas](../understand/task-sequence-action-variables.md).|  
|Agregar un paso de variable de secuencia de tareas en una secuencia de tareas|Especifica la variable de secuencia de tareas y el valor en el entorno de secuencia de tareas cuando se ejecuta el paso como parte de una secuencia de tareas. Todos los pasos de secuencia de tareas posteriores pueden tener acceso a la variable de entorno y su valor.|  
|Definir una variable por recopilación|Especifica las variables de secuencia de tareas y los valores de una recopilación de equipos. Todas las secuencias de tareas destinadas a la recopilación pueden tener acceso a las variables de secuencia de tareas y sus valores.|  
|Definir una variable por equipo|Especifica las variables de secuencia de tareas y los valores de un equipo determinado. Todas las secuencias de tareas destinadas al equipo pueden tener acceso a las variables de secuencia de tareas y sus valores.|  
|Agregar una variable de secuencia de tareas en la página **Personalización** del Asistente para crear medio de secuencia de tareas|Especifica las variables de secuencia de tareas y los valores para la secuencia de tareas que se ejecuta desde el medio que puede tener acceso a la variable de secuencia de tareas y su valor.|  

 Para reemplazar el valor predeterminado de una variable de secuencia de tareas integrada, debe definir una variable de secuencia de tareas con el mismo nombre que la variable de secuencia de tareas integrada. Para obtener una lista de variables de secuencia de tareas integradas con las acciones asociadas y el uso, consulte [Variables integradas de secuencia de tareas](../understand/task-sequence-built-in-variables.md).  

 Puede eliminar una variable de secuencia de tareas desde el entorno de secuencia de tareas con los mismos métodos usados para la creación de una variable de secuencia de tareas. En este caso, para eliminar una variable desde el entorno de secuencia de tareas, establezca el valor de la variable de secuencia de tareas en una cadena vacía.  

 Puede combinar métodos para establecer una variable de secuencia de tareas de entorno en valores diferentes para la misma secuencia. En un escenario avanzado, podría configurar los valores predeterminados de los pasos en una secuencia mediante el Editor de secuencia de tareas y, después, establecer un valor de variable personalizado mediante métodos de creación diferentes. La lista siguiente describe las reglas que determinan qué valor se utiliza cuando se crea una variable de secuencia de tareas mediante el uso de más de un método.  

1.  El paso **Configurar variable de secuencia de tareas** reemplaza todos los demás métodos de creación.  

2.  Las variables por equipo tienen prioridad sobre las variables por recopilación. Si especifica el mismo nombre de variable de secuencia de tareas para una variable por equipo y una variable por recopilación, el valor de la variable por equipo se usará cuando el equipo de destino ejecute la secuencia de tareas implementada.  

3.  Las secuencias de tareas se pueden ejecutar desde un medio. Use las variables de los medios en lugar de las variables por recopilación o por equipo. Si se está ejecutando la secuencia de tareas desde un medio, las variables por equipo y por recopilación no se aplican y no se utilizan. En su lugar, se usan las variables de secuencia de tareas definidas en la página **Personalización** del Asistente para crear medio de secuencia de tareas para configurar valores específicos en una secuencia de tareas que se ejecuta desde un medio.  

4.  Si el valor de la variable de secuencia de tareas no se configura en el entorno de la secuencia general, las acciones integradas usarán el valor predeterminado del paso, tal como esté configurado en el Editor de secuencia de tareas.  

 Además de invalidar valores de configuración de pasos de secuencia de tareas integrados, también puede crear una nueva variable de entorno para usar en un paso de secuencia de tareas, script, línea de comandos o condición. Cuando especifique un nombre para una nueva variable de secuencia de tareas, siga estas instrucciones:  

-   El nombre de la variable de secuencia de tareas que especifique puede contener letras, números, el carácter de subrayado (_) y un guión (-).  

-   El nombre de la variable de secuencia de tareas tiene una longitud mínima de 1 carácter y una longitud máxima de 256 caracteres.  

-   Las variables definidas por el usuario deben comenzar con una letra (A-z o a-z).  

-   Los nombres de las variables definidas por el usuario no pueden comenzar con el carácter de subrayado. Solo las variables de secuencia de tareas de solo lectura van precedidas por el carácter de subrayado.  

    > [!NOTE]  
    >  Los pasos de secuencia de tareas pueden leer las variables de secuencia de tareas de solo lectura en una secuencia de tareas, pero no pueden configurarse. Por ejemplo, puede usar una variable de secuencia de tareas de solo lectura como parte de la línea de comandos para una variable de acción de secuencia de tareas **Ejecutar línea de comandos**, pero no puede configurar una variable de solo lectura con la variable de acción **Configurar variable de secuencia de tareas**.  

-   Los nombres de variables de secuencia de tareas no distinguen mayúsculas de minúsculas. Por ejemplo, OSDVAR y osdvar representan la misma variable de secuencia de tareas.  

-   Los nombres de variables de secuencia de tareas no pueden comenzar ni terminar con un espacio; tampoco pueden contener espacios incrustados. Los espacios que quedan al principio o al final de un nombre de variable de secuencia de tareas se ignoran.  

 La tabla siguiente contiene ejemplos de variables de secuencia de tareas especificadas por el usuario válidas y no válidas.  

|Ejemplos de nombres de variables especificadas por el usuario válidas|Ejemplos de nombres de variables especificadas por el usuario no válidas|  
|-------------------------------------------------------|----------------------------------------------------------|  
|MyVariable|1Variable<br /><br /> Las variables de secuencia de tareas especificadas por el usuario no pueden empezar por un número.|  
|My_Variable|MyV@riable<br /><br /> Las variables de secuencia de tareas especificadas por el usuario no pueden contener el símbolo @.|  
|My_Variable_2|_MyVariable<br /><br /> Las variables de secuencia de tareas especificadas por el usuario no pueden empezar por un carácter de subrayado.|  

 Limitaciones generales para las variables de secuencia de tareas:  

-   Los valores de las variables de secuencia de tareas no pueden superar los 4.000 caracteres.  

-   No se puede crear o reemplazar una variable de secuencia de tareas de solo lectura. Las variables de solo lectura se designan mediante nombres que empiezan por un carácter de subrayado (_). Puede acceder al valor de las variables de secuencia de tareas de solo lectura en su secuencia de tareas; sin embargo, no puede cambiar los valores asociados.  

-   Los valores de variables de secuencias de tareas pueden distinguir entre mayúsculas y minúsculas dependiendo del uso del valor. En la mayoría de los casos, los valores de variables de secuencias de tareas no distinguen entre mayúsculas y minúsculas. Sin embargo, algunos valores pueden distinguir entre mayúsculas y minúsculas, como una variable que contiene una contraseña.  

-   No hay ningún límite respecto al número de variables de secuencias de tareas que se pueden crear. Sin embargo, el número de variables está limitado por el tamaño del entorno de secuencia de tareas. El límite de tamaño total para el entorno de secuencia de tareas es de 32 MB.  

###  <a name="a-namebkmktsenvironmentvariablesa-access-environment-variables"></a><a name="BKMK_TSEnvironmentVariables"></a> Acceso a variables de entorno  
 Después de especificar la variable de secuencia de tareas y su valor mediante uno de los métodos indicados en la sección anterior, puede utilizar el valor de la variable de entorno en sus secuencias de tareas. Puede acceder a los valores predeterminados de las variables de secuencia de tareas integradas, especificar un nuevo valor para una variable integrada o utilizar una variable de secuencia de tareas personalizada en una línea de comandos o un script.  

 En la tabla siguiente se describen las operaciones de secuencia de tareas que se pueden realizar mediante el acceso a las variables de entorno de secuencia de tareas.  

|Operación de secuencia de tareas|Uso|  
|-----------------------------|-----------|  
|Configurar las opciones de una acción|Puede especificar que se proporcione una opción de paso de la secuencia de tareas mediante un valor de la variable cuando se ejecuta la secuencia.<br /><br /> Para proporcionar una opción de paso de la secuencia de tareas mediante una variable de entorno de secuencia de tareas, utilice el Editor de secuencia de tareas para editar el paso y especifique el nombre de la variable como el valor de campo. El nombre de la variable debe ir entre signos de porcentaje (%) para indicar que se trata de una variable de entorno.|  
|Proporcionar argumentos de la línea de comandos|Puede especificar una línea de comandos personalizada, parcial o totalmente, mediante un valor de la variable de entorno.<br /><br /> Para proporcionar una opción de la línea de comandos mediante una variable de entorno, use el nombre de la variable como parte del campo **Línea de comandos** del paso de la secuencia de tareas **Ejecutar línea de comandos**. El nombre de la variable debe ir entre signos de porcentaje (%).<br /><br /> Por ejemplo, en la siguiente línea de comandos se utiliza una variable de entorno integrada para escribir el nombre del equipo en C:\File.txt.<br /><br /> <br /><br /> **Cmd /C %_SMSTSMachineName% > C:\File.txt**|  
|Evaluar una condición de un paso|Puede utilizar variables de entorno de secuencia de tareas integradas o personalizadas como parte de una condición de paso o de grupo de secuencia de tareas. El valor de la variable de entorno se evaluará antes de que se ejecute el paso o el grupo de la secuencia de tareas.<br /><br /> Para agregar una condición que evalúa un valor de variable, haga lo siguiente:<br /><br /> 1.  Seleccione el paso o el grupo al que desea agregar la condición.<br />2.  En la pestaña **Opciones** correspondiente al paso o al grupo, seleccione **Variable de secuencia de tareas** en la lista desplegable **Agregar condición**.<br />3.  En el cuadro de diálogo **Variable de secuencia de tareas**, especifique el nombre de la variable, la condición que se prueba y el valor de la variable.|  
|Proporcionar información para un script personalizado|Las variables de la secuencia de tareas se pueden leer y escribir mediante el objeto COM de Microsoft.SMS.TSEnvironment mientras la secuencia de tareas está en ejecución.<br /><br /> En el ejemplo siguiente, un archivo de script de Visual Basic consulta la variable de secuencia de tareas **_SMSTSLogPath** para obtener la ubicación del registro actual. El script también establece una variable personalizada.<br /><br /> <br /><br /> **dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")**<br /><br /> <br /><br /> **dim logPath**<br /><br /> <br /><br /> **' Puede consultar el entorno para obtener una variable existente.**<br /><br /> **logPath = env("_SMSTSLogPath")**<br /><br /> <br /><br /> **' También se puede establecer una variable en el entorno de OSD.**<br /><br /> **env("MyCustomVariable") = "varname"**<br /><br /> <br /><br /> Para obtener más información acerca de cómo utilizar las variables de secuencia de tareas en scripts, consulte la documentación del SDK.|  

###  <a name="a-namebkmkcomputercollectionvariablesa-computer-and-collection-variables"></a><a name="BKMK_ComputerCollectionVariables"></a> Variables de equipo y colección  
 Puede configurar las secuencias de tareas para que se ejecuten simultáneamente en varios equipos o recopilaciones. Puede especificar información exclusiva de cada equipo o cada recopilación; por ejemplo, puede especificar una clave de producto exclusiva del sistema operativo o unir todos los miembros de una recopilación en un dominio especificado.  

 Puede asignar las variables de secuencia de tareas a un único equipo o una recopilación. Cuando la secuencia de tareas se inicia para ejecutarse en el equipo o la recopilación de destino, los valores especificados se aplican al equipo o a la recopilación de destino.  

 Puede especificar las variables de secuencia de tareas de un único equipo o una recopilación. Cuando la secuencia de tareas se inicia para ejecutarse en el equipo o la recopilación de destino, las variables especificadas se agregan al entorno y los valores están disponibles para todos los pasos de la secuencia de tareas.  

> [!WARNING]  
>  Si utiliza el mismo nombre de variable para las variables de una recopilación y de un equipo, el valor de la variable del equipo tiene prioridad sobre la variable de la recopilación. Las variables de secuencia de tareas que se asignan a las recopilaciones tienen prioridad sobre las variables de secuencia de tareas integradas.  

 Para obtener más información sobre cómo crear variables de secuencia de tareas para equipos y recopilaciones, consulte [Creación de variables de secuencia de tareas para equipos y recopilaciones](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTSVariables).  

###  <a name="a-namebkmktsmediavariablesa-task-sequence-media-variables"></a><a name="BKMK_TSMediaVariables"></a> Variables de medio de secuencia de tareas  
 Puede especificar variables de secuencia de tareas para las secuencias de tareas que se ejecutan desde un medio. Cuando se utiliza un medio para implementar el sistema operativo se agregan las variables de secuencia de tareas y se especifican sus valores al crear el medio; las variables y sus valores se almacenan en el medio.  

> [!NOTE]  
>  Las secuencias de tareas se almacenan en medios independientes. Sin embargo, todos los demás tipos de medios, como los medios preconfigurados, recuperan la secuencia de tareas desde un punto de administración.  

 Puede especificar las variables de secuencia de tareas en la página **Personalización** del Asistente para crear medio de secuencia de tareas. Para obtener más información sobre cómo usar los medios, consulte [Creación de medios de secuencia de tareas](../deploy-use/create-task-sequence-media.md).  

> [!TIP]  
>  La secuencia de tareas escribe el identificador de paquete y el comando de preinicio, incluidos los valores de las variables de secuencia de tareas, en el archivo de registro CreateTSMedia.log en el equipo que ejecuta la consola de Configuration Manager. Puede revisar este archivo de registro para comprobar el valor de las variables de secuencia de tareas.  

##  <a name="a-namebkmktscreatea-create-a-task-sequence"></a><a name="BKMK_TSCreate"></a> Creación de una secuencia de tareas  
 Las secuencias de tareas se crean mediante el Asistente para crear secuencia de tareas. El asistente puede crear secuencias de tareas integradas que realizan tareas específicas o secuencias de tareas personalizadas que pueden realizar muchas tareas diferentes.  

 Por ejemplo, es posible crear secuencias de tareas que permiten generar y capturar una imagen del sistema operativo de un equipo de referencia, instalar la imagen de un sistema operativo existente en un equipo de destino o crear una secuencia de tareas personalizada que realiza una tarea personalizada. Las secuencias de tareas personalizadas se pueden usar para realizar implementaciones de sistema operativo especializadas.  

 Para obtener más información sobre cómo crear secuencias de tareas, consulte [Crear secuencias de tareas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence).  

##  <a name="a-namebkmktsedita-edit-a-task-sequence"></a><a name="BKMK_TSEdit"></a> Edición de una secuencia de tareas  
 Una secuencia de tareas se edita mediante el **Editor de secuencia de tareas**. El editor permite realizar los siguientes cambios en la secuencia de tareas:  

-   Se puede agregar o quitar pasos de la secuencia de tareas.  

-   Se puede cambiar el orden de los pasos de la secuencia de tareas.  

-   Se puede agregar o quitar grupos de pasos.  

-   Se puede especificar si la secuencia de tareas continúa cuando se produce un error.  

-   Se puede agregar condiciones a los pasos y grupos de una secuencia de tareas.  

> [!IMPORTANT]  
>  Si la secuencia de tareas tiene referencias sin asociar a un paquete o a un programa a consecuencia de la edición, debe corregir la referencia, eliminar el programa sin referencia de la secuencia de tareas o deshabilitar temporalmente el paso de la secuencia de tareas con errores hasta que la referencia errónea se corrija o se quite.  

 Para obtener más información sobre cómo editar una secuencia de tareas, consulte [Editar una secuencia de tareas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

##  <a name="a-namebkmktsdeploya-deploy-a-task-sequence"></a><a name="BKMK_TSDeploy"></a> Implementación de una secuencia de tareas  
 Se puede implementar una secuencia de tareas en equipos de destino que estén en cualquier recopilación de Configuration Manager. Se incluye la recopilación **Todos los equipos desconocidos** que se utiliza para implementar sistemas operativos en equipos desconocidos. Sin embargo, no se puede implementar una secuencia de tareas en recopilaciones de usuarios.  

> [!IMPORTANT]  
>  No implemente secuencias de tareas que instalen sistemas operativos en recopilaciones inapropiadas, como la recopilación **Todos los sistemas** . Asegúrese de que la recopilación en la que implementa la secuencia de tareas contenga solo los equipos en los que desea instalar el sistema operativo. Para evitar una implementación de sistema operativo no deseada, puede administrar la configuración de implementación. Para obtener más información, consulte [Configuración para administrar implementaciones de alto riesgo](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

 Cada equipo de destino que recibe la secuencia de tareas la ejecuta según la configuración especificada en la implementación. Las secuencias de tareas no contienen programas o archivos asociados. Todos los archivos a los que hace referencia una secuencia de tareas deben estar ya presentes en el equipo de destino o residir en un punto de distribución al que puedan acceder los clientes. Además, la secuencia de tareas instala los paquetes a los que hacen referencia los programas, aunque el programa o el paquete ya esté instalado en el equipo de destino.  

> [!NOTE]  
>  En comparación con los paquetes y los programas, si la secuencia de tareas instala una aplicación, la aplicación se instala solo si las reglas de requisitos de la misma se cumplen y si no está ya instalada, según el método de detección especificado para la aplicación.  

 El cliente de Configuration Manager ejecuta una implementación de secuencia de tareas cuando descarga la directiva de cliente. Para iniciar esta acción en lugar de esperar hasta el próximo ciclo de sondeo, consulte [Inicio de la recuperación de directivas para un cliente de Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 Cuando se implementan secuencias de tareas en dispositivos de Windows Embedded con filtros de escritura habilitados, se puede especificar si se desea deshabilitar el filtro de escritura en el dispositivo durante la implementación y luego reiniciar el dispositivo después de esta operación. Si no se deshabilita el filtro de escritura, la secuencia de tareas se implementa en una superposición temporal y no estará disponible cuando se reinicie el dispositivo.  

> [!NOTE]  
>  Cuando implemente una secuencia de tareas en un dispositivo de Windows Embedded, asegúrese de que el dispositivo es miembro de una recopilación que tenga una ventana de mantenimiento configurada. Esto le permite administrar cuándo se deshabilita y habilita el filtro de escritura, y cuándo se reinicia el dispositivo.  
>   
>  Si los clientes descargan secuencias de tareas fuera de una ventana de mantenimiento, la secuencia de tareas se descarga dos veces. En este escenario los clientes descargan la secuencia de tareas, deshabilitan los filtros de escritura, reinician el equipo y, a continuación, descargan la secuencia de tareas de nuevo porque se descargó en la superposición temporal que se borra al reiniciarse el dispositivo.  

 Para obtener más información sobre cómo implementar secuencias de tareas, consulte [Implementar una secuencia de tareas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

##  <a name="a-namebkmktsexportimporta-export-and-import-a-task-sequences"></a><a name="BKMK_TSExportImport"></a> Exportación e importación de una secuencia de tareas  
 Configuration Manager permite exportar e importar secuencias de tareas. Al exportar una secuencia de tareas, puede incluir los objetos a los que hace referencia la secuencia de tareas. Se incluyen una imagen de sistema operativo, una imagen de arranque, un paquete de agente cliente, un paquete de controladores y las aplicaciones que tienen dependencias.  

> [!NOTE]  
>  El proceso de exportación e importación de las secuencias de tareas es muy similar al proceso de exportación e importación de las aplicaciones de Configuration Manager.  

 Para obtener más información sobre cómo exportar e importar secuencias de tareas, consulte [Exportación e importación de secuencias de tareas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport).  

##  <a name="a-namebkmktsruna-run-a-task-sequence"></a><a name="BKMK_TSRun"></a> Ejecución de una secuencia de tareas  
 De forma predeterminada las secuencias de tareas siempre se ejecutan mediante la cuenta de sistema local. El paso de la línea de comandos de la secuencia de tareas permite ejecutar la secuencia de tareas como una cuenta diferente. Cuando se ejecuta la secuencia de tareas, el cliente de Configuration Manager comprueba en primer lugar si hay paquetes con referencia antes de iniciar los pasos de la secuencia de tareas. Si un paquete con referencia no se valida o no está disponible en un punto de distribución, la secuencia de tareas devuelve un error para el paso de la secuencia de tareas asociado.  

 Si una secuencia de tareas distribuida está configurada para descargarse y ejecutarse, todos los paquetes y aplicaciones dependientes se descargan en la caché del cliente de Configuration Manager. Los paquetes y aplicaciones necesarios se obtienen de los puntos de distribución, y si la caché del cliente de Configuration Manager es demasiado reducida o no se encuentra el paquete o la aplicación, la secuencia de tareas produce un error y se genera un mensaje de estado. También se puede especificar que el cliente descargue el contenido solo cuando sea necesario si se selecciona **Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas**, o se puede utilizar la opción **Ejecutar programa desde el punto de distribución** para especificar que el cliente instale los archivos directamente desde el punto de distribución sin descargarlos primero en la caché. La opción **Ejecutar programa desde el punto de distribución** solo está disponible si los paquetes con referencia tienen la opción **Copiar el contenido de este paquete en un recurso compartido de paquete en los puntos de distribución** habilitada en la pestaña **Acceso a datos** de las propiedades del **Paquete**.  

 Si el cliente que ejecuta la secuencia de tareas no encuentra un paquete o una aplicación dependiente, dicho cliente envía de inmediato un error si la implementación está configurada como **Disponible**. Pero, si la implementación está configurada como **Requerido**, el cliente de Configuration Manager espera hasta la fecha límite para volver a intentar descargar el contenido, en el caso de que el contenido no estuviera replicado aún en un punto de distribución al que pueda acceder el cliente.  

 Cuando una secuencia de tareas se completa correctamente o produce error, Configuration Manager lo registra en el historial del cliente de Configuration Manager. No se puede cancelar o detener una secuencia de tareas una vez que se inicia en un equipo.  

> [!IMPORTANT]  
>  Si un paso de la secuencia de tareas requiere que se reinicie el equipo cliente, el cliente debe poder arrancar en una partición de disco con formato. De lo contrario, la secuencia de tareas produce un error independientemente del control de errores especificado en la secuencia de tareas.  

 Cuando un objeto dependiente de una secuencia de tareas, tal como un paquete de distribución de software, se actualiza a una versión más reciente, toda secuencia de tareas que haga referencia a ese paquete automáticamente se actualiza y hace referencia a la versión más nueva, independientemente de cuántas actualizaciones se hayan implementado.  

> [!NOTE]  
>  Antes de que un cliente de Configuration Manager ejecute una secuencia de tareas, el cliente comprueba todas las secuencias de tareas para ver si hay posibles dependencias y la disponibilidad de tales dependencias en un punto de distribución. Si el cliente encuentra un objeto eliminado del que depende la secuencia de tareas, el cliente genera un error y no ejecuta la secuencia de tareas.  

###  <a name="a-namebkmkrunprograma-run-a-program-before-the-task-sequence-is-run"></a><a name="BKMK_RunProgram"></a> Ejecución de un programa antes de ejecutar la secuencia de tareas  
 Puede seleccionar un programa para que se ejecute antes de que se ejecute la secuencia de tareas. Para especificar que un programa se ejecute primero, abra el cuadro de diálogo **Propiedades** para la secuencia de tareas y seleccione la pestaña **Avanzadas** para establecer las opciones siguientes:  

> [!IMPORTANT]  
>  Para ejecutar un programa antes de que se ejecute la secuencia de tareas, todo el contenido de la secuencia de tareas y el programa debe estar disponible en un recurso compartido de paquete para el paquete. El recurso compartido de paquete se configura en la pestaña **Acceso a datos** de las propiedades del paquete.  

-   **Ejecutar otro programa primero**: especifique que quiere que otro programa se ejecute antes de que se ejecute la secuencia de tareas.  

    > [!IMPORTANT]  
    >  Esta configuración solo se aplica a las secuencias de tareas que se ejecutan en el sistema operativo completo. Configuration Manager ignora esta configuración si la secuencia de tareas se inicia mediante PXE o medios de arranque.  

-   **Paquete**: especifique el paquete que contiene el programa.  

-   **Programa**: especifique el programa que debe ejecutarse.  

-   **Ejecutar siempre este programa primero**: especifique que quiere que Configuration Manager ejecute este programa cada vez que se ejecuta la secuencia de tareas en el mismo cliente. De forma predeterminada, una vez que un programa se ejecuta correctamente, el programa no se ejecuta otra vez si se vuelve a ejecutar la secuencia de tareas en el mismo cliente.  

 Si el programa seleccionado no se ejecuta en un cliente, la secuencia de tareas tampoco se ejecuta.  

##  <a name="a-namebkmktsmaintenancewindowa-use-a-maintenance-window-to-specify-when-a-task-sequence-can-run"></a><a name="BKMK_TSMaintenanceWindow"></a> Uso de una ventana de mantenimiento para especificar cuñando se puede ejecutar una tarea  
 Puede especificar en qué momento se puede ejecutar la secuencia de tareas mediante la definición de una ventana de mantenimiento para la recopilación que contiene los equipos de destino. Las ventanas de mantenimiento se configuran con fecha de inicio, hora de inicio y de finalización, y un patrón de periodicidad. Además, cuando establece la programación de la ventana de mantenimiento, puede especificar que la ventana de mantenimiento se aplique solo a las secuencias de tareas. Para obtener más información, consulte [How to Use Maintenance Windows in Configuration Manager](../../core/clients/manage/collections/use-maintenance-windows.md) (Uso de ventanas de mantenimiento en Configuration Manager).  

> [!IMPORTANT]  
>  Cuando se configura una ventana de mantenimiento para ejecutar una secuencia de tareas, una vez que se inicia la secuencia de tareas, continuará ejecutándose incluso si la ventana de mantenimiento se cierra. La secuencia de tareas llegará a finalizar correctamente o producirá un error.  

##  <a name="a-namebkmktsnetworkaccessaccounta-task-sequences-and-the-network-access-account"></a><a name="BKMK_TSNetworkAccessAccount"></a> Secuencias de tareas y la cuenta de acceso de red  
 Aunque las secuencias de tareas se ejecutan solo en el contexto de la cuenta de sistema local, es posible que deba configurar la cuenta de acceso de red en las siguientes circunstancias:  

-   Debe configurar la cuenta de acceso de red correctamente o la secuencia de tareas producirá un error si intenta tener acceso a paquetes de Configuration Manager en puntos de distribución para completar su tarea. Para obtener más información sobre la cuenta de acceso a la red, consulte [Cuenta de acceso de red](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#a-namebkmknaaa-network-access-account).  

    > [!NOTE]  
    >  La cuenta de acceso de red nunca se utiliza como contexto de seguridad para ejecutar programas, instalar aplicaciones, instalar actualizaciones o ejecutar secuencias de tareas. Sin embargo, la cuenta de acceso de red se emplea para el acceso a los recursos asociados en la red.  

-   Si usa una imagen de arranque para iniciar una implementación de sistema operativo, Configuration Manager usa el entorno de Windows PE, que no es un sistema operativo completo. El entorno de Windows PE utiliza un nombre aleatorio, generado automáticamente, que no pertenece a ningún dominio. Si no configura la cuenta de acceso de red correctamente, el equipo podría no tener los permisos necesarios para acceder a los paquetes de Configuration Manager para completar la secuencia de tareas.  

##  <a name="a-namebkmktscreatemediaa-create-media-for-task-sequences"></a><a name="BKMK_TSCreateMedia"></a> Creación de medios para secuencias de tareas  
 Puede escribir secuencias de tareas y sus archivos y dependencias relacionados para diferentes tipos de medios. Esto incluye escribir en medios extraíbles como un conjunto de DVD o CD, o usar una unidad flash USB para medios de arranque, independientes o de captura, o escribir en un archivo Windows Imaging Format (WIM) para medios preconfigurados.  

 Puede crear los siguientes tipos de medios:  

-   **Medio de captura**. Los medios de captura permiten capturar una imagen de sistema operativo configurada y creada fuera de la infraestructura de Configuration Manager. Los medios de captura pueden contener programas personalizados que se pueden ejecutar antes de que se ejecute una secuencia de tareas. El programa personalizado puede interactuar con el escritorio, solicitar al usuario valores de entrada o crear variables para que utilice la secuencia de tareas.  

     Para obtener más información, consulte [Crear medios de captura](../deploy-use/create-capture-media.md).  

-   **Medio independiente**. Los medios independientes contienen la secuencia de tareas y todos los objetos asociados necesarios para ejecutar la secuencia de tareas. Las secuencias de tareas de medios independientes pueden ejecutarse cuando Configuration Manager tiene conectividad limitada a la red, o cuando no tiene conectividad. Los medios independientes pueden ejecutarse de las siguientes maneras:  

    -   Si el equipo de destino no ha arrancado, se usa la imagen de Windows PE asociada a la secuencia de tareas desde el medio independiente, y se inicia la secuencia de tareas.  

    -   Los medios independientes pueden iniciarse manualmente si un usuario está conectado a la red e inicia la instalación.  

    > [!IMPORTANT]  
    >  Los pasos de una secuencia de tareas de medios independientes deben poder ejecutarse sin necesidad de recuperar datos de la red. De lo contrario, el paso de la secuencia de tareas que intente recuperar esos datos producirá un error. Por ejemplo, un paso de una secuencia de tareas que requiera que un punto de distribución obtenga un paquete generará un error. No obstante, si el paquete necesario se encuentra contenido en el mismo medio independiente, el paso de la secuencia de tareas se completará correctamente.  

     Para obtener más información, consulte [Crear medios independientes](../deploy-use/create-stand-alone-media.md).  

-   **Medios de arranque** Los medios de arranque contienen los archivos necesarios para iniciar un equipo de destino de manera tal que pueda conectarse a la infraestructura de Configuration Manager para determinar qué secuencias de tareas ejecutar según su pertenencia a una recopilación. La secuencia de tareas y los objetos dependientes no están contenidos en el medio, sino que se obtienen a través de la red desde el cliente de Configuration Manager. Este método resulta útil para equipos nuevos o implementaciones sin sistema operativo, o si el cliente de Configuration Manager o el sistema operativo no se encuentran en el equipo de destino.  

     Para obtener más información, consulte [Crear medios de arranque](../deploy-use/create-bootable-media.md).  

-   **Medios preconfigurados** Los medios preconfigurados implementan una imagen de sistema operativo en un equipo de destino no aprovisionado. Los medios preconfigurados se archivan como un archivo Windows Imaging Format (WIM) que puede ser instalado en un equipo sin sistema operativo por el fabricante o en un centro de configuración empresarial no relacionado con el entorno de Configuration Manager.  

     Para obtener más información, consulte [Crear medios preconfigurados](../deploy-use/create-prestaged-media.md).  

 Cuando cree un medio, especifique una contraseña para el medio a fin de controlar el acceso a los archivos contenidos en ese medio. Si se especifica una contraseña, debe haber un usuario presente para escribir la contraseña en el equipo de destino cuando se ejecuta la secuencia de tareas.  

 Si ejecuta una secuencia de tareas utilizando medios, la arquitectura de chip de equipo especificada en el medio no se reconocerá y la secuencia de tareas intentará ejecutarse incluso aunque la arquitectura especificada no coincida con lo que está instalado en el equipo de destino. Si la arquitectura de chip contenida en el medio no coincide con la arquitectura de chip instalada en el equipo de destino, se produce un error en la instalación.  

 Para obtener más información sobre cómo implementar sistemas operativos a través de medios, consulte [Crear medios de secuencia de tareas](../deploy-use/create-task-sequence-media.md).  



<!--HONumber=Nov16_HO1-->


