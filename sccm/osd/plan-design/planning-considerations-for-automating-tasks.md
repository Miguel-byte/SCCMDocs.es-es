---
title: Planeamiento de la automatización de tareas
titleSuffix: Configuration Manager
description: Realice un planeamiento previo a la creación de secuencias de tareas para automatizar tareas con Configuration Manager.
ms.date: 10/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 608b947e75ff29cf9653b2a12497918846556f4d
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411296"
---
# <a name="planning-considerations-for-automating-tasks-in-configuration-manager"></a>Consideraciones de planeamiento para la automatización de tareas en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

 Puede crear secuencias de tareas para automatizar tareas en su entorno de Configuration Manager. Estas tareas van desde la captura de un sistema operativo en un equipo de referencia hasta la implementación del sistema operativo en uno o varios equipos de destino. Las acciones de la secuencia de tareas se definen en los pasos individuales de la secuencia. Cuando se ejecuta la secuencia de tareas, esta ejecuta las acciones de cada paso a nivel de la línea de comandos en el contexto del sistema local. Este comportamiento significa que la secuencia de tareas se ejecuta completamente automatizada sin intervención del usuario. 



##  <a name="BKMK_TSStepsActions"></a> Acciones y etapas de una secuencia de tareas  

 Los pasos son los componentes básicos de una secuencia de tareas. Pueden incluir comandos tales como:  
   - Configurar y capturar el sistema operativo de un equipo de referencia  
   - Instalar Windows, los controladores de hardware, el cliente de Configuration Manager y el software en el equipo de destino   


 Las acciones del paso definen los comandos de un paso de secuencia de tareas. Existen dos tipos de acciones:  
   - Una acción definida mediante una cadena de línea de comandos se conoce como una *acción personalizada*.  
   - Una acción predefinida por Configuration Manager se conoce como una *acción integrada*.  


 Una secuencia de tareas puede realizar cualquier combinación de acciones personalizadas e integradas.  

 Los pasos de secuencia de tareas también pueden incluir condiciones que controlan cómo se comporta el paso. Estos comportamientos incluyen la detención de la secuencia de tareas o la continuación de la secuencia de tareas si se produce un error. Un tipo de condición es una variable de secuencia de tareas. Por ejemplo, utilice la variable **SMSTSLastActionRetCode** para probar la condición del paso anterior. Agregue condiciones a un solo paso o a un grupo de pasos.  

 La secuencia de tareas procesa los pasos secuencialmente. Esta secuencia incluye la acción del paso y las condiciones en el paso. Cuando Configuration Manager comienza a procesar un paso de la secuencia de tareas, el paso siguiente no se inicia hasta que haya finalizado la acción anterior. 

 Una secuencia de tareas se considera completa cuando: 
   - Todos sus pasos han finalizado  
   - Un paso con error hace que Configuration Manager detenga la ejecución de la secuencia de tareas antes de que se completen todos sus pasos.  


 Por ejemplo, si el paso de una secuencia de tareas no puede encontrar una imagen a la que se hace referencia o un paquete en un punto de distribución, la secuencia de tareas incluye una referencia errónea. Configuration Manager deja de ejecutar la secuencia de tareas en ese momento, a menos que el paso con errores tenga una condición para continuar cuando se produce un error.  

 > [!IMPORTANT]  
 >  De forma predeterminada, una secuencia de tareas produce un error después de que un paso o una acción produzcan un error. Si quiere que la secuencia de tareas continúe incluso cuando un paso produce error, edite la secuencia de tarea, haga clic en la pestaña **Opciones** y luego seleccione **Continuar después del error**.  

 Para obtener más información sobre los pasos que se pueden agregar a una secuencia de tareas, consulte [Pasos de la secuencia de tareas](/sccm/osd/understand/task-sequence-steps).  



