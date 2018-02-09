---
title: Pasos de la secuencia de tareas
titleSuffix: Configuration Manager
description: "Obtenga información sobre los pasos de la secuencia de tareas que puede agregar a una secuencia de tareas de Configuration Manager."
ms.custom: na
ms.date: 01/12/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
caps.latest.revision: 
caps.handback.revision: 
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 5320d7747f7e2c6164da8c1801e631b749935d6d
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2018
---
# <a name="task-sequence-steps-in-system-center-configuration-manager"></a>Pasos de la secuencia de tareas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los siguientes pasos de secuencia de tareas se pueden agregar a una secuencia de tareas de Configuration Manager. Para obtener información sobre cómo editar una secuencia de tareas, consulte [Editar una secuencia de tareas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

Las opciones siguientes son comunes a todos los pasos de secuencia de tareas:

En la pestaña **Propiedades**:
 - **Nombre**: el editor de secuencia de tareas requiere que se especifique un nombre corto para describir este paso. Cuando se agrega un paso nuevo, el editor de secuencia de tareas establece el nombre en Tipo de forma predeterminada. La longitud de **Nombre** no puede superar los 50 caracteres.
 - **Descripción**: si quiere, especifique información más detallada sobre este paso. La longitud de **Descripción** no puede superar los 256 caracteres.
En el resto de este artículo se describen los demás valores de la pestaña **Propiedades** para cada paso de secuencia de tareas.

En la pestaña **Opciones**:  
-   **Deshabilitar este paso**: la secuencia de tareas omite este paso cuando se ejecuta en un equipo. El icono para este paso está atenuado en el editor de secuencia de tareas. 
-   **Continuar después de un error**: la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso.  
-   **Agregar condición**: la secuencia de tareas evalúa estas instrucciones condicionales para determinar si se ejecuta el paso.   
En las secciones siguientes para pasos de secuencia de tareas específicos se describen otros valores posibles en la pestaña **Opciones**.



##  <a name="BKMK_ApplyDataImage"></a> Aplicar imágenes de datos   
 Use este paso para copiar la imagen de datos en la partición de destino especificada.  

 Este paso solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para más información sobre las variables de secuencia de tareas, vea [Variables de acción de secuencias de tareas](task-sequence-action-variables.md).  

En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Imágenes** y seleccione **Aplicar imagen de datos** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Paquete de imágenes**  
 Haga clic en **Examinar** para especificar el **Paquete de imágenes** que se usa en esta secuencia de tareas. Seleccione el paquete que desea instalar en el cuadro de diálogo **Seleccionar un paquete** . La información de propiedades de los paquetes de imágenes se muestra en la parte inferior del cuadro de diálogo **Seleccionar un paquete** . En la lista desplegable, seleccione la **Imagen** que desea instalar desde el **Paquete de imágenes**seleccionado.  

> [!NOTE]  
>  Esta acción de secuencia de tareas trata la imagen como un archivo de datos. Esta acción no realiza ninguna configuración para arrancar la imagen como un sistema operativo.  

 **Destino**  
 Configure una de las opciones siguientes:

-   **Siguiente partición disponible:** use la siguiente partición secuencial que no haya sido destino previo de las acciones **Aplicar el sistema operativo** o **Aplicar imagen de datos** en esta secuencia de tareas.  

-   **Disco y partición específicos**: seleccione el número de **Disco** (empezando por 0) y el número de **Partición** (empezando por 1).  

-   **Letra de unidad lógica específica**: especifique la **Letra de unidad** asignada a la partición por Windows PE. Esta letra de unidad puede ser diferente de la que asigna el sistema operativo recién implementado.  

-   **Letra de unidad lógica almacenada en una variable**: especifique la variable de secuencia de tareas que contiene la letra de unidad asignada a la partición por Windows PE. Normalmente, esta variable se establece en la sección Avanzado del cuadro de diálogo **Propiedades de la partición** de la acción de la secuencia de tareas **Formatear y crear particiones en el disco**.  

**Eliminar todo el contenido en la partición antes de aplicar la imagen**  
 Especifica que la secuencia de tareas elimina todos los archivos en la partición de destino antes de instalar la imagen. Si no se elimina el contenido de la partición, este paso puede usarse para aplicar contenido adicional a una partición de destino previa.  



