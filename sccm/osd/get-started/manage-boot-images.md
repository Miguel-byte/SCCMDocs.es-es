---
title: 'Administrar imágenes de arranque '
titleSuffix: Configuration Manager
description: En Configuration Manager, aprenda a administrar las imágenes de arranque de Windows PE que se usan durante una implementación de sistema operativo.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b0fa269199f7f3bf4299f90faef9e55766f775d4
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421338"
---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>Administrar imágenes de arranque con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Una imagen de arranque de Configuration Manager es una imagen de [Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) (WinPE) que se usa durante la implementación de un sistema operativo. Las imágenes de arranque se usan para iniciar un equipo en WinPE. Este sistema operativo mínimo contiene servicios y componentes limitados. Configuration Manager usa WinPE para preparar el equipo de destino para la instalación de Windows. Utilice las siguientes secciones para administrar imágenes de arranque:

## <a name="BKMK_BootImageDefault"></a> Imágenes de arranque predeterminadas
Configuration Manager proporciona dos imágenes de arranque predeterminadas: Una para plataformas x86 y otra para plataformas x64. Estas imágenes se almacenan en: \\\\*NombreDeServidor*>\SMS_<*códigoDeSitio*>\osd\boot\\<*x64*> o <*i386*>. Las imágenes de arranque predeterminadas se actualizan o se vuelven a generar según la acción que realice.

Tenga en cuenta los comportamientos siguientes de cualquiera de las acciones descritas para las imágenes de arranque predeterminadas:
- Los objetos de controlador de origen deben ser válidos. Estos objetos incluyen los archivos de origen del controlador. Si los objetos no son válidos, el sitio no agrega los controladores a las imágenes de arranque.
- No se modifican las imágenes de arranque que no estén basadas en las imágenes de arranque predeterminadas, incluso si usan la misma versión de Windows PE.
- Vuelva a distribuir las imágenes de arranque modificadas en los puntos de distribución.
- Vuelva a crear los medios que usen las imágenes de arranque modificadas.
- Si no quiere que las imágenes de arranque predeterminadas o personalizadas se actualicen automáticamente, no las almacene en la ubicación predeterminada.

> [!NOTE]
> La herramienta de registro de seguimiento de Configuration Manager (CMTrace) se agrega a todas las imágenes de arranque en la **Biblioteca de software**. Cuando esté en Windows PE, inicie la herramienta escribiendo **CMTrace** desde el símbolo del sistema. A partir de la versión 1802, al iniciar cmtrace.exe en Windows PE, ya no se le solicita que elija si este programa se establece como el visor predeterminado para los archivos de registro.

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Uso de las actualizaciones y el mantenimiento para instalar la última versión de Configuration Manager
A partir de la versión 1702, al actualizar la versión de Windows Assessment and Deployment Kit (ADK), y después usar las actualizaciones para instalar la última versión de Configuration Manager, el sitio regenera las imágenes de arranque predeterminadas. Esta actualización incluye la nueva versión de WinPE de Windows ADK actualizado y la versión nueva del cliente de Configuration Manager, los controladores y las personalizaciones. El sitio no modifica las imágenes de arranque personalizadas.

En versiones anteriores a 1702, Configuration Manager actualiza la imagen de arranque existente con los componentes de cliente, los controladores y las personalizaciones, pero no usa la última versión de WinPE desde Windows ADK. Modifique manualmente la imagen de arranque para usar la nueva versión de Windows ADK.

### <a name="upgrade-from-configuration-manager-2012-to-configuration-manager-current-branch-cb"></a>Actualización desde Configuration Manager 2012 a la rama actual (CB) de Configuration Manager
Cuando se actualiza Configuration Manager 2012 a la rama actual (CB) de Configuration Manager mediante el proceso de instalación, el sitio regenera las imágenes de arranque predeterminadas. Esta actualización incluye la versión nueva de WinPE de Windows ADK actualizado y la versión nueva del cliente de Configuration Manager. Todas las personalizaciones de imagen de arranque permanecen sin cambios. El sitio no modifica las imágenes de arranque personalizadas.

