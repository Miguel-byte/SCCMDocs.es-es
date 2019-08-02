---
title: Administrar secuencias de tareas
titleSuffix: Configuration Manager
description: Cree, edite, implemente, importe y exporte secuencias de tareas para administrarlas y automatizar las tareas en su entorno.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 041654b3ba1a25c832232fb26fa09f7ea12e8f97
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537065"
---
# <a name="manage-task-sequences-to-automate-tasks"></a>Administrar secuencias de tareas para automatizar tareas

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use secuencias de tareas para automatizar los pasos en su entorno de Configuration Manager. Estos pasos pueden implementar una imagen de sistema operativo en un equipo de destino, compilar y capturar una imagen de sistema operativo a partir de un conjunto de archivos de instalación de sistema operativo, y capturar y restaurar la información de estado de usuario. Las secuencias de tareas se encuentran en la consola de Configuration Manager. En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**. El nodo **Secuencia de tareas**, incluidas todas las subcarpetas creadas, se replica en toda la jerarquía de Configuration Manager. Para obtener información, consulte [Planning considerations for automating tasks](/sccm/osd/plan-design/planning-considerations-for-automating-tasks) (Consideraciones de planeación para la automatización de tareas).  



## <a name="BKMK_CreateTaskSequence"></a> Crear secuencias de tareas  

Cree secuencias de tareas con el Asistente para crear secuencia de tareas. Este asistente puede crear los siguientes tipos de secuencias de tareas:  

|Tipo de secuencia de tareas|Más información|  
|------------------------|----------------------|  
|[Secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md)|Este tipo de secuencia de tareas crea los pasos para instalar un sistema operativo. También incluye opciones para migrar datos de usuario, incluir actualizaciones de software e instalar aplicaciones.|  
|[Secuencia de tareas para actualizar un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md)|Este tipo de secuencia de tareas crea los pasos para actualizar un sistema operativo. También incluye opciones para incluir actualizaciones de software e instalar aplicaciones.|  
|[Secuencia de tareas para capturar un sistema operativo](create-a-task-sequence-to-capture-an-operating-system.md)|Este tipo de secuencia de tareas crea los pasos para compilar y capturar un sistema operativo desde un equipo de referencia. Puede incluir actualizaciones de software e instalar aplicaciones en el equipo de referencia antes de capturar la imagen.|  
|[Secuencia de tareas para capturar y restaurar el estado de usuario](create-a-task-sequence-to-capture-and-restore-user-state.md)|En esta secuencia de tareas se indican las etapas que se deben agregar a una secuencia de tareas existente para capturar y restaurar los datos de estado de usuario.|  
|[Secuencia de tareas personalizada](create-a-custom-task-sequence.md)|Este tipo de secuencia de tareas no agrega ninguna etapa a la secuencia de tareas. Después de crear esta secuencia de tareas, modifíquela y agregue pasos.|  



## <a name="BKMK_ModifyTaskSequence"></a> Editar  

Modifique una secuencia de tareas, agregue o quite pasos, agregue o quite grupos, o cambie el orden de los pasos. Use el procedimiento siguiente para modificar una secuencia de tareas existente:  

