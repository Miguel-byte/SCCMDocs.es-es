---
title: 'Administrar controladores '
titleSuffix: Configuration Manager
description: Use el catálogo de controladores de Configuration Manager para importar controladores de dispositivos, controladores de grupo en paquetes y distribuir esos paquetes a puntos de distribución.
ms.date: 01/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4eb97430bd5d7ae5cc50044f8049f41cb9b4cf08
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351537"
---
# <a name="manage-drivers-in-system-center-configuration-manager"></a>Administrar controladores en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

System Center Configuration Manager proporciona un catálogo de controladores que puede usar para administrar los controladores de dispositivos Windows en su entorno de Configuration Manager. Puede usar el catálogo de controladores para importar controladores de dispositivos en Configuration Manager, agruparlos en paquetes y distribuirlos a puntos de distribución para obtener acceso a los mismos al implementar un sistema operativo. Los controladores de dispositivos se pueden usar cuando se instala un sistema operativo completo en el equipo de destino y cuando se instala Windows PE mediante una imagen de arranque. Los controladores de dispositivos de Windows están compuestos por un archivo de información de instalación (INF) y los archivos adicionales necesarios para admitir el dispositivo. Cuando se implementa un sistema operativo, Configuration Manager obtiene la información de hardware y plataforma para el dispositivo mediante el archivo INF. Utilice lo siguiente para administrar controladores en su entorno de Configuration Manager.

##  <a name="BKMK_DriverCategories"></a> Categorías de controlador de dispositivos  
 Cuando importa controladores de dispositivos, puede asignarlos a una categoría. Las categorías de controladores de dispositivos permiten agrupar controladores de dispositivos de uso similar en el catálogo de controladores. Por ejemplo, puede asignar todos los controladores de dispositivos adaptadores de red a una determinada categoría. A continuación, cuando se crea una secuencia de tareas que incluye la etapa [Aplicar controladores automáticamente	](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers), puede especificar una categoría específica de controladores de dispositivos. Configuration Manager examina el hardware y selecciona los controladores aplicables de dicha categoría en la fase del sistema que va a usar el programa de instalación de Windows.  

##  <a name="BKMK_ManagingDriverPackages"></a> Paquetes de controladores  
 Puede agrupar controladores de dispositivos similares en paquetes para facilitar las implementaciones de sistema operativo. Por ejemplo, puede optar por crear un paquete de controladores para cada fabricante de equipos de la red. Puede crear un paquete de controladores al importar controladores en el catálogo de controladores directamente en el nodo **Paquetes de controladores** . Al finalizar la creación del paquete de controladores, deberá distribuirlo a puntos de distribución desde los cuales los equipos cliente de Configuration Manager podrán instalar los controladores como corresponda. Tenga en cuenta lo siguiente:  

-   Cuando crea un paquete de controladores, la ubicación de origen del paquete debe apuntar a un recurso compartido de red vacío que ningún otro paquete de controladores esté utilizando, y el proveedor de SMS debe tener permisos de lectura y escritura en esa ubicación.  

-   Al agregar controladores de dispositivos a un paquete de controladores, Configuration Manager copia el controlador de dispositivo en la ubicación de origen del paquete de controladores. Solo puede agregar a un paquete de controladores de dispositivos los controladores importados y habilitados en el catálogo de controladores.  

-   Para copiar un subconjunto de controladores de dispositivos de un paquete de controladores existente, cree un nuevo paquete de controladores, agregue el subconjunto de controladores de dispositivos al nuevo paquete y, después, distribuya el nuevo paquete a un punto de distribución.  

 Use las secciones siguientes para crear y administrar paquetes de controladores.  

###  <a name="CreatingDriverPackages"></a> Crear un paquete de controladores  
 Utilice el procedimiento siguiente para crear un nuevo paquete de controladores.  

> [!IMPORTANT]  
>  Para crear un paquete de controladores, debe tener una carpeta de red vacía que no use otro paquete de controladores. En la mayoría de los casos, debe crear una nueva carpeta antes de iniciar este procedimiento.  

