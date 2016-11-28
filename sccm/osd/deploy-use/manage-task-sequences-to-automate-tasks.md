---
title: "Administración de secuencias de tareas para automatizar tareas | Configuration Manager"
description: Puede crear, editar, implementar, importar y exportar secuencias de tareas para administrarlas en su entorno de System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
caps.latest.revision: 10
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 04e4e8193d427289a3b84a14efe18511bf5c9731


---
# <a name="manage-task-sequences-to-automate-tasks-in-system-center-configuration-manager"></a>Administrar secuencias de tareas para automatizar tareas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Utilice secuencias de tareas para automatizar los pasos en su entorno de System Center Configuration Manager. Estas etapas pueden implementar una imagen de sistema operativo en un equipo de destino, compilar y capturar una imagen de sistema operativo a partir de un conjunto de archivos de instalación de sistema operativo, y capturar y restaurar la información de estado de usuario. Las secuencias de tareas se ubican en la consola de Configuration Manager, en el área de trabajo **Biblioteca de software** > **Sistemas operativos** > **Secuencia de tareas**. El nodo **Secuencia de tareas**, incluidas todas las subcarpetas creadas, se replica en toda la jerarquía de Configuration Manager. Para obtener información, consulte [Planning considerations for automating tasks](../plan-design/planning-considerations-for-automating-tasks.md) (Consideraciones de planeación para la automatización de tareas).  

 Consulte las siguientes secciones para administrar secuencias de tareas:

##  <a name="a-namebkmkcreatetasksequencea-create-task-sequences"></a><a name="BKMK_CreateTaskSequence"></a> Crear secuencias de tareas  
 Cree secuencias de tareas con el Asistente para crear secuencia de tareas. Este asistente puede crear los siguientes tipos de secuencias de tareas:  

|Tipo de secuencia de tareas|Más información|  
|------------------------|----------------------|  
|[Secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md)|Este tipo de secuencia de tareas crea las etapas para instalar un sistema operativo, así como la opción para migrar datos de usuario, incluir actualizaciones de software e instalar aplicaciones.|  
|[Secuencia de tareas para actualizar un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md)|Este tipo de secuencia de tareas crea las etapas para actualizar un sistema operativo, así como la opción para incluir actualizaciones de software e instalar aplicaciones.|  
|[Secuencia de tareas para capturar un sistema operativo](create-a-task-sequence-to-capture-an-operating-system.md)|Este tipo de secuencia de tareas crea las etapas para compilar y capturar un sistema operativo desde un equipo de referencia. Puede incluir actualizaciones de software e instalar aplicaciones en el equipo de referencia antes de capturar la imagen.|  
|[Secuencia de tareas para capturar y restaurar el estado de usuario](create-a-task-sequence-to-capture-and-restore-user-state.md)|En esta secuencia de tareas se indican las etapas que se deben agregar a una secuencia de tareas existente para capturar y restaurar los datos de estado de usuario.|  
|[Secuencia de tareas para administrar discos duros virtuales](use-a-task-sequence-to-manage-virtual-hard-disks.md)|Este tipo de secuencia de tareas contiene las etapas para crear un VHD, que incluye la instalación de un sistema operativo y aplicaciones, que puede publicar en System Center Virtual Machine Manager (VMM) desde la consola de Configuration Manager.|  
|[Secuencia de tareas personalizada](create-a-custom-task-sequence.md)|Este tipo de secuencia de tareas no agrega ninguna etapa a la secuencia de tareas. Debe editar la secuencia de tareas y agregar etapas a la secuencia de tareas después de crearla.|  

##  <a name="a-namebkmkmodifytasksequencea-edit-a-task-sequence"></a><a name="BKMK_ModifyTaskSequence"></a> Editar una secuencia de tareas  
 Para modificar una secuencia de tareas, agregue o quite pasos de la secuencia de tareas, agregue o quite grupos de secuencias de tareas, o cambie el orden de los pasos. Utilice el siguiente procedimiento para modificar una secuencia de tareas existente.  