> [!IMPORTANT]  
> Cuando edite una secuencia de tareas creada mediante el Asistente para crear secuencia de tareas, el nombre del paso puede ser la acción o el tipo de paso. Por ejemplo, puede ver un paso con el nombre "Disco de partición 0", que es la acción de un paso de tipo [Formatear y crear particiones en el disco](/sccm/osd/understand/task-sequence-steps#BKMK_FormatandPartitionDisk). Todos los pasos de la secuencia de tareas se documentan por su tipo, no necesariamente por el nombre del paso que se muestra en el editor.  

### <a name="process-to-edit-a-task-sequence"></a>Proceso para editar una secuencia de tareas  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y, luego, seleccione el nodo **Secuencias de tareas**.  

2. En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que desee editar.  

3. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Secuencia de tareas** y seleccione **Editar**. A continuación, realice cualquiera de las siguientes operaciones:  

    - Para agregar un paso de secuencia de tareas, haga clic en **Agregar**, seleccione el tipo de paso y seleccione el paso que quiere agregar. Por ejemplo, para agregar el paso [Ejecutar línea de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine), seleccione **Agregar**, elija **General** y, luego, **Ejecutar línea de comandos**.  

    - Para agregar un grupo a la secuencia de tareas, seleccione en **Agregar** y, luego, haga clic en **Nuevo grupo**. Después de agregar un grupo, puede agregar pasos al grupo.  

    - Para cambiar el orden de los pasos y los grupos de la secuencia de tareas, seleccione el paso o grupo que quiera reordenar y use los iconos **Subir elemento** o **Bajar elemento**. Solo puede mover un paso o un grupo cada vez.  

    - Para quitar un paso o un grupo, seleccione el paso o el grupo y elija **Quitar**.  

4. Para guardar los cambios y cerrar la ventana, seleccione **Aceptar**. Para guardar los cambios y mantener abierto el editor de secuencia de tareas, seleccione **Aplicar**.  

Para obtener una lista de las etapas de secuencia de tareas disponibles, consulte [Pasos de la secuencia de tareas](/sccm/osd/understand/task-sequence-steps).  

### <a name="bkmk_sedo"></a> Reclamación de bloqueo para editar secuencias de tareas

<!--3699337-->
Si la consola de Configuration Manager deja de responder, podría quedarse bloqueado y no poder realizar más cambios hasta que expire el bloqueo al cabo de 30 minutos. Este bloqueo forma parte del sistema SEDO (edición serializada de objetos distribuidos) de Configuration Manager. Para obtener más información, vea [Configuration Manager SEDO](/sccm/develop/core/understand/sedo) (SEDO de Configuration Manager).

A partir de la versión 1906, puede borrar el bloqueo en una secuencia de tareas. Esta acción solo se aplica a la cuenta de usuario que tiene el bloqueo, en el mismo dispositivo desde el que el sitio concedió el bloqueo. Cuando intente obtener acceso a una secuencia de tareas bloqueada, ahora podrá **descartar los cambios** y seguir editando el objeto. Estos cambios se perderían de todos modos al expirar el bloqueo.


## <a name="bkmk_prop-general"></a> Configuración de las propiedades del Centro de software

Siga este procedimiento para configurar los detalles de la secuencia de tareas que aparece en el Centro de software. Estos detalles son meramente informativos.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. Seleccione la secuencia de tareas que se va editar y seleccione **Propiedades**.  

3. En la pestaña **General**, está disponible la siguiente configuración para el Centro de software:  

    - **Es necesario reiniciar**: permite al usuario saber si es necesario reiniciar durante la instalación.  

    - **Tamaño de descarga (MB)** : especifica cuántos megabytes se muestran en el Centro de software para la secuencia de tareas.  

    - **Tiempo de ejecución estimado (minutos)** : especifica el tiempo de ejecución estimado en minutos que se muestra en el Centro de software para la secuencia de tareas.  



## <a name="bkmk_prop-advanced"></a> Configuración de los ajustes de la secuencia de tareas avanzada

Use el procedimiento siguiente para configurar el comportamiento de la secuencia de tareas en el cliente de Configuration Manager.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. Seleccione la secuencia de tareas que se va editar y seleccione **Propiedades**.  

3. En la pestaña **Avanzadas** están disponibles las opciones siguientes:  

    - **Ejecutar otro programa primero**: active esta casilla para ejecutar un programa en otro paquete antes de ejecutar la secuencia de tareas. De forma predeterminada, esta casilla de verificación está desactivada. No es necesario implementar por separado el programa especificado para que se ejecute primero.  

        > [!IMPORTANT]
        > Esta configuración solo se aplica a las secuencias de tareas que se ejecutan en el sistema operativo completo. Si inicia la secuencia de tareas mediante PXE o medios de arranque, Configuration Manager ignora este ajuste.  

        - **Paquete**: busque el paquete que contiene el programa para ejecutar antes de esta secuencia de tareas.  

        - **Programa**: seleccione el programa para ejecutar antes de esta secuencia de tareas.  

        > [!NOTE]  
        > Si el programa seleccionado no se ejecuta en un cliente, la secuencia de tareas tampoco se ejecuta. Si el programa seleccionado se ejecuta correctamente, no se ejecutará de nuevo, incluso aunque la secuencia de tareas se vuelva a ejecutar en el mismo cliente.  

    - **Suprimir notificaciones de secuencia de tareas**: seleccione esta opción para ocultar la notificación del sistema **Hay nuevo software disponible**. En el área de notificaciones se seguirá mostrando el icono **Nuevo software** del Centro de software. Esta opción está deshabilitada de forma predeterminada.  

    - **Deshabilitar esta secuencia de tareas en los equipos en los que se implementó**: si selecciona esta opción, Configuration Manager deshabilita temporalmente todas las implementaciones que contienen esta secuencia de tareas. También quita la secuencia de tareas de la lista de implementaciones disponibles para su ejecución. La secuencia de tareas no se ejecuta hasta que la habilite. Esta opción está deshabilitada de forma predeterminada.  

    - **Tiempo de ejecución máximo permitido**: especifica el tiempo máximo (en minutos) previsto para la ejecución de la secuencia de tareas en el equipo de destino. Use un número entero igual o mayor que cero. De forma predeterminada, este valor es de 120 minutos.  

        > [!IMPORTANT]  
        > Si está usando ventanas de mantenimiento para la recopilación en las que implementa esta secuencia de tareas, puede producirse un conflicto si el **Tiempo de ejecución máximo permitido** es mayor que la ventana de mantenimiento programada. Si el tiempo de ejecución máximo se establece en **0**, la secuencia de tareas se inicia durante la ventana de mantenimiento. Sigue ejecutándose hasta que se complete o se produzca un error después de cerrar la ventana de mantenimiento. Como resultado, las secuencias de tareas con un tiempo de ejecución máximo establecido en **0** podrían ejecutarse después del final de sus ventanas de mantenimiento. Si establece el tiempo de ejecución máximo en un periodo específico (diferente de 0) que supera la duración de cualquiera de las ventanas de mantenimiento disponibles, la secuencia de tareas no se ejecutará. Para obtener más información, consulte [How to Use Maintenance Windows in Configuration Manager](/sccm/core/clients/manage/collections/use-maintenance-windows) (Uso de ventanas de mantenimiento en Configuration Manager).  

        Si el valor se establece en **0**, Configuration Manager evalúa el tiempo de ejecución máximo permitido en **12** horas (720 minutos) para el progreso de la supervisión. Aun así, la secuencia de tareas se iniciará siempre y cuando la duración de la cuenta atrás no supere el valor de la ventana de mantenimiento.  

        > [!NOTE]  
        > Cuando alcanza el tiempo de ejecución máximo, si ha configurado la opción de **Ejecutar con derechos administrativos** y no establece la opción de **Permitir a los usuarios interactuar con este programa**, Configuration Manager detiene la secuencia de tareas. Si no se detiene la secuencia de tareas, Configuration Manager detiene la supervisión de la secuencia de tareas una vez que se alcanza el tiempo de ejecución máximo permitido.  

    - **Use a boot image** (Usar una imagen de arranque): habilite esta opción para usar la imagen de arranque seleccionada cuando se ejecuta la secuencia de tareas. Seleccione **Examinar** para seleccionar otra imagen de arranque. Desactive esta opción para deshabilitar el uso de la imagen de arranque seleccionada cuando se ejecuta la secuencia de tareas.  

    - **This task sequence can run on any platform** (Esta secuencia de tareas puede ejecutarse en cualquier plataforma): si activa esta opción, Configuration Manager no comprueba el tipo de plataforma del equipo de destino cuando se ejecuta la secuencia de tareas. Esta opción está seleccionada de forma predeterminada.  

    - **This task sequence can only run on the specified client platforms** (Esta secuencia de tareas solo puede ejecutarse en las plataformas cliente especificadas): esta opción especifica los procesadores, las versiones de sistema operativo y los Service Pack en los que se puede ejecutar esta secuencia de tareas. Cuando seleccione esta opción, seleccione al menos una plataforma de la lista. De forma predeterminada, no hay ninguna plataforma seleccionada. Configuration Manager usa esta información cuando se evalúa qué equipos de destino de una recopilación reciben la secuencia de tareas implementada.  

        > [!NOTE]  
        > Cuando se ejecuta una secuencia de tareas desde PXE o medios de arranque, Configuration Manager ignora esta opción. La secuencia de tareas se ejecuta como si estuviera seleccionada la opción **Este programa puede ejecutarse en cualquier plataforma**.  



## <a name="configure-high-impact-task-sequence-settings"></a>Configuración de los ajustes de la secuencia de tareas de gran impacto

Configure una secuencia de tareas como de gran impacto y personalice los mensajes que reciben los usuarios cuando ejecutan la secuencia de tareas.


### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Establecer una secuencia de tareas como una secuencia de tareas de alto impacto

Siga este procedimiento para establecer una secuencia de tareas como de alto impacto.

> [!NOTE]  
> Cualquier secuencia de tareas que cumpla determinadas condiciones se define automáticamente como de alto impacto. Para obtener más información, vea [Configuración para administrar implementaciones de alto riesgo](/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. Seleccione la secuencia de tareas que se va editar y seleccione **Propiedades**.  

3. En la pestaña **Notificación de usuario**, seleccione **Es una secuencia de tareas de alto impacto**.  


### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Crear una notificación personalizada para implementaciones de alto riesgo

Utilice el procedimiento siguiente para crear una notificación personalizada para las implementaciones de gran impacto.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. Seleccione la secuencia de tareas que se va editar y seleccione **Propiedades**.  

3. En la pestaña **Notificación de usuario**, seleccione **Usar texto personalizado**.  

    > [!NOTE]
    > Solo puede establecer el texto de la notificación del usuario cuando seleccione la opción **Es una secuencia de tareas de alto impacto**.  

4. Configure las siguientes opciones:  

    > [!Note]  
    > Cada cuadro de texto tiene un límite máximo de 255 caracteres.  

    - **Texto del título de la notificación de usuario**: especifica el texto azul que aparece en la notificación de usuario del Centro de software. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene: "Confirm you want to upgrade the operating system on this computer" (Confirme que quiere actualizar el sistema operativo en este equipo).  

    - **Texto del mensaje de notificación de usuario**: hay tres cuadros de texto que proporcionan el cuerpo de la notificación personalizada. Todos los cuadros de texto requieren que agregue texto.  

        - Primer cuadro de texto: especifica el cuerpo principal del texto, que normalmente contiene instrucciones para el usuario. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene: "Upgrading the operating system takes time and your computer might restart several times" (La actualización del sistema operativo lleva un tiempo y es posible que el equipo se reinicie varias veces).  

        - Segundo cuadro de texto: especifica el texto en negrita debajo del cuerpo de texto principal. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene: "This in-place upgrade installs the new operating system and automatically migrates your apps, data, and settings" (Esta actualización en contexto instala el nuevo sistema operativo y migra automáticamente sus aplicaciones, datos y configuración).  

        - Tercer cuadro de texto: especifica la última línea de texto debajo del texto en negrita. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene: "Click Install to begin" (Haga clic en Instalar para comenzar). De lo contrario, haga clic en Cancelar".  

#### <a name="example"></a>Ejemplo

Supongamos que configura la siguiente notificación personalizada en las propiedades.

![Pestaña de notificación de usuario personalizada de las propiedades de la secuencia de tareas](../media/user-notification.png)

Se mostrará el siguiente mensaje de notificación cuando el usuario final abra la instalación desde el Centro de software.

![Notificación de la secuencia de tareas personalizada que se muestra al usuario final desde el Centro de software](../media/user-notification-enduser.png)



## <a name="BKMK_DistributeTS"></a> Distribución del contenido al que se hace referencia  

Antes de que los clientes ejecuten una secuencia de tareas que haga referencia a contenido, distribuya dicho contenido a los puntos de distribución. En cualquier momento, puede seleccionar la secuencia de tareas y distribuir su contenido para crear una nueva lista de paquetes de referencia para su distribución. Si realiza cambios en la secuencia de tareas con contenido actualizado, redistribuya el contenido antes de que esté disponible para los clientes. Utilice el siguiente procedimiento para distribuir el contenido al que hace referencia una secuencia de tareas.  

### <a name="process-to-distribute-referenced-content-to-distribution-points"></a>Proceso para distribuir el contenido al que se hace referencia a los puntos de distribución  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y, luego, seleccione el nodo **Secuencias de tareas**.  

2. En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que desee distribuir.  

3. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Implementación** y seleccione **Distribuir contenido**. Esta acción inicia al Asistente para distribuir contenido.  

4. En la página **General** , compruebe que esté seleccionada la secuencia de tareas correcta para la distribución.  

5. En la página **Contenido**, compruebe el contenido que se va a distribuir, como la imagen de arranque a la que hace referencia la secuencia de tareas.  

6. En la página **Destino del contenido**, especifique las recopilaciones, el punto de distribución o el grupo de puntos de distribución donde quiera distribuir el contenido de la secuencia de tareas.  

    > [!IMPORTANT]  
    > Si la secuencia de tareas seleccionada hace referencia a contenido que ya se distribuyó a un punto de distribución específico, el asistente no muestra ese punto de distribución.  

7. Complete el asistente.  

También puede preconfigurar el contenido al que se hace referencia en la secuencia de tareas. Configuration Manager crea un archivo de contenido preconfigurado comprimido que contiene los archivos, las dependencias asociadas y los metadatos asociados del contenido que se selecciona. A continuación puede importar manualmente el contenido en un servidor de sitio, un sitio secundario o un punto de distribución. Para más información sobre cómo preconfigurar archivos de contenido, consulte [Preconfigurar el contenido](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  



## <a name="BKMK_DeployTS"></a> Implementar  

Para obtener más información, vea [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence).

## <a name="BKMK_ExportImport"></a> Exportación e importación  

Exporte e importe secuencias de tareas con o sin sus objetos relacionados. Este contenido al que se hace referencia incluye los siguientes objetos:  

- Imágenes de SO  
- Imágenes de arranque  
- Paquetes como el cliente de instalación del cliente  
- Paquetes de controladores  
- Aplicaciones con dependencias  

Considere los puntos siguientes al exportar e importar secuencias de tareas:  

- Configuration Manager no exporta contraseñas en la secuencia de tareas. Si exporta e importa una secuencia de tareas que contiene contraseñas, edite la secuencia de tareas importada para especificar las contraseñas de nuevo. Revise los siguientes pasos que pueden incluir una contraseña:  

    - [Unirse a dominio o grupo de trabajo](/sccm/osd/understand/task-sequence-steps#BKMK_JoinDomainorWorkgroup)  
    - [Conectar a carpeta de red](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder)  
    - [Ejecutar línea de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)  

- Cuando exporta una secuencia de tareas con el paso **Establecer variables dinámicas**, Configuration Manager no exporta ningún valor para las variables que configure con la opción **Valor secreto**. Vuelva a escribir los valores de estas variables después de importar la secuencia de tareas.  

- Si tiene varios sitios primarios, importe las secuencias de tareas en el sitio de administración central.  


### <a name="process-to-export-task-sequences"></a>Proceso para exportar secuencias de tareas  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y, luego, seleccione el nodo **Secuencias de tareas**.  

2. En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que va a exportar. Si selecciona más de una secuencia de tareas, se almacenan en un archivo de exportación.  

3. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Secuencia de tareas** y seleccione **Exportar**. Esta acción inicia al Asistente para exportar secuencia de tareas.  

4. En la página **General** , especifique la siguiente configuración:  

    - **Archivo**: especifique la ubicación y el nombre del archivo de exportación. Si escribe el nombre de archivo directamente, asegúrese de incluir la extensión .zip. Si examina el archivo de exportación, el asistente agrega automáticamente esta extensión de nombre de archivo.  

    - Si no desea exportar las dependencias de secuencia de tareas, desactive la opción de **Exportar todas las dependencias de secuencia de tareas**. De forma predeterminada, el asistente explora todos los objetivos relacionados y los exporta con la secuencia de tareas. Estas dependencias incluyen secuencias de tareas para las aplicaciones.  

    - Si no desea copiar el contenido del origen de paquete en la ubicación de exportación, desactive la opción de **Exportar todo el contenido de las secuencias de tareas y las dependencias seleccionadas**. Si activa esta opción, el Asistente para importar secuencia de tareas utiliza la ruta de acceso de importación como la nueva ubicación del origen de paquete.  

    - **Comentarios del administrador**: agregue una descripción de la secuencia de tareas que va a exportar.  

5. Complete el asistente.  

El asistente crea los siguientes archivos de salida:  

- Si no se exporta contenido: un archivo .zip.  

- Si se exporta contenido: un archivo .zip y una carpeta *export*_files, donde *export* es el nombre del archivo .zip que contiene el contenido exportado.  

Si incluye contenido cuando exporta una secuencia de tareas, asegúrese de que copia el archivo .zip y la carpeta *export*_files; de lo contrario, la importación no se completará correctamente.  


### <a name="process-to-import-task-sequences"></a>Proceso para importar secuencias de tareas  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y, luego, seleccione el nodo **Secuencias de tareas**.  

2. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Crear** y seleccione **Importar secuencia de tareas**. Esta acción inicia al Asistente para importar secuencia de tareas.  

3. En la página **General** de la cinta de opciones, especifique el archivo .zip exportado.  

4. En la página **Contenido del archivo** , seleccione la acción que requiere para cada objeto que importa. En esta página se muestran todos los objetos que Configuration Manager ha encontrado para importar.  

    - Si es la primera vez que se importó el objeto, seleccione **Crear nuevo**.  

    - Si no es la primera vez que se importa, seleccione una de las siguientes acciones:  

        - **Omitir duplicado** (opción predeterminada): esta acción no importa el objeto. En su lugar, el asistente vincula el objeto existente con la secuencia de tareas.  

        - **Sobrescribir**: esta acción sobrescribe el objeto existente con el objeto importado. Para aplicaciones, puede agregar una revisión para actualizar la aplicación existente o crear una aplicación nueva.  

5. Complete el asistente.  

Después de importar la secuencia de tareas, edítela para especificar las contraseñas que se encontraban en la secuencia de tareas original. Por motivos de seguridad, no se exportan las contraseñas.  



## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Volver a la página anterior cuando se produce un error en una secuencia de tareas

Puede volver a la página anterior cuando ejecuta una secuencia de tareas y se produce un error. En versiones anteriores de Configuration Manager, tenía que reiniciar la secuencia de tareas si se producía un error. Use el botón **Anterior** en los siguientes escenarios:

- Cuando un equipo se inicia en Windows PE, el cuadro de diálogo de arranque de la secuencia de tareas puede mostrarse antes de que la secuencia de tareas esté disponible. Cuando hace clic en Siguiente en este escenario, la página final de la secuencia de tareas se muestra con un mensaje de que no existe ninguna secuencia de tareas disponible. Ahora, puede seleccionar **Anterior** para buscar de nuevo secuencias de tareas disponibles. Puede repetir este proceso hasta que la secuencia de tareas esté disponible.  

- Cuando ejecuta una secuencia de tareas, pero los paquetes de contenido dependientes todavía no están disponibles en los puntos de distribución, se produce un error en la secuencia de tareas. Si aún no se ha distribuido el contenido que faltan, distribúyalo ahora. También puede esperar a que el contenido esté disponible en los puntos de distribución. Después, seleccione **Anterior** para que la secuencia de tareas busque de nuevo el contenido.



## <a name="BKMK_CreateTSVariables"></a> Crear variables de secuencia de tareas para equipos y recopilaciones  

Puede definir variables de secuencia de tareas personalizadas para equipos y recopilaciones. Las variables que se definen para un determinado equipo se conocen como variables de secuencia de tareas por equipo. Las variables definidas para una determinada recopilación se conocen como variables de secuencia de tareas por recopilación. Si hay un conflicto, las variables por equipo tienen prioridad sobre las variables por recopilación. Este comportamiento significa que las variables de secuencia de tareas asignadas a un determinado equipo tienen automáticamente más prioridad que las variables asignadas a la recopilación que contiene el equipo.  

Por ejemplo, el equipo XYZ es miembro de la recopilación ABC. Asigna MiVariable a la recopilación ABC con un valor de 1. También asigna MiVariable al equipo XYZ con un valor de 2. La variable que se asigna al equipo XYZ tiene mayor prioridad que la variable que se asigna a la recopilación ABC. Cuando se ejecuta una secuencia de tareas con esta variable en el equipo XYZ, MiVariable tiene un valor de 2.

Puede ocultar las variables por equipo y por recopilación para que no sean visibles en la consola de Configuration Manager. Cuando se usa la opción **No mostrar este valor en la consola de Configuration Manager**, el valor de la variable no se muestra en la consola. Aun así, la secuencia de tareas puede seguir usando la variable cuando se ejecute. Si ya no desea que estas variables estén ocultas, elimínelas en primer lugar. A continuación, vuelva a definir las variables sin seleccionar la opción para ocultarlas.  

> [!WARNING]  
> La opción **No mostrar este valor en la consola de Configuration Manager** solo se aplica a la consola de Configuration Manager. Los valores de las variables siguen apareciendo en el archivo de registro de la secuencia de tareas (SMSTS.LOG).

Puede administrar las variables por equipo en un sitio primario o en un sitio de administración central. Configuration Manager no admite más de 1000 variables asignadas en un equipo.  

> [!IMPORTANT]  
> Cuando se usan variables por recopilación para secuencias de tareas, tenga en cuenta los comportamientos siguientes:  
>
> - Los cambios en las recopilaciones siempre se replican por toda la jerarquía. Los cambios que realice en las variables de la recopilación se aplicarán no solo a los miembros del sitio actual, sino a todos los miembros de la recopilación en la jerarquía.  
>  
> - Cuando se elimina una recopilación también se eliminan las variables de secuencia de tareas que configuró para la recopilación.  


### <a name="process-to-create-task-sequence-variables-for-a-computer"></a>Proceso para crear variables de secuencia de tareas para un equipo  

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y haga clic en el nodo **Dispositivos**.  

2. Seleccione el equipo de destino y elija **Propiedades**.  

3. En el cuadro de diálogo **Propiedades**, cambie a la pestaña **Variables**.  

4. Para cada variable que quiera crear, seleccione el icono **Nuevo**. Especifique el **Nombre** y el **Valor** de la variable de la secuencia de tareas. Active la opción **No mostrar este valor en la consola de Configuration Manager** si desea ocultar la variable para que no esté visible en la consola de Configuration Manager.  

5. Después de agregar todas las variables a las propiedades del equipo, seleccione **Aceptar**.  


### <a name="process-to-create-task-sequence-variables-for-a-collection"></a>Proceso para crear variables de secuencia de tareas para una recopilación  

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y seleccione el nodo **Recopilaciones de dispositivos**. Seleccione la recopilación de destino y elija **Propiedades**.  

2. En el cuadro de diálogo **Propiedades**, cambie a la pestaña **Variables de la recopilación**.  

3. Para cada variable que quiera crear, seleccione el icono **Nuevo**. Especifique el **Nombre** y el **Valor** de la variable de la secuencia de tareas. Active la opción **No mostrar este valor en la consola de Configuration Manager** si desea ocultar la variable para que no esté visible en la consola de Configuration Manager.  

4. Si lo desea, especifique la prioridad de Configuration Manager que desea utilizar cuando se evalúen las variables de la secuencia de tareas.  

5. Después de agregar todas las variables a las propiedades de la recopilación, seleccione **Aceptar**.  



## <a name="BKMK_AdditionalActionsTS"></a> Acciones adicionales para administrar secuencias de tareas  

Puede administrar secuencias de tareas con acciones adicionales cuando se selecciona la secuencia de tareas.  

### <a name="available-options"></a>Opciones disponibles

#### <a name="edit"></a>Editar

Para obtener más información, vea [Editar una secuencia de tareas](#BKMK_ModifyTaskSequence).

#### <a name="enable"></a>Habilitar

Habilita la secuencia de tareas para que los clientes la puedan ejecutar. No es necesario volver a implementar una secuencia de tareas después de habilitarla.  

#### <a name="disable"></a>Deshabilitar

Deshabilita la secuencia de tareas para que no pueda ejecutarse en equipos. Puede implementar una secuencia de tareas deshabilitada, pero los equipos no la ejecutarán hasta que la habilite.  

#### <a name="export"></a>Exportar

Para más información, consulte [Exportar e importar secuencias de tareas](#BKMK_ExportImport).

#### <a name="copy"></a>Copiar

Realiza una copia de la secuencia de tareas seleccionada. Esta acción es útil para crear una secuencia de tareas basada en una secuencia de tareas existente.

Al realizar una copia de una secuencia de tareas en una carpeta, la copia se muestra en la carpeta hasta que actualice el nodo de secuencia de tareas. Después de la actualización, la copia aparece en la carpeta raíz.  

#### <a name="refresh"></a>Actualizar

Actualiza los detalles de la secuencia de tareas seleccionada.

#### <a name="delete"></a>Eliminar

Elimina la secuencia de tareas seleccionada.

#### <a name="create-phased-deployment"></a>Crear una implementación por fases

Para más información, vea [Crear implementaciones por fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).

#### <a name="deploy"></a>Implementar

Para obtener más información, vea [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence).

#### <a name="distribute-content"></a>Distribuir contenido

Inicia el Asistente para distribuir contenido para enviar el contenido al que se hace referencia a los puntos de distribución.

#### <a name="create-prestaged-content-file"></a>Crear archivo de contenido preconfigurado

Inicia el Asistente para crear archivos de contenido preconfigurados para preconfigurar el contenido de la secuencia de tareas. Para obtener información sobre cómo crear un archivo de contenido preconfigurado, consulte [Preconfigurar el contenido](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).

#### <a name="move"></a>Mover

Mueve la secuencia de tareas a otra carpeta en el nodo **Secuencias de tareas**.

#### <a name="set-security-scopes"></a>Establecer ámbitos de seguridad

Seleccione los ámbitos de seguridad para la secuencia de tareas seleccionada. Para obtener más información, consulte [Ámbitos de seguridad](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope).

#### <a name="properties"></a>Propiedades

Para obtener más información, consulte [Configurar propiedades del Centro de software](#bkmk_prop-general) y [Configuración de los ajustes de la secuencia de tareas avanzada](#bkmk_prop-advanced).

#### <a name="view"></a>Ver

<!--3633146-->
A partir de la versión 1902, la acción **Ver** de las secuencias de tareas es la predeterminada. Esta acción le permite ver los pasos de la secuencia de tareas sin bloquearla para su edición.  


## <a name="see-also"></a>Consulte también

[Escenarios para implementar sistemas operativos de empresa](scenarios-to-deploy-enterprise-operating-systems.md)
