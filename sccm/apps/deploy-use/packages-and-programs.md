---
title: Paquetes y programas
titleSuffix: Configuration Manager
description: Implementaciones compatibles con paquetes y programas o aplicaciones con System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c840c0a42ccf36e9c69044a6591b29d70c19093
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126478"
---
# <a name="packages-and-programs-in-system-center-configuration-manager"></a>Paquetes y programas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

System Center Configuration Manager sigue siendo compatible con los paquetes y programas usados en Configuration Manager 2007. Una implementación que utilice paquetes y programas podría ser más adecuada que una implementación que use una aplicación cuando se implementa algo de lo siguiente:  

- Aplicaciones en servidores Linux y UNIX
- Scripts que no instalan una aplicación en un equipo, como un script para desfragmentar la unidad de disco del equipo.
- Scripts "únicos" que no es necesario supervisar continuamente.  
- Scripts que se ejecutan según una programación periódica y no pueden usar evaluación global.

Al migrar paquetes desde una versión anterior de Configuration Manager puede implementarlos en su jerarquía de Configuration Manager. Cuando la migración se haya completado, los paquetes aparecerán en el nodo **Paquetes** del área de trabajo **Biblioteca de software**.

Puede modificar e implementar estos paquetes de la misma manera que mediante la distribución de software. El **Asistente para importar paquetes desde una definición** permanece en Configuration Manager para importar paquetes heredados. Los anuncios se convierten en implementaciones cuando se migran desde Configuration Manager 2007a una jerarquía de Configuration Manager.  