> [!IMPORTANT]  
>  Cuando edite una secuencia de tareas creada mediante el Asistente para crear secuencia de tareas, el nombre del paso puede ser la acción o el tipo de paso. Por ejemplo, puede ver un paso con el nombre "Disco de partición 0", que es la acción de un paso de tipo [Formatear y crear particiones en el disco](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk). Todos los pasos de la secuencia de tareas se documentan por su tipo, no necesariamente por el nombre del paso que se muestra en el Editor.  

#### <a name="to-edit-a-task-sequence"></a>Para editar una secuencia de tareas  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que desee editar.  

4.  En la pestaña **Inicio** , en el grupo **Secuencia de tareas** , haga clic en **Editar**y, a continuación, realice alguna de las operaciones siguientes:  

    -   Para agregar un paso de secuencia de tareas, haga clic en **Agregar**, seleccione el tipo de paso y, a continuación, haga clic en el paso de secuencia de tareas que desea agregar. Por ejemplo, para agregar el paso de ejecución de línea de comandos haga clic en **Agregar**, seleccione **General**y, a continuación, haga clic en **Ejecutar línea de comandos**.  

         Para obtener una lista de todos los pasos de secuencia de tareas y su tipo, consulte la tabla que sigue a este procedimiento.  

    -   Para agregar un grupo a la secuencia de tareas, haga clic en **Agregar**y, a continuación, haga clic en **Nuevo grupo**. Después de agregar un grupo, podrá agregar pasos al grupo.  

    -   Para cambiar el orden de los pasos y los grupos en la secuencia de tareas, seleccione el paso o grupo que desee reordenar y, a continuación, use los iconos **Aumentar prioridad** o **Reducir prioridad** . Solo puede mover un paso o un grupo cada vez.  

    -   Para quitar un paso o un grupo, seleccione el paso o el grupo y haga clic en **Quitar**.  

5.  Haga clic en **Aceptar** para guardar los cambios.  

 Para obtener una lista de las etapas de secuencia de tareas disponibles, consulte [Pasos de la secuencia de tareas](../understand/task-sequence-steps.md).  

##  <a name="a-namebkmkdistributetsa-distribute-content-referenced-by-a-task-sequence"></a><a name="BKMK_DistributeTS"></a> Distribuir contenido al que hace referencia una secuencia de tareas  
 Antes de que los clientes ejecuten una secuencia de tareas que haga referencia a contenido, debe distribuir dicho contenido a los puntos de distribución. En cualquier momento, puede seleccionar la secuencia de tareas y distribuir su contenido para crear una nueva lista de paquetes de referencia para su distribución. Si realiza cambios en la secuencia de tareas con contenido actualizado, debe redistribuir el contenido antes de que esté disponible para los clientes. Utilice el siguiente procedimiento para distribuir el contenido al que hace referencia una secuencia de tareas.  

#### <a name="to-distribute-referenced-content-to-distribution-points"></a>Para distribuir el contenido al que se hace referencia a los puntos de distribución  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que desee distribuir.  

4.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Distribuir contenido** para iniciar el Asistente para distribuir contenido.  

5.  En la página **General** , compruebe que esté seleccionada la secuencia de tareas correcta para la distribución y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Contenido** , compruebe el contenido que se va a distribuir, como la imagen de arranque a la que hace referencia la secuencia de tareas, y, a continuación, haga clic en **Siguiente**.  

7.  En la página **Destino del contenido** , especifique las recopilaciones, el punto de distribución o el grupo de puntos de destino donde desee distribuir el contenido de la secuencia de tareas y, a continuación, haga clic en **Siguiente**.  

    > [!IMPORTANT]  
    >  Si la secuencia de tareas seleccionada hace referencia a contenido que ya se distribuyó a un punto de distribución específico, el asistente no mostrará ese punto de distribución en la lista.  

8.  Complete el asistente.  

 Puede preconfigurar el contenido al que se hace referencia en la secuencia de tareas. Configuration Manager crea un archivo de contenido preconfigurado comprimido que contiene los archivos, las dependencias asociadas y los metadatos asociados del contenido que se selecciona. A continuación, puede importar manualmente el contenido en un servidor de sitio, un sitio secundario o un punto de distribución. Para más información sobre cómo preconfigurar archivos de contenido, consulte [Preconfigurar el contenido](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content).  