##  <a name="BKMK_TSGroups"></a> Grupos de secuencias de tareas  

 Puede agrupar varios pasos dentro de una secuencia de tareas. Un grupo de secuencia de tareas consta de un nombre, una descripción opcional y cualquier condición opcional. La secuencia de tareas evalúa las condiciones del grupo como una unidad antes de continuar con el paso siguiente. Anide grupos entre sí, o incluya una combinación de pasos y subgrupos. Los grupos son útiles para la combinación de varios pasos que comparten una condición común.  

 Asigne un nombre a los grupos de la secuencia de tareas. No tiene que ser único. También puede proporcionar una descripción opcional para el grupo de secuencia de tareas.  

 > [!IMPORTANT]  
 >  De forma predeterminada, se produce un error de un grupo de secuencia de tareas cuando se produce un error en cualquier paso o grupo integrado dentro del grupo. Si quiere que la secuencia de tareas continúe cuando un paso o un grupo integrado produzca error, establezca la opción **Continuar después del error** en el paso o grupo.  

 La tabla siguiente muestra cómo funciona la opción **Continuar después de un error** cuando se agrupan pasos.  

 En este ejemplo, hay dos grupos de secuencias de tareas que incluyen tres pasos de secuencia de tareas cada uno.  

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

 -   Si se produce un error en el paso de la secuencia de tareas 2, la secuencia de tareas no ejecuta el paso de secuencia de tareas 3. Dado que el grupo de secuencia de tareas 1 está configurado para **Continuar después del error**, la secuencia de tareas continúa al grupo de secuencia de tareas 2. Ejecuta a continuación el paso de secuencia de tareas 4.  

 -   Si se produce un error en el paso de secuencia de tareas 4, no se ejecuta ningún paso más. La secuencia de tareas produce un error porque el ajuste **Continuar después del error** no está configurado para el grupo de secuencia de tareas 2.  