> [!NOTE]  
>  Puede usar el administrador de conversión de paquetes de Microsoft System Center Configuration Manager para convertir paquetes y programas en aplicaciones de Configuration Manager.  
>   
>  Para obtener más información, consulte [Administrador de conversión de paquetes de Configuration Manager](https://technet.microsoft.com/library/hh531519.aspx).  

Los paquetes pueden usar algunas características nuevas de Configuration Manager, incluidos los grupos de puntos de distribución y la supervisión. No se pueden distribuir aplicaciones de Microsoft Application Virtualization (App-V) mediante el uso de paquetes y programas en Configuration Manager. Para distribuir aplicaciones virtuales, deben crearse como aplicaciones de Configuration Manager.  

##  <a name="create-a-package-and-program"></a>Crear un paquete y programa  
 Use uno de estos procedimientos como ayuda para crear o importar paquetes y programas.  

### <a name="create-a-package-and-program-using-the-create-package-and-program-wizard"></a>Crear un paquete y un programa con el Asistente para crear paquetes y programas  

1. En la consola de Configuration Manager, seleccione **Biblioteca de software** > **Administración de aplicaciones** > **Paquetes**.  

2. En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear paquete**.  

3. En el **paquete** página de la **crear un paquete y programa asistente**, especifique la siguiente información:  

   -   **Nombre**: especifique un nombre para el paquete con un máximo de 50 caracteres.  

   -   **Descripción**: especifique una descripción para este paquete con un máximo de 128 caracteres.  

   -   **Fabricante** (opcional): especifique un nombre de fabricante para ayudarle a identificar el paquete en la consola de Configuration Manager. Este nombre puede ser un máximo de 32 caracteres.

   -   **Idioma** (opcional): especifique la versión de idioma del paquete con un máximo de 32 caracteres.  

   -   **Versión** (opcional):  especifique un número de versión del paquete con un máximo de 32 caracteres.

   -   **Este paquete contiene archivos de origen**: este valor indica si el paquete requiere que los archivos de origen estén presentes en los dispositivos cliente. De forma predeterminada, esta casilla está desactivada y Configuration Manager no usa puntos de distribución para el paquete. Cuando se selecciona esta casilla, se utilizan puntos de distribución.  

   -   **Carpeta de origen**: si el paquete contiene archivos de origen, haga clic en **Examinar** para abrir el cuadro de diálogo **Establecer carpeta de origen** y, después, especifique la ubicación de los archivos de origen del paquete.  

       > [!NOTE]  
       >  La cuenta de equipo del servidor de sitio debe tener permisos de acceso de lectura a la carpeta de origen que especifique.  

4. En la página **Tipo de programa** del **Asistente para crear paquetes y programas**, seleccione el tipo de programa que quiere crear y, luego, seleccione **Siguiente**. Puede crear un programa para un equipo o dispositivo, o puede omitir este paso y crear un programa más tarde.  

   > [!TIP]  
   >  Para crear un programa para un paquete existente, seleccione primero el paquete. Después, en la pestaña **Inicio**, en el grupo **Paquete**, seleccione **Crear programa** para abrir el **Asistente para crear programas**.  

5. Utilice uno de los siguientes procedimientos para crear un programa estándar o un dispositivo.  

   #### <a name="create-a-standard-program"></a>Crear un programa estándar  

   1.  En la página **Tipo de programa** del **Asistente para crear paquetes y programas**, seleccione **Programa estándar** y, luego, **Siguiente**.     

   2.  En la página **Programa estándar** , especifique la siguiente información:  

       -   **Nombre:** especifique un nombre para el programa con un máximo de 50 caracteres.  

           > [!NOTE]  
           >  El nombre del programa debe ser único dentro de un paquete. Después de crear un programa, no puede modificar su nombre.  

       -   **Línea de comandos**: escriba la línea de comandos que se va a usar para iniciar este programa, o bien haga clic en **Examinar** para ir a la ubicación del archivo.  

           Si un nombre de archivo no tiene una extensión especificada, Configuration Manager intenta usar .com, .exe y .bat como posibles extensiones.  

            Cuando se ejecuta el programa en un cliente, Configuration Manager busca primero el nombre del archivo de la línea de comandos dentro del paquete, luego busca en la carpeta de Windows local y, después, busca en la ubicación *%path%* local. Si no se encuentra el archivo, se produce un error en el programa.  

       -   **Carpeta de inicio** (opcional): especifique la carpeta desde la que se ejecuta el programa, con un máximo de 127 caracteres. Esta carpeta puede ser una ruta de acceso absoluta en el cliente, o una ruta de acceso relacionada con la carpeta del punto de distribución que contiene el paquete.

       -   **Ejecutar**: especifique el modo en el que se ejecuta el programa en los equipos cliente. Seleccione una de las acciones siguientes:  

           -   **Normal**: el programa se ejecuta en el modo normal según los valores predeterminados del programa y del sistema. Este es el modo predeterminado.  

           -   **Minimizado**: el programa se ejecuta minimizado en los dispositivos cliente. Los usuarios pueden ver la actividad de instalación en el área de notificación o la barra de tareas.  

           -   **Maximizado**: el programa se ejecuta maximizado en los dispositivos cliente. Los usuarios ven toda la actividad de instalación.  

           -   **Oculto**: el programa se ejecuta de forma oculta en los dispositivos cliente. Los usuarios no ven ninguna actividad de instalación.  

       -   **El programa se puede ejecutar**: especifique si el programa se ejecuta solo cuando un usuario haya iniciado sesión, solo cuando ningún usuario haya iniciado sesión, o bien si se ejecuta con independencia de que un usuario haya iniciado sesión en el equipo cliente.  

       -   **Modo de ejecución**: especifique si el programa se ejecuta con permisos administrativos o con los permisos del usuario que tenga la sesión actualmente iniciada.  

       -   **Permitir a los usuarios ver la instalación del programa e interactuar con la misma**: use esta opción, si está disponible, para especificar si quiere permitir a los usuarios interactuar con el programa de instalación. Esta casilla solo está disponible cuando se selecciona **Solo cuando ningún usuario haya iniciado sesión** o **Tanto si un usuario ha iniciado sesión como si no** en **El programa puede ejecutarse** y también se selecciona **Ejecutar con derechos administrativos** en **Modo de ejecución**.  

       -   **Modo de unidad**: especifique información sobre cómo se ejecuta este programa en la red. Elija una de las acciones siguientes:  

           -   **Se ejecuta con nombre UNC**: especifique que el programa se ejecuta con un nombre de convención de nomenclatura universal (UNC). Esta es la configuración predeterminada.  

           -   **Requiere letra de unidad**: indica que el programa requiere una letra de unidad para que su ubicación esté completa. Para esta configuración, Configuration Manager puede usar cualquier letra de unidad disponible en el cliente.  

           -   **Requiere una letra de unidad específica**: especifique que el programa requiere una letra de unidad específica que establezca para que su ubicación esté completa (por ejemplo, **Z:**). Si la letra de unidad especificada ya se usa en un cliente, el programa no se ejecuta.  

       -   **Reconectarse al punto de distribución al iniciar sesión**: use esta casilla para indicar si el equipo cliente se vuelve a conectar al punto de distribución cuando el usuario inicie sesión. De forma predeterminada, esta casilla de verificación está desactivada.  

   3.  En la página **Requisitos** del **Asistente para crear paquetes y programas**, especifique la información siguiente:  

       -   **Ejecutar otro programa primero**: use esta opción para identificar un paquete y un programa que se ejecutan antes que este paquete y programa.  

       -   **Requisitos de la plataforma**: seleccione **Este programa puede ejecutarse en cualquier plataforma** o **Este programa solo puede ejecutarse en las plataformas especificadas** y, después, seleccione los sistemas operativos que los clientes deben ejecutar para poder instalar el paquete y el programa.  

       -   **Espacio en disco estimado**: especifique la cantidad de espacio en disco que requiere el programa de software para poder ejecutarse en el equipo. Esto puede especificarse como **desconocido** (el valor predeterminado) o como un número entero mayor o igual que cero. Si se especifica un valor, también deben especificarse unidades para el valor.  

       -   **Duración máxima permitida de la ejecución (minutos)**: Especifica la duración máxima esperada de la ejecución del programa en el equipo cliente. Esto puede especificarse como **desconocido** (el valor predeterminado) o como un número entero mayor que cero.  

            De forma predeterminada, este valor está establecido en 120 minutos.  

           > [!IMPORTANT]  
           >  Si está usando ventanas de mantenimiento para la recopilación en la que se ejecuta este programa, puede producirse un conflicto si el **Tiempo de ejecución máximo permitido** es mayor que la ventana de mantenimiento programada. En cambio, si el tiempo de ejecución máximo se establece como **Desconocido**, el programa iniciará su ejecución durante la ventana de mantenimiento y seguirá ejecutándose según sea necesario después de cerrar la ventana de mantenimiento. Si el usuario establece el tiempo de ejecución máximo en un periodo concreto que supere la duración de alguna ventana de mantenimiento disponible, el programa no se ejecutará.  

            Si el valor se configura como **Desconocido**, Configuration Manager establece el tiempo máximo de ejecución permitido en 12 horas (720 minutos).  

           > [!NOTE]  
           >  Si se supera el tiempo de ejecución máximo (ya sea un valor establecido por el usuario o el valor predeterminado), Configuration Manager detiene el programa si se selecciona **Ejecutar con derechos administrativos** y no se selecciona **Permitir a los usuarios ver la instalación del programa e interactuar con la misma**.  

   4.  Elija **Siguiente**.  

   #### <a name="create-a-device-program"></a>Crear un programa de dispositivo  

   1.  En la página **Tipo de programa** del **Asistente para crear paquetes y programas**, seleccione **Programa para dispositivo** y, luego, **Siguiente**.  

   2.  En la página **Programa para dispositivo**, especifique lo siguiente:  

       -   **Nombre**: especifique un nombre para el programa con un máximo de 50 caracteres.  

           > [!NOTE]  
           >  El nombre del programa debe ser único dentro de un paquete. Después de crear un programa, no puede modificar su nombre.  

       -   **Comentario** (opcional): especifique un comentario para este programa de dispositivo con un máximo de 127 caracteres.  

       -   **Carpeta de descarga**: especifique el nombre de la carpeta del dispositivo de Windows CE en la que se almacenarán los archivos de origen del paquete. El valor predeterminado es **\Temp\\\**.  

       -   **Línea de comandos**: escriba la línea de comandos que se va a usar para iniciar este programa, o bien haga clic en **Examinar** para ir a la ubicación del archivo.  

       -   **Ejecutar línea de comandos en carpeta de descarga**: seleccione esta opción para ejecutar el programa desde la carpeta de descarga especificada anteriormente.  

       -   **Ejecutar línea de comandos desde esta carpeta**: seleccione esta opción para especificar otra carpeta desde la que se va a ejecutar el programa.  

   3.  En la página **Requisitos**, especifique lo siguiente:  

       -   **Espacio en disco estimado**: especifique la cantidad de espacio en disco necesario para el software. Se mostrará a los usuarios de dispositivos móviles antes de instalar el programa.  

       -   **Descargar programa**: especifique información sobre cuándo se puede descargar este programa en dispositivos móviles. Puede especificar **tan pronto como sea posible**, **sólo a través de una red rápida**, o **sólo cuando el dispositivo está acoplado**.  

       -   **Requisitos adicionales**: especifique los requisitos adicionales para este programa. Se mostrarán a los usuarios antes de instalar el software. Por ejemplo, podría notificar a los usuarios que necesitan para cerrar todas las demás aplicaciones antes de ejecutar el programa.  

   4.  Elija **Siguiente**.  

   7.  En la página **Resumen**, revise las acciones que deberán realizarse y, después, complete el asistente.  

   Compruebe que el nuevo paquete y programa aparecen en el nodo **Paquetes** del área de trabajo **Biblioteca de software**.  

## <a name="create-a-package-and-program-from-a-package-definition-file"></a>Crear un paquete y un programa a partir de un archivo de definición del paquete  

1. En la consola de Configuration Manager, seleccione **Biblioteca de software** > **Administración de aplicaciones** > **Paquetes**.  

2. En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear paquete a partir de definición**.  

3. En la página **Definición de paquete** del **Asistente para crear paquete a partir de definición**, elija un archivo de definición del paquete existente o seleccione **Examinar** para abrir un nuevo archivo de definición del paquete. Después de especificar un nuevo archivo de definición del paquete, selecciónelo en la lista **Definición de paquete** y, luego, seleccione **Siguiente**.  

4. En la página **Archivos de origen**, especifique la información sobre los archivos de origen necesarios para el paquete y el programa y, después, seleccione **Siguiente**.  

5. Si el paquete requiere archivos de origen, en la página **Carpeta de origen**, especifique la ubicación desde la que se deben obtener los archivos de origen y, luego, seleccione **Siguiente**.  

6. En la página **Resumen**, revise las acciones que deberán realizarse y, después, complete el asistente. El nuevo paquete y programa aparecen en el nodo **Paquetes** del área de trabajo **Biblioteca de software**.  

   Para obtener más información sobre los archivos de definición de paquete, vea [Sobre el formato de archivo de definición de paquete](/sccm/apps/deploy-use/packages-and-programs#about-the-package-definition-file-format) en este tema.  

##  <a name="deploy-packages-and-programs"></a>Implementar paquetes y programas  

1. En la consola de Configuration Manager, seleccione **Biblioteca de software** > **Administración de aplicaciones** > **Paquetes**.  

2. Seleccione el paquete que quiere implementar y, después, en la pestaña **Inicio**, en el grupo **Implementación**, seleccione **Implementar**.  

3. En la página **General** del **Asistente para implementar software**, especifique el nombre del paquete y el programa que quiere implementar, la recopilación en la que quiere implementar el paquete y el programa, y comentarios opcionales para la implementación.  

    Seleccione **usar grupos de puntos de distribución predeterminados asociados a esta recopilación** si desea almacenar el contenido del paquete en el grupo de puntos de distribución de colecciones predeterminadas. Si no asocia la recopilación seleccionada con un grupo de puntos de distribución, esta opción no estará disponible.  

4. En la página **Contenido**, seleccione **Agregar** y, después, seleccione los puntos de distribución o los grupos de puntos de distribución en los que quiere implementar el contenido asociado a este paquete y programa.  

5. En la página **Configuración de implementación**, elija un propósito para esta implementación y especifique opciones para los paquetes de reactivación y conexiones de uso medido:  

   - **Finalidad**: Elija de entre las siguientes opciones:  

     -   **Disponible**: si la aplicación se implementa en un usuario, este verá el paquete y el programa publicados en el catálogo de aplicaciones y podrá solicitarlos a petición. Si el paquete y el programa se implementan en un dispositivo, el usuario los verá en el Centro de software y los podrá instalar a petición.  

     -   **Requerido**: el paquete y el programa se implementan de forma automática según la programación configurada. Sin embargo, un usuario puede realizar un seguimiento del estado de implementación de paquete y programa e instalarlo antes de la fecha límite mediante el centro de Software.  

     > [!NOTE]
     >  Si varios usuarios inician sesión en el dispositivo, es posible que las implementaciones de paquete y secuencia de tareas no aparezcan en el centro de Software.

   - **Enviar paquetes de reactivación**: si el propósito de la implementación se establece en **Requerido** y se selecciona esta opción, se envía un paquete de reactivación a los equipos antes de instalar la implementación para reactivar el equipo en suspensión a la hora límite de instalación. Para poder usar esta opción, los equipos deben configurarse para Wake On LAN.  

   - **Permitir a los clientes de una conexión a Internet de uso medido descargar contenido una vez cumplida la fecha límite de instalación, lo cual podría suponer costos adicionales**: seleccione esta opción si es necesario.  

   > [!NOTE]  
   >  La opción **Implementar previamente el software en el dispositivo primario del usuario** no está disponible al implementar un paquete y un programa.  

6. En la página **Programación**, configure cuándo se implementará o estará disponible este paquete y programa para dispositivos cliente.  

    Las opciones de esta página variarán en función de si la acción de implementación se establece en **Disponible** o **Requerido**.  

7. Si el propósito de implementación se establece en **Requerido**, configure el comportamiento de reejecución del programa en la lista desplegable **Comportamiento de reejecución**. Elija entre las siguientes opciones:  


   |             comportamiento de reejecución             |                                                                                                                        Más información                                                                                                                        |
   |----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |      Nunca vuelva a ejecutar el programa implementado      |                                                                      El programa no volverá a ejecutarse en el cliente, incluso aunque se produjese un error en el programa originalmente o se cambiasen los archivos de programa.                                                                      |
   |          Siempre vuelva a ejecutar el programa          |   El programa siempre se volverá a ejecutar en el cliente cuando se programa la implementación, incluso aunque el sistema ya se haya ejecutado correctamente. Esto puede ser útil cuando se utilizan implementaciones periódicas en el que el programa se actualiza, por ejemplo con software antivirus.    |
   |    Vuelva a ejecutar si el error del intento anterior    |                                                                              El programa se volverá a ejecutar cuando la implementación se programe solo si se produjo un error en el intento de ejecución anterior.                                                                              |
   | Vuelva a ejecutar si se realizó correctamente en el intento anterior | El programa solo se volverá a ejecutar si previamente se ejecutó correctamente en el cliente. Esto es útil cuando se utilizan anuncios periódicos en el que el programa se actualiza regularmente y que cada actualización requiere la actualización anterior se instalaron correctamente. |


8. En la página **Experiencia del usuario** , especifique la siguiente información:  

    -   **Permitir que los usuarios ejecuten el programa independientemente de las asignaciones**: si se habilita, los usuarios pueden instalar este software desde el Centro de software independientemente de la hora de instalación programada.  

    -   **Instalación de software**: permite que el software se instale fuera de las ventanas de mantenimiento configuradas.  

    -   **Reinicio del sistema (si es necesario para completar la instalación)**: si la instalación de software requiere un reinicio del dispositivo para completarse, permite que se produzca fuera de las ventanas de mantenimiento configuradas.  

    -   **Dispositivos de Embedded**: cuando se implementan paquetes y programas en dispositivos de Windows Embedded habilitados con filtro de escritura, puede especificar que los paquetes y programas se instalen en la superposición temporal y confirmar los cambios más tarde. También puede confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento. Al confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento, es necesario reiniciar. Los cambios se conservan en el dispositivo.  

        > [!NOTE]  
        >  Al implementar un paquete o programa a un dispositivo de Windows Embedded, asegúrese de que el dispositivo es un miembro de una colección que tiene una ventana de mantenimiento configurada. Para obtener más información sobre cómo se usan las ventanas de mantenimiento al implementar paquetes y programas en dispositivos de Windows Embedded, vea [Creación de aplicaciones de Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).  

9. En la página **Puntos de distribución** , especifique la siguiente información:  

    -   **Opciones de implementación**: especifique las acciones que debe realizar un cliente para ejecutar contenido del programa. Puede especificar el comportamiento cuando el cliente está en un límite de red rápida o un límite de red lentas o poco confiables.  

    -   **Permitir a los clientes compartir el contenido con otros clientes en la misma subred**: para reducir la carga en la red, seleccione esta opción para permitir que los clientes descarguen contenido de otros clientes en la red que ya han descargado el contenido y lo han almacenado en caché. Esta opción utiliza Windows BranchCache y se puede utilizar en equipos que ejecutan Windows Vista SP2 y posterior.  

    -   **Permitir a los clientes usar una ubicación de origen de reserva para el contenido**:  

        -  **Versiones anteriores a 1610**: puede activa la casilla **Permitir ubicación de origen de reserva para contenido** para permitir que los clientes que están fuera de estos grupos de límites reviertan y usen el punto de distribución como una ubicación de origen para el contenido cuando no estén disponibles otros puntos de distribución.

        - **Versión 1610 y posteriores**: ya no se puede configurar **Permitir ubicación de origen de reserva para contenido**.  En su lugar, se deben configurar relaciones entre grupos de límites que determinen cuándo puede un cliente empezar a buscar grupos de límites adicionales para una ubicación de origen de contenido válida.

10. En la página **Resumen**, revise las acciones que deberán realizarse y, después, complete el asistente.  

     Puede ver la implementación en el **implementaciones** nodo de la **supervisión** área de trabajo y en el panel de detalles de la pestaña de la implementación de paquete cuando se selecciona la implementación. Para obtener más información, vea [Supervisar paquetes y programas](/sccm/apps/deploy-use/packages-and-programs#monitor-packages-and-programs) en este tema.  

> [!IMPORTANT]  
>  Si ha configurado la opción **Ejecutar programa desde el punto de distribución** en la página **Puntos de distribución** del **Asistente para implementar software**, no desactive la opción **Copiar el contenido de este paquete en un recurso compartido de paquete en los puntos de distribución**, ya que esto hará que el paquete no se pueda ejecutar desde puntos de distribución.  

##  <a name="monitor-packages-and-programs"></a>Supervisar paquetes y programas  
 Para supervisar las implementaciones de paquetes y programas, use los mismos procedimientos que usa para supervisar aplicaciones, tal y como se detalla en [Supervisar aplicaciones](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 Los paquetes y programas también incluyen varios informes integrados, lo que permite supervisar la información sobre el estado de implementación de los paquetes y programas. Estos informes tienen la categoría de informe de **la distribución de Software, paquetes y programas** y **distribución de Software-paquete y el estado de implementación de programa**.  

 Para obtener más información sobre cómo configurar los informes en Configuration Manager, vea [Generación de informes en System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="manage-packages-and-programs"></a>Administrar paquetes y programas  
 En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones**, seleccione **Paquetes**, elija el paquete que quiere administrar y, luego, seleccione una tarea de administración de la tabla siguiente:  

|Tarea|Más información|  
|----------|----------------------|  
|**Crear archivo de contenido preconfigurado**|Abre el **Asistente para crear archivos de contenido preconfigurados**, que le permite crear un archivo que incluye el contenido del paquete que se puede importar manualmente a otro sitio. Esto es útil en situaciones donde tiene poco ancho de banda entre el servidor de sitio y el punto de distribución.|  
|**Crear el programa**|Abre el **Asistente para crear programas**, que le permite crear un programa para este paquete.|  
|**Exportarar**|Abre el **Asistente para exportar paquete**, que le permite exportar el paquete seleccionado y su contenido en un archivo.<br /><br /> Para obtener información sobre cómo importar paquetes y programas, consulte [Crear un paquete y programa](/sccm/apps/deploy-use/packages-and-programs#create-packages-and-programs) en este tema.|  
|**Implementar**|Abre el **Asistente para implementar software**, que le permite implementar el paquete y el programa seleccionados en una recopilación. Para obtener más información, vea [Implementar paquetes y programas](/sccm/apps/deploy-use/packages-and-programs#deploy-packages-and-programs) en este tema.|  
|**Distribuir contenido**|Abre el **Asistente para distribuir contenido**, que le permite enviar el contenido asociado con el paquete y el programa a puntos de distribución o grupos de puntos de distribución seleccionados.|  
|**Actualizar puntos de distribución**|Actualiza los puntos de distribución con el contenido más reciente para el programa y el paquete seleccionados.|  

##  <a name="about-the-package-definition-file-format"></a>Sobre el formato de archivo de definición de paquete  
 Los archivos de definición del paquete son scripts que puede usar como ayuda para automatizar la creación de paquetes y programas con Configuration Manager. Proporcionan toda la información que Configuration Manager necesita para crear un paquete y un programa, excepto la ubicación de los archivos de origen del paquete. Cada archivo de definición del paquete es un archivo de texto ASCII o UTF-8 que usa el formato de archivo .ini y contiene las secciones siguientes:  

###  <a name="pdf"></a>[PDF]  
 Esta sección identifica el archivo como un archivo de definición de paquete. Contiene la siguiente información:  

-   **Versión**: especifique la versión del formato de archivo de definición del paquete que usa el archivo. Esto corresponde a la versión de System Management Server (SMS) o Configuration Manager para la que se ha escrito. Esta entrada es necesaria.  

###  <a name="package-definition"></a>[Definición del paquete]  
 Especifique las propiedades del paquete y del programa. Proporciona la siguiente información:  

-   **Nombre**: el nombre del paquete, de hasta 50 caracteres.  

-   **Versión** (opcional): la versión del paquete, de hasta 32 caracteres.  

-   **Icono** (opcional): archivo que contiene el icono que se va a usar para este paquete. Si se especifica, este icono reemplaza al icono de paquete predeterminado en la consola de Configuration Manager.

-   **Publicador**: el publicador del paquete, de hasta 32 caracteres.

-   **Idiomas**: la versión de idioma del paquete, de hasta 32 caracteres.

-   **Comentario** (opcional): comentario sobre el paquete, de hasta 127 caracteres.

-   **ContainsNoFiles**: esta entrada indica si es o no un origen asociado con el paquete.  

-   **Programas**: programas definidos para este paquete. Cada nombre de programa se corresponde con un **[programa]** sección en este archivo de definición de paquete.  

     Ejemplo:  

     `Programs=Typical, Custom, Uninstall`  

-   **MIFFileName**: el nombre del archivo de formato de información de administración (MIF) que contiene el estado del paquete, hasta 50 caracteres.  

-   **MIFName**: el nombre del paquete (para la coincidencia de MIF), hasta 50 caracteres.  

-   **MIFVersion**: el número de versión del paquete (para la coincidencia de MIF), hasta 32 caracteres.  

-   **MIFPublisher**: el editor de software del paquete (para la coincidencia de MIF), hasta 32 caracteres.  

###  <a name="program"></a>[programa]  
 Por cada programa especificado en la entrada **Programas** de la sección **[Package Definition]**, el archivo de definición del paquete debe incluir una sección [Program] que defina ese programa. Cada sección de programa proporciona la siguiente información:  

-   **Nombre**: el nombre del programa, hasta 50 caracteres. Esta entrada debe ser única dentro de un paquete. Este nombre se usa al definir los anuncios. En los equipos cliente, se muestra el nombre del programa en **ejecutar programas anunciados** en el Panel de Control.  

-   **Icono** (opcional): especifique el archivo que contiene el icono que se va a usar para este programa. Si se especifica, este icono reemplaza al icono de programa predeterminado en la consola de Configuration Manager y se muestra en los equipos cliente cuando se anuncia el programa.

-   **Comentario** (opcional): comentario sobre el programa, de hasta 127 caracteres.

-   **CommandLine**: especifique la línea de comandos del programa, de hasta 127 caracteres. El comando es relativa a la carpeta de origen del paquete.

-   **StartIn**: especifique la carpeta de trabajo del programa, de hasta 127 caracteres. Esta entrada puede ser una ruta de acceso absoluta en el equipo cliente o una ruta de acceso relativa a la carpeta de origen del paquete.

-   **Ejecutar**: especifique el modo de programa en el que se ejecuta el programa. Puede especificar **minimizada**, **maximizado**, o **Hidden**. Si no se incluye esta entrada, el programa se ejecuta en modo normal.  

-   **AfterRunning**: especifique alguna acción especial que se produzca cuando el programa se complete correctamente. Las opciones disponibles son **SMSRestart**, **ProgramRestart**, o **SMSLogoff**. Si no se incluye esta entrada, el programa no ejecuta ninguna acción especial.  

-   **EstimatedDiskSpace**: especifique la cantidad de espacio en disco que requiere el programa de software para poder ejecutarse en el equipo. Esto puede especificarse como **desconocido** (el valor predeterminado) o como un número entero mayor o igual que cero. Si se especifica un valor, deben especificarse también las unidades para el valor.  

     Ejemplo:  

     `EstimatedDiskSpace=38MB`  

-   **EstimatedRunTime**: especifique la duración estimada (en minutos) que se espera que el programa se ejecute en el equipo cliente. Esto puede especificarse como **desconocido** (el valor predeterminado) o como un número entero mayor que cero.  

     Ejemplo:  

     `EstimatedRunTime=25`  

-   **SupportedClients**: especifique los procesadores y sistemas operativos en los que se ejecuta este programa. Las plataformas especificadas deben estar separadas por comas. Si no se incluye esta entrada, se deshabilita la comprobación de la plataforma compatible para este programa.  

-   **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: especifique el intervalo de inicio a fin de los números de versión de los sistemas operativos especificados en la entrada **SupportedClients**.  

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

-   **AdditionalProgramRequirements** (opcional): proporcione otra información o requisitos de los equipos cliente, hasta 127 caracteres.

-   **CanRunWhen**: especifique el estado de usuario que el programa requiere para ejecutarse en el equipo cliente. Los valores disponibles son **UserLoggedOn**, **NoUserLoggedOn**, o **AnyUserStatus**. El valor predeterminado es **UserLoggedOn**.  

-   **UserInputRequired**: especifique si el programa requiere interacción con el usuario. Los valores disponibles son **True** o **False**. El valor predeterminado es **True**. Esta entrada se establece en **False** si **CanRunWhen** no está establecido en **UserLoggedOn**.  

-   **AdminRightsRequired**: especifique si el programa requiere credenciales administrativas en el equipo para ejecutarse. Los valores disponibles son **True** o **False**. El valor predeterminado es **False**. Esta entrada se establece en **True** si **CanRunWhen** no está establecido en **UserLoggedOn**.  

-   **UseInstallAccount**: especifique si el programa usa la cuenta de instalación del software cliente cuando se ejecuta en equipos cliente. De forma predeterminada, este valor es **False**. Este valor también es **False** si **CanRunWhen** está establecido en **UserLoggedOn**.  

-   **DriveLetterConnection**: especifique si el programa requiere la conexión de una letra de unidad con los archivos del paquete que se encuentran en el punto de distribución. Puede especificar **True** o **False**. El valor predeterminado es **False**, lo que permite al programa usar una conexión de convención de nomenclatura universal (UNC). Cuando este valor se establece como **True**, se usa la siguiente letra de unidad disponible (comenzando por Z: y continuando hacia atrás).  

-   **SpecifyDrive** (opcional): especifique una letra de unidad que el programa necesita para conectarse a los archivos del paquete en el punto de distribución. Esta especificación fuerza el uso de la letra de unidad especificada para las conexiones de cliente a los puntos de distribución.

-   **ReconnectDriveAtLogon**: especifique si el equipo se vuelve a conectar al punto de distribución cuando el usuario inicia sesión. Los valores disponibles son **True** o **False**. El valor predeterminado es **False**.  

-   **DependentProgram**: especifique un programa de este paquete que se tenga que ejecutar antes del programa actual. Esta entrada usa el formato **DependentProgram**=<**nombrePrograma**, donde **<nombrePrograma\>** es la entrada **Nombre** del programa en el archivo de definición del paquete. Si no hay ningún programa dependiente, deje en blanco esta entrada.  

     Ejemplo:  

     DependentProgram = Admin  
    DependentProgram =  

-   **Asignación**: especifique cómo se asigna el programa a los usuarios. Este valor puede ser: **FirstUser** (solo el primer usuario que inicia sesión en el cliente ejecuta el programa) o **EveryUser** (todos los usuarios que inician sesión ejecutan el programa). Cuando **CanRunWhen** no está establecido en **UserLoggedOn**, esta entrada se establece en **FirstUser**.  

-   **Disabled**: especifique si este programa se puede anunciar a los clientes. Los valores disponibles son **True** o **False**. El valor predeterminado es **False**.  
