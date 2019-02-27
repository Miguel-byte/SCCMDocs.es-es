---
title: Uso de variables en una secuencia de tareas
titleSuffix: Configuration Manager
description: Obtenga información sobre el uso de variables en una secuencia de tareas de Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3e8ebea21b735e6b93d73bf6ff5eb842243ef42d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121869"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Uso de variables en una secuencia de tareas en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

 El motor de secuencia de tareas en la característica de implementación de sistema operativo de Configuration Manager usa muchas variables para controlar sus comportamientos. Use estas variables para: 
 - Establecer las condiciones en los pasos  
 - Cambiar los comportamientos de determinados pasos  
 - Usar en scripts para acciones más complejas  


 Para consultar una referencia de todas las variables de secuencia de tareas disponibles, conste [Variables de secuencia de tareas](/sccm/osd/understand/task-sequence-variables).



## <a name="bkmk_types"></a> Tipos de variables

 Hay varios tipos de variables:  
 - [Integrada](#bkmk_built-in)  
 - [Acción](#bkmk_action)  
 - [Personalizado](#bkmk_custom)  
 - [Solo lectura](#bkmk_read-only)  
 - [Matriz](#bkmk_array)  


### <a name="bkmk_built-in"></a> Variables integradas

 Las variables integradas proporcionan información sobre el entorno donde se ejecuta la secuencia de tareas. Sus valores están disponibles a lo largo de toda la secuencia de tareas. Por lo general, el motor de secuencia de tareas inicializa las variables integradas antes de ejecutar los pasos. 

 Por ejemplo, **\_SMSTSLogPath** es una variable de entorno que especifica la ruta de acceso en la que los componentes de Configuration Manager escriben archivos de registro. Cualquier paso de secuencia de tareas puede tener acceso a esta variable de entorno. 

 La secuencia de tareas evalúa algunas de las variables antes de cada paso. Por ejemplo, **\_SMSTSCurrentActionName** muestra el nombre del paso actual. 

### <a name="bkmk_action"></a> Variables de acción

 Las variables de acción de secuencia de tareas especifican los valores de configuración que utiliza un único paso de una secuencia de tareas. De forma predeterminada, el paso inicializa su configuración antes de ejecutarse. Esta configuración solo está disponible mientras se está ejecutando el paso asociado de la secuencia de tareas. La secuencia de tareas agrega el valor de la variable de acción al entorno antes de ejecutar el paso. Luego, quita el valor del entorno después de que se ejecuta el paso.

 Por ejemplo, agrega el paso **Ejecutar línea de comandos** a una secuencia de tareas. Este paso incluye un propiedad **Iniciar en**. La secuencia de tareas almacena un valor predeterminado para esta propiedad como variable **WorkingDirectory**. La secuencia de tareas inicializa este valor antes de ejecutar el paso **Ejecutar línea de comandos**. Mientras se ejecuta este paso, acceda al valor de propiedad **Iniciar en** desde el valor **WorkingDirectory**. Una vez completado el paso (etapa), la secuencia de tareas quita el valor de la variable **WorkingDirectory** del entorno. Si la secuencia de tareas incluye otro paso **Ejecutar línea de comandos**, inicializa una nueva variable **WorkingDirectory**. En ese momento, la secuencia de tareas establece la variable como el valor inicial para el paso actual. Para obtener más información, consulte [WorkingDirectory](using-task-sequence-variables.md#WorkingDirectory).  

 El valor *predeterminado* de una variable de acción está presente cuando se ejecuta el paso. Si establece un *nuevo* valor, estará disponible para varios pasos de la secuencia de tareas. Si reemplaza un valor predeterminado, el nuevo valor permanece en el entorno. Este nuevo valor reemplaza al valor predeterminado para otros pasos en la secuencia de tareas. Por ejemplo, agregue un paso **Configurar variable de secuencia de tareas** como primer paso de la secuencia de tareas. Este paso establece la variable **WorkingDirectory** en `C:\`. Cualquier paso de **Ejecutar línea de comandos** de la secuencia de tareas usa el nuevo valor de directorio inicial.  

 Algunos pasos de secuencia de tareas marcan determinadas variables de acción como *salida*. Las pasos que tienen lugar posteriormente en la secuencia de tareas leen estas variables de salida.

 > [!Note]  
 > No todos los pasos de secuencia de tareas tienen variables de acción. Por ejemplo, aunque hay variables asociadas a la acción **Habilitar BitLocker**, no hay ninguna variable asociada a la acción **Deshabilitar BitLocker**.  


### <a name="bkmk_custom"></a> Variables personalizadas

 Estas variables son aquellas que Configuration Manager no crea. Inicialice sus propias variables para usarlas como condiciones, en líneas de comandos o en scripts. 

 Cuando especifique un nombre para una nueva variable de secuencia de tareas, siga estas instrucciones:  

 - El nombre de la variable de secuencia de tareas puede incluir letras, números, el carácter de subrayado (`_`) y un guión (`-`).  

 - El nombre de la variable de secuencia de tareas tiene una longitud mínima de 1 carácter y una longitud máxima de 256 caracteres.  

 - Las variables definidas por el usuario deben comenzar con una letra (`A-Z` o `a-z`).  

 - Los nombres de las variables definidas por el usuario no pueden comenzar con el carácter de subrayado. Únicamente las variables de secuencia de tareas de solo lectura van precedidas por el carácter de subrayado.  

 - Los nombres de variables de secuencia de tareas no distinguen mayúsculas de minúsculas. Por ejemplo, `OSDVAR` y `osdvar` son la misma variable de secuencia de tareas.  

 - Los nombres de variables de secuencia de tareas no pueden comenzar ni terminar con un espacio. Tampoco pueden contener espacios incrustados. La secuencia de tareas ignora los espacios que quedan al principio o al final de un nombre de variable.  


 No hay ningún límite establecido respecto al número de variables de secuencias de tareas que puede crear. Sin embargo, el número de variables está limitado por el tamaño del entorno de secuencia de tareas. El límite de tamaño total para el entorno de secuencia de tareas es de 32 MB.  


### <a name="bkmk_read-only"></a> Variables de solo lectura

 No se puede cambiar el valor de algunas variables, que son de solo lectura. Normalmente, el nombre comienza con un carácter de subrayado (\_). La secuencia de tareas las usa para sus operaciones. Las variables de solo lectura están visibles en el entorno de secuencia de tareas. 

 Estas variables son útiles en los scripts o líneas de comandos. Por ejemplo, la ejecución de una línea de comandos y la canalización de la salida a un registro de archivo en **\_SMSTSLogPath** con los demás archivos de registro.

 > [!NOTE]  
 >  Los pasos de secuencia de tareas pueden leer las variables de secuencia de tareas de solo lectura en una secuencia de tareas, pero no pueden configurarse. Por ejemplo, utilice una variable de solo lectura como parte de la línea de comandos para un paso **Ejecutar línea de comandos**. No puede establecer una variable de solo lectura mediante el paso **Configurar variable de secuencia de tareas**.  



### <a name="bkmk_array"></a> Variables de matriz

 La secuencia de tareas almacena algunas de las variables como una matriz. Cada uno de los elementos de la matriz representa la configuración de un único objeto. Use estas variables cuando un dispositivo tenga más de un objeto que configurar. Los siguientes pasos de secuencia de tareas utilizan variables de matriz:

 - [Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

 - [Formatear y crear particiones en el disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  



## <a name="bkmk_set"></a> Configuración de las variables

 En el caso de las variables personalizadas o las variables que no son de solo lectura, existen varios métodos para inicializar y establecer el valor de la variable:  

 - [Establecer variable de secuencia de tareas](#bkmk_set-ts-step)  
 - [Establecer variables dinámicas](#bkmk_set-dyn-step)  
 - [Variables de recopilación y dispositivo](#bkmk_set-coll-var)  
 - [Objeto COM TSEnvironment](#bkmk_set-com)  
 - [Comando de preinicio](#bkmk_set-prestart)  
 - [Asistente para crear medio de secuencia de tareas](#bkmk_set-media)  


 Elimine una variable del entorno con alguno de los métodos que sirven para crear una variable. Para eliminar una variable, establezca el valor de la variable en una cadena vacía.  

 Puede combinar métodos para establecer una variable de secuencia de tareas en valores diferentes para la misma secuencia. Por ejemplo, establezca los valores predeterminados mediante el editor de secuencia de tareas y, a continuación, establezca valores personalizados mediante un script. 

 Si establece la misma variable por medio de distintos métodos, el motor de secuencia de tareas utiliza el siguiente orden:  

 1. Primero se evalúan las variables de la recopilación.  

 2. Las variables específicas de dispositivo invalidan la misma variable establecida en una recopilación.  

 3. Las variables establecidas por cualquier método durante la secuencia de tareas tienen prioridad sobre las variables de la recopilación o el dispositivo.  


#### <a name="general-limitations-for-task-sequence-variable-values"></a>Limitaciones generales para los valores de las variables de secuencia de tareas  

 - Los valores de las variables de secuencia de tareas no pueden superar los 4000 caracteres.  

 - No se puede cambiar una variable de secuencia de tareas de solo lectura. Las variables de solo lectura tienen nombres que empiezan por un carácter de subrayado (`_`).  

 - Los valores de variables de secuencias de tareas pueden distinguir entre mayúsculas y minúsculas dependiendo del uso del valor. En la mayoría de los casos, los valores de variables de secuencias de tareas no distinguen entre mayúsculas y minúsculas. Una variable que incluye una contraseña distingue mayúsculas de minúsculas.  


### <a name="bkmk_set-ts-step"></a> Establecer variable de secuencia de tareas

 Utilice este paso en la secuencia de tareas para establecer una única variable en un solo valor. 

 Para más información, vea [Configurar variable de secuencia de tareas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable). 


### <a name="bkmk_set-dyn-step"></a> Establecer variables dinámicas

 Utilice este paso en la secuencia de tareas para establecer una o varias variables de secuencia de tareas. Defina reglas en este paso para determinar las variables y los valores que se usarán. 

 Para obtener más información, consulte [Establecer variables dinámicas](/sccm/osd/understand/task-sequence-steps#BKMK_SetDynamicVariables).


### <a name="bkmk_set-coll-var"></a> Variables de recopilación y dispositivo

 Establezca las variables en las propiedades de una recopilación o un dispositivo específico. 

 Para más información, consulte [Crear variables de secuencia de tareas para equipos y recopilaciones](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_CreateTSVariables).


### <a name="bkmk_set-com"></a> Objeto COM TSEnvironment

 Para trabajar con variables de un script, use el objeto **TSEnvironment**. 

 Para obtener más información, consulte [How to use variables in a running task sequence](/sccm/develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence) (Uso de variables en una secuencia de tareas en ejecución) en el SDK de Configuration Manager.


### <a name="bkmk_set-prestart"></a> Comando de preinicio

 El comando de preinicio es un script o un archivo ejecutable que se ejecuta en Windows PE antes de que el usuario seleccione la secuencia de tareas. El comando de preinicio puede consultar una variable o pedir información al usuario y, luego, guardarla en el entorno. Use el objeto COM [TSEnvironment](#bkmk_set-com) para leer y escribir variables desde el comando de preinicio. 

 Para obtener más información, consulte [Prestart commands for task sequence media](/sccm/osd/understand/prestart-commands-for-task-sequence-media) (Comandos de preinicio para medios de secuencia de tareas).


### <a name="bkmk_set-media"></a> Asistente para crear medio de secuencia de tareas

 Especifique las variables de secuencias de tareas que se ejecutan desde un medio. Cuando se utiliza un medio para implementar el sistema operativo, se agregan las variables de secuencia de tareas y se especifican sus valores al crear el medio. Las variables y sus valores se almacenan en el medio.  

 > [!NOTE]  
 >  Las secuencias de tareas se almacenan en medios independientes. Sin embargo, todos los demás tipos de medios, como los medios preconfigurados, recuperan la secuencia de tareas desde un punto de administración.  

 Al ejecutar una secuencia de tareas desde un medio, puede agregar una variable a la página **Personalización** del asistente. 

 Use las variables de los medios en lugar de las variables por recopilación o por equipo. Si se está ejecutando la secuencia de tareas desde un medio, las variables por equipo y por recopilación no se aplican y no se utilizan.  

 > [!TIP]  
 >  La secuencia de tareas escribe el identificador de paquete y la línea de comandos de preinicio en el archivo **CreateTSMedia.log** en el equipo que ejecuta la consola de Configuration Manager. Este archivo de registro incluye el valor de las variables de secuencia de tareas. Revise este archivo de registro para comprobar el valor de las variables de secuencia de tareas.  

 Para obtener más información, consulte [Crear medios de secuencia de tareas ](/sccm/osd/deploy-use/create-task-sequence-media).



## <a name="bkmk_access"></a> Acceso a variables

 Después de especificar la variable y su valor mediante uno de los métodos indicados en la sección anterior, utilícela en sus secuencias de tareas. Por ejemplo, acceda a los valores predeterminados para las variables de secuencia de tareas integradas o condicione un paso al valor de una variable.  

 Use los siguientes métodos para tener acceso a los valores de las variables en el entorno de la secuencia de tareas:
 - [Usar en un paso](#bkmk_access-step)  
 - [Condición de paso](#bkmk_access-condition)  
 - [Script personalizado](#bkmk_access-script)  
 - [Archivo de respuesta de configuración de Windows](#bkmk_access-answer)  
  

### <a name="bkmk_access-step"></a> Usar en un paso

 Especifique un valor de variable para un ajuste de un paso de secuencia de tareas. En el editor de secuencia de tareas, modifique el paso y especifique el nombre de variable como el valor del campo. Rodee el nombre de la variable de signos de porcentaje (`%`). 

 Por ejemplo, utilice el nombre de la variable como parte del campo **Línea de comandos** del paso **Ejecutar línea de comandos**. La siguiente línea de comandos escribe el nombre del equipo en un archivo de texto. 

 `cmd.exe /c %_SMSTSMachineName% > C:\File.txt`


### <a name="bkmk_access-condition"></a> Condición de paso

 Use variables de secuencia de tareas integradas o personalizadas como parte de una condición en un paso o grupo. La secuencia de tareas evalúa el valor de la variable antes de ejecutar el paso o grupo.

 Para agregar una condición que evalúa un valor de variable, haga lo siguiente:  

 1. En el editor de secuencia de tareas, seleccione el paso o grupo al que desea agregar la condición.  

 2. Cambie a la pestaña **Opciones** para el paso o grupo. Haga clic en **Agregar condición** y seleccione **Variable de secuencia de tareas**.  

 3. En el cuadro de diálogo **Variable de secuencia de tareas**, especifique la siguiente configuración:  

    - **Variable**: nombre de la variable. Por ejemplo, `_SMSTSInWinPE`.  

    - **Condición**: condición para evaluar el valor variable. Por ejemplo, **igual a**.  

    - **Valor**: valor de la variable que se va a comprobar. Por ejemplo, `false`.  


 Los tres ejemplos anteriores conforman en conjunto una condición para comprobar si la secuencia de tareas se está ejecutando desde una imagen de arranque de Windows PE: 

 > **Variable de secuencia de tareas** `_SMSTSInWinPE equals "false"`

 Consulte esta condición en el grupo **Capturar archivos y configuraciones** de la plantilla de secuencia de tareas predeterminada para instalar una imagen de sistema operativo existente.


### <a name="bkmk_access-script"></a> Script personalizado

 Lea y escriba variables mediante el objeto COM de **Microsoft.SMS.TSEnvironment** mientras la secuencia de tareas está en ejecución.

 El ejemplo siguiente de Windows PowerShell consulta la variable **_SMSTSLogPath** para obtener la ubicación del registro actual. El script también establece una variable personalizada.

 ```PowerShell
 # Create an object to access the task sequence environment
 $tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment
 
 # Query the environment to get an existing variable
 # Set a variable for the task sequence log path
 $LogPath = $tsenv.Value("_SMSTSLogPath")

 # Or, convert all of the variables currently in the environment to PowerShell variables
 $tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

 # Write a message to a log file
 Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append
 
 # Set a custom variable "startTime" to the current time
 $tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
 ```


###  <a name="bkmk_access-answer"></a> Archivo de respuesta de configuración de Windows

El archivo de respuesta de configuración de Windows que suministre puede tener insertadas variables de secuencia de tareas. Utilice el formulario `%varname%`, donde *varname* es el nombre de la variable. El paso **Instalar Windows y Configuration Manager** sustituye la cadena del nombre de la variable por el valor real de la variable. Estas variables de secuencia de tareas insertadas no se pueden usar en campos solo numéricos de un archivo de respuesta unattend.xml.

Para obtener más información, consulte [Instalar Windows y Configuration Manager](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).



## <a name="see-also"></a>Consulte también

- [Pasos de la secuencia de tareas](/sccm/osd/understand/task-sequence-steps)
- [Variables de secuencias de tareas](/sccm/osd/understand/task-sequence-variables)
- [Planificación de consideraciones para la automatización de tareas](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)