> [!NOTE]  
>  Cuando use secuencias de tareas para instalar controladores, cree paquetes de controladores que contengan menos de 500 controladores de dispositivos.  

 Utilice el procedimiento siguiente para crear un paquete de controladores.  

#### <a name="to-create-a-driver-package"></a>Para crear un paquete de controladores  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Paquetes de controladores**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear paquete de controladores**.  

4.  En el cuadro **Nombre** , especifique un nombre descriptivo para el paquete de controladores.  

5.  En el cuadro **Comentario** , escriba una descripción opcional del paquete de controladores. Asegúrese de que la descripción proporciona información sobre el contenido o el propósito del paquete de controladores.  

6.  En el cuadro **Ruta de acceso** , especifique una carpeta de origen vacía para el paquete de controladores. Escriba la ruta de acceso a la carpeta de origen en formato de convención de nomenclatura universal (UNC). Cada paquete de controladores debe utilizar una carpeta única.  

    > [!IMPORTANT]  
    >  La cuenta de servidor de sitio debe tener permisos de **lectura** y **escritura** en la carpeta de origen especificada.  

 El nuevo paquete de controladores no contiene ningún controlador. El siguiente paso es agregar controladores al paquete.  

 Si el nodo **Paquetes de controladores** contiene varios paquetes, puede agregar carpetas al nodo para separar los paquetes en grupos lógicos.  

###  <a name="BKMK_PackageActions"></a> Acciones adicionales para paquetes de controladores  
 Se pueden realizar otras acciones para administrar paquetes de controladores cuando se seleccione uno o varios paquetes de controladores del nodo **Paquetes de controladores** . Estas acciones incluyen las siguientes:  

|Acción|Descripción|  
|------------|-----------------|  
|**Crear archivo de contenido preconfigurado**|Crea archivos que se pueden utilizar para importar manualmente contenido y sus metadatos asociados. Utilice el contenido preconfigurado si dispone de poco ancho de banda de red entre el servidor de sitio y los puntos de distribución donde se almacena el paquete de controladores.|  
|**Eliminar**|Quita el paquete de controladores del nodo **Paquetes de controladores** .|  
|**Distribuir contenido**|Distribuye el paquete de controladores a puntos de distribución, grupos de puntos de distribución y grupos de puntos de distribución asociados a recopilaciones.|  
|**Administrar cuentas de acceso**|Agrega, modifica o elimina cuentas de acceso para el paquete de controladores.<br /><br /> Para obtener más información sobre las cuentas de acceso de paquete, consulte [Referencia técnica para las cuentas que se usan en Configuration Manager](../../core/plan-design/hierarchy/accounts.md).|  
|**Moverr**|Mueve el paquete de controladores a otra carpeta en el nodo **Paquetes de controladores** .|  
|**Actualizar puntos de distribución**|Actualiza el paquete de controladores de dispositivo en todos los puntos de distribución en los que se almacena el paquete. Esta acción copia solo el contenido que ha cambiado desde la última vez que se distribuyó.|  
|**Propiedades**|Abre el cuadro de diálogo **Propiedades** , en el que puede revisar y cambiar las propiedades y el contenido del controlador de dispositivo. Por ejemplo, puede cambiar el nombre y la descripción del controlador de dispositivo, habilitarlo y especificar las plataformas en las que se puede ejecutar.|  

##  <a name="BKMK_DeviceDrivers"></a> Controladores de dispositivo  
 Puede instalar controladores de dispositivos en equipos de destino sin incluirlos en la imagen del sistema operativo que se va a implementar. Configuration Manager proporciona un catálogo de controladores con referencias a todos los controladores de dispositivos que se importan a Configuration Manager. El catálogo de controladores se encuentra en el área de trabajo **Biblioteca de software** y se compone de dos nodos: **Controladores** y **Paquetes de controladores**. El nodo **Controladores** enumera todos los controladores que haya importado en el catálogo de controladores. Use este nodo para detectar detalles acerca de cada controlador importado, modificar los controladores de un paquete de controladores o una imagen de arranque, habilitar o deshabilitar un controlador, etc.  