##  <a name="a-namebkmkdeploytsa-deploy-a-task-sequence"></a><a name="BKMK_DeployTS"></a> Implementar una secuencia de tareas  
 Utilice el siguiente procedimiento para implementar una secuencia de tareas en los equipos de una recopilación.  

> [!WARNING]  
>  Puede administrar el comportamiento de las implementaciones de secuencias de tareas de alto riesgo. Una implementación de alto riesgo es una implementación que se instala automáticamente y puede provocar resultados no deseados. Por ejemplo, una secuencia de tareas con el propósito **Requerido** que implementa un sistema operativo se considera una implementación de alto riesgo. Para obtener más información, consulte [Settings to manage high-risk deployments](../../protect/understand/settings-to-manage-high-risk-deployments.md) (Configuración para administrar implementaciones de alto riesgo).  

> [!NOTE]  
>  Los mensajes de estado para la implementación de la secuencia de tareas se muestran en la ventana Mensaje en un sitio primario, pero no se muestran en un sitio de administración central.  

#### <a name="to-deploy-a-task-sequence"></a>Para implementar una secuencia de tareas  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que desee implementar.  

4.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.  

    > [!NOTE]  
    >  Si **Implementar** no está disponible, la secuencia de tareas tiene una referencia que no es válida.  Corrija la referencia y, a continuación, intente implementar la secuencia de tareas de nuevo.  

5.  En la página **General** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    -   **Secuencia de tareas**: especifique la secuencia de tareas que quiere implementar. De forma predeterminada, este cuadro muestra la secuencia de tareas seleccionada.  

    -   **Recopilación**: especifique la recopilación que contiene los equipos que ejecutarán la secuencia de tareas.  

         No implemente secuencias de tareas que instalen sistemas operativos en recopilaciones inapropiadas, como la recopilación **Todos los sistemas** . Asegúrese de que la recopilación que seleccione contiene solo los equipos que desea que ejecuten la secuencia de tareas.  

        > [!NOTE]  
        >  Al realizar una implementación de alto riesgo, como un sistema operativo, la ventana **Seleccionar recopilación** muestra solo las recopilaciones personalizadas que cumplen con la configuración de comprobación de implementación que está configurada en las propiedades del sitio. Las implementaciones de alto riesgo siempre se limitan a las recopilaciones personalizadas, las recopilaciones que cree y la recopilación integrada **Equipos desconocidos** . Cuando cree una implementación de alto riesgo, no puede seleccionar una recopilación integrada como **Todos los sistemas**. Desactive **Ocultar recopilaciones con un número de miembros superior a la configuración de tamaño mínimo del sitio** para ver todas las recopilaciones personalizadas que contienen menos clientes que el tamaño máximo configurado. Para obtener más información, consulte [Settings to manage high-risk deployments](../../protect/understand/settings-to-manage-high-risk-deployments.md) (Configuración para administrar implementaciones de alto riesgo).  
        >   
        >  La configuración de comprobación de implementación se basa en la pertenencia actual de la recopilación. Después de implementar la secuencia de tareas, la pertenencia a la recopilación no se vuelve a evaluar para la configuración de implementación de alto riesgo.  
        >   
        >  Por ejemplo, supongamos que establece el **Tamaño predeterminado** en 100 y el **Tamaño máximo** en 1000. Al crear una implementación de alto riesgo, la ventana **Seleccionar recopilación** solo mostrará las recopilaciones que contienen menos de 100 clientes. Si desactiva la configuración **Ocultar recopilaciones con un recuento de miembros mayor que la configuración de tamaño mínimo del sitio**, la ventana mostrará las recopilaciones que contienen menos de 1000 clientes.  
        >   
        >  Al seleccionar una recopilación que contenga un rol de sitio, se aplicará lo siguiente:  
        >   
        >  -   Si la recopilación contiene un servidor de sistema de sitio y establece la configuración de comprobación de implementación para bloquear las recopilaciones con servidores de sistema de sitio, se producirá un error y no podrá continuar.  
        > -   El Asistente para implementar software mostrará una advertencia de alto riesgo cuando la recopilación contenga un servidor de sistema de sitio y establezca la configuración de comprobación de implementación para advertirle si las recopilaciones tienen servidores de sistema de sitio, si la recopilación supera el valor de tamaño predeterminado o si la recopilación contiene un servidor. Debe aceptar la creación de una implementación de alto riesgo y se creará un mensaje de estado de auditoría.  

    -   **Comentarios (opcional)**: especifique información adicional que describa esta implementación de la secuencia de tareas.  

