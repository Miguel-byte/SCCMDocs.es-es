---
title: Pasos de la secuencia de tareas
titleSuffix: Configuration Manager
description: "Obtenga información sobre los pasos de la secuencia de tareas que puede agregar a una secuencia de tareas de Configuration Manager."
ms.custom: na
ms.date: 03/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
caps.latest.revision: "26"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 8bc73b8aaafa9af4e12589b2d2a742bfc18afd0e
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="task-sequence-steps-in-system-center-configuration-manager"></a>Pasos de la secuencia de tareas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los siguientes pasos de secuencia de tareas se pueden agregar a una secuencia de tareas de Configuration Manager. Para obtener información sobre cómo editar una secuencia de tareas, consulte [Editar una secuencia de tareas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  


##  <a name="BKMK_ApplyDataImage"></a> Paso de secuencia de tareas Aplicar imagen de datos  
 Use el paso la secuencia de tareas **Aplicar imagen de datos** para copiar la imagen de datos en la partición de destino especificada.  

 Este paso solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de secuencias de tareas](task-sequence-action-variables.md).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Paquete de imágenes**  
 Haga clic en **Examinar** y especifique el **Paquete de imágenes**que será usado por este paso de secuencia de tareas. Seleccione el paquete que desea instalar en el cuadro de diálogo **Seleccionar un paquete** . La información de propiedades de los paquetes de imágenes se muestra en la parte inferior del cuadro de diálogo **Seleccionar un paquete** . En la lista desplegable, seleccione la **Imagen** que desea instalar desde el **Paquete de imágenes**seleccionado.  

> [!NOTE]  
>  En esta acción de la secuencia de tareas, la imagen se trata como un archivo de datos y no se lleva a cabo ningún paso de configuración necesario para que dicha imagen arranque como un sistema operativo.  

 **Destino**  
 Especifica un disco duro y una partición con formato, una letra de unidad lógica específica o el nombre de una variable de la secuencia de tareas que contiene la letra de unidad lógica.  

-   **Siguiente partición disponible:** use la siguiente partición secuencial que no haya sido destino previo de las acciones Aplicar sistema operativo o Aplicar imagen de datos en esta secuencia de tareas.  

-   **Disco y partición específicos:** seleccione el número de **Disco** (empezando por 0) y el número de **Partición** (empezando por 1).  

-   **Letra de unidad lógica específica:** especifique la **Letra de unidad** asignada a la partición por Windows PE. Tenga en cuenta que esta letra de unidad puede ser diferente de la que asignará el sistema operativo recién implementado.  

-   **Letra de unidad lógica almacenada en una variable:** especifique la variable de secuencia de tareas que contiene la letra de unidad asignada a la partición por Windows PE. Normalmente, esta variable se establece en la sección Avanzado del cuadro de diálogo **Propiedades de la partición** de la acción de la secuencia de tareas **Formatear y crear particiones en el disco** .  

 **Eliminar todo el contenido en la partición antes de aplicar la imagen**  
 Especifica que, antes de instalar la imagen, se eliminarán todos los archivos de la partición de destino. Si no se elimina el contenido de la partición, este paso puede usarse para aplicar contenido adicional a una partición de destino previa.  