###  <a name="BKMK_ImportDrivers"></a> Importar controladores de dispositivos en el catálogo de controladores  
 Debe importar los controladores de dispositivos en el catálogo de controladores para poder usarlos al implementar un sistema operativo. Para administrar mejor los controladores de dispositivos, importe solo los controladores que pretende instalar como parte de la implementación de sistema operativo. Sin embargo, también puede guardar varias versiones de controladores de dispositivos en el catálogo de controladores para proporcionar una manera sencilla de actualizar los controladores existentes de dispositivos cuando se producen cambios en los requisitos de hardware en la red.  

 Como parte del proceso de importación del controlador de dispositivo, Configuration Manager lee la información de proveedor, clase, versión, firma, hardware compatible y plataforma compatible asociada al dispositivo. De forma predeterminada, el controlador recibe el nombre del primer dispositivo de hardware al que presta servicio; sin embargo, puede cambiar el nombre del controlador de dispositivo más tarde. La lista de plataformas compatibles se basa en la información del archivo INF del controlador. Como la exactitud de esta información puede variar, compruebe manualmente que el controlador de dispositivo es compatible después de importarlo en el catálogo de controladores.  

 Después de importar controladores de dispositivos en el catálogo, puede agregarlos a paquetes de controladores o a paquetes de imágenes de arranque.  

> [!IMPORTANT]  
>  No puede importar controladores de dispositivos directamente en una subcarpeta del nodo **Controladores** . Para importar un controlador de dispositivo en una subcarpeta, primero importe el controlador de dispositivo en el nodo **Controladores** y, después, mueva el controlador a la subcarpeta.  

 Utilice el siguiente procedimiento para importar controladores de dispositivos de Windows.  

#### <a name="to-import-windows-device-drivers-into-the-driver-catalog"></a>Para importar controladores de dispositivos de Windows en el catálogo de controladores  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Controladores**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Importar controlador** para iniciar el **Asistente para importar nuevo controlador**.  

4.  En la página **Buscar controlador** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**:  

    -   **Importar todos los controladores en la siguiente ruta de acceso de red (UNC)**: para importar todos los controladores de dispositivos incluidos en una carpeta específica, especifique la ruta de acceso de red a la carpeta de controladores de dispositivos. Por ejemplo:  **\\\servername\folder**.  

        > [!NOTE]  
        >  El proceso para importar todos los controladores puede tardar algún tiempo si hay un gran número de carpetas y una gran cantidad de archivos de controlador (.inf).  

    -   **Importar un controlador específico**: para importar un controlador específico desde una carpeta, especifique la ruta de acceso de red (UNC) del archivo Txtsetup.oem de almacenamiento o .INF del controlador de dispositivo de Windows.  

    -   **Especificar la opción para controladores duplicados**: seleccione cómo desea que Configuration Manager administre las categorías de controladores cuando se importe un controlador de dispositivo duplicado.  

    > [!IMPORTANT]  
    >  Cuando se importan controladores, el servidor de sitio debe tener permiso de **lectura** en la carpeta o se producirá un error en la importación.  

