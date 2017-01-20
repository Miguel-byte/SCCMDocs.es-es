---
title: Paquetes y programas | System Center Configuration Manager
description: Implementaciones compatibles con paquetes y programas o aplicaciones con System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
caps.latest.revision: 8
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5303edf0fe8a3e322b52cabd116b1877a14f8821


---
# <a name="packages-and-programs-in-system-center-configuration-manager"></a>Paquetes y programas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

System Center Configuration Manager sigue siendo compatible con los paquetes y programas usados en Configuration Manager 2007. Una implementación que utilice paquetes y programas podría ser más adecuada que una implementación que use una aplicación cuando se implementa algo de lo siguiente:  

- Quiere implementar aplicaciones en servidores Linux y UNIX.  
- Scripts que no instalan una aplicación en un equipo, como un script para desfragmentar la unidad de disco del equipo.  
- Secuencias de comandos "Uso único" que no es necesario supervisar de forma constante.  
- Scripts que se ejecutan según una programación periódica y no pueden usar evaluación global.  
  
Al migrar paquetes desde una versión anterior de Configuration Manager puede implementarlos en su jerarquía de Configuration Manager. Cuando la migración se haya completado, los paquetes aparecerán en el nodo **Paquetes** del área de trabajo **Biblioteca de software**. Puede modificar e implementar estos paquetes de la misma manera que mediante la distribución de software. El **Asistente para importar paquetes desde una definición** permanece en Configuration Manager para importar paquetes heredados. Los anuncios se convierten en implementaciones cuando se migran desde Configuration Manager 2007a una jerarquía de Configuration Manager.  
  