##  <a name="BKMK_ApplyDriverPackage"></a> Aplicar paquete de controladores  
 Use el paso de secuencia de tareas **Aplicar paquete de controladores** para descargar todos los controladores del paquete de controladores e instalarlos en el sistema operativo Windows.

 El paso de secuencia de tareas **Aplicar paquete de controladores** hace que todos los controladores de dispositivo incluidos en un paquete de controladores estén disponibles para su uso con Windows. Este paso se puede agregar a una secuencia de tareas entre los pasos **Aplicar el sistema operativo**  e **Instalar Windows y Configuration Manager** a fin de que los controladores de dispositivo del paquete de controladores estén disponibles para Windows. Normalmente, el paso **Aplicar paquete de controladores** va después del paso de secuencia de tareas **Aplicar controladores automáticamente** . El paso de secuencia de tareas **Aplicar paquete de controladores** también es útil en escenarios de implementación de medios independientes.  

 Asegúrese de que los controladores de dispositivo similares se colocan en un paquete de controladores y distribúyalos a los puntos de distribución adecuados. Una vez distribuidos, los equipos cliente de Configuration Manager pueden instalarlos. Por ejemplo, puede colocar todos los controladores de dispositivo de un fabricante en un paquete de controladores y, a continuación, distribuir el paquete a los puntos de distribución, donde los equipos asociados podrán tener acceso a ellos.

 Este paso resulta útil para medios independientes y para administradores que deseen instalar un conjunto específico de controladores, como los controladores de dispositivos que no se detectan en un análisis de Plug-n-Play (por ejemplo, las impresoras de red).  

 Este paso de secuencia de tareas solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Aplicar paquetes de controladores](task-sequence-action-variables.md#BKMK_ApplyDriverPackage).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Paquete de controladores**  
 Especifique el paquete de controladores que contiene los controladores de dispositivo necesarios. Para ello, haga clic en **Examinar** e inicie el cuadro de diálogo **Seleccionar un paquete** . Especifique un paquete existente para que esté disponible. Las propiedades asociadas del paquete se muestran en la parte inferior del cuadro de diálogo.  

 **Seleccionar en el paquete el controlador de almacenamiento que debe instalarse antes de la configuración en sistemas operativos anteriores a Windows Vista**  
 Especifique los controladores de dispositivo de almacenamiento que son necesarios para instalaciones de sistema operativo anteriores a Windows Vista.  

 **Controlador**  
 Seleccione el archivo del controlador de dispositivo de almacenamiento que debe instalarse antes de la configuración en implementaciones de sistemas operativos anteriores a Windows Vista. La lista desplegable se rellena con el paquete especificado.  

 **Modelo**  
 Especifique el dispositivo crítico para el arranque que se necesita en implementaciones de sistemas operativos anteriores a Windows Vista.  

 **Llevar a cabo la instalación desatendida de controladores no firmados en versiones de Windows en las que se permita**  
 Seleccione esta opción para permitir que Windows instale controladores no firmados en el equipo de referencia.  

##  <a name="BKMK_ApplyNetworkSettings"></a> Paso Aplicar configuración de red  
 Use el paso de secuencia de tareas **Aplicar configuración de red** para especificar la información de configuración de red o grupo de trabajo del equipo de destino. Los valores especificados se almacenan en un formato de archivo de respuesta adecuado para el programa de instalación de Windows cuando se ejecute el paso de secuencia de tareas **Instalar Windows y Configuration Manager** .  

 Este paso de secuencia de tareas se ejecuta en un sistema operativo estándar o en Windows PE. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Aplicar configuración de red](task-sequence-action-variables.md#BKMK_ApplyNetworkSettings).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Unirse a un grupo de trabajo**  
 Seleccione esta opción para que el equipo de destino se una al grupo de trabajo especificado. Escriba el nombre del grupo de trabajo en la línea **Grupo de trabajo** . Este valor puede reemplazarse por el valor que se captura mediante el paso de secuencia de tareas **Capturar configuración de red** .  

 **Unirse a un dominio**  
 Seleccione esta opción para que el equipo de destino se una al dominio especificado. Especifique o busque el dominio, como *fabricam.com*. Especifique o busque una ruta de acceso de protocolo ligero de acceso a directorios (LDAP) de una unidad organizativa (es decir, LDAP//OU=equipos, DC=Fabricam.com, C=com).  

 **Cuenta**  
 Haga clic en **Establecer** para especificar una cuenta con los permisos necesarios para unir el equipo al dominio. En el cuadro de diálogo **Cuenta de usuario de Windows** puede especificar el nombre de usuario con el formato siguiente: **Dominio\Usuario** .  

 **Configuración del adaptador**  
 Especifique la configuración de red para cada adaptador de red del equipo. Haga clic en **Nuevo** para abrir el cuadro de diálogo **Configuración de red** y después especifique la configuración de red. Si la configuración de red se ha capturado anteriormente en un paso de secuencia de tareas **Capturar configuración de red** , la configuración que se aplica al adaptador de red es la anterior, y no la especificada en este paso. Si no se ha capturado previamente la configuración de red, la configuración especificada en el paso **Aplicar configuración de red** se aplica a los adaptadores de red en el orden de enumeración de dispositivos de Windows.  

##  <a name="BKMK_ApplyOperatingSystemImage"></a> Aplicar imagen de sistema operativo  
 Use el paso de secuencia de tareas **Aplicar imagen de sistema operativo** para instalar un sistema operativo en el equipo de destino. Este paso de secuencia de tareas realiza un conjunto de acciones en función de si usa una imagen de sistema operativo o un paquete de instalación de sistema operativo para instalar el sistema operativo.  

 El paso **Aplicar imagen de sistema operativo** realiza las siguientes acciones cuando se usa una imagen de sistema operativo.  

1.  Elimina todo el contenido del volumen de destino, excepto los archivos de la carpeta especificada por la variable de secuencia de tareas &#95;SMSTSUserStatePath.  

2.  Extrae el contenido del archivo .wim especificado a la partición de destino especificada.  

3.  Prepara el archivo de respuesta:  

    1.  Crea un nuevo archivo de respuesta predeterminado de instalación de Windows (sysprep.inf o unattend.xml) para el sistema operativo que se va a implementar.  

    2.  Combina los valores del archivo de respuesta proporcionado por el usuario.  

4.  Copias los cargadores de arranque de Windows en la partición activa.  

5.  Configura el archivo boot.ini o la base de datos de la configuración de arranque (BCD) para que hagan referencia al sistema operativo que se acaba de instalar.  

 El paso **Aplicar imagen de sistema operativo** realiza las siguientes acciones cuando se usa un paquete de instalación de sistema operativo.  

1.  Elimina todo el contenido del volumen de destino, excepto los archivos de la carpeta especificada por la variable de secuencia de tareas &#95;SMSTSUserStatePath.  

2.  Prepara el archivo de respuesta:  

    1.  Crea un archivo de respuesta nuevo con los valores estándar creados por Configuration Manager.  

    2.  Combina los valores del archivo de respuesta proporcionado por el usuario.  

> [!NOTE]  
>  La instalación real de Windows se inicia de forma efectiva con el paso de secuencia de tareas **Instalar Windows y Configuration Manager** . Después de que se ejecute la acción de secuencia de tareas **Aplicar el sistema operativo** , la variable de secuencia de tareas OSDTargetSystemDrive se establece en la letra de unidad de la partición que contiene los archivos de sistema operativo.  

 Este paso de secuencia de tareas solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de secuencia de tareas Aplicar imagen de sistema operativo](task-sequence-action-variables.md#BKMK_ApplyOperatingSystem).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   **Acceder al contenido directamente desde el punto de distribución**:  

     Use esta opción para especificar si desea que la secuencia de tareas tenga acceso a la imagen de sistema operativo directamente desde el punto de distribución. Por ejemplo, puede usar esta opción al implementar sistemas operativos en dispositivos incrustados que tengan una capacidad de almacenamiento limitada. Cuando se selecciona esta opción, también debe definir la configuración del recurso compartido de paquete en la pestaña **Acceso a datos** de las propiedades del paquete.  

    > [!NOTE]  
    >  Esta configuración reemplaza la opción de implementación que está configurada en la página **Puntos de distribución** del **Asistente para implementar software** , pero solo para la imagen de sistema operativo especificada en este paso de secuencia de tareas, y no todo el contenido de la secuencia de tareas completa.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Aplicar el sistema operativo de una imagen capturada**  
 Instala una imagen de sistema operativo que se ha capturado previamente. Haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar un paquete** y luego seleccione el paquete de imágenes existente que desee instalar. Si hay varias imágenes asociadas con el **Paquete de imágenes**especificado, use la lista desplegable para indicar la imagen asociada que se usará para esta implementación. Para ver información básica sobre cada imagen, haga clic en la imagen.  

 **Aplicar imagen de sistema operativo desde un origen de instalación original**  
 Instala un sistema operativo mediante un origen de instalación original. Haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar un paquete de instalación de sistema operativo** y, a continuación, seleccione el paquete de instalación de sistema operativo existente que desee usar. Para ver información básica sobre cada origen de imagen existente, haga clic en el origen de imagen. Las propiedades asociadas del origen de imagen se muestran en el panel de resultados en la parte inferior del cuadro de diálogo. Si hay varias ediciones asociadas con el paquete especificado, use la lista desplegable para especificar la **Edición** asociada que se utiliza.  

 **Usar un archivo de respuesta Sysprep o de instalación desatendida para realizar una instalación personalizada**  
 Use esta opción para proporcionar un archivo de respuesta del programa de instalación de Windows (**unattend.xml**, **unattend.txt**o **sysprep.inf**) según el método de instalación y la versión del sistema operativo. El archivo que especifique puede incluir cualquiera de las opciones de configuración estándar compatibles con los archivos de respuesta de Windows. Por ejemplo, puede usarlo para especificar la página principal predeterminada de Internet Explorer. Debe especificar el paquete que contiene el archivo de respuesta y la ruta de acceso asociada al archivo en el paquete.  

> [!NOTE]  
>  El archivo de respuesta del programa de instalación de Windows que suministre puede contener variables de secuencia de tareas insertadas de tipo %*varname*%, donde varname es el nombre de la variable. La cadena %*varname*% se sustituirá por los valores reales de variable en la acción de secuencia de tareas **Instalar Windows y Configuration Manager** . Sin embargo, tenga en cuenta que dichas variables de secuencia de tareas insertadas no se pueden usar en campos solo numéricos de un archivo de respuesta unattend.xml.  

 Si no se proporciona un archivo de respuesta del programa de instalación de Windows, esta acción de secuencia de tareas generará automáticamente un archivo de respuesta.  

 **Destino**  
 Especifica un disco duro y una partición con formato, una letra de unidad lógica específica o el nombre de una variable de la secuencia de tareas que contiene la letra de unidad lógica.  

-   **Siguiente partición disponible:** use la siguiente partición secuencial que no haya sido destino previo de las acciones Aplicar sistema operativo o Aplicar imagen de datos en esta secuencia de tareas.  

-   **Disco y partición específicos:** seleccione el número de **Disco** (empezando por 0) y el número de **Partición** (empezando por 1).  

-   **Letra de unidad lógica específica:** especifique la **Letra de unidad** asignada a la partición por Windows PE. Tenga en cuenta que esta letra de unidad puede ser diferente de la que asignará el sistema operativo recién implementado.  

-   **Letra de unidad lógica almacenada en una variable:** especifique la variable de secuencia de tareas que contiene la letra de unidad asignada a la partición por Windows PE. Normalmente, esta variable se establece en la sección Avanzado del cuadro de diálogo **Propiedades de la partición** de la acción de la secuencia de tareas **Formatear y crear particiones en el disco** .  

##  <a name="BKMK_ApplyWindowsSettings"></a> Aplicar configuraciones de Windows  
 Use el paso de secuencia de tareas **Aplicar configuraciones de Windows** para configurar las opciones de Windows del equipo de destino. Los valores especificados se almacenan en un formato de archivo de respuesta adecuado para el programa de instalación de Windows cuando se ejecute el paso de secuencia de tareas **Instalar Windows y Configuration Manager** .  

 Este paso de secuencia de tareas solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de secuencia de tareas Aplicar configuración de Windows](task-sequence-action-variables.md#BKMK_ApplyWindowsSettings).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Nombre de usuario**  
 Especifique el nombre de usuario registrado que está asociado con el equipo de destino. Este valor puede reemplazarse por el valor que se captura mediante el paso de secuencia de tareas **Capturar configuración de Windows** .  

 **Nombre de la organización**  
 Especifique el nombre de la organización registrado que está asociado con el equipo de destino. Este valor puede reemplazarse por el valor que se captura mediante el paso de secuencia de tareas **Capturar configuración de Windows** .  

 **Clave de producto**  
 Especifique la clave de producto que se usa para la instalación de Windows en el equipo de destino.  

 **Licencia de servidor**  
 Especificar el modo de licencia de servidor. Como modo de licencia, puede seleccionar **Por servidor** o **Por usuario** . Si selecciona el modo de licencia “por servidor”, también deberá especificar el número máximo de conexiones permitidas según el contrato de licencia. Seleccione **No especificar** si el equipo de destino no es un servidor o si no desea especificar el modo de licencia.  

 **Número máximo de conexiones**  
 Especifique el número máximo de conexiones disponibles para este equipo según lo indicado en el contrato de licencia.  

 **Generar la contraseña de administrador local aleatoriamente y deshabilitar la cuenta en todas las plataformas admitidas (recomendado)**  
 Seleccione esta opción para generar de forma aleatoria una contraseña de administrador local. Con esto se crea una contraseña de administrador local y se deshabilita la cuenta en las plataformas compatibles.  

 **Habilitar la cuenta y especificar la contraseña de administrador local**  
 Seleccione esta opción para habilitar la cuenta de administrador local y crear la contraseña de administrador local. Escriba la contraseña en la línea **Contraseña** y confírmela en la línea **Confirmar contraseña** .  

 **Zona horaria**  
 Especifique la zona horaria que se configurará en el equipo de destino. Este valor puede reemplazarse por el valor que se captura mediante el paso de secuencia de tareas **Capturar configuración de Windows** .  

##  <a name="BKMK_AutoApplyDrivers"></a> Aplicar controladores automáticamente  
 Use el paso de secuencia de tareas **Aplicar controladores automáticamente** para comparar e instalar controladores como parte de la implementación del sistema operativo.  

 El paso de secuencia de tareas **Aplicar controladores automáticamente** realiza las acciones siguientes:  

1.  Examina el hardware y busca los identificadores de Plug and Play de todos los dispositivos presentes en el sistema.  

2.  Envía la lista de dispositivos y sus identificadores de Plug and Play al punto de administración. El punto de administración devuelve, desde el catálogo de controladores, una lista de los controladores compatibles con cada dispositivo. El punto de administración considera todos los controladores independientemente del paquete de controladores que podrían estar en él. Solo se consideran aquellos controladores que se etiquetan con la categoría de controlador especificada y aquellos controladores que no están marcados como deshabilitados.  

3.  Para cada dispositivo, el cliente elige el controlador más apropiado para el sistema operativo en el que se implementa y que se encuentra en un punto de distribución accesible.  

4.  El controlador (o controladores) seleccionado se descarga desde un punto de distribución y se preconfigura en el sistema operativo de destino.  

    1.  Para instalaciones basadas en imagen, los controladores se colocan en el almacén de controladores del sistema operativo.  

    2.  Para las instalaciones basadas en el programa de instalación, el programa de instalación de Windows se configura con la ubicación en la que se deben buscar los controladores.  

5.  Cuando la acción de secuencia de tareas **Instalar Windows y Configuration Manager** se ejecute y Windows arranque por primera vez, se encontrará con los controladores preconfigurados por esta acción.  

> [!IMPORTANT]
>  El paso de secuencia de tareas **Aplicar controladores automáticamente** no puede usarse con medios independientes debido a que el programa de instalación de Windows no tendrá conexión al sitio de Configuration Manager.

Este paso de secuencia de tareas solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Aplicar controladores automáticamente](task-sequence-action-variables.md#BKMK_AutoApplyDrivers).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Instalar solo los controladores compatibles más coincidentes**  
 Especifica que el paso de secuencia de tareas solo instala el controlador que mejor coincide con cada dispositivo de hardware detectado.  

 **Instalar todos los controladores compatibles**  
 Especifica que el paso de secuencia de tareas instala todos los controladores compatibles con cada dispositivo de hardware detectado y permite que el programa de instalación de Windows elija el mejor controlador. Esta opción ocupa más espacio en disco y ancho de banda de red porque se descargan más controladores, pero puede seleccionar un controlador más adecuado.  

 **Considerar controladores de todas las categorías**  
 Especifica que la acción de secuencia de tareas busca los controladores de dispositivo apropiados en todas las categorías de controladores disponibles.  

 **Limitar la coincidencia de controladores a los controladores de las categorías seleccionadas**  
 Especifica que la acción de secuencia de tareas busca los controladores de dispositivo en las categorías de controlador especificadas.  

 **Llevar a cabo la instalación desatendida de controladores no firmados en versiones de Windows en las que se permita**  
 Permite que esta acción de secuencia de tareas instale controladores de dispositivo de Windows sin firmar.  

> [!IMPORTANT]  
>  Esta opción no es aplicable a los sistemas operativos en los que no se puede configurar la directiva de firma de controladores.  

##  <a name="BKMK_CaptureNetworkSettings"></a> Capturar configuración de red  
 Use el paso de secuencia de tareas **Capturar configuración de red** para capturar la configuración de red de Microsoft en el equipo que ejecuta la secuencia de tareas. La configuración se guarda en variables de secuencia de tareas que reemplazarán la configuración predeterminada que configure en el paso de secuencia de tareas **Aplicar configuración de red** .  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Capturar configuración de red](task-sequence-action-variables.md#BKMK_CaptureNetworkSettings).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Especifica un nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Proporciona más información detallada sobre la acción realizada en este paso.  

 **Migrar la pertenencia a grupo de trabajo y dominio**  
 Captura la información de pertenencia a dominio y grupo de trabajo del equipo de destino.  

 **Migrar la configuración del adaptador de red**  
 Captura la configuración del adaptador de red del equipo de destino. La información capturada incluye la configuración de red global, el número de adaptadores y la configuración de red asociada a cada adaptador. Esta configuración incluye opciones asociadas con DNS, WINS, IP y filtros de puertos.  

##  <a name="BKMK_CaptureOperatingSystemImage"></a> Capturar imagen de sistema operativo  
 Use el paso de secuencia de tareas **Capturar imagen de sistema operativo** para capturar una o más imágenes en un equipo de referencia y almacenarlas en un archivo WIM en el recurso compartido de red especificado. Después, el asistente para agregar paquetes de imagen de sistema operativo puede usarse para importar este archivo .WIM en Configuration Manager, de modo que pueda usarse en implementaciones de sistema operativo basadas en imagen.  

 Cada volumen (unidad) del equipo de referencia se captura como una imagen independiente en el archivo .wim. Si el equipo al que se hace referencia tiene varios volúmenes, el archivo WIM resultante contendrá una imagen independiente para cada volumen. Solo se capturan los volúmenes formateados como NTFS o FAT32. Se omiten los volúmenes con otros formatos y los volúmenes USB.  

 El sistema operativo instalado en el equipo de referencia debe ser una versión de Windows que sea compatible con Configuration Manager y debe haberse preparado con la herramienta SysPrep. El volumen del sistema operativo instalado y el volumen de arranque deben ser el mismo.  

 También debe especificar una cuenta de Windows que tenga permisos de escritura en el recurso compartido de red que ha seleccionado.  

 Este paso de secuencia de tareas solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Capturar sistema operativo](task-sequence-action-variables.md#BKMK_CaptureOperatingSystemImage).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Destino**  
 Ruta de acceso del sistema de archivos a la ubicación que Configuration Manager usa al almacenar la imagen capturada del sistema operativo.  

 **Descripción**  
 Descripción opcional definida por el usuario de la imagen capturada del sistema operativo que está almacenada en el archivo .WIM.  

 **Versión**  
 Número de versión opcional definido por el usuario que se asigna a la imagen capturada del sistema operativo. Este valor puede ser cualquier combinación de letras y números y se almacena en el archivo .WIM.  

 **Creado por**  
 Nombre opcional del usuario que creó la imagen del sistema operativo y se almacena en el archivo .WIM.  

 **Cuenta de captura de imagen del sistema operativo**  
 Debe especificar la cuenta de Windows que tenga permisos en el recurso compartido de red que especifique. Haga clic en **Establecer** para especificar el nombre de esa cuenta de Windows.  

##  <a name="BKMK_CaptureUserState"></a> Capturar estado de usuario  
 Use el paso de secuencia de tareas **Capturar estado de usuario** para utilizar la herramienta de migración de estado de usuario (USMT) a fin de capturar el estado de usuario y la configuración del equipo que ejecuta la secuencia de tareas. Este paso de secuencia de tareas se usa junto con el paso **Restaurar estado de usuario** . Con USMT 3.0.1 y versiones posteriores, esta opción siempre cifra el almacén de estado de USMT mediante una clave de cifrado generada y administrada por Configuration Manager.  

 Para obtener más información sobre cómo administrar el estado de usuario al implementar sistemas operativos, consulte [Administrar el estado de usuario](../get-started/manage-user-state.md).  

 También puede usar el paso de secuencia de tareas **Capturar estado de usuario** con los pasos **Solicitar almacén de estado** y **Liberar almacén de estado** si quiere guardar la configuración de estado en un punto de migración de estado, o restaurar la configuración a partir de un punto de migración de estado, en el sitio de Configuration Manager.  

 El paso de secuencia de tareas **Capturar estado de usuario** proporciona control sobre un subconjunto limitado de las opciones de USMT más usadas. Con la variable de secuencia de tareas OSDMigrateAdditionalCaptureOptions se pueden especificar más opciones de línea de comandos.  

 Este paso de secuencia de tareas solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Capturar estado de usuario](task-sequence-action-variables.md#BKMK_CaptureUserState).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Paquete de herramientas de migración de estado de usuario**  
 Especifique el paquete de Configuration Manager que contiene la versión de USMT de este paso de secuencia de tareas que se usará al capturar la configuración y el estado de usuario. Este paquete no requiere un programa. Cuando se ejecuta el paso de secuencia de tareas, la secuencia de tareas usará la versión de USMT del paquete que especifique. Especifique un paquete que contenga la versión de 32 bits o x64 de USMT, en función de la arquitectura del sistema operativo en el que se captura el estado.  

 **Capturar todos los perfiles de usuario mediante opciones estándar**  
 Seleccione esta opción para migrar toda la información de perfiles de usuario. Esta opción está seleccionada de forma predeterminada.  

 Si selecciona esta opción, pero no selecciona la opción “Restaurar perfiles de usuario de equipo local” en el paso de secuencia de tareas “Restaurar estado de usuario”, la secuencia de tareas producirá un error porque Configuration Manager no puede migrar las cuentas nuevas sin asignarles contraseñas. Además, si usa el asistente **Nueva secuencia de tareas** y crea una secuencia de tareas para **Instalar un paquete de imágenes existente**, la secuencia de tareas resultante tendrá como valor predeterminado “Capturar todos los perfiles de usuario mediante opciones estándar”, pero sin seleccionar la opción “Restaurar perfiles de usuario de equipo local” (es decir, cuentas que no son de dominio).  

 Seleccione **Restaurar perfiles de usuario de equipo local** y proporcione una contraseña para la cuenta que desea migrar. En una secuencia de tareas creada manualmente, esta configuración se encuentra en el paso “Restaurar estado de usuario”. En una secuencia de tareas creada por el asistente **Nueva secuencia de tareas** , esta configuración se encuentra en el paso **Restaurar configuración y archivos de usuario** .  

 Si no tiene ninguna cuenta de usuario local, esto no se aplica.  

 **Personalizar la captura de perfiles de usuario**  
 Seleccione esta opción para especificar una migración de archivos de perfil personalizada. Haga clic en **Archivos** para seleccionar los archivos de configuración que USMT usará en este paso. Debe especificar un archivo .xml personalizado que contenga las reglas que definen los archivos de estado de usuario que se van a migrar.  

 **Haga clic aquí para seleccionar archivos de configuración:**  
 Seleccione esta opción para elegir los archivos de configuración en el paquete USMT que desea usar para capturar los perfiles de usuario. Haga clic en el botón **Archivos** botón para iniciar el cuadro de diálogo **Archivos de configuración** . Para especificar un archivo de configuración, escriba el nombre del archivo en la línea **Nombre de archivo** y haga clic en el botón **Agregar** .  

 **Habilitar el registro detallado**  
 Habilite esta opción para generar información más detallada en el archivo de registro. Al capturar el estado, se genera el registro Scanstate.log, que se almacena de forma predeterminada en la carpeta de registro de la secuencia de tareas \windows\system32\ccm\logs.  

 **Omitir archivos que usan el sistema de cifrado de archivos**  
 Habilite esta opción si desea omitir la captura de los archivos que estén cifrados mediante el sistema de cifrado de archivos (EFS), incluidos los archivos de perfil. Según el sistema operativo y la versión de USMT, los archivos cifrados podrían no ser legibles después de la restauración. Para obtener más información, consulte la documentación de USMT.  

 **Copiar mediante el acceso al sistema de archivos**  
 Habilite esta opción para especificar cualquiera de las siguientes opciones:  

-   **Continuar si algunos archivos no se pueden capturar**: habilite esta configuración para continuar con el proceso de migración incluso en el caso de que algunos archivos no se puedan capturar. Si deshabilita esta opción y no se puede capturar un archivo, se produce un error en el paso de secuencia de tareas. Esta opción está habilitada de forma predeterminada.  

-   **Capturar localmente mediante vínculos en vez de mediante la copia de archivos**: habilite esta opción para usar vínculos físicos NTFS para capturar archivos.  

     Para obtener más información sobre cómo migrar datos mediante vínculos físicos, consulte el tema en el que se describe el [almacén de migración de vínculos físicos](http://go.microsoft.com/fwlink/p/?LinkId=240222)  

-   **Capturar en modo fuera de línea (solo Windows PE)**: habilite esta opción para capturar el estado de usuario en Windows PE en lugar de todo el sistema operativo.  

 **Capturar mediante el Servicio de instantánea de copia de volumen (VSS)**  
 Esta opción permite capturar archivos incluso si otra aplicación los ha bloqueado para su edición.  

##  <a name="BKMK_CaptureWindowsSettings"></a> Capturar configuración de Windows  
 Use el paso de secuencia de tareas **Capturar configuraciones de Windows** para capturar la configuración de Windows en el equipo que ejecuta la secuencia de tareas. La configuración se guarda en variables de secuencia de tareas que reemplazarán la configuración predeterminada que configure en el paso de secuencia de tareas **Aplicar configuraciones de Windows** .  

 Este paso de secuencia de tareas se ejecuta en un sistema operativo estándar o en Windows PE. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Capturar configuración de Windows](task-sequence-action-variables.md#BKMK_CaptureWindowsSettings).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Migrar nombre de equipo**  
 Seleccione esta opción para capturar el nombre de equipo NetBIOS del equipo.  

 **Migrar nombres de organización y usuario registrados**  
 Seleccione esta opción para capturar los nombres de organización y usuario registrados en el equipo.  

 **Migrar zona horaria**  
 Seleccione esta opción para capturar la configuración de zona horaria en el equipo.  

##  <a name="BKMK_CheckReadiness"></a> Comprobar preparación  
 Use el paso de secuencia de tareas **Comprobar preparación** para verificar que el equipo de destino cumple los requisitos previos de implementación especificados.  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso. No seleccione esta opción para este paso; si la selecciona, el paso registrará únicamente las comprobaciones de preparación y no detendrá la secuencia de tareas cuando se produce un error en una comprobación.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Garantizar mínimo de memoria (MB)**  
 Seleccione esta opción para verificar si la cantidad de memoria (expresada en megabytes) instalada en el equipo de destino cumple o supera la cantidad especificada. De forma predeterminada, esta opción está seleccionada.  

 **Garantizar velocidad mínima de procesador (MHz)**  
 Seleccione esta opción para verificar que la velocidad del procesador (expresada en megahercios [MHz]), instalada en el equipo de destino cumple o supera la cantidad especificada. De forma predeterminada, esta opción está seleccionada.  

 **Garantizar espacio libre en disco mínimo (MB)**  
 Seleccione esta opción para verificar que la cantidad de espacio libre en disco (expresada en megabytes) en el equipo de destino cumple o supera la cantidad especificada.  

 **Garantizar que el sistema operativo actual que se va a actualizar es**  
 Seleccione esta opción para verificar que el sistema operativo instalado en el equipo de destino cumple el requisito que especifique. De forma predeterminada, esta opción tiene un valor de **CLIENTE**.  

##  <a name="BKMK_ConnectToNetworkFolder"></a> Conectar a carpeta de red  
 Use la acción de secuencia de tareas **Conectar a carpeta de red** para crear una conexión a una carpeta de red compartida.  

 Este paso de secuencia de tareas se ejecuta en un sistema operativo estándar o en Windows PE. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Conectar a carpeta de red](task-sequence-action-variables.md#BKMK_ConnecttoNetworkFolder).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

##  <a name="BKMK_DisableBitLocker"></a> Deshabilitar BitLocker  
 Use el paso de secuencia de tareas **Deshabilitar BitLocker** para deshabilitar el cifrado de BitLocker en la unidad de sistema operativo actual o en una unidad específica. Con esta acción, los protectores de clave se hacen visibles en texto no cifrado en el disco duro, pero no se descifra el contenido de la unidad. Por lo tanto, esta acción se realiza casi al instante.  

> [!NOTE]  
>  El cifrado de unidad de BitLocker ofrece cifrado de nivel bajo del contenido de un volumen de disco.  

 Si tiene varias unidades cifradas, debe deshabilitar BitLocker en las unidades de datos antes de deshabilitar BitLocker en la unidad del sistema operativo.  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE.  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Especifica un nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Proporciona más información detallada sobre la acción realizada en este paso.  

 **Unidad actual del sistema operativo**  
 Deshabilita BitLocker en la unidad actual del sistema operativo.  

 **Unidad específica**  
 Deshabilita BitLocker en una unidad específica. Use la lista desplegable para especificar la unidad donde se deshabilita BitLocker.  

##  <a name="BKMK_DownloadPackageContent"></a> Descargar contenido de paquete  
 Use el paso de la secuencia de tareas **Descargar contenido de paquete** para descargar cualquiera de los siguientes tipos de paquete:  

-   Imágenes de sistema operativo  

-   Paquetes de actualización del sistema operativo  

-   Paquetes de controladores  

-   Paquetes  

 Este paso funciona bien en una secuencia de tareas para actualizar un sistema operativo en los escenarios siguientes:  

-   Para usar una secuencia de tareas de actualización única que funciona con las plataformas x86 y x64. Para hacerlo, incluya dos pasos **Descargar contenido de paquete** en el grupo **Preparación para actualización** con condiciones para detectar la arquitectura del cliente y descargar únicamente el paquete de actualización del sistema operativo adecuado. Configure todos los pasos **Descargar contenido de paquete** para que usen la misma variable, y use la variable para la ruta de los medios en el paso **Actualizar sistema operativo** .  

-   Para descargar dinámicamente un paquete de controladores aplicables, use dos pasos **Descargar contenido de paquete** con condiciones para detectar el tipo de hardware adecuado para cada paquete de controlador. Configure todos los pasos **Descargar contenido de paquete** para que usen la misma variable, y use la variable para el valor **Staged content** en la sección de controladores en el paso **Actualizar sistema operativo** .  

> [!NOTE]    
> Al implementar una secuencia de tareas que contiene el paso Descargar contenido de paquete, no seleccione **Download all content locally before starting the task sequence** (Descargar todo el contenido localmente antes de iniciar la secuencia de tareas) para **Opciones de implementación** en la página **Puntos de distribución** del Asistente para implementar software.  

Este paso se ejecuta en un sistema operativo estándar o en Windows PE. Pero en WinPE no se admite la opción de guardar el paquete en la caché de cliente de Configuration Manager.

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Especifica un nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Proporciona más información detallada sobre la acción realizada en este paso.  

 Icono**Seleccione el paquete**  
 Haga clic en el icono para seleccionar el paquete de descarga. Después de seleccionar un paquete, puede hacer clic en el icono de nuevo para elegir otro paquete.  

 **Colocar en la siguiente ubicación**  
 Elija esta opción para guardar el paquete en una de las siguientes ubicaciones:  

 -   **Directorio de trabajo de secuencia de tareas**  

 -   **Caché de cliente de Configuration Manager**: use esta opción para almacenar el contenido en la caché de los clientes. Esto permite que el cliente actúe como origen de caché del mismo nivel para otros clientes de caché del mismo nivel. Para obtener más información, consulte [Preparar el almacenamiento en caché del mismo nivel de Windows PE para reducir el tráfico WAN](../get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

 -   **Ruta de acceso personalizada**  

 **Guardar ruta de acceso como variable**  
 Puede guardar la ruta de acceso como una variable que puede usar en otro paso de la secuencia de tareas. Configuration Manager agrega un sufijo numérico al nombre de variable. Por ejemplo, si especifica una variable de %*mycontent*% como una variable personalizada, es la raíz de donde se almacena todo el contenido al que se hace referencia (que pueden ser varios paquetes). Al hacer referencia a la variable, agregará un sufijo numérico a la variable. Por ejemplo, para el primer paquete, hará referencia a la variable %*mycontent01*%. Cuando se hace referencia a la variable en unos pasos de subsecuencia, como Actualizar sistema operativo, usaría %*mycontent02*% o %*mycontent03*%, donde el número corresponde al orden en el que el paquete aparece en el paso.  

 **Si se produce un error en la descarga de un paquete, continúe con la descarga de otros paquetes de la lista**  
 Especifica que si se produce un error al descargar el paquete, pasará al siguiente paquete de la lista e iniciará la descarga.  

##  <a name="BKMK_EnableBitLocker"></a> Habilitar BitLocker  
 Use el paso de secuencia de tareas **Habilitar BitLocker** para habilitar el cifrado de BitLocker en al menos dos particiones del disco duro. La primera partición activa contiene el código de arranque de Windows. La otra partición contiene el sistema operativo. La partición de arranque debe permanecer sin cifrar.  

 Use el paso de secuencia de tareas **Tener en servicio BitLocker** para habilitar BitLocker en una unidad de disco en Windows PE. Para obtener más información, consulte la sección [Tener en servicio BitLocker](#BKMK_PreProvisionBitLocker) de este tema.  

> [!NOTE]  
>  El cifrado de unidad de BitLocker ofrece cifrado de nivel bajo del contenido de un volumen de disco.  

 El paso **Habilitar BitLocker** solo se ejecuta en un sistema operativo estándar, no en Windows PE. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Habilitar BitLocker](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

 El Módulo de plataforma segura (TPM) debe estar en el siguiente estado cuando se especifica **Solo TPM**, **TPM y clave de inicio en USB** o **TPM con PIN**antes de poder ejecutar el paso **Habilitar BitLocker** :  

-   Habilitado  

-   Activado  

-   Propiedad permitida  

 El paso de secuencia de tareas puede completar cualquier inicialización de TPM restante, ya que los pasos que faltan no requieren presencia física ni reinicios. Los demás pasos de inicialización de TPM que puede completar de forma transparente **Habilitar BitLocker** (si es necesario) son:  

-   Crear par de claves de aprobación  

-   Crear valor de autorización de propietario y custodia para Active Directory, que debe extenderse para admitir este valor  

-   Tomar posesión  

-   Crear la clave raíz de almacenamiento, o restablecerla si ya existe pero no es compatible  

 Si desea que el paso **Habilitar BitLocker** espere hasta que finalice el proceso de cifrado de unidad antes de continuar con el siguiente paso de secuencia de tareas, seleccione la casilla **Espere** . Si no selecciona la casilla **Espere** , el proceso de cifrado de unidad se realizará en segundo plano y la ejecución de la secuencia de tareas pasará inmediatamente al paso siguiente.  

 BitLocker puede usarse para cifrar varias unidades en un equipo (tanto de sistema operativo como de datos). Para cifrar una unidad de datos, el sistema operativo debe estar ya cifrado y el proceso de cifrado debe haberse completado, ya que los protectores de clave de las unidades de datos se almacenan en la unidad del sistema operativo. Como resultado, si se cifran la unidad del sistema operativo y la unidad de datos en el mismo proceso, debe seleccionarse la opción de espera para el paso que habilita BitLocker en la unidad del sistema operativo.  

 Si el disco duro ya está cifrado, pero BitLocker está deshabilitado, “Habilitar BitLocker” vuelve a habilitar el protector o los protectores de clave casi al instante. En este caso no es necesario recifrar la unidad de disco duro.  

 Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Habilitar BitLocker](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Especifica un nombre descriptivo para este paso de secuencia de tareas.  

 **Descripción**  
 Le permite especificar opcionalmente una descripción para este paso de secuencia de tareas.  

 **Elija la unidad que desea cifrar**  
 Especifica la unidad que se va a cifrar. Para cifrar la unidad actual del sistema operativo, seleccione **Unidad actual del sistema operativo** y, a continuación, configure una de las siguientes opciones para la administración de claves:  

-   **Solo TPM**: seleccione esta opción para usar solo el Módulo de plataforma segura (TPM).  

-   **Clave de inicio solo en USB**: seleccione esta opción para usar una clave de inicio almacenada en una unidad flash USB. Si se selecciona esta opción, BitLocker bloquea el proceso de arranque normal hasta que se conecte al equipo un dispositivo USB que contenga una clave de inicio de BitLocker.  

-   **TPM y clave de inicio en USB**: seleccione esta opción para usar TPM y una clave de inicio almacenada en una unidad flash USB. Si se selecciona esta opción, BitLocker bloquea el proceso de arranque normal hasta que se conecte al equipo un dispositivo USB que contenga una clave de inicio de BitLocker.  

-   **TPM con NIP**: seleccione esta opción para usar TPM y un número de identificación personal (NIP). Si selecciona esta opción, BitLocker bloquea el proceso de arranque normal hasta que el usuario proporcione el PIN.  

 Para cifrar una determinada unidad de datos que no sean del sistema operativo, seleccione **Unidad específica**y, a continuación, seleccione la unidad en la lista.  

 **Elija la ubicación en la que desea crear la clave de recuperación**  
 Para especificar dónde se crea la contraseña de recuperación, seleccione **En Active Directory** para custodiar la contraseña en Active Directory. Si selecciona esta opción, debe extender Active Directory para el sitio a fin de que se guarde la información de recuperación de BitLocker asociada. Puede no crear ninguna contraseña si selecciona **No crear clave de recuperación**. Sin embargo, lo recomendable es crear una contraseña.  

 **Esperar a que BitLocker complete el proceso de cifrado de unidad en todas las unidades antes de continuar con la ejecución de la secuencia de tareas**  
 Seleccione esta opción para permitir que se complete el cifrado de unidad de BitLocker antes de ejecutar el siguiente paso en la secuencia de tareas. Si se selecciona esta opción, se cifra todo el volumen de disco antes de que el usuario pueda iniciar sesión en el equipo.  

 El proceso de cifrado puede tardar horas en completarse cuando se cifra una unidad de disco duro grande. Si no selecciona esta opción, permitirá que la secuencia de tareas continúe inmediatamente.  

##  <a name="BKMK_FormatandPartitionDisk"></a> Formatear y crear particiones en el disco  
 Use el paso de secuencia de tareas **Formatear y crear particiones de disco** para formatear y crear particiones en el disco especificado del equipo de destino.  

> [!IMPORTANT]  
>  Cada valor especificado para este paso de secuencia de tareas se aplica a un único disco. Si desea dar formato y crear particiones en otro disco del equipo de destino, debe agregar otro paso **Formatear y crear particiones de disco** a la secuencia de tareas.  

 Este paso de secuencia de tareas solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Formatear y crear particiones en el disco](task-sequence-action-variables.md#BKMK_FormatPartitionDisk).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Número de disco**  
 El número de disco físico del disco al que se dará formato. El número se basa en el orden de enumeración de disco de Windows.  

 **Tipo de disco**  
 El tipo de disco al que se da formato. Hay dos opciones para seleccionar en la lista desplegable:  

-   Estándar (MBR): registro de arranque maestro.  

-   GPT: tabla de particiones GUID  

> [!NOTE]  
>  Si cambia el tipo de disco de **Estándar (MBR)** a **GPT**y el diseño de partición contiene una partición extendida, todas las particiones extendidas y lógicas se quitarán del diseño. Se le pedirá que confirme esta acción antes de cambiar el tipo de disco.  

 **Volumen**  
 Información específica sobre la partición o el volumen que se creará, incluido:  

-   Nombre  

-   Espacio en disco restante  

 Para crear una nueva partición, haga clic en **Nuevo** y se abrirá el cuadro de diálogo **Propiedades de la partición** . Puede especificar el tipo y el tamaño de la partición, e indicar si será una partición de arranque. Para modificar una partición existente, haga clic en la partición que desea modificar y, a continuación, haga clic en el botón de propiedades. Para obtener más información sobre cómo configurar particiones de disco duro, consulte uno de los siguientes temas:  

-   [Configuración de particiones de disco duro basadas en UEFI/GPT](http://go.microsoft.com/fwlink/?LinkID=272104)  

-   [Configuración de particiones de disco duro basadas en BIOS/MBR](http://go.microsoft.com/fwlink/?LinkId=272105)  

 Para eliminar una partición, seleccione la partición que desea eliminar y haga clic en **Eliminar**.  

##  <a name="BKMK_InstallApplication"></a> Instalar aplicación  
 Use el paso de secuencia de tareas **Instalar aplicación** para instalar aplicaciones como parte de la secuencia de tareas. Este paso puede instalar un conjunto de aplicaciones que se especifican en el paso de secuencia de tareas o un conjunto de aplicaciones que se especifican mediante una lista dinámica de variables de secuencia de tareas. Cuando se ejecuta este paso, la instalación de aplicaciones se inicia de inmediato sin tener que esperar durante un intervalo de sondeo de directiva.  

 Cada aplicación instalada debe cumplir los siguientes criterios:  

-   La aplicación debe ser un tipo de implementación de Windows Installer o un instalador de scripts. No se admiten los tipos de implementación de paquete de aplicación de Windows (archivo .appx).  

-   Debe ejecutarse en la cuenta sistema local y no en la cuenta de usuario.  

-   No debe interactuar con el escritorio. El programa debe ejecutarse en modo silencioso o en modo desatendido.  

-   No debe iniciarse ni reiniciarse por sí misma. La aplicación debe solicitar un reinicio mediante el código estándar de reinicio: un código de salida 3010. Esto garantiza que el paso de secuencia de tareas controlará correctamente el reinicio. Si la aplicación devuelve un código de salida 3010, el motor de secuencia de tareas subyacente lleva a cabo el reinicio. Tras el reinicio, la secuencia de tareas continúa automáticamente.  

 Cuando se ejecuta el paso **Instalar aplicación** , la aplicación comprueba la aplicabilidad de las reglas de requisitos y el método de detección en los tipos de implementación de la aplicación. Según los resultados de esta comprobación, la aplicación instala el tipo de implementación correspondiente. Si un tipo de implementación contiene dependencias, el tipo de implementación dependiente se evalúa y se instala como parte del paso de instalación de la aplicación. Las dependencias de aplicación no son compatibles con medios independientes.  

> [!NOTE]  
>  Para instalar una aplicación que reemplace a otra aplicación, los archivos de contenido de la aplicación sustituida deben estar disponibles o se producirá un error en el paso de secuencia de tareas. Por ejemplo, Microsoft Visio 2010 se instala en un cliente o en una imagen capturada. Cuando se ejecuta el paso de secuencia de tareas “Instalar aplicación” para instalar Microsoft Visio 2013, los archivos de contenido de Microsoft Visio 2010 (la aplicación sustituida) deben estar disponibles en un punto de distribución o, de lo contrario, se producirá un error en la secuencia de tareas. Un cliente o una imagen capturada que no tenga instalado Microsoft Visio completará la instalación de Microsoft Visio 2013 sin comprobar los archivos de contenido de Microsoft Visio 2010.  

> [!NOTE]
> Puede usar las variables integradas SMSTSMPListRequestTimeoutEnabled y SMSTSMPListRequestTimeout para habilitar y especificar la cantidad de milisegundos que espera una secuencia de tareas antes de volver a intentar instalar una aplicación después de no poder recuperar la lista de puntos de administración de los servicios de ubicación. Para obtener más información, consulte [Variables integradas de la secuencia de tareas](task-sequence-built-in-variables.md).

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE.  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especifique esta opción para volver a intentar este paso si el equipo se reinicia inesperadamente. También puede especificar el número de reintentos después de un reinicio.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Instalar las aplicaciones siguientes**  
 Esta opción especifica las aplicaciones que se instalan en el orden en que se especifican.  

 Configuration Manager filtrará las aplicaciones deshabilitadas o las que tengan los valores siguientes. Estas aplicaciones no aparecerán en el cuadro de diálogo **Seleccione la aplicación que desea instalar** .  

-   Solo cuando un usuario haya iniciado sesión  

-   Ejecutar con derechos de usuario  

 **Instalar aplicaciones según la lista de variables dinámicas**  
 Esta configuración especifica el nombre base de un conjunto de variables de secuencia de tareas que se definen para una colección o un equipo. Estas variables especifican las aplicaciones que se instalarán para esa colección o equipo. Cada nombre de variable consta de su nombre base común además de un sufijo numérico que empieza en 01. El valor de cada variable debe contener el nombre de la aplicación y nada más.  

 Para que las aplicaciones se instalen mediante una lista de variables dinámicas, debe habilitarse la siguiente configuración en la pestaña **General** del cuadro de diálogo **Propiedades** de la aplicación: **Permitir que esta aplicación se instale desde la secuencia de tareas de instalación de aplicación en vez de implementarla manualmente**  

> [!NOTE]  
>  No se pueden instalar aplicaciones mediante una lista de variables dinámicas para las implementaciones de medios independientes.  

 Por ejemplo, para instalar una aplicación mediante una variable de secuencia de tareas llamada AA01, especifique la siguiente variable:  

|Nombre de variable|Valor de variable|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

 Para instalar dos aplicaciones, debe especificar las siguientes variables:  

|Nombre de variable|Valor de variable|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

 Las siguientes condiciones afectarán a lo que se instala:  

-   Si el valor de una variable contiene alguna información que no sea el nombre de la aplicación, esa aplicación no se instala y la secuencia de tareas continúa.  

-   Si no se encuentra ninguna variable con el nombre base especificado y el sufijo "01", no se instala ninguna aplicación. Si selecciona **Continuar después de un error** en la pestaña Opciones del paso de secuencia de tareas, la secuencia de tareas continúa cuando no se puede instalar una aplicación. Si no se selecciona esta opción, la secuencia de tareas produce un error y no instalarán las aplicaciones restantes.  

 **Continuar instalando otras aplicaciones en la lista si se produce un error de instalación de aplicación**  
 Esta configuración especifica que el paso continúa si se produce un error la instalación de una aplicación. Si se especifica este valor, la secuencia de tareas continuará sin tener en cuenta los errores de instalación que se devuelven. Si no se especifica este valor y una instalación produce error, el paso de secuencia de tareas finalizará inmediatamente.  

##  <a name="BKMK_InstallPackage"></a> Instalar paquete

 Use el paso de secuencia de tareas **Instalar paquete** para instalar software como parte de la secuencia de tareas. Cuando se ejecuta este paso, la instalación se inicia de inmediato sin tener que esperar durante un intervalo de sondeo de directiva.  

 El software que se instala debe cumplir los siguientes criterios:  

-   Debe ejecutarse en la cuenta sistema local y no en la cuenta de usuario.  

-   No debe interactuar con el escritorio. El programa debe ejecutarse en modo silencioso o en modo desatendido.  

-   No debe iniciarse ni reiniciarse por sí misma. El software debe solicitar un reinicio mediante el código estándar de reinicio: un código de salida 3010. Esto garantiza que el paso de secuencia de tareas controlará correctamente el reinicio. Si el software devuelve un código de salida 3010, el motor de secuencia de tareas subyacente lleva a cabo el reinicio. Tras el reinicio, la secuencia de tareas continúa automáticamente.  

 Los programas que usan la opción **Ejecutar otro programa primero** para instalar un programa dependiente no se admiten al implementar un sistema operativo. Si **Ejecutar otro programa primero** está habilitada para el software y el programa dependiente ya se ha ejecutado en el equipo de destino, se ejecutará el programa dependiente y continuará la secuencia de tareas. Sin embargo, si el programa dependiente todavía no se ha ejecutado en el equipo de destino, el paso de secuencia de tareas producirá un error.  

> [!NOTE]  
>  El sitio de administración central no tiene las directivas de configuración de cliente necesarias para habilitar el agente de distribución de software durante la ejecución de la secuencia de tareas. Cuando se crea el medio independiente para una secuencia de tareas en el sitio de administración central, y la secuencia de tareas incluye un paso **Instalar paquete** , es posible que aparezca el siguiente error en el archivo CreateTsMedia.log:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>   
>  En medios independientes que incluyen un paso Instalar paquete, debe crear el medio independiente en un sitio primario que tenga el agente de distribución de software habilitado o agregar un paso **Ejecutar línea de comandos** después del paso **Instalar Windows y Configuration Manager** y antes del primer paso **Instalar paquete** . El paso **Ejecutar línea de comandos** ejecuta un comando de WMIC para habilitar el agente de distribución de software antes de que se ejecuta el primer paso Instalar paquete. Puede utilizar lo siguiente en su paso de secuencia de tareas **Ejecutar línea de comandos** :  
>   
>  **Línea de comandos**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  
>   
>  Para obtener información sobre cómo crear medios independientes, consulte [Crear medios independientes](../deploy-use/create-stand-alone-media.md).  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE.  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Instalar un solo paquete de software**  
 Esta configuración especifica un paquete de software de Configuration Manager. El paso esperará hasta que finalice la instalación.  

 **Instalar paquetes de software según la lista de variables dinámicas**  
 Esta configuración especifica el nombre base de un conjunto de variables de secuencia de tareas que se definen para una colección o un equipo. Estas variables especifican los paquetes que se instalarán para esa colección o equipo. Cada nombre de variable consta de su nombre base común además de un sufijo numérico que empieza en 001. El valor de cada variable debe contener un identificador de paquete y el nombre del software separado por dos puntos.  

 Para que el software pueda instalarse con una lista de variables dinámicas, debe habilitarse la siguiente configuración en la pestaña **Avanzadas** del cuadro de diálogo **Propiedades** del paquete: **Permitir que este programa se instale desde la secuencia de tareas de instalación de paquete sin implementarse**  

> [!NOTE]  
>  No se pueden instalar paquetes de software mediante una lista de variables dinámicas para las implementaciones de medios independientes.  

 Por ejemplo, para instalar un paquete de software mediante una variable de secuencia de tareas llamada AA001, especifique la siguiente variable:  

|Nombre de variable|Valor de variable|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

 Para instalar tres paquetes de software, debe especificar las siguientes variables:  

|Nombre de variable|Valor de variable|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

 Las siguientes condiciones afectarán a lo que se instala:  

-   Si el valor de una variable no se crea en el formato correcto o no se especifica un nombre y un identificador de aplicación válidos, se producirá un error en la instalación del software.  

-   Si el identificador de paquete contiene caracteres en minúsculas, se producirá un error en la instalación de software.  

-   Si no se encuentra ninguna variable con el nombre base especificado y el sufijo "001", no se instalará ningún paquete y la secuencia de tareas continuará.  

 **Continuar instalando otros paquetes en la lista si se produce un error de instalación de un paquete de software**  
 Esta configuración especifica que el paso continúa si se produce un error la instalación de un paquete de software. Si se especifica este valor, la secuencia de tareas continuará sin tener en cuenta los errores de instalación que se devuelven. Si no se especifica este valor y una instalación produce error, el paso de secuencia de tareas finalizará inmediatamente.  

##  <a name="BKMK_InstallSoftwareUpdates"></a> Instalar actualizaciones de software  
 Use el paso de secuencia de tareas **Instalar actualizaciones de software** para instalar las actualizaciones de software en el equipo de destino. No se evalúa si hay actualizaciones de software aplicables al equipo de destino hasta que se ejecuta este paso de secuencia de tareas. En ese momento, se evalúa si existen actualizaciones de software para el equipo de destino igual que para cualquier otro cliente administrado de Configuration Manager. En concreto, este paso solo instala las actualizaciones de software destinadas a las colecciones de las que el equipo es actualmente miembro.  
>  [!IMPORTANT]
>Es recomendable instalar la versión más reciente del agente de Windows Update para un rendimiento mucho mejor cuando se usa el paso de la secuencia de tareas Instalar actualizaciones de software.
>* Para Windows 7, consulte el [artículo de Knowledge Base 3161647](https://support.microsoft.com/kb/3161647).
>* Para Windows 8, consulte el [artículo de Knowledge Base 3163023](https://support.microsoft.com/kb/3163023).

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Instalar actualizaciones de software](task-sequence-action-variables.md#BKMK_InstallSoftwareUpdates).

 > [!NOTE]
 > Puede usar las variables integradas SMSTSMPListRequestTimeoutEnabled y SMSTSMPListRequestTimeout para habilitar y especificar la cantidad de milisegundos que espera una secuencia de tareas antes de volver a intentar instalar una aplicación después de no poder recuperar la lista de puntos de administración de los servicios de ubicación. Para obtener más información, consulte [Variables integradas de la secuencia de tareas](task-sequence-built-in-variables.md).

> [!NOTE]
>En la pestaña de opciones, puede configurar esta secuencia de tareas para volver a intentar si el equipo se reinicia inesperadamente. Por ejemplo, una instalación de actualización de software que reinicia automáticamente el equipo. A partir de Configuration Manager 1602, puede configurar la variable SMSTSWaitForSecondReboot para especificar cuánto tiempo (en segundos) debe durar la pausa de la secuencia de tareas después de reiniciar el equipo al instalar las actualizaciones de software. Para obtener más información, consulte [Variables integradas de la secuencia de tareas](task-sequence-built-in-variables.md).

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especifique esta opción para volver a intentar este paso si el equipo se reinicia inesperadamente. También puede especificar el número de reintentos después de un reinicio.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Necesario para la instalación: solo actualizaciones de software obligatorias**  
 Seleccione esta opción para instalar todas las actualizaciones de software etiquetadas en Configuration Manager como obligatorias para los equipos de destino que reciban la secuencia de tareas. Las actualizaciones de software obligatorias tienen fechas límite de instalación definidas por el administrador.  

 **Disponible para la instalación: todas las actualizaciones de software**  
 Seleccione esta opción para instalar todas las actualizaciones de software disponibles que tengan como destino la recopilación de Configuration Manager que recibirá la secuencia de tareas. Todas las actualizaciones de software disponibles se instalarán en los equipos de destino.  

 **Evaluación de las actualizaciones de software a partir de los resultados del análisis en caché**  
A partir de Configuration Manager versión 1606, puede realizar un análisis completo de las actualizaciones de software en lugar de usar los resultados del análisis almacenado en caché. De forma predeterminada, la secuencia de tareas utiliza los resultados almacenados en caché. Puede desactivar la casilla para que el cliente se conecte al punto de actualización de software para procesar y descargar el catálogo de actualizaciones de software más reciente. Seleccione esta opción cuando use una secuencia de tareas para [capturar y crear una imagen de sistema operativo](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md), donde se sabe que habrá un gran número de actualizaciones de software, especialmente muchas con dependencias (es necesario instalar X antes de que aparezca Y como procede). Al desactivar esta opción e implementar la secuencia de tareas en un gran número de clientes, todos se conectarán al punto de actualización de software al mismo tiempo. Esto podría producir problemas de rendimiento durante el proceso y la descarga del catálogo. En la mayoría de los casos, se recomienda utilizar la configuración predeterminada.

Se introdujo en Configuration Manager versión 1606 una nueva variable de secuencia de tareas, SMSTSSoftwareUpdateScanTimeout, para ofrecerle la capacidad de controlar el tiempo de espera para la detección de actualizaciones de software durante el paso de secuencia de tareas de instalación de actualizaciones de software. El valor predeterminado es 30 minutos. Para obtener más información, consulte [Variables integradas de la secuencia de tareas](task-sequence-built-in-variables.md).


##  <a name="BKMK_JoinDomainorWorkgroup"></a> Unirse a dominio o grupo de trabajo  
 Use el paso de secuencia de tareas **Unirse a dominio o grupo de trabajo** para agregar el equipo de destino a un grupo de trabajo o dominio.  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de secuencia de tareas de unión a un dominio o un grupo de trabajo](task-sequence-action-variables.md#BKMK_JoinDomainWorkgroup).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Unirse a un grupo de trabajo**  
 Seleccione esta opción para que el equipo de destino se una al grupo de trabajo especificado. Si el equipo pertenece actualmente a un dominio, la selección de esta opción hará que el equipo se reinicie.  

 **Unirse a un dominio**  
 Seleccione esta opción para que el equipo de destino se una al dominio especificado.  

 Si lo desea, escriba o busque una unidad organizativa (OU) en el dominio especificado para que se una el equipo. Si el equipo pertenece actualmente a otro dominio o grupo de trabajo, esto hará que el equipo se reinicie. Si el equipo ya pertenece a alguna otra unidad organizativa, Active Directory Domain Services no permitirán cambiar la unidad organizativa y este valor se omite.  

 **Especifique la cuenta que tiene permiso para unirse al dominio**  
 Haga clic en **Establecer** para especificar una cuenta y una contraseña que tenga permisos para unirse al dominio. La cuenta debe especificarse en el formato siguiente:  

 *Dominio\cuenta*  

## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> Preparar el cliente de Configuration Manager para la captura  
Use el paso **Preparar el cliente de Configuration Manager para la captura** para quitar el cliente de Configuration Manager o para configurar el cliente en el equipo de referencia y prepararlo para la captura como parte del proceso de creación de imágenes.

A partir de la versión 1610 de Configuration Manager, el paso Preparar el cliente de Configuration Manager quita por completo el cliente de Configuration Manager, en lugar de quitar solo la información de clave. Cuando la secuencia de tareas implementa la imagen capturada del sistema operativo, se instala un nuevo cliente de Configuration Manager cada vez.  

> [!Note]  
>  El cliente solo se quita durante la secuencia de tareas **Generar y capturar una imagen de sistema operativo de referencia**. Otros métodos de captura como los medios de captura o las secuencias de tareas personalizadas no quitarán el cliente.

Antes de la versión 1610 de Configuration Manager, este paso realiza las siguientes tareas:  

-   Quita la sección de propiedades de configuración de cliente del archivo smscfg.ini en el directorio de Windows. Estas propiedades incluyen información específica del cliente, como el GUID de Configuration Manager y otros identificadores de cliente.  

-   Elimina todos los certificados de equipo de Configuration Manager o SMS.  

-   Elimina la memoria caché del cliente de Configuration Manager.  

-   Borra la variable de sitio asignada del cliente de Configuration Manager.  

-   Elimina todas las directivas locales de Configuration Manager.  

-   Quita la clave raíz confiable del cliente de Configuration Manager.  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE.  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

##  <a name="BKMK_PrepareWindowsforCapture"></a> Prepare Windows for Capture  
 Use el paso de secuencia de tareas **Preparar Windows para la captura** para especificar las opciones de Sysprep que se usarán al capturar una imagen de sistema operativo en el equipo de referencia. Esta acción de secuencia de tareas ejecuta Sysprep y, a continuación, reinicia el equipo en la imagen de arranque de Windows PE especificada para la secuencia de tareas. Para que esta acción se complete correctamente, el equipo de referencia no debe estar unido a un dominio.  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Preparar Windows para la captura](task-sequence-action-variables.md#BKMK_PrepareWindowsCapture).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Generar automáticamente lista de controladores almacenamiento masivo**  
 Seleccione esta opción para que Sysprep genere automáticamente una lista de controladores de almacenamiento del equipo de referencia. Esta opción habilita la opción de compilar controladores de almacenamiento en el archivo sysprep.inf en el equipo de referencia. Para obtener más información sobre esta configuración, consulte la documentación de Sysprep.  

 **No restablecer la marca de activación**  
 Seleccione esta opción para impedir que Sysprep restablezca la marca de activación de producto.  

##  <a name="BKMK_PreProvisionBitLocker"></a> Tener en servicio BitLocker  
 Use el paso de secuencia de tareas **Tener en servicio BitLocker** para habilitar BitLocker en una unidad de disco en Windows PE. Sólo se cifra el espacio de la unidad que se utiliza, por ello los tiempos de cifrado son mucho más rápidos. Las opciones de administración de claves se aplican mediante el paso de secuencia de tareas [Habilitar BitLocker](#BKMK_EnableBitLocker) después de que se instale el sistema operativo. Este paso solo se ejecuta en Windows PE, no en sistemas operativos estándar.  

> [!IMPORTANT]  
>  Para tener en servicio BitLocker, debe implementar un sistema operativo mínimo de Windows 7 y el equipo debe admitir y tener habilitado TPM.  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Especifique un nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Especifique información detallada sobre la acción realizada en este paso.  

 **Aplicar BitLocker a la unidad especificada**  
 Especifique la unidad para la que desea habilitar BitLocker. Solo se cifra el espacio usado en la unidad.  

 **Omitir este paso para equipos que no tengan TPM o cuando TPM no esté habilitado**  
 Seleccione esta opción para omitir el cifrado de unidad cuando el hardware del equipo no es compatible con TPM o cuando TPM no está habilitado. Por ejemplo, puede usar esta opción al implementar un sistema operativo en una máquina virtual.  

##  <a name="BKMK_ReleaseStateStore"></a> Liberar almacén de estado  
 Use el paso de secuencia de tareas **Liberar almacén de estado** para notificar al punto de migración de estado que la acción de captura o restauración se ha completado. Este paso se usa conjuntamente con los pasos de secuencia de tareas **Solicitar almacén de estado**, **Capturar estado de usuario**y **Restaurar estado de usuario** para migrar datos de estado de usuario mediante la herramienta de migración de estado de usuario (USMT) y un punto de migración de estado.  

 Para obtener más información sobre cómo administrar el estado de usuario al implementar sistemas operativos, consulte [Administrar el estado de usuario](../get-started/manage-user-state.md).  

 Si solicitó acceso a un punto de migración de estado para capturar el estado de usuario en el paso de secuencia de tareas **Solicitar almacén de estado**  , este paso le notifica al punto de migración de estado que el proceso de captura se ha completado y que los datos de estado de usuario están disponibles para su restauración. El punto de migración de estado establece los permisos de control de acceso para el estado capturado de modo que solo sea accesible (como de solo lectura) para el equipo de la restauración.  

 Si solicitó acceso a un punto de migración de estado para restaurar el estado de usuario en el paso de secuencia de tareas **Solicitar almacén de estado** , este paso le notifica al punto de migración de estado que el proceso de restauración ha finalizado. En este momento, se activa cualquier configuración de retención que haya configurado para el punto de migración de estado.  

> [!IMPORTANT]  
>  Es recomendable establecer **Continuar después de un error** en los pasos de secuencia de tareas entre los pasos **Solicitar almacén de estado** y **Liberar almacén de estado** , de modo que cada acción de secuencia de tareas **Solicitar almacén de estado** coincida con una acción de secuencia de tareas **Liberar almacén de estado** .  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Liberar almacén de estado](task-sequence-action-variables.md#BKMK_ReleaseStateStore).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

##  <a name="BKMK_RequestStateStore"></a> Solicitar almacén de estado  
 Use el paso de secuencia de tareas **Solicitar almacén de estado** para solicitar acceso a un punto de migración de estado al capturar el estado de un equipo o restaurar el estado en un equipo.  

 Para obtener más información sobre cómo administrar el estado de usuario al implementar sistemas operativos, consulte [Administrar el estado de usuario](../get-started/manage-user-state.md).  

 Puede usar el paso de secuencia de tareas **Solicitar almacén de estado** conjuntamente con los pasos **Liberar almacén de estado**, **Capturar estado de usuario**y **Restaurar estado de usuario** para migrar el estado del equipo mediante un punto de migración de estado y la herramienta de migración de estado de usuario (USMT).  

> [!NOTE]  
>  Si acaba de establecer un se ha establecido un nuevo rol de sitio de punto de migración de estado (SMP), este puede tardar hasta una hora en estar disponible para el almacenamiento de estado de usuario. Para acelerar la disponibilidad del SMP, puede ajustar cualquier valor de propiedad del punto de migración de estado para que desencadene una actualización del archivo de control de sitio.  

 Este paso de secuencia de tareas se ejecuta en un sistema operativo estándar y en Windows PE para USMT sin conexión. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Solicitar almacén de estado](task-sequence-action-variables.md#BKMK_RequestState).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Capturar estado del equipo**  
 Busca un punto de migración de estado que cumpla los requisitos mínimos definidos en la configuración de punto de migración de estado (número máximo de clientes y cantidad mínima de espacio libre en disco), pero no garantiza que haya suficiente espacio en el momento de la migración de estado. Si selecciona esta opción, se solicitará acceso al punto de migración de estado con el fin de capturar el estado de usuario y la configuración de un equipo.  

 Si el sitio de Configuration Manager tiene varios puntos de migración de estado habilitados, este paso de secuencia de tareas buscará un punto de migración de estado que tenga espacio en disco disponible. Para ello, consultará el punto de administración del sitio para obtener una lista de puntos de migración de estado y evaluará cada uno de ellos hasta encontrar uno que cumpla los requisitos mínimos.  

 **Restaurar estado de otro equipo**  
 Seleccione esta opción para solicitar acceso a un punto de migración de estado con el fin de restaurar la configuración y el estado de usuario capturados anteriormente en un equipo de destino.  

 Si el sitio de Configuration Manager tiene varios puntos de migración de estado, este paso de secuencia de tareas busca el punto de migración de estado que tenga el estado del equipo que se ha almacenado para el equipo de destino.  

 **Número de reintentos**  
 Número de veces que este paso de secuencia de tareas intentará encontrar un punto de migración de estado adecuado antes de desistir.  

 **Intervalo entre reintentos (en segundos)**  
 Cantidad de tiempo en segundos que el paso de secuencia de tareas espera entre reintentos.  

 **Usar la cuenta de acceso de red si la cuenta de equipo no puede conectarse a un almacén de estado.**  
 Especifica que las credenciales de cuenta de acceso de red de Configuration Manager se usarán para conectarse al punto de migración de estado si el cliente de Configuration Manager no puede obtener acceso al almacén de estado de SMP con la cuenta de equipo. Esta opción es menos segura porque otros equipos podrían usar la cuenta de acceso de red para acceder a su estado almacenado, pero puede ser necesaria si el equipo de destino no está unido al dominio.  

##  <a name="BKMK_RestartComputer"></a> Reiniciar equipo  
 Use el paso de secuencia de tareas **Reiniciar equipo** para reiniciar el equipo que ejecuta la secuencia de tareas. Después del reinicio, el equipo continuará automáticamente con el siguiente paso de secuencia de tareas.  

 Este paso puede ejecutarse en un sistema operativo estándar o en Windows PE. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Reiniciar equipo](task-sequence-action-variables.md#BKMK_RestartComputer).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **La imagen de arranque asignada a esta secuencia de tareas**  
 Seleccione esta opción para que el equipo de destino use la imagen de arranque que está asignada a la secuencia de tareas. La imagen de arranque se usará para ejecutar los pasos posteriores de secuencia de tareas que se ejecutan en Windows PE.  

 **El sistema operativo predeterminado instalado actualmente**  
 Seleccione esta opción para que el equipo de destino se reinicie en el sistema operativo instalado.  

 **Informar al usuario antes de reiniciar**  
 Seleccione esta opción para informar al usuario de que se reiniciará el equipo de destino. Esta opción está seleccionada de forma predeterminada.  

 **Mensaje de notificación**  
 Escriba el mensaje de notificación que se muestra al usuario antes de que se reinicie el equipo de destino.  

 **Tiempo de espera de visualización de mensaje**  
 Especifique la cantidad de tiempo en segundos que se concederá al usuario antes de que se reinicie el equipo de destino. La cantidad de tiempo predeterminada es sesenta (60) segundos.  

##  <a name="BKMK_RestoreUserState"></a> Restaurar estado de usuario  
 Use el paso de secuencia de tareas **Restaurar estado de usuario** para iniciar la herramienta de migración de estado de usuario (USMT) con el fin de restaurar la configuración y el estado de usuario en el equipo de destino. Este paso de secuencia de tareas se usa junto con el paso **Capturar estado de usuario** .  

 Para obtener más información sobre cómo administrar el estado de usuario al implementar sistemas operativos, consulte [Administrar el estado de usuario](../get-started/manage-user-state.md).  

 También puede usar el paso de secuencia de tareas **Restaurar estado de usuario** con los pasos **Solicitar almacén de estado** y **Liberar almacén de estado** si quiere guardar la configuración de estado en un punto de migración de estado, o restaurar la configuración a partir de un punto de migración de estado, en el sitio de Configuration Manager. Con USMT 3.0 y versiones superiores, esta opción siempre descifra el almacén de estado de USMT mediante una clave de cifrado generada y administrada por Configuration Manager.  

 El paso de secuencia de tareas **Restaurar estado de usuario** proporciona control sobre un subconjunto limitado de las opciones de USMT más usadas. Con la variable de secuencia de tareas OSDMigrateAdditionalRestoreOptions se pueden especificar más opciones de línea de comandos.  

> [!IMPORTANT]  
>  Si usa el paso de secuencia de tareas **Restaurar estado de usuario** con una finalidad no relacionada con un escenario de implementación de sistema operativo, agregue el paso de secuencia de tareas [Reiniciar equipo](#BKMK_RestartComputer) inmediatamente después del paso **Restaurar estado de usuario** .  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Restaurar estado de usuario](task-sequence-action-variables.md#BKMK_RestoreUserState).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Especifica un nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Especifica más información detallada sobre la acción realizada en este paso.  

 **Paquete de herramientas de migración de estado de usuario**  
 Especifique el paquete de Configuration Manager que contiene la versión de USMT de este paso que se usará al restaurar la configuración y el estado de usuario. Este paquete no requiere un programa. Cuando se ejecuta el paso de secuencia de tareas, la secuencia de tareas usará la versión de USMT del paquete que especifique. Especifique un paquete que contenga la versión de 32 bits o x64 de USMT, en función de la arquitectura del sistema operativo en el que se restaura el estado.  

 **Restaurar todos los perfiles de usuario capturados con opciones estándar**  
 Restaura los perfiles de usuario capturados con las opciones estándar. Para personalizar las opciones que se restaurarán, seleccione **Personalizar captura de perfil de usuario**.  

 **Personalizar la restauración de perfiles de usuario**  
 Le permite personalizar los archivos que desea restaurar en el equipo de destino. Haga clic en **Archivos** para especificar los archivos de configuración en el paquete de USMT que desea usar para restaurar los perfiles de usuario. Para agregar un archivo de configuración, escriba el nombre del archivo en el cuadro **Nombre de archivo** y, a continuación, haga clic en **Agregar**. Los archivos de configuración que se usarán para la operación se muestran en el panel de archivos. El archivo .xml que especifique define el archivo de usuario que se restaurará.  

 **Restaurar perfiles de usuario de equipo local**  
 Restaura los perfiles de usuario (es decir, no el usuario de dominio) del equipo local. Deberá asignar nuevas contraseñas a las cuentas de usuario local restauradas porque no es posible migrar las contraseñas originales. Escriba la nueva contraseña en el cuadro **Contraseña** y confirme la contraseña en el cuadro **Confirmar contraseña** .  

 **Continuar si algunos archivos no se pueden restaurar**  
 Continúa restaurando la configuración y el estado de usuario incluso si algunos archivos no pueden restaurarse. Esta opción está habilitada de forma predeterminada. Si deshabilita esta opción y se producen errores durante la restauración de los archivos, el paso finalizará inmediatamente con un error y no se restaurarán todos los archivos.  

 **Habilitar el registro detallado**  
 Habilite esta opción para generar información más detallada en el archivo de registro. Al restaurar el estado, se genera el registro Loadstate.log, que se almacena de forma predeterminada en la carpeta de registro de la secuencia de tareas \windows\system32\ccm\logs.  

##  <a name="BKMK_RunCommandLine"></a> Ejecutar línea de comandos  
 Use el paso de secuencia de tareas **Ejecutar línea de comandos** para ejecutar una línea de comandos especificada.  

 Este paso puede ejecutarse en un sistema operativo estándar o en Windows PE. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Ejecutar línea de comandos](task-sequence-action-variables.md#BKMK_RunCommand).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Especifica un nombre corto definido por el usuario que describe la línea de comandos que se ejecuta.  

 **Descripción**  
 Especifica información más detallada sobre la línea de comandos que se ejecuta.  

 **Línea de comandos**  
 Especifica la línea de comandos que se ejecuta. Este campo es obligatorio. Es recomendable incluir extensiones de nombre de archivo, por ejemplo, .vbs y .exe. Incluya todos los archivos de configuración, las opciones de línea de comandos o los modificadores que sean necesarios.  

 Si el nombre de archivo no tiene una extensión de nombre de archivo especificada, Configuration Manager prueba con .com, .exe y .bat. Si el nombre de archivo tiene una extensión que no es un archivo ejecutable, Configuration Manager intenta aplicar una asociación local. Por ejemplo, si la línea de comandos es readme.gif, Configuration Manager inicia la aplicación especificada en el equipo de destino para abrir archivos .gif.  

 Ejemplos:  

 **setup.exe /a**  

 **cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat**  

> [!NOTE]  
>  Para que se ejecuten correctamente, las acciones de línea de comandos, como el redireccionamiento de la salida, la canalización o la copia (como en el ejemplo anterior), deben ir precedidas del comando **cmd.exe /c**.  

 **Deshabilitar el redireccionamiento del sistema de archivos de 64 bits**  
 De forma predeterminada, al ejecutar un sistema operativo de 64 bits, el archivo ejecutable en la línea de comandos se encuentra y ejecuta mediante el redirector del sistema de archivos WOW64 para que se encuentren las versiones de 32 bits de los ejecutables del sistema operativo y los archivos DLL.  Si selecciona esta opción, se deshabilita el uso del redirector del sistema de archivos WOW64 para que se puedan encontrar las versiones nativas de 64 bits de los ejecutables del sistema operativo y los archivos DLL.  Seleccionar esta opción no tiene ningún efecto cuando se ejecuta en un sistema operativo de 32 bits.  

 **Iniciar en**  
 Especifica la carpeta ejecutable para el programa, con un máximo de 127 caracteres. Esta carpeta puede ser una ruta de acceso absoluta en el equipo de destino, o una ruta de acceso relacionada con la carpeta del punto de distribución que contiene el paquete. Este campo es opcional.  

 Ejemplos:  

 **c:\officexp**  

 **i386**  

> [!NOTE]  
>  El botón **Examinar** examina los archivos y las carpetas del equipo local, por lo que cualquier cosa que se seleccione de este modo, también existirá en la misma ubicación del equipo de destino y con los mismos nombres de archivo y carpeta.  

 **Paquete**  
 Al especificar en la línea de comandos archivos o programas que aún no están presentes en el equipo de destino, seleccione esta opción para especificar el paquete de Configuration Manager que contiene los archivos adecuados. El paquete no requiere un programa. Esta opción no es necesaria si los archivos especificados existen en el equipo de destino.  

 **Tiempo de espera**  
 Especifica un valor que representa el tiempo que Configuration Manager permitirá la ejecución de la línea de comandos. Este valor puede estar comprendido entre 1 minuto y 999 minutos. El valor predeterminado es 15 minutos.  

 Esta opción está deshabilitada de forma predeterminada.  

> [!IMPORTANT]  
>  Si escribe un valor que no permita un tiempo suficiente para que el paso de secuencia de tareas “Ejecutar línea de comandos” se complete correctamente, se producirá un error en el paso y, en función del resto de opciones de control, también en la secuencia de tareas completa. Si se agota el tiempo de espera, Configuration Manager finalizará el proceso de línea de comandos.  

 **Ejecutar esta etapa como la cuenta siguiente**  
 Especifica que la línea de comandos se ejecuta como una cuenta de usuario de Windows diferente de la cuenta de sistema local.  

> [!NOTE]  
>  Cuando se especifica otra cuenta para este paso y se produce después de un paso de instalación del sistema operativo, la cuenta debe agregarse al equipo antes de que pueden ejecutarse scripts o comandos sencillos, y el perfil para la cuenta de usuario de Windows debe restaurarse para ejecutar programas más complejos, como un archivo MSI.  

 **Cuenta**  
 Especifica la cuenta de usuario de ejecución como Windows para la tarea de línea de comandos en la secuencia de tareas que se va a ejecutar mediante esta acción. La línea de comandos se ejecutará con los permisos de la cuenta especificada. Haga clic en **Establecer** para especificar la cuenta de usuario o dominio local.  

> [!IMPORTANT]  
>  Si una acción de secuencia de tareas **Ejecutar línea de comandos** que especifica una cuenta de usuario se ejecuta en Windows PE, se producirá un error en la acción porque Windows PE no puede unirse a un dominio. El error se registrará en el archivo smsts.log.  

##  <a name="BKMK_RunPowerShellScript"></a> Ejecutar script de PowerShell  
 Use el paso de secuencia de tareas **Ejecutar script PowerShell** para ejecutar un script de PowerShell especificado.  

 Este paso puede ejecutarse en un sistema operativo estándar o en Windows PE. Para ejecutar este paso en Windows PE, PowerShell debe estar habilitado en la imagen de arranque. Puede habilitar Windows PowerShell (WinPE-PowerShell) desde la pestaña **Componentes opcionales** de las propiedades de la imagen de arranque. Para obtener más información sobre cómo modificar una imagen de arranque, consulte [Administrar imágenes de arranque](../get-started/manage-boot-images.md).  

> [!NOTE]  
>  PowerShell no está habilitado de forma predeterminada en los sistemas operativos Windows Embedded.  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Especifica un nombre corto definido por el usuario que describe la línea de comandos que se ejecuta.  

 **Descripción**  
 Especifica información más detallada sobre la línea de comandos que se ejecuta.  

 **Paquete**  
 Especifique el paquete de Configuration Manager que contiene el script de PowerShell. Un paquete puede contener varios scripts de PowerShell.  

 **Nombre de script**  
 Especifica el nombre del script de PowerShell que se va a ejecutar. Este campo es obligatorio.  

 **Parámetros**  
 Especifica los parámetros que se pasarán al script de Windows PowerShell. Configure los parámetros como si los agregase al script de Windows PowerShell desde una línea de comandos.  

> [!IMPORTANT]  
>  Proporcione parámetros usados por el script, no por la línea de comandos de Windows PowerShell.  
>   
>  El ejemplo siguiente contiene parámetros válidos:  
>   
>  **-MyParameter1 MyValue1 -MyParameter2 MyValue2**  
>   
>  El ejemplo siguiente contiene parámetros no válidos. Los elementos en negrita son parámetros de línea de comandos de Windows PowerShell (-nologo y –executionpolicy unrestricted) no usados por el script.  
>   
>  **-nologo-executionpolicy unrestricted-File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2**  

 **Directiva de ejecución de PowerShell**  
 Seleccionar esta opción permite determinar qué scripts de Windows PowerShell (en su caso) se podrán ejecutar en el equipo. Elija una de las siguientes directivas de ejecución:  

-   **AllSigned**: solo se pueden ejecutar scripts firmados por un editor de confianza.  

-   **Sin definir**: no está definida ninguna directiva de ejecución. .  

-   **Desviar**: carga todos los archivos de configuración y ejecuta todos los scripts. Si ejecuta un script sin firma que se descargó de Internet, no se le pedirá confirmación antes de ejecutarlo.  

> [!IMPORTANT]  
>  PowerShell 1.0 no admite las directivas de ejecución Sin definir ni Desviar.  

##  <a name="BKMK_SetDynamicVariables"></a> Establecer variables dinámicas  
 Use el paso de secuencia de tareas **Establecer variables dinámicas** para realizar lo siguiente:  

1.  Recopilar información del equipo y del entorno en el que se encuentra y, a continuación, establecer las variables de secuencia de tareas con esa información.  

2.  Evaluar reglas definidas y establecer las variables de secuencia de tareas basadas en las variables y los valores configurados para las reglas que se evalúan como true.  

 La secuencia de tareas establece automáticamente las siguientes variables de la secuencia de tareas de solo lectura:  

 -   &#95;SMSTSMake  

 -   &#95;SMSTSModel  

 -   &#95;SMSTSMacAddresses  

 -   &#95;SMSTSIPAddresses  

 -   &#95;SMSTSSerialNumber  

 -   &#95;SMSTSAssetTag  

 -   &#95;SMSTSUUID  

 Este paso puede ejecutarse en un sistema operativo estándar o en Windows PE. Para obtener más información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de secuencias de tareas](task-sequence-action-variables.md).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

**Nombre**  
 Nombre corto definido por el usuario para este paso de secuencia de tareas.  

**Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

**Variables y reglas dinámicas**  
 Para establecer una variable dinámica que se use en la secuencia de tareas, puede agregar una regla y luego especificar un valor para cada variable que especifique para la regla, o agregar una o más variables para establecerlas sin agregar una regla. Al agregar una regla, puede elegir entre las siguientes categorías de regla:  

 -   **Equipo**: use esta categoría de regla para evaluar los valores de la etiqueta de inventario, el UUID, el número de serie o la dirección mac. Puede establecer varios valores y, si cualquier valor es true, la regla se evaluará como true. Por ejemplo, la siguiente regla se evalúa en true si el número de serie es 5892087 independientemente de si la dirección MAC equivale a 26-78-13-5A-A4-22.  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

-   **Ubicación**: use esta categoría de regla para evaluar los valores de la puerta de enlace predeterminada.  

-   **Marca y modelo**: use esta categoría de regla para evaluar los valores de marca y modelo de un equipo. La marca y el modelo deben evaluarse como true para que la regla se evalúe como true.   

    A partir de la versión 1610 de Configuration Manager, puede especificar un asterisco (*****) y un signo de interrogación (**?**) como caracteres comodín, donde ***** coincide con varios caracteres y **?** coincide con un carácter simple. Por ejemplo, la cadena "DELL*900?" coincidirá con DELL-ABC-9001 y con DELL9009.

-   **Variable de secuencia de tareas**: use esta categoría de regla para agregar una variable de secuencia de tareas, la condición y el valor que quiere evaluar. La regla se evalúa como true cuando el valor establecido para la variable cumple la condición especificada.  

Puede especificar una o más variables que se establecerán para una regla que se evalúa como true o establecer variables sin usar una regla. Puede seleccionar entre las variables existentes o crear una variable personalizada.  

 -   **Variables de secuencia de tareas existentes**: use esta opción para seleccionar una o más variables en una lista de variables de secuencia de tareas existente. Las variables de matriz no están disponibles para seleccionar.  

 -   **Variables de secuencia de tareas personalizadas**: use esta opción para definir una variable de secuencia de tareas personalizada. También puede especificar una variable de secuencia de tareas existente. Esto es útil para especificar una matriz de variables existente, como OSDAdapter, ya que las matrices de variables no están en la lista de variables de secuencia de tareas existentes.  

Después de seleccionar las variables de una regla, debe proporcionar un valor para cada variable. La variable se establece en el valor especificado cuando la regla se evalúa como true. Para cada variable, puede seleccionar **Valor secreto** para ocultar el valor de la variable. De forma predeterminada, algunas de las variables existentes ocultan valores, como la variable de secuencia de tareas de OSDCaptureAccountPassword.  

> [!IMPORTANT]  
>  Al importar una secuencia de tareas con el paso “Establecer variables dinámicas”, y **Valor secreto** está seleccionado para el valor de la variable, el valor se quita al importar la secuencia de tareas. Como resultado, debe volver a escribir el valor de la variable dinámica después de importar la secuencia de tareas.  

##  <a name="BKMK_SetTaskSequenceVariable"></a> Establecer variable de secuencia de tareas  
Use el paso de secuencia de tareas **Configurar variable de secuencia de tareas** para establecer el valor de una variable que se utiliza con la secuencia de tareas.  

Este paso puede ejecutarse en un sistema operativo estándar o en Windows PE. Las variables de secuencia de tareas son leídas por acciones de secuencia de tareas y especifican el comportamiento de esas acciones. Para obtener más información sobre las variables de secuencia de tareas específicas, consulte [Variables de acción de secuencias de tareas](task-sequence-action-variables.md).  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario para este paso de secuencia de tareas.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Variable de secuencia de tareas**  
 Nombre definido por el usuario para la variable de secuencia de tareas.  

 **Valor**  
 Valor que está asociado a la variable de secuencia de tareas. El valor puede ser otra variable de secuencia de tareas en la sintaxis\>%<nombre de variable>%.  

## <a name="hide-task-sequence-progress"></a>Ocultación del progreso de la secuencia de tareas
<!-- 1354291 -->
Con la versión 1706, puede controlar cuándo se muestra el progreso de la secuencia de tareas a los usuarios finales mediante una variable nueva. En la secuencia de tareas, use el paso **Configurar variable de secuencia de tareas** para establecer el valor de la variable **TSDisableProgressUI** a fin de ocultar o mostrar el progreso de la secuencia de tareas. Puede usar el paso Configurar variable de secuencia de tareas varias veces en una secuencia de tareas para cambiar el valor de la variable. Esto le permite ocultar o mostrar el progreso de la secuencia de tareas en secciones diferentes de la secuencia de tareas.

 - **Para ocultar el progreso de la secuencia de tareas**  
En el editor de la secuencia de tareas, use el paso [Configurar variable de secuencia de tareas](#BKMK_SetTaskSequenceVariable) para establecer el valor de la variable **TSDisableProgressUI** en **True** para ocultar el progreso de la secuencia de tareas.

 - **Para mostrar el progreso de la secuencia de tareas**  
En el editor de la secuencia de tareas, use el paso [Configurar variable de secuencia de tareas](#BKMK_SetTaskSequenceVariable) para establecer el valor de la variable **TSDisableProgressUI** en **False** para mostrar el progreso de la secuencia de tareas.

##  <a name="BKMK_SetupWindowsandConfigMgr"></a> Instalar Windows y Configuration Manager  
 Use el paso de secuencia de tareas **Instalar Windows y Configuration Manager** para realizar la transición desde Windows PE al nuevo sistema operativo. Este paso de secuencia de tareas es una parte necesaria de cualquier implementación de sistema operativo. Se instala el cliente de Configuration Manager en el nuevo sistema operativo y se prepara para que la secuencia de tareas continúe con la ejecución en el sistema operativo.  

 Este paso solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Instalar Windows y Configuration Manager](task-sequence-action-variables.md#BKMK_SetupWindows).  

 La acción de secuencia de tareas **Instalar Windows y Configuration Manager** reemplaza las variables de directorio sysprep.inf o unattend.xml, como %WINDIR% y %ProgramFiles%, por el directorio de instalación de Windows PE X:\Windows. Las variables de secuencia de tareas especificadas mediante estas variables de entorno se omitirán.  

 Use este paso de secuencia de tareas para realizar las siguientes acciones:  

1.  Pasos preliminares: Windows°PE  

    1.  Realiza la sustitución de las variables de secuencia de tareas en el archivo unattend.xml.  

    2.  Descarga el paquete que contiene el cliente de Configuration Manager y lo coloca en la imagen implementada.  

2.  Configurar Windows  

    1.  Instalación basada en imagen.  

        1.  Deshabilita el cliente de Configuration Manager en la imagen (es decir, deshabilita el inicio automático del servicio de cliente de Configuration Manager).  

        2.  Actualiza el Registro en la imagen implementada para asegurarse de que el sistema operativo implementado se inicia con la misma letra de unidad que tenía en el equipo de referencia.  

        3.  Se reinicia en el sistema operativo implementado.  

        4.  La instalación mínima de Windows se ejecuta con los archivos sysprep.inf o unattend.xml especificados anteriormente que tienen suprimida toda la interacción del usuario final. Nota: Si en **Aplicar configuración de red** se especificó la unión a un dominio, entonces esa información se encuentra en los archivos sysprep.inf o unattend.xml, y la instalación mínima de Windows realiza la unión al dominio.  

    2.  Instalación basada en Setup.exe.  Ejecuta Setup.exe que sigue el proceso de instalación típico de Windows:  

        1.  Copia en la unidad de disco duro el paquete de instalación de sistema operativo especificado en una secuencia de tareas **Aplicar el sistema operativo** anterior.  

        2.  Se reinicia en el sistema operativo recién implementado.  

        3.  La instalación mínima de Windows se ejecuta con los archivos sysprep.inf o unattend.xml especificados anteriormente que tienen suprimida la configuración de la interfaz de usuario. Nota: Si en **Aplicar configuración de red** se especificó la unión a un dominio, entonces esa información se encuentra en los archivos sysprep.inf o unattend.xml, y la instalación mínima de Windows realiza la unión al dominio.  

3.  Configurar el cliente de Configuration Manager  

    1.  Una vez finalizada la instalación mínima de Windows, la secuencia de tareas se reanuda mediante setupcomplete.cmd.  

    2.  Habilita o deshabilita la cuenta de administrador local, según la opción seleccionada en el paso **Aplicar configuraciones de Windows** .  

    3.  Instala el cliente de Configuration Manager mediante el paquete descargado anteriormente (1.b) y las propiedades de instalación especificadas en el Editor de secuencia de tareas. El cliente se instala en “modo de aprovisionamiento” para impedir que procese nuevas solicitudes de directiva hasta que se haya completado la secuencia de tareas.  

    4.  Espera a que el cliente esté totalmente operativo.  

    5.  Si el equipo está funcionando en un entorno con Protección de acceso a redes habilitada, el cliente busca e instala todas las actualizaciones necesarias para que estén presentes antes de que la secuencia de tareas continúe ejecutándose.  

4.  La secuencia de tareas continúa ejecutándose con el paso siguiente.  

> [!NOTE]  
>  La acción de secuencia de tareas **Instalar Windows y Configuration Manager** es la encargada de ejecutar la directiva de grupo en el equipo recién instalado. La directiva de grupo se aplica una vez finalizada la secuencia de tareas.  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   No seleccione para que la secuencia de tareas continúe aunque se produzca un error durante la ejecución del paso. Si se produce un error, habrá un error en la secuencia de tareas, tanto si selecciona esta opción como si no.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Especifica un nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Especifica información detallada adicional sobre la acción realizada en este paso.  

 **Paquete de cliente**  
 Especifica el paquete de instalación de cliente de Configuration Manager que se usará en este paso de secuencia de tareas. Haga clic en **Examinar** y seleccione el paquete de instalación de cliente que quiera usar para instalar el cliente de Configuration Manager.  

 **Usar el paquete de cliente de preproducción cuando esté disponible**  
 Especifica que si hay un paquete de cliente de preproducción disponible, el paso de secuencia de tareas usará este paquete en lugar del paquete de cliente de producción. Normalmente, el cliente de preproducción es una versión más reciente que se está probando en el entorno de producción. Haga clic en **Examinar** y seleccione el paquete de instalación de cliente de preproducción que quiera usar para instalar el cliente de Configuration Manager.  

 **Propiedades de instalación**  
 La acción de secuencia de tareas especifica automáticamente la asignación de sitios y la configuración predeterminada. Puede usar este campo para especificar propiedades de instalación adicionales que se utilizarán al instalar el cliente. Si desea especificar varias propiedades de instalación, sepárelas con un espacio.  

 Puede especificar opciones de línea de comandos para que se usen durante la instalación de cliente. Por ejemplo, puede escribir **/skipprereq: silverlight.exe** para informar a CCMSetup.exe que no instale el requisito previo de Microsoft Silverlight. Para obtener más información sobre las opciones de líneas de comandos disponibles para CCMSetup.exe, consulte [Acerca de las propiedades de instalación de clientes](../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="BKMK_UpgradeOS"></a> Actualizar el sistema operativo  
 Use el paso de secuencia de tareas **Actualizar sistema de operativo** para actualizar un sistema operativo Windows 7, Windows 8, Windows 8.1 o Windows 10 existente a Windows 10.  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE.  

### <a name="details"></a>Detalles  
 En la pestaña **Propiedades** de este paso, puede configurar las opciones descritas en esta sección.  

 Además, use la pestaña **Opciones** para realizar las siguientes acciones:  

-   Deshabilitar el paso.  

-   Especificar si la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  

-   Especificar las condiciones que deben cumplirse para que se ejecute el paso.  

 **Nombre**  
 Nombre corto definido por el usuario que describe la acción realizada en este paso.  

 **Descripción**  
 Información detallada adicional sobre la acción realizada en este paso.  

 **Paquete de actualización**  
 Seleccione esta opción para especificar el paquete de actualización del sistema operativo de Windows 10 que se usará para la actualización.  

 **Ruta de origen**  
 Especifica una ruta local o de red a los medios de Windows 10 que se deben usar (corresponde a la opción de línea de comandos /installFrom). También puede especificar una variable, como %mycontentpath% o %DPC01%. Cuando se use una variable para la ruta de origen, debe especificarse previamente en la secuencia de tareas. Por ejemplo, si usa el paso [Descargar contenido de paquete](#BKMK_DownloadPackageContent) en la secuencia de tareas, puede especificar una variable para la ubicación del paquete de actualización del sistema operativo. A continuación, puede usar esa variable para la ruta de origen para este paso.  

 **Edición**  
 Especifique la edición en los medios del sistema operativo que se usará para la actualización.  

 **Clave de producto**  
 Especifique la clave de producto que se debe aplicar al proceso de actualización.  

 **Proporcionar el contenido del controlador siguiente al programa de configuración de Windows durante la actualización**  
 Seleccione esta opción para agregar controladores al equipo de destino durante el proceso de actualización (corresponde a la opción de línea de comandos /InstallDriver). Los controladores deben ser compatibles con Windows 10. Especifique una de las siguientes opciones:  

-   **Paquete de controladores**: haga clic en **Examinar** y seleccione un paquete de controladores existente en la lista.  

-   **Contenido almacenado provisionalmente**: seleccione esta opción para especificar la ubicación del paquete de controladores. Puede especificar una carpeta local, la ruta de red o una variable de secuencia de tareas. Cuando se use una variable para la ruta de origen, debe especificarse previamente en la secuencia de tareas. Por ejemplo, mediante el paso [Descargar contenido de paquete](task-sequence-steps.md#BKMK_DownloadPackageContent).  

 **Tiempo de espera (minutos)**  
 Especifica el número de minutos que la instalación debe ejecutarse antes de que Configuration Manager considere que se ha producido un error en el paso de secuencia de tareas.  

 **Realizar examen de compatibilidad del programa de instalación de Windows sin iniciar la actualización**  
 Especifica que se realice el examen de compatibilidad de la instalación de Windows sin iniciar el proceso de actualización (corresponde a la opción de línea de comandos /Compat ScanOnly). También debe implementar el origen de instalación completo cuando use esta opción. La instalación devuelve un código de salida como resultado de la exploración. En la tabla siguiente se proporcionan algunos de los códigos de salida más comunes.  

|Código de salida|Detalles|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|No hay problemas de compatibilidad ("correcto").|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Problemas de compatibilidad accionables.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|La opción de migración seleccionada no está disponible. Por ejemplo, una actualización de Enterprise a Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|No elegible para Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|No hay suficiente espacio en disco libre.|  

 Para más información sobre este parámetro, vea [Opciones de la línea de comandos del programa de instalación de Windows](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx).  

 **Omitir cualquier mensaje de compatibilidad descartable**  
 Especifica que el programa de instalación completa la instalación, omitiendo los mensajes de compatibilidad descartables (corresponde a la opción de línea de comandos /Compat IgnoreWarning).  

 **Actualizar programa de instalación de Windows dinámicamente con Windows Update**  
 Especifica si el programa de instalación llevará a cabo las operaciones de actualización dinámica, como buscar, descargar e instalar actualizaciones (corresponde a la opción de línea de comandos /DynamicUpdate). Esta configuración no es compatible con las actualizaciones de software de Configuration Manager, pero se puede habilitar al controlar las actualizaciones con WSUS (independiente) o Windows Update.  

 **Invalidar directiva y usar Microsoft Update predeterminado**: seleccione esta opción para invalidar temporalmente la directiva local en tiempo real para ejecutar operaciones de actualización dinámica y que el equipo obtenga actualizaciones de Windows Update.  