5.  En la página **Detalles del controlador** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**:  

    -   **Ocultar los controladores que no sean de almacenamiento o red (para imágenes de arranque)**: use esta opción para mostrar solo los controladores de almacenamiento y de red, y para ocultar otros controladores que no suelen ser necesarios para las imágenes de arranque, como un controlador de vídeo o de módem.  

    -   **Ocultar los controladores que no estén firmados digitalmente**: use esta opción para ocultar los controladores que no estén firmados digitalmente.  

    -   En la lista de controladores, seleccione los controladores que desee importar en el catálogo de controladores.  

    -   **Habilitar estos controladores y permitir que los equipos los instalen**: seleccione esta opción para permitir que los equipos instalen los controladores de dispositivo. De forma predeterminada, esta casilla está activada.  

        > [!IMPORTANT]  
        >  Si un controlador de dispositivo causa un problema o desea suspender la instalación de un controlador de dispositivo, puede deshabilitarlo si desactiva la casilla **Habilitar estos controladores y permitir que los equipos los instalen** . También puede deshabilitar controladores después de haberlos importado.  

    -   Para asignar controladores de dispositivos a una categoría administrativa con propósitos de filtrado, como las categorías de "Equipos de escritorio" o "Blocs de notas", haga clic en **Categorías** y seleccione una categoría existente o cree una nueva categoría. También puede usar la asignación de categorías para configurar los controladores de dispositivos que se aplican a la implementación por el paso de la secuencia de tareas [Aplicar controladores automáticamente](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).  

6.  En la página **Agregar controlador a paquetes** , elija si quiere agregar los controladores a un paquete y, después, haga clic en **Siguiente**. Tenga en cuenta lo siguiente para agregar los controladores a un paquete:  

    -   Seleccione los paquetes de controladores que se utilizan para distribuir los controladores de dispositivos.  

         O, si lo desea, haga clic en **Nuevo paquete** para crear un nuevo paquete de controladores. Cuando cree un nuevo paquete de controladores, debe proporcionar un recurso compartido de red que no use ningún otro paquete de controladores.  

    -   Si el paquete ya se distribuyó a los puntos de distribución, haga clic en **Sí** en el cuadro de diálogo para actualizar las imágenes de arranque en los puntos de distribución. No puede utilizar controladores de dispositivos hasta que se distribuyen a los puntos de distribución. Si hace clic en **No**, debe ejecutar la acción **Actualizar punto de distribución** antes de que la imagen de arranque contenga los controladores actualizados. Si el paquete de controladores no se distribuyó nunca, debe hacer clic en **Distribuir contenido** en el nodo **Paquetes de controladores** .  

7.  En la página **Agregar controlador a imágenes de arranque** , elija si desea agregar los controladores de dispositivos a imágenes de arranque existentes y, después, haga clic en **Siguiente**. Si selecciona una imagen de arranque, tenga en cuenta lo siguiente:  

    > [!NOTE]  
    >  Se recomienda que solo agregue controladores de dispositivos de red y almacenamiento masivo a las imágenes de arranque para escenarios de implementación de sistema operativo.  

    -   Haga clic en **Sí** en el cuadro de diálogo para actualizar las imágenes de arranque en los puntos de distribución. No puede utilizar controladores de dispositivos hasta que se distribuyen a los puntos de distribución. Si hace clic en **No**, debe ejecutar la acción **Actualizar punto de distribución** antes de que la imagen de arranque contenga los controladores actualizados. Si el paquete de controladores no se distribuyó nunca, debe hacer clic en **Distribuir contenido** en el nodo **Paquetes de controladores** .  

    -   Configuration Manager le advierte si la arquitectura de uno o varios controladores no coincide con la arquitectura de las imágenes de arranque que seleccionó. Si no coincide, haga clic en **Aceptar** y vuelva a la página **Detalles del controlador** para borrar los controladores que no coinciden con la arquitectura de la imagen de arranque seleccionada. Por ejemplo, si selecciona una imagen de arranque x64 y x86, todos los controladores deben admitir ambas arquitecturas. Si selecciona una imagen de arranque x64, todos los controladores deben admitir la arquitectura x64.  

        > [!NOTE]  
        >  -   La arquitectura se basa en la arquitectura que se indica en el archivo .INF del fabricante.  
        > -   Si un controlador indica que es compatible con ambas arquitecturas, puede importarlo en ambas imágenes de arranque.  

    -   Configuration Manager le advierte si agrega controladores de dispositivos que no son controladores de red o de almacenamiento a una imagen de arranque, porque en la mayoría de los casos no son necesarios para la imagen de arranque. Haga clic en **Sí** para agregar los controladores a la imagen de arranque o **No** para volver atrás y modificar la selección de controladores.  

    -   Configuration Manager le advierte si uno o varios de los controladores seleccionados no están firmados digitalmente de forma correcta. Haga clic en **Sí** para continuar y haga clic en **No** para volver atrás y cambiar la selección de controladores.  