6.  En la página **Configuración de implementación** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    -   **Propósito**: en la lista desplegable, elija una de las opciones que se indican a continuación.  

        -   **Disponible**: si la secuencia de tareas se implementa en un usuario, el usuario verá la secuencia de tareas publicada en el catálogo de aplicaciones y podrá solicitarla a petición. Si la secuencia de tareas se implementa en un dispositivo, el usuario la verá en el Centro de software y la podrá instalar a petición.  

        -   **Necesario**: la secuencia de tareas se implementa automáticamente, según la programación configurada. Sin embargo, un usuario puede realizar un seguimiento del estado de la implementación de la secuencia de tareas (si no está oculto) y puede instalar la secuencia de tareas antes de la fecha límite mediante el Centro de software.  

    -   **Implementar automáticamente según la programación tanto si un usuario inició sesión como si no**: esta opción no está disponible cuando se implementa una secuencia de tareas.  

    -   **Enviar paquetes de reactivación**: si el propósito de la implementación se establece como **Necesario** y se selecciona esta opción, se enviará un paquete de reactivación a los equipos antes de instalar la implementación para reactivar el equipo en suspensión a la hora límite de la instalación. Para poder utilizar esta opción, los equipos y las redes deben configurarse para Wake on LAN.  

    -   **Permitir a los clientes de una conexión a Internet de uso medido descargar contenido una vez cumplida la fecha límite de instalación, lo cual podría suponer costes adicionales**: si tiene una secuencia de tareas que instala una aplicación, pero no implementa un sistema operativo, puede especificar si permite a los clientes descargar contenido una vez cumplida la fecha límite de la instalación cuando usan una conexión a Internet de uso medido. En ocasiones, los proveedores de acceso a Internet cobran según la cantidad de datos que envía y recibe cuando se utiliza una conexión a Internet de uso medido.  

        > [!NOTE]  
        >  Aunque el uso de una conexión a Internet de uso medido podría funcionar para secuencias de tareas que no implementan un sistema operativo, no se admite este tipo de conexión para este propósito.  

    -   **Solicitar aprobación del administrador si los usuarios solicitan esta aplicación**: esta opción no está disponible cuando se implementa una secuencia de tareas.  

    -   **Estar disponible para**: especifique si la secuencia de tareas debe estar disponible para medios, el entorno PXE o clientes de Configuration Manager.  

        > [!IMPORTANT]  
        >  Use la opción **Sólo medios y PXE (ocultos)** para implementaciones automatizadas de secuencia de tareas. Seleccione **Permitir la implementación desatendida de sistema operativo** y configure la variable SMSTSPreferredAdvertID como parte del medio para que el equipo arranque automáticamente en la implementación sin interacción del usuario. Para más información sobre las variables integradas, vea [Variables integradas de secuencia de tareas en Configuration Manager](../understand/task-sequence-built-in-variables.md).  