> [!NOTE]  
>  Puede usar el administrador de conversión de paquetes de Microsoft System Center Configuration Manager para convertir paquetes y programas en aplicaciones de Configuration Manager.  
>   
>  Para obtener más información, consulte [Administrador de conversión de paquetes de Configuration Manager](https://technet.microsoft.com/library/hh531519.aspx).  

Los paquetes pueden usar algunas características nuevas de Configuration Manager, incluidos los grupos de puntos de distribución y la supervisión. No se pueden distribuir aplicaciones de Microsoft Application Virtualization (App-V) mediante el uso de paquetes y programas en Configuration Manager. Para distribuir aplicaciones virtuales, deben crearse como aplicaciones de Configuration Manager.  

##  <a name="create-a-package-and-program"></a>Crear un paquete y programa  
 Utilice uno de estos procedimientos como ayuda para crear o importar paquetes y programas.  

### <a name="create-a-package-and-program-using-the-create-package-and-program-wizard"></a>Crear un paquete y un programa con el Asistente para crear paquetes y programas  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Paquetes**.  

3.  En el **Inicio** ficha el **crear** de grupo, haga clic en **Crear paquete**.  

4.  En la página **Paquete** del Asistente para crear paquetes y programas, especifique la siguiente información:  

    -   **Nombre**: especifique un nombre para el paquete con un máximo de 50 caracteres.  

    -   **Descripción**: opcionalmente, puede especificar una descripción para este paquete con un máximo de 128 caracteres.  

    -   **Fabricante**: opcionalmente, puede especificar un nombre de fabricante para ayudarle a identificar el paquete en la consola de Configuration Manager. Este nombre puede ser un máximo de 32 caracteres.  

    -   **Idioma**: opcionalmente, especifique la versión de idioma del paquete con un máximo de 32 caracteres.  

    -   **Versión**: opcionalmente, puede especificar un número de versión del paquete con un máximo de 32 caracteres.  

    -   **Este paquete contiene archivos de código fuente** -este valor indica si el paquete requiere que los archivos de origen esté presente en los dispositivos cliente. De forma predeterminada, esta casilla de verificación está desactivada y Configuration Manager no usa puntos de distribución para el paquete. Cuando se selecciona esta casilla, se utilizan puntos de distribución.  

    -   **Carpeta de origen**: si el paquete contiene archivos de origen, haga clic en **Examinar** para abrir el cuadro de diálogo **Establecer carpeta de origen** y especifique la ubicación de los archivos de origen del paquete.  

        > [!NOTE]  
        >  La cuenta de equipo del servidor de sitio debe tener permisos de acceso de lectura a la carpeta de origen que especifique.  

5.  En la página **Tipo de programa** del Asistente para crear paquetes y programas, seleccione el tipo de programa que quiere crear y luego haga clic en **Siguiente**. Puede crear un programa para un equipo o dispositivo, o puede omitir este paso y crear un programa más tarde.  

    > [!TIP]  
    >  Para crear un nuevo programa para un paquete existente, seleccione el paquete y, en la pestaña **Inicio** del grupo **Paquete**, haga clic en **Crear programa** para abrir el Asistente para crear programas.  

6.  Utilice uno de los siguientes procedimientos para crear un programa estándar o un dispositivo.  
  
    #### <a name="create-a-standard-program"></a>Crear un programa estándar  
  
  1.  En el **tipo de programa** página de la **crear un paquete y programa asistente**, seleccione **programa estándar**, y, a continuación, haga clic en **siguiente**.     2.  En la página **Programa estándar** , especifique la siguiente información:  

        -   **Nombre:** Especifique un nombre para el programa con un máximo de 50 caracteres.  

            > [!NOTE]  
            >  El nombre del programa debe ser único dentro de un paquete. Después de crear un programa, no puede modificar su nombre.  

        -   **Línea de comandos**: escriba la línea de comandos que se usará para iniciar este programa o haga clic en **Examinar** para ir a la ubicación del archivo.  

             Si un nombre de archivo especificado no tiene una extensión especificada, Configuration Manager intenta usar .com, .exe y .bat como posibles extensiones.  

             Cuando se ejecuta el programa en un cliente, Configuration Manager busca primero el nombre del archivo de la línea de comandos dentro del paquete, luego busca en la carpeta de Windows local y, después, busca en la ubicación *%path%* local. Si no se encuentra el archivo, se produce un error en el programa.  

        -   **Carpeta de inicio**: opcionalmente, puede usar este campo para especificar la carpeta desde la que se ejecuta el programa, con hasta 127 caracteres. Esta carpeta puede ser una ruta de acceso absoluta o una ruta de acceso relativa a la carpeta de punto de distribución que contiene el paquete.  

        -   **Ejecutar**: especifica el modo en que se ejecutará el programa en los equipos cliente. Seleccione una de las acciones siguientes:  

            -   **Normal** -el programa se ejecuta en el modo normal en función de los valores predeterminados del sistema y de programas. Este es el modo predeterminado.  

            -   **Minimizada** : el programa se ejecuta minimizado en dispositivos cliente. Los usuarios pueden ver la actividad de instalación en el área de notificación o la barra de tareas.  

            -   **Maximizado** : el programa se ejecuta maximizado en dispositivos cliente. Los usuarios verán toda la actividad de instalación.  

            -   **Hidden** : el programa se ejecuta oculto en los dispositivos cliente. Los usuarios no verán ninguna actividad de instalación.  

        -   **El programa se puede ejecutar**: especifique si el programa se puede ejecutar solo cuando un usuario haya iniciado sesión, solo cuando ningún usuario haya iniciado sesión, o si se ejecutará sin importar si un usuario ha iniciado sesión en el equipo cliente.  

        -   **Modo de ejecución**: especifique si el programa se ejecutará con permisos administrativos o con los permisos del usuario que tenga la sesión actualmente iniciada.  

        -   **Permiten a los usuarios ver e interactuar con el programa de instalación** -Utilice esta opción, si está disponible, para especificar si desea permitir a los usuarios interactuar con el programa de instalación. Esta casilla de verificación sólo está disponible cuando **sólo cuando ningún usuario ha iniciado sesión** o **o no un usuario inicia sesión** se selecciona para **programa puede ejecutarse** y **Ejecutar con derechos administrativos** está seleccionada para **modo de ejecución**.  

        -   **Modo de unidad**: especifique información sobre cómo se ejecutará este programa en la red. Elija una de las acciones siguientes:  

            -   **Se ejecuta con nombre UNC** -indica que el programa se ejecuta con un nombre de convención de nomenclatura Universal (UNC). Esta es la configuración predeterminada.  

            -   **Requiere la letra de unidad** -indica que el programa requiere una letra de unidad para completar su ubicación. Para esta configuración, Configuration Manager puede usar cualquier letra de unidad disponible en el cliente.  

            -   **Requiere la letra de unidad específica (ejemplo: Z:)** -indica que el programa requiere una letra de unidad específica que especifique para calificar totalmente su ubicación. Si la letra de unidad especificada ya se usa en un cliente, el programa no se ejecuta.  

        -   **Volver a conectar al punto de distribución de registro en** -Utilice esta casilla de verificación para indicar si el equipo cliente se vuelve a conectar al punto de distribución cuando el usuario inicia sesión. De forma predeterminada, esta casilla de verificación está desactivada.  

  3.  En el **requisitos** página del Asistente del programa y crear un paquete, especifique la siguiente información:  

        -   **Ejecutar otro programa primero** : puede usar esta opción para identificar un paquete y un programa que se ejecutará antes que este paquete y programa que se va a ejecutar.  

        -   **Requisitos de la plataforma** : seleccione **este programa puede ejecutarse en cualquier plataforma** o seleccione **este programa sólo puede ejecutarse en plataformas especificadas** y, a continuación, elija los sistemas operativos que los clientes deben estar ejecutándose para que pueda instalar el paquete y programa.  

        -   **Espacio en disco estimado**: especifique la cantidad de espacio en disco que requiere el programa de software para poder ejecutarse en el equipo. Esto puede especificarse como **desconocido** (el valor predeterminado) o como un número entero mayor o igual que cero. Si se especifica un valor, también deben especificarse unidades para el valor.  

        -   **Tiempo de ejecución máximo permitido (minutos)** : especifique el tiempo máximo que se espera que el programa se ejecute en el equipo cliente. Esto puede especificarse como **desconocido** (el valor predeterminado) o como un número entero mayor que cero.  

             De forma predeterminada, este valor está establecido en 120 minutos.  

            > [!IMPORTANT]  
            >  Si utiliza ventanas de mantenimiento de la colección en el que se ejecuta este programa, puede producirse un conflicto si el **tiempo de ejecución máximo permitido** es mayor que la ventana de mantenimiento programado. Sin embargo, si el número máximo de tiempo de ejecución se establece en **desconocido**, el programa empezará a ejecutarse durante el mantenimiento y continuará ejecutándose según sea necesario después de cerrar la ventana de mantenimiento. Si el usuario establece el máximo de tiempo de ejecución en un periodo específico que supera la longitud de cualquier ventana de mantenimiento disponibles, no se ejecutará el programa.  

             Si el valor se establece como **desconocido**, Configuration Manager establece el número máximo de tiempo de ejecución en 12 horas (720 minutos).  

            > [!NOTE]  
            >  Si se supera el máximo (si establecida por el usuario o como el valor predeterminado) de tiempo de ejecución, Configuration Manager detendrá el programa si **Ejecutar con derechos administrativos** está seleccionada y **Permitir a los usuarios ver e interactuar con el programa de instalación** no está seleccionada.  

  4.  Haga clic en **Siguiente**.  
  
    #### <a name="create-a-device-program"></a>Crear un programa de dispositivo  
  
  1.  En el **tipo de programa** página de la **crear un paquete y programa asistente**, seleccione **programa para dispositivo**, y, a continuación, haga clic en **siguiente**.  

  2.  En la página **Programa para dispositivo**, especifique lo siguiente:  

        -   **Nombre:** Especifique un nombre para el programa con un máximo de 50 caracteres.  

            > [!NOTE]  
            >  El nombre del programa debe ser único dentro de un paquete. Después de crear un programa, no puede modificar su nombre.  

        -   **Comentario**: opcionalmente, puede especificar un comentario para este programa de dispositivo con un máximo de 127 caracteres.  

        -   **Carpeta de descarga**: especifique el nombre de la carpeta del dispositivo de Windows CE en la que se almacenarán los archivos de origen del paquete. El valor predeterminado es **\Temp\\\**.  

        -   **Línea de comandos**: escriba la línea de comandos que se usará para iniciar este programa o haga clic en **Examinar** para ir a la ubicación del archivo.  

        -   **Ejecutar línea de comandos en la carpeta de descarga** : seleccione esta opción para ejecutar el programa desde la carpeta de descarga especificado anteriormente.  

        -   **Ejecutar línea de comandos de esta carpeta** : seleccione esta opción para especificar una carpeta diferente de la que se va a ejecutar el programa.  

    3.  En la página **Requisitos**, especifique lo siguiente:  

        -   **Espacio en disco estimado**: especifique la cantidad de espacio en disco necesario para el software. Se mostrará a los usuarios de dispositivos móviles antes de instalar el programa.  

        -   **Descargar programa**: especifique información sobre cuándo se puede descargar este programa en dispositivos móviles. Puede especificar **tan pronto como sea posible**, **sólo a través de una red rápida**, o **sólo cuando el dispositivo está acoplado**.  

        -   **Requisitos adicionales**: especifique los requisitos adicionales para este programa. Éstos se mostrarán a los usuarios antes de instalar el software. Por ejemplo, podría notificar a los usuarios que necesitan para cerrar todas las demás aplicaciones antes de ejecutar el programa.  

  4.  Haga clic en **Siguiente**.  

  7.  En la página **Resumen**, revise las acciones que deberán realizarse y, después, complete el asistente.  

 Compruebe que el nuevo paquete y programa aparecen en el nodo **Paquetes** del área de trabajo **Biblioteca de software**.  

## <a name="create-a-package-and-program-from-a-package-definition-file"></a>Crear un paquete y un programa a partir de un archivo de definición del paquete  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Paquetes**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear paquete a partir de definición**.  

4.  En la página **Definición de paquete** del Asistente para crear paquete a partir de definición, elija un archivo de definición del paquete existente o haga clic en **Examinar** para abrir un nuevo archivo de definición del paquete. Después de haber especificado un nuevo archivo de definición de paquete, selecciónelo de la **definición del paquete** lista y, a continuación, haga clic en **siguiente**.  

5.  En la página **Archivos de origen**, especifique la información sobre los archivos de origen necesarios para el paquete y el programa y, después, haga clic en **Siguiente**.  

6.  Si el paquete requiere archivos de origen, en la página **Carpeta de origen**, especifique la ubicación desde la que se deben obtener los archivos de origen y luego haga clic en **Siguiente**.  

7.  En la página **Resumen**, revise las acciones que deberán realizarse y, después, complete el asistente. El nuevo paquete y el programa se muestra en el **paquetes** nodo de la **biblioteca de Software** área de trabajo.  

 Para obtener más información sobre los archivos de definición de paquete, vea [Sobre el formato de archivo de definición de paquete](/sccm/apps/deploy-use/packages-and-programs#about-the-package-definition-file-format) en este tema.  

##  <a name="deploy-packages-and-programs"></a>Implementar paquetes y programas  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Paquetes**.  

3.  Seleccione el paquete que desea implementar, y, a continuación, en la **Inicio** ficha en el **implementación** de grupo, haga clic en **implementar**.  

4.  En el **General** página del Asistente para implementar Software, especifique el nombre del paquete y programa que desea implementar, la colección a la que desea implementar el paquete y programa y comentarios opcionales para la implementación.  

     Seleccione **usar grupos de puntos de distribución predeterminados asociados a esta recopilación** si desea almacenar el contenido del paquete en el grupo de puntos de distribución de colecciones predeterminadas. Si no ha asociado la colección seleccionada un grupo de puntos de distribución, esta opción no estará disponible.  

5.  En la página **Contenido**, haga clic en **Agregar** y, después, seleccione los puntos de distribución o los grupos de puntos de distribución en los que quiere implementar el contenido asociado a este paquete y programa.  

6.  En la página **Configuración de implementación**, elija un propósito para esta implementación y especifique opciones para los paquetes de reactivación y conexiones de uso medido:  

    -   **Propósito**: elija de entre las siguientes opciones:  

        -   **Disponible** -si se implementa la aplicación a un usuario, el usuario verá el paquete publicado y el programa en el catálogo de aplicaciones y podrá solicitarla a petición. Si se implementa el paquete y programa en un dispositivo, el usuario verá en el centro de Software y puede instalar a petición.  

        -   **Requiere** -el paquete y el programa se implementa automáticamente, según la programación configurada. Sin embargo, un usuario puede realizar un seguimiento del estado de implementación de paquete y programa e instalarlo antes de la fecha límite mediante el centro de Software.  

    -   **Enviar paquetes de reactivación** : si el propósito de la implementación se establece en **requiere** y se selecciona esta opción, un paquete de reactivación se enviará a los equipos antes de instalar la implementación para reactivar el equipo en suspensión a la hora de la fecha límite de instalación. Para poder usar esta opción, los equipos deben configurarse para Wake On LAN.  

    -   Seleccione **Permitir a los clientes de una conexión a Internet de uso medido descargar contenido una vez cumplida la fecha límite de instalación, lo cual podría suponer costos adicionales**, si es necesario.  

    > [!NOTE]  
    >  La opción **Implementar previamente el software en el dispositivo primario del usuario** no está disponible al implementar un paquete y un programa.  

7.  En la página **Programación**, configure cuándo se implementará o estará disponible este paquete y programa para dispositivos cliente.  

     Las opciones de esta página varían dependiendo de si se establece la acción de implementación **disponible** o **requiere**.  

8.  Si el propósito de la implementación se establece en **requiere**, configurar el comportamiento de volver a ejecutar el programa de la **comportamiento de reejecución** lista desplegable. Elija entre las siguientes opciones:  

    |comportamiento de reejecución|Más información|  
    |--------------------|----------------------|  
    |Nunca vuelva a ejecutar el programa implementado|El programa no volverá a ejecutar en el cliente, incluso si el programa no pudo originalmente, o se cambian los archivos de programa.|  
    |Siempre vuelva a ejecutar el programa|El programa siempre volverá a ejecutar en el cliente cuando se programa la implementación, incluso si ha ejecutado correctamente el programa. Esto puede ser útil cuando se utilizan implementaciones periódicas en el que el programa se actualiza, por ejemplo con software antivirus.|  
    |Vuelva a ejecutar si el error del intento anterior|El programa volverá a ejecutar cuando se programa la implementación sólo si se produjo un error en el intento de ejecución anterior.|  
    |Vuelva a ejecutar si se realizó correctamente en el intento anterior|El programa volverá a ejecutar solo si previamente ejecutó correctamente en el cliente. Esto es útil cuando se utilizan anuncios periódicos en el que el programa se actualiza regularmente y que cada actualización requiere la actualización anterior se instalaron correctamente.|  

9. En la página **Experiencia del usuario** , especifique la siguiente información:  

    -   **Permitir que los usuarios ejecuten el programa independientemente de las asignaciones**: si se habilita, los usuarios pueden instalar este software desde el Centro de software independientemente de la hora de instalación programada.  

    -   **Instalación de software** – permite que el software se instale fuera de las ventanas de mantenimiento configurada.  

    -   **Reiniciar el sistema (si es necesario para completar la instalación)** : si la instalación de software requiere reiniciar el dispositivo para completar, que esto suceda fuera de las ventanas de mantenimiento configurada.  

    -   **Embedded Devices** (Dispositivos incrustados): cuando implementa paquetes y programas en dispositivos de Windows Embedded habilitados con filtro de escritura, puede especificar la instalación de paquetes y programas en la superposición temporal y confirmar los cambios más tarde, o puede confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento. Al confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento, es necesario reiniciar. Los cambios se conservan en el dispositivo.  

        > [!NOTE]  
        >  Al implementar un paquete o programa a un dispositivo de Windows Embedded, asegúrese de que el dispositivo es un miembro de una colección que tiene una ventana de mantenimiento configurada. Para obtener más información sobre cómo se usan las ventanas de mantenimiento al implementar paquetes y programas en dispositivos de Windows Embedded, vea [Creación de aplicaciones de Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).  
  
10. En la página **Puntos de distribución** , especifique la siguiente información:  

    -   **Opciones de implementación** : especificar las acciones que un cliente debe realizar para ejecutar el contenido de programa. Puede especificar el comportamiento cuando el cliente está en un límite de red rápida o un límite de red lentas o poco confiables.  

    -   **Permiten a los clientes compartir el contenido con otros clientes en la misma subred** : seleccione esta opción para reducir la carga en la red al permitir que los clientes descarguen contenido desde otros clientes de la red que ya descargado y lo almacena en caché el contenido. Esta opción utiliza Windows BranchCache y se puede utilizar en equipos que ejecutan Windows Vista SP2 y posterior.  

    -   **Permiten a los clientes usar una ubicación de origen de reserva para contenido** : si está habilitada, los clientes pueden buscar otros puntos de distribución en la jerarquía de tipo de contenido necesario si no está disponible en el punto de distribución especificada o grupos de puntos de distribución.  

11. En la página **Resumen**, revise las acciones que deberán realizarse y, después, complete el asistente.  

     Puede ver la implementación en el **implementaciones** nodo de la **supervisión** área de trabajo y en el panel de detalles de la pestaña de la implementación de paquete cuando se selecciona la implementación. Para obtener más información, vea [Supervisar paquetes y programas](/sccm/apps/deploy-use/packages-and-programs#monitor-packages-and-programs) en este tema.  

> [!IMPORTANT]  
>  Si ha configurado la opción **Ejecutar programa desde el punto de distribución** en el **puntos de distribución** página del Asistente para implementar Software, desactive la opción **copiar el contenido de este paquete en un recurso compartido de paquete en puntos de distribución**, ya que esto hará que el paquete no está disponible para ejecutarse desde puntos de distribución.  

##  <a name="monitor-packages-and-programs"></a>Supervisar paquetes y programas  
 Para supervisar las implementaciones de paquetes y programas, use los mismos procedimientos que usa para supervisar aplicaciones, tal y como se detalla en [Supervisar aplicaciones](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 Los paquetes y programas también incluyen varios informes integrados, lo que permite supervisar la información sobre el estado de implementación de los paquetes y programas. Estos informes tienen la categoría de informe de **la distribución de Software, paquetes y programas** y **distribución de Software-paquete y el estado de implementación de programa**.  

 Para obtener más información sobre cómo configurar los informes en Configuration Manager, vea [Generación de informes en System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="manage-packages-and-programs"></a>Administrar paquetes y programas  
 En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones**, haga clic en **Paquetes**, seleccione el paquete que quiere administrar y luego seleccione una tarea de administración de la tabla siguiente:  

|Tarea|Más información|  
|----------|----------------------|  
|**Crear archivo de contenido preconfigurado**|Se abre al preconfigurados contenido del Asistente para crear archivos que le permite crear un archivo que contiene el contenido del paquete que se puede importar manualmente a otro sitio. Esto es útil en situaciones donde tiene poco ancho de banda entre el servidor de sitio y el punto de distribución.|  
|**Crear el programa**|Se abre al programa asistente que permite crear un nuevo programa para este paquete.|  
|**Exportar**|Abre el Asistente para exportar paquete que le permite exportar el paquete seleccionado y su contenido en un archivo.<br /><br /> Para obtener información sobre cómo importar paquetes y programas, vea Cómo crear paquetes y programas en este tema.|  
|**Implementar**|Abre el Asistente para implementar software que le permite implementar el paquete y el programa seleccionados en una recopilación. Para obtener más información, vea [Implementar paquetes y programas](/sccm/apps/deploy-use/packages-and-programs#deploy-packages-and-programs) en este tema.|  
|**Distribuir contenido**|Se abre al Asistente para distribuir contenido que le permite enviar el contenido que está asociado con el paquete y programa para puntos de distribución seleccionados o grupos de puntos de distribución.|  
|**Actualizar puntos de distribución**|Actualiza los puntos de distribución con el contenido más reciente para el programa y el paquete seleccionados.|  

##  <a name="about-the-package-definition-file-format"></a>Sobre el formato de archivo de definición de paquete  
 Los archivos de definición del paquete son scripts que puede usar como ayuda para automatizar la creación de paquetes y programas con Configuration Manager. Proporcionan toda la información que Configuration Manager necesita para crear un paquete y programa, excepto la ubicación del paquete de archivos de código fuente. Cada archivo de definición de paquete es un archivo de texto ASCII o UTF-8, siguiendo el formato de archivo .ini y que contiene las siguientes secciones se describe:  

###  <a name="pdf"></a>[PDF]  
 Esta sección identifica el archivo como un archivo de definición de paquete. Contiene la siguiente información:  

-   **Versión**: Especifica la versión del formato de archivo de definición de paquete que usa el archivo. Esto corresponde a la versión de System Management Server (SMS) o Configuration Manager para la que se ha escrito. Esta entrada es necesaria.  

###  <a name="package-definition"></a>[Definición del paquete]  
 En esta sección del archivo de definición de paquete especifica las propiedades del paquete y programa. Proporciona la siguiente información:  

-   **Nombre**: El nombre del paquete, de hasta 50 caracteres. Esta entrada es necesaria.  

-   **Versión**: La versión del paquete, de hasta 32 caracteres. Esta entrada es opcional.  

-   **Icono**: Opcionalmente, el archivo que contiene el icono que se va a usar para este paquete. Si se especifica, este icono reemplazará el icono de paquete predeterminado en la consola de Configuration Manager.  

-   **Publisher**: El publicador del paquete, de hasta 32 caracteres. Esta entrada es necesaria.  

-   **Idioma**: La versión de idioma del paquete, de hasta 32 caracteres. Esta entrada es necesaria.  

-   **Comentario**: Un comentario opcional sobre el paquete, hasta 127 caracteres.  

-   **ContainsNoFiles**: Esta entrada indica si es o no un origen asociado con el paquete.  

-   **Programas**: Los programas definidos para este paquete. Cada nombre de programa se corresponde con un **[programa]** sección en este archivo de definición de paquete. Esta entrada es necesaria.  

     Ejemplo:  

     `Programs=Typical, Custom, Uninstall`  

-   **MIFFileName**: El nombre del archivo de formato de información de administración (MIF) que contiene el estado del paquete, hasta 50 caracteres.  

-   **MIFName**: El nombre del paquete (para la coincidencia de MIF), hasta 50 caracteres.  

-   **MIFVersion**: El número de versión del paquete (para la coincidencia de MIF), hasta 32 caracteres.  

-   **MIFPublisher**: El Editor de software del paquete (para la coincidencia de MIF), hasta 32 caracteres.  

###  <a name="program"></a>[programa]  
 Para cada programa especificado en el **programas** entrada en el **[Package Definition]** sección, el archivo de definición de paquete debe incluir una sección [programa] que define ese programa. Cada sección de programa proporciona la siguiente información:  

-   **Nombre**: El nombre del programa, hasta 50 caracteres. Esta entrada debe ser única dentro de un paquete. Este nombre se usa al definir los anuncios. En los equipos cliente, se muestra el nombre del programa en **ejecutar programas anunciados** en el Panel de Control. Esta entrada es necesaria.  

-   **Icono**: Opcionalmente, especifica el archivo que contiene el icono que se utilizará para este programa. Si se especifica, este icono reemplazará el icono de programa predeterminado en la consola de Configuration Manager y se mostrará en los equipos cliente cuando se anuncia el programa.  

-   **Comentario**: Un comentario opcional sobre el programa, hasta 127 caracteres.  

-   **CommandLine**: Especifica la línea de comandos para el programa, hasta 127 caracteres. El comando es relativa a la carpeta de origen del paquete. Esta entrada es necesaria.  

-   **StartIn**: Especifica la carpeta de trabajo para el programa, hasta 127 caracteres. Esta entrada puede ser una ruta de acceso absoluta en el equipo cliente o una ruta de acceso relativa a la carpeta de origen del paquete. Esta entrada es necesaria.  

-   **Ejecutar**: Especifica el modo de programa en el que se ejecutará el programa. Puede especificar **minimizada**, **maximizado**, o **Hidden**. Si no se incluye esta entrada, el programa se ejecutará en modo normal.  

-   **AfterRunning**: Especifica cualquier acción especial que se produce después de que el programa se ha completado correctamente. Las opciones disponibles son **SMSRestart**, **ProgramRestart**, o **SMSLogoff**. Si no se incluye esta entrada, el programa no ejecutará una acción especial.  

-   **EstimatedDiskSpace**: Especifica la cantidad de espacio en disco que el programa de software que se requiere para poder ejecutarse en el equipo. Esto puede especificarse como **desconocido** (el valor predeterminado) o como un número entero mayor o igual que cero. Si se especifica un valor, deben especificarse también las unidades para el valor.  

     Ejemplo:  

     `EstimatedDiskSpace=38MB`  

-   **EstimatedRunTime**: Especifica la duración estimada (en minutos) que se espera que el programa se ejecute en el equipo cliente. Esto puede especificarse como **desconocido** (el valor predeterminado) o como un número entero mayor que cero.  

     Ejemplo:  

     `EstimatedRunTime=25`  

-   **SupportedClients**: Especifica los procesadores y sistemas operativos en los que se ejecutará este programa. Las plataformas especificadas deben estar separadas por comas. Si no se incluye esta entrada, se deshabilitará la comprobación de la plataforma compatible para este programa.  

-   **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: Especifica el intervalo de principio a fin de los números de versión para los sistemas operativos especificados en la **SupportedClients** entrada.  

     Ejemplo:  

    ```  
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999   
    ```  

-   **AdditionalProgramRequirements**: Opcionalmente, escriba cualquier otra información o requisitos para equipos cliente, hasta 127 caracteres.  

-   **CanRunWhen**: Especifica el estado de usuario que el programa necesita para poder ejecutarse en el equipo cliente. Los valores disponibles son **UserLoggedOn**, **NoUserLoggedOn**, o **AnyUserStatus**. El valor predeterminado es **UserLoggedOn**.  

-   **UserInputRequired**: Especifica si el programa requiere interacción con el usuario. Los valores disponibles son **True** o **False**. El valor predeterminado es **True**. Esta entrada se establece en **False** si **CanRunWhen** no está establecido en **UserLoggedOn**.  

-   **AdminRightsRequired**: Especifica si el programa requiere credenciales administrativas en el equipo para poder ejecutarse. Los valores disponibles son **True** o **False**. El valor predeterminado es **False**. Esta entrada se establece en **True** si **CanRunWhen** no está establecido en **UserLoggedOn**.  

-   **UseInstallAccount**: Especifica si el programa utiliza la cuenta de instalación de Software de cliente cuando se ejecuta en los equipos cliente. De forma predeterminada, este valor es **False**. Este valor también es **False** si **CanRunWhen** está establecido en **UserLoggedOn**.  

-   **DriveLetterConnection**: Especifica si el programa requiere una conexión de la letra de unidad para los archivos del paquete que se encuentran en el punto de distribución. Puede especificar **True** o **False**. El valor predeterminado es **False**, lo que permite al programa usar una conexión de convención de nomenclatura Universal (UNC). Cuando este valor se establece en **True**, se utilizará la siguiente letra de unidad disponible (comenzando por Z: y continuar hacia atrás).  

-   **SpecifyDrive**: Opcionalmente, especifica una letra de unidad que el programa necesita para conectarse a los archivos del paquete en el punto de distribución. Esta especificación fuerza el uso de la letra de unidad especificada para las conexiones de cliente a los puntos de distribución.  

-   **ReconnectDriveAtLogon**: Especifica si el equipo se vuelve a conectar al punto de distribución cuando el usuario inicia sesión. Los valores disponibles son **True** o **False**. El valor predeterminado es **False**.  

-   **DependentProgram**: Especifica un programa en este paquete que se debe ejecutar antes de que el programa actual. Esta entrada usa el formato **DependentProgram**=<**nombrePrograma**, donde **<nombrePrograma\>** es la entrada **Nombre** del programa en el archivo de definición del paquete. Si no hay ningún programa dependiente, deje en blanco esta entrada.  

     Ejemplo:  

     DependentProgram = Admin  
    DependentProgram =  

-   **Asignación**: Especifica cómo se asigna el programa a los usuarios. Este valor puede ser: **FirstUser,** sólo el primer usuario que inicia sesión, ejecuta el programa; o **EveryUser,** cada usuario que inicia sesión en el cliente se ejecuta el programa. Cuando **CanRunWhen** no está establecido en **UserLoggedOn**, esta entrada se establece en **FirstUser**.  

-   **Deshabilitado**: Especifica si este programa puede anunciarse a los clientes. Los valores disponibles son **True** o **False**. El valor predeterminado es **False**.  



<!--HONumber=Nov16_HO1-->