### <a name="update-distribution-points-with-the-boot-image"></a>Actualización de puntos de distribución con la imagen
Cuando se usa la acción **Actualizar puntos de distribución** del nodo **Imágenes de arranque** en la consola, el sitio actualiza la imagen de arranque de destino con los componentes de cliente, los controladores y las personalizaciones.    

A partir de la versión 1706 de Configuration Manager, vuelva a cargar la imagen de arranque con la versión más reciente de WinPE desde el directorio de instalación de Windows ADK. En la página **General** del Asistente para actualizar puntos de distribución se proporciona la información siguiente: 
 - La versión de Windows ADK instalada en el servidor de sitio.
 - La versión de Windows ADK de WinPE en la imagen de arranque.
 - La versión del cliente de Configuration Manager. Use esta información para decidir si se debe volver a cargar la imagen de arranque. En el nodo **Imágenes de arranque** también se incluye una columna nueva para (**Versión del cliente**). Use esta columna para ver rápidamente la versión del cliente de Configuration Manager en cada imagen de arranque.    


##  <a name="BKMK_BootImageCustom"></a> Personalización de una imagen de arranque  
 Cuando una imagen de arranque se basa en una versión de WinPE desde la versión admitida de Windows ADK, puede personalizar o [modificar una imagen de arranque](#BKMK_ModifyBootImages), desde la consola. Cuando se actualiza un sitio con una versión nueva y se instala una versión nueva de Windows ADK, las imágenes de arranque personalizadas (que no se encuentran en la ubicación de la imagen de arranque predeterminada) no se actualizan con la versión nueva de Windows ADK. Si esto ocurre, no podrá personalizar las imágenes de arranque en la consola de Configuration Manager. Pero continuarán funcionando como lo hacían antes de la actualización.  

 Si una imagen de arranque se basa en otra versión de Windows ADK instalada en un sitio, debe personalizar las imágenes de arranque. Use otro método para personalizar estas imágenes de arranque, como la herramienta de línea de comandos Administración y mantenimiento de imágenes de implementación (DISM). DISM forma parte de Windows ADK. Para obtener más información, consulte [Customize boot images](customize-boot-images.md) (Personalización de imágenes de arranque).  

##  <a name="BKMK_AddBootImages"></a> Incorporación de una imagen de arranque  

 Durante la instalación de sitio, Configuration Manager agrega automáticamente imágenes de arranque basadas en una versión de WinPE desde la versión admitida de Windows ADK. Según la versión de Configuration Manager, es posible que pueda agregar imágenes de arranque basadas en una versión de WinPE desde la versión admitida de Windows ADK. Se produce un error al intentar agregar una imagen de arranque que contiene una versión no admitida de WinPE. En la lista siguiente se muestran las versiones de Windows ADK y WinPE que se admiten actualmente: 

- **Versión de Windows ADK**  

   Windows ADK para Windows 10  

- **Versiones de Windows PE para imágenes de arranque personalizables desde la consola de Configuration Manager**  

   Windows PE 10  

- **Versiones admitidas de Windows PE para imágenes de arranque que no se pueden personalizar desde la consola de Configuration Manager**  

   Windows PE 3.1<sup>1</sup> y Windows PE 5  

   <sup>1</sup> Solo se puede agregar una imagen de arranque a Configuration Manager si se basa en Windows PE 3.1. Actualice el AIK de Windows para Windows 7 (basado en Windows PE 3.0) con el complemento de AIK de Windows para Windows 7 SP1 (basado en Windows PE 3.1). Descargue el complemento de AIK de Windows para Windows 7 SP1 en el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

   Por ejemplo, use la consola de Configuration Manager para personalizar las imágenes de arranque basadas en Windows PE 10 desde Windows ADK para Windows 10. Para una imagen de arranque basada en Windows PE 5, personalícela desde otro equipo con la versión de DISM de Windows ADK para Windows 8. Después, agregue la imagen de arranque personalizada a la consola de Configuration Manager. Para obtener más información, consulte [Customize boot images](customize-boot-images.md) (Personalización de imágenes de arranque).

  Use el siguiente procedimiento para agregar una imagen de arranque manualmente.  

#### <a name="to-add-a-boot-image"></a>Para agregar una imagen de arranque  

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2. En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Imágenes de arranque**.  

3. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Agregar imagen de arranque** para iniciar el Asistente para agregar imagen de archivo.  

4. En la página **Origen de datos** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**:  

   -   En el cuadro **Ruta de acceso** , especifique la ruta de acceso del archivo WIM de imagen de arranque.  

        La ruta de acceso especificada debe ser una ruta de acceso de red válida con el formato UNC. Por ejemplo: \\\\<*nombreDeServidor*\\<*nombreRecursoCompartido*>\\<*nombreImagenArranque*> WIM.  

   -   Seleccione la imagen de arranque de la lista desplegable **Imagen de arranque** . Si el archivo WIM contiene varias imágenes de arranque, seleccione la imagen apropiada.  

5. En la página **General**  , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

   -   En el cuadro **Nombre** , especifique un nombre único para la imagen de arranque.  

   -   En el cuadro **Versión** , especifique un número de versión para la imagen de arranque.  

   -   En el cuadro **Comentario** , especifique una descripción breve sobre cómo se utiliza la imagen de arranque.  

6. Complete el asistente.  

   La imagen de arranque se muestra en el nodo **Imagen de arranque** de la consola de Configuration Manager. Antes de usar la imagen de arranque para implementar un sistema operativo, distribúyala a los puntos de distribución. 

> [!NOTE]  
>  En el nodo **Imagen de arranque** de la consola, en la columna **Tamaño (KB)** se muestra el tamaño descomprimido de cada imagen de arranque. Cuando el sitio envía una imagen de arranque a través de la red, envía una copia comprimida. Esta copia normalmente es más pequeña que el tamaño que se muestra en la columna **Tamaño (KB)**.  

##  <a name="BKMK_DistributeBootImages"></a> Distribución de imágenes de arranque a un punto de distribución  
 Las imágenes de arranque se distribuyen a los puntos de distribución de la misma forma en que se reparte otro tipo de contenido. En la mayoría de los casos, debe distribuir la imagen de arranque a un punto de distribución como mínimo, antes de implementar un sistema operativo y de crear medios.   

> [!NOTE]  
> Para usar PXE para implementar un sistema operativo, considere los aspectos siguientes antes de distribuir la imagen de arranque:  
> - Configure el punto de distribución para aceptar solicitudes PXE.  
> - Distribuya una imagen de arranque x86 y x64 habilitada para PXE a un punto de distribución habilitado para PXE como mínimo.  
> - Configuration Manager distribuye las imágenes de arranque a la carpeta **RemoteInstall** en el punto de distribución habilitado para PXE.  
>   
> Para obtener más información sobre el uso de PXE para implementar sistemas operativos, consulte [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Uso de PXE para implementar Windows a través de la red).  

 Para conocer los pasos de distribución de una imagen de arranque, consulte [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute) (Distribuir contenido).  

##  <a name="BKMK_ModifyBootImages"></a> Modificación de una imagen de arranque  
 Puede agregar o quitar controladores de dispositivo para la imagen o editar las propiedades asociadas a la imagen de arranque. Los controladores de dispositivo que agregue o quite pueden incluir adaptadores de red o controladores de dispositivo de almacenamiento masivo. Tenga en cuenta los siguientes factores al modificar imágenes de arranque:  

- Importe y habilite los controladores de dispositivo en el catálogo de controladores de dispositivo antes de agregarlos a la imagen de arranque.  

- Al modificar una imagen de arranque, dicha imagen no cambia ninguno de los paquetes asociados a los que hace referencia.  

- Después de realizar cambios en una imagen de arranque, **actualícela** en los puntos de distribución que ya la tienen. Este proceso hace que la versión más reciente de la imagen de arranque esté disponible para los clientes. Para obtener más información, vea [Manage content you have distributed](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage) (Administración del contenido que ha distribuido).  

  Use el procedimiento siguiente para modificar una imagen de arranque.  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>Para modificar las propiedades de una imagen de arranque  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Imágenes de arranque**.  

3.  Seleccione la imagen de arranque que desee modificar.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades** para abrir el cuadro de diálogo **Propiedades** de la imagen de arranque.  

5.  Defina cualquiera de las siguientes opciones para cambiar el comportamiento de la imagen de arranque:  

    -   En la pestaña **Imágenes** , si cambió las propiedades de la imagen de arranque mediante una herramienta externa, haga clic en **Recargar**.  

    -   En la ficha **Controladores** , agregue los controladores de dispositivo de Windows necesarios para arrancar WinPE. Tenga en cuenta los aspectos siguientes cuando agregue controladores de dispositivo:  

        -   Seleccione **Ocultar controladores que no coincidan con la arquitectura de la imagen de arranque** para mostrar solo los controladores para la arquitectura de la imagen de arranque. La arquitectura se basa en la arquitectura que se indica en el archivo INF del fabricante.  

        -   Seleccione **Ocultar los controladores que no sean de almacenamiento o red (para imágenes de arranque)** para mostrar solo los controladores de almacenamiento y de red. Esta opción también oculta otros controladores que no suelen ser necesarios para las imágenes de arranque, como un controlador de vídeo o de módem.  

        -   Seleccione **Ocultar los controladores que no estén firmados digitalmente** para ocultar los controladores que no tengan una firma digital válida.  

        -   Como procedimiento recomendado, agregue solo controladores de red y almacenamiento masivo a la imagen de arranque, a menos que existan requisitos para otros controladores en WinPE.  

        -   Dado que WinPE ya viene con muchos controladores integrados, agregue solo los controladores de red y almacenamiento masivo que no se incluyan con WinPE.  

        -   Asegúrese de que los controladores que se agregan a la imagen de arranque coinciden con la arquitectura de la imagen de arranque.  

        > [!NOTE]  
        >  Debe importar los controladores de dispositivos en el catálogo de controladores antes de agregarlos a una imagen de arranque. Para más información sobre cómo importar controladores de dispositivo, consulte [Manage drivers](manage-drivers.md) (Administración de controladores).  

    -   En la pestaña **Personalización** , seleccione cualquiera de las siguientes opciones:  

        -   Active la casilla **Habilitar comando de preinicio** para especificar que se ejecute un comando antes de que se ejecute la secuencia de tareas. Cuando habilite esta opción, especifique también la línea de comandos que se va a ejecutar y los archivos de compatibilidad requeridos por el comando.  

            > [!WARNING]  
            >  Agregue **cmd /c** al principio de la línea de comandos. Si no se especifica **cmd /c**, el comando no se cerrará después de ejecutarlo. La implementación sigue a la espera de que finalice el comando y no se iniciará ningún otro comando o acción que se hayan configurado.  

            > [!TIP]  
            >  Durante la creación de los medios de secuencia de tareas, el asistente escribe el identificador de paquete y la línea de comandos de preinicio, incluidos los valores de las variables de secuencia de tareas, en el archivo de registro CreateTSMedia.log. Este registro se encuentra en el equipo que ejecuta la consola de Configuration Manager. Revise este archivo de registro para comprobar el valor de las variables de secuencia de tareas.  

        -   Defina los valores de **Fondo de Windows PE** para especificar si quiere usar el fondo predeterminado de WinPE o un fondo personalizado.  

        -   Seleccione **Habilitar compatibilidad de comando (solo prueba)** para abrir un símbolo del sistema mediante la tecla **F8** mientras se implementa la imagen de arranque. Esta opción es útil para solucionar problemas mientras se prueba la implementación. No se recomienda usar esta opción en una implementación de producción.  

        -   Configure el espacio de desecho de Windows PE, que es el almacenamiento temporal (unidad RAM) usado por WinPE. Por ejemplo, cuando se ejecuta una aplicación en WinPE y necesita escribir archivos temporales, WinPE redirige los archivos al espacio de desecho en la memoria para simular la presencia de un disco duro. De forma predeterminada, WinPE asigna 32 megabytes (MB) de memoria grabable.  

    -   En la pestaña **Origen de datos** , actualice cualquiera de las siguientes opciones:  

        -   Para cambiar el archivo de origen de la imagen de arranque, establezca **Ruta de acceso de la imagen** e **Índice de imágenes**.  

        -   Para crear una programación para cuando el sitio actualice la imagen de arranque, seleccione **Actualizar puntos de distribución en una programación**.  

        -   Si no quiere que el contenido de este paquete deje la caché de cliente para hacer sitio a otro contenido, seleccione **Conservar contenido en caché de cliente**.  

        -   Para especificar que el sitio solo distribuya los archivos cambiados cuando actualice el paquete de imagen de arranque en el punto de distribución, seleccione **Habilitar replicación diferencial binaria** (BDR). Esta configuración minimiza el tráfico de red entre sitios. La BDR es especialmente útil cuando el paquete de imagen de arranque es grande y los cambios son relativamente pequeños.  

        -   Si la imagen de arranque se usa en una implementación habilitada para PXE, seleccione **Implementar esta imagen de arranque desde el punto de distribución habilitado con PXE**.  

            > [!NOTE]  
            >  Para obtener más información, vea [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Uso de PXE para implementar Windows a través de la red).  

    -   En la pestaña **Acceso a datos** , seleccione cualquiera de las siguientes opciones:  

        -   Defina la **Configuración del recurso compartido de paquete** si desea que los clientes instalen el contenido de este paquete desde la red.  

        -   Establezca la **Configuración de la actualización del paquete** para especificar cómo desea que desconecte a los usuarios desde el punto de distribución. Es posible que Configuration Manager no pueda actualizar la imagen de arranque cuando los usuarios están conectados al punto de distribución.  

    -   En la pestaña **Configuración de distribución** , seleccione cualquiera de las siguientes opciones:  

        -   En la lista **Prioridad de distribución**, especifique el nivel de prioridad. Configuration Manager usa esta lista de prioridad cuando el sitio distribuye varios paquetes en el mismo punto de distribución.  

        -   Si quiere habilitar la distribución de contenido a petición en puntos de distribución preferidos, seleccione **Distribuir el contenido de este paquete en puntos de distribución preferidos**. Cuando se habilita esta opción, si un cliente solicita el contenido del paquete y el contenido no está disponible en ningún punto de distribución preferido, el punto de administración distribuye el contenido en todos los puntos de distribución preferidos.  

        -   Para especificar cómo quiere que el sitio distribuya la imagen de arranque en los puntos de distribución habilitados para el contenido preconfigurado, establezca la **Configuración de punto de distribución preconfigurado**.  

            > [!NOTE]  
            >  Para más información sobre el contenido preconfigurado, consulte [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage) (Preconfigurar el contenido).  

    -   En la pestaña **Ubicaciones de contenido** , seleccione el punto de distribución o el grupo de puntos de distribución y realice cualquiera de las siguientes acciones:  

        -   Haga clic en **Redistribuir** para distribuir de nuevo la imagen de arranque en el punto de distribución o el grupo de puntos de distribución seleccionado.  

        -   Haga clic en **Validar** para comprobar la integridad del paquete de imagen de arranque en el punto de distribución o el grupo de puntos de distribución seleccionado.  

    -   En la pestaña **Componentes opcionales**, especifique los componentes agregados a Windows PE para su uso con Configuration Manager. Para obtener más información sobre los componentes opcionales, vea [WinPE: agregar paquetes (referencia de los componentes opcionales)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

    -   En la pestaña **Seguridad** , seleccione un usuario administrativo y cambie las operaciones que puede realizar.  

6.  Después de configurar las propiedades, haga clic en **Aceptar**.  

##  <a name="BKMK_BootImagePXE"></a> Configuración de una imagen de arranque para implementar desde un punto de distribución habilitado con PXE  
 Para poder usar una imagen de arranque para una implementación de sistema operativo PXE, debe configurar la imagen de arranque para que se implemente desde un punto de distribución habilitado con PXE.  

#### <a name="to-configure-a-boot-image-to-deploy-from-a-pxe-enabled-distribution-point"></a>Para configurar una imagen de arranque para implementar desde un punto de distribución habilitado con PXE  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Imágenes de arranque**.  

3.  Seleccione la imagen de arranque que desee modificar.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades** para abrir el cuadro de diálogo **Propiedades** de la imagen de arranque.  

5.  En la pestaña **Origen de datos** , seleccione **Implementar esta imagen de arranque desde el punto de distribución habilitado con PXE**.  

    > [!NOTE]  
    >  Para obtener más información, vea [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Uso de PXE para implementar Windows a través de la red).  

6.  Después de configurar las propiedades, haga clic en **Aceptar**.  

##  <a name="BKMK_BootImageLanguage"></a> Configuración de varios idiomas para la implementación de una imagen de arranque  
 Las imágenes de arranque son independientes del idioma. Esta funcionalidad permite usar una imagen de arranque para mostrar el texto de la secuencia de tareas en varios idiomas en WinPE. Incluya la compatibilidad de idioma adecuada de la pestaña **Componentes opcionales** de la imagen de arranque. Después, establezca la variable de secuencia de tareas correspondiente para indicar el idioma que se va a mostrar. El idioma del sistema operativo implementado es independiente del idioma de WinPE. El idioma que WinPE muestra al usuario se determina de la manera siguiente:  

- Cuando un usuario ejecuta la secuencia de tareas desde un sistema operativo existente, Configuration Manager utiliza automáticamente el idioma configurado para el usuario. Cuando la secuencia de tareas se ejecuta automáticamente como resultado de una fecha límite de implementación obligatoria, Configuration Manager utiliza el idioma del sistema operativo.  

- Para las implementaciones de sistema operativo que usan PXE o medios, establezca el valor del identificador de idioma en la variable **SMSTSLanguageFolder** como parte de un comando de preinicio. Cuando el equipo arranca WinPE, los mensajes se muestran en el idioma que especificó en la variable. Si se produce un error al tener acceso al archivo de recursos de idioma en la carpeta especificada, o bien no se establece la variable, WinPE muestra los mensajes en el idioma predeterminado.  

  > [!NOTE]  
  >  Si el medio está protegido con una contraseña, el texto que solicita la contraseña al usuario siempre se muestra en el idioma de WinPE.  

  Use el procedimiento siguiente para establecer el idioma de WinPE de las implementaciones de sistema operativo iniciadas por un medio o por PXE.  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>Para establecer el idioma de Windows PE de una implementación de sistema operativo iniciada por un medio o por PXE  

1.  Compruebe que el archivo de recursos de secuencia de tareas correcto (tsres.dll) se encuentra en la carpeta de idioma correspondiente en el servidor de sitio antes de actualizar la imagen de arranque. Por ejemplo, el archivo de recursos en inglés está en la ubicación siguiente: <*CarpetaDeInstalaciónDeConfigurationManager*> \OSD\bin\x64\00000409\tsres.dll.  

2.  Como parte de su comando de preinicio, configure la variable de entorno SMSTSLanguageFolder con el identificador de idioma correspondiente. El identificador de idioma no debe especificarse con un formato hexadecimal sino mediante el formato decimal. Por ejemplo, para establecer el Id. de idioma en inglés, especifique el valor decimal 1033, no el valor hexadecimal 00000409 del nombre de carpeta.  