7.  En la página **Programación** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    > [!IMPORTANT]  
    >  Cuando un cliente de Windows PE se inicia desde PXE o desde un medio de arranque, el cliente no evalúa las programaciones de implementación (horas límite, de inicio y de expiración). Configure programaciones en implementaciones únicamente en clientes que se inicien desde el sistema operativo Windows completo. Considere el uso de otros métodos (como periodos de mantenimiento) para controlar las secuencias de tareas activas implementadas en clientes que se inician desde Windows PE.  

    -   **Programar cuándo estará disponible esta implementación**: especifique la fecha y hora en que la secuencia de tareas estará disponible para ejecutarse en el equipo de destino. Cuando selecciona la casilla **UTC** , este valor garantiza que la secuencia de tareas estará disponible en varios equipos de destino a la misma hora, en lugar de en horas diferentes, según la hora local de los equipos de destino.  

         Si la hora de inicio es anterior a la hora requerida, el cliente descarga la secuencia de tareas a la hora de inicio que especifique.  

    -   **Programar cuándo expirará esta implementación**: especifique la fecha y hora en que expirará la secuencia de tareas en el equipo de destino. Cuando seleccione la casilla **UTC** , este valor garantiza que la secuencia de tareas expira en varios equipos de destino a la misma hora, en lugar de en horas diferentes, según la hora local de los equipos de destino.  

    -   **Programación de asignación**: especifique cuándo debe ejecutarse la secuencia de tareas necesaria en el equipo de destino. Puede agregar varias programaciones.  

         Puede especificar la fecha y hora de inicio de la programación, si la secuencia de tareas se ejecuta semanalmente, mensualmente o en un intervalo personalizado, y si la secuencia de tareas se ejecuta tras un evento, como un inicio o cierre de sesión.  

        > [!NOTE]  
        >  Si, para una secuencia de tareas requerida, programa una hora de inicio anterior a la fecha y hora que define el inicio de la disponibilidad de la secuencia de tareas, el cliente de Configuration Manager descarga la secuencia de tareas a la hora de inicio programada, aunque la secuencia de tareas esté disponible a una hora anterior.  

    -   **Comportamiento de reejecución**: especifique cuándo se volverá a ejecutar la secuencia de tareas. Puede especificar una de las siguientes opciones.  

        -   **No volver a ejecutar nunca el programa implementado**: la secuencia de tareas no se vuelve a ejecutar en el cliente si ya se ejecutó antes en este. La secuencia de tareas no se vuelve a ejecutar aunque no se completara en su primera ejecución o sus archivos cambiaron.  

        -   **Volver a ejecutar siempre el programa**: la secuencia de tareas se vuelve a ejecutar siempre en el cliente cuando se programa la implementación, incluso si se ejecutó antes correctamente. Esta opción es especialmente útil cuando se utilizan implementaciones periódicas en las que la secuencia de tareas se actualiza regularmente.  

            > [!IMPORTANT]  
            >  Aunque es una opción predeterminada, no tiene ningún efecto hasta que se le asigna una implementación requerida. Los usuarios siempre pueden volver a ejecutar las implementaciones disponibles.  

        -   **Volver a ejecutar en caso de error del intento anterior**: la secuencia de tareas se vuelve a ejecutar cuando se programa la implementación solo si la secuencia de tareas no se pudo ejecutar anteriormente. Esta opción es particularmente útil para implementaciones requeridas. Las implementaciones reintentarán automáticamente su ejecución de acuerdo a la programación de asignación si el último intento de ejecución no se completó correctamente.  

        -   Volver a ejecutar si el intento anterior se realizó correctamente: la secuencia de tareas se vuelve a ejecutar solo si se ejecutó antes correctamente en el cliente. Esta configuración es útil cuando se utiliza en implementaciones periódicas en las que la secuencia de tareas se actualiza periódicamente, y cada actualización requiere que la actualización anterior está instalada correctamente.  

        > [!NOTE]  
        >  Dado que un usuario puede volver a ejecutar una implementación de secuencia de tareas disponible, asegúrese de que antes de implementar una secuencia de tareas disponible en un entorno de producto, evalúa y prueba cuidadosamente qué ocurre si un usuario vuelve a ejecutar la secuencia de tareas varias veces.  

8.  En la página **Experiencia del usuario** , especifique la siguiente información y, a continuación, haga clic en **Siguiente**.  

    -   **Permitir que los usuarios ejecuten el programa independientemente de las asignaciones**: especifique si se le permite al usuario ejecutar una secuencia de tareas necesaria independientemente de las asignaciones de la implementación.  

    -   **Mostrar progreso de la secuencia de tareas**: especifique si el cliente de Configuration Manager debe mostrar el progreso de la secuencia de tareas.  

    -   **Instalación de software**: especifique si el usuario puede instalar software fuera de las ventanas de mantenimiento configuradas después del tiempo programado.  

    -   **Reinicio del sistema (si es necesario para completar la instalación)**: especifique si se permite al usuario reiniciar el equipo tras una instalación de software fuera de una ventana de mantenimiento configurada tras la hora de asignación.  

    -   **Permitir que la secuencia de tareas se ejecute para el cliente en Internet**: especifique si se permite que la secuencia de tareas se ejecute en un cliente basado en Internet que Configuration Manager detecte en Internet. Las operaciones que instalan software, como un sistema operativo, no son compatibles con esta configuración. Utilice esta opción solo para secuencias de tareas basadas en scripts que realizan operaciones en el sistema operativo estándar.  

