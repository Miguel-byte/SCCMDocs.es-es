---
title: Administrar secuencias de tareas
titleSuffix: Configuration Manager
description: Cree, edite, implemente, importe y exporte secuencias de tareas para administrarlas y automatizar las tareas en su entorno.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0a2ee528c8b38acbc18aa051dd84a7634b66713b
ms.sourcegitcommit: 2687489aa409a050dcacd67f17b3dad3ab7f1804
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/15/2019
ms.locfileid: "54316599"
---
# <a name="manage-task-sequences-to-automate-tasks-in-configuration-manager"></a>Administración de secuencias de tareas para automatizar tareas en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use secuencias de tareas para automatizar los pasos en su entorno de Configuration Manager. Estos pasos pueden implementar una imagen de sistema operativo en un equipo de destino, compilar y capturar una imagen de sistema operativo a partir de un conjunto de archivos de instalación de sistema operativo, y capturar y restaurar la información de estado de usuario. Las secuencias de tareas se encuentran en la consola de Configuration Manager. En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**. El nodo **Secuencia de tareas**, incluidas todas las subcarpetas creadas, se replica en toda la jerarquía de Configuration Manager. Para obtener información, consulte [Planning considerations for automating tasks](/sccm/osd/plan-design/planning-considerations-for-automating-tasks) (Consideraciones de planeación para la automatización de tareas).  



##  <a name="BKMK_CreateTaskSequence"></a> Crear secuencias de tareas  

 Cree secuencias de tareas con el Asistente para crear secuencia de tareas. Este asistente puede crear los siguientes tipos de secuencias de tareas:  

|Tipo de secuencia de tareas|Más información|  
|------------------------|----------------------|  
|[Secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md)|Este tipo de secuencia de tareas crea los pasos para instalar un sistema operativo. También incluye opciones para migrar datos de usuario, incluir actualizaciones de software e instalar aplicaciones.|  
|[Secuencia de tareas para actualizar un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md)|Este tipo de secuencia de tareas crea los pasos para actualizar un sistema operativo. También incluye opciones para incluir actualizaciones de software e instalar aplicaciones.|  
|[Secuencia de tareas para capturar un sistema operativo](create-a-task-sequence-to-capture-an-operating-system.md)|Este tipo de secuencia de tareas crea los pasos para compilar y capturar un sistema operativo desde un equipo de referencia. Puede incluir actualizaciones de software e instalar aplicaciones en el equipo de referencia antes de capturar la imagen.|  
|[Secuencia de tareas para capturar y restaurar el estado de usuario](create-a-task-sequence-to-capture-and-restore-user-state.md)|En esta secuencia de tareas se indican las etapas que se deben agregar a una secuencia de tareas existente para capturar y restaurar los datos de estado de usuario.|  
|[Secuencia de tareas personalizada](create-a-custom-task-sequence.md)|Este tipo de secuencia de tareas no agrega ninguna etapa a la secuencia de tareas. Después de crear esta secuencia de tareas, modifíquela y agregue pasos.|  



## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Volver a la página anterior cuando se produce un error en una secuencia de tareas

Puede volver a la página anterior cuando ejecuta una secuencia de tareas y se produce un error. En versiones anteriores de Configuration Manager, tenía que reiniciar la secuencia de tareas si se producía un error. Use el botón **Anterior** en los siguientes escenarios:

- Cuando un equipo se inicia en Windows PE, el cuadro de diálogo de arranque de la secuencia de tareas puede mostrarse antes de que la secuencia de tareas esté disponible. Cuando hace clic en Siguiente en este escenario, la página final de la secuencia de tareas se muestra con un mensaje de que no existe ninguna secuencia de tareas disponible. Ahora, puede hacer clic en **Anterior** para buscar de nuevo secuencias de tareas disponibles. Puede repetir este proceso hasta que la secuencia de tareas esté disponible.  

- Cuando ejecuta una secuencia de tareas, pero los paquetes de contenido dependientes todavía no están disponibles en los puntos de distribución, se produce un error en la secuencia de tareas. Si aún no se ha distribuido el contenido que faltan, distribúyalo ahora. También puede esperar a que el contenido esté disponible en los puntos de distribución. Después, haga clic en **Anterior** para que la secuencia de tareas busque de nuevo el contenido.



##  <a name="BKMK_ModifyTaskSequence"></a> Editar una secuencia de tareas  

 Modifique una secuencia de tareas, agregue o quite pasos, agregue o quite grupos, o cambie el orden de los pasos. Use el procedimiento siguiente para modificar una secuencia de tareas existente:  