##  <a name="BKMK_ApplyDriverPackage"></a> Aplicar paquete de controladores  
 Use este paso para descargar todos los controladores del paquete de controladores e instalarlos en el sistema operativo Windows.

 El paso de secuencia de tareas **Aplicar paquete de controladores** hace que todos los controladores de dispositivo incluidos en un paquete de controladores estén disponibles para su uso con Windows. Agregue este paso entre los pasos **Aplicar el sistema operativo** e **Instalar Windows y Configuration Manager** para que los controladores del paquete estén disponibles para Windows. Normalmente, el paso **Aplicar paquete de controladores** va después del paso de secuencia de tareas **Aplicar controladores automáticamente** . El paso de secuencia de tareas **Aplicar paquete de controladores** también es útil en escenarios de implementación de medios independientes.  

 Asegúrese de que los controladores de dispositivo similares se colocan en un paquete de controladores y distribúyalos a los puntos de distribución adecuados. Una vez distribuidos, los equipos cliente de Configuration Manager pueden instalarlos. Por ejemplo, coloque todos los controladores de un fabricante en un paquete de controladores. Después, distribuya el paquete a puntos de distribución a los que los equipos asociados puedan tener acceso.

 El paso **Aplicar paquete de controladores** resulta útil para medios independientes. Este paso también es útil si quiere instalar un conjunto específico de controladores. Estos tipos de controladores incluyen los dispositivos que no se detectarán en un análisis de Plug and Play, como las impresoras de red.  

 Este paso de secuencia de tareas solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Aplicar paquetes de controladores](task-sequence-action-variables.md#BKMK_ApplyDriverPackage).  

En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Controladores** y seleccione **Aplicar paquete de controladores** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Paquete de controladores**  
 Especifique el paquete de controladores que contiene los controladores de dispositivo necesarios. Para ello, haga clic en **Examinar** e inicie el cuadro de diálogo **Seleccionar un paquete** . Especifique un paquete existente para que esté disponible. Las propiedades asociadas del paquete se muestran en la parte inferior del cuadro de diálogo.  

 **Seleccionar en el paquete el controlador de almacenamiento que debe instalarse antes de la configuración en sistemas operativos anteriores a Windows Vista**  
 Especifique los controladores de almacenamiento masivo necesarios para instalar un sistema operativo clásico.  

 **Controlador**  
 Seleccione el archivo de controlador de almacenamiento masivo para instalar antes de la instalación de un sistema operativo clásico. La lista desplegable se rellena con el paquete especificado.  

 **Modelo**  
 Especifique el dispositivo crítico para el arranque que se necesita en implementaciones de sistemas operativos anteriores a Windows Vista.  

 **Llevar a cabo la instalación desatendida de controladores no firmados en versiones de Windows en las que se permita**  
 Esta opción permite que Windows instale controladores sin una firma digital.  



##  <a name="BKMK_ApplyNetworkSettings"></a> Aplicar configuración de red   
 Use este paso para especificar la información de configuración de red o grupo de trabajo del equipo de destino. La secuencia de tareas almacena estos valores en el archivo de respuesta adecuado. El programa de instalación de Windows usa este archivo de respuesta durante la acción **Instalar Windows y Configuration Manager**.  

 Este paso de secuencia de tareas se ejecuta en un sistema operativo estándar o en Windows PE. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Aplicar configuración de red](task-sequence-action-variables.md#BKMK_ApplyNetworkSettings).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Configuración** y seleccione **Aplicar configuración de red** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Unirse a un grupo de trabajo**  
 Seleccione esta opción para que el equipo de destino se una al grupo de trabajo especificado. Escriba el nombre del grupo de trabajo en la línea **Grupo de trabajo** . Este valor puede reemplazarse por el valor que se captura mediante el paso de secuencia de tareas **Capturar configuración de red** .  

 **Unirse a un dominio**  
 Seleccione esta opción para que el equipo de destino se una al dominio especificado. Especifique o busque el dominio, como *fabricam.com*. Especifique o busque una ruta de acceso de protocolo ligero de acceso a directorios (LDAP) de una unidad organizativa. Por ejemplo: *LDAP//OU=computers, DC=Fabricam.com, C=com*  

 **Cuenta**  
 Haga clic en **Establecer** para especificar una cuenta con los permisos necesarios para unir el equipo al dominio. En el cuadro de diálogo **Cuenta de usuario de Windows** puede escribir el nombre de usuario con el formato siguiente: **Dominio\Usuario**.  

 **Configuración del adaptador**  
 Especifique la configuración de red para cada adaptador de red del equipo. Haga clic en **Nuevo** para abrir el cuadro de diálogo **Configuración de red** y después especifique la configuración de red. Si también usa el paso **Capturar configuración de red**, la secuencia de tareas aplica al adaptador de red los valores capturados anteriormente. La secuencia de tareas no aplica la configuración especificada en este paso. Si la secuencia de tareas no ha capturado previamente la configuración de red, aplica la configuración especificada en el paso **Aplicar configuración de red**. La secuencia de tareas aplica esta configuración a los adaptadores de red en el orden de enumeración de los dispositivos de Windows.  



##  <a name="BKMK_ApplyOperatingSystemImage"></a> Aplicar imagen de sistema operativo  

> [!TIP]  
> A partir de la versión 1709 de Windows 10, los medios incluyen varias ediciones. Cuando se configura una secuencia de tareas para usar un paquete de actualización del sistema operativo o una imagen del sistema operativo, no olvide seleccionar una [edición admitida](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

 Use este paso para instalar un sistema operativo en el equipo de destino. Este paso realiza acciones en función de si usa una imagen de sistema operativo o un paquete de actualización del sistema operativo.  

 El paso **Aplicar imagen de sistema operativo** realiza las acciones siguientes cuando se usa una imagen de sistema operativo:  

1.  Elimina todo el contenido en el volumen de destino, excepto los archivos de la carpeta que especifica la variable &#95;SMSTSUserStatePath.

2.  Extrae el contenido del archivo .wim especificado en la partición de destino especificada.  

3.  Prepara el archivo de respuesta:  

    1.  Crea un nuevo archivo de respuesta predeterminado de instalación de Windows (sysprep.inf o unattend.xml) para el sistema operativo que se va a implementar.  

    2.  Combina los valores del archivo de respuesta proporcionado por el usuario.  

4.  Copia los cargadores de arranque de Windows en la partición activa.  

5.  Configura el archivo boot.ini o la base de datos de la configuración de arranque (BCD) para que hagan referencia al sistema operativo que se acaba de instalar.  

 El paso **Aplicar imagen de sistema operativo** realiza las acciones siguientes cuando se usa un paquete de actualización del sistema operativo:  

1.  Elimina todo el contenido en el volumen de destino, excepto los archivos de la carpeta que especifica la variable &#95;SMSTSUserStatePath.  

2.  Prepara el archivo de respuesta:  

    1.  Cree un archivo de respuesta nuevo con los valores estándar creados por Configuration Manager.  

    2.  Combina los valores del archivo de respuesta proporcionado por el usuario.  

> [!NOTE]  
>  El paso **Instalar Windows y Configuration Manager** inicia la instalación de Windows. 

 Después de que se ejecute la acción **Aplicar el sistema operativo**, la variable OSDTargetSystemDrive se establece en la letra de unidad de la partición que contiene los archivos de sistema operativo.  

 Este paso de secuencia de tareas solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de secuencia de tareas Aplicar imagen de sistema operativo](task-sequence-action-variables.md#BKMK_ApplyOperatingSystem).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Imágenes** y seleccione **Aplicar imagen de sistema operativo** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Aplicar el sistema operativo de una imagen capturada**  
 Instala una imagen de sistema operativo que se ha capturado previamente. Haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar un paquete** y luego seleccione el paquete de imágenes existente que desee instalar. Si hay varias imágenes asociadas con el **Paquete de imágenes**especificado, use la lista desplegable para indicar la imagen asociada que se va a usa para esta implementación. Para ver información básica sobre cada imagen, haga clic en la imagen.  

 **Aplicar imagen de sistema operativo desde un origen de instalación original**  
 Instala un sistema operativo mediante un origen de instalación original. Haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar un paquete de instalación de sistema operativo**. Después, seleccione el paquete de actualización de sistema operativo existente que quiera usar. Para ver información básica sobre cada origen de imagen existente, haga clic en el origen de imagen. Las propiedades asociadas del origen de imagen se muestran en el panel de resultados en la parte inferior del cuadro de diálogo. Si hay varias ediciones asociadas con el paquete especificado, use la lista desplegable para especificar la **Edición** asociada que se utiliza.  

 **Usar un archivo de respuesta Sysprep o de instalación desatendida para realizar una instalación personalizada**  
 Use esta opción para proporcionar un archivo de respuesta del programa de instalación de Windows (**unattend.xml**, **unattend.txt**o **sysprep.inf**) según el método de instalación y la versión del sistema operativo. El archivo que especifique puede incluir cualquiera de las opciones de configuración estándar compatibles con los archivos de respuesta de Windows. Por ejemplo, puede usarlo para especificar la página principal predeterminada de Internet Explorer. Especifique el paquete que contiene el archivo de respuesta y la ruta de acceso asociada al archivo en el paquete.  

> [!NOTE]  
>  El archivo de respuesta del programa de instalación de Windows que suministre puede contener variables de secuencia de tareas insertadas de tipo %*varname*%, donde *varname* es el nombre de la variable. El paso **Instalar Windows y Configuration Manager** sustituye la cadena %*varname*% por los valores de variable reales. Estas variables de secuencia de tareas insertadas no se pueden usar en campos solo numéricos de un archivo de respuesta unattend.xml.  

 Si no se proporciona un archivo de respuesta del programa de instalación de Windows, esta acción de secuencia de tareas genera automáticamente un archivo de respuesta.  

 **Destino**  
 Configure una de las opciones siguientes:  

-   **Siguiente partición disponible:** use la siguiente partición secuencial que no haya sido destino previo de las acciones **Aplicar el sistema operativo** o **Aplicar imagen de datos** en esta secuencia de tareas. 

-   **Disco y partición específicos**: seleccione el número de **Disco** (empezando por 0) y el número de **Partición** (empezando por 1).  

-   **Letra de unidad lógica específica**: especifique la **Letra de unidad** asignada a la partición por Windows PE. Esta letra de unidad puede ser diferente de la que asigna el sistema operativo recién implementado.  

-   **Letra de unidad lógica almacenada en una variable**: especifique la variable de secuencia de tareas que contiene la letra de unidad asignada a la partición por Windows PE. Normalmente, esta variable se establece en la sección Avanzado del cuadro de diálogo **Propiedades de la partición** de la acción de la secuencia de tareas **Formatear y crear particiones en el disco**.  

### <a name="options"></a>Opciones  
 Además de las opciones predeterminadas, configure las siguientes opciones adicionales en la pestaña **Opciones** de este paso de secuencia de tareas:  

-   **Acceder al contenido directamente desde el punto de distribución**  
     Configure la secuencia de tareas para que tenga acceso a la imagen de sistema operativo directamente desde el punto de distribución. Por ejemplo, use esta opción al implementar sistemas operativos en dispositivos incrustados que tengan una capacidad de almacenamiento limitada. Cuando seleccione esta opción, establezca también la configuración del recurso compartido de paquete en la pestaña **Acceso a datos** de las propiedades del paquete.  

    > [!NOTE]  
    >  Esta configuración invalida la opción de implementación que se configura en la página **Puntos de distribución** del **Asistente para implementar software**. Esta invalidación es solo para la imagen de sistema operativo especificada en este paso, no para el contenido de todas las secuencia de tareas.  



##  <a name="BKMK_ApplyWindowsSettings"></a> Aplicar configuraciones de Windows  
 Use este paso para configurar las opciones de Windows del equipo de destino. La secuencia de tareas almacena estos valores en el archivo de respuesta adecuado. El programa de instalación de Windows usa este archivo de respuesta durante la acción **Instalar Windows y Configuration Manager**.  

 Este paso de secuencia de tareas solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de secuencia de tareas Aplicar configuración de Windows](task-sequence-action-variables.md#BKMK_ApplyWindowsSettings).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Configuración** y seleccione **Aplicar configuraciones de Windows** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Nombre de usuario**  
 Especifique el nombre de usuario registrado que está asociado con el equipo de destino. Este valor puede reemplazarse por el valor que se captura mediante el paso de secuencia de tareas **Capturar configuración de Windows** .  

 **Nombre de la organización**  
 Especifique el nombre de la organización registrado que está asociado con el equipo de destino. Este valor puede reemplazarse por el valor que se captura mediante el paso de secuencia de tareas **Capturar configuración de Windows** .  

 **Clave de producto**  
 Especifique la clave de producto que se usa para la instalación de Windows en el equipo de destino.  

 **Licencia de servidor**  
 Especificar el modo de licencia de servidor. Como modo de licencia, puede seleccionar **Por servidor** o **Por usuario** . Si selecciona **Por servidor**, especifique también el número máximo de conexiones permitidas según el contrato de licencia. Seleccione **No especificar** si el equipo de destino no es un servidor o si no desea especificar el modo de licencia.  

 **Número máximo de conexiones**  
 Especifique el número máximo de conexiones disponibles para este equipo según lo indicado en el contrato de licencia.  

 **Generar la contraseña de administrador local aleatoriamente y deshabilitar la cuenta en todas las plataformas admitidas (recomendado)**  
 Seleccione esta opción para establecer la contraseña de administrador local en una cadena generada de forma aleatoria. Esta opción también deshabilita la cuenta de administrador local en las plataformas que admiten esta característica.  

 **Habilitar la cuenta y especificar la contraseña de administrador local**  
 Seleccione esta opción para habilitar la cuenta de administrador local con la contraseña especificada. Escriba la contraseña en la línea **Contraseña** y confírmela en la línea **Confirmar contraseña** .  

 **Zona horaria**  
 Especifique la zona horaria que se configurará en el equipo de destino. Este valor puede reemplazarse por el valor que se captura mediante el paso de secuencia de tareas **Capturar configuración de Windows** .  



##  <a name="BKMK_AutoApplyDrivers"></a> Aplicar controladores automáticamente  
 Use este paso para hacer coincidir e instalar controladores como parte de la implementación de sistema operativo.  

 El paso de secuencia de tareas **Aplicar controladores automáticamente** realiza las acciones siguientes:  

1.  Examina el hardware y busca los identificadores de Plug and Play de todos los dispositivos presentes en el sistema.  

2.  Envía la lista de dispositivos y sus identificadores de Plug and Play al punto de administración. El punto de administración devuelve, desde el catálogo de controladores, una lista de los controladores compatibles con cada dispositivo de hardware. En la lista se incluyen todos los controladores independientemente del paquete de controladores en el que estén, los controladores etiquetados con la categoría de controlador especificado y los controladores que no se han deshabilitado.  

3.  Para cada dispositivo de hardware, la secuencia de tareas elige el mejor controlador. Este controlador es adecuado para el sistema operativo implementado y se encuentra en un punto de distribución accesible.  

4.  La secuencia de tareas descarga los controladores seleccionados desde un punto de distribución y los preconfigura en el sistema operativo de destino.  

    1.  Para las instalaciones basadas en imagen, la secuencia de tareas coloca los controladores en el almacén de controladores del sistema operativo.  

    2.  Para las instalaciones basadas en el programa de instalación, la secuencia de tareas configura el programa de instalación de Windows con la ubicación de los controladores.  

5.  Durante el paso **Instalar Windows y Configuration Manager** de la secuencia de tareas, el programa de instalación de Windows busca los controladores preconfigurados por esta acción.  

> [!IMPORTANT]
>  Los medios independientes no pueden usar el paso **Aplicar controladores automáticamente**. El programa de instalación de Windows no tiene conexión con el sitio de Configuration Manager en este escenario.

Este paso de secuencia de tareas solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Aplicar controladores automáticamente](task-sequence-action-variables.md#BKMK_AutoApplyDrivers).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Controladores** y seleccione **Aplicar controladores automáticamente** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Instalar solo los controladores compatibles más coincidentes**  
 Especifica que el paso de secuencia de tareas solo instala el controlador que mejor coincide con cada dispositivo de hardware detectado.  

 **Instalar todos los controladores compatibles**  
 La secuencia de tareas instala todos los controladores compatibles para cada dispositivo de hardware detectado. Después, el programa de instalación de Windows elige el mejor controlador. Esta opción consume más ancho de banda de red y espacio de disco. La secuencia de tareas descarga más controladores, pero Windows puede seleccionar un controlador más adecuado.  

 **Considerar controladores de todas las categorías**  
 La secuencia de tareas busca los controladores de dispositivo apropiados en todas las categorías de controladores disponibles.  

 **Limitar la coincidencia de controladores a los controladores de las categorías seleccionadas**  
 La secuencia de tareas busca los controladores de dispositivo apropiados en las categorías de controlador especificadas.  

 **Llevar a cabo la instalación desatendida de controladores no firmados en versiones de Windows en las que se permita**  
 Esta opción permite que Windows instale controladores sin una firma digital.   

  > [!IMPORTANT]  
  >  Esta opción no es aplicable a los sistemas operativos en los que no se puede configurar la directiva de firma de controladores.  



##  <a name="BKMK_CaptureNetworkSettings"></a> Capturar configuración de red  
 Use este paso para capturar la configuración de red de Microsoft en el equipo que ejecuta la secuencia de tareas. La secuencia de tareas guarda esta configuración en las variables de secuencia de tareas. Esta configuración invalida la predeterminada que establezca en el paso **Aplicar configuración de red**.  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Capturar configuración de red](task-sequence-action-variables.md#BKMK_CaptureNetworkSettings).  

En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Configuración** y seleccione **Capturar configuración de red** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Migrar la pertenencia a grupo de trabajo y dominio**  
 Captura la información de pertenencia a dominio y grupo de trabajo del equipo de destino.  

 **Migrar la configuración del adaptador de red**  
 Captura la configuración del adaptador de red del equipo de destino. La información capturada incluye la configuración de red global, el número de adaptadores y la configuración de red asociada a cada adaptador. Esta configuración incluye opciones asociadas con DNS, WINS, IP y filtros de puertos.  



##  <a name="BKMK_CaptureOperatingSystemImage"></a> Capturar imagen de sistema operativo  
 Este paso captura una o más imágenes de un equipo de referencia. La secuencia de tareas crea un archivo de imagen de Windows (.wim) en el recurso compartido de red especificado. Después, use el asistente para **agregar paquete de imagen de sistema operativo** para importar esta imagen a Configuration Manager para las implementaciones de sistema operativo basadas en imágenes.  

 Configuration Manager captura cada volumen (unidad) del equipo de referencia como una imagen independiente en el archivo .wim. Si el equipo al que se hace referencia tiene varios volúmenes, el archivo .wim resultante contiene una imagen independiente para cada volumen. Solo se capturan los volúmenes formateados como NTFS o FAT32. Se omiten los volúmenes con otros formatos y los volúmenes USB.  

 El sistema operativo instalado en el equipo de referencia debe ser una versión de Windows que sea compatible con Configuration Manager. Use la herramienta SysPrep para preparar el sistema operativo del equipo de referencia. El volumen del sistema operativo instalado y el volumen de arranque deben ser el mismo.  

 Especifique una cuenta con permisos de escritura en el recurso compartido de red seleccionado.  

 Este paso de secuencia de tareas solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Capturar sistema operativo](task-sequence-action-variables.md#BKMK_CaptureOperatingSystemImage).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Imágenes** y seleccione **Capturar imagen de sistema operativo** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

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
 Use este paso para usar la herramienta de migración de estado de usuario (USMT) para de capturar el estado de usuario y la configuración del equipo que ejecuta la secuencia de tareas. Este paso de secuencia de tareas se usa junto con el paso **Restaurar estado de usuario** . Con USMT 3.0.1 y versiones posteriores, esta opción siempre cifra el almacén de estado de USMT mediante una clave de cifrado generada y administrada por Configuration Manager.  

 Para obtener más información sobre cómo administrar el estado de usuario al implementar sistemas operativos, consulte [Administrar el estado de usuario](../get-started/manage-user-state.md).  

 Si quiere guardar y restaurar la configuración de estado de usuario desde un punto de migración de estado, use el paso **Capturar estado de usuario** con los pasos **Solicitar almacén de estado** y **Liberar almacén de estado**.  

 El paso de secuencia de tareas **Capturar estado de usuario** proporciona control sobre un subconjunto limitado de las opciones de USMT más usadas. Con la variable de secuencia de tareas OSDMigrateAdditionalCaptureOptions se pueden especificar más opciones de línea de comandos.  

 Este paso de secuencia de tareas solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Capturar estado de usuario](task-sequence-action-variables.md#BKMK_CaptureUserState).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Estado de usuario** y seleccione **Capturar estado de usuario** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Paquete de herramientas de migración de estado de usuario**  
 Especifique el paquete que contiene la herramienta de migración de estado de usuario (USMT). La secuencia de tareas usa esta versión de USMT para capturar el estado de usuario y la configuración. Este paquete no requiere un programa. Especifique un paquete que contenga la versión de 32 o 64 bits de USMT. La arquitectura de USMT depende de la arquitectura del sistema operativo desde el que la secuencia de tareas captura el estado.  

 **Capturar todos los perfiles de usuario mediante opciones estándar**  
 Migre toda la información de perfiles de usuario. Es la opción predeterminada.  

 Si selecciona esta opción, pero no selecciona **Restaurar perfiles de usuario de equipo local** en el paso **Restaurar estado de usuario**, se produce un error en la secuencia de tareas. Configuration Manager no puede migrar las cuentas nuevas sin asignarles contraseñas. 

 Cuando se usa la opción **Instalar un paquete de imágenes existente** del asistente **Nueva secuencia de tareas**, la secuencia de tareas resultante tiene como valor predeterminado **Capturar todos los perfiles de usuario mediante opciones estándar**. Esta secuencia de tareas predeterminada no selecciona la opción **Restaurar perfiles de usuario de equipo local**, es decir, cuentas de usuario que no son de dominio.  

 Seleccione **Restaurar perfiles de usuario de equipo local** y proporcione una contraseña para la cuenta que desea migrar. En una secuencia de tareas creada manualmente, esta configuración se encuentra en el paso “Restaurar estado de usuario”. En una secuencia de tareas creada por el asistente **Nueva secuencia de tareas** , esta configuración se encuentra en el paso **Restaurar configuración y archivos de usuario** .  

 Si no tiene ninguna cuenta de usuario local, esta configuración no se aplica.  

 **Personalizar la captura de perfiles de usuario**  
 Seleccione esta opción para especificar una migración de archivos de perfil personalizada. Haga clic en **Archivos** para seleccionar los archivos de configuración que USMT usará en este paso. Especifique un archivo .xml personalizado que contenga las reglas que definen los archivos de estado de usuario que se van a migrar.  

 **Haga clic aquí para seleccionar archivos de configuración:**  
 Seleccione esta opción para elegir los archivos de configuración en el paquete USMT que desea usar para capturar los perfiles de usuario. Haga clic en el botón **Archivos** botón para iniciar el cuadro de diálogo **Archivos de configuración** . Para especificar un archivo de configuración, escriba el nombre del archivo en la línea **Nombre de archivo** y haga clic en el botón **Agregar** .  

 **Habilitar el registro detallado**  
 Habilite esta opción para generar información más detallada en el archivo de registro. Al capturar el estado, la secuencia de tareas genera de forma predeterminada ScanState.log en la carpeta de registro de secuencia de tareas, \windows\system32\ccm\logs.   

 **Omitir archivos que usan el sistema de cifrado de archivos**  
 Habilite esta opción para omitir la captura de archivos cifrados con el Sistema de cifrado de archivos (EFS). Estos archivos incluyen archivos de perfil de usuario. Según el sistema operativo y la versión de USMT, los archivos cifrados podrían no ser legibles después de la restauración. Para obtener más información, consulte la documentación de USMT.  

 **Copiar mediante el acceso al sistema de archivos**  
 Habilite esta opción para especificar cualquiera de las siguientes opciones:  

-   **Continuar si algunos archivos no se pueden capturar**: habilite esta configuración para continuar con el proceso de migración incluso en el caso de que algunos archivos no se puedan capturar. Si deshabilita esta opción, se produce un error en este paso si no se puede capturar un archivo. Esta opción está habilitada de forma predeterminada.  

-   **Capturar localmente mediante vínculos en vez de mediante la copia de archivos**: habilite esta opción para usar vínculos físicos NTFS para capturar archivos.  

     Para obtener más información sobre cómo migrar datos mediante vínculos físicos, consulte el tema en el que se describe el [almacén de migración de vínculos físicos](http://go.microsoft.com/fwlink/p/?LinkId=240222)  

-   **Capturar en modo fuera de línea (solo Windows PE)**: habilite esta opción para capturar el estado de usuario en Windows PE en lugar de todo el sistema operativo.  
    
**Capturar mediante el Servicio de instantánea de copia de volumen (VSS)**  
 Esta opción permite capturar archivos incluso si otra aplicación los ha bloqueado para su edición.  



##  <a name="BKMK_CaptureWindowsSettings"></a> Capturar configuración de Windows  
 Use este paso para capturar la configuración de Windows en el equipo que ejecuta la secuencia de tareas. La secuencia de tareas guarda esta configuración en las variables de secuencia de tareas. Esta configuración capturada invalida la predeterminada que establezca en el paso **Aplicar configuración de Windows**.  

 Este paso de secuencia de tareas se ejecuta en un sistema operativo estándar o en Windows PE. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Capturar configuración de Windows](task-sequence-action-variables.md#BKMK_CaptureWindowsSettings).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Configuración** y seleccione **Capturar configuración de Windows** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Migrar nombre de equipo**  
 Capture el nombre de equipo NetBIOS del equipo.  

 **Migrar nombres de organización y usuario registrados**  
 Capture los nombres de organización y usuario registrados en el equipo.  

 **Migrar zona horaria**  
 Capture la configuración de zona horaria en el equipo.  



##  <a name="BKMK_CheckReadiness"></a> Comprobar preparación  
 Use este paso para comprobar que el equipo de destino cumpla los requisitos previos de implementación especificados.  

En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **General** y seleccione **Comprobar preparación** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Garantizar mínimo de memoria (MB)**  
 Compruebe que la cantidad de memoria, en megabytes (MB), coincide o supera la cantidad especificada. El paso habilita esta configuración de forma predeterminada.  

 **Garantizar velocidad mínima de procesador (MHz)**  
 Compruebe que la velocidad del procesador, expresada en megahercios (MHz), cumple o supera la cantidad especificada. El paso habilita esta configuración de forma predeterminada.  

 **Garantizar espacio libre en disco mínimo (MB)**  
 Compruebe que la cantidad de espacio libre en disco, en megabytes (MB), cumple o supera la cantidad especificada.  

 **Garantizar que el sistema operativo actual que se va a actualizar es**  
 Compruebe que el sistema operativo instalado en el equipo de destino cumple el requisito especificado. El paso lo establece en **CLIENTE** de forma predeterminada.  

### <a name="options"></a>Opciones
 > [!NOTE]  
 > Si habilita la opción **Continuar después de un error** en la pestaña **Opciones** de este paso, solo registra los resultados de la comprobación de preparación. Si se produce un error en una comprobación, la secuencia de tareas no se detiene.



##  <a name="BKMK_ConnectToNetworkFolder"></a> Conectar a carpeta de red  
 Use este paso para crear una conexión a una carpeta de red compartida.  

 Este paso de secuencia de tareas se ejecuta en un sistema operativo estándar o en Windows PE. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Conectar a carpeta de red](task-sequence-action-variables.md#BKMK_ConnecttoNetworkFolder).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **General** y seleccione **Conectar a carpeta de red** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Ruta de acceso**  
 Haga clic en **Examinar** para especificar la ruta de acceso de la carpeta de red. Use el formato *\\\servidor\recurso compartido*.

 **Unidad**  
 Seleccione la letra de unidad local que se va a asignar a esta conexión. 

 **Cuenta**  
 Haga clic en **Establecer** para especificar la cuenta de usuario con permisos para conectarse a esta carpeta de red.



##  <a name="BKMK_DisableBitLocker"></a> Deshabilitar BitLocker  
 Use este paso para deshabilitar el cifrado de BitLocker en la unidad de sistema operativo actual o en una unidad específica. Con esta acción, los protectores de clave se hacen visibles en texto no cifrado en el disco duro, pero no se descifra el contenido de la unidad. Por lo tanto, esta acción se realiza casi al instante.  

> [!NOTE]  
>  El cifrado de unidad de BitLocker ofrece cifrado de nivel bajo del contenido de un volumen de disco.  

 Si tiene varias unidades cifradas, debe deshabilitar BitLocker en las unidades de datos antes de deshabilitar BitLocker en la unidad del sistema operativo.  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE.  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Discos** y seleccione **Deshabilitar BitLocker** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Unidad actual del sistema operativo**  
 Deshabilita BitLocker en la unidad actual del sistema operativo.  

 **Unidad específica**  
 Deshabilita BitLocker en una unidad específica. Use la lista desplegable para especificar la unidad donde se deshabilita BitLocker.  



##  <a name="BKMK_DownloadPackageContent"></a> Descargar contenido de paquete  
 Use este paso para descargar cualquiera de los tipos de paquete siguientes:  

-   Imágenes de sistema operativo  

-   Paquetes de actualización del sistema operativo  

-   Paquetes de controladores  

-   Paquetes  
    
Este paso funciona bien en una secuencia de tareas para actualizar un sistema operativo en los escenarios siguientes:  

-   Para usar una secuencia de tareas de actualización única que funciona con las plataformas x86 y x64. Incluya dos pasos **Descargar contenido de paquete** en el grupo **Preparación para actualización**. Especifique las condiciones en la pestaña **Opciones** para detectar la arquitectura de cliente y descargar únicamente el paquete de actualización del sistema operativo adecuado. Configure los pasos **Descargar contenido de paquete** para que usen la misma variable. Use la variable para la ruta de acceso de medios en el paso **Actualizar sistema operativo**.  

-   Para descargar dinámicamente un paquete de controladores aplicables, use dos pasos **Descargar contenido de paquete** con condiciones para detectar el tipo de hardware adecuado para cada paquete de controlador. Configure los pasos **Descargar contenido de paquete** para que usen la misma variable. Use la variable para el valor **Contenido preconfigurado** de la sección Controladores del paso **Actualizar sistema operativo**.  

> [!NOTE]    
> Al implementar una secuencia de tareas que contiene el paso Descargar contenido de paquete, no seleccione **Descargar todo el contenido localmente antes de iniciar la secuencia de tareas** o **Acceder al contenido directamente desde un punto de distribución** para **Opciones de implementación** en la página **Puntos de distribución** del Asistente para implementar software.  

Este paso se ejecuta en un sistema operativo estándar o en Windows PE. Pero en WinPE no se admite la opción de guardar el paquete en la caché de cliente de Configuration Manager.

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Software** y seleccione **Descargar contenido de paquete** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 Icono**Seleccione el paquete**  
 Haga clic en el icono para seleccionar el paquete de descarga. Después de seleccionar un paquete, puede hacer clic en el icono de nuevo para elegir otro paquete.  

 **Colocar en la siguiente ubicación**  
 Elija esta opción para guardar el paquete en una de las siguientes ubicaciones:  

 -   **Directorio de trabajo de secuencia de tareas**  

 -   **Caché de cliente de Configuration Manager**: use esta opción para almacenar el contenido en la caché de cliente. El cliente actúa como origen de caché del mismo nivel para otros clientes de caché del mismo nivel. Para obtener más información, consulte [Preparar el almacenamiento en caché del mismo nivel de Windows PE para reducir el tráfico WAN](../get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

 -    **Ruta de acceso personalizada**: con esta opción, el motor de secuencia de tareas descarga primero el paquete en el directorio de trabajo de la secuencia de tareas y lo mueve a la ruta de acceso que se especifique. El motor de secuencia de tareas anexa la ruta de acceso al identificador del paquete. 
   
**Guardar ruta de acceso como variable**  
 Puede guardar la ruta de acceso como una variable que puede usar en otro paso de la secuencia de tareas. Configuration Manager agrega un sufijo numérico al nombre de variable. Por ejemplo, si especifica una variable %*mycontent*% como variable personalizada, será la raíz donde la secuencia de tareas almacena todo el contenido al que se hace referencia. Este contenido puede incluir varios paquetes. Después, al hacer referencia a la variable, agregue un sufijo numérico. Por ejemplo, para el primer paquete, haga referencia a %*mycontent01*%. Cuando se hace referencia a la variable en pasos posteriores, como **Actualizar sistema operativo**, use %*mycontent02*% o %*mycontent03*%, donde el número corresponde al orden en el que el paso **Descargar contenido de paquete** enumera los paquetes.  

**Si se produce un error en la descarga de un paquete, continúe con la descarga de otros paquetes de la lista**  
 Si se produce un error en la secuencia de tareas al descargar un paquete, se inicia la descarga del paquete siguiente en la lista.  



##  <a name="BKMK_EnableBitLocker"></a> Habilitar BitLocker  
Use este paso para habilitar el cifrado de BitLocker en al menos dos particiones en el disco duro. La primera partición activa contiene el código de arranque de Windows. La otra partición contiene el sistema operativo. La partición de arranque debe permanecer sin cifrar.  

Use el paso de secuencia de tareas **Tener en servicio BitLocker** para habilitar BitLocker en una unidad de disco en Windows PE. Para más información, vea la sección [Tener en servicio BitLocker](#BKMK_PreProvisionBitLocker).  

> [!NOTE]  
>  El cifrado de unidad de BitLocker ofrece cifrado de nivel bajo del contenido de un volumen de disco.  

El paso **Habilitar BitLocker** solo se ejecuta en un sistema operativo estándar, no en Windows PE. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Habilitar BitLocker](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

Cuando se especifica **Solo TPM**, **TPM y clave de inicio en USB** o **TPM con PIN**, el Módulo de plataforma segura (TPM) debe estar en el siguiente estado antes de poder ejecutar el paso **Habilitar BitLocker**:  

-   Habilitado  
-   Activado  
-   Propiedad permitida  
   
Este paso completa cualquier inicialización de TPM restante. Los pasos restantes no requieren presencia física ni reinicios. El paso **Habilitar BitLocker** finaliza de forma transparente los demás pasos de inicialización de TPM, si es necesario:  

-   Crear par de claves de aprobación  
-   Crear valor de autorización de propietario y custodia para Active Directory, que debe extenderse para admitir este valor  
-   Tomar posesión  
-   Crear la clave raíz de almacenamiento, o restablecerla si ya existe pero no es compatible  
   
Si quiere que la secuencia de tareas espere a que el paso **Habilitar BitLocker** complete el proceso de cifrado de unidad, seleccione la opción **Esperar**. Si no selecciona la opción **Esperar**, el proceso de cifrado de unidad tiene lugar en segundo plano. La secuencia de tareas continúa inmediatamente al paso siguiente.  

BitLocker puede usarse para cifrar varias unidades en un equipo (tanto de sistema operativo como de datos). Para cifrar una unidad de datos, cifre primero la unidad del sistema operativo y complete el proceso de cifrado. Este requisito se debe a que la unidad del sistema operativo almacena los protectores de clave para las unidades de datos. Si cifra el sistema operativo y las unidades de datos en la misma secuencia de tareas, seleccione la opción **Esperar** en el paso **Habilitar BitLocker** para la unidad de sistema operativo.  

Si el disco duro ya está cifrado pero BitLocker está deshabilitado, el paso **Habilitar BitLocker** vuelve a habilitar los protectores de clave y se completa con rapidez. En este caso no es necesario recifrar la unidad de disco duro.  

Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Habilitar BitLocker](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Discos** y seleccione **Habilitar BitLocker** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Elija la unidad que desea cifrar**  
 Especifica la unidad que se va a cifrar. Para cifrar la unidad actual del sistema operativo, seleccione **Unidad actual del sistema operativo** y, a continuación, configure una de las siguientes opciones para la administración de claves:  

-   **Solo TPM**: seleccione esta opción para usar solo el Módulo de plataforma segura (TPM).  

-   **Clave de inicio solo en USB**: seleccione esta opción para usar una clave de inicio almacenada en una unidad flash USB. Si se selecciona esta opción, BitLocker bloquea el proceso de arranque normal hasta que se conecte al equipo un dispositivo USB que contenga una clave de inicio de BitLocker.  

-   **TPM y clave de inicio en USB**: seleccione esta opción para usar TPM y una clave de inicio almacenada en una unidad flash USB. Si se selecciona esta opción, BitLocker bloquea el proceso de arranque normal hasta que se conecte al equipo un dispositivo USB que contenga una clave de inicio de BitLocker.  

-   **TPM con NIP**: seleccione esta opción para usar TPM y un número de identificación personal (NIP). Si selecciona esta opción, BitLocker bloquea el proceso de arranque normal hasta que el usuario proporcione el PIN.  
   
Para cifrar una determinada unidad de datos que no sean del sistema operativo, seleccione **Unidad específica**y, a continuación, seleccione la unidad en la lista.  

**Elija la ubicación en la que desea crear la clave de recuperación**  
 Para especificar que BitLocker cree la contraseña de recuperación y custodiarla en Active Directory, seleccione **En Active Directory**. Si selecciona esta opción, debe extender Active Directory para el sitio. Después, BitLocker puede guardar la información de recuperación asociada en Active Directory. Seleccione **No crear clave de recuperación** para no crear ninguna contraseña. La creación de una contraseña es el procedimiento recomendado.  

**Esperar a que BitLocker complete el proceso de cifrado de unidad en todas las unidades antes de continuar con la ejecución de la secuencia de tareas**  
 Seleccione esta opción para permitir que se complete el cifrado de unidad de BitLocker antes de ejecutar el siguiente paso de la secuencia de tareas. Si selecciona esta opción, BitLocker cifra el volumen de todo el disco antes de que el usuario pueda iniciar sesión en el equipo.  

El proceso de cifrado puede tardar horas en completarse cuando se cifra una unidad de disco duro grande. Si no se selecciona esta opción, se permite que la secuencia de tareas continúe inmediatamente.  



##  <a name="BKMK_FormatandPartitionDisk"></a> Formatear y crear particiones en el disco  
 Use este paso para dar formato y crear particiones en el disco especificado en el equipo de destino.  

> [!IMPORTANT]  
>  Cada valor especificado para este paso de secuencia de tareas se aplica a un único disco. Para dar formato y crear particiones en otro disco del equipo de destino, agregue otro paso **Formatear y crear particiones de disco** a la secuencia de tareas.  

 Este paso de secuencia de tareas solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de la secuencia de tareas aplicables a esta acción, consulte [Variables de acción de la secuencia de tareas Formatear y crear particiones en el disco](task-sequence-action-variables.md#BKMK_FormatPartitionDisk).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Discos** y seleccione **Formatear y crear particiones de disco** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Número de disco**  
 El número de disco físico del disco al que se va a dar formato. El número se basa en el orden de enumeración de disco de Windows.  

 **Tipo de disco**  
 El tipo de disco al que se da formato. Hay dos opciones para seleccionar en la lista desplegable: 

-   Estándar (MBR): registro de arranque maestro
-   GPT: tabla de particiones GUID  

> [!NOTE]  
>  Si cambia el tipo de disco de **Estándar (MBR)** a **GPT** y el diseño de partición contiene una partición extendida, la secuencia de tareas elimina todas las particiones extendidas y lógicas del diseño. El editor de secuencia de tareas le pide que confirme esta acción antes de cambiar el tipo de disco.  
   
**Volumen**  
 Información específica sobre la partición o volumen que crea la secuencia de tareas, incluidos los atributos siguientes:  

-   Nombre  
-   Espacio en disco restante  
   
Para crear una nueva partición, haga clic en **Nuevo** y se abrirá el cuadro de diálogo **Propiedades de la partición** . Especifique el tipo de partición y el tamaño, y si es una partición de arranque. Para modificar una partición existente, haga clic en la partición que desea modificar y, a continuación, haga clic en el botón de propiedades. Para más información sobre cómo configurar particiones de disco duro, vea uno de los artículos siguientes:  

-   [Configuración de particiones de disco duro basadas en UEFI/GPT](http://go.microsoft.com/fwlink/?LinkID=272104)  
-   [Configuración de particiones de disco duro basadas en BIOS/MBR](http://go.microsoft.com/fwlink/?LinkId=272105)  

Para eliminar una partición, seleccione la partición que desea eliminar y haga clic en **Eliminar**.  



##  <a name="BKMK_InstallApplication"></a> Instalar aplicación  
Este paso instala las aplicaciones especificadas, o un conjunto de aplicaciones definido por una lista dinámica de variables de secuencia de tareas. Cuando se ejecuta este paso, la instalación de aplicaciones se inicia de inmediato sin tener que esperar durante un intervalo de sondeo de directiva.  

Cada aplicación instalada debe cumplir los siguientes criterios:  

-   La aplicación debe ser un tipo de implementación de Windows Installer o un instalador de scripts. No se admiten los tipos de implementación de paquete de aplicación de Windows (archivo .appx).  

-   Debe ejecutarse en la cuenta sistema local y no en la cuenta de usuario.  

-   No debe interactuar con el escritorio. El programa debe ejecutarse en modo silencioso o en modo desatendido.  

-   No debe iniciarse ni reiniciarse por sí misma. La aplicación debe solicitar un reinicio mediante el código estándar de reinicio: un código de salida 3010. Este comportamiento garantiza que el paso de secuencia de tareas controla correctamente el reinicio. Si la aplicación devuelve un código de salida 3010, el motor de secuencia de tareas subyacente lleva a cabo el reinicio. Tras el reinicio, la secuencia de tareas continúa automáticamente.  

Cuando se ejecuta el paso **Instalar aplicación**, la aplicación comprueba la aplicabilidad de las reglas de requisitos y el método de detección en sus tipos de implementación. Según los resultados de esta comprobación, la aplicación instala el tipo de implementación correspondiente. Si un tipo de implementación contiene dependencias, el tipo de implementación dependiente se evalúa y se instala como parte del paso de instalación de la aplicación. Las dependencias de aplicación no son compatibles con medios independientes.  

> [!NOTE]  
>  Para instalar una aplicación que reemplace a otra, los archivos de contenido de la aplicación sustituida deben estar disponibles. En caso contrario, se producirá un error en este paso de secuencia de tareas. Por ejemplo, Microsoft Visio 2010 se instala en un cliente o en una imagen capturada. Cuando el paso **Instalar aplicación** instala Microsoft Visio 2013, los archivos de contenido de Microsoft Visio 2010 (la aplicación sustituida) deben estar disponibles en un punto de distribución. Si Microsoft Visio no está instalado en un cliente o una imagen capturada, la secuencia de tareas instala Microsoft Visio 2013 sin comprobar los archivos de contenido de Microsoft Visio 2010.  

> [!NOTE]
> Si el cliente no puede recuperar la lista de puntos de administración de los servicios de ubicación, use las variables integradas SMSTSMPListRequestTimeoutEnabled y SMSTSMPListRequestTimeout para especificar la cantidad de milisegundos que espera una secuencia de tareas antes de volver a intentar instalar una aplicación o actualización de software. Para obtener más información, consulte [Variables integradas de la secuencia de tareas](task-sequence-built-in-variables.md).

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE.  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Software** y seleccione **Instalar aplicación** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Instalar las aplicaciones siguientes**  
 La secuencia de tareas instala estas aplicaciones en el orden especificado.  

 Configuration Manager filtra las aplicaciones deshabilitadas o las que tengan los valores siguientes:  

-   Solo cuando un usuario haya iniciado sesión  
-   Ejecutar con derechos de usuario  

Estas aplicaciones no aparecen en el cuadro de diálogo **Seleccione la aplicación que desea instalar**.
  
**Instalar aplicaciones según la lista de variables dinámicas**  
La secuencia de tareas instala las aplicaciones mediante este nombre variable de base. El nombre variable de base es para un conjunto de variables de secuencia de tareas definidas para una colección o equipo. Estas variables especifican las aplicaciones que la secuencia de tareas instala para esa colección o equipo. Cada nombre de variable consta de su nombre base común además de un sufijo numérico que empieza en 01. El valor de cada variable debe contener el nombre de la aplicación y nada más.  

Para que la secuencia de tareas instale aplicaciones mediante una lista de variables dinámicas, habilite la siguiente configuración en la pestaña **General** de las **Propiedades** de la aplicación: **Permitir que esta aplicación se instale desde la secuencia de tareas de instalación de aplicación en vez de implementarla manualmente**  

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

Las condiciones siguientes afectan a las aplicaciones instaladas por la secuencia de tareas:  

-   Si el valor de una variable contiene alguna información que no sea el nombre de la aplicación, La secuencia de tareas no instala la aplicación y continúa.  

-   Si la secuencia de tareas no encuentra una variable con el nombre de base especificado y el sufijo "01", no instala ninguna aplicación. 
   
**Continuar instalando otras aplicaciones en la lista si se produce un error de instalación de aplicación**  
 Esta configuración especifica que el paso continúe cuando se produzca un error en la instalación de una aplicación. Si especifica esta opción, la secuencia de tareas continúa con independencia de los errores de instalación. Si no se especifica esta opción y se produce un error en la instalación, el paso finaliza inmediatamente.  

### <a name="options"></a>Opciones
 > [!NOTE] 
 > Si selecciona **Continuar después de un error** en la pestaña **Opciones** de este paso, la secuencia de tareas continúa cuando no se puede instalar una aplicación. Cuando no se habilita esta opción, se produce un error en la secuencia de tareas y no instala las aplicaciones restantes.  
 
Además de las opciones predeterminadas, configure las siguientes opciones adicionales en la pestaña **Opciones** de este paso de secuencia de tareas:  

-   **Volver a intentar este paso si el equipo se reinicia inesperadamente**  
    Si una de las instalaciones de aplicaciones reinicia inesperadamente el equipo, vuelva a intentar este paso. El paso habilita esta configuración de forma predeterminada con dos reintentos. Puede especificar de uno a cinco reintentos.  



##  <a name="BKMK_InstallPackage"></a> Instalar paquete
Use este paso para instalar un paquete de software como parte de la secuencia de tareas. Cuando se ejecuta este paso, la instalación se inicia de inmediato sin tener que esperar durante un intervalo de sondeo de directiva.  

El paquete debe cumplir los criterios siguientes:  

-   Debe ejecutarse en la cuenta de sistema local y no en una cuenta de usuario.  

-   No debe interactuar con el escritorio. El programa debe ejecutarse en modo silencioso o en modo desatendido.  

-   No debe iniciarse ni reiniciarse por sí misma. El software debe solicitar un reinicio mediante el código estándar de reinicio: un código de salida 3010. Este comportamiento garantiza que el paso de secuencia de tareas controla correctamente el reinicio. Si el software devuelve un código de salida 3010, el motor de secuencia de tareas subyacente reinicia el equipo. Tras el reinicio, la secuencia de tareas continúa automáticamente.  

Los programas que usan la opción **Ejecutar otro programa primero** para instalar un programa dependiente no se admiten al implementar un sistema operativo. Si habilita la opción de paquete **Ejecutar otro programa primero** y el programa dependiente ya se ha ejecutado en el equipo de destino, se ejecuta el programa dependiente y la secuencia de tareas continúa. Pero si el programa dependiente todavía no se ha ejecutado en el equipo de destino, se produce un error en el paso de secuencia de tareas.  

> [!NOTE]  
>  El sitio de administración central no tiene las directivas de configuración de cliente necesarias para habilitar el agente de distribución de software durante la secuencia de tareas. Cuando se crea el medio independiente para una secuencia de tareas en el sitio de administración central, y la secuencia de tareas incluye un paso **Instalar paquete** , es posible que aparezca el siguiente error en el archivo CreateTsMedia.log:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>   
>  Para los medios independientes que incluyan un paso **Instalar paquete**, cree los medios independientes en un sitio primario que tenga habilitado el agente de distribución de software. O bien, agregue un paso **Ejecutar línea de comandos** después del paso **Instalar Windows y Configuration Manager** y antes del primer paso **Instalar paquete**. El paso **Ejecutar línea de comandos** ejecuta un comando de WMIC para habilitar el agente de distribución de software antes del primer paso **Instalar paquete**. Use el comando siguiente en el paso **Ejecutar línea de comandos**:  
>   
>  **Línea de comandos**: `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>   
>  Para obtener información sobre cómo crear medios independientes, consulte [Crear medios independientes](../deploy-use/create-stand-alone-media.md).  

Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE.  

En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Software** y seleccione **Instalar paquete** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Instalar un solo paquete de software**  
 Esta configuración especifica un paquete de software de Configuration Manager. El paso espera hasta que finalice la instalación.  

 **Instalar paquetes de software según la lista de variables dinámicas**  
 La secuencia de tareas instala los paquetes mediante este nombre variable de base. El nombre variable de base es para un conjunto de variables de secuencia de tareas definidas para una colección o equipo. Estas variables especifican los paquetes que la secuencia de tareas instala para esa colección o equipo. Cada nombre de variable consta de su nombre base común además de un sufijo numérico que empieza en 001. El valor de cada variable debe contener un identificador de paquete y el nombre del software separado por dos puntos.  

 Para que la secuencia de tareas instale software mediante una lista de variables dinámicas, habilite la opción **Permitir que este programa se instale desde la secuencia de tareas de instalación de paquete sin implementarse** en la pestaña **Avanzadas** de las **Propiedades** del paquete.  

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

 Las condiciones siguientes afectan a los paquetes instalados por la secuencia de tareas:  

-   Si no crea el valor de una variable en el formato correcto o no se especifica un identificador y nombre de paquete válidos, se produce un error en la instalación del software.  

-   Si el identificador de paquete contiene caracteres en minúsculas, se produce un error en la instalación de software.  

-   Si la secuencia de tareas no encuentra una variable con el nombre de base especificado y el sufijo "001", la secuencia de tareas no instala ningún paquete. La secuencia de tareas continúa.  
   
**Continuar instalando otros paquetes en la lista si se produce un error de instalación de un paquete de software**  
 Esta configuración especifica que el paso continúa si se produce un error la instalación de un paquete de software. Si especifica esta opción, la secuencia de tareas continúa con independencia de los errores de instalación. Si no se especifica esta opción y se produce un error en la instalación, el paso finaliza inmediatamente.  



##  <a name="BKMK_InstallSoftwareUpdates"></a> Instalar actualizaciones de software  
Use este paso para instalar actualizaciones de software en el equipo de destino. No se evalúa si hay actualizaciones de software aplicables al equipo de destino hasta que se ejecuta este paso de secuencia de tareas. En ese momento, se evalúa si existen actualizaciones de software para el equipo de destino igual que para cualquier otro cliente de Configuration Manager. Para que este paso instale las actualizaciones de software, primero debe implementarlas en una colección de la que el equipo de destino sea miembro.  
>  [!IMPORTANT]
> Un procedimiento recomendado para obtener un rendimiento óptimo es instalar la versión más reciente del agente de Windows Update. 
>* Para Windows 7, consulte el [artículo de Knowledge Base 3161647](https://support.microsoft.com/kb/3161647).
>* Para Windows 8, consulte el [artículo de Knowledge Base 3163023](https://support.microsoft.com/kb/3163023).

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Instalar actualizaciones de software](task-sequence-action-variables.md#BKMK_InstallSoftwareUpdates).

 > [!NOTE]
 > Si el cliente no puede recuperar la lista de puntos de administración de los servicios de ubicación, use las variables integradas SMSTSMPListRequestTimeoutEnabled y SMSTSMPListRequestTimeout para especificar la cantidad de milisegundos que espera una secuencia de tareas antes de volver a intentar instalar una aplicación o actualización de software. Para obtener más información, consulte [Variables integradas de la secuencia de tareas](task-sequence-built-in-variables.md).

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Software** y seleccione **Instalar actualizaciones de software** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Necesario para la instalación: solo actualizaciones de software obligatorias**  
 Seleccione esta opción para instalar todas las actualizaciones de software obligatorias con fechas límite de instalación definidas por el administrador.  

 **Disponible para la instalación: todas las actualizaciones de software**  
 Seleccione esta opción para instalar todas las actualizaciones de software disponibles. En primer lugar debe implementar estas actualizaciones en una colección de la que el equipo sea miembro. La secuencia de tareas instala todas las actualizaciones de software disponibles en los equipos de destino.  

 **Evaluación de las actualizaciones de software a partir de los resultados del análisis en caché**  
 De forma predeterminada, la secuencia de tareas usa los resultados del análisis en caché de Windows Update Agent. Desactive la casilla para indicar al agente de Windows Update que descargue el catálogo más reciente del punto de actualización de software. Seleccione esta opción cuando se use una secuencia de tareas para [capturar y crear una imagen de sistema operativo](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md). En este escenario es probable que haya un gran número de actualizaciones de software. Muchas de estas actualizaciones tendrán dependencias, por ejemplo, aparece instalar X antes Y según corresponda. Al desactivar esta opción e implementar la secuencia de tareas en un muchos clientes, todos se conectan al punto de actualización de software al mismo tiempo. Este comportamiento produce problemas de rendimiento durante el proceso y la descarga del catálogo. El procedimiento recomendado es la configuración predeterminada para usar los resultados del análisis almacenados en caché. 

La variable de secuencia de tareas SMSTSSoftwareUpdateScanTimeout controla el tiempo de espera del análisis de actualizaciones de software durante este paso. El valor predeterminado es 30 minutos. Para obtener más información, consulte [Variables integradas de la secuencia de tareas](task-sequence-built-in-variables.md).

### <a name="options"></a>Opciones   
 Además de las opciones predeterminadas, configure las siguientes opciones adicionales en la pestaña **Opciones** de este paso de secuencia de tareas:  

-   **Volver a intentar este paso si el equipo se reinicia inesperadamente**  
    Si una de las actualizaciones reinicia inesperadamente el equipo, vuelva a intentar este paso. El paso habilita esta configuración de forma predeterminada con dos reintentos. Puede especificar de uno a cinco reintentos.  

    > [!NOTE]
    > Configure la variable SMSTSWaitForSecondReboot para especificar cuántos segundos se pausa la secuencia de tareas después de reiniciar el equipo en este escenario. Para obtener más información, consulte [Variables integradas de la secuencia de tareas](task-sequence-built-in-variables.md).



##  <a name="BKMK_JoinDomainorWorkgroup"></a> Unirse a dominio o grupo de trabajo  
 Use este paso para agregar el equipo de destino a un grupo de trabajo o dominio.  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de secuencia de tareas de unión a un dominio o un grupo de trabajo](task-sequence-action-variables.md#BKMK_JoinDomainWorkgroup).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **General** y seleccione **Unirse a dominio o grupo de trabajo** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Unirse a un grupo de trabajo**  
 Seleccione esta opción para que el equipo de destino se una al grupo de trabajo especificado. Si el equipo pertenece actualmente a un dominio, la selección de esta opción hace que el equipo se reinicie.  

 **Unirse a un dominio**  
 Seleccione esta opción para que el equipo de destino se una al dominio especificado.  

 Si lo desea, escriba o busque una unidad organizativa (OU) en el dominio especificado para que se una el equipo. Si el equipo pertenece actualmente a otro dominio o grupo de trabajo, esta opción hace que el equipo se reinicie. Si el equipo ya pertenece a otra unidad organizativa, como Active Directory Domain Services no permite cambiar la unidad organizativa a través de este método, el programa de instalación de Windows ignora esta configuración.  

 **Especifique la cuenta que tiene permiso para unirse al dominio**  
 Haga clic en **Establecer** para escribir el nombre de usuario y la contraseña de una cuenta con permisos para unirse al dominio. Escriba la cuenta en el formato: *Dominio\cuenta*  



## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> Preparar el cliente de Configuration Manager para la captura  
Use este paso para quitar o configurar al cliente de Configuration Manager en el equipo de referencia. Esta acción prepara el equipo para la captura como parte del proceso de creación de imágenes.

A partir de la versión 1610 de Configuration Manager, el paso **Preparar el cliente de Configuration Manager** quita por completo el cliente de Configuration Manager, en lugar de quitar solo la información de clave. Cuando la secuencia de tareas implementa la imagen de sistema operativo capturada, instala un cliente nuevo de Configuration Manager cada vez.  

> [!Note]  
>  El motor de secuencia de tareas solo quita el cliente durante la secuencia de tareas **Generar y capturar una imagen de sistema operativo de referencia**. El motor de secuencia de tareas no quita al cliente durante otros métodos de captura, como medios de captura o una secuencia de tareas personalizada.

Antes de la versión 1610 de Configuration Manager, este paso realiza las siguientes tareas:  

-   Quita la sección de propiedades de configuración de cliente del archivo smscfg.ini en el directorio de Windows. Estas propiedades incluyen información específica del cliente, como el GUID de Configuration Manager y otros identificadores de cliente.  

-   Elimina todos los certificados de equipo de Configuration Manager o SMS.  

-   Elimina la memoria caché del cliente de Configuration Manager.  

-   Borra la variable de sitio asignada del cliente de Configuration Manager.  

-   Elimina todas las directivas locales de Configuration Manager.  

-   Quita la clave raíz confiable del cliente de Configuration Manager.  

Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE.  

En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Imágenes** y seleccione **Preparar el cliente de Configuration Manager para la captura** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 Este paso no requiere ninguna configuración en la pestaña **Propiedades**.



##  <a name="BKMK_PrepareWindowsforCapture"></a> Prepare Windows for Capture  
 Use este paso para especificar las opciones de Sysprep al capturar una imagen de sistema operativo en el equipo de referencia. Esta acción de secuencia de tareas ejecuta Sysprep y, después, reinicia el equipo en la imagen de arranque de Windows PE especificada para la secuencia de tareas. Se produce un error en esta acción si el equipo de referencia está unido a un dominio.  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Preparar Windows para la captura](task-sequence-action-variables.md#BKMK_PrepareWindowsCapture).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Imágenes** y seleccione **Preparar Windows para la captura** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Generar automáticamente lista de controladores almacenamiento masivo**  
 Seleccione esta opción para que Sysprep genere automáticamente una lista de controladores de almacenamiento del equipo de referencia. Esta opción habilita la opción de compilar controladores de almacenamiento en el archivo sysprep.inf en el equipo de referencia. Para más información sobre esta configuración, vea la documentación de Sysprep.  

 **No restablecer la marca de activación**  
 Seleccione esta opción para impedir que Sysprep restablezca la marca de activación de producto.  



##  <a name="BKMK_PreProvisionBitLocker"></a> Tener en servicio BitLocker  
 Use este paso para habilitar BitLocker en una unidad cuando se usa Windows PE. Sólo se cifra el espacio de la unidad que se utiliza, por ello los tiempos de cifrado son mucho más rápidos. Las opciones de administración de claves se aplican mediante el paso de secuencia de tareas [Habilitar BitLocker](#BKMK_EnableBitLocker) después de que se instale el sistema operativo. Este paso solo se ejecuta en Windows PE, no en sistemas operativos estándar.  

> [!IMPORTANT]  
>  Para tener en servicio BitLocker se requiere al menos Windows 7. El equipo también debe contener un Módulo de plataforma segura (TPM) compatible y habilitado.  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Discos** y seleccione **Tener en servicio BitLocker** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Aplicar BitLocker a la unidad especificada**  
 Especifique la unidad para la que desea habilitar BitLocker. Solo se cifra el espacio usado en la unidad.  

 **Omitir este paso para equipos que no tengan TPM o cuando TPM no esté habilitado**  
 Seleccione esta opción para omitir el cifrado de unidad en un equipo que no contenga un TPM compatible o habilitado según sea necesario. Por ejemplo, use esta opción al implementar un sistema operativo en una máquina virtual.  



##  <a name="BKMK_ReleaseStateStore"></a> Liberar almacén de estado  
 Use este paso para notificar al punto de migración de estado que la acción de captura o restauración se completó. Use este paso junto con los pasos **Solicitar almacén de estado**, **Capturar estado de usuario** y **Restaurar estado de usuario**. Estos pasos se usan para migrar datos de estado de usuario mediante un punto de migración de estado y la herramienta de migración de estado de usuario (USMT).  

 Para obtener más información sobre cómo administrar el estado de usuario al implementar sistemas operativos, consulte [Administrar el estado de usuario](../get-started/manage-user-state.md).  

 Si usa el paso **Solicitar almacén de estado** para solicitar acceso a un punto de migración de estado para *capturar* el estado de usuario, este paso notifica al punto de migración de estado que el proceso de captura ha finalizado. Después, el punto de migración de estado marca los datos de estado de usuario como disponibles para la restauración. El punto de migración de estado establece los permisos de control de acceso para los datos de estado de usuario de modo que el equipo de la restauración tenga acceso de solo lectura.  

 Si usa el paso **Solicitar almacén de estado** para solicitar acceso a un punto de migración de estado para *restaurar* el estado de usuario, este paso notifica al punto de migración de estado que el proceso de restauración ha finalizado. Después, el punto de migración de estado activa su configuración de retención de datos.  

> [!IMPORTANT]  
>  Un procedimiento recomendado consiste en establecer la opción **Continuar después de un error** para todos los pasos entre **Solicitar almacén de estado** y **Liberar almacén de estado**. Cada paso **Solicitar almacén de estado** debe tener su correspondiente paso **Liberar almacén de estado**.  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Liberar almacén de estado](task-sequence-action-variables.md#BKMK_ReleaseStateStore).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Estado de usuario** y seleccione **Liberar almacén de estado** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 Este paso no requiere ninguna configuración en la pestaña **Propiedades**.



##  <a name="BKMK_RequestStateStore"></a> Solicitar almacén de estado  
 Use este paso para solicitar acceso a un punto de migración de estado al capturar o restaurar el estado.  

 Para obtener más información sobre cómo administrar el estado de usuario al implementar sistemas operativos, consulte [Administrar el estado de usuario](../get-started/manage-user-state.md).  

 Use este paso junto con los pasos **Liberar almacén de estado**, **Capturar estado de usuario** y **Restaurar estado de usuario**. Estos pasos se usan para migrar el estado del equipo mediante un punto de migración de estado y la herramienta de migración de estado de usuario (USMT).  

> [!NOTE]  
>  Al crear un nuevo punto de migración de estado, el almacenamiento de estado de usuario puede tardar hasta una hora en estar disponible. Para acelerar la disponibilidad, ajuste cualquier valor de propiedad del punto de migración de estado para desencadenar una actualización del archivo de control de sitio.  

 Este paso de secuencia de tareas se ejecuta en un sistema operativo estándar y en Windows PE para USMT sin conexión. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Solicitar almacén de estado](task-sequence-action-variables.md#BKMK_RequestState).  

En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Estado de usuario** y seleccione **Solicitar almacén de estado** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Capturar estado del equipo**  
 Busque un punto de migración de estado que cumpla los requisitos mínimos definidos en la configuración de punto de migración de estado. Por ejemplo, **Número máximo de clientes** y **Cantidad mínima de espacio libre en disco**. Esta opción no garantiza que haya espacio suficiente disponible en el momento de la migración de estado. Esta opción solicita acceso al punto de migración de estado con el fin de capturar el estado de usuario y la configuración de un equipo.  

 Si el sitio de Configuration Manager tiene varios puntos de migración de estado activo, este paso busca un punto de migración de estado con espacio en disco disponible. La secuencia de tareas consulta el punto de administración para obtener una lista de puntos de migración de estado y, después, los evalúa hasta encontrar uno que cumpla los requisitos mínimos.  

 **Restaurar estado de otro equipo**  
 Solicite acceso a un punto de migración de estado para restaurar la configuración y el estado de usuario capturados anteriormente en un equipo de destino.  

 Si hay varios puntos de migración de estado, este paso busca el punto de migración de estado que tenga el estado para el equipo de destino.  

 **Número de reintentos**  
 El número de veces que este paso intenta encontrar un punto de migración de estado adecuado antes de que se produzca un error.  

 **Intervalo entre reintentos (en segundos)**  
 Cantidad de tiempo en segundos que el paso de secuencia de tareas espera entre reintentos.  

 **Usar la cuenta de acceso de red si la cuenta de equipo no puede conectarse a un almacén de estado.**  
 Si la secuencia de tareas no puede tener acceso al punto de migración de estado mediante la cuenta de equipo, usa las credenciales de la cuenta de acceso a la red para conectarse. Esta opción es menos segura porque otros equipos podrían usar la cuenta de acceso a la red para obtener acceso al estado almacenado. Es posible que esta opción sea necesaria si el equipo de destino no está unido al dominio.  



##  <a name="BKMK_RestartComputer"></a> Reiniciar equipo  
 Use este paso para reiniciar el equipo que ejecuta la secuencia de tareas. Después del reinicio, el equipo continúa automáticamente con el siguiente paso de la secuencia de tareas.  

 Este paso puede ejecutarse en un sistema operativo estándar o en Windows PE. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Reiniciar equipo](task-sequence-action-variables.md#BKMK_RestartComputer).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **General** y seleccione **Reiniciar equipo** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **La imagen de arranque asignada a esta secuencia de tareas**  
 Seleccione esta opción para que el equipo de destino use la imagen de arranque asignada a la secuencia de tareas. La secuencia de tareas usa la imagen de arranque para ejecutar pasos posteriores en Windows PE.  

 **El sistema operativo predeterminado instalado actualmente**  
 Seleccione esta opción para que el equipo de destino se reinicie en el sistema operativo instalado.  

 **Informar al usuario antes de reiniciar**  
 Seleccione esta opción para mostrar una notificación al usuario antes de que se reinicie el equipo de destino. El paso selecciona esta opción de forma predeterminada.  

 **Mensaje de notificación**  
 Escriba un mensaje de notificación para mostrar al usuario antes de que se reinicie el equipo de destino.  

 **Tiempo de espera de visualización de mensaje**  
 Especifique la cantidad de tiempo en segundos antes de que se reinicie el equipo de destino. El valor predeterminado es 60 segundos.  



##  <a name="BKMK_RestoreUserState"></a> Restaurar estado de usuario  
 Use este paso para iniciar la herramienta de migración de estado de usuario (USMT) para restaurar el estado de usuario y la configuración en un equipo de destino. Use este paso junto con el paso **Capturar estado de usuario**.  

 Para obtener más información sobre cómo administrar el estado de usuario al implementar sistemas operativos, consulte [Administrar el estado de usuario](../get-started/manage-user-state.md).  

 Use este paso con los pasos **Solicitar almacén de estado** y **Liberar almacén de estado** para guardar o restaurar la configuración de estado con un punto de migración de estado. Con USMT 3.0 y versiones superiores, esta opción siempre descifra el almacén de estado de USMT mediante una clave de cifrado generada y administrada por Configuration Manager.  

 El paso **Restaurar estado de usuario** proporciona control sobre un subconjunto limitado de las opciones de USMT más usadas. Especifique más opciones de línea de comandos con la variable de secuencia de tareas OSDMigrateAdditionalRestoreOptions.  

> [!IMPORTANT]  
>  Si usa este paso con una finalidad no relacionada con un escenario de implementación de sistema operativo, agregue el paso [Reiniciar equipo](#BKMK_RestartComputer) inmediatamente después del paso **Restaurar estado de usuario**.  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Restaurar estado de usuario](task-sequence-action-variables.md#BKMK_RestoreUserState).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Estado de usuario** y seleccione **Restaurar estado de usuario** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Paquete de herramientas de migración de estado de usuario**  
 Especifique el paquete que contiene la versión de USMT que se va a usar en este paso. Este paquete no requiere un programa. Cuando se ejecuta el paso, la secuencia de tareas usa la versión de USMT en el paquete especificado. Especifique un paquete que contenga la versión de 32 o 64 bits de USMT. La arquitectura de USMT depende de la arquitectura del sistema operativo en el que la secuencia de tareas restaura el estado. 

 **Restaurar todos los perfiles de usuario capturados con opciones estándar**  
 Restaura los perfiles de usuario capturados con las opciones estándar. Para personalizar las opciones que USMT restaura, seleccione **Personalizar captura de perfil de usuario**.  

 **Personalizar la restauración de perfiles de usuario**  
 Le permite personalizar los archivos que desea restaurar en el equipo de destino. Haga clic en **Archivos** para especificar los archivos de configuración en el paquete de USMT que desea usar para restaurar los perfiles de usuario. Para agregar un archivo de configuración, escriba el nombre del archivo en el cuadro **Nombre de archivo** y, a continuación, haga clic en **Agregar**. En el panel Archivos se enumeran los archivos de configuración que usa USMT. El archivo .xml que especifique define el archivo de usuario que USMT restaura.  

 **Restaurar perfiles de usuario de equipo local**  
 Restaura los perfiles de usuario de equipo local. Estos perfiles no son para los usuarios del dominio. Debe asignar contraseñas nuevas a las cuentas de usuario local restauradas. USMT no puede migrar las contraseñas originales. Escriba la nueva contraseña en el cuadro **Contraseña** y confirme la contraseña en el cuadro **Confirmar contraseña** .  

 **Continuar si algunos archivos no se pueden restaurar**  
 Continúa restaurando la configuración y el estado de usuario incluso si USMT no puede restaurar algunos archivos. El paso habilita esta opción de forma predeterminada. Si deshabilita esta opción y USMT detecta errores durante la restauración de archivos, se produce un error inmediatamente en este paso. USMT no restaura todos los archivos.   

 **Habilitar el registro detallado**  
 Habilite esta opción para generar información más detallada en el archivo de registro. Al restaurar el estado, la secuencia de tareas genera de forma predeterminada Loadstate.log en la carpeta de registro de secuencia de tareas, \windows\system32\ccm\logs.  



##  <a name="BKMK_RunCommandLine"></a> Ejecutar línea de comandos  
 Use este paso para ejecutar la línea de comandos especificada.  

 Este paso puede ejecutarse en un sistema operativo estándar o en Windows PE. Para obtener información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Ejecutar línea de comandos](task-sequence-action-variables.md#BKMK_RunCommand).  

 En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **General** y seleccione **Ejecutar línea de comandos** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Línea de comandos**  
 Especifica la línea de comandos que se ejecuta. Este campo es obligatorio. Es recomendable incluir extensiones de nombre de archivo, por ejemplo, .vbs y .exe. Incluya todos los archivos de configuración, las opciones de línea de comandos o los modificadores que sean necesarios.  

 Si el nombre de archivo no tiene una extensión de nombre de archivo especificada, Configuration Manager prueba con .com, .exe y .bat. Si el nombre de archivo tiene una extensión que no es un archivo ejecutable, Configuration Manager intenta aplicar una asociación local. Por ejemplo, si la línea de comandos es readme.gif, Configuration Manager inicia la aplicación especificada en el equipo de destino para abrir archivos .gif.  

 Ejemplo:  

 `setup.exe /a`  

 `cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
>  Para que se ejecute correctamente, coloque el comando **cmd.exe /c** delante de las acciones de línea de comandos. Ejemplos de estas acciones son los comandos de redirección de salida, canalización y copia.  

 **Deshabilitar el redireccionamiento del sistema de archivos de 64 bits**  
 En los sistemas operativos de 64 bits se usa el redirector del sistema de archivos WOW64 de forma predeterminada para ejecutar líneas de comandos. Este comportamiento es para encontrar correctamente las versiones de 32 bits de archivos ejecutables y bibliotecas del sistema operativo. Seleccione esta opción para deshabilitar el uso del redirector del sistema de archivos WOW64. Windows ejecuta el comando con las versiones nativas de 64 bits de los archivos ejecutables y las bibliotecas del sistema operativo. Esta opción no tiene ningún efecto cuando se ejecuta en un sistema operativo de 32 bits.  

 **Iniciar en**  
 Especifica la carpeta ejecutable para el programa, con un máximo de 127 caracteres. Esta carpeta puede ser una ruta de acceso absoluta en el equipo de destino, o una ruta de acceso relacionada con la carpeta del punto de distribución que contiene el paquete. Este campo es opcional.  

 Ejemplo:  

 **c:\officexp**  

 **i386**  

> [!NOTE]  
>  El botón **Examinar** busca los archivos y carpetas en el equipo local. Todo lo que seleccione también debe existir en el equipo de destino en la misma ubicación y con los mismos nombres de archivo y carpeta.  

 **Paquete**  
 Al especificar en la línea de comandos archivos o programas que aún no están presentes en el equipo de destino, seleccione esta opción para especificar el paquete de Configuration Manager que contiene los archivos adecuados. El paquete no requiere un programa. Esta opción no es necesaria si los archivos especificados existen en el equipo de destino.  

 **Tiempo de espera**  
 Especifica un valor que representa el tiempo que Configuration Manager permite la ejecución de la línea de comandos. Este valor puede estar comprendido entre 1 minuto y 999 minutos. El valor predeterminado es 15 minutos.  

 Esta opción está deshabilitada de forma predeterminada.  

> [!IMPORTANT]  
>  Si escribe un valor que no permita tiempo suficiente para que se complete correctamente el comando especificado, se produce un error en este paso. Podría producirse un error en la secuencia de tareas completa según otra configuración del control. Si se agota el tiempo de espera, Configuration Manager finaliza el proceso de línea de comandos.  

 **Ejecutar esta etapa como la cuenta siguiente**  
 Especifica que la línea de comandos se ejecuta como una cuenta de usuario de Windows diferente de la cuenta de sistema local.  

> [!NOTE]  
>  Para ejecutar comandos o scripts sencillos con otra cuenta después de instalar el sistema operativo, primero debe agregar la cuenta al equipo. Además, debe restaurar el perfil de cuenta de usuario de Windows para ejecutar programas más complejos, como Windows Installer.  

 **Cuenta**  
 Especifica la cuenta de usuario de Windows que se usa en este paso para ejecutar la línea de comandos. La línea de comandos se ejecuta con los permisos de la cuenta especificada. Haga clic en **Establecer** para especificar la cuenta de usuario o dominio local.  

> [!IMPORTANT]  
>  Si este paso especifica una cuenta de usuario y se ejecuta en Windows PE, se produce un error en la acción. No se puede unir Windows PE a un dominio. El archivo smsts.log registra este error.  



##  <a name="BKMK_RunPowerShellScript"></a> Ejecutar script de PowerShell  
 Use este paso para ejecutar el script de PowerShell especificado.  

 Este paso puede ejecutarse en un sistema operativo estándar o en Windows PE. Para ejecutar este paso en Windows PE, PowerShell debe estar habilitado en la imagen de arranque. Puede habilitar Windows PowerShell (WinPE-PowerShell) desde la pestaña **Componentes opcionales** de las propiedades de la imagen de arranque. Para obtener más información sobre cómo modificar una imagen de arranque, consulte [Administrar imágenes de arranque](../get-started/manage-boot-images.md).  

> [!NOTE]  
>  PowerShell no está habilitado de forma predeterminada en los sistemas operativos Windows Embedded.  

En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **General** y seleccione **Ejecutar Script PowerShell** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Paquete**  
 Especifique el paquete de Configuration Manager que contiene el script de PowerShell. Un paquete puede contener varios scripts de PowerShell.  

 **Nombre de script**  
 Especifica el nombre del script de PowerShell que se va a ejecutar. Este campo es obligatorio.  

 **Parámetros**  
 Especifica los parámetros que se pasan al script de Windows PowerShell. Estos parámetros son los mismos que los parámetros de script de Windows PowerShell en la línea de comandos.  

> [!IMPORTANT]  
>  Proporcione parámetros usados por el script, no por la línea de comandos de Windows PowerShell.  
>   
>  El ejemplo siguiente contiene parámetros válidos:  
>   
>  `-MyParameter1 MyValue1 -MyParameter2 MyValue2`  
>   
>  El ejemplo siguiente contiene parámetros no válidos. Los dos primeros elementos son parámetros de línea de comandos de Windows PowerShell (**-NoLogo** y **-ExecutionPolicy Unrestricted**). El script no consume estos parámetros.  
>   
>  `-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`  

 **Directiva de ejecución de PowerShell**  
 Determine qué scripts de Windows PowerShell (si existen) se permiten ejecutar en el equipo. Elija una de las siguientes directivas de ejecución:  

-   **AllSigned**: solo se ejecutan scripts firmados por un editor de confianza  

-   **Undefined**: no se define ninguna directiva de ejecución  

-   **Bypass**: se cargan todos los archivos de configuración y se ejecutan todos los scripts. Si descarga un script no firmado desde Internet, Windows PowerShell no solicita permiso antes de ejecutarlo.  

> [!IMPORTANT]  
>  PowerShell 1.0 no admite las directivas de ejecución Sin definir ni Desviar.  



##  <a name="child-task-sequence"></a> Ejecutar secuencia de tareas

A partir de Configuration Manager versión 1710, puede agregar un nuevo paso que ejecute otra secuencia de tareas. Este paso crea una relación primario-secundario entre las secuencias de tareas. Con las secuencias de tareas secundarias, puede crear secuencias de tareas más modulares y reutilizables.

Tenga en cuenta las siguientes instrucciones al agregar una secuencia de tareas secundaria a una secuencia de tareas:
 - Las secuencias de tareas primaria y secundaria se combinan eficazmente en una única directiva que ejecuta el cliente.
 - El entorno es global. Si la secuencia de tareas primaria establece una variable y, después, la secuencia de tareas secundaria cambia esa variable, conserva el valor más reciente. Si la secuencia de tareas secundaria crea una variable, está disponible para el resto de la secuencia de tareas primaria.
 - Los mensajes de estado se envían de manera normal para una operación de secuencia de tareas única.
 - Las secuencias de tareas escriben entradas en el archivo smsts.log, con nuevas entradas de registro que dejan claro cuando se inicia una secuencia de tareas secundaria.

En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **General** y seleccione **Ejecutar secuencia de tareas** para agregar este paso. 

### <a name="properties"></a>Propiedades
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

**Seleccionar la secuencia de tareas que se va a ejecutar**  
 Haga clic en **Examinar** para seleccionar la secuencia de tareas secundaria. En el cuadro de diálogo **Seleccionar una secuencia de tareas** no se muestra la secuencia de tarea primaria.



##  <a name="BKMK_SetDynamicVariables"></a> Establecer variables dinámicas  
 Use este paso para realizar las acciones siguientes:  

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

En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **General** y seleccione **Establecer variables dinámicas** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

**Variables y reglas dinámicas**  
 Para establecer una variable dinámica para su uso en la secuencia de tareas, agregue una regla. Después, establezca un valor para cada variable especificada en la regla. Además, puede agregar una o más variables sin agregar una regla. Cuando se agrega una regla, elija entre las siguientes categorías:  

 -   **Equipo**: evalúe los valores para la etiqueta de inventario de hardware, UUID, número de serie o dirección MAC. Establezca varios valores según sea necesario. Si alguno de los valores es true, la regla se evalúa como true. Por ejemplo, la regla siguiente se evalúa como true si el número de serie del dispositivo es 5892087 y la dirección MAC es 22-A4-5A-13-78-26.  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

-   **Ubicación**: evalúe los valores de la puerta de enlace de red predeterminada  

-   **Marca y modelo**: evalúe los valores de la marca y modelo de un equipo. La marca y el modelo deben evaluarse como true para que la regla se evalúe como true.   

    <!-- for future edits: an escape code must be used for the bolded asterisk character, but may be removed somewhere along the way. Instead of five asterisk, should be bold tags with &#42; in-between -->

    A partir de la versión 1610 de Configuration Manager, puede especificar un asterisco (**&#42;**) y un signo de interrogación (**?**) como caracteres comodín, donde **&#42;** coincide con varios caracteres y **?** coincide con un carácter simple. Por ejemplo, la cadena "DELL*900?" coincidirá con DELL-ABC-9001 y con DELL9009. 

    Especifique un asterisco (**&#42;**) y un signo de interrogación (**?**) como caracteres comodín, donde **&#42;** coincide con varios caracteres y **?** coincide con un carácter simple. Por ejemplo, la cadena "DELL*900?" coincide con DELL-ABC-9001 y DELL9009.

-   **Variable de secuencia de tareas**: agregue una variable de secuencia de tareas, la condición y el valor que se van a evaluar. La regla se evalúa como true cuando el valor establecido para la variable cumple la condición especificada.  

    Especifique una o más variables que se van a establecer para una regla que se evalúa como true, o bien establezca variables sin usar una regla. Seleccione una variable existente o cree una variable personalizada.  

     -   **Variables de secuencia de tareas existentes**: seleccione una o más variables en una lista de variables de secuencia de tareas existentes. Las variables de matriz no están disponibles para seleccionar.  

     -   **Variables de secuencia de tareas personalizadas**: defina una variable de secuencia de tareas personalizada. También puede especificar una variable de secuencia de tareas existente. Este valor es útil para especificar una matriz de variables existente, como OSDAdapter, ya que las matrices de variables no están en la lista de variables de secuencia de tareas existentes.  

Después de seleccionar las variables de una regla, debe proporcionar un valor para cada variable. La variable se establece en el valor especificado cuando la regla se evalúa como true. Para cada variable, puede seleccionar **Valor secreto** para ocultar el valor de la variable. De forma predeterminada, algunas de las variables existentes ocultan valores, como la variable de secuencia de tareas de OSDCaptureAccountPassword.  

> [!IMPORTANT]  
>  Configuration Manager quita los valores de variable marcados como **Valor secreto** al importar una secuencia de tareas con el paso **Establecer variables dinámicas**. Vuelva a escribir el valor de la variable dinámica después de importar la secuencia de tareas.  



##  <a name="BKMK_SetTaskSequenceVariable"></a> Establecer variable de secuencia de tareas  
Use este paso para establecer el valor de una variable que se usa con la secuencia de tareas.  

Este paso puede ejecutarse en un sistema operativo estándar o en Windows PE. Las variables de secuencia de tareas son leídas por acciones de secuencia de tareas y especifican el comportamiento de esas acciones. Para más información sobre las variables de acción de secuencias de tareas específicas, vea [Variables de acción de secuencias de tareas](task-sequence-action-variables.md). Para más información sobre variables integradas de secuencia de tareas, vea [Variables integradas de secuencia de tareas](/sccm/osd/understand/task-sequence-built-in-variables).

En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **General** y seleccione **Configurar variable de secuencia de tareas** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Variable de secuencia de tareas**  
 Especifique el nombre de una variable de acción o de secuencia de tareas integrada, o bien especifique su propio nombre de variable definido por el usuario.  

 **Valor**  
 La secuencia de tareas establece la variable en este valor. Establezca esta variable de secuencia de tareas en el valor de otra variable de secuencia de tareas con la sintaxis %varname%.  



##  <a name="BKMK_SetupWindowsandConfigMgr"></a> Instalar Windows y Configuration Manager  
 Use este paso para realizar la transición desde Windows PE al nuevo sistema operativo. Este paso de secuencia de tareas es una parte necesaria de cualquier implementación de sistema operativo. Se instala el cliente de Configuration Manager en el nuevo sistema operativo y se prepara para que la secuencia de tareas continúe con la ejecución en el sistema operativo.  

 Este paso solo se ejecuta en Windows PE, no en sistemas operativos estándar. Para obtener más información sobre las variables de secuencia de tareas para esta acción, consulte [Variables de acción de la secuencia de tareas Instalar Windows y Configuration Manager](task-sequence-action-variables.md#BKMK_SetupWindows).  

 Este paso reemplaza las variables de directorio sysprep.inf o unattend.xml, como %WINDIR% y %ProgramFiles%, por el directorio de instalación de Windows PE, X:\Windows. La secuencia de tareas ignora las variables especificadas mediante estas variables de entorno.  

 Use este paso de secuencia de tareas para realizar las siguientes acciones:  

1.  Pasos preliminares: Windows°PE  

    1.  Sustituya las variables de secuencia de tareas en el archivo unattend.xml.  

    2.  Descargue el paquete que contiene el cliente de Configuration Manager. Agregue el paquete a la imagen implementada.  

2.  Configurar Windows  

    1.  Instalación basada en imagen  

        1.  Deshabilite el cliente de Configuration Manager en la imagen, si existe. En otras palabras, deshabilite el inicio automático para el servicio de cliente de Configuration Manager.  

        2.  Actualice el Registro en la imagen implementada para iniciar el sistema operativo implementado con la misma letra de unidad que el equipo de referencia.  

        3.  Reinicie en el sistema operativo implementado.  

        4.  La instalación mínima de Windows se ejecuta con los archivos de respuesta sysprep.inf o unattend.xml especificados anteriormente que tienen suprimida toda la interacción del usuario final. Si se usa el paso **Aplicar configuración de red** para unirse a un dominio, después esa información se encuentra en el archivo de respuesta. La instalación mínima de Windows une el equipo al dominio.  

    2.  Instalación basada en Setup.exe.  Ejecuta Setup.exe que sigue el proceso de instalación típico de Windows:  

        1.  Copie el paquete de actualización del sistema operativo, especificado en el paso **Aplicar el sistema operativo**, en la unidad de disco duro.  

        2.  Reinicie en el sistema operativo recién implementado.  

        3.  La instalación mínima de Windows se ejecuta con los archivos de respuesta sysprep.inf o unattend.xml especificados anteriormente que tienen suprimida toda la configuración de la interfaz de usuario. Si se usa el paso **Aplicar configuración de red** para unirse a un dominio, después esa información se encuentra en el archivo de respuesta. La instalación mínima de Windows une el equipo al dominio.  

3.  Configurar el cliente de Configuration Manager  

    1.  Una vez finalizada la instalación mínima de Windows, la secuencia de tareas se reanuda mediante setupcomplete.cmd.  

    2.  Habilite o deshabilite la cuenta de administrador local, según la opción seleccionada en el paso **Aplicar configuraciones de Windows**.  

    3.  Instale el cliente de Configuration Manager mediante el paquete descargado anteriormente y las propiedades de instalación especificadas en este paso. El cliente se instala en "modo de aprovisionamiento" para impedir que procese nuevas solicitudes de directiva hasta que se complete la secuencia de tareas.  

    4.  Espere a que el cliente esté totalmente operativo.  

4.  La secuencia de tareas continúa ejecutando el paso siguiente.  

<!-- Engineering confirmed that the task sequence does nothing with respect to group policy processing.
> [!NOTE]  
>  The **Setup Windows and ConfigMgr** task sequence action is responsible for running Group Policy on the newly installed computer. The Group Policy is applied after the task sequence is finished.  
-->

En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Imágenes** y seleccione **Instalar Windows y Configuration Manager** para agregar este paso. 

### <a name="properties"></a>Propiedades  
 En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

 **Paquete de cliente**  
 Haga clic en **Examinar** y después seleccione el paquete de instalación de cliente de Configuration Manager para usar con este paso.  

 **Usar el paquete de cliente de preproducción cuando esté disponible**  
 Si hay un paquete de cliente de preproducción disponible y el equipo forma parte de la colección de uso piloto, la secuencia de tareas lo usa en lugar del paquete de cliente de producción. El cliente de preproducción es una versión más reciente para pruebas en el entorno de producción. Haga clic en **Examinar** y después seleccione el paquete de instalación de cliente de preproducción para usar con este paso.  

 **Propiedades de instalación**  
 La acción de secuencia de tareas especifica automáticamente la asignación de sitios y la configuración predeterminada. Puede usar este campo para especificar propiedades de instalación adicionales que se utilizarán al instalar el cliente. Si desea especificar varias propiedades de instalación, sepárelas con un espacio.  

 Puede especificar opciones de línea de comandos para que se usen durante la instalación de cliente. Por ejemplo, puede escribir **/skipprereq: silverlight.exe** para informar a CCMSetup.exe que no instale el requisito previo de Microsoft Silverlight. Para obtener más información sobre las opciones de líneas de comandos disponibles para CCMSetup.exe, consulte [Acerca de las propiedades de instalación de clientes](../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="options"></a>Opciones
> [!NOTE]
> No habilite **Continuar después de un error** en la pestaña **Opciones**. Si se produce un error durante este paso, se produce un error en la secuencia de tareas con independencia de que se habilite o no esta configuración.



##  <a name="BKMK_UpgradeOS"></a> Actualizar el sistema operativo  
 > [!TIP]  
 > A partir de la versión 1709 de Windows 10, los medios incluyen varias ediciones. Cuando se configura una secuencia de tareas para usar un paquete de actualización del sistema operativo o una imagen del sistema operativo, no olvide seleccionar una [edición admitida](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

 Use este paso para actualizar una versión anterior de Windows a una versión más reciente de Windows 10.  

 Este paso solo se ejecuta en un sistema operativo estándar, no en Windows PE.  

En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Imágenes** y seleccione **Actualizar sistema operativo** para agregar este paso. 

### <a name="properties"></a>Propiedades  
En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

**Paquete de actualización**  
 Seleccione esta opción para especificar el paquete de actualización del sistema operativo de Windows 10 que se usará para la actualización.  

**Ruta de origen**  
 Especifica una ruta de acceso local o de red para los medios de Windows 10 que usa el programa de instalación de Windows. Esta opción corresponde a la opción de línea de comandos de instalación de Windows **/InstallFrom**. También puede especificar una variable, como %mycontentpath% o %DPC01%. Cuando se use una variable para la ruta de origen, debe especificarse previamente en la secuencia de tareas. Por ejemplo, si usa el paso [Descargar contenido de paquete](#BKMK_DownloadPackageContent) en la secuencia de tareas, puede especificar una variable para la ubicación del paquete de actualización del sistema operativo. A continuación, puede usar esa variable para la ruta de origen para este paso.  

**Edición**  
 Especifique la edición en los medios del sistema operativo que se usará para la actualización.  

**Clave de producto**  
 Especifique la clave de producto que se debe aplicar al proceso de actualización.  

**Proporcionar el contenido del controlador siguiente al programa de configuración de Windows durante la actualización**  
 Agregue controladores al equipo de destino durante el proceso de actualización. Esta opción corresponde a la opción de línea de comandos de instalación de Windows **/InstallDriver**. Los controladores deben ser compatibles con Windows 10. especifique una de las siguientes opciones:  

-   **Paquete de controladores**: haga clic en **Examinar** y seleccione un paquete de controladores existente en la lista.  

-   **Contenido almacenado provisionalmente**: seleccione esta opción para especificar la ubicación del paquete de controladores. Puede especificar una carpeta local, la ruta de red o una variable de secuencia de tareas. Cuando se use una variable para la ruta de origen, debe especificarse previamente en la secuencia de tareas. Por ejemplo, mediante el paso [Descargar contenido de paquete](task-sequence-steps.md#BKMK_DownloadPackageContent).  

**Tiempo de espera (minutos)**  
 Especifica el número de minutos antes de que se produzca un error de Configuration Manager en este paso. Esta opción es útil si el programa de instalación de Windows detiene el procesamiento pero no finaliza.  

**Realizar examen de compatibilidad del programa de instalación de Windows sin iniciar la actualización**  
 Realice el examen de compatibilidad del programa de instalación de Windows sin iniciar el proceso de actualización. Esta opción corresponde a la opción de línea de comandos de instalación de Windows **/Compat ScanOnly**. Debe implementar el origen de instalación completo cuando use esta opción. La instalación devuelve un código de salida como resultado de la exploración. En la tabla siguiente se proporcionan algunos de los códigos de salida más comunes.  

|Código de salida|Detalles|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|No hay problemas de compatibilidad ("correcto").|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Problemas de compatibilidad accionables.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|La opción de migración seleccionada no está disponible. Por ejemplo, una actualización de Enterprise a Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|No elegible para Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|No hay suficiente espacio en disco libre.|  

Para más información sobre este parámetro, vea [Opciones de la línea de comandos del programa de instalación de Windows](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx).  

**Omitir cualquier mensaje de compatibilidad descartable**  
 Especifica que el programa de instalación completa la instalación, omitiendo los mensajes de compatibilidad descartables. Esta opción corresponde a la opción de línea de comandos de instalación de Windows **/Compat IgnoreWarning**.  

**Actualizar programa de instalación de Windows dinámicamente con Windows Update**  
 Habilite el programa de instalación para realizar operaciones de actualización dinámica, como buscar, descargar e instalar actualizaciones. Esta opción corresponde a la opción de línea de comandos de instalación de Windows **/DynamicUpdate**. Esta opción no es compatible con las actualizaciones de software de Configuration Manager. Habilite esta opción cuando administre actualizaciones con Windows Server Update Services (WSUS) independiente o Windows Update para empresas.  

**Invalidar directiva y usar Microsoft Update predeterminado**: invalide temporalmente la directiva local en tiempo real para ejecutar operaciones de actualización dinámica y que el equipo obtenga actualizaciones de Windows Update.