## <a name="add-child-task-sequences-to-a-task-sequence"></a>Adición de secuencias de tareas secundarias a una secuencia de tareas
 <!--1261338--> A partir de Configuration Manager versión 1710, puede agregar un nuevo paso de secuencia de tareas que ejecute otra secuencia de tareas. Este paso crea una relación primario-secundario entre las secuencias de tareas. El uso de este paso le permite crear más secuencias de tareas modulares que puede volver a usar.  

 Para obtener más información, vea [Ejecutar secuencia de tareas](/sccm/osd/understand/task-sequence-steps#child-task-sequence). 

 > [!Note]  
 > Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para más información, vea [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  



##  <a name="BKMK_TSVariables"></a> Variables de secuencias de tareas  

 Las variables de secuencia de tareas son un conjunto de pares de nombre y valor. Proporcionan configuración y ajustes de implementación del sistema operativo para las tareas de configuración del estado del usuario, el equipo y el sistema operativo en un cliente de Configuration Manager. Las variables de secuencia de tareas proporcionan un mecanismo para configurar y personalizar los pasos en una secuencia de tareas.  

 Cuando se ejecuta una secuencia de tareas, muchos de los valores de configuración de la secuencia de tareas se almacenan como variables de entorno. Puede acceder a los valores de las variables integradas de la secuencia de tareas o cambiarlos. También puede crear nuevas variables de secuencias de tareas para personalizar la forma en que se ejecuta una secuencia de tareas en un equipo de destino.  

 Use las variables de la secuencia de tareas para realizar las siguientes acciones:  

 -   Configurar las opciones de una acción de la secuencia de tareas  

 -   Proporcionar argumentos de la línea de comandos para un paso de la secuencia de tareas  

 -   Evaluar una condición que determina si se ejecuta un paso o un grupo de la secuencia de tareas  

 -   Proporcionar valores para scripts personalizados usados en una secuencia de tareas  


 Por ejemplo, tiener una secuencia de tareas que incluye un paso de secuencia de tareas **Unirse a dominio o grupo de trabajo**. Implemente la secuencia de tareas en diferentes recopilaciones, donde la pertenencia de la recopilación viene determinada por la pertenencia al dominio. Especifique una variable de secuencia de tareas por recopilación para cada nombre de dominio de recopilación. A continuación, use esa variable de secuencia de tareas para proporcionar el nombre de dominio adecuado en la secuencia de tareas.  

 Para obtener más información, consulte [How to use task sequence variables](/sccm/osd/understand/using-task-sequence-variables) (Uso de variables de secuencia de tareas).



##  <a name="BKMK_TSCreate"></a> Creación de una secuencia de tareas  

 Cree secuencias de tareas con el Asistente para crear secuencia de tareas. El asistente puede crear secuencias de tareas integradas que realizan tareas específicas o secuencias de tareas personalizadas que pueden realizar muchas tareas diferentes. Este asistente le permite crear los siguientes tipos de secuencias de tareas:

 - Instalación de una imagen de sistema operativo existente en un equipo de destino  

 - Generación y captura de una imagen de sistema operativo de un equipo de referencia  

 - Actualización a Windows 10 desde un paquete de actualización de sistema operativo en un equipo de destino   

 - Creación de una secuencia de tareas personalizada que realiza una tarea personalizada o una implementación de sistema operativo especializada  


 Para obtener más información, consulte [Crear secuencias de tareas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_CreateTaskSequence).  



##  <a name="BKMK_TSEdit"></a> Editar una secuencia de tareas  

 Edite la secuencia de tareas mediante el **Editor de secuencia de tareas**. El editor permite realizar los siguientes cambios en la secuencia de tareas:  

 - Agregar o quitar pasos de la secuencia de tareas  

 - Cambiar el orden de los pasos de la secuencia de tareas  

 - Agregar o quitar grupos de pasos  

 - Especificar si la secuencia de tareas continúa cuando se produce un error  

 - Agregar condiciones a los pasos y grupos de una secuencia de tareas  


 > [!IMPORTANT]  
 >  Si la secuencia de tareas tiene referencias sin asociar a un objeto como resultado de la edición, el editor requiere que corrija la referencia para cerrarse. Las posibles acciones incluyen:  
 > - Corregir la referencia  
 > - Eliminar el objeto sin referencia de la secuencia de tareas  
 > - Deshabilitar temporalmente el paso de la secuencia de tareas con errores hasta que se corrija o se quite la referencia errónea  


 Para obtener más información sobre cómo editar una secuencia de tareas, consulte [Editar una secuencia de tareas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ModifyTaskSequence).  



##  <a name="BKMK_TSDeploy"></a> Implementar una secuencia de tareas  

 Implemente una secuencia de tareas en equipos de destino que estén en cualquier recopilación de Configuration Manager. Use la recopilación **Todos los equipos desconocidos** integrada para implementar sistemas operativos en equipos desconocidos. No puede implementar una secuencia de tareas en recopilaciones de usuarios.  

 > [!IMPORTANT]  
 >  No implemente secuencias de tareas que instalen sistemas operativos en recopilaciones inapropiadas. Asegúrese de que la recopilación en la que implementa la secuencia de tareas incluye solo los equipos en los que desea instalar el sistema operativo. Para ayudar a evitar las implementaciones de sistema operativo no deseadas, configure las opciones para las implementaciones de alto riesgo. Para obtener más información, consulte [Settings to manage high-risk deployments](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments) (Configuración para administrar implementaciones de alto riesgo).  

 Cada equipo de destino que recibe la secuencia de tareas la ejecuta según la configuración especificada en la implementación. Las secuencias de tareas no contienen programas o archivos asociados. Todos los archivos a los que hace referencia una secuencia de tareas deben estar ya presentes en el equipo de destino o residir en un punto de distribución al que puedan acceder los clientes. 

 > [!NOTE]  
 > La secuencia de tareas instala los paquetes a los que hacen referencia los programas, aunque el programa o el paquete ya esté instalado en el equipo de destino. 
 > 
 > Si la secuencia de tareas instala una aplicación, la aplicación se instala solo si las reglas de requisitos de la misma se cumplen y si no está ya instalada, según el método de detección especificado para la aplicación.  

 El cliente de Configuration Manager ejecuta una implementación de secuencia de tareas cuando descarga la directiva de cliente. Para iniciar esta acción en lugar de esperar hasta el próximo ciclo de sondeo, consulte [Inicio de la recuperación de directivas para un cliente de Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

 Cuando se implementan secuencias de tareas en dispositivos de Windows Embedded con filtros de escritura habilitados, se puede especificar si se desea deshabilitar el filtro de escritura en el dispositivo durante la implementación y luego reiniciar el dispositivo después de esta operación. Si no se deshabilita el filtro de escritura, la secuencia de tareas se implementa en una superposición temporal y no estará disponible cuando se reinicie el dispositivo.  

 > [!NOTE]  
 >  Cuando implemente una secuencia de tareas en un dispositivo de Windows Embedded, asegúrese de que el dispositivo es miembro de una recopilación que tenga una ventana de mantenimiento configurada. Esto le permite administrar cuándo se deshabilita y habilita el filtro de escritura, y cuándo se reinicia el dispositivo.  
 >   
 >  Si los clientes descargan secuencias de tareas fuera de una ventana de mantenimiento, la secuencia de tareas se descarga dos veces. En este escenario, el cliente descarga la secuencia de tareas, deshabilita el filtro de escritura, reinicia el equipo y, a continuación, descarga la secuencia de tareas de nuevo. Este comportamiento se debe a que la secuencia de tareas se descargó originalmente en la superposición temporal, que se borra al reiniciarse el dispositivo.  

 Para obtener más información sobre cómo implementar secuencias de tareas, consulte [Implementar una secuencia de tareas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  



##  <a name="BKMK_TSExportImport"></a> Exportación e importación de una secuencia de tareas  

 Configuration Manager permite exportar e importar secuencias de tareas. Al exportar una secuencia de tareas, puede incluir los objetos a los que hace referencia la secuencia de tareas. 

 Para más información, consulte [Exportar e importar secuencias de tareas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ExportImport).  



##  <a name="BKMK_TSRun"></a> Ejecución de una secuencia de tareas  

 Las secuencias de tareas siempre se ejecutan mediante la cuenta de sistema local. Cuando se ejecuta la secuencia de tareas, el cliente de Configuration Manager comprueba en primer lugar si hay paquetes con referencia antes de iniciar los pasos de la secuencia de tareas. Si no puede validar ni descargar un paquete al que se hace referencia, la secuencia de tareas devuelve un error para el paso de la secuencia de tareas asociado.  

 > [!Note]  
 > El paso de la secuencia de tareas **Ejecutar línea de comandos** permite ejecutar la secuencia de tareas como una cuenta diferente.  

 Si configura una implementación de secuencia de tareas para que se descargue y ejecute, el cliente de Configuration Manager descarga todo el contenido dependiente en su memoria caché. Si el tamaño de caché del cliente es demasiado pequeño o no se encuentra el contenido, se produce un error en la secuencia de tareas. El cliente genera un mensaje de estado. 

 También puede especificar que el cliente descargue el contenido solo cuando sea necesario. Para ello, seleccione **Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas** en la implementación de la secuencia de tareas. Otra opción es **Ejecutar programa desde el punto de distribución**. Con esta opción, el cliente instala los archivos directamente desde el punto de distribución sin descargarlos primero en la memoria caché. 

 Al configurar la implementación de la secuencia de tareas como **Disponible**, si el cliente no puede encontrar contenido dependiente para la secuencia de tareas, envía de inmediato un error. En el caso de una implementación **obligatoria**, el cliente de Configuration Manager espera en esta situación. Vuelve a intentar la descarga del contenido hasta la fecha límite, en caso de que el contenido no se haya replicado aún en una ubicación de contenido a la que pueda acceder el cliente.  

 Cuando una secuencia de tareas se completa correctamente o produce error, Configuration Manager registra este estado en el historial del cliente. 

 Una vez que se inicia una secuencia de tareas en un equipo, no se puede cancelar ni detener.  

 > [!IMPORTANT]  
 >  Si un paso de la secuencia de tareas requiere que se reinicie el equipo, el cliente debe poder arrancar en una partición de disco con formato. De lo contrario, la secuencia de tareas produce un error independientemente del control de errores que especifique en la secuencia de tareas.  

 Cuando un objeto dependiente de una secuencia de tareas se actualiza a una versión más reciente, se actualiza automáticamente cualquier secuencia de tareas que haga referencia al paquete. Hace referencia a la versión más reciente, independientemente de cuántas actualizaciones haya implementado.  



##  <a name="BKMK_TSMaintenanceWindow"></a> Uso de una ventana de mantenimiento para especificar cuñando se puede ejecutar una tarea  

 Puede especificar en qué momento se puede ejecutar la secuencia de tareas mediante la definición de una ventana de mantenimiento para la recopilación de dispositivos. Configure ventanas de mantenimiento con una fecha de inicio, una hora de inicio y de finalización y un patrón de periodicidad. Cuando establece la programación de la ventana de mantenimiento, puede especificar que la ventana de mantenimiento se aplique solo a las secuencias de tareas. Para obtener más información, consulte [How to Use Maintenance Windows in Configuration Manager](/sccm/core/clients/manage/collections/use-maintenance-windows) (Uso de ventanas de mantenimiento en Configuration Manager).  

 > [!IMPORTANT]  
 >  Cuando se configura una ventana de mantenimiento para ejecutar una secuencia de tareas, una vez que se inicia la secuencia de tareas, continuará ejecutándose incluso si la ventana de mantenimiento se cierra.  



##  <a name="BKMK_TSNetworkAccessAccount"></a> Secuencias de tareas y la cuenta de acceso a la red  

> [!Important]  
> A partir de la versión 1806, en algunos escenarios de implementación de sistema operativo no es necesario usar la cuenta de acceso a la red. Para obtener más información, vea [HTTP mejorado](#enhanced-http).

Aunque las secuencias de tareas se ejecutan solo en el contexto de la cuenta de sistema local, es posible que deba configurar la [cuenta de acceso a la red](/sccm/core/plan-design/hierarchy/accounts#network-access-account) en las siguientes circunstancias:  

- Si la secuencia de tareas intenta tener acceso a contenido de Configuration Manager en los puntos de distribución. Configure correctamente la cuenta de acceso a la red o se producirá un error en la secuencia de tareas.   

- Al utilizar una imagen de arranque para iniciar una implementación de sistema operativo. En este caso, Configuration Manager usa el entorno Windows PE, que no es un sistema operativo completo. El entorno de Windows PE utiliza un nombre aleatorio, generado automáticamente, que no pertenece a ningún dominio. Si no configura correctamente la cuenta de acceso a la red, el equipo no puede acceder al contenido necesario para la secuencia de tareas.  

> [!NOTE]  
>  La cuenta del acceso a la red no se utiliza nunca como contexto de seguridad para ejecutar programas, instalar aplicaciones, instalar actualizaciones o ejecutar secuencias de tareas. La cuenta de acceso a la red solo se usa para tener acceso a los recursos asociados en la red.  

Para obtener más información sobre la cuenta de acceso a la red, consulte [Cuenta de acceso a la red](/sccm/core/plan-design/hierarchy/accounts#network-access-account).  


### <a name="enhanced-http"></a>HTTP mejorado
<!--1358278-->

A partir de la versión 1806, al habilitar **HTTP mejorado**, en los escenarios siguientes no se necesita una cuenta de acceso a la red para descargar contenido desde un punto de distribución:
  
- Secuencias de tareas que se ejecutan desde un entorno PXE o medios de arranque  
- Secuencias de tareas que se ejecutan desde el Centro de software  

Estas secuencias de tareas pueden ser para la implementación del sistema operativo o ser personalizadas. También se admite en los equipos de grupos de trabajo.
 
Para obtener más información, vea [HTTP mejorado](/sccm/core/plan-design/hierarchy/enhanced-http).  

> [!Note]  
> Los escenarios de implementación de sistema operativo siguientes aún requieren el uso de una cuenta de acceso a la red:
>  
> - La [opción de implementación](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS) de secuencia de tareas, **Acceder al contenido directamente desde un punto de distribución cuando sea necesario mediante la ejecución de la secuencia de tareas**   
> - La opción de paso [Solicitar almacén de estado](/sccm/osd/understand/task-sequence-steps#BKMK_RequestStateStore), **Use la cuenta de acceso a la red si la cuenta de equipo no puede conectarse a un almacén de estado** 
> - Al conectarse a un dominio de confianza o a través de bosques de Active Directory 
> - La opción de paso [Aplicar imagen de sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyOperatingSystemImage), **Acceder al contenido directamente desde el punto de distribución** 
> - La[configuración avanzada](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#bkmk_prop-advanced) de secuencia de tareas para **Ejecutar otro programa primero** 
> - [Multidifusión](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network)  



##  <a name="BKMK_TSCreateMedia"></a> Creación de medios para secuencias de tareas  

 Puede escribir secuencias de tareas y sus archivos y dependencias relacionados para diferentes tipos de medios. Configuration Manager admite medios extraíbles, como un DVD o una unidad flash USB para medios de arranque, independientes o de captura. Los medios preconfigurados utilizan un archivo de imagen (WIM) de Windows.  

 Al crear medios, especifique una contraseña para controlar el acceso. Así, una persona debe escribir la contraseña en el equipo de destino para ejecutar la secuencia de tareas.  

 Al ejecutar una secuencia de tareas desde un medio, no se reconoce la arquitectura del procesador especificado del medio. Si la arquitectura especificada no coincide con el equipo de destino, la secuencia de tareas sigue intentando ejecutarse. Si la arquitectura del medio no coincide con la arquitectura del equipo de destino, se produce un error en la secuencia de tareas.  

 Para obtener más información, consulte [Crear medios de secuencia de tareas ](/sccm/osd/deploy-use/create-task-sequence-media).  


### <a name="media-types"></a>Tipos de medios
 Configuration Manager admite los siguientes tipos de medios:  

#### <a name="capture-media"></a>Medios de captura
 Los medios de captura permiten capturar una imagen de sistema operativo configurada y creada fuera de la infraestructura de Configuration Manager. Los medios de captura pueden contener programas personalizados que se pueden ejecutar antes de que se ejecute una secuencia de tareas. El programa personalizado puede interactuar con el escritorio, solicitar al usuario valores de entrada o crear variables para que utilice la secuencia de tareas.  

 Para obtener más información, consulte [Create capture media](/sccm/osd/deploy-use/create-capture-media) (Crear medios de captura).  

#### <a name="stand-alone-media"></a>Medios independientes
 Los medios independientes contienen la secuencia de tareas y todos los objetos asociados necesarios para ejecutar la secuencia de tareas. Las secuencias de tareas de medios independientes pueden ejecutarse cuando Configuration Manager tiene conectividad limitada a la red, o cuando no tiene conectividad. Ejecute los medios independientes de las siguientes maneras:  

 - Si el equipo de destino no ha arrancado, se usa la imagen de Windows PE asociada a la secuencia de tareas desde el medio independiente, y se inicia la secuencia de tareas.  

 - Inicio manual de los medios independientes. Si un usuario ha iniciado sesión en el equipo, puede iniciar la secuencia de tareas desde el medio.  


 > [!IMPORTANT]  
 >  Los pasos de una secuencia de tareas de medios independientes deben ser capaces de ejecutarse sin tener que recuperar todos los datos de la red. En caso contrario, se produce un error en el paso de la secuencia de tareas que intenta recuperar los datos. Por ejemplo, se produce un error en un paso de la secuencia de tareas que requiere un punto de distribución para obtener un paquete. Si los medios independientes contienen el paquete necesario, el paso de la secuencia de tareas se ejecuta correctamente.  


 Para obtener más información, consulte [Crear medios independientes](/sccm/osd/deploy-use/create-stand-alone-media).  

#### <a name="bootable-media"></a>Medio de arranque
 Los medios de arranque contienen los archivos necesarios para iniciar un equipo de destino de manera tal que pueda conectarse a la infraestructura de Configuration Manager. A continuación, determina qué secuencias de tareas se ejecutan según sus pertenencias a recopilaciones. Estos medios no incluyen la secuencia de tareas ni los objetos dependientes. En su lugar, el cliente descarga el contenido a través de la red. Este método resulta útil para equipos nuevos o implementaciones sin sistema operativo, cuando no hay ningún sistema operativo en el equipo de destino.  

 Para obtener más información, consulte [Crear medios de arranque](/sccm/osd/deploy-use/create-bootable-media).  

#### <a name="prestaged-media"></a>Medio preconfigurado
 Los medios preconfigurados implementan una imagen de sistema operativo en un equipo de destino no aprovisionado. Los medios preconfigurados se almacenan como un archivo de imagen (WIM) de Windows. Este archivo puede instalarse en un equipo sin sistema operativo por el fabricante o en un centro de configuración empresarial. Una ventaja de los medios preconfigurados es que estas ubicaciones no requieren una conexión a su entorno de Configuration Manager.  

 Para obtener más información, consulte [Crear medios preconfigurados](/sccm/osd/deploy-use/create-prestaged-media).  