> [!IMPORTANT]  
>  Cuando edite una secuencia de tareas creada mediante el Asistente para crear secuencia de tareas, el nombre del paso puede ser la acción o el tipo de paso. Por ejemplo, puede ver un paso con el nombre "Disco de partición 0", que es la acción de un paso de tipo [Formatear y crear particiones en el disco](/sccm/osd/understand/task-sequence-steps#BKMK_FormatandPartitionDisk). Todos los pasos de la secuencia de tareas se documentan por su tipo, no necesariamente por el nombre del paso que se muestra en el editor.  

#### <a name="to-edit-a-task-sequence"></a>Para editar una secuencia de tareas  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que desee editar.  

4.  En la pestaña **Inicio** , en el grupo **Secuencia de tareas** , haga clic en **Editar**y, a continuación, realice alguna de las operaciones siguientes:  

    -   Para agregar un paso de secuencia de tareas, haga clic en **Agregar**, seleccione el tipo de paso y haga clic en el paso que quiere agregar. Por ejemplo, para agregar el paso de ejecución de línea de comandos haga clic en **Agregar**, seleccione **General**y, a continuación, haga clic en **Ejecutar línea de comandos**.  

    -   Para agregar un grupo a la secuencia de tareas, haga clic en **Agregar**y, a continuación, haga clic en **Nuevo grupo**. Después de agregar un grupo, puede agregar pasos al grupo.  

    -   Para cambiar el orden de los pasos y los grupos de la secuencia de tareas, seleccione el paso o grupo que quiera reordenar y use los iconos **Subir elemento** o **Bajar elemento**. Solo puede mover un paso o un grupo cada vez.  

    -   Para quitar un paso o un grupo, seleccione el paso o el grupo y haga clic en **Quitar**.  

5.  Haga clic en **Aceptar** para guardar los cambios.  


 Para obtener una lista de las etapas de secuencia de tareas disponibles, consulte [Pasos de la secuencia de tareas](/sccm/osd/understand/task-sequence-steps).  



## <a name="bkmk_prop-general"></a> Configuración de las propiedades del Centro de software

 Siga este procedimiento para configurar los detalles de la secuencia de tareas que aparece en el Centro de software. Estos detalles son meramente informativos.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. Seleccione la secuencia de tareas que se va editar y haga clic en **Propiedades**.  

3. En la pestaña **General**, está disponible la siguiente configuración para el Centro de software:  

   - **Es necesario reiniciar**: permite al usuario saber si es necesario reiniciar durante la instalación.  

   - **Tamaño de la descarga (MB)**: especifica cuántos megabytes se muestran en el Centro de software para la secuencia de tareas.  

   - **Tiempo de ejecución estimado (minutos)**: especifica el tiempo de ejecución estimado en minutos que se muestra en el Centro de software para la secuencia de tareas.  



## <a name="bkmk_prop-advanced"></a> Configuración de los ajustes de la secuencia de tareas avanzada

 Use el procedimiento siguiente para configurar el comportamiento de la secuencia de tareas en el cliente de Configuration Manager.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. Seleccione la secuencia de tareas que se va editar y haga clic en **Propiedades**.  

3. En la pestaña **Avanzadas** están disponibles las opciones siguientes:  

   - **Ejecutar otro programa primero**: seleccione esta opción para ejecutar un programa en otro paquete antes de ejecutar la secuencia de tareas. De forma predeterminada, esta casilla de verificación está desactivada. No es necesario implementar por separado el programa especificado para que se ejecute primero.  

     > [!IMPORTANT]
     >   Esta configuración solo se aplica a las secuencias de tareas que se ejecutan en el sistema operativo completo. Si inicia la secuencia de tareas mediante PXE o medios de arranque, Configuration Manager ignora este ajuste.  

     - **Paquete**: busque el paquete que contiene el programa que se va a ejecutar antes de esta secuencia de tareas.  

     - **Programa**: seleccione el programa que se va a ejecutar antes de esta secuencia de tareas.  

       > [!NOTE]    
       > Si el programa seleccionado no se ejecuta en un cliente, la secuencia de tareas tampoco se ejecuta. Si el programa seleccionado se ejecuta correctamente, no se ejecutará de nuevo, incluso aunque la secuencia de tareas se vuelva a ejecutar en el mismo cliente.  
   
   - **Suprimir notificaciones de secuencia de tareas**: Seleccione esta opción para ocultar la notificación del sistema "Hay nuevo software disponible". En el área de notificaciones se seguirá mostrando el icono de "nuevo software" del Centro de software. De forma predeterminada, esta casilla de verificación está desactivada.  
 
   - **Deshabilitar esta secuencia de tareas en los equipos en los que se implementó**: si selecciona esta opción, Configuration Manager deshabilita temporalmente todas las implementaciones que contienen esta secuencia de tareas. También quita la secuencia de tareas de la lista de implementaciones disponibles para su ejecución. La secuencia de tareas no se ejecuta hasta que la habilite. De forma predeterminada, esta opción está deshabilitada.  

   - **Tiempo de ejecución máximo permitido**: especifica el tiempo máximo (en minutos) previsto para la ejecución de la secuencia de tareas en el equipo de destino. Use un número entero igual o mayor que cero. De forma predeterminada, este valor es de 120 minutos.  

       > [!IMPORTANT]    
       > Si está usando ventanas de mantenimiento para la recopilación en las que implementa esta secuencia de tareas, puede producirse un conflicto si el **Tiempo de ejecución máximo permitido** es mayor que la ventana de mantenimiento programada. Si el tiempo de ejecución máximo se establece en **0**, la secuencia de tareas se inicia durante la ventana de mantenimiento. Sigue ejecutándose hasta que se complete o se produzca un error después de cerrar la ventana de mantenimiento. Como resultado, las secuencias de tareas con un tiempo de ejecución máximo establecido en **0** podrían ejecutarse después del final de sus ventanas de mantenimiento. Si establece el tiempo de ejecución máximo en un periodo específico (diferente de 0) que supera la duración de cualquiera de las ventanas de mantenimiento disponibles, la secuencia de tareas no se ejecutará. Para obtener más información, consulte [How to Use Maintenance Windows in Configuration Manager](/sccm/core/clients/manage/collections/use-maintenance-windows) (Uso de ventanas de mantenimiento en Configuration Manager).  
 
      Si el valor se establece en **0**, Configuration Manager evalúa el tiempo de ejecución máximo permitido en **12** horas (720 minutos) para el progreso de la supervisión. Aun así, la secuencia de tareas se iniciará siempre y cuando la duración de la cuenta atrás no supere el valor de la ventana de mantenimiento.  

      > [!NOTE]    
      > Cuando alcanza el tiempo de ejecución máximo, si ha configurado la opción de **Ejecutar con derechos administrativos** y no establece la opción de **Permitir a los usuarios interactuar con este programa**, Configuration Manager detiene la secuencia de tareas. Si no se detiene la secuencia de tareas, Configuration Manager detiene la supervisión de la secuencia de tareas una vez que se alcanza el tiempo de ejecución máximo permitido.  

   - **Usar una imagen de arranque**: use la imagen de arranque seleccionada cuando se ejecuta la secuencia de tareas. Haga clic en **Examinar** para seleccionar otra imagen de arranque. Desactive esta opción para deshabilitar el uso de la imagen de arranque seleccionada cuando se ejecuta la secuencia de tareas.  

   - **This task sequence can run on any platform** (Esta secuencia de tareas puede ejecutarse en cualquier plataforma): si selecciona esta opción, Configuration Manager no comprueba el tipo de plataforma del equipo de destino cuando se implementa la secuencia de tareas. Esta opción está seleccionada de forma predeterminada.  

   - **This task sequence can only run on the specified client platforms** (Esta secuencia de tareas solo puede ejecutarse en las plataformas cliente especificadas): Esta opción especifica los procesadores, las versiones de sistema operativo y los Service Pack en los que se puede ejecutar esta secuencia de tareas. Cuando seleccione esta opción, seleccione al menos una plataforma de la lista. De forma predeterminada, no hay ninguna plataforma seleccionada. Configuration Manager usa esta información cuando se evalúa qué equipos de destino de una recopilación reciben la secuencia de tareas implementada.  

       > [!NOTE]    
       > Cuando se ejecuta una secuencia de tareas desde PXE o medios de arranque, Configuration Manager ignora esta opción. La secuencia de tareas se ejecuta como si estuviera seleccionada la opción **Este programa puede ejecutarse en cualquier plataforma**.  



## <a name="configure-high-impact-task-sequence-settings"></a>Configuración de los ajustes de la secuencia de tareas de gran impacto

 Configure una secuencia de tareas como de gran impacto y personalice los mensajes que reciben los usuarios cuando ejecutan la secuencia de tareas.


### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Establecer una secuencia de tareas como una secuencia de tareas de alto impacto

 Siga este procedimiento para establecer una secuencia de tareas como de alto impacto.

> [!NOTE]    
> Cualquier secuencia de tareas que cumpla determinadas condiciones se define automáticamente como de alto impacto. Para obtener más información, vea [Configuración para administrar implementaciones de alto riesgo](/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. Seleccione la secuencia de tareas que se va editar y haga clic en **Propiedades**.  

3. En la pestaña **Notificación de usuario**, seleccione **Es una secuencia de tareas de alto impacto**.  


### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Crear una notificación personalizada para implementaciones de alto riesgo

 Utilice el procedimiento siguiente para crear una notificación personalizada para las implementaciones de gran impacto.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. Seleccione la secuencia de tareas que se va editar y haga clic en **Propiedades**.  

3. En la pestaña **Notificación de usuario**, seleccione **Usar texto personalizado**.  

   > [!NOTE]
   >  Solo puede establecer el texto de la notificación del usuario cuando seleccione la opción **Es una secuencia de tareas de alto impacto**.  

4. Configure las siguientes opciones:  

    > [!Note]  
    > Cada cuadro de texto tiene un límite máximo de 255 caracteres.  

    **Texto del título de la notificación de usuario**: especifica el texto de color azul que aparece en la notificación de usuario del Centro de software. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene: "Confirm you want to upgrade the operating system on this computer" (Confirme que quiere actualizar el sistema operativo en este equipo).  

    **Texto del mensaje de notificación de usuario**: hay tres cuadros de texto que proporcionan el cuerpo de la notificación personalizada. Todos los cuadros de texto requieren que agregue texto.  

    - Cuadro de texto 1: especifica el cuerpo principal del texto, que normalmente contiene instrucciones para el usuario. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene: "Upgrading the operating system takes time and your computer might restart several times" (La actualización del sistema operativo lleva un tiempo y es posible que el equipo se reinicie varias veces).  

    - Cuadro de texto 2: especifica el texto en negrita debajo del cuerpo de texto principal. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene: "This in-place upgrade installs the new operating system and automatically migrates your apps, data, and settings" (Esta actualización en contexto instala el nuevo sistema operativo y migra automáticamente sus aplicaciones, datos y configuración).  

    - Cuadro de texto 3: especifica la última línea de texto debajo del texto en negrita. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene: "Click Install to begin" (Haga clic en Instalar para comenzar). De lo contrario, haga clic en Cancelar".   

#### <a name="example"></a>Ejemplo
Supongamos que configura la siguiente notificación personalizada en las propiedades.

![Pestaña de notificación de usuario personalizada de las propiedades de la secuencia de tareas](../media/user-notification.png)

Se mostrará el siguiente mensaje de notificación cuando el usuario final abra la instalación desde el Centro de software.

![Notificación de la secuencia de tareas personalizada que se muestra al usuario final desde el Centro de software](../media/user-notification-enduser.png)



##  <a name="BKMK_DistributeTS"></a> Distribuir contenido al que hace referencia una secuencia de tareas  

 Antes de que los clientes ejecuten una secuencia de tareas que haga referencia a contenido, distribuya dicho contenido a los puntos de distribución. En cualquier momento, puede seleccionar la secuencia de tareas y distribuir su contenido para crear una nueva lista de paquetes de referencia para su distribución. Si realiza cambios en la secuencia de tareas con contenido actualizado, redistribuya el contenido antes de que esté disponible para los clientes. Utilice el siguiente procedimiento para distribuir el contenido al que hace referencia una secuencia de tareas.  

#### <a name="to-distribute-referenced-content-to-distribution-points"></a>Para distribuir el contenido al que se hace referencia a los puntos de distribución  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que desee distribuir.  

4.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Distribuir contenido** para iniciar el Asistente para distribuir contenido.  

5.  En la página **General** , compruebe que esté seleccionada la secuencia de tareas correcta para la distribución. A continuación, haga clic en **Siguiente**.  

6.  En la página **Contenido** , compruebe el contenido que se va a distribuir, como la imagen de arranque a la que hace referencia la secuencia de tareas, y, a continuación, haga clic en **Siguiente**.  

7.  En la página **Destino del contenido**, especifique las recopilaciones, el punto de distribución o el grupo de puntos de distribución donde quiera distribuir el contenido de la secuencia de tareas. A continuación, haga clic en **Siguiente**.  

    > [!IMPORTANT]  
    >  Si la secuencia de tareas seleccionada hace referencia a contenido que ya se distribuyó a un punto de distribución específico, el asistente no muestra ese punto de distribución.  

8.  Complete el asistente.  


 También puede preconfigurar el contenido al que se hace referencia en la secuencia de tareas. Configuration Manager crea un archivo de contenido preconfigurado comprimido que contiene los archivos, las dependencias asociadas y los metadatos asociados del contenido que se selecciona. A continuación puede importar manualmente el contenido en un servidor de sitio, un sitio secundario o un punto de distribución. Para más información sobre cómo preconfigurar archivos de contenido, consulte [Preconfigurar el contenido](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  



##  <a name="BKMK_DeployTS"></a> Implementar una secuencia de tareas  

 Utilice el siguiente procedimiento para implementar una secuencia de tareas en los equipos de una recopilación.  

> [!WARNING]  
>  Puede administrar el comportamiento de las implementaciones de secuencias de tareas de alto riesgo. Una implementación de alto riesgo es una implementación que se instala automáticamente y puede provocar resultados no deseados. Por ejemplo, una secuencia de tareas con el propósito **Requerido** que implementa un sistema operativo se considera una implementación de alto riesgo. Para obtener más información, consulte [Settings to manage high-risk deployments](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments) (Configuración para administrar implementaciones de alto riesgo).  

> [!NOTE]  
>  Los mensajes de estado para la implementación de la secuencia de tareas se muestran en la ventana Mensaje en un sitio primario, pero no se muestran en un sitio de administración central.  

#### <a name="to-deploy-a-task-sequence"></a>Para implementar una secuencia de tareas    

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2. En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3. En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que desee implementar.  

4. En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.  

   > [!NOTE]  
   >  Si **Implementar** no está disponible, la secuencia de tareas tiene una referencia que no es válida. Corrija la referencia y, a continuación, intente implementar la secuencia de tareas de nuevo.  

5. On the **General** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

   - **Secuencia de tareas**: especifique la secuencia de tareas que se va a implementar. De forma predeterminada, este cuadro muestra la secuencia de tareas seleccionada.  

   - **Colección**: seleccione la colección que contiene los equipos que ejecutan la secuencia de tareas.  

      No implemente una secuencia de tareas que instale un sistema operativo en recopilaciones inapropiadas, como la recopilación de todos los servidores del centro de datos. Asegúrese de que la recopilación que seleccione contiene solo los equipos que desea que ejecuten la secuencia de tareas.  

     > [!NOTE]
     >  Al realizar una implementación de alto riesgo, como un sistema operativo, en la ventana **Seleccionar recopilación** solo se muestran las recopilaciones personalizadas que cumplen con la configuración de comprobación de implementación que está configurada en las propiedades del sitio. Las implementaciones de alto riesgo siempre se limitan a las recopilaciones personalizadas, las recopilaciones que cree y la recopilación integrada **Equipos desconocidos** . Si crea una implementación de alto riesgo, no podrá seleccionar una recopilación integrada como **Todos los sistemas**. Desactive **Ocultar recopilaciones con un número de miembros superior a la configuración de tamaño mínimo del sitio** para ver todas las recopilaciones personalizadas que contienen menos clientes que el tamaño máximo configurado. Para obtener más información, consulte [Settings to manage high-risk deployments](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments) (Configuración para administrar implementaciones de alto riesgo).  
     > 
     >  La configuración de comprobación de implementación se basa en la pertenencia actual de la recopilación. Después de implementar la secuencia de tareas, Configuration Manager no vuelve a evaluar la pertenencia a la recopilación para la configuración de implementación de alto riesgo.  
     > 
     >  Por ejemplo, supongamos que establece el **Tamaño predeterminado** en 100 y el **Tamaño máximo** en 1000. Al crear una implementación de alto riesgo, en la ventana **Seleccionar recopilación** solo se muestran las recopilaciones que contienen menos de 100 clientes. Si desactiva la opción **Hide collections with a member count greater than the site's minimum size configuration** (Ocultar recopilaciones con un número de miembros superior a la configuración de tamaño mínimo del sitio), en la ventana se muestran las recopilaciones que contienen menos de 1000 clientes.  
     > 
     >  Al seleccionar una recopilación que contiene un rol de sitio, se aplica el comportamiento siguiente:  
     > 
     > - Si la recopilación contiene un servidor de sistema de sitio y ha configurado los valores de comprobación de implementación de modo que bloqueen las recopilaciones con servidores de sistema de sitio, se producirá un error. No podrá seguir creando la implementación.  
     >   -   Si se aplica uno de los siguientes criterios, el Asistente para implementar software muestra una advertencia de alto riesgo. Para continuar, debe aceptar que se cree una implementación de alto riesgo. El sitio genera un mensaje de estado de auditoría.  
     >   - Si la recopilación contiene un servidor de sistema de sitio y ha configurado los valores de comprobación de implementación de modo que adviertan sobre las recopilaciones con servidores de sistema de sitio
     >   - Si la recopilación supera el valor de tamaño predeterminado
     >   - Si la recopilación contiene un servidor  

   - **Usar grupos de puntos de distribución predeterminados asociados a esta colección**: almacene el contenido de la secuencia de tareas en el grupo de puntos de distribución predeterminado de la colección. Si no ha asociado la colección seleccionada a un grupo de puntos de distribución, esta opción estará atenuada.  

   - **Distribuir contenido automáticamente para las dependencias**: si alguno de los contenidos a los que se hace referencia tiene dependencias, el sitio también envía contenido dependiente a los puntos de distribución.  

   - **Descargar contenido previamente para esta secuencia de tareas**: Para obtener más información, vea [Configuración del contenido de la caché previa](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

   - **Seleccionar plantilla de implementación**: a partir de la versión 1802 de Configuration Manager, <!--1357391--> puede guardar y especificar una plantilla de implementación para una secuencia de tareas.     

        > [!IMPORTANT]  
        > En Configuration Manager versión 1802, algunos elementos no se guardan en la plantilla.  <!--510610--> Asegúrese de que estos elementos se aplican al ejecutar el asistente para la implementación:  
        > - Instalación de software 
        > - Programación 
        > - Descarga previa de contenido
 
   - **Comentarios (opcional)**: especifique información adicional que describa esta implementación de la secuencia de tareas.  

6. En la página **Configuración de implementación** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

   - **Finalidad**: en la lista desplegable, elija una de las siguientes opciones:  

     -   **Disponible**: el usuario ve la secuencia de tareas en el Centro de software y la puede instalar a petición.  

     -   **Obligatoria**: Configuration Manager ejecuta la secuencia de tareas automáticamente de acuerdo con la programación configurada. Si la secuencia de tareas no está oculta, el usuario todavía puede seguir su estado de implementación. También puede usar el Centro de software para instalar la secuencia de tareas antes de la fecha límite.  

     > [!NOTE]
     >  Si varios usuarios inician sesión en el dispositivo, es posible que las implementaciones de paquete y secuencia de tareas no aparezcan en el centro de Software.  

   - **Estar disponible para**: especifique si la secuencia de tareas está disponible para uno de los tipos siguientes:  
     - Solo clientes de Configuration Manager  
     - Clientes de Configuration Manager, medios y PXE  
     - Solo medios y PXE  
     - Sólo medios y PXE (ocultos)  

     > [!IMPORTANT]  
     >  Use la opción **Sólo medios y PXE (ocultos)** para implementaciones automatizadas de secuencia de tareas. Para que el equipo arranque automáticamente en la implementación sin interacción del usuario, seleccione **Permitir la implementación desatendida de sistema operativo** y configure la variable **SMSTSPreferredAdvertID** como parte del medio. Para obtener más información sobre las variables de secuencia de tareas para esta acción, consulte [Task sequence variables](/sccm/osd/understand/task-sequence-variables#SMSTSPreferredAdvertID) (Variables de secuencia de tareas).  

   - **Enviar paquetes de reactivación**: si la implementación es **Obligatoria** y selecciona esta opción, el sitio envía un paquete de reactivación a los equipos antes de que el cliente ejecute la implementación. Este paquete reactiva el equipo en suspensión a la hora límite de instalación. Para poder usar esta opción, los equipos y las redes deben configurarse para Wake On LAN. Para obtener más información, vea [Planear la reactivación de clientes](/sccm/core/clients/deploy/plan/plan-wake-up-clients).  

   - **Permitir a los clientes de una conexión a Internet de uso medido descargar contenido una vez cumplida la fecha límite de instalación, lo cual podría suponer costos adicionales**: esta opción solo está disponible para las implementaciones **obligatorias**. Si tiene una secuencia de tareas personalizada que instala una aplicación pero no implementa un sistema operativo, puede especificar si permite a los clientes descargar contenido una vez cumplida la fecha límite de la instalación cuando utilizan una conexión a Internet de uso medido. En ocasiones, los proveedores de acceso a Internet cobran según la cantidad de datos que use cuando se utiliza una conexión de uso medido.  

     > [!NOTE]  
     >  Aunque el uso de una conexión a Internet de uso medido podría funcionar para secuencias de tareas que no implementan un sistema operativo, no se admite este tipo de conexión para este propósito.  

7. En la página **Programación** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

   > [!IMPORTANT]  
   >  Cuando un cliente de Windows PE se inicia desde PXE o desde un medio de arranque, el cliente no evalúa las programaciones de implementación. Estas programaciones incluyen las horas límite, de inicio y de expiración. Configure programaciones en implementaciones únicamente en clientes que se inicien desde el sistema operativo Windows completo. Considere el uso de otros métodos (como periodos de mantenimiento) para controlar las secuencias de tareas activas implementadas en clientes que se inician desde Windows PE.  

   -   **Programar cuándo estará disponible esta implementación**: Especifique la fecha y la hora en las que la secuencia de tareas estará disponible para su ejecución en el equipo de destino. Cuando seleccione la casilla **UTC**, la secuencia de tareas estará disponible en varios equipos al mismo tiempo. En caso contrario, la implementación estará disponible en horas diferentes, según la hora local en cada equipo.  

        Si la hora de inicio es anterior a la hora requerida, el cliente descarga el contenido de la secuencia de tareas a la hora de inicio.  

   -   **Programar cuándo expirará esta implementación**: Especifique la fecha y hora de expiración de la secuencia de tareas en el equipo de destino. Cuando seleccione la casilla **UTC**, la secuencia de tareas expira en varios equipos de destino al mismo tiempo. En caso contrario, la implementación expira en horas diferentes, según la hora local en cada equipo.  

   -   **Programación de asignación:**: para una implementación **Obligatoria**, especifique cuándo ejecuta el cliente la secuencia de tareas. Puede agregar varias programaciones. La programación de asignación puede tener una de las siguientes configuraciones:   
       - Una fecha y hora específicas  
       - Patrón de periodicidad mensual, semanal o personalizado  
       - En cuanto sea posible  
       - Eventos de inicio o cierre de sesión  

       > [!NOTE]  
       >  Si programa una hora de inicio para una implementación obligatoria que sea anterior a la fecha y hora en que la secuencia de tareas está disponible, el cliente de Configuration Manager descarga el contenido a la hora de inicio asignada. Este comportamiento se produce incluso si ha programado la secuencia de tareas para que esté disponible en un momento posterior.<!--SCCMDocs issue 777-->  

   -   **Comportamiento de reejecución**: especifique cuándo se vuelve a ejecutar la secuencia de tareas. Seleccione una de las siguientes opciones:  

       -   **No volver a ejecutar nunca el programa implementado**: si el cliente ya ha ejecutado la secuencia de tareas, no se vuelve a ejecutar. La secuencia de tareas no se vuelve a ejecutar, aunque no se completara en su primera ejecución o los archivos hayan cambiado.  

       -   **Volver a ejecutar siempre el programa**: la secuencia de tareas siempre se vuelve a ejecutar en el cliente cuando se programa la implementación. Se vuelve a ejecutar incluso si la secuencia de tareas ya se ha ejecutado correctamente. Esta opción es útil cuando se usan implementaciones periódicas en las que la secuencia de tareas se actualiza regularmente.  

           > [!IMPORTANT]  
           >  Esta opción está seleccionada de forma predeterminada. Sin embargo, no surte ningún efecto hasta que se asigne una implementación obligatoria. Un usuario siempre puede volver a ejecutar las implementaciones disponibles.  

       -   **Volver a ejecutar en caso de error del intento anterior**: la secuencia de tareas se vuelve a ejecutar cuando se programa la implementación, solo si anteriormente no se pudo ejecutar. Esta opción es útil para las implementaciones obligatorias. Si el último intento de ejecución no se completó correctamente, las implementaciones reintentarán automáticamente su ejecución de acuerdo a la programación de asignación.  

       -   **Volver a ejecutar si el intento anterior se realizó correctamente**: la secuencia de tareas se vuelve a ejecutar solo si se ejecutó antes correctamente en el cliente. Esta configuración es útil cuando se utiliza en implementaciones periódicas en las que la secuencia de tareas se actualiza periódicamente, y cada actualización requiere que la actualización anterior está instalada correctamente.  

       > [!NOTE]  
       >  Un usuario puede volver a ejecutar una implementación de secuencia de tareas disponible. Antes de implementar una secuencia de tareas disponible en un entorno de producción, pruebe en primer lugar qué sucede si un usuario vuelve a ejecutar la secuencia de tareas varias veces.  

8. En la página **Experiencia del usuario** , especifique la siguiente información y, a continuación, haga clic en **Siguiente**.  

   -   **Permitir que los usuarios ejecuten el programa independientemente de las asignaciones**: especifique si un usuario puede ejecutar una implementación obligatoria fuera de la programación de asignación. Esta opción siempre está habilitada para las implementaciones disponibles.   

   -   **Mostrar progreso de la secuencia de tareas**: especifique si el cliente de Configuration Manager debe mostrar el progreso de la secuencia de tareas.  

   -   **Instalación de software**: especifique si el usuario puede instalar software fuera de una ventana de mantenimiento configurada después de la hora programada.  

   -   **Reinicio del sistema (si es necesario para completar la instalación)**: especifique si se permite al usuario reiniciar el equipo tras una instalación de software fuera de una ventana de mantenimiento configurada tras la hora de asignación.  

   - **Tratamiento de filtros de escritura para dispositivos de Windows Embedded**: esta opción controla el comportamiento de instalación en los dispositivos Windows Embedded habilitados con un filtro de escritura. Elija esta opción para que los cambios se confirmen en la fecha límite de instalación o durante una ventana de mantenimiento. Al seleccionar esta opción, se necesita un reinicio y los cambios persisten en el dispositivo. De lo contrario, la aplicación se instala en la superposición temporal y se confirma más tarde. Cuando implemente una secuencia de tareas en un dispositivo de Windows Embedded, asegúrese de que el dispositivo es miembro de una recopilación que tenga una ventana de mantenimiento configurada.  

   -   **Permitir que la secuencia de tareas se ejecute para el cliente en Internet**: especifique si la secuencia de tareas se puede ejecutar en un cliente basado en Internet. Las operaciones que instalan software, como un sistema operativo, no son compatibles con esta configuración. Use esta opción solo para secuencias de tareas basadas en scripts que realizan operaciones en el sistema operativo estándar.  

        - A partir de la versión 1802, esta configuración se admite para implementaciones de una secuencia de tareas de actualización local de Windows 10 en clientes basados en Internet a través de Cloud Management Gateway. Para obtener más información, vea [Implementar una actualización local de Windows 10 a través de CMG](#deploy-windows-10-in-place-upgrade-via-cmg).    

9. En la página **Alertas** , especifique la configuración de alertas que desea establecer para esta implementación de secuencia de tareas y, a continuación, haga clic en **Siguiente**.  

10. En la página **Puntos de distribución** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    -   **Opciones de implementación**: especifique una de las siguientes opciones:  

        > [!NOTE]  
        >  Si usa multidifusión para implementar un sistema operativo, descargue el contenido cuando se necesite o antes de que se ejecute la secuencia de tareas.  

        - **Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas**: especifique que los clientes descarguen el contenido desde el punto de distribución como necesite la secuencia de tareas. El cliente inicia la secuencia de tareas. Cuando un paso de una secuencia de tareas requiera contenido, este se descarga antes de que se ejecute el paso.  

        - **Descargar todo el contenido localmente antes de iniciar la secuencia de tareas**: especifique que los clientes descarguen todo el contenido desde el punto de distribución antes de que se ejecute la secuencia de tareas. Si ha hecho que la secuencia de tareas esté disponible para implementaciones del medio de arranque y PXE en la página **Configuración de implementación**, esta opción no se muestra.  

        - **Acceder al contenido directamente desde un punto de distribución cuando sea necesario mediante la ejecución de la secuencia de tareas**: Especificar que los clientes ejecuten el contenido desde el punto de distribución. Esta opción está disponible solo cuando todos los paquetes asociados con la secuencia de tareas están habilitados para utilizar un recurso compartido de paquete en el punto de distribución. Para habilitar el contenido de tal modo que utilice un recurso compartido de paquete, consulte la pestaña **Acceso a datos** en las **Propiedades** de cada paquete.  

    -   **Cuando no haya disponible ningún punto de distribución local, usar un punto de distribución remoto**: especifique si los clientes pueden usar puntos de distribución de un grupo de límites vecino para descargar el contenido necesario para la secuencia de tareas.  

    - **Permitir que los clientes usen puntos de distribución del grupo de límite del sitio predeterminado**: especifique si los clientes deben descargar contenido desde un punto de distribución en el grupo de límites predeterminados del sitio, cuando el contenido no está disponible desde un punto de distribución en el grupo actual o en los grupos de límites vecinos.  

        > [!Note]  
        > A partir de la versión 1810, cuando un dispositivo ejecuta una secuencia de tareas y necesita adquirir contenido, usa los comportamientos de grupos de límites similares al cliente de Configuration Manager. Para obtener más información, vea [Task sequence support for boundary groups](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgr-osd) (Compatibilidad de la secuencia de tareas con grupos de límites).<!--1359025-->  

11. A partir de Configuration Manager 1802, en la pestaña **Resumen**, haga clic en **Save As Template** (Guardar como plantilla) si quiere guardar la configuración para volver a usarla. Asigne un nombre a la plantilla y seleccione la configuración que quiere guardar.  

12. Complete el asistente.  


### <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>Implementar una actualización local de Windows 10 a través de CMG
<!-- 1357149 -->

A partir de la versión 1802, la secuencia de tareas de actualización local de Windows 10 admite la implementación en los clientes basados en Internet que se administran a través de [Cloud Management Gateway](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG). Esta función permite a los usuarios remotos actualizar con mayor facilidad a Windows 10 sin necesidad de conectarse a la intranet. 

Asegúrese de que todo el contenido al que hace referencia la secuencia de tareas de actualización en contexto se distribuye a un [punto de distribución de nube](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). En caso contrario, los dispositivos no podrán ejecutar la secuencia de tareas.

Cuando se implementa una secuencia de tareas de actualización, utilice la siguiente configuración:

- **Permitir que la secuencia de tareas se ejecute para el cliente en Internet**, en la pestaña Experiencia del usuario de la implementación.  

- **Descargar todo el contenido localmente antes de iniciar la secuencia de tareas** en la página Puntos de distribución de la implementación. Otras opciones como **Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas** no funcionan en este escenario. El motor de la secuencia de tareas no puede obtener contenido actualmente desde un punto de distribución de nube. El cliente de Configuration Manager debe descargar el contenido desde el punto de distribución de nube antes de iniciar la secuencia de tareas.  

- (*Opcional*) **Descargar contenido previamente para esta secuencia de tareas** en la pestaña General de la implementación. Para obtener más información, vea [Configuración del contenido de la caché previa](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  



##  <a name="BKMK_ExportImport"></a> Exportar e importar secuencias de tareas  

 Puede exportar e importar secuencias de tareas con o sin sus objetos relacionados. Este contenido al que se hace referencia incluye los siguientes objetos:  
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


### <a name="to-export-task-sequences"></a>Para exportar secuencias de tareas  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que va a exportar. Si selecciona más de una secuencia de tareas, se almacenan en un archivo de exportación.  

4.  En la pestaña **Inicio** , en el grupo **Secuencia de tareas** , haga clic en **Exportar** para iniciar el Asistente para exportar secuencias de tareas.  

5.  En la página **General** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    -   En el cuadro **Archivo** , especifique la ubicación y el nombre del archivo de exportación. Si escribe el nombre de archivo directamente, asegúrese de incluir la extensión .zip. Si examina el archivo de exportación, el asistente agrega automáticamente esta extensión de nombre de archivo.  

    -   Si no desea exportar las dependencias de secuencia de tareas, desactive la opción de **Exportar todas las dependencias de secuencia de tareas**. De forma predeterminada, el asistente explora todos los objetivos relacionados y los exporta con la secuencia de tareas. Estas dependencias incluyen secuencias de tareas para las aplicaciones.  

    -   Si no desea copiar el contenido del origen de paquete en la ubicación de exportación, desactive la opción de **Exportar todo el contenido de las secuencias de tareas y las dependencias seleccionadas**. Si activa esta opción, el Asistente para importar secuencia de tareas utiliza la ruta de acceso de importación como la nueva ubicación del origen de paquete.  

    -   En el cuadro **Comentarios del administrador** , agregue una descripción de la secuencia de tareas que va a exportar.  

6.  Complete el asistente.  


 El asistente crea los siguientes archivos de salida:  

-   Si no se exporta contenido: un archivo .zip.  

-   Si se exporta contenido: un archivo .zip y una carpeta *export*_files, donde *export* es el nombre del archivo .zip que contiene el contenido exportado.  


 Si incluye contenido cuando exporta una secuencia de tareas, asegúrese de que copia el archivo .zip y la carpeta *export*_files; de lo contrario, la importación no se completará correctamente.  


### <a name="to-import-task-sequences"></a>Para importar secuencias de tareas  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Importar secuencia de tareas** para iniciar el Asistente para importar secuencia de tareas.  

4.  En la página **General** , especifique el archivo .zip exportado y, a continuación, haga clic en **Siguiente**.  

5.  En la página **Contenido del archivo** , seleccione la acción que requiere para cada objeto que importa. En esta página se muestran todos los objetos que Configuration Manager ha encontrado para importar.  

    -   Si es la primera vez que se importó el objeto, seleccione **Crear nuevo**.  

    -   Si no es la primera vez que se importa, seleccione una de las siguientes acciones:  

        -   **Omitir duplicado** (predeterminado): esta acción no importa el objeto. En su lugar, el asistente vincula el objeto existente con la secuencia de tareas.  

        -   **Sobrescribir**: esta acción sobrescribe el objeto existente con el objeto importado. Para aplicaciones, puede agregar una revisión para actualizar la aplicación existente o crear una aplicación nueva.  

6.  Complete el asistente.  


 Después de importar la secuencia de tareas, edítela para especificar las contraseñas que se encontraban en la secuencia de tareas original. Por motivos de seguridad, no se exportan las contraseñas.  



##  <a name="BKMK_CreateTSVariables"></a> Crear variables de secuencia de tareas para equipos y recopilaciones  

 Puede definir variables de secuencia de tareas personalizadas para equipos y recopilaciones. Las variables que se definen para un determinado equipo se conocen como variables de secuencia de tareas por equipo. Las variables definidas para una determinada recopilación se conocen como variables de secuencia de tareas por recopilación. Si hay un conflicto, las variables por equipo tienen prioridad sobre las variables por recopilación. Este comportamiento significa que las variables de secuencia de tareas asignadas a un determinado equipo tienen automáticamente más prioridad que las variables asignadas a la recopilación que contiene el equipo.  

 Por ejemplo, el equipo XYZ es miembro de la recopilación ABC. Asigna MiVariable a la recopilación ABC con un valor de 1. También asigna MiVariable al equipo XYZ con un valor de 2. La variable que se asigna al equipo XYZ tiene mayor prioridad que la variable que se asigna a la recopilación ABC. Cuando se ejecuta una secuencia de tareas con esta variable en el equipo XYZ, MiVariable tiene un valor de 2. 

 Puede ocultar las variables por equipo y por recopilación para que no sean visibles en la consola de Configuration Manager. Cuando se usa la opción **No mostrar este valor en la consola de Configuration Manager**, el valor de la variable no se muestra en la consola. Aun así, la secuencia de tareas puede seguir usando la variable cuando se ejecute. Si ya no desea que estas variables estén ocultas, elimínelas en primer lugar. A continuación, vuelva a definir las variables sin seleccionar la opción para ocultarlas.  

 > [!WARNING]    
 > La opción **Do not display this value in the Configuration Manager console** (No mostrar este valor en la consola de Configuration Manager) solo se aplica a la consola de Configuration Manager. Los valores de las variables siguen apareciendo en el archivo de registro de la secuencia de tareas (SMSTS.LOG). 

 Puede administrar las variables por equipo en un sitio primario o en un sitio de administración central. Configuration Manager no admite más de 1000 variables asignadas en un equipo.  

> [!IMPORTANT]  
>  Cuando se usan variables por recopilación para secuencias de tareas, tenga en cuenta los comportamientos siguientes:  
>   
> - Los cambios en las recopilaciones siempre se replican por toda la jerarquía. Los cambios que realice en las variables de la recopilación se aplicarán no solo a los miembros del sitio actual, sino a todos los miembros de la recopilación en la jerarquía.  
>  
> - Cuando se elimina una recopilación también se eliminan las variables de secuencia de tareas que configuró para la recopilación.  


### <a name="to-create-task-sequence-variables-for-a-computer"></a>Para crear variables de secuencia de tareas para un equipo  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad**, seleccione el nodo **Dispositivos**.  

3.  Seleccione el equipo de destino y haga clic en **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades** , haga clic en la pestaña **Variables** .  

5.  Para cada variable que quiera crear, haga clic en el icono **Nuevo**. Especifique el **Nombre** y el **Valor** de la variable de la secuencia de tareas. Active la opción **No mostrar este valor en la consola de Configuration Manager** si desea ocultar la variable para que no esté visible en la consola de Configuration Manager.  

6.  Después de agregar todas las variables a las propiedades del equipo, haga clic en **Aceptar**.  


### <a name="to-create-task-sequence-variables-for-a-collection"></a>Para crear variables de secuencia de tareas para una recopilación  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad**, seleccione el nodo **Recopilaciones de dispositivos**. Seleccione la recopilación de destino y haga clic en **Propiedades**.  

3.  En el cuadro de diálogo **Propiedades** , haga clic en la pestaña **Variables de la recopilación** .  

4.  Para cada variable que quiera crear, haga clic en el icono **Nuevo**. Especifique el **Nombre** y el **Valor** de la variable de la secuencia de tareas. Active la opción **No mostrar este valor en la consola de Configuration Manager** si desea ocultar la variable para que no esté visible en la consola de Configuration Manager.  

5.  Si lo desea, especifique la prioridad de Configuration Manager que desea utilizar cuando se evalúen las variables de la secuencia de tareas.  

6.  Después de agregar todas las variables a las propiedades de la recopilación, haga clic en **Aceptar**.  



##  <a name="BKMK_AdditionalActionsTS"></a> Acciones adicionales para administrar secuencias de tareas  

 Puede administrar secuencias de tareas con acciones adicionales cuando se selecciona la secuencia de tareas.  

#### <a name="to-select-a-task-sequence-to-manage"></a>Para seleccionar la secuencia de tareas que desea administrar  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos** y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que desea administrar y, a continuación, seleccione una de las opciones disponibles.  


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
 Para obtener más información, vea [Deploy a task sequence](#BKMK_DeployTS).

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



## <a name="see-also"></a>Consulte también

[Escenarios para implementar sistemas operativos de empresa](scenarios-to-deploy-enterprise-operating-systems.md)
