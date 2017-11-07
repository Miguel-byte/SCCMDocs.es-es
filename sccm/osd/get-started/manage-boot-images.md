---
title: "Administrar imágenes de arranque "
titleSuffix: Configuration Manager
description: "En Configuration Manager, aprenda a administrar las imágenes de arranque de Windows PE que se usan durante una implementación de sistema operativo."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
caps.latest.revision: "23"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 1f169dbf645096777f3fd244d24ca5be92efa180
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>Administrar imágenes de arranque con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Una imagen de arranque de Configuration Manager es una imagen de [Windows PE (WinPE)](https://msdn.microsoft.com/library/windows/hardware/dn938389%28v=vs.85%29.aspx) que se usa durante la implementación de sistema operativo. Las imágenes de arranque se usan para iniciar un equipo en WinPE, que es un sistema operativo mínimo con componentes y servicios limitados que prepara el equipo de destino para la instalación de Windows.  Utilice las siguientes secciones para administrar imágenes de arranque:

## <a name="BKMK_BootImageDefault"></a> Imágenes de arranque predeterminadas
Configuration Manager proporciona dos imágenes de arranque predeterminadas: una compatible con las plataformas x86 y otra compatible con las plataformas x64. Estas imágenes se almacenan en: \\\\*NombreDeServidor*>\SMS_<*códigoDeSitio*>\osd\boot\\<*x64*> o <*i386*>. Las imágenes de arranque predeterminadas se actualizan o se vuelven a generar según la acción que realice.

Tenga en cuenta lo siguiente en cualquiera de las acciones descritas en las secciones siguientes:
- Los objetos de controlador de origen deben ser válidos, incluidos los archivos de origen de controlador; de lo contrario, los controladores no se agregarán a las imágenes de arranque en el sitio.
- Tampoco se modificarán las imágenes de arranque que no estén basadas en las imágenes de arranque predeterminadas, incluso si usan la misma versión de Windows PE.
- Debe redistribuir las imágenes de arranque modificadas a puntos de distribución.
- Debe volver a crear los medios que usen las imágenes de arranque modificadas.
- Si no quiere que las imágenes de arranque predeterminadas o personalizadas se actualicen automáticamente, no las almacene en la ubicación predeterminada.

> [!NOTE]
> La herramienta de registro de seguimiento de Configuration Manager se agrega a todas las imágenes de arranque que se agregan a la **Biblioteca de software**. Cuando esté en Windows PE, puede iniciar la herramienta de registro de seguimiento de Configuration Manager escribiendo **CMTrace** desde un símbolo del sistema.  

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Uso de las actualizaciones y el mantenimiento para instalar la última versión de Configuration Manager
A partir de la versión 1702, al actualizar la versión de Windows ADK y usar las actualizaciones para instalar la última versión de Configuration Manager, este regenerará las imágenes de arranque predeterminadas. Esto incluye la nueva versión de Windows PE a partir del Windows ADK actualizado y la nueva versión del cliente de Configuration Manager, así como los controladores, las personalizaciones, etc. Las imágenes de arranque personalizadas no se verán modificadas.

Antes de la versión 1702, Configuration Manager actualiza la imagen de arranque existente (boot.wim) con los componentes de cliente, los controladores, las personalizaciones, etc., pero no usará la última versión de Windows PE desde Windows ADK. Debe modificar manualmente la imagen de arranque para usar la nueva versión de Windows ADK.

### <a name="upgrade-from-configuration-manager-2012-to-configuration-manager-current-branch-cb"></a>Actualización desde Configuration Manager 2012 a la rama actual (CB) de Configuration Manager
Cuando actualice Configuration Manager 2012 a la rama actual (CB) de Configuration Manager mediante el proceso de instalación, Configuration Manager regenerará las imágenes de arranque predeterminadas. Esto incluye la nueva versión de Windows PE a partir del Windows ADK actualizado, la nueva versión del cliente de Configuration Manager y todas las personalizaciones permanecen sin cambios. Las imágenes de arranque personalizadas no se verán modificadas.

### <a name="update-distribution-points-with-the-boot-image"></a>Actualización de puntos de distribución con la imagen
Cuando use la acción **Actualizar puntos de distribución** desde el nodo **Imágenes de arranque** en la consola de Configuration Manager, Configuration Manager actualiza la imagen de arranque de destino con los componentes de cliente, los controladores, las personalizaciones, etc.    

A partir de la versión 1706 de Configuration Manager, puede volver a cargar la versión más reciente de Windows PE (desde el directorio de instalación de Windows ADK) en la imagen de arranque. La página **General** del Asistente para actualizar puntos de distribución proporciona información sobre la versión de Windows ADK instalada en el servidor de sitio, la versión de Windows ADK desde la que se usó Windows PE en la imagen de arranque y la versión de cliente de Configuration Manager. Puede utilizar esta información para ayudarle a decidir si desea volver a cargar la imagen de arranque. Además, se ha agregado una nueva columna (**Versión del cliente**) al visualizar imágenes de arranque en el nodo **Imágenes de arranque** para que pueda conocer la versión del cliente de Configuration Manager que utiliza cada imagen de arranque.    


##  <a name="BKMK_BootImageCustom"></a> Personalización de una imagen de arranque  
 Puede personalizar una imagen de arranque, o [Modificar una imagen de arranque](#BKMK_ModifyBootImages), desde la consola de Configuration Manager cuando se base en una versión de Windows PE desde la versión admitida de Windows ADK. Cuando se actualiza un sitio con una nueva versión y se instala una nueva versión de Windows ADK, las imágenes de arranque personalizadas (que no se encuentran en la ubicación de la imagen de arranque predeterminada) no se actualizan con la nueva versión de Windows ADK. Si esto ocurre, no podrá personalizar las imágenes de arranque en la consola de Configuration Manager. Sin embargo, continuarán funcionando como lo hacían antes de la actualización.  

 Si una imagen de arranque se basa en una versión de Windows ADK distinta a la que está instalada en un sitio, debe personalizar las imágenes de arranque mediante otros métodos como, por ejemplo, a través de la herramienta de línea de comandos Administración y mantenimiento de imágenes de implementación (DISM) que forma parte de AIK de Windows y Windows ADK. Para obtener más información, consulte [Customize boot images](customize-boot-images.md) (Personalización de imágenes de arranque).  

##  <a name="BKMK_AddBootImages"></a> Incorporación de una imagen de arranque  

 Durante la instalación de sitio, Configuration Manager agrega automáticamente imágenes de arranque basadas en una versión de WinPE desde la versión admitida de Windows ADK. Según la versión de Configuration Manager, es posible que pueda agregar imágenes de arranque basadas en una versión de WinPE desde la versión admitida de Windows ADK.  Se produce un error al intentar agregar una imagen de arranque que contiene una versión no admitida de WinPE.  

 En la tabla siguiente se proporciona la versión admitida de Windows ADK, la versión de Windows PE en la que se basa la imagen de arranque y que se puede personalizar mediante la consola de Configuration Manager, y las versiones de Windows PE en las que se basa la imagen de arranque, que puede personalizar mediante DISM y, después, agregar la imagen a Configuration Manager.  

-   **Versión de Windows ADK**  

     Windows ADK para Windows 10  

-   **Versiones de Windows PE para imágenes de arranque personalizables desde la consola de Configuration Manager**  

     Windows PE 10  

-   **Versiones admitidas de Windows PE para imágenes de arranque que no se pueden personalizar desde la consola de Configuration Manager**  

     Windows PE 3.1<sup>1</sup> y Windows PE 5  

     <sup>1</sup> Solo se puede agregar una imagen de arranque a Configuration Manager si se basa en Windows PE 3.1. Instale el complemento de AIK de Windows para Windows 7 SP1 a fin de actualizar AIK de Windows para Windows 7 (basado en Windows PE 3) con el complemento de AIK de Windows para Windows 7 SP1 (basado en Windows PE 3.1). Puede descargar el complemento de AIK de Windows para Windows 7 SP1 en el [Centro de descarga de Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

     Por ejemplo, si tiene Configuration Manager, puede personalizar imágenes de arranque desde Windows ADK para Windows 10 (basado en Windows PE 10) mediante la consola de Configuration Manager. Sin embargo, aunque se admiten imágenes de arranque basadas en Windows PE 5, debe personalizarlas desde otro equipo y usar la versión de DISM instalada con Windows ADK para Windows 8. Después, puede agregar la imagen de arranque a la consola de Configuration Manager. Para obtener más información sobre los pasos para personalizar una imagen de arranque (agregar componentes y controladores adicionales), habilitar la compatibilidad con comandos en la imagen de arranque, agregar la imagen de arranque a la consola de Configuration Manager y actualizar los puntos de distribución con la imagen de arranque, consulte [Personalizar imágenes de arranque](customize-boot-images.md).

 Use el siguiente procedimiento para agregar una imagen de arranque manualmente.  

#### <a name="to-add-a-boot-image"></a>Para agregar una imagen de arranque  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Imágenes de arranque**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Agregar imagen de arranque** para iniciar el Asistente para agregar imagen de archivo.  

4.  En la página **Origen de datos** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**:  

    -   En el cuadro **Ruta de acceso** , especifique la ruta de acceso del archivo WIM de imagen de arranque.  

         La ruta de acceso especificada debe ser una ruta de acceso de red válida con el formato UNC. Por ejemplo: \\\\<*nombreDeServidor*\\<*nombreRecursoCompartido*>\\<*nombreImagenArranque*> WIM.  

    -   Seleccione la imagen de arranque de la lista desplegable **Imagen de arranque** . Si el archivo WIM contiene varias imágenes de arranque, seleccione la imagen apropiada.  

5.  En la página **General**  , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    -   En el cuadro **Nombre** , especifique un nombre único para la imagen de arranque.  

    -   En el cuadro **Versión** , especifique un número de versión para la imagen de arranque.  

    -   En el cuadro **Comentario** , especifique una descripción breve sobre cómo se utiliza la imagen de arranque.  

6.  Complete el asistente.  

 La imagen de arranque se muestra en el nodo **Imagen de arranque** de la consola de Configuration Manager. No obstante, antes de poder usar la imagen de arranque para implementar un sistema operativo, debe distribuirla en puntos de distribución, grupos de puntos de distribución o recopilaciones asociadas a grupos de puntos de distribución.  

> [!NOTE]  
>  Si selecciona el nodo **Imagen de arranque** en la consola de Configuration Manager, la columna **Tamaño (KB)** muestra el tamaño descomprimido de cada imagen de arranque. Sin embargo, si Configuration Manager envía una imagen de arranque a través de la red, envía una copia comprimida de la imagen, cuyo tamaño es muy inferior al tamaño que se muestra en la columna **Tamaño (KB)**.  

##  <a name="BKMK_DistributeBootImages"></a> Distribución de imágenes de arranque a un punto de distribución  
 Las imágenes de arranque se distribuyen a los puntos de distribución de la misma forma en que se reparte otro tipo de contenido. En la mayoría de los casos, debe distribuir la imagen de arranque a un punto de distribución como mínimo, antes de implementar un sistema operativo y de crear medios.  

> [!NOTE]  
>  Para usar PXE para implementar un sistema operativo, considere lo siguiente antes de distribuir la imagen de arranque:  
>   
>  -   El punto de distribución debe estar configurado para aceptar solicitudes de PXE.  
> -   Debe distribuir una imagen de arranque habilitada para PXE x86 y x64 a un punto de distribución habilitado para PXE como mínimo.  
> -   Configuration Manager distribuye las imágenes de arranque a la carpeta **RemoteInstall** en el punto de distribución habilitado para PXE.  
>   
>  Para obtener más información sobre el uso de PXE para implementar sistemas operativos, consulte [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Uso de PXE para implementar Windows a través de la red).  

 Para conocer los pasos de distribución de una imagen de arranque, consulte [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute) (Distribuir contenido).  

##  <a name="BKMK_ModifyBootImages"></a> Modificación de una imagen de arranque  
 Puede agregar o quitar controladores de dispositivo para la imagen o editar las propiedades asociadas a la imagen de arranque. Los controladores de dispositivo que agregue o quite pueden incluir adaptadores de red o controladores de dispositivo de almacenamiento masivo. Tenga en cuenta los siguientes factores al modificar imágenes de arranque:  

-   Debe importar y habilitar los controladores de dispositivo en el catálogo de controladores de dispositivo antes de agregarlos a la imagen de arranque.  

-   Al modificar una imagen de arranque, dicha imagen no cambia ninguno de los paquetes asociados a los que hace referencia.  

-   Después de realizar cambios en una imagen de arranque, debe **actualizar** dicha imagen en los puntos de distribución que ya la contienen para que esté disponible su versión más reciente. Para obtener más información, vea [Manage content you have distributed](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage) (Administración del contenido que ha distribuido).  

 Use el procedimiento siguiente para modificar una imagen de arranque.  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>Para modificar las propiedades de una imagen de arranque  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Imágenes de arranque**.  

3.  Seleccione la imagen de arranque que desee modificar.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades** para abrir el cuadro de diálogo **Propiedades** de la imagen de arranque.  

5.  Defina cualquiera de las siguientes opciones para cambiar el comportamiento de la imagen de arranque:  

    -   En la pestaña **Imágenes** , si cambió las propiedades de la imagen de arranque mediante una herramienta externa, haga clic en **Recargar**.  

    -   En la ficha **Controladores** , agregue los controladores de dispositivo de Windows necesarios para arrancar WinPE. Cuando agregue controladores de dispositivos, tenga en cuenta lo siguiente:  

        -   Seleccione **Ocultar controladores que no coincidan con la arquitectura de la imagen de arranque** para mostrar solo los controladores para la arquitectura de la imagen de arranque. La arquitectura se basa en la arquitectura que se indica en el archivo .INF del fabricante.  

        -   Seleccione **Ocultar los controladores que no sean de almacenamiento o red (para imágenes de arranque)** para mostrar solo los controladores de almacenamiento y de red, y ocultar otros controladores que no suelen ser necesarios para las imágenes de arranque, como un controlador de vídeo o de módem.  

        -   Seleccione **Ocultar los controladores que no estén firmados digitalmente** para ocultar los controladores que no estén firmados digitalmente.  

        -   Como práctica recomendada, agregue solo controladores de almacenamiento masivo y NIC a la imagen de arranque, a menos que existan requisitos para que otros controladores formen parte de WinPE.  

        -   Dado que WinPE ya viene con muchos controladores integrados, agregue solo controladores de almacenamiento masivo y NIC que no se incluyan con WinPE.  

        -   Asegúrese de que los controladores que agregue a la imagen de arranque coincidan con la arquitectura de la imagen de arranque.  

        > [!NOTE]  
        >  Debe importar los controladores de dispositivos en el catálogo de controladores antes de agregarlos a una imagen de arranque. Para más información sobre cómo importar controladores de dispositivo, consulte [Manage drivers](manage-drivers.md) (Administración de controladores).  

    -   En la pestaña **Personalización** , seleccione cualquiera de las siguientes opciones:  

        -   Active la casilla **Habilitar comando de preinicio** para especificar que se ejecute un comando antes de que se ejecute la secuencia de tareas. Cuando se habiliten comandos de preinicio, después podrá especificar la línea de comandos que se ejecuta, si son necesarios archivos auxiliares para ejecutar el comando y la ubicación de origen de esos archivos auxiliares.  

            > [!WARNING]  
            >  Debe agregar **cmd /c** al principio de la línea de comandos. Si no se especifica **cmd /c**, el comando no se cerrará después de ejecutarlo. La implementación sigue a la espera de que finalice el comando y no se iniciará ningún otro comando o acción que se hayan configurado.  

            > [!TIP]  
            >  Durante la creación de medios de secuencia de tareas, la secuencia de tareas escribe el identificador de paquete y la línea de comandos de preinicio, incluidos los valores de las variables de secuencia de tareas, en el archivo de registro CreateTSMedia.log en el equipo que ejecuta la consola de Configuration Manager. Puede revisar este archivo de registro para comprobar el valor de las variables de secuencia de tareas.  

        -   Defina los valores de **Fondo de Windows PE** para especificar si quiere usar el fondo predeterminado de WinPE o un fondo personalizado.  

        -   Seleccione **Habilitar compatibilidad de comando (solo prueba)** para abrir un símbolo del sistema mediante la tecla **F8** mientras se implementa la imagen de arranque. Esto resulta útil para solucionar problemas mientras está probando su implementación. No se recomienda usar esta opción en una implementación de producción.  

        -   Configure el espacio de desecho de Windows PE, que es el almacenamiento temporal (unidad RAM) usado por WinPE. Por ejemplo, cuando se ejecuta una aplicación en WinPE y necesita escribir archivos temporales, WinPE redirige los archivos al espacio de desecho en la memoria para simular la presencia de un disco duro. De forma predeterminada, WinPE asigna 32 megabytes (MB) de memoria grabable.  

    -   En la pestaña **Origen de datos** , actualice cualquiera de las siguientes opciones:  

        -   Establezca **Ruta de acceso de la imagen** e **Índice de imágenes** para cambiar el archivo de origen de la imagen de arranque.  

        -   Seleccione **Actualizar puntos de distribución en una programación** para crear una programación para cuando se actualice la imagen de arranque.  

        -   Seleccione **Conservar contenido en caché de cliente** si no desea que el contenido de este paquete deje la memoria caché del cliente para hacer sitio a otro contenido.  

        -   Seleccione **Habilitar replicación diferencial binaria** para especificar que solo se distribuyan archivos cambiados cuando se actualice el paquete de imagen de arranque en el punto de distribución. Esta configuración reduce al mínimo el tráfico de red entre sitios, especialmente cuando el paquete de imagen de arranque es grande y los cambios son relativamente pequeños.  

        -   Seleccione **Implementar esta imagen de arranque desde el punto de distribución habilitado con PXE** si se usa la imagen de arranque en una implementación habilitada para PXE.  

            > [!NOTE]  
            >  Para más información, vea [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Uso de PXE para implementar Windows a través de la red).  

    -   En la pestaña **Acceso a datos** , seleccione cualquiera de las siguientes opciones:  

        -   Defina la **Configuración del recurso compartido de paquete** si desea que los clientes instalen el contenido de este paquete desde la red.  

        -   Establezca la **Configuración de la actualización del paquete** para especificar cómo desea que desconecte a los usuarios desde el punto de distribución. Es posible que Configuration Manager no pueda actualizar la imagen de arranque cuando los usuarios están conectados al punto de distribución.  

    -   En la pestaña **Configuración de distribución** , seleccione cualquiera de las siguientes opciones:  

        -   En la lista **Prioridad de distribución**, especifique el nivel de prioridad que desea que use Configuration Manager cuando se distribuyan varios paquetes en el mismo punto de distribución.  

        -   Seleccione **Distribuir el contenido de este paquete en puntos de distribución preferidos** si desea habilitar la distribución de contenido a petición en puntos de distribución preferidos. Cuando se habilita esta opción, el punto de administración distribuye el contenido en todos los puntos de distribución preferidos cuando un cliente solicite el contenido del paquete y el contenido no esté disponible en ningún punto de distribución preferido.  

        -   Defina la **Configuración de punto de distribución preconfigurado** para especificar cómo desea que se distribuya la imagen de arranque en puntos de distribución habilitados para el contenido preconfigurado.  

            > [!NOTE]  
            >  Para más información sobre el contenido preconfigurado, consulte [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage) (Preconfigurar el contenido).  

    -   En la pestaña **Ubicaciones de contenido** , seleccione el punto de distribución o el grupo de puntos de distribución y realice cualquiera de las siguientes acciones:  

        -   Haga clic en **Redistribuir** para distribuir de nuevo la imagen de arranque en el punto de distribución o el grupo de puntos de distribución seleccionado.  

        -   Haga clic en **Validar** para comprobar la integridad del paquete de imagen de arranque en el punto de distribución o el grupo de puntos de distribución seleccionado.  

    -   En la pestaña **Componentes opcionales**, especifique los componentes agregados a Windows PE para su uso con Configuration Manager. Para más información acerca de los componentes opcionales disponibles, consulte [WinPE: agregar paquetes (referencia de los componentes opcionales)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx).  

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
 Las imágenes de arranque son independientes del idioma. Esto le permite usar una imagen de arranque que mostrará el texto de la secuencia de tareas en varios idiomas en WinPE, si incluye la compatibilidad de idioma adecuada de los componentes opcionales de Windows PE y establece la variable de secuencia de tareas correspondiente para indicar el idioma que se puede mostrar. El idioma del sistema operativo que se implementa es independiente del idioma que se muestra en WinPE, independientemente de la versión de Configuration Manager. El idioma que se muestra al usuario se determina de la manera siguiente:  

-   Cuando un usuario ejecuta la secuencia de tareas desde un sistema operativo existente, Configuration Manager utiliza automáticamente el idioma configurado para el usuario. Cuando la secuencia de tareas se ejecuta automáticamente como resultado de una fecha límite de implementación obligatoria, Configuration Manager utiliza el idioma del sistema operativo.  

-   Para las implementaciones de sistema operativo que usan PXE o medios, puede establecer el valor del identificador de idioma en la variable SMSTSLanguageFolder como parte de un comando de preinicio. Cuando el equipo arranca WinPE, los mensajes se muestran en el idioma que especificó en la variable. Si hay un error al acceder al archivo de recursos de idioma en la carpeta especificada o no se establece la variable, los mensajes se muestran en el idioma de WinPE.  

    > [!NOTE]  
    >  Si el medio está protegido con una contraseña, el texto que solicita la contraseña al usuario siempre se muestra en el idioma de WinPE.  

 Use el procedimiento siguiente para establecer el idioma de WinPE de las implementaciones de sistema operativo iniciadas por un medio o por PXE.  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>Para establecer el idioma de Windows PE de una implementación de sistema operativo iniciada por un medio o por PXE  

1.  Compruebe que el archivo de recursos de secuencia de tareas correcto (tsres.dll) figura en la carpeta de idioma correspondiente en el servidor de sitio antes de actualizar la imagen de arranque. Por ejemplo, el archivo de recursos en inglés está en la siguiente ubicación: <*ConfigMgrInstallationFolder*> \OSD\bin\x64\00000409\tsres.dll.  

2.  Como parte de su comando de preinicio, configure la variable de entorno SMSTSLanguageFolder con el identificador de idioma correspondiente. El identificador de idioma no debe especificarse con un formato hexadecimal sino mediante el formato decimal. Por ejemplo, para establecer el identificador para el idioma inglés, se debe especificar el valor decimal 1033 en lugar del valor hexadecimal 00000409 utilizado para el nombre de la carpeta.  