8.  Complete el asistente.  

###  <a name="BKMK_ModifyDriverPackage"></a> Administrar controladores de dispositivos en un paquete de controladores  
 Utilice los procedimientos siguientes para modificar paquetes de controladores e imágenes de arranque. Para agregar o quitar controladores de dispositivos, busque los controladores en el nodo **Controladores** y, a continuación, edite los paquetes o imágenes de arranque a los que están asociados los controladores seleccionados.  

#### <a name="to-modify-the-device-drivers-in-a-driver-package"></a>Para modificar los controladores de dispositivos en un paquete de controladores  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Controladores**.  

3.  En el nodo **Controladores** , seleccione los controladores de dispositivos que desee agregar al paquete de controladores.  

4.  En la pestaña **Inicio** , en el grupo **Controlador** , haga clic en **Editar**y, a continuación, haga clic en **Paquetes de controladores**.  

5.  Para agregar un controlador de dispositivo, active la casilla de los paquetes de controladores a los que desee agregar el controlador de dispositivo. Para quitar un controlador de dispositivo, desactive la casilla de los paquetes de controladores de los que desee quitar el controlador de dispositivo.  

     Si está agregando controladores de dispositivos asociados a paquetes de controladores, tiene la opción de crear un nuevo paquete. Para ello, haga clic en **Nuevo paquete**, que abre el cuadro de diálogo **Nuevo paquete de controladores.  

6.  Si el paquete ya se distribuyó a los puntos de distribución, haga clic en **Sí** en el cuadro de diálogo para actualizar las imágenes de arranque en los puntos de distribución. No puede utilizar controladores de dispositivos hasta que se distribuyen a los puntos de distribución. Si hace clic en **No**, debe ejecutar la acción **Actualizar punto de distribución** antes de que la imagen de arranque contenga los controladores actualizados. Si el paquete de controladores no se distribuyó nunca, debe hacer clic en **Distribuir contenido** en el nodo **Paquetes de controladores** . Para que los controladores estén disponibles, debe actualizar el paquete de controladores en los puntos de distribución.  

     Haga clic en **Aceptar**.  

###  <a name="BKMK_ManageDriversBootImage"></a> Administrar controladores de dispositivos en una imagen de arranque  
 Puede agregar a imágenes de arranque los controladores de dispositivos de Windows que se han importado en el catálogo de controladores. Use las siguientes directrices al agregar controladores de dispositivos a una imagen de arranque:  

-   Solo agregue controladores de dispositivos de adaptadores de red y almacenamiento a las imágenes de arranque: habitualmente no se requieren otros tipos de controladores. La incorporación de controladores que no son necesarios aumenta el tamaño de la imagen de arranque innecesariamente.  

-   Agregue solo controladores de dispositivos para Windows 10 a la imagen de arranque, ya que la versión requerida de Windows PE se basa en Windows 10.  

-   Asegúrese de que usa el controlador de dispositivo correcto para la arquitectura de la imagen de arranque.  No agregue un controlador de dispositivo x86 a una imagen de arranque x64.  

 Use el siguiente procedimiento para agregar o quitar controladores de dispositivos en una imagen de arranque.  

#### <a name="to-modify-the--device-drivers-associated-with-a-boot-image"></a>Para modificar los controladores de dispositivos asociados a una imagen de arranque  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Controladores**.  

3.  En el nodo **Controladores** , seleccione los controladores de dispositivos que desee agregar al paquete de controladores.  

4.  En la pestaña **Inicio** , en el grupo **Controlador** , haga clic en **Editar**y, a continuación, haga clic en **Imágenes de arranque**.  