9. En la página **Alertas** , especifique la configuración de alertas que desea establecer para esta implementación de secuencia de tareas y, a continuación, haga clic en **Siguiente**.  

10. En la página **Puntos de distribución** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    -   **Opciones de implementación**: especifique una de las siguientes opciones.  

        > [!NOTE]  
        >  si utiliza multidifusión para implementar un sistema operativo, el contenido se debe descargar en los equipos de destino, como se necesite o antes de que se ejecute la secuencia de tareas.  

        -   Especificar que los clientes descarguen el contenido desde el punto de distribución en el equipo de destino como necesite la secuencia de tareas.  

        -   Especificar que los clientes descarguen todo el contenido desde el punto de distribución en el equipo de destino antes de que se ejecute la secuencia de tareas. Esta opción no estará disponible si la tarea está disponible para implementación de medios de arranque y PXE (consulte la página **Configuración de implementación** ).  

        -   Especificar que los clientes ejecuten el contenido desde el punto de distribución. Esta opción está disponible sólo cuando todos los paquetes asociados con la secuencia de tareas están habilitados para utilizar un recurso compartido de paquete en el punto de distribución. Para habilitar el contenido de tal modo que utilice un recurso compartido de paquete, consulte la pestaña **Acceso a datos** en las **Propiedades** de cada paquete.  

    -   **Cuando no haya disponible ningún punto de distribución local, usar un punto de distribución remoto**: especifique si los clientes pueden usar puntos de distribución en redes lentas y poco confiables para descargar el contenido necesario para la secuencia de tareas.  

11. Complete el asistente.  

##  <a name="a-namebkmkexportimporta-export-and-import-task-sequences"></a><a name="BKMK_ExportImport"></a> Exportar e importar secuencias de tareas  
 Puede exportar e importar secuencias de tareas con o sin sus objetos relacionados, como, por ejemplo, una imagen de sistema operativo, una imagen de arranque, un paquete de agentes de cliente, un paquete de controladores y aplicaciones que tengan dependencias.  

 Considere lo siguiente al exportar e importar secuencias de tareas.  

-   Las contraseñas almacenadas en la secuencia de tareas no se exportan. Si exporta e importa una secuencia de tareas que contiene contraseñas, debe editar la secuencia de tareas importada y especificar las contraseñas de nuevo. Procure especificar contraseñas para las acciones [Unirse a dominio o grupo de trabajo](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup), [Conectar a carpeta de red](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) y [Ejecutar línea de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine).  

-   Como práctica recomendada, si tiene varios sitios primarios, importe las secuencias de tareas en el sitio de administración central.  

 Utilice los siguientes procedimientos para exportar e importar una secuencia de tareas.  

#### <a name="to-export-task-sequences"></a>Para exportar secuencias de tareas  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que va a exportar. Si selecciona más de una secuencia de tareas, se almacenan en un archivo de exportación.  

4.  En la pestaña **Inicio** , en el grupo **Secuencia de tareas** , haga clic en **Exportar** para iniciar el Asistente para exportar secuencias de tareas.  

5.  En la página **General** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    -   En el cuadro **Archivo** , especifique la ubicación y el nombre del archivo de exportación. Si escribe el nombre de archivo directamente, asegúrese de incluir la extensión .zip. Si examina el archivo de exportación, el asistente agrega automáticamente esta extensión de nombre de archivo.  

    -   Desactive la casilla **Exportar todas las dependencias de secuencia de tareas** si no desea exportar las dependencias de secuencia de tareas. De forma predeterminada, el asistente explora todos los objetivos relacionados y los exporta con la secuencia de tareas. Esto incluye todas las dependencias para aplicaciones.  

    -   Desactive la casilla **Exportar todo el contenido de las secuencias de tareas y las dependencias seleccionadas** si no desea copiar el contenido del origen de paquete en la ubicación de exportación. Si activa esta casilla de verificación, el Asistente para importar secuencia de tareas utiliza la ruta de acceso de importación como la nueva ubicación del origen de paquete.  

    -   En el cuadro **Comentarios del administrador** , agregue una descripción de la secuencia de tareas que va a exportar.  