5.  Para agregar un controlador de dispositivo, active la casilla de la imagen de arranque a la que desee agregar el controlador de dispositivo. Para quitar un controlador de dispositivo, desactive la casilla de la imagen de arranque de la que desee quitar el controlador de dispositivo.  

6.  Si no desea actualizar los puntos de distribución donde se almacena la imagen de arranque, desactive la casilla **Actualizar puntos de distribución cuando termine** . De forma predeterminada, los puntos de distribución se actualizan cuando se actualiza la imagen de arranque.  

     Haga clic en **Aceptar** y tenga en cuenta lo siguiente:  

    -   Haga clic en **Sí** en el cuadro de diálogo para actualizar las imágenes de arranque en los puntos de distribución. No puede utilizar controladores de dispositivos hasta que se distribuyen a los puntos de distribución. Si hace clic en **No**, debe ejecutar la acción **Actualizar punto de distribución** antes de que la imagen de arranque contenga los controladores actualizados. Si el paquete de controladores no se distribuyó nunca, debe hacer clic en **Distribuir contenido** en el nodo **Paquetes de controladores** .  

    -   Configuration Manager le advierte si la arquitectura de uno o varios controladores no coincide con la arquitectura de las imágenes de arranque que seleccionó. Si no coincide, haga clic en **Aceptar** y vuelva a la página **Detalles del controlador** para borrar los controladores que no coinciden con la arquitectura de la imagen de arranque seleccionada. Por ejemplo, si selecciona una imagen de arranque x64 y x86, todos los controladores deben admitir ambas arquitecturas. Si selecciona una imagen de arranque x64, todos los controladores deben admitir la arquitectura x64.  

        > [!NOTE]  
        >  -   La arquitectura se basa en la arquitectura que se indica en el archivo .INF del fabricante.  
        > -   Si un controlador indica que es compatible con ambas arquitecturas, puede importarlo en ambas imágenes de arranque.  

    -   Configuration Manager le advierte si agrega controladores de dispositivos que no son controladores de red o de almacenamiento a una imagen de arranque, porque en la mayoría de los casos no son necesarios para la imagen de arranque. Haga clic en **Sí** para agregar los controladores a la imagen de arranque o **No** para volver atrás y modificar la selección de controladores.  

    -   Configuration Manager le advierte si uno o varios de los controladores seleccionados no están firmados digitalmente de forma correcta. Haga clic en **Sí** para continuar y haga clic en **No** para volver atrás y cambiar la selección de controladores.  

7.  Haga clic en **Aceptar**.  

###  <a name="BKMK_DriverActions"></a> Acciones adicionales para controladores de dispositivos  
 Se pueden realizar otras acciones para administrar controladores de dispositivos cuando se seleccione uno o varios controladores de dispositivos del nodo **Controladores** . Estas acciones incluyen las siguientes:  

|Acción|Descripción|  
|------------|-----------------|  
|**Clasificar**|Borra, administra o establece una categoría administrativa para los controladores de dispositivos seleccionados.|  
|**Eliminar**|Quita el controlador de dispositivo del nodo **Controladores** y también quita el controlador de los puntos de distribución asociados.|  
|**Deshabilitar**|Impide que el controlador de dispositivo se instale. Puede deshabilitar temporalmente controladores de dispositivos de forma que los equipos cliente de Configuration Manager y las secuencias de tareas no puedan instalarlos cuando se implementen sistemas operativos. **Nota**  : La acción de deshabilitación solo impide que los controladores realicen la instalación mediante el paso de la secuencia de tareas Aplicar controladores automáticamente.|  
|**Habilitar**|Permite a los equipos cliente de Configuration Manager y las secuencias de tareas instalar el controlador de dispositivo cuando se implementa el sistema operativo.|  
|**Moverr**|Mueve el controlador de dispositivo a otra carpeta en el nodo **Controladores** .|  
|**Propiedades**|Abre el cuadro de diálogo **Propiedades** , donde puede revisar y cambiar las propiedades del controlador de dispositivo. Por ejemplo, puede cambiar el nombre y la descripción del controlador de dispositivo, habilitarlo y especificar en qué plataformas se puede ejecutar.|  

##  <a name="BKMK_TSDrivers"></a> Usar secuencias de tareas para instalar controladores de dispositivos  
 Use secuencias de tareas para automatizar la implementación del sistema operativo. Cada paso en la secuencia de tareas puede realizar una acción determinada como, por ejemplo, la instalación de un controlador de dispositivo. Puede usar estos dos pasos de secuencia de tareas para instalar controladores de dispositivos durante la implementación de sistemas operativos:  

-   [Aplicar controladores automáticamente	](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers): esta etapa le permite encontrar controladores de dispositivos coincidentes e instalarlos automáticamente como parte de una implementación de sistema operativo. Puede configurar el paso de la secuencia de tareas para instalar solo los controladores más coincidentes para los dispositivos de hardware detectados, o especificar que el paso de la secuencia de tareas instale todos los controladores admitidos de los dispositivos de hardware detectados y, a continuación, dejar al programa de instalación de Windows seleccionar el controlador más adecuado. Además, puede especificar una categoría de controladores de dispositivos para limitar los controladores que están disponibles en este paso.  

-   [Aplicar paquete de controladores](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage): esta etapa le permite poner todos los controladores de dispositivos en un determinado paquete de controladores a disposición del programa de instalación de Windows. El programa de instalación de Windows busca los controladores de dispositivos necesarios en los paquetes de controladores especificados. Al crear medios independientes, debe usar esta etapa para instalar controladores de dispositivos.  

 Al usar estos pasos de la secuencia de tareas, también puede especificar cómo se instalan los controladores de dispositivos en el equipo en el que se implementa el sistema operativo. Para obtener más información, vea [Manage task sequences to automate tasks](../deploy-use/manage-task-sequences-to-automate-tasks.md) (Administración de secuencias de tareas para automatizar tareas).  

##  <a name="BKMK_InstallingDeviceDiriversTS"></a> Usar secuencias de tareas para instalar controladores de dispositivos en equipos  
 Utilice el procedimiento siguiente para instalar controladores de dispositivos como parte de la implementación de sistema operativo.  

#### <a name="use-a-task-sequence-to-install-device-drivers"></a>Usar una secuencia de tareas para instalar controladores de dispositivos  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En el nodo **Secuencia de tareas** , seleccione la secuencia de tareas que desea modificar para instalar el controlador de dispositivos y, a continuación, haga clic en **Editar**.  

4.  Vaya a la ubicación en la que desea agregar pasos de **Controlador** , haga clic en **Agregar**y, a continuación, seleccione **Controladores**.  

5.  Agregue el paso **Aplicar controladores automáticamente** si desea que la secuencia de tareas instale todos los controladores de dispositivos o las categorías especificadas. Especifique las opciones del paso en la pestaña **Propiedades** y todas las condiciones del paso en la pestaña **Opciones** .  

     Agregue el paso **Aplicar paquete de controladores** si desea que la secuencia de tareas instale solo los controladores de dispositivo del paquete especificado. Especifique las opciones del paso en la pestaña **Propiedades** y todas las condiciones del paso en la pestaña **Opciones** .  

    > [!IMPORTANT]  
    >  También puede seleccionar **Deshabilitar esta etapa** en la pestaña **Opciones** para deshabilitar la etapa si es preciso solucionar problemas de la secuencia de tareas.  

6.  Haga clic en **Aceptar** para guardar la secuencia de tareas.  

 Para obtener más información sobre cómo crear una secuencia de tareas para instalar un sistema operativo, vea [Create a task sequence to install an operating system](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md) (Creación de una secuencia de tareas para instalar un sistema operativo).  

##  <a name="BKMK_DriverReports"></a> Informes de administración de controladores  
 Puede usar varios informes en la categoría de informes **Administración de controladores** para obtener información general acerca de los controladores de dispositivos en el catálogo de controladores. Para obtener más información sobre informes, consulte [Generación de informes](../../core/servers/manage/reporting.md).