6.  Complete el asistente.  

 El asistente crea los siguientes archivos de salida:  

-   Si no se exporta contenido: un archivo .zip.  

-   Si se exporta contenido: un archivo .zip y una carpeta *export*_files, donde *export* es el nombre del archivo .zip que contiene el contenido exportado.  

 Si incluye contenido cuando exporta una secuencia de tareas, asegúrese de que copia el archivo .zip y la carpeta *export*_files; de lo contrario, la importación no se completará correctamente.  

#### <a name="to-import-task-sequences"></a>Para importar secuencias de tareas  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Importar secuencia de tareas** para iniciar el Asistente para importar secuencia de tareas.  

4.  En la página **General** , especifique el archivo .zip exportado y, a continuación, haga clic en **Siguiente**.  

5.  En la página **Contenido del archivo** , seleccione la acción que requiere para cada objeto que importa. Esta página muestra todos los objetos que importará Configuration Manager.  

    -   Si es la primera vez que se importó el objeto, seleccione **Crear nuevo**.  

    -   Si no es la primera vez que se importa, seleccione una de las siguientes acciones:  

        -   **Omitir duplicado** (opción predeterminada): esta acción no importa el objeto. En su lugar, el asistente vincula el objeto existente con la secuencia de tareas.  

        -   **Sobrescribir**: esta acción sobrescribe el objeto existente con el objeto importado. Para aplicaciones, puede agregar una revisión para actualizar la aplicación existente o crear una aplicación nueva.  

6.  Complete el asistente.  

 Después de importar la secuencia de tareas, edítela para especificar las contraseñas que se encontraban en la secuencia de tareas original. Por motivos de seguridad, no se exportan las contraseñas.  

##  <a name="a-namebkmkcreatetsvariablesa-create-task-sequence-variables-for-computers-and-collections"></a><a name="BKMK_CreateTSVariables"></a> Crear variables de secuencia de tareas para equipos y recopilaciones  
 Puede definir variables de secuencia de tareas personalizadas para equipos y recopilaciones. Las variables que se definen para un determinado equipo se conocen como variables de secuencia de tareas por equipo. Las variables definidas para una determinada recopilación se conocen como variables de secuencia de tareas por recopilación. Si hay un conflicto, las variables por equipo tienen prioridad sobre las variables por recopilación. Por lo tanto, las variables de secuencia de tareas asignadas a un determinado equipo tienen automáticamente más prioridad que las variables asignadas a la recopilación que contiene al equipo.  

 Por ejemplo, si hay una variable asignada a la recopilación ABC y hay una variable con el mismo nombre asignada al equipo XYZ, que forma parte de la recopilación ABC, la variable asignada al equipo XYZ tiene una prioridad más alta que la variable asignada a la recopilación ABC.  

 Puede ocultar las variables por equipo y por recopilación para que no sean visibles en la consola de Configuration Manager. Si ya no desea ocultar estas variables, debe eliminarlas y redefinirlas sin seleccionar la opción para ocultarlas. Cuando se usa la opción **No mostrar este valor en la consola de Configuration Manager**, el valor de la variable no se muestra, pero la secuencia de tareas lo puede seguir usando cuando se ejecute.  

 Puede administrar las variables por equipo en un sitio primario o en un sitio de administración central. Configuration Manager no admite más de 1000 variables asignadas en un equipo.  

> [!WARNING]  
>  Cuando se usan variables por recopilación para secuencias de tareas, tenga en cuenta lo siguiente:  
>   
>  -   Dado que los cambios en recopilaciones siempre se replican a través de la jerarquía, los cambios que realice en las variables de la recopilación se aplicarán no solo en los miembros del sitio actual, sino en todos los miembros de la recopilación en la jerarquía.  
> -   Cuando se elimina una recopilación también se eliminan las variables de secuencia de tareas que están configuradas para la recopilación.  

 Utilice los procedimientos siguientes para crear variables de secuencia de tareas para un equipo o una recopilación.  

#### <a name="to-create-task-sequence-variables-for-a-computer"></a>Para crear variables de secuencia de tareas para un equipo  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , expanda la recopilación que contiene el equipo al que desea agregar la variable.  

3.  Seleccione el equipo y haga clic en **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades** , haga clic en la pestaña **Variables** .  

5.  Para cada variable que desee crear, haga clic en el icono **Nueva** en el cuadro de diálogo **<Nueva\> variable** y especifique el nombre y el valor de la variable de secuencia de tareas. Desactive la casilla **No mostrar este valor en la consola de Configuration Manager** si desea ocultar las variables para que no estén visibles en la consola de Configuration Manager.  

6.  Después de agregar todas las variables al equipo, haga clic en **Aceptar**.  

#### <a name="to-create-task-sequence-variables-for-a-collection"></a>Para crear variables de secuencia de tareas para una recopilación  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , seleccione la recopilación a la que desea agregar la variable y, a continuación, haga clic en **Propiedades**.  

3.  En el cuadro de diálogo **Propiedades** , haga clic en la pestaña **Variables de la recopilación** .  

4.  Para cada variable que desee crear, haga clic en el icono **Nueva** en el cuadro de diálogo **<Nueva\> variable** y especifique el nombre y el valor de la variable de secuencia de tareas. Desactive la casilla **No mostrar este valor en la consola de Configuration Manager** si desea ocultar las variables para que no estén visibles en la consola de Configuration Manager.  

5.  Si lo desea, especifique la prioridad de  Configuration Manager que desea utilizar cuando se evalúen las variables de la secuencia de tareas.  

6.  Después de agregar todas las variables a la recopilación, haga clic en **Aceptar**.  

##  <a name="a-namebkmkadditionalactionstsa-additional-actions-to-manage-task-sequences"></a><a name="BKMK_AdditionalActionsTS"></a> Acciones adicionales para administrar secuencias de tareas  
 Puede administrar secuencias de tareas con acciones adicionales cuando se selecciona la secuencia de tareas mediante el procedimiento siguiente.  

#### <a name="to-select-a-task-sequence-to-manage"></a>Para seleccionar la secuencia de tareas que desea administrar  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos** y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que desea administrar y, a continuación, seleccione una de las opciones disponibles.  

 Utilice la tabla siguiente para obtener más información acerca de las acciones adicionales para administrar las secuencias de tareas.  

|Acción|Descripción|  
|------------|-----------------|  
|**Copiar**|Realiza una copia de la secuencia de tareas seleccionada. Es posible que esta acción sea útil si desea crear una nueva secuencia de tareas basada en una secuencia de tareas existente.<br /><br /> Al realizar una copia de una secuencia de tareas en una carpeta, la copia se muestra en la carpeta hasta que actualice el nodo de secuencia de tareas.  Después de la actualización, la copia aparece en la carpeta raíz.|  
|**Deshabilitar**|Deshabilita la secuencia de tareas para que no pueda ejecutarse en equipos. Las secuencias de tareas deshabilitadas pueden implementarse en equipos, pero los equipos no podrán ejecutar las secuencias de tareas hasta que se habiliten.|  
|**Habilitar**|Habilita la secuencia de tareas para que se pueda ejecutar. No es necesario volver a implementar las secuencias de tareas implementadas después de habilitarlas.|  
|**Crear archivo de contenido preconfigurado**|Inicia el Asistente para crear archivos de contenido preconfigurados para preconfigurar el contenido de la secuencia de tareas. Para obtener información sobre cómo crear un archivo de contenido preconfigurado, consulte [Preconfigurar el contenido](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content).|  
|**Moverr**|La secuencia de tareas seleccionada se mueve a otra carpeta.|  
|**Propiedades**|Abre el cuadro de diálogo **Propiedades** de la secuencia de tareas seleccionada. Utilice este cuadro de diálogo para cambiar el comportamiento del objeto de secuencia de tareas. Sin embargo, los pasos de la secuencia de tareas no se pueden cambiar mediante este cuadro de diálogo.|  

## <a name="next-steps"></a>Pasos siguientes
[Escenarios para implementar sistemas operativos de empresa](scenarios-to-deploy-enterprise-operating-systems.md)



<!--HONumber=Nov16_HO1-->


