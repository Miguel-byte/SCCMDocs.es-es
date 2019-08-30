---
title: Pasos de la secuencia de tareas
titleSuffix: Configuration Manager
description: Obtenga información sobre los pasos que puede agregar a una secuencia de tareas de Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4ee01c85cf978b595aa9d6a7948503b34927c31
ms.sourcegitcommit: 2d38de4846ea47a03cc884cbd3df27db48f64a6a
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2019
ms.locfileid: "70110242"
---
# <a name="task-sequence-steps"></a>Pasos de la secuencia de tareas

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los siguientes pasos de secuencia de tareas se pueden agregar a una secuencia de tareas de Configuration Manager. Para obtener información sobre cómo editar una secuencia de tareas, consulte [Editar una secuencia de tareas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ModifyTaskSequence).  

Las opciones siguientes son comunes a todos los pasos de secuencia de tareas:

#### <a name="properties-tab"></a>Ficha Propiedades

- **Nombre**: el editor de secuencia de tareas requiere que se especifique un nombre corto para describir este paso. Cuando se agrega un paso nuevo, el editor de secuencia de tareas establece el nombre en Tipo de forma predeterminada. La longitud de **Nombre** no puede superar los 50 caracteres.  

- **Descripción**: si quiere, especifique información más detallada sobre este paso. La longitud de **Descripción** no puede superar los 256 caracteres.  

En el resto de este artículo se describen los demás valores de la pestaña **Propiedades** para cada paso de secuencia de tareas.

#### <a name="options-tab"></a>Pestaña Opciones  

- **Deshabilitar este paso**: la secuencia de tareas omite este paso cuando se ejecuta en un equipo. El icono para este paso está atenuado en el editor de secuencia de tareas.  

- **Continuar después de un error**: la secuencia de tareas continúa aunque se produzca un error durante la ejecución del paso. Para obtener información, consulte [Planeación de consideraciones para la automatización de tareas](/sccm/osd/plan-design/planning-considerations-for-automating-tasks#BKMK_TSGroups).  

- **Agregar condición**: la secuencia de tareas evalúa estas instrucciones condicionales para determinar si se ejecuta el paso. Para obtener un ejemplo del uso de una variable de secuencia de tareas como una condición, vea [How to use task sequence variables](/sccm/osd/understand/using-task-sequence-variables#bkmk_access-condition) (Uso de variables de secuencia de tareas).  

En las secciones siguientes para pasos de secuencia de tareas específicos se describen otros valores posibles en la pestaña **Opciones**.



## <a name="BKMK_ApplyDataImage"></a> Aplicar imágenes de datos

Use este paso para copiar la imagen de datos en la partición de destino especificada.  

Este paso solo se ejecuta en Windows PE, No se ejecuta en el sistema operativo completo.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDDataImageIndex](/sccm/osd/understand/task-sequence-variables#OSDDataImageIndex)  
- [OSDWipeDestinationPartition](/sccm/osd/understand/task-sequence-variables#OSDWipeDestinationPartition)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Imágenes** y **Aplicar imagen de datos**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="image-package"></a>Paquete de imágenes

Seleccione **Examinar** para especificar el **Paquete de imágenes** que se usa en esta secuencia de tareas. Seleccione el paquete que desea instalar en el cuadro de diálogo **Seleccionar un paquete** . En la parte inferior del cuadro de diálogo se muestra la información de propiedades asociada para cada paquete de imagen existente. En la lista desplegable, seleccione la **Imagen** que desea instalar desde el **Paquete de imágenes**seleccionado.  

> [!NOTE]  
> Esta acción de secuencia de tareas trata la imagen como un archivo de datos. Esta acción no realiza ninguna configuración para arrancar la imagen como un sistema operativo.  

#### <a name="destination"></a>Destino

Configure una de las opciones siguientes:

- **Siguiente partición disponible:** use la siguiente partición secuencial que no haya sido destino previo de los pasos **Aplicar el sistema operativo** o **Aplicar imagen de datos** en esta secuencia de tareas.  

- **Disco y partición específicos**: seleccione el número de **Disco** (empezando por 0) y el número de **Partición** (empezando por 1).  

- **Letra de unidad lógica específica**: especifique la **Letra de unidad** que Windows PE asigna a la partición. Esta letra de unidad puede ser diferente de la que asigna el sistema operativo recién implementado.  

- **Letra de unidad lógica almacenada en una variable**: especifique la variable de secuencia de tareas que contiene la letra de unidad asignada a la partición por Windows PE. Normalmente, esta variable se establece en la sección Avanzado del cuadro de diálogo **Propiedades de la partición** del paso de la secuencia de tareas **Formatear y crear particiones en el disco**.  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>Eliminar todo el contenido en la partición antes de aplicar la imagen  

Especifica que la secuencia de tareas elimina todos los archivos en la partición de destino antes de instalar la imagen. Si no se elimina el contenido de la partición, esta acción puede usarse para aplicar contenido adicional a una partición de destino previa.  



## <a name="BKMK_ApplyDriverPackage"></a> Aplicar paquete de controladores  

Use este paso para descargar todos los controladores del paquete de controladores e instalarlos en el sistema operativo Windows.

El paso de secuencia de tareas **Aplicar paquete de controladores** hace que todos los controladores de dispositivo incluidos en un paquete de controladores estén disponibles para su uso con Windows. Agregue este paso entre los pasos **Aplicar el sistema operativo** e **Instalar Windows y Configuration Manager** para que los controladores del paquete estén disponibles para Windows. El paso de secuencia de tareas **Aplicar paquete de controladores** también es útil en escenarios de implementación de medios independientes.  

Coloque los controladores de dispositivo en un paquete de controladores y distribúyalos a los puntos de distribución adecuados. Por ejemplo, coloque todos los controladores de un fabricante en un paquete de controladores. Después, distribuya el paquete a puntos de distribución a los que los equipos asociados puedan tener acceso.

El paso **Aplicar paquete de controladores** resulta útil para medios independientes. Este paso también es útil para instalar un conjunto específico de controladores. Estos tipos de controladores incluyen los dispositivos que no se detectarán en un análisis de Plug and Play de Windows, como las impresoras de red.  

Este paso de secuencia de tareas solo se ejecuta en Windows PE, No se ejecuta en el sistema operativo completo.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDApplyDriverBootCriticalContentUniqueID](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalContentUniqueID)  
- [OSDApplyDriverBootCriticalHardwareComponent](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalHardwareComponent)  
- [OSDApplyDriverBootCriticalID](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalID)  
- [OSDApplyDriverBootCriticalINFFile](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalINFFile)  
- [OSDInstallDriversAdditionalOptions](/sccm/osd/understand/task-sequence-variables#OSDInstallDriversAdditionalOptions)<!--516679/2840016--> (A partir de la versión 1806).  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Controladores** y **Aplicar paquete de controladores**.

### <a name="properties"></a>Propiedades

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="driver-package"></a>Paquete de controladores

Especifique el paquete de controladores que contiene los controladores de dispositivo necesarios. Seleccione **Examinar** para iniciar el cuadro de diálogo **Seleccionar un paquete**. Seleccione el paquete de controladores existente que desee aplicar. La parte inferior del cuadro de diálogo muestras las propiedades del paquete asociado.  

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>Seleccionar en el paquete el controlador de almacenamiento que debe instalarse antes de la configuración en sistemas operativos anteriores a Windows Vista

Especifique los controladores de almacenamiento masivo necesarios para instalar un sistema operativo clásico.  

#### <a name="driver"></a>Controlador

Seleccione el archivo de controlador de almacenamiento masivo para instalar antes de la instalación de un sistema operativo clásico. La lista desplegable se rellena con el paquete especificado.  

#### <a name="model"></a>Modelo

Especifique el dispositivo crítico para el arranque que se necesita en implementaciones de sistemas operativos anteriores a Windows Vista.  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>Llevar a cabo la instalación desatendida de controladores no firmados en versiones de Windows en las que se permita

Esta opción permite que Windows instale controladores sin una firma digital.  



## <a name="BKMK_ApplyNetworkSettings"></a> Aplicar configuración de red  

Use este paso para especificar la información de configuración de red o grupo de trabajo del equipo de destino. La secuencia de tareas almacena estos valores en el archivo de respuesta adecuado. El programa de instalación de Windows usa este archivo de respuesta durante la acción **Instalar Windows y Configuration Manager**.  

Este paso de secuencia de tareas solo se ejecuta en Windows PE, No se ejecuta en el sistema operativo completo.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDAdapter](/sccm/osd/understand/task-sequence-variables#OSDAdapter)  
- [OSDAdapterCount](/sccm/osd/understand/task-sequence-variables#OSDAdapterCount)  
- [OSDDNSDomain](/sccm/osd/understand/task-sequence-variables#OSDDNSDomain)  
- [OSDDNSSuffixSearchOrder](/sccm/osd/understand/task-sequence-variables#OSDDNSSuffixSearchOrder)  
- [OSDDomainName](/sccm/osd/understand/task-sequence-variables#OSDDomainName)  
- [OSDDomainOUName](/sccm/osd/understand/task-sequence-variables#OSDDomainOUName)  
- [OSDEnableTCPIPFiltering](/sccm/osd/understand/task-sequence-variables#OSDEnableTCPIPFiltering)  
- [OSDJoinAccount](/sccm/osd/understand/task-sequence-variables#OSDJoinAccount)  
- [OSDJoinPassword](/sccm/osd/understand/task-sequence-variables#OSDJoinPassword)  
- [OSDWorkgroupName](/sccm/osd/understand/task-sequence-variables#OSDWorkgroupName)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Configuración** y **Aplicar configuración de red**.

### <a name="properties"></a>Propiedades

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="join-a-workgroup"></a>Unirse a un grupo de trabajo

Seleccione esta opción para que el equipo de destino se una al grupo de trabajo especificado. Escriba el nombre del grupo de trabajo en la línea **Grupo de trabajo** . El valor que captura la secuencia de tareas **Capturar configuración de red** puede reemplazar este valor.

#### <a name="join-a-domain"></a>Unirse a un dominio

Seleccione esta opción para que el equipo de destino se una al dominio especificado. Especifique o busque el dominio, como `fabricam.com`. Especifique o busque una ruta de acceso de protocolo ligero de acceso a directorios (LDAP) de una unidad organizativa. Por ejemplo: `LDAP//OU=computers, DC=Fabricam.com, C=com`.  

#### <a name="account"></a>Cuenta

Seleccione **Establecer** para especificar una cuenta con los permisos necesarios para unir el equipo al dominio. En el cuadro de diálogo **Cuenta de usuario de Windows** puede especificar el nombre de usuario con el formato siguiente: `Domain\User`. Para obtener más información, consulte [Cuenta de unión de dominio](/sccm/core/plan-design/hierarchy/accounts#task-sequence-domain-join-account).

#### <a name="adapter-settings"></a>Configuración del adaptador

Especifique la configuración de red para cada adaptador de red del equipo. Seleccione **Nuevo** para abrir el cuadro de diálogo **Configuración de red** y después especifique la configuración de red.

- Si también usa el paso **Capturar configuración de red**, la secuencia de tareas aplica al adaptador de red los valores capturados anteriormente.
- Si la secuencia de tareas no ha capturado previamente la configuración de red, aplica la configuración especificada en el paso.
- La secuencia de tareas aplica esta configuración a los adaptadores de red en el orden de enumeración de los dispositivos de Windows.  
- La secuencia de tareas no aplica de inmediato la configuración especificada en este paso en el equipo.



## <a name="BKMK_ApplyOperatingSystemImage"></a> Aplicar imagen de sistema operativo  

> [!TIP]  
> A partir de la versión 1709 de Windows 10, los medios incluyen varias ediciones. Cuando se configura una secuencia de tareas para usar un paquete de actualización del sistema operativo o una imagen del sistema operativo, no olvide seleccionar una [edición admitida](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).  

Use este paso para instalar un sistema operativo en el equipo de destino.

> [!NOTE]  
> El paso **Instalar Windows y Configuration Manager** inicia la instalación de Windows.

Después de que se ejecute la acción **Aplicar el sistema operativo**, establece la variable **OSDTargetSystemDrive** en la letra de unidad de la partición que contiene los archivos de sistema operativo.  

Este paso de secuencia de tareas solo se ejecuta en Windows PE, No se ejecuta en el sistema operativo completo.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDConfigFileName](/sccm/osd/understand/task-sequence-variables#OSDConfigFileName)  
- [OSDImageIndex](/sccm/osd/understand/task-sequence-variables#OSDImageIndex)  
- [OSDTargetSystemDrive](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemDrive)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Imágenes** y **Aplicar imagen de sistema operativo**.

Este paso realiza acciones en función de si usa una imagen de sistema operativo o un paquete de actualización del sistema operativo.  

#### <a name="os-image-actions"></a>Acciones de imagen de sistema operativo

El paso **Aplicar imagen de sistema operativo** realiza las acciones siguientes cuando se usa una imagen de sistema operativo:  

1. Elimina todo el contenido en el volumen de destino, excepto los archivos de la carpeta que especifica la variable **\_SMSTSUserStatePath**.  

2. Extrae el contenido del archivo .wim especificado en la partición de destino especificada.  

3. Prepara el archivo de respuesta:  

    1. Crea un nuevo archivo de respuesta predeterminado de instalación de Windows (sysprep.inf o unattend.xml) para el sistema operativo implementado.  

    2. Combina los valores del archivo de respuesta proporcionado por el usuario.  

4. Copia los cargadores de arranque de Windows en la partición activa.  

5. Configura el archivo boot.ini o la base de datos de la configuración de arranque (BCD) para que hagan referencia al sistema operativo que se acaba de instalar.  

#### <a name="os-upgrade-package-actions"></a>Acciones del paquete de actualización del sistema operativo

El paso **Aplicar imagen de sistema operativo** realiza las acciones siguientes cuando se usa un paquete de actualización del sistema operativo:  

1. Elimina todo el contenido en el volumen de destino, excepto los archivos de la carpeta que especifica la variable **\_SMSTSUserStatePath**.  

2. Prepara el archivo de respuesta:  

    1. Cree un archivo de respuesta nuevo con los valores estándar creados por Configuration Manager.  

    2. Combina los valores del archivo de respuesta proporcionado por el usuario.  

### <a name="properties"></a>Propiedades

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="apply-operating-system-from-a-captured-image"></a>Aplicar el sistema operativo de una imagen capturada

Instala una imagen de sistema operativo que capture. Seleccione **Examinar** para abrir el cuadro de diálogo **Seleccionar un paquete**. Después, seleccione el paquete de imagen existente que quiera instalar. Si hay varias imágenes asociadas con el **Paquete de imágenes** especificado, seleccione en la lista desplegable la imagen asociada que se va a usar para esta implementación. Para ver información básica sobre cada imagen, selecciónela.  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>Aplicar imagen de sistema operativo desde un origen de instalación original

Instala un sistema operativo mediante un paquete de actualización del sistema operativo, que también es un origen de instalación original. Seleccione **Examinar** para abrir el cuadro de diálogo **Seleccionar un paquete de actualización del sistema operativo**. Después, seleccione el paquete de actualización de sistema operativo existente que quiera usar. Para ver información básica sobre cada origen de imagen, selecciónelo. El panel de resultados de la parte inferior del cuadro de diálogo muestra las propiedades asociadas del origen de imagen. Si hay varias ediciones asociadas con el paquete especificado, use la lista desplegable para seleccionar la **Edición** que desea usar.  

> [!NOTE]  
> Los **paquetes de actualización del sistema operativo** están pensados principalmente para su uso con las actualizaciones locales, no para las nuevas instalaciones de Windows. Al implementar nuevas instalaciones de Windows, use la opción **Aplicar el sistema operativo de una imagen capturada** junto a **install.wim** desde los archivos de origen de instalación.
>
> La implementación de nuevas instalaciones de Windows a través de **paquetes de actualización del sistema operativo** se sigue permitiendo, pero dependerá de que los controladores sean compatibles con este método. Cuando se instala Windows desde un paquete de actualización del sistema operativo, los controladores se instalan en Windows PE en lugar de simplemente inyectarse en Windows PE. Algunos controladores no son compatibles con la instalación en Windows PE.
>
> Si los controladores no son compatibles con la instalación en Windows PE, cree una **imagen de sistema operativo** con el **install.wim** de los archivos de origen de instalación originales. Luego, impleméntelo usando la opción **Aplicar el sistema operativo de una imagen capturada** en su lugar.

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>Usar un archivo de respuesta Sysprep o de instalación desatendida para realizar una instalación personalizada

Use esta opción para proporcionar un archivo de respuesta del programa de instalación de Windows (**unattend.xml**, **unattend.txt**o **sysprep.inf**) según el método de instalación y la versión del sistema operativo. El archivo que especifique puede incluir cualquiera de las opciones de configuración estándar compatibles con los archivos de respuesta de Windows. Por ejemplo, puede usarlo para especificar la página principal predeterminada de Internet Explorer. Especifique el paquete que contiene el archivo de respuesta y la ruta de acceso asociada al archivo en el paquete.  

> [!NOTE]  
> El archivo de respuesta del programa de instalación de Windows que suministre puede contener variables de secuencia de tareas insertadas de tipo `%varname%`, donde *varname* es el nombre de la variable. El paso **Instalar Windows y Configuration Manager** sustituye a la cadena de variable por el valor real de la variable. No puede usar estas variables de secuencia de tareas insertadas en campos solo numéricos de un archivo de respuesta unattend.xml.  

Si no se proporciona un archivo de respuesta del programa de instalación de Windows, esta secuencia de tareas genera automáticamente un archivo de respuesta.  

#### <a name="destination"></a>Destino

Configure una de las opciones siguientes:  

- **Siguiente partición disponible:** use la siguiente partición secuencial que no haya sido destino previo de los pasos **Aplicar el sistema operativo** o **Aplicar imagen de datos** en esta secuencia de tareas.  

- **Disco y partición específicos**: seleccione el número de **Disco** (empezando por 0) y el número de **Partición** (empezando por 1).  

- **Letra de unidad lógica específica**: especifique la **Letra de unidad** asignada a la partición por Windows PE. Esta letra de unidad puede ser diferente de la que asigna el sistema operativo recién implementado.  

- **Letra de unidad lógica almacenada en una variable**: especifique la variable de secuencia de tareas que contiene la letra de unidad asignada a la partición por Windows PE. Normalmente, esta variable se establece en la sección Avanzado del cuadro de diálogo **Propiedades de la partición** del paso de la secuencia de tareas **Formatear y crear particiones en el disco**.  

### <a name="options"></a>Opciones  

Además de las opciones predeterminadas, configure las siguientes opciones adicionales en la pestaña **Opciones** de este paso de secuencia de tareas:  

#### <a name="access-content-directly-from-the-distribution-point"></a>Acceder al contenido directamente desde el punto de distribución

Configure la secuencia de tareas para que tenga acceso a la imagen de sistema operativo directamente desde el punto de distribución. Por ejemplo, use esta opción al implementar sistemas operativos en dispositivos incrustados que tengan una capacidad de almacenamiento limitada. Cuando seleccione esta opción, establezca también la configuración del recurso compartido de paquete en la pestaña **Acceso a datos** de las propiedades de imagen del sistema operativo.  

> [!NOTE]  
> Esta configuración invalida la opción de implementación que se configura en la página **Puntos de distribución** del **Asistente para implementar software**. Esta invalidación es solo para la imagen de sistema operativo especificada en este paso, no para el contenido de todas las secuencia de tareas.  

> [!IMPORTANT]  
> Para mayor seguridad, se recomienda encarecidamente no seleccionar esta opción. Esta opción está diseñada principalmente para su uso en dispositivos con capacidad de almacenamiento limitada. No está pensada para ayudar a aumentar la velocidad de la secuencia de tareas. Cuando se selecciona esta opción, no se comprueba el hash del paquete del sistema operativo. Por lo tanto, no se puede garantizar la integridad del paquete porque es posible que los usuarios con derechos administrativos alteren o manipulen el contenido del paquete.



## <a name="BKMK_ApplyWindowsSettings"></a> Aplicar configuraciones de Windows  

Use este paso para configurar las opciones de Windows del equipo de destino. La secuencia de tareas almacena estos valores en el archivo de respuesta adecuado. El programa de instalación de Windows usa este archivo de respuesta durante el paso **Instalar Windows y Configuration Manager**.  

Este paso de secuencia de tareas solo se ejecuta en Windows PE, No se ejecuta en el sistema operativo completo.  

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDComputerName](/sccm/osd/understand/task-sequence-variables#OSDComputerName-input)  
- [OSDLocalAdminPassword](/sccm/osd/understand/task-sequence-variables#OSDLocalAdminPassword)  
- [OSDProductKey](/sccm/osd/understand/task-sequence-variables#OSDProductKey)  
- [OSDRandomAdminPassword](/sccm/osd/understand/task-sequence-variables#OSDRandomAdminPassword)  
- [OSDRegisteredOrgName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredOrgName-input)  
- [OSDRegisteredUserName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredUserName)  
- [OSDServerLicenseConnectionLimit](/sccm/osd/understand/task-sequence-variables#OSDServerLicenseConnectionLimit)  
- [OSDServerLicenseMode](/sccm/osd/understand/task-sequence-variables#OSDServerLicenseMode)  
- [OSDTimeZone](/sccm/osd/understand/task-sequence-variables#OSDTimeZone-input)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Configuración** y **Aplicar configuraciones de Windows**.

### <a name="properties"></a>Propiedades

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="user-name"></a>Nombre de usuario

Especifique el nombre de usuario registrado para asociar con el equipo de destino. El valor que captura el paso de la secuencia de tareas **Capturar configuración de Windows** puede reemplazar este valor.  

#### <a name="organization-name"></a>Nombre de la organización

Especifique el nombre de la organización registrado para asociar con el equipo de destino. El valor que captura el paso de la secuencia de tareas **Capturar configuración de Windows** puede reemplazar este valor.  

#### <a name="product-key"></a>Clave de producto  

Especifique la clave de producto para usar en la instalación de Windows en el equipo de destino.  

#### <a name="server-licensing"></a>Licencia de servidor

Especificar el modo de licencia de servidor.

- Seleccione **Por servidor** o **Por usuario** como modo de licencia.  
- Si selecciona **Por servidor**, especifique también el número máximo de conexiones permitidas según el contrato de licencia.  
- Si el equipo de destino no es un servidor o si no desea especificar el modo de licencia, seleccione **No especificar**.  

#### <a name="maximum-connections"></a>Núm. máximo de conexiones

Especifique el número máximo de conexiones disponibles para este equipo según lo indicado en el contrato de licencia.  

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>Generar la contraseña de administrador local aleatoriamente y deshabilitar la cuenta en todas las plataformas admitidas (recomendado)  

Seleccione esta opción para establecer la contraseña de administrador local en una cadena generada de forma aleatoria. Esta opción también deshabilita la cuenta de administrador local en las plataformas que admiten esta característica.  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>Habilitar la cuenta y especificar la contraseña de administrador local  

Seleccione esta opción para habilitar la cuenta de administrador local con la contraseña especificada. Escriba la contraseña en la línea **Contraseña** y confírmela en la línea **Confirmar contraseña** .  

#### <a name="time-zone"></a>Zona horaria

Especifique la zona horaria que se configurará en el equipo de destino. El valor que captura el paso de la secuencia de tareas **Capturar configuración de Windows** puede reemplazar este valor.  



## <a name="BKMK_AutoApplyDrivers"></a> Aplicar controladores automáticamente  

Use este paso para hacer coincidir e instalar controladores como parte de la implementación de sistema operativo.  

El paso de secuencia de tareas **Aplicar controladores automáticamente** realiza las acciones siguientes:  

1. Examina el hardware y busca los identificadores de Plug and Play de todos los dispositivos presentes en el sistema.  

2. Envía la lista de dispositivos y sus identificadores de Plug and Play al punto de administración. El punto de administración devuelve, desde el catálogo de controladores, una lista de los controladores compatibles con cada dispositivo de hardware. En la lista se incluyen todos los controladores habilitados independientemente del paquete de controladores en el que estén y los controladores etiquetados con la categoría de controlador especificado.  

3. Para cada dispositivo de hardware, la secuencia de tareas elige el mejor controlador. Este controlador es adecuado para el sistema operativo implementado y se encuentra en un punto de distribución accesible.  

4. La secuencia de tareas descarga los controladores seleccionados desde un punto de distribución y los preconfigura en el sistema operativo de destino.  

    1. Cuando se usa una imagen de sistema operativo, la secuencia de tareas coloca los controladores en el almacén de controladores del sistema operativo.  

    2. Cuando se usa un paquete de actualización del sistema operativo como origen de instalación original, la secuencia de tareas configura la instalación de Windows con la ubicación de los controladores.  

5. Durante el paso **Instalar Windows y Configuration Manager** de la secuencia de tareas, el programa de instalación de Windows busca los controladores preconfigurados por este paso.  

> [!IMPORTANT]  
> Los medios independientes no pueden usar el paso **Aplicar controladores automáticamente**. La secuencia de tareas no tiene conexión con el sitio de Configuration Manager en este escenario.  

Este paso de secuencia de tareas solo se ejecuta en Windows PE, No se ejecuta en el sistema operativo completo.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDAutoApplyDriverBestMatch](/sccm/osd/understand/task-sequence-variables#OSDAutoApplyDriverBestMatch)  
- [OSDAutoApplyDriverCategoryList](/sccm/osd/understand/task-sequence-variables#OSDAutoApplyDriverCategoryList)  
- [SMSTSDriverRequestConnectTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestConnectTimeOut)  
- [SMSTSDriverRequestReceiveTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestReceiveTimeOut)  
- [SMSTSDriverRequestResolveTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestResolveTimeOut)  
- [SMSTSDriverRequestSendTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestSendTimeOut)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Controladores** y **Aplicar controladores automáticamente**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>Instalar solo los controladores compatibles más coincidentes

Especifica que el paso de secuencia de tareas solo instala el controlador que mejor coincide con cada dispositivo de hardware detectado.  

#### <a name="install-all-compatible-drivers"></a>Instalar todos los controladores compatibles

La secuencia de tareas instala todos los controladores compatibles para cada dispositivo de hardware detectado. Después, el programa de instalación de Windows elige el mejor controlador. Esta opción consume más ancho de banda de red y espacio de disco. La secuencia de tareas descarga más controladores, pero Windows puede seleccionar un controlador más adecuado.  

#### <a name="consider-drivers-from-all-categories"></a>Considerar controladores de todas las categorías

La secuencia de tareas busca los controladores de dispositivo apropiados en todas las categorías de controladores disponibles.  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>Limitar la coincidencia de controladores a los controladores de las categorías seleccionadas

La secuencia de tareas busca los controladores de dispositivo apropiados en las categorías de controlador especificadas.  

Si selecciona varias categorías, se devuelven todos los controladores coincidentes que existen en cualquiera de las categorías. Es equivalente a una operación `OR`.<!-- SCCMDocs issue 851 -->

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>Llevar a cabo la instalación desatendida de controladores no firmados en versiones de Windows en las que se permita

Esta opción permite que Windows instale controladores sin una firma digital.  

> [!IMPORTANT]  
> Esta opción no es aplicable a los sistemas operativos en los que no se puede configurar la directiva de firma de controladores.  



## <a name="BKMK_CaptureNetworkSettings"></a> Capturar configuración de red  

Use este paso para capturar la configuración de red de Microsoft en el equipo que ejecuta la secuencia de tareas. La secuencia de tareas guarda esta configuración en las variables de secuencia de tareas. Esta configuración invalida la predeterminada que establezca en el paso **Aplicar configuración de red**.  

Este paso de secuencia de tareas solo se ejecuta en el sistema operativo completo. No se ejecuta en Windows PE.  

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDMigrateAdapterSettings](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdapterSettings)  
- [OSDMigrateNetworkMembership](/sccm/osd/understand/task-sequence-variables#OSDMigrateNetworkMembership)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Configuración** y **Capturar configuración de red**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="migrate-domain-and-workgroup-membership"></a>Migrar la pertenencia a grupo de trabajo y dominio

Captura la información de pertenencia a dominio y grupo de trabajo del equipo de destino.  

#### <a name="migrate-network-adapter-configuration"></a>Migrar la configuración del adaptador de red

Captura la configuración del adaptador de red del equipo de destino. Captura la siguiente información:

- Configuración de red global  
- Número de adaptadores  
- La siguiente configuración de red asociada a cada adaptador: DNS, WINS, IP y filtros de puerto



## <a name="BKMK_CaptureOperatingSystemImage"></a> Capturar imagen de sistema operativo  

Este paso captura una o más imágenes de un equipo de referencia. La secuencia de tareas crea un archivo de imagen de Windows (.wim) en el recurso compartido de red especificado. Después, use el asistente para **agregar paquete de imagen de sistema operativo** para importar esta imagen a Configuration Manager para las implementaciones de sistema operativo basadas en imágenes.  

Configuration Manager captura cada volumen (unidad) del equipo de referencia como una imagen independiente en el archivo .wim. Si el equipo al que se hace referencia tiene varios volúmenes, el archivo .wim resultante contiene una imagen independiente para cada volumen. Este paso solo captura los volúmenes formateados como NTFS o FAT32. Omite los volúmenes con otros formatos y los volúmenes USB.  

El sistema operativo instalado en el equipo de referencia debe ser una versión de Windows que sea compatible con Configuration Manager. Use la herramienta SysPrep para preparar el sistema operativo en el equipo de referencia. El volumen del sistema operativo instalado y el volumen de arranque deben ser el mismo.  

Especifique una cuenta con permisos de escritura en el recurso compartido de red seleccionado. Para obtener más información sobre la cuenta de captura de imagen del sistema operativo, consulte [Cuentas](/sccm/core/plan-design/hierarchy/accounts#capture-os-image-account).

Este paso de secuencia de tareas solo se ejecuta en Windows PE, No se ejecuta en el sistema operativo completo.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDCaptureAccount](/sccm/osd/understand/task-sequence-variables#OSDCaptureAccount)  
- [OSDCaptureAccountPassword](/sccm/osd/understand/task-sequence-variables#OSDCaptureAccountPassword)  
- [OSDCaptureDestination](/sccm/osd/understand/task-sequence-variables#OSDCaptureDestination)  
- [OSDImageCreator](/sccm/osd/understand/task-sequence-variables#OSDImageCreator)  
- [OSDImageDescription](/sccm/osd/understand/task-sequence-variables#OSDImageDescription)  
- [OSDImageVersion](/sccm/osd/understand/task-sequence-variables#OSDImageVersion)  
- [OSDTargetSystemRoot](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemRoot-input)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Imágenes** y **Capturar imagen de sistema operativo**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="target"></a>Target  

Ruta de acceso del sistema de archivos a la ubicación que Configuration Manager usa al almacenar la imagen capturada del sistema operativo.  

#### <a name="description"></a>Descripción  

Descripción opcional definida por el usuario de la imagen capturada del sistema operativo que está almacenada en el archivo de imagen.  

#### <a name="version"></a>Versión  

Número de versión opcional definido por el usuario que se asigna a la imagen capturada del sistema operativo. Este valor puede ser cualquier combinación de letras y números. Se almacena en el archivo de imagen.  

#### <a name="created-by"></a>Creado por  

El nombre opcional del usuario que creó la imagen del sistema operativo. Se almacena en el archivo de imagen.  

#### <a name="capture-operating-system-image-account"></a>Cuenta de captura de imagen del sistema operativo  

Especifique la cuenta de Windows que tenga permisos en el recurso compartido de red especificado. Seleccione **Establecer** para especificar el nombre de esa cuenta de Windows.  



## <a name="BKMK_CaptureUserState"></a> Capturar estado de usuario  

Este paso usa la herramienta de migración de estado de usuario (USMT) para de capturar el estado de usuario y la configuración del equipo que ejecuta la secuencia de tareas. Este paso de secuencia de tareas se usa junto con el paso **Restaurar estado de usuario** . Este paso siempre cifra el almacén de estado de USMT mediante una clave de cifrado generada y administrada por Configuration Manager.  

Para obtener más información sobre cómo administrar el estado de usuario al implementar sistemas operativos, consulte [Administrar el estado de usuario](/sccm/osd/get-started/manage-user-state).  

Si quiere guardar y restaurar la configuración de estado de usuario desde un punto de migración de estado, use este paso con los pasos **Solicitar almacén de estado** y **Liberar almacén de estado**.  

Este paso proporciona control sobre un subconjunto limitado de las opciones de USMT más usadas. Especifique más opciones de línea de comandos con la variable de secuencia de tareas **OSDMigrateAdditionalCaptureOption**.  

Este paso de secuencia de tareas solo se ejecuta en Windows PE, No se ejecuta en el sistema operativo completo.  

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [_OSDMigrateUsmtPackageID](/sccm/osd/understand/task-sequence-variables#OSDMigrateUsmtPackageID)  
- [OSDMigrateAdditionalCaptureOptions](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdditionalCaptureOptions)  
- [OSDMigrateConfigFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateConfigFiles)  
- [OSDMigrateContinueOnLockedFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateContinueOnLockedFiles)  
- [OSDMigrateEnableVerboseLogging](/sccm/osd/understand/task-sequence-variables#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateMode](/sccm/osd/understand/task-sequence-variables#OSDMigrateMode)  
- [OSDMigrateSkipEncryptedFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateSkipEncryptedFiles)  
- [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Estado de usuario** y **Capturar estado de usuario**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="user-state-migration-tool-package"></a>Paquete de herramientas de migración de estado de usuario

Especifique el paquete que contiene la herramienta de migración de estado de usuario (USMT). La secuencia de tareas usa esta versión de USMT para capturar el estado de usuario y la configuración. Este paquete no requiere un programa. Especifique un paquete que contenga la versión de 32 o 64 bits de USMT. La arquitectura de USMT depende de la arquitectura del sistema operativo desde el que la secuencia de tareas captura el estado.  

#### <a name="capture-all-user-profiles-with-standard-options"></a>Capturar todos los perfiles de usuario mediante opciones estándar

Migre toda la información de perfiles de usuario. Esta opción es el valor predeterminado.  

Si selecciona esta opción, pero no selecciona **Restaurar perfiles de usuario de equipo local** en el paso **Restaurar estado de usuario**, se produce un error en la secuencia de tareas. Configuration Manager no puede migrar las cuentas nuevas sin asignarles contraseñas.

Cuando se usa la opción **Instalar un paquete de imágenes existente** del asistente **Nueva secuencia de tareas**, la secuencia de tareas resultante tiene como valor predeterminado **Capturar todos los perfiles de usuario mediante opciones estándar**. Esta secuencia de tareas predeterminada no selecciona la opción **Restaurar perfiles de usuario de equipo local**, es decir, cuentas de usuario que no son de dominio.  

Seleccione **Restaurar perfiles de usuario de equipo local** y proporcione una contraseña para la cuenta que desea migrar. En una secuencia de tareas creada manualmente, esta configuración se encuentra en el paso **Restaurar estado de usuario**. En una secuencia de tareas creada por el asistente **Nueva secuencia de tareas** , esta configuración se encuentra en el paso **Restaurar configuración y archivos de usuario** .  

Si no tiene ninguna cuenta de usuario local, esta configuración no se aplica.  

#### <a name="customize-how-user-profiles-are-captured"></a>Personalizar la captura de perfiles de usuario

Seleccione esta opción para especificar una migración de archivos de perfil personalizada. Seleccione **Archivos** para seleccionar los archivos de configuración que USMT usará en este paso. Especifique un archivo .xml personalizado que contenga las reglas que definen los archivos de estado de usuario que se van a migrar.  

#### <a name="click-here-to-select-configuration-files"></a>Haga clic aquí para seleccionar archivos de configuración

Seleccione esta opción para elegir los archivos de configuración en el paquete USMT que desea usar para capturar los perfiles de usuario. Seleccione el botón **Archivos** para iniciar el cuadro de diálogo **Archivos de configuración**. Para especificar un archivo de configuración, escriba el nombre del archivo en la línea **Nombre de archivo** y seleccione el botón **Agregar**.  

#### <a name="enable-verbose-logging"></a>Habilitar el registro detallado

Habilite esta opción para generar información más detallada en el archivo de registro. Al capturar el estado, la secuencia de tareas genera de forma predeterminada **ScanState.log** en la carpeta de registro de secuencia de tareas, `%WinDir%\ccm\logs`.  

#### <a name="skip-files-using-encrypted-file-system"></a>Omitir archivos que usan el sistema de cifrado de archivos

Habilite esta opción para omitir la captura de archivos cifrados con el Sistema de cifrado de archivos (EFS). Estos archivos incluyen archivos de perfil de usuario. Según el sistema operativo y las versiones de USMT, los archivos cifrados podrían no ser legibles después de la restauración. Para obtener más información, consulte la documentación de USMT.  

#### <a name="copy-by-using-file-system-access"></a>Copiar mediante el acceso al sistema de archivos

Habilite esta opción para especificar cualquiera de las siguientes opciones:  

- **Continuar si algunos archivos no se pueden capturar**: habilite esta configuración para continuar con el proceso de migración incluso si no puede capturar algunos archivos. Si deshabilita esta opción, se produce un error en este paso si no se puede capturar un archivo. Esta opción está habilitada de forma predeterminada.  

- **Capturar localmente mediante vínculos en vez de mediante la copia de archivos**: habilite esta opción para usar vínculos físicos NTFS para capturar archivos.  

    Para obtener más información sobre cómo migrar datos mediante vínculos físicos, consulte el tema en el que se describe el [almacén de migración de vínculos físicos](https://docs.microsoft.com/windows/deployment/usmt/usmt-hard-link-migration-store).  

- **Capturar en modo fuera de línea (solo Windows PE)** : habilite esta opción para capturar el estado de usuario en Windows PE en lugar de todo el sistema operativo.  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>Capturar mediante el Servicio de instantánea de copia de volumen (VSS)

Esta opción permite capturar archivos incluso si otra aplicación los ha bloqueado para su edición.  



## <a name="BKMK_CaptureWindowsSettings"></a> Capturar configuración de Windows  

Use este paso para capturar la configuración de Windows en el equipo que ejecuta la secuencia de tareas. La secuencia de tareas guarda esta configuración en las variables de secuencia de tareas. Esta configuración capturada invalida la predeterminada que establezca en el paso **Aplicar configuración de Windows**.  

Este paso de secuencia de tareas se ejecuta en el sistema operativo completo o Windows PE.  

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDComputerName](/sccm/osd/understand/task-sequence-variables#OSDComputerName-output)  
- [OSDMigrateComputerName](/sccm/osd/understand/task-sequence-variables#OSDMigrateComputerName)  
- [OSDMigrateRegistrationInfo](/sccm/osd/understand/task-sequence-variables#OSDMigrateRegistrationInfo)  
- [OSDMigrateTimeZone](/sccm/osd/understand/task-sequence-variables#OSDMigrateTimeZone)  
- [OSDRegisteredOrgName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredOrgName-output)  
- [OSDTimeZone](/sccm/osd/understand/task-sequence-variables#OSDTimeZone-output)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Configuración** y **Capturar configuración de Windows**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="migrate-computer-name"></a>Migrar nombre de equipo

Capture el nombre de equipo NetBIOS del equipo.  

#### <a name="migrate-registered-user-and-organization-names"></a>Migrar nombres de organización y usuario registrados

Capture los nombres de organización y usuario registrados en el equipo.  

#### <a name="migrate-time-zone"></a>Migrar zona horaria

Capture la configuración de zona horaria en el equipo.  



## <a name="BKMK_CheckReadiness"></a> Comprobar preparación  

Use este paso para comprobar que el equipo de destino cumpla los requisitos previos de implementación especificados.  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **General** y **Comprobar preparación**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="ensure-minimum-memory-mb"></a>Garantizar mínimo de memoria (MB)

Compruebe que la cantidad de memoria, en megabytes (MB), coincide o supera la cantidad especificada. El paso habilita esta configuración de forma predeterminada.  

#### <a name="ensure-minimum-processor-speed-mhz"></a>Garantizar velocidad mínima de procesador (MHz)  

Compruebe que la velocidad del procesador, expresada en megahercios (MHz), cumple o supera la cantidad especificada. El paso habilita esta configuración de forma predeterminada.  

#### <a name="ensure-minimum-free-disk-space-mb"></a>Garantizar espacio libre en disco mínimo (MB)

Compruebe que la cantidad de espacio libre en disco, en megabytes (MB), cumple o supera la cantidad especificada.  

#### <a name="ensure-current-os-to-be-refreshed-is"></a>Garantizar que el sistema operativo actual que se va a actualizar es

Compruebe que el sistema operativo instalado en el equipo de destino cumple el requisito especificado. El paso lo establece en **CLIENTE** de forma predeterminada.  

### <a name="options"></a>Opciones

> [!NOTE]  
> Si habilita la opción **Continuar después de un error** en la pestaña **Opciones** de este paso, solo registra los resultados de la comprobación de preparación. Si se produce un error en una comprobación, la secuencia de tareas no se detiene.  



## <a name="BKMK_ConnectToNetworkFolder"></a> Conectar a carpeta de red  

Use este paso para crear una conexión a una carpeta de red compartida.  

Este paso de secuencia de tareas se ejecuta en el sistema operativo completo o Windows PE.  

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [SMSConnectNetworkFolderAccount](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderAccount)  
- [SMSConnectNetworkFolderDriveLetter](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderDriveLetter)  
- [SMSConnectNetworkFolderPassword](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderPassword)  
- [SMSConnectNetworkFolderPath](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderPath)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **General** y **Conectar a carpeta de red**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="path"></a>Ruta de acceso  

Seleccione **Examinar** para especificar la ruta de acceso de la carpeta de red. Use el formato `\\server\share`.

#### <a name="drive"></a>Unidad  

Seleccione la letra de unidad local que se va a asignar a esta conexión.

#### <a name="account"></a>Cuenta

Seleccione **Establecer** para especificar la cuenta de usuario con permisos para conectarse a esta carpeta de red. Para obtener más información sobre la cuenta de conexión de la carpeta de red de la secuencia de tareas, consulte [Cuentas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-network-folder-connection-account).



## <a name="BKMK_DisableBitLocker"></a> Deshabilitar BitLocker  

Use este paso para deshabilitar el cifrado de BitLocker en la unidad de sistema operativo actual o en una unidad específica. Con esta acción, los protectores de clave permanecen visibles en texto no cifrado en el disco duro. No descifra el contenido de la unidad. Esta acción se completa casi al instante.  

> [!NOTE]  
> El cifrado de unidad de BitLocker ofrece cifrado de nivel bajo del contenido de un volumen de disco.  

Si tiene varias unidades cifradas, deshabilite BitLocker en las unidades de datos antes de deshabilitar BitLocker en la unidad del sistema operativo.  

Este paso solo se ejecuta en el sistema operativo completo. No se ejecuta en Windows PE.  

A partir de la versión 1906, use las siguientes variables de secuencia de tareas con este paso:  

- [OSDBitLockerRebootCount](/sccm/osd/understand/task-sequence-variables#OSDBitLockerRebootCount)  
- [OSDBitLockerRebootCountOverride](/sccm/osd/understand/task-sequence-variables#OSDBitLockerRebootCountOverride)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Discos** y **Deshabilitar BitLocker**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="current-operating-system-drive"></a>Unidad actual del sistema operativo

Deshabilita BitLocker en la unidad actual del sistema operativo.  

#### <a name="specific-drive"></a>Unidad específica  

Deshabilita BitLocker en una unidad específica. Use la lista desplegable para especificar la unidad donde se deshabilita BitLocker.  

#### <a name="resume-protection-after-windows-has-been-restarted-the-specified-number-of-times"></a>Reanudar la protección después de que se haya reiniciado Windows el número de veces especificado

<!-- 4512937 -->
A partir de la versión 1906, use esta opción para especificar el número de reinicios para mantener BitLocker deshabilitado. En lugar de agregar varias instancias de este paso, defina un valor comprendido entre 1 (el predeterminado) y 15.

Puede establecer y modificar este comportamiento con las variables de secuencia de tareas [OSDBitLockerRebootCount](/sccm/osd/understand/task-sequence-variables#OSDBitLockerRebootCount) y [OSDBitLockerRebootCountOverride](/sccm/osd/understand/task-sequence-variables#OSDBitLockerRebootCountOverride).


## <a name="BKMK_DownloadPackageContent"></a> Descargar contenido de paquete  

Use este paso para descargar cualquiera de los tipos de paquete siguientes:  

- Imágenes de SO  
- Paquetes de actualización del sistema operativo  
- Paquetes de controladores  
- Paquetes  
- Imágenes de arranque (en la versión 1810 y anteriores)  

Este paso funciona bien en una secuencia de tareas para actualizar un sistema operativo en los escenarios siguientes:  

- Para usar una secuencia de tareas de actualización única que funciona con las plataformas x86 y x64. Incluya dos pasos **Descargar contenido de paquete** en el grupo **Preparación para actualización**. Especifique las condiciones en la pestaña **Opciones** para detectar la arquitectura de cliente y descargar únicamente el paquete de actualización del sistema operativo adecuado. Configure los pasos **Descargar contenido de paquete** para que usen la misma variable. Use la variable para la ruta de acceso de medios en el paso **Actualizar sistema operativo**.  

- Para descargar dinámicamente un paquete de controladores aplicables, use dos pasos **Descargar contenido de paquete** con condiciones para detectar el tipo de hardware adecuado para cada paquete de controlador. Configure los pasos **Descargar contenido de paquete** para que usen la misma variable. Use la variable para el valor **Contenido preconfigurado** de la sección Controladores del paso **Actualizar sistema operativo**.  

> [!NOTE]  
> Al implementar una secuencia de tareas que contiene este paso, no seleccione **Descargar todo el contenido localmente antes de iniciar la secuencia de tareas** o **Acceder al contenido directamente desde un punto de distribución** para **Opciones de implementación** en la página **Puntos de distribución** del Asistente para implementar software.  

Este paso se ejecuta en el sistema operativo completo o Windows PE. En Windows PE no se admite la opción de guardar el paquete en la caché de cliente de Configuration Manager.

> [!NOTE]  
> La tarea **descargar contenido de paquete** no se admite para su uso con medios independientes. Para obtener más información, consulte [acciones no compatibles para medios independientes](/sccm/osd/deploy-use/create-stand-alone-media#unsupported-actions-for-stand-alone-media).  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Software** y **Descargar contenido de paquete**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="select-package"></a>Seleccionar paquete  

Seleccione el icono para elegir el paquete de descarga. Después de elegir un paquete, seleccione el icono de nuevo para elegir otro paquete.  

#### <a name="place-into-the-following-location"></a>Colocar en la siguiente ubicación

Elija guardar el paquete en una de las siguientes ubicaciones:  

- **Directorio de trabajo de secuencia de tareas**: esta ubicación también se conoce como memoria caché de la secuencia de tareas.  

- **Caché de cliente de Configuration Manager**: use esta opción para almacenar el contenido en la caché de cliente. De forma predeterminada, esta ruta de acceso es `%WinDir%\ccmcache`.  

- **Ruta de acceso personalizada**: el motor de secuencia de tareas descarga primero el paquete en el directorio de trabajo de la secuencia de tareas. A continuación, mueve el contenido a esta ruta de acceso que especifique. El motor de secuencia de tareas anexa la ruta de acceso al identificador del paquete.  

#### <a name="save-path-as-a-variable"></a>Guardar ruta de acceso como variable

Guarde la ruta de acceso del paquete en una variable de secuencia de tareas personalizada. A continuación, utilice esta variable en otro paso de la secuencia de tareas.

Configuration Manager agrega un sufijo numérico al nombre de variable. Por ejemplo, especifique una variable de `%MyContent%` como variable personalizada. Es la raíz para la que la secuencia de tareas almacena todo el contenido al que se hace referencia en este paso. Este contenido puede incluir varios paquetes. Al hacer referencia a la variable, agregue un sufijo numérico. Para el primer paquete, haga referencia a `%MyContent01%`. Cuando se hace referencia a la variable en pasos posteriores, como **Actualizar sistema operativo**, use `%MyContent02%` o `%MyContent03%`, donde el número corresponde al orden en el que el paso **Descargar contenido de paquete** enumera los paquetes.  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>Si se produce un error en la descarga de un paquete, continúe con la descarga de otros paquetes de la lista

Si se produce un error en la secuencia de tareas al descargar un paquete, se inicia la descarga del paquete siguiente en la lista.  



## <a name="BKMK_EnableBitLocker"></a> Habilitar BitLocker  

Use este paso para habilitar el cifrado de BitLocker en al menos dos particiones en el disco duro. La primera partición activa contiene el código de arranque de Windows. La otra partición contiene el sistema operativo. La partición de arranque debe permanecer sin cifrar.  

Use el paso **Tener en servicio BitLocker** para habilitar BitLocker en una unidad de disco en Windows PE. Para obtener más información, consulte [Tener en servicio BitLocker](#BKMK_PreProvisionBitLocker).  

> [!NOTE]  
> El cifrado de unidad de BitLocker ofrece cifrado de nivel bajo del contenido de un volumen de disco.  

Este paso solo se ejecuta en el sistema operativo completo. No se ejecuta en Windows PE.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDBitLockerRecoveryPassword](/sccm/osd/understand/task-sequence-variables#OSDBitLockerRecoveryPassword)  
- [OSDBitLockerStartupKey](/sccm/osd/understand/task-sequence-variables#OSDBitLockerStartupKey)  

Cuando se especifica **Solo TPM**, **TPM y clave de inicio en USB** o **TPM con PIN**, el Módulo de plataforma segura (TPM) debe estar en el siguiente estado antes de poder ejecutar el paso **Habilitar BitLocker**:  

- Habilitado  
- Activado  
- Propiedad permitida  

Este paso completa cualquier inicialización de TPM restante. Los pasos restantes no requieren presencia física ni reinicios. El paso **Habilitar BitLocker** finaliza de forma transparente los demás pasos de inicialización de TPM, si es necesario:  

- Crear par de claves de aprobación  
- Crear valor de autorización de propietario y custodia para Active Directory, que debe extenderse para admitir este valor  
- Tomar posesión  
- Crear la clave raíz de almacenamiento, o restablecerla si ya existe pero no es compatible  

Si quiere que la secuencia de tareas espere a que el paso **Habilitar BitLocker** complete el proceso de cifrado de unidad, seleccione la opción **Esperar**. Si no selecciona la opción **Esperar**, el proceso de cifrado de unidad tiene lugar en segundo plano. La secuencia de tareas continúa inmediatamente al paso siguiente.  

BitLocker puede usarse para cifrar varias unidades en un equipo (tanto de sistema operativo como de unidades de datos). Para cifrar una unidad de datos, cifre primero la unidad del sistema operativo y complete el proceso de cifrado. Este requisito se debe a que la unidad del sistema operativo almacena los protectores de clave para las unidades de datos. Si cifra el sistema operativo y las unidades de datos en la misma secuencia de tareas, seleccione la opción **Esperar** en el paso **Habilitar BitLocker** para la unidad de sistema operativo.  

Si el disco duro ya está cifrado pero BitLocker está deshabilitado, el paso **Habilitar BitLocker** vuelve a habilitar los protectores de clave y se completa con rapidez. En este caso no es necesario volver a cifrar la unidad de disco duro.  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Discos** y **Habilitar BitLocker**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="choose-the-drive-to-encrypt"></a>Elija la unidad que desea cifrar

Especifica la unidad que se va a cifrar. Para cifrar la unidad del sistema operativo actual, seleccione **Unidad actual del sistema operativo**. Configure una de las opciones siguientes para la administración de claves:  

- **Solo TPM**: seleccione esta opción para usar solo el Módulo de plataforma segura (TPM).  

- **Clave de inicio solo en USB**: seleccione esta opción para usar una clave de inicio almacenada en una unidad flash USB. Si se selecciona esta opción, BitLocker bloquea el proceso de arranque normal hasta que se conecte al equipo un dispositivo USB que contenga una clave de inicio de BitLocker.  

- **TPM y clave de inicio en USB**: seleccione esta opción para usar TPM y una clave de inicio almacenada en una unidad flash USB. Si se selecciona esta opción, BitLocker bloquea el proceso de arranque normal hasta que se conecte al equipo un dispositivo USB que contenga una clave de inicio de BitLocker.  

- **TPM con NIP**: seleccione esta opción para usar TPM y un número de identificación personal (NIP). Si selecciona esta opción, BitLocker bloquea el proceso de arranque normal hasta que el usuario proporcione el PIN.  

Para cifrar una unidad de datos específica, que no es de sistema operativo, seleccione **Unidad específica**. A continuación, seleccione la unidad en la lista.  

#### <a name="use-full-disk-encryption"></a>Usar cifrado de disco completo

<!--SCCMDocs-pr issue 2671-->
De forma predeterminada, este paso solo cifra el espacio utilizado en la unidad. Este comportamiento predeterminado es el recomendado, ya que es más rápido y eficaz. A partir de la versión 1806, si la organización necesita cifrar toda la unidad durante la instalación, habilite esta opción. El programa de instalación de Windows espera a que se cifre toda la unidad, lo que tarda mucho tiempo, especialmente en unidades de gran tamaño.

#### <a name="choose-where-to-create-the-recovery-key"></a>Elegir la ubicación en la que desea crear la clave de recuperación

Para especificar que BitLocker cree la contraseña de recuperación y custodiarla en Active Directory, seleccione **En Active Directory**. Esta opción requiere que extienda Active Directory para la custodia de claves de BitLocker. Después, BitLocker puede guardar la información de recuperación asociada en Active Directory. Seleccione **No crear clave de recuperación** para no crear ninguna contraseña. La opción recomendada es crear una contraseña.  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>Esperar a que BitLocker complete el proceso de cifrado de unidad en todas las unidades antes de continuar con la ejecución de la secuencia de tareas

Seleccione esta opción para permitir que se complete el cifrado de unidad de BitLocker antes de ejecutar el siguiente paso de la secuencia de tareas. Si selecciona esta opción, BitLocker cifra el volumen de todo el disco antes de que el usuario pueda iniciar sesión en el equipo.  

El proceso de cifrado puede tardar horas en completarse cuando se cifra una unidad de disco duro grande. Si no se selecciona esta opción, se permite que la secuencia de tareas continúe inmediatamente.  



## <a name="BKMK_FormatandPartitionDisk"></a> Formatear y crear particiones en el disco  

Use este paso para dar formato y crear particiones en el disco especificado en el equipo de destino.  

> [!IMPORTANT]  
> Cada valor especificado para este paso se aplica a un único disco. Para dar formato y crear particiones en otro disco del equipo de destino, agregue otro paso **Formatear y crear particiones de disco** a la secuencia de tareas.  

Este paso solo se ejecuta en Windows PE, No se ejecuta en el sistema operativo completo.  

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDDiskIndex](/sccm/osd/understand/task-sequence-variables#OSDDiskIndex)  
- [OSDGPTBootDisk](/sccm/osd/understand/task-sequence-variables#OSDGPTBootDisk)  
- [OSDPartitions](/sccm/osd/understand/task-sequence-variables#OSDPartitions)  
- [OSDPartitionStyle](/sccm/osd/understand/task-sequence-variables#OSDPartitionStyle)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Discos** y **Formatear y crear particiones de disco**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="disk-number"></a>Número de disco

El número de disco físico del disco al que se va a dar formato. El número se basa en el orden de enumeración de disco de Windows.  

#### <a name="disk-type"></a>Tipo de disco

El tipo de disco al que dar formato. Hay dos opciones para seleccionar en la lista desplegable:

- **Estándar (MBR)** : registro de arranque maestro  
- **GPT**: tabla de particiones GUID  

> [!NOTE]  
> Si cambia el tipo de disco de **Estándar (MBR)** a **GPT** y el diseño de partición contiene una partición extendida, la secuencia de tareas elimina todas las particiones extendidas y lógicas del diseño. El editor de secuencia de tareas le pide que confirme esta acción antes de cambiar el tipo de disco.  

#### <a name="volume"></a>Volumen

Información específica sobre la partición o volumen que crea la secuencia de tareas, incluidos los atributos siguientes:  

- Nombre  
- Espacio en disco restante  

Para crear una nueva partición, seleccione **Nuevo** y se abrirá el cuadro de diálogo **Propiedades de la partición**. Especifique el tipo de partición y el tamaño, y si es una partición de arranque. Para modificar una partición existente, seleccione la partición que desea modificar y, a continuación, seleccione el botón **Propiedades**. Para más información sobre cómo configurar particiones de disco duro, vea uno de los artículos siguientes:  

- [Particiones de disco duro basadas en UEFI/GPT](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
- [Particiones de disco duro basadas en BIOS/MBR](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  

Para eliminar una partición, elija la partición en cuestión y seleccione **Eliminar**.  



## <a name="BKMK_InstallApplication"></a> Instalar aplicación  

Este paso instala las aplicaciones especificadas, o un conjunto de aplicaciones definido por una lista dinámica de variables de secuencia de tareas. Cuando se ejecuta este paso de la secuencia de tareas, la instalación de aplicaciones se inicia de inmediato sin tener que esperar durante un intervalo de sondeo de directiva.  

Las aplicaciones deben cumplir los criterios siguientes:  

- La aplicación debe ser un tipo de implementación de **Windows Installer** o un instalador de **scripts**. No se admiten los tipos de implementación de paquete de aplicación de Windows (archivo .appx).  

- Debe ejecutarse en la cuenta sistema local y no en la cuenta de usuario.  

- No debe interactuar con el escritorio. El programa debe ejecutarse en modo silencioso o en modo desatendido.  

- No debe iniciarse ni reiniciarse por sí misma. La aplicación debe solicitar un reinicio mediante el código estándar de reinicio: 3010. Este comportamiento garantiza que este paso controla correctamente el reinicio. Si la aplicación devuelve un código de salida 3010, el motor de secuencia de tareas reinicia el equipo. Tras el reinicio, la secuencia de tareas continúa automáticamente.  

> [!Note]
> Si la aplicación [comprueba si hay archivos](/sccm/apps/deploy-use/deploy-applications#bkmk_exe-check)ejecutables en ejecución, la secuencia de tareas no podrá instalarlos. Si no configura este paso para continuar después de un error, se produce un error en la secuencia de tareas completa.

Cuando se ejecuta este paso, la aplicación comprueba la aplicabilidad de las reglas de requisitos y el método de detección en sus tipos de implementación. Según los resultados de esta comprobación, la aplicación instala el tipo de implementación correspondiente. Si un tipo de implementación contiene dependencias, el tipo de implementación dependiente se evalúa y se instala como parte del paso. Las dependencias de aplicación no son compatibles con medios independientes.  

> [!NOTE]  
> Para instalar una aplicación que reemplace a otra, los archivos de contenido de la aplicación sustituida deben estar disponibles. En caso contrario, se producirá un error en este paso de secuencia de tareas. Por ejemplo, Microsoft Visio 2010 se instala en un cliente o en una imagen capturada. Cuando el paso **Instalar aplicación** instala Microsoft Visio 2013, los archivos de contenido de Microsoft Visio 2010 (la aplicación sustituida) deben estar disponibles en un punto de distribución. Si Microsoft Visio no está instalado en un cliente o una imagen capturada, la secuencia de tareas instala Microsoft Visio 2013 sin comprobar los archivos de contenido de Microsoft Visio 2010.  
>
> Si retira una aplicación reemplazada y se hace referencia a la nueva aplicación en una secuencia de tareas, la secuencia de tareas no se inicia.
Este comportamiento es así por diseño: la secuencia de tareas requiere todas las referencias de la aplicación.<!-- SCCMDocs 1711 -->  

Este paso de secuencia de tareas solo se ejecuta en el sistema operativo completo. No se ejecuta en Windows PE.  

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [_TSAppInstallStatus](/sccm/osd/understand/task-sequence-variables#TSAppInstallStatus)  
- [SMSTSMPListRequestTimeoutEnabled](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeout)  
- [TSErrorOnWarning](/sccm/osd/understand/task-sequence-variables#TSErrorOnWarning)  

> [!NOTE]  
> Si el cliente no puede recuperar la lista de puntos de administración de los servicios de ubicación, use las variables de secuencia de tareas **SMSTSMPListRequestTimeoutEnabled** y **SMSTSMPListRequestTimeout**. Estas variables especifican los milisegundos que espera una secuencia de tareas antes de reintentar la instalación de una aplicación. Para más información, vea [Task sequence variables](/sccm/osd/understand/task-sequence-variables) (Variables de secuencia de tareas).

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Software** e **Instalar aplicación**.

Administre este paso con los siguientes cmdlets de PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallapplication?view=sccm-ps)
- [New-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallapplication?view=sccm-ps)
- [Remove-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallapplication?view=sccm-ps)
- [Set-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallapplication?view=sccm-ps)

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="install-the-following-applications"></a>Instalar las aplicaciones siguientes

La secuencia de tareas instala estas aplicaciones en el orden especificado.  

Configuration Manager filtra las aplicaciones deshabilitadas o las que tengan los valores siguientes:  

- Solo cuando un usuario haya iniciado sesión  
- Ejecutar con derechos de usuario  

Estas aplicaciones no aparecen en el cuadro de diálogo **Seleccione la aplicación que desea instalar**.

#### <a name="install-applications-according-to-dynamic-variable-list"></a>Instalar aplicaciones según la lista de variables dinámicas

La secuencia de tareas instala las aplicaciones mediante este nombre variable de base. El nombre variable de base es para un conjunto de variables de secuencia de tareas definidas para una colección o equipo. Estas variables especifican las aplicaciones que la secuencia de tareas instala para esa colección o equipo. Cada nombre de variable consta de su nombre base común además de un sufijo numérico que empieza en 01. El valor de cada variable debe contener el nombre de la aplicación y nada más.  

Para que la secuencia de tareas instale aplicaciones mediante una lista de variables dinámicas, habilite la siguiente configuración en la pestaña **General** de las **Propiedades** de la aplicación: **Permitir que esta aplicación se instale desde la secuencia de tareas de instalación de aplicación en vez de implementarla manualmente**.  

> [!NOTE]  
> No se pueden instalar aplicaciones mediante una lista de variables dinámicas para las implementaciones de medios independientes.  

Por ejemplo, para instalar una aplicación mediante una variable de secuencia de tareas llamada AA01, especifique la siguiente variable:  

|Nombre de variable|Valor de variable|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

Para instalar dos aplicaciones, especifique las siguientes variables:  

|Nombre de variable|Valor de variable|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

Las condiciones siguientes afectan a las aplicaciones instaladas por la secuencia de tareas:  

- Si el valor de una variable contiene alguna información que no sea el nombre de la aplicación, La secuencia de tareas no instala la aplicación y continúa.  

- Si la secuencia de tareas no encuentra una variable con el nombre de base especificado y el sufijo "01", no instala ninguna aplicación.  

> [!Important]  
> Estos valores distinguen entre mayúsculas y minúsculas. Por ejemplo, "instalar" es distinto de "Instalar". Si tiene que cambiar el valor, el editor de secuencia de tareas no detecta los cambios de mayúsculas y minúsculas. Realice otra modificación al mismo tiempo; por ejemplo, modificar la descripción del paso.<!--509714-->

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>Continuar instalando otras aplicaciones en la lista si se produce un error de instalación de aplicación

Esta configuración especifica que el paso continúe cuando se produzca un error en la instalación de una aplicación. Si especifica esta opción, la secuencia de tareas continúa con independencia de los errores de instalación. Si no se especifica esta opción y se produce un error en la instalación, el paso finaliza inmediatamente.  

#### <a name="clear-application-content-from-cache-after-installing"></a>Borrar el contenido de la aplicación de la memoria caché después de instalar

<!--4485675-->
A partir de la versión 1906, elimine el contenido de la aplicación de la memoria caché del cliente después de que se ejecute el paso. Este comportamiento es beneficioso en dispositivos con unidades de disco duro pequeñas o cuando se instala una gran cantidad de aplicaciones de gran tamaño de forma sucesiva.


### <a name="options"></a>Opciones

> [!NOTE]  
> Si selecciona **Continuar después de un error** en la pestaña **Opciones** de este paso, la secuencia de tareas continúa cuando no se puede instalar una aplicación. Cuando no se habilita esta opción, se produce un error en la secuencia de tareas y no instala las aplicaciones restantes.  

Además de las opciones predeterminadas, configure las siguientes opciones adicionales en la pestaña **Opciones** de este paso de secuencia de tareas:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Volver a intentar este paso si el equipo se reinicia inesperadamente

Si una de las instalaciones de aplicaciones reinicia inesperadamente el equipo, vuelva a intentar este paso. El paso habilita esta configuración de forma predeterminada con dos reintentos. Puede especificar de uno a cinco reintentos.  



## <a name="BKMK_InstallPackage"></a> Instalar paquete

Use este paso para instalar un paquete de software como parte de la secuencia de tareas. Cuando se ejecuta este paso, la instalación se inicia de inmediato sin tener que esperar durante un intervalo de sondeo de directiva.  

El paquete debe cumplir los criterios siguientes:  

- Debe ejecutarse en la cuenta de sistema local y no en una cuenta de usuario.  

- No debe interactuar con el escritorio. El programa debe ejecutarse en modo silencioso o en modo desatendido.  

- No debe iniciarse ni reiniciarse por sí misma. El software debe solicitar un reinicio mediante el código estándar de reinicio: 3010. Este comportamiento garantiza que la secuencia de tareas controla correctamente el reinicio. Si el software devuelve un código de salida 3010, el motor de secuencia de tareas reinicia el equipo. Tras el reinicio, la secuencia de tareas continúa automáticamente.  

Los programas que usan la opción **Ejecutar otro programa primero** para instalar un programa dependiente no se admiten al implementar un sistema operativo. Si habilita la opción de paquete **Ejecutar otro programa primero** y el programa dependiente ya se ha ejecutado en el equipo de destino, se ejecuta el programa dependiente y la secuencia de tareas continúa. Pero si el programa dependiente todavía no se ha ejecutado en el equipo de destino, se produce un error en el paso de secuencia de tareas.  

> [!NOTE]  
> El sitio de administración central no tiene las directivas de configuración de cliente necesarias para habilitar el agente de distribución de software durante la secuencia de tareas. Cuando se crea el medio independiente para una secuencia de tareas en el sitio de administración central, y la secuencia de tareas incluye un paso **Instalar paquete** , es posible que aparezca el siguiente error en el archivo CreateTsMedia.log:  
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>
> Para los medios independientes que incluyan un paso **Instalar paquete**, cree los medios independientes en un sitio primario que tenga habilitado el agente de distribución de software. O bien, agregue un paso **Ejecutar línea de comandos** después del paso **Instalar Windows y Configuration Manager** y antes del primer paso **Instalar paquete**. El paso **Ejecutar línea de comandos** ejecuta un comando de WMIC para habilitar el agente de distribución de software antes del primer paso **Instalar paquete**. Use el comando siguiente en el paso **Ejecutar línea de comandos**:  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>
> Para obtener información sobre cómo crear medios independientes, consulte [Crear medios independientes](/sccm/osd/deploy-use/create-stand-alone-media).  

Este paso de secuencia de tareas solo se ejecuta en el sistema operativo completo. No se ejecuta en Windows PE.  

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDDoNotLogCommand](/sccm/osd/understand/task-sequence-variables#OSDDoNotLogCommand) (a partir de la versión 1806)<!--1358493-->  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Software** e **Instalar paquete**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="install-a-single-software-package"></a>Instalar un solo paquete de software

Esta configuración especifica un paquete de software de Configuration Manager. El paso espera hasta que finalice la instalación.  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>Instalar paquetes de software según la lista de variables dinámicas

La secuencia de tareas instala los paquetes mediante este nombre variable de base. El nombre variable de base es para un conjunto de variables de secuencia de tareas definidas para una colección o equipo. Estas variables especifican los paquetes que la secuencia de tareas instala para esa colección o equipo. Cada nombre de variable consta de su nombre base común además de un sufijo numérico que empieza en 001. El valor de cada variable debe contener un identificador de paquete y el nombre del software separado por dos puntos.  

Para que la secuencia de tareas instale software mediante una lista de variables dinámicas, habilite la opción **Permitir que este programa se instale desde la secuencia de tareas de instalación de paquete sin implementarse** en la pestaña **Avanzadas** de las **Propiedades** del paquete.  

> [!NOTE]  
> No se pueden instalar paquetes de software mediante una lista de variables dinámicas para las implementaciones de medios independientes.  

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

- Si no crea el valor de una variable en el formato correcto o no se especifica un identificador y nombre de paquete válidos, se produce un error en la instalación del software.  

- Si el identificador de paquete contiene caracteres en minúsculas, se produce un error en la instalación de software.  

- Si la secuencia de tareas no encuentra una variable con el nombre de base especificado y el sufijo "001", no instala ningún paquete. La secuencia de tareas continúa.  

> [!Important]  
> Estos valores distinguen entre mayúsculas y minúsculas. Por ejemplo, "instalar" es distinto de "Instalar". Si tiene que cambiar el valor, el editor de secuencia de tareas no detecta los cambios de mayúsculas y minúsculas. Realice otra modificación al mismo tiempo; por ejemplo, modificar la descripción del paso.<!--509714-->

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>Continuar instalando otros paquetes en la lista si se produce un error de instalación de un paquete de software

Esta configuración especifica que el paso continúa si se produce un error la instalación de un paquete de software. Si especifica esta opción, la secuencia de tareas continúa con independencia de los errores de instalación. Si no se especifica esta opción y se produce un error en la instalación, el paso finaliza inmediatamente.  



## <a name="BKMK_InstallSoftwareUpdates"></a> Instalar actualizaciones de software  

Use este paso para instalar actualizaciones de software en el equipo de destino. No se evalúa si hay actualizaciones de software aplicables al equipo de destino hasta que se ejecuta este paso de secuencia de tareas. En ese momento, se evalúa si existen actualizaciones de software para el equipo de destino igual que para cualquier otro cliente de Configuration Manager. Para que este paso instale las actualizaciones de software, primero impleméntelas en una recopilación de la que el equipo de destino sea miembro.  

> [!IMPORTANT]  
> Para obtener el mejor rendimiento, instale la versión más reciente del agente de Windows Update.  

Este paso de secuencia de tareas solo se ejecuta en el sistema operativo completo. No se ejecuta en Windows PE.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [SMSInstallUpdateTarget](/sccm/osd/understand/task-sequence-variables#SMSInstallUpdateTarget)  
- [SMSTSMPListRequestTimeoutEnabled](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeout)  
- [SMSTSSoftwareUpdateScanTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout)  
- [SMSTSWaitForSecondReboot](/sccm/osd/understand/task-sequence-variables#SMSTSWaitForSecondReboot)  

> [!NOTE]  
> Si el cliente no puede recuperar la lista de puntos de administración de servicios de ubicación, use las variables **SMSTSMPListRequestTimeoutEnabled** y **SMSTSMPListRequestTimeout**. Estas variables especifican la cantidad de milisegundos que espera una secuencia de tareas antes de reintentar la instalación de una aplicación o actualización de software. Para más información, vea [Task sequence variables](/sccm/osd/understand/task-sequence-variables) (Variables de secuencia de tareas).  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Software** e **Instalar actualizaciones de software**.

Para obtener más recomendaciones y un diagrama técnico de diagrama de flujo para este paso, consulte [Instalar actualizaciones de software](/sccm/osd/understand/install-software-updates).

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>Necesario para la instalación: solo actualizaciones de software obligatorias

Seleccione esta opción para instalar todas las actualizaciones de software obligatorias con fechas límite de instalación definidas por el administrador.  

#### <a name="available-for-installation---all-software-updates"></a>Disponible para la instalación: todas las actualizaciones de software

Seleccione esta opción para instalar todas las actualizaciones de software disponibles. Primero implemente estas actualizaciones en una recopilación de la que el equipo sea miembro. La secuencia de tareas instala todas las actualizaciones de software disponibles en los equipos de destino.  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>Evaluación de las actualizaciones de software a partir de los resultados del análisis en caché

De forma predeterminada, este paso utiliza los resultados del análisis en caché de Windows Update Agent. Desactive esta opción para indicar al agente de Windows Update que descargue el catálogo más reciente del punto de actualización de software. Habilite esta opción cuando se use una secuencia de tareas para [capturar y crear una imagen de sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system). En este escenario es probable que haya un gran número de actualizaciones de software.

Muchas de estas actualizaciones tienen dependencias. Por ejemplo, instale la actualización ABC antes que la actualización XYZ aparezca como aplicable. Al desactivar esta opción e implementar la secuencia de tareas en un muchos clientes, todos se conectan al punto de actualización de software al mismo tiempo. Este comportamiento produce problemas de rendimiento durante el proceso y la descarga del catálogo de actualizaciones.

En la mayoría de circunstancias, use la configuración predeterminada para usar los resultados del análisis almacenados en caché.

La variable **SMSTSSoftwareUpdateScanTimeout** controla el tiempo de espera del análisis de actualizaciones de software durante este paso. El valor predeterminado es 30 minutos. Para más información, vea [Task sequence variables](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout) (Variables de secuencia de tareas).

### <a name="options"></a>Opciones  

Además de las opciones predeterminadas, configure las siguientes opciones adicionales en la pestaña **Opciones** de este paso de secuencia de tareas:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Volver a intentar este paso si el equipo se reinicia inesperadamente

Si una de las actualizaciones reinicia inesperadamente el equipo, vuelva a intentar este paso. El paso habilita esta configuración de forma predeterminada con dos reintentos. Puede especificar de uno a cinco reintentos.  

> [!NOTE]  
> Configure la variable **SMSTSWaitForSecondReboot** para especificar cuántos segundos se pausa la secuencia de tareas después de reiniciar el equipo en este escenario. Para más información, vea [Task sequence variables](/sccm/osd/understand/task-sequence-variables#SMSTSWaitForSecondReboot) (Variables de secuencia de tareas).  



## <a name="BKMK_JoinDomainorWorkgroup"></a> Unirse a dominio o grupo de trabajo  

Use este paso para agregar el equipo de destino a un grupo de trabajo o dominio.  

Este paso de secuencia de tareas solo se ejecuta en el sistema operativo completo. No se ejecuta en Windows PE.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDJoinAccount](/sccm/osd/understand/task-sequence-variables#OSDJoinAccount)  
- [OSDJoinDomainName](/sccm/osd/understand/task-sequence-variables#OSDJoinDomainName)  
- [OSDJoinDomainOUName](/sccm/osd/understand/task-sequence-variables#OSDJoinDomainOUName)  
- [OSDJoinPassword](/sccm/osd/understand/task-sequence-variables#OSDJoinPassword)  
- [OSDJoinSkipReboot](/sccm/osd/understand/task-sequence-variables#OSDJoinSkipReboot)  
- [OSDJoinType](/sccm/osd/understand/task-sequence-variables#OSDJoinType)  
- [OSDJoinWorkgroupName](/sccm/osd/understand/task-sequence-variables#OSDJoinWorkgroupName)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **General** y **Unirse a dominio o grupo de trabajo**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="join-a-workgroup"></a>Unirse a un grupo de trabajo

Seleccione esta opción para que el equipo de destino se una al grupo de trabajo especificado. Si el equipo pertenece actualmente a un dominio, la selección de esta opción hace que el equipo se reinicie.  

#### <a name="join-a-domain"></a>Unirse a un dominio

Seleccione esta opción para que el equipo de destino se una al dominio especificado.  

Si lo desea, escriba o busque una unidad organizativa (OU) en el dominio especificado para que se una el equipo. Si el equipo pertenece actualmente a otro dominio o grupo de trabajo, esta opción hace que el equipo se reinicie. Si el equipo ya pertenece a otra unidad organizativa, como Active Directory Domain Services no permite cambiar la unidad organizativa a través de este método, el programa de instalación de Windows ignora esta configuración.  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>Especifique la cuenta que tiene permiso para unirse al dominio

Seleccione **Establecer** para escribir el nombre de usuario y la contraseña de una cuenta con permisos para unirse al dominio. Escriba la cuenta en el formato: `Domain\account`. Para obtener más información sobre la cuenta de unión a dominio de la secuencia de tareas, consulte [Cuentas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-domain-join-account).  



## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> Preparar el cliente de Configuration Manager para la captura  

Use este paso para quitar o configurar al cliente de Configuration Manager en el equipo de referencia. Esta acción prepara el equipo para la captura como parte del proceso de creación de imágenes.

Este paso quita por completo el cliente de Configuration Manager en lugar de quitar solo la información de clave. Cuando la secuencia de tareas implementa la imagen de sistema operativo capturada, instala un cliente nuevo de Configuration Manager cada vez.  

> [!Note]  
> El motor de secuencia de tareas solo quita el cliente durante la secuencia de tareas **Generar y capturar una imagen de sistema operativo de referencia**. El motor de secuencia de tareas no quita al cliente durante otros métodos de captura, como medios de captura o una secuencia de tareas personalizada.  

Este paso de secuencia de tareas solo se ejecuta en el sistema operativo completo. No se ejecuta en Windows PE.  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Imágenes** y **Preparar el cliente de Configuration Manager para la captura**.

### <a name="properties"></a>Propiedades  

Este paso no requiere ninguna configuración en la pestaña **Propiedades**.



## <a name="BKMK_PrepareWindowsforCapture"></a> Prepare Windows for Capture  

Use este paso para especificar las opciones de Sysprep al capturar una imagen de sistema operativo en el equipo de referencia. Este paso ejecuta Sysprep y, a continuación, reinicia el equipo en la imagen de arranque de Windows PE especificada para la secuencia de tareas. Se produce un error en esta acción si el equipo de referencia está unido a un dominio.  

Este paso solo se ejecuta en el sistema operativo completo. No se ejecuta en Windows PE.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDKeepActivation](/sccm/osd/understand/task-sequence-variables#OSDKeepActivation)  
- [OSDTargetSystemRoot](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemRoot-output)  

Para agregar este paso en el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **Imágenes** y seleccione **Preparar Windows para la captura**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="automatically-build-mass-storage-driver-list"></a>Generar automáticamente lista de controladores almacenamiento masivo

Seleccione esta opción para que Sysprep genere automáticamente una lista de controladores de almacenamiento del equipo de referencia. Esta opción habilita la opción de compilar controladores de almacenamiento en el archivo sysprep.inf en el equipo de referencia. Para más información sobre esta configuración, vea la documentación de Sysprep.  

#### <a name="do-not-reset-activation-flag"></a>No restablecer la marca de activación

Seleccione esta opción para impedir que Sysprep restablezca la marca de activación de producto.  

#### <a name="shutdown-the-computer-after-running-this-action"></a>Apagar el equipo después de ejecutar esta acción

<!--SCCMDocs-pr issue 2695-->
A partir de la versión 1806, esta opción indica a Sysprep que apague el equipo en lugar de su comportamiento de reinicio predeterminado.

A partir de la versión 1810, este paso se usa en la secuencia de tareas [Windows Autopilot para dispositivos existentes](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices).

- Si desea que la secuencia de tareas actualice el dispositivo y, a continuación, inicie inmediatamente OOBE de Autopilot, deje esta opción desactivada.  

- Habilite esta opción para apagar el dispositivo después de la creación de imágenes. A continuación, puede entregar el dispositivo a un usuario, que inicia OOBE con Autopilot cuando se enciende por primera vez.  



## <a name="BKMK_PreProvisionBitLocker"></a> Tener en servicio BitLocker  

Use este paso para habilitar BitLocker en una unidad cuando se usa Windows PE. De manera predeterminada, solo se cifra el espacio de la unidad que se utiliza, por ello los tiempos de cifrado son mucho más rápidos. Las opciones de administración de claves se aplican mediante el paso [Habilitar BitLocker](#BKMK_EnableBitLocker) después de que se instale el sistema operativo.

Este paso solo se ejecuta en Windows PE, No se ejecuta en el sistema operativo completo.  

> [!IMPORTANT]  
> Para tener en servicio BitLocker se requiere al menos Windows 7. El equipo también debe contener un Módulo de plataforma segura (TPM) compatible y habilitado.  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Discos** y **Tener en servicio BitLocker**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>Aplicar BitLocker a la unidad especificada

Especifique la unidad para la que desea habilitar BitLocker. BitLocker solo cifra el espacio usado en la unidad.  

#### <a name="use-full-disk-encryption"></a>Usar cifrado de disco completo

<!--SCCMDocs-pr issue 2671-->
De forma predeterminada, este paso solo cifra el espacio utilizado en la unidad. Este comportamiento predeterminado es el recomendado, ya que es más rápido y eficaz. A partir de la versión 1806, si la organización necesita cifrar toda la unidad durante la instalación, habilite esta opción. El programa de instalación de Windows espera a que se cifre toda la unidad, lo que tarda mucho tiempo, especialmente en unidades de gran tamaño.

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>Omitir este paso para equipos que no tengan TPM o cuando TPM no esté habilitado

Seleccione esta opción para omitir el cifrado de unidad en un equipo que no contenga un TPM compatible o habilitado. Por ejemplo, use esta opción al implementar un sistema operativo en una máquina virtual.  



## <a name="BKMK_ReleaseStateStore"></a> Liberar almacén de estado  

Use este paso para notificar al punto de migración de estado que la acción de captura o restauración se completó. Use este paso junto con los pasos **Solicitar almacén de estado**, **Capturar estado de usuario** y **Restaurar estado de usuario**. Estos pasos se usan para migrar datos de estado de usuario mediante un punto de migración de estado y la herramienta de migración de estado de usuario (USMT).  

Para obtener más información sobre cómo administrar el estado de usuario al implementar sistemas operativos, consulte [Administrar el estado de usuario](/sccm/osd/get-started/manage-user-state).  

Si usa el paso **Solicitar almacén de estado** para solicitar acceso a un punto de migración de estado para *capturar* el estado de usuario, este paso notifica al punto de migración de estado que el proceso de captura ha finalizado. Después, el punto de migración de estado marca los datos de estado de usuario como disponibles para la restauración. El punto de migración de estado establece los permisos de control de acceso para los datos de estado de usuario de modo que el equipo de la restauración tenga acceso de solo lectura.  

Si usa el paso **Solicitar almacén de estado** para solicitar acceso a un punto de migración de estado para *restaurar* el estado de usuario, este paso notifica al punto de migración de estado que el proceso de restauración ha finalizado. Después, el punto de migración de estado activa su configuración de retención de datos.  

> [!IMPORTANT]  
> Establezca la opción **Continuar después de un error** para todos los pasos entre **Solicitar almacén de estado** y **Liberar almacén de estado**. Cada paso **Solicitar almacén de estado** debe tener su correspondiente paso **Liberar almacén de estado**.  

Este paso solo se ejecuta en el sistema operativo completo. No se ejecuta en Windows PE.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Estado de usuario** y **Liberar almacén de estado**.

### <a name="properties"></a>Propiedades  

Este paso no requiere ninguna configuración en la pestaña **Propiedades**.



## <a name="BKMK_RequestStateStore"></a> Solicitar almacén de estado  

Use este paso para solicitar acceso a un punto de migración de estado al capturar o restaurar el estado.  

Para obtener más información sobre cómo administrar el estado de usuario al implementar sistemas operativos, consulte [Administrar el estado de usuario](/sccm/osd/get-started/manage-user-state).  

Use este paso junto con los pasos **Liberar almacén de estado**, **Capturar estado de usuario** y **Restaurar estado de usuario**. Estos pasos se usan para migrar el estado del equipo mediante un punto de migración de estado y la herramienta de migración de estado de usuario (USMT).  

> [!NOTE]  
> Al crear un nuevo punto de migración de estado, el almacenamiento de estado de usuario puede tardar hasta una hora en estar disponible. Para acelerar la disponibilidad, ajuste cualquier valor de propiedad del punto de migración de estado para desencadenar una actualización del archivo de control de sitio.  

Este paso se ejecuta en el sistema operativo completo y en Windows PE para USMT sin conexión.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDStateFallbackToNAA](/sccm/osd/understand/task-sequence-variables#OSDStateFallbackToNAA)  
- [OSDStateSMPRetryCount](/sccm/osd/understand/task-sequence-variables#OSDStateSMPRetryCount)  
- [OSDStateSMPRetryTime](/sccm/osd/understand/task-sequence-variables#OSDStateSMPRetryTime)  
- [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Estado de usuario** y **Solicitar almacén de estado**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="capture-state-from-the-computer"></a>Capturar estado del equipo

Busque un punto de migración de estado que cumpla los requisitos mínimos definidos en la configuración de punto de migración de estado. Por ejemplo, **Número máximo de clientes** y **Cantidad mínima de espacio libre en disco**. Esta opción no garantiza que haya espacio suficiente disponible en el momento de la migración de estado. Esta opción solicita acceso al punto de migración de estado con el fin de capturar el estado de usuario y la configuración de un equipo.  

Si el sitio de Configuration Manager tiene varios puntos de migración de estado activo, este paso busca un punto de migración de estado con espacio en disco disponible. La secuencia de tareas consulta el punto de administración para obtener una lista de puntos de migración de estado y, después, los evalúa hasta encontrar uno que cumpla los requisitos mínimos.  

#### <a name="restore-state-from-another-computer"></a>Restaurar estado de otro equipo

Solicite acceso a un punto de migración de estado para restaurar la configuración y el estado de usuario capturados anteriormente en un equipo de destino.  

Si hay varios puntos de migración de estado, este paso busca el punto de migración de estado que tenga el estado para el equipo de destino.  

#### <a name="number-of-retries"></a>Número de reintentos

El número de veces que este paso intenta encontrar un punto de migración de estado adecuado antes de que se produzca un error.  

#### <a name="retry-delay-in-seconds"></a>Intervalo entre reintentos (en segundos)

Cantidad de tiempo en segundos que el paso de secuencia de tareas espera entre reintentos.  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>Use la cuenta de acceso de red si la cuenta de equipo no puede conectarse a un almacén de estado.

Si la secuencia de tareas no puede tener acceso al punto de migración de estado mediante la cuenta de equipo, usa las credenciales de la cuenta de acceso a la red para conectarse. Esta opción es menos segura porque otros equipos podrían usar la cuenta de acceso a la red para obtener acceso al estado almacenado. Es posible que esta opción sea necesaria si el equipo de destino no está unido al dominio.  



## <a name="BKMK_RestartComputer"></a> Reiniciar equipo  

Use este paso para reiniciar el equipo que ejecuta la secuencia de tareas. Después del reinicio, el equipo continúa automáticamente con el siguiente paso de la secuencia de tareas.  

Este paso se puede ejecutar en el sistema operativo completo o Windows PE.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [SMSRebootMessage](/sccm/osd/understand/task-sequence-variables#SMSRebootMessage)  
- [SMSRebootTimeout](/sccm/osd/understand/task-sequence-variables#SMSRebootTimeout)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **General** y **Reiniciar equipo**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>La imagen de arranque asignada a esta secuencia de tareas

Seleccione esta opción para que el equipo de destino use la imagen de arranque asignada a la secuencia de tareas. La secuencia de tareas usa la imagen de arranque para ejecutar pasos posteriores en Windows PE.  

#### <a name="the-currently-installed-default-operating-system"></a>El sistema operativo predeterminado instalado actualmente

Seleccione esta opción para que el equipo de destino se reinicie en el sistema operativo instalado.  

#### <a name="notify-the-user-before-restarting"></a>Informar al usuario antes de reiniciar

Seleccione esta opción para mostrar una notificación al usuario antes de que se reinicie el equipo de destino. El paso selecciona esta opción de forma predeterminada.  

#### <a name="notification-message"></a>Mensaje de notificación

Escriba un mensaje de notificación para mostrar al usuario antes de que se reinicie el equipo de destino.  

#### <a name="message-display-time-out"></a>Tiempo de espera de visualización de mensaje

Especifique la cantidad de tiempo en segundos antes de que se reinicie el equipo de destino. El valor predeterminado es 60 segundos.  



## <a name="BKMK_RestoreUserState"></a> Restaurar estado de usuario  

Use este paso para iniciar la herramienta de migración de estado de usuario (USMT) para restaurar el estado de usuario y la configuración en un equipo de destino. Use este paso junto con el paso **Capturar estado de usuario**.  

Para obtener más información sobre cómo administrar el estado de usuario al implementar sistemas operativos, consulte [Administrar el estado de usuario](/sccm/osd/get-started/manage-user-state).  

Use este paso con los pasos **Solicitar almacén de estado** y **Liberar almacén de estado** para guardar o restaurar la configuración de estado con un punto de migración de estado. Esta opción siempre descifra el almacén de estado de USMT mediante una clave de cifrado generada y administrada por Configuration Manager.  

El paso **Restaurar estado de usuario** proporciona control sobre un subconjunto limitado de las opciones de USMT más usadas. Especifique más opciones de línea de comandos con la variable **OSDMigrateAdditionalRestoreOptions**.  

> [!IMPORTANT]  
> Si usa este paso con una finalidad no relacionada con un escenario de implementación de sistema operativo, agregue el paso [Reiniciar equipo](#BKMK_RestartComputer) inmediatamente después del paso **Restaurar estado de usuario**.  

Este paso solo se ejecuta en el sistema operativo completo. No se ejecuta en Windows PE.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [_OSDMigrateUsmtRestorePackageID](/sccm/osd/understand/task-sequence-variables#OSDMigrateUsmtRestorePackageID)  
- [OSDMigrateAdditionalRestoreOptions](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdditionalRestoreOptions)  
- [OSDMigrateContinueOnRestore](/sccm/osd/understand/task-sequence-variables#OSDMigrateContinueOnRestore)  
- [OSDMigrateEnableVerboseLogging](/sccm/osd/understand/task-sequence-variables#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateLocalAccounts](/sccm/osd/understand/task-sequence-variables#OSDMigrateLocalAccounts)  
- [OSDMigrateLocalAccountPassword](/sccm/osd/understand/task-sequence-variables#OSDMigrateLocalAccountPassword)  
- [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Estado de usuario** y **Restaurar estado de usuario**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="user-state-migration-tool-package"></a>Paquete de herramientas de migración de estado de usuario

Especifique el paquete que contiene la versión de USMT que se va a usar en este paso. Este paquete no requiere un programa. Cuando se ejecuta el paso, la secuencia de tareas usa la versión de USMT en el paquete especificado. Especifique un paquete que contenga la versión de 32 o 64 bits de USMT. La arquitectura de USMT depende de la arquitectura del sistema operativo en el que la secuencia de tareas restaura el estado.

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>Restaurar todos los perfiles de usuario capturados con opciones estándar

Restaura los perfiles de usuario capturados con las opciones estándar. Para personalizar las opciones que USMT restaura, seleccione **Personalizar captura de perfil de usuario**.  

#### <a name="customize-how-user-profiles-are-restored"></a>Personalizar la restauración de perfiles de usuario

Le permite personalizar los archivos que desea restaurar en el equipo de destino. Seleccione **Archivos** para especificar los archivos de configuración en el paquete de USMT que desea usar para restaurar los perfiles de usuario. Para agregar un archivo de configuración, escriba el nombre del archivo en el cuadro **Nombre de archivo** y, a continuación, seleccione **Agregar**. En el panel Archivos se enumeran los archivos de configuración que usa USMT. El archivo .xml que especifique define el archivo de usuario que USMT restaura.  

#### <a name="restore-local-computer-user-profiles"></a>Restaurar perfiles de usuario de equipo local

Restaura los perfiles de usuario de equipo local. Estos perfiles no son para los usuarios del dominio. Asigne contraseñas nuevas a las cuentas de usuario local restauradas. USMT no puede migrar las contraseñas originales. Escriba la nueva contraseña en el cuadro **Contraseña** y confirme la contraseña en el cuadro **Confirmar contraseña** .  

#### <a name="continue-if-some-files-cannot-be-restored"></a>Continuar si algunos archivos no se pueden restaurar

Continúa restaurando la configuración y el estado de usuario incluso si USMT no puede restaurar algunos archivos. El paso habilita esta opción de forma predeterminada. Si deshabilita esta opción y USMT detecta errores durante la restauración de archivos, se produce un error inmediatamente en este paso. USMT no restaura todos los archivos.

#### <a name="enable-verbose-logging"></a>Habilitar el registro detallado

Habilite esta opción para generar información más detallada en el archivo de registro. Al restaurar el estado, la secuencia de tareas genera de forma predeterminada **Loadstate.log** en la carpeta de registro de secuencia de tareas, `%WinDir%\ccm\logs`.  



## <a name="BKMK_RunCommandLine"></a> Ejecutar línea de comandos  

Use este paso para ejecutar la línea de comandos especificada.  

Este paso se puede ejecutar en el sistema operativo completo o Windows PE.

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDDoNotLogCommand](/sccm/osd/understand/task-sequence-variables#OSDDoNotLogCommand) (a partir de la versión 1902)<!--3654172-->  
- [SMSTSDisableWow64Redirection](/sccm/osd/understand/task-sequence-variables#SMSTSDisableWow64Redirection)  
- [SMSTSRunCommandLineUserName](/sccm/osd/understand/task-sequence-variables#SMSTSRunCommandLineUserName)  
- [SMSTSRunCommandLinePassword](/sccm/osd/understand/task-sequence-variables#SMSTSRunCommandLinePassword)  
- [WorkingDirectory](/sccm/osd/understand/task-sequence-variables#WorkingDirectory)  

Para agregar este paso en el editor de secuencia de tareas,seleccione **Agregar**, **General** y **Ejecutar línea de comandos**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="command-line"></a>Línea de comandos

Especifica la línea de comandos que ejecuta la secuencia de tareas. Este campo es obligatorio. Incluye extensiones de nombre de archivo, por ejemplo, .vbs y .exe. Incluya todos los archivos de configuración o las opciones de línea de comandos que sean necesarios.  

Si no especifica una extensión de nombre de archivo, Configuration Manager prueba con .com, .exe y .bat. Si el nombre de archivo tiene una extensión que no es un tipo ejecutable, Configuration Manager intenta aplicar una asociación local. Por ejemplo, si la línea de comandos es readme.gif, Configuration Manager inicia la aplicación especificada en el equipo de destino para abrir archivos .gif.  

Ejemplo:  

`setup.exe /a`  

`cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
> Para que se ejecute correctamente, coloque el comando **cmd.exe /c** delante de las acciones de línea de comandos. Ejemplos de estas acciones son los comandos de redirección de salida, canalización y copia.  

#### <a name="disable-64-bit-file-system-redirection"></a>Deshabilitar la redirección de sistema de archivos de 64 bits

En los sistemas operativos de 64 bits se usa el redirector del sistema de archivos WOW64 de forma predeterminada para ejecutar líneas de comandos. Este comportamiento es para encontrar correctamente las versiones de 32 bits de archivos ejecutables y bibliotecas del sistema operativo. Seleccione esta opción para deshabilitar el uso del redirector del sistema de archivos WOW64. Windows ejecuta el comando con las versiones nativas de 64 bits de los archivos ejecutables y las bibliotecas del sistema operativo. Esta opción no tiene ningún efecto cuando se ejecuta en un sistema operativo de 32 bits.  

#### <a name="start-in"></a>Iniciar en

Especifica la carpeta ejecutable para el programa, con un máximo de 127 caracteres. Esta carpeta puede ser una ruta de acceso absoluta en el equipo de destino, o una ruta de acceso relacionada con la carpeta del punto de distribución que contiene el paquete. Este campo es opcional.  

Ejemplo:  

`c:\officexp`  

`i386`  

> [!NOTE]  
> El botón **Examinar** busca los archivos y carpetas en el equipo local. Todo lo que seleccione también debe existir en el equipo de destino. Debe existir en la misma ubicación y con los mismos nombres de archivo y carpeta.  

#### <a name="package"></a>Paquete

Al especificar en la línea de comandos archivos o programas que aún no están presentes en el equipo de destino, seleccione esta opción para especificar el paquete de Configuration Manager que contiene los archivos necesarios. El paquete no requiere un programa. Esta opción no es necesaria si los archivos especificados existen en el equipo de destino.  

#### <a name="time-out"></a>Tiempo de espera

Especifica un valor que representa el tiempo que Configuration Manager permite la ejecución de la línea de comandos. Este valor puede estar comprendido entre 1 minuto y 999 minutos. El valor predeterminado es 15 minutos. Esta opción está deshabilitada de forma predeterminada.  

> [!IMPORTANT]  
> Si escribe un valor que no permita tiempo suficiente para que se complete correctamente el comando especificado, se produce un error en este paso. Podría producirse un error en la secuencia de tareas completa en función de las condiciones del paso o el grupo. Si se agota el tiempo de espera, Configuration Manager finaliza el proceso de línea de comandos.  

#### <a name="run-this-step-as-the-following-account"></a>Ejecutar esta etapa como la cuenta siguiente

Especifica que la línea de comandos se ejecuta como una cuenta de usuario de Windows diferente de la cuenta de sistema local.  

> [!NOTE]  
> Para ejecutar comandos o scripts sencillos con otra cuenta después de instalar el sistema operativo, primero agregue la cuenta al equipo. Además, quizá tenga que restaurar los perfiles de usuario de Windows para ejecutar programas más complejos, como Windows Installer.  

#### <a name="account"></a>Cuenta

Especifica la cuenta de usuario de Windows que se usa en este paso para ejecutar la línea de comandos. La línea de comandos se ejecuta con los permisos de la cuenta especificada. Seleccione **Establecer** para especificar la cuenta de usuario o dominio local. Para obtener más información sobre la cuenta de "ejecutar como" de la secuencia de tareas, consulte [Cuentas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account).

> [!IMPORTANT]  
> Si este paso especifica una cuenta de usuario y se ejecuta en Windows PE, se produce un error en la acción. No se puede unir Windows PE a un dominio. El archivo **smsts.log** registra este error.  

### <a name="options"></a>Opciones  

Además de las opciones predeterminadas, configure las siguientes opciones adicionales en la pestaña **Opciones** de este paso de secuencia de tareas:  

#### <a name="success-codes"></a>Códigos de éxito

Incluya otros códigos de salida del script que el paso debería valorar como correctos.



## <a name="BKMK_RunPowerShellScript"></a> Ejecutar script de PowerShell  

Use este paso para ejecutar el script de Windows PowerShell especificado.  

Este paso se puede ejecutar en el sistema operativo completo o Windows PE. Para ejecutar este paso en Windows PE, habilite PowerShell en la imagen de arranque. Habilite el componente WinPE-PowerShell desde la pestaña **Componentes opcionales** de las propiedades de la imagen de arranque. Para obtener más información sobre cómo modificar una imagen de arranque, consulte [Administrar imágenes de arranque](/sccm/osd/get-started/manage-boot-images).  

> [!NOTE]  
> PowerShell no está habilitado de forma predeterminada en los sistemas operativos Windows Embedded.  

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [OSDLogPowerShellParameters](/sccm/osd/understand/task-sequence-variables#OSDLogPowerShellParameters) (a partir de la versión 1902)<!--3556028-->  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **General** y **Ejecutar Script PowerShell**.

> [!Note]  
> Use scripts de PowerShell firmados en formato Unicode. El formato ANSI, que es el predeterminado, no funciona con este paso.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="package"></a>Paquete

Especifique el paquete de Configuration Manager que contiene el script de PowerShell. Un paquete puede contener varios scripts de PowerShell.  

#### <a name="script-name"></a>Nombre de script

Especifica el nombre del script de PowerShell que se va a ejecutar. Este campo es obligatorio.  

#### <a name="enter-a-powershell-script"></a>Especificar un script de PowerShell

<!-- 3556028 -->
A partir de la versión 1902, puede escribir directamente código de Windows PowerShell en este paso. Esta característica permite ejecutar comandos de PowerShell durante una secuencia de tareas sin necesidad de crear y distribuir primero un paquete con el script.

Al agregar o editar un script, la ventana de scripts de PowerShell proporciona las siguientes acciones:  

- Editar el script directamente  

- Abrir un script existente desde un archivo  

- Ir a un [script](/sccm/apps/deploy-use/create-deploy-scripts) aprobado existente en Configuration Manager

> [!Important]  
> Para aprovechar esta nueva característica de Configuration Manager, después de actualizar el sitio, actualice también los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.

#### <a name="parameters"></a>Parámetros

Especifica los parámetros que se pasan al script de PowerShell. Estos parámetros son los mismos que los parámetros de script de PowerShell en la línea de comandos.  

Proporcione parámetros usados por el script, no por la línea de comandos de Windows PowerShell.  
El ejemplo siguiente contiene parámetros válidos:  

`-MyParameter1 MyValue1 -MyParameter2 MyValue2`  

El ejemplo siguiente contiene parámetros no válidos. Los dos primeros elementos son parámetros de línea de comandos de Windows PowerShell ( **-NoLogo** y **-ExecutionPolicy Unrestricted**). El script no consume estos parámetros.  

`-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`

<!-- SCCMDocs-pr issue 3561 -->
Si un valor de parámetro incluye un carácter especial, use comillas simples (`'`) alrededor del valor. El uso de comillas dobles (`"`) puede hacer que el paso de la secuencia de tareas procese el parámetro de manera incorrecta.

Por ejemplo: `-Arg1 '%TSVar1%' -Arg2 '%TSVar2%'`

#### <a name="powershell-execution-policy"></a>Directiva de ejecución de PowerShell

Determine qué scripts de PowerShell (si hay alguno) se permiten ejecutar en el equipo. Elija una de las siguientes directivas de ejecución:  

- **AllSigned**: solo se ejecutan scripts firmados por un editor de confianza  

- **Undefined**: no se define ninguna directiva de ejecución  

- **Bypass**: se cargan todos los archivos de configuración y se ejecutan todos los scripts. Si descarga un script no firmado desde Internet, Windows PowerShell no solicita permiso antes de ejecutarlo.  

> [!IMPORTANT]  
> PowerShell 1.0 no admite las directivas de ejecución Sin definir ni Desviar.  

#### <a name="output-to-task-sequence-variable"></a>Salida a la variable de secuencia de tareas

<!-- 3556028 -->
A partir de la versión 1902, guarde la salida del script en una variable de secuencia de tareas personalizada.

#### <a name="start-in"></a>Iniciar en

<!-- 3556028 -->
A partir de la versión 1902, especifique la carpeta de inicio del script, hasta 127 caracteres. Esta carpeta puede ser una ruta de acceso absoluta en el equipo de destino, o una ruta de acceso relacionada con la carpeta del punto de distribución que contiene el paquete. Este campo es opcional.  

> [!NOTE]  
> El botón **Examinar** busca los archivos y carpetas en el equipo local. Todo lo que seleccione también debe existir en el equipo de destino. Debe existir en la misma ubicación y con los mismos nombres de archivo y carpeta.  

#### <a name="time-out"></a>Tiempo de espera

<!-- 3556028 -->
A partir de la versión 1902, especifique un valor que represente cuánto tiempo permite Configuration Manager que se ejecute el script de PowerShell. Este valor puede estar comprendido entre 1 minuto y 999 minutos. El valor predeterminado es 15 minutos. Esta opción está deshabilitada de forma predeterminada.  

> [!IMPORTANT]  
> Si escribe un valor que no permite tiempo suficiente para que finalice correctamente el script especificado, se produce un error en este paso. Podría producirse un error en la secuencia de tareas completa en función de las condiciones del paso o el grupo. Si se agota el tiempo de espera, Configuration Manager finaliza el proceso de PowerShell.  

#### <a name="run-this-step-as-the-following-account"></a>Ejecutar esta etapa como la cuenta siguiente

<!-- 3556028 -->
A partir de la versión 1902, especifique que el script de PowerShell se ejecuta como una cuenta de usuario de Windows diferente de la cuenta del sistema local.  

> [!NOTE]  
> Para ejecutar comandos o scripts sencillos con otra cuenta después de instalar el sistema operativo, primero agregue la cuenta al equipo. Además, es posible que deba restaurar perfiles de usuario de Windows para ejecutar acciones más complejas.  

#### <a name="account"></a>Cuenta

<!-- 3556028 -->
A partir de la versión 1902, especifique la cuenta de usuario de Windows que se usa en este paso para ejecutar el script de PowerShell. La cuenta especificada debe ser un administrador local en el sistema y el script se ejecuta con los permisos de esta cuenta. Seleccione **Establecer** para especificar la cuenta de usuario o dominio local. Para obtener más información sobre la cuenta de "ejecutar como" de la secuencia de tareas, consulte [Cuentas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account).

> [!IMPORTANT]  
> Si este paso especifica una cuenta de usuario y se ejecuta en Windows PE, se produce un error en la acción. No se puede unir Windows PE a un dominio. El archivo **smsts.log** registra este error.  

### <a name="options"></a>Opciones  

Además de las opciones predeterminadas, configure las siguientes opciones adicionales en la pestaña **Opciones** de este paso de secuencia de tareas:  

#### <a name="success-codes"></a>Códigos de éxito

<!-- 3556028 -->
A partir de la versión 1902, incluya otros códigos de éxito del script que el paso debe valorar como correctos.



## <a name="child-task-sequence"></a> Ejecutar secuencia de tareas

> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Habilítela para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).

Este paso ejecuta otra secuencia de tareas. Se crea una relación de elementos primarios y secundarios entre las secuencias de tareas. Con las secuencias de tareas secundarias, puede crear secuencias de tareas más modulares y reutilizables.

Para agregar este paso en el editor de secuencia de tareas,seleccione **Agregar**, **General** y **Ejecutar secuencia de tareas**.

A partir de la versión 1906, administre este paso con los siguientes cmdlets de PowerShell:<!-- 2839943, SCCMDocs #1118 -->

- **New-CMTSStepRunTaskSequence**
- **Set-CMTSStepRunTaskSequence**

### <a name="specifications-and-limitations"></a>Especificaciones y limitaciones

Tenga en cuenta los siguientes puntos al agregar una secuencia de tareas secundaria a una secuencia de tareas:  

- Las secuencias de tareas primaria y secundaria se combinan eficazmente en una única directiva que ejecuta el cliente.  

- El entorno es global. Si la secuencia de tareas primaria establece una variable y, después, la secuencia de tareas secundaria cambia esa variable, conserva el valor más reciente. Si la secuencia de tareas secundaria crea una variable, está disponible para el resto de la secuencia de tareas primaria.  

- Los mensajes de estado se envían de manera normal para una operación de secuencia de tareas única.  

- Las secuencias de tareas escriben entradas en el archivo **smsts.log**, con nuevas entradas de registro que dejan claro cuando se inicia una secuencia de tareas secundaria.  

<!--the following points are from SCCMdocs issue #1079-->

- No puede seleccionar una secuencia de tareas con una referencia de imagen de arranque. Para cualquier implementación que requiera una imagen de arranque, especifíquela en la secuencia de tareas primaria.  

- Si se deshabilita una secuencia de tareas secundaria, se produce un error en la implementación. No puede usar la opción **Continuar después de un error** para sortear esta limitación.  

- Si una secuencia de tareas secundaria contiene los pasos que se consideran de *alto impacto*, el centro de software no lo detecta y muestra la notificación de alto impacto. Modifique las propiedades de la secuencia de tareas primaria, en la pestaña Notificación de usuario, para especificar que **es una secuencia de tareas de alto impacto**.  

- Si a una secuencia de tareas secundaria le falta una referencia de paquete, la visualización de la secuencia de tareas primaria no detecta este estado. Si edita la secuencia de tareas primaria, detecta todas las referencias que faltan en secuencias de tareas secundarias al realizar cambios en el elemento primario.  

### <a name="properties"></a>Propiedades

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="select-task-sequence-to-run"></a>Seleccionar la secuencia de tareas que se va a ejecutar

Seleccione **Examinar** para seleccionar la secuencia de tareas secundaria. En el cuadro de diálogo **Seleccionar una secuencia de tareas** no se muestra la secuencia de tarea primaria.



## <a name="BKMK_SetDynamicVariables"></a> Establecer variables dinámicas  

Use este paso para realizar las acciones siguientes:  

1. Recopilar información del equipo y su entorno. A continuación, establezca las variables de la secuencia de tareas con la información.  

2. Evaluar las reglas definidas. Establezca las variables de secuencia de tareas en función de las reglas que se evalúen como verdaderas.  

La secuencia de tareas establece automáticamente las siguientes variables de la secuencia de tareas de solo lectura:  

- [\_SMSTSMake](/sccm/osd/understand/task-sequence-variables#SMSTSMake)  
- [\_SMSTSModel](/sccm/osd/understand/task-sequence-variables#SMSTSModel)  
- [\_SMSTSMacAddresses](/sccm/osd/understand/task-sequence-variables#SMSTSMacAddresses)  
- [\_SMSTSIPAddresses](/sccm/osd/understand/task-sequence-variables#SMSTSIPAddresses)  
- [\_SMSTSSerialNumber](/sccm/osd/understand/task-sequence-variables#SMSTSSerialNumber)  
- [\_SMSTSAssetTag](/sccm/osd/understand/task-sequence-variables#SMSTSAssetTag)  
- [\_SMSTSUUID](/sccm/osd/understand/task-sequence-variables#SMSTSUUID)  

Este paso se puede ejecutar en el sistema operativo completo o Windows PE.  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **General** y **Establecer variables dinámicas**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="dynamic-rules-and-variables"></a>Variables y reglas dinámicas

Para establecer una variable dinámica para su uso en la secuencia de tareas, agregue una regla. Después, establezca un valor para cada variable especificada en la regla. Además, puede agregar una o más variables sin agregar una regla. Cuando se agrega una regla, elija entre las siguientes categorías:  

- **Equipo**: evalúe los valores para la etiqueta de inventario de hardware, UUID, número de serie o dirección MAC. Establezca varios valores según sea necesario. Si alguno de los valores es true, la regla se evalúa como true. Por ejemplo, la regla siguiente se evalúa como true si el número de serie del dispositivo es 5892087 y la dirección MAC es 22-A4-5A-13-78-26:  

    `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

- **Ubicación**: evalúe los valores de la puerta de enlace de red predeterminada  

- **Marca y modelo**: evalúe los valores de la marca y modelo de un equipo. La marca y el modelo deben evaluarse como true para que la regla se evalúe como true.

    Especifique un asterisco (`*`) y un signo de interrogación (`?`) como caracteres comodín. El asterisco coincide con varios caracteres y el signo de interrogación con un solo carácter. Por ejemplo, la cadena `DELL*900?` coincide con `DELL-ABC-9001` y `DELL9009`.  

- **Variable de secuencia de tareas**: agregue una variable de secuencia de tareas, la condición y el valor que se van a evaluar. La regla se evalúa como true cuando el valor establecido para la variable cumple la condición especificada.  

    Especifique una o más variables que se van a establecer para una regla que se evalúa como true, o bien establezca variables sin usar una regla. Seleccione una variable existente o cree una variable personalizada.  

    - **Variables de secuencia de tareas existentes**: seleccione una o más variables en una lista de variables de secuencia de tareas existentes. Las variables de matriz no están disponibles para seleccionar.  

    - **Variables de secuencia de tareas personalizadas**: defina una variable de secuencia de tareas personalizada. También puede especificar una variable de secuencia de tareas existente. Este valor es útil para especificar una matriz de variables existente, como **OSDAdapter**, ya que las matrices de variables no están en la lista de variables de secuencia de tareas existentes.  

Después de seleccionar las variables de una regla, proporcione un valor para cada variable. La variable se establece en el valor especificado cuando la regla se evalúa como true. Para cada variable, puede seleccionar **Valor secreto** para ocultar el valor de la variable. De forma predeterminada, algunas de las variables existentes ocultan valores, como la variable **OSDCaptureAccountPassword**.  

> [!IMPORTANT]  
> Configuration Manager quita los valores de variable marcados como **Valor secreto** al importar una secuencia de tareas con el paso **Establecer variables dinámicas**. Vuelva a escribir el valor de la variable dinámica después de importar la secuencia de tareas.  



## <a name="BKMK_SetTaskSequenceVariable"></a> Establecer variable de secuencia de tareas  

Use este paso para establecer el valor de una variable que se usa con la secuencia de tareas.  

Este paso se puede ejecutar en el sistema operativo completo o Windows PE.

Las variables de secuencia de tareas son leídas por acciones de secuencia de tareas y especifican el comportamiento de esas acciones. Para obtener más información acerca de las variables de secuencia de tareas específicas y cómo usarlas, consulte los artículos siguientes:  

- [Uso de variables de secuencias de tareas](/sccm/osd/understand/using-task-sequence-variables)  
- [Variables de secuencias de tareas](/sccm/osd/understand/task-sequence-variables)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **General** y **Configurar variable de secuencia de tareas**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="task-sequence-variable"></a>Variable de secuencia de tareas

Especifique el nombre de una variable de acción o de secuencia de tareas integrada, o bien especifique su propio nombre de variable definido por el usuario.  

#### <a name="do-not-display-this-value"></a>No mostrar este valor

<!--1358330-->
A partir de la versión 1806, habilite esta opción para enmascarar datos confidenciales almacenados en variables de secuencia de tareas. Por ejemplo, al especificar una contraseña.

> [!Note]  
> Habilite esta opción y, a continuación, establezca el valor de la variable de secuencia de tareas. En caso contrario, el valor de la variable no se configura tal como desea, lo cual puede provocar comportamientos inesperados cuando se ejecuta la secuencia de tareas.<!--SCCMdocs issue #800-->

#### <a name="value"></a>Valor  

La secuencia de tareas establece la variable en este valor. Establezca esta variable de secuencia de tareas en el valor de otra variable de secuencia de tareas con la sintaxis `%varname%`.  



## <a name="BKMK_SetupWindowsandConfigMgr"></a> Instalar Windows y Configuration Manager  

Use este paso para realizar la transición desde Windows PE al nuevo sistema operativo. Este paso de secuencia de tareas es una parte necesaria de cualquier implementación de sistema operativo. Se instala el cliente de Configuration Manager en el nuevo sistema operativo y se prepara para que la secuencia de tareas continúe con la ejecución en el sistema operativo.  

Este paso es responsable de la transición de la secuencia de tareas de Windows PE al sistema operativo completo. El paso se ejecuta tanto en Windows PE como en el sistema operativo completo debido a esta transición. Sin embargo, dado que la transición comienza en Windows PE, solo se puede Agregar durante la parte de Windows PE de la secuencia de tareas.  

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [SMSClientInstallProperties](/sccm/osd/understand/task-sequence-variables#SMSClientInstallProperties)  

Este paso reemplaza las variables de directorio sysprep.inf o unattend.xml, como `%WINDIR%` y `%ProgramFiles%`, por el directorio de instalación de Windows PE, `X:\Windows`. La secuencia de tareas ignora las variables especificadas mediante estas variables de entorno.  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Imágenes** e **Instalar Windows y Configuration Manager**.

### <a name="step-actions"></a>Acciones del paso

Este paso realiza las siguientes acciones:  

#### <a name="preliminaries-windows-pe"></a>Pasos preliminares: Windows°PE  

1. Sustituya las variables de secuencia de tareas en el archivo unattend.xml.  

2. Descargue el paquete que contiene el cliente de Configuration Manager. Agregue el paquete a la imagen implementada.  

#### <a name="set-up-windows"></a>Configurar Windows  

- Instalación basada en imagen  

    1. Deshabilite el cliente de Configuration Manager en la imagen, si existe. En otras palabras, deshabilite el inicio automático para el servicio de cliente de Configuration Manager.  

    2. Actualice el Registro en la imagen implementada para iniciar el sistema operativo implementado con la misma letra de unidad que el equipo de referencia.  

    3. Reinicie en el sistema operativo implementado.  

    4. La instalación mínima de Windows se ejecuta con los archivos de respuesta sysprep.inf o unattend.xml especificados anteriormente que tienen suprimida toda la interacción del usuario final. Si se usa el paso **Aplicar configuración de red** para unirse a un dominio, después esa información se encuentra en el archivo de respuesta. La instalación mínima de Windows une el equipo al dominio.  

- Instalación basada en Setup.exe. Ejecuta Setup.exe que sigue el proceso de instalación típico de Windows:  

    1. Copie el paquete de actualización del sistema operativo, especificado en el paso **Aplicar el sistema operativo**, en la unidad de disco duro.  

    2. Reinicie en el sistema operativo recién implementado.  

    3. La instalación mínima de Windows se ejecuta con los archivos de respuesta sysprep.inf o unattend.xml especificados anteriormente que tienen suprimida toda la configuración de la interfaz de usuario. Si se usa el paso **Aplicar configuración de red** para unirse a un dominio, después esa información se encuentra en el archivo de respuesta. La instalación mínima de Windows une el equipo al dominio.  

#### <a name="set-up-the-configuration-manager-client"></a>Configurar el cliente de Configuration Manager  

1. Una vez finalizada la instalación mínima de Windows, la secuencia de tareas se reanuda mediante setupcomplete.cmd.  

2. Habilite o deshabilite la cuenta de administrador local, según la opción seleccionada en el paso **Aplicar configuraciones de Windows**.  

3. Instale el cliente de Configuration Manager mediante el paquete descargado anteriormente y las propiedades de instalación especificadas en este paso. El cliente se instala en "modo de aprovisionamiento". Este modo impide que el cliente procese nuevas solicitudes de directiva hasta que se complete la secuencia de tareas. Para obtener más información, vea [Modo de aprovisionamiento](/sccm/osd/understand/provisioning-mode).  

4. Espere a que el cliente esté totalmente operativo.  

#### <a name="the-step-completes"></a>Se completa el paso

La secuencia de tareas continúa ejecutando el paso siguiente.  

> [!Note]  
> La directiva de grupo de Windows no se procesa normalmente hasta haber finalizado la secuencia de tareas. Este comportamiento es coherente entre las distintas versiones de Windows. Otras acciones personalizadas durante la secuencia de tareas pueden desencadenar la evaluación de directivas de grupo.<!-- 2841304 -->


### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="client-package"></a>Paquete de cliente

Seleccione **Examinar** y luego elija el paquete de instalación de cliente de Configuration Manager para usar con este paso.  

#### <a name="use-pre-production-client-package-when-available"></a>Usar el paquete de cliente de preproducción cuando esté disponible

Si hay un paquete de cliente de preproducción disponible y el equipo forma parte de la recopilación de uso piloto, la secuencia de tareas lo usa en lugar del paquete de cliente de producción. El cliente de preproducción es una versión más reciente para pruebas en el entorno de producción. Seleccione **Examinar** y después elija el paquete de instalación de cliente de preproducción para usar con este paso.  

#### <a name="installation-properties"></a>Propiedades de instalación

El paso de la secuencia de tareas especifica automáticamente la asignación de sitios y la configuración predeterminada. Use este campo para especificar propiedades de instalación adicionales que se utilizarán al instalar el cliente. Si desea especificar varias propiedades de instalación, sepárelas con un espacio.  

Especifique opciones de línea de comandos para que se usen durante la instalación de cliente. Por ejemplo, escriba `/skipprereq: silverlight.exe` para informar a CCMSetup.exe que no instale el requisito previo de Microsoft Silverlight. Para obtener más información sobre las opciones de líneas de comandos disponibles para CCMSetup.exe, consulte [Acerca de las propiedades de instalación de clientes](/sccm/core/clients/deploy/about-client-installation-properties).  

### <a name="options"></a>Opciones

> [!NOTE]  
> No habilite **Continuar después de un error** en la pestaña **Opciones**. Si se produce un error durante este paso, se produce un error en la secuencia de tareas con independencia de que se habilite o no esta configuración.  



## <a name="BKMK_UpgradeOS"></a> Actualizar el sistema operativo  

> [!TIP]  
> A partir de la versión 1709 de Windows 10, los medios incluyen varias ediciones. Cuando se configura una secuencia de tareas para usar un paquete de actualización del sistema operativo o una imagen del sistema operativo, no olvide seleccionar una [edición admitida](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).  

Use este paso para actualizar una versión anterior de Windows a una versión más reciente de Windows 10.  

Este paso de secuencia de tareas solo se ejecuta en el sistema operativo completo. No se ejecuta en Windows PE.  

Utilice las siguientes variables de secuencia de tareas con este paso:  

- [_SMSTSOSUpgradeActionReturnCode](/sccm/osd/understand/task-sequence-variables#SMSTSOSUpgradeActionReturnCode)  
- [OSDSetupAdditionalUpgradeOptions](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions)  

Para agregar este paso en el editor de secuencia de tareas, seleccione **Agregar**, **Imágenes** y **Actualizar sistema operativo**.

### <a name="properties"></a>Propiedades  

En la pestaña **Propiedades** de este paso, configure las opciones descritas en esta sección.  

#### <a name="upgrade-package"></a>Paquete de actualización

Seleccione esta opción para especificar el paquete de actualización del sistema operativo de Windows 10 que se usará para la actualización.  

#### <a name="source-path"></a>Ruta de origen

Especifica una ruta de acceso local o de red para los medios de Windows 10 que usa el programa de instalación de Windows. Esta opción corresponde a la opción de línea de comandos de instalación de Windows `/InstallFrom`.

También puede especificar una variable, como `%MyContentPath%` o `%DPC01%`. Cuando se use una variable para la ruta de origen, establezca su valor previamente en la secuencia de tareas. Por ejemplo, use el paso [Descargar contenido de paquete](#BKMK_DownloadPackageContent) para especificar una variable para la ubicación del paquete de actualización del sistema operativo. A continuación, use esa variable para la ruta de origen para este paso.  

#### <a name="edition"></a>Edición

Especifique la edición en los medios del sistema operativo que se usará para la actualización.  

#### <a name="product-key"></a>Clave de producto

Especifique la clave de producto que se debe aplicar al proceso de actualización.  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>Proporcionar el contenido del controlador siguiente al programa de configuración de Windows durante la actualización

Agregue controladores al equipo de destino durante el proceso de actualización. Esta opción corresponde a la opción de línea de comandos de instalación de Windows `/InstallDriver`. Los controladores deben ser compatibles con Windows 10. Especifique una de las siguientes opciones:  

- **Paquete de controladores**: seleccione **Examinar** y elija un paquete de controladores existente en la lista.  

- **Contenido almacenado provisionalmente**: seleccione esta opción para especificar la ubicación del paquete de controladores. Puede especificar una carpeta local, la ruta de red o una variable de secuencia de tareas. Cuando se use una variable para la ruta de origen, establezca su valor previamente en la secuencia de tareas. Por ejemplo, mediante el paso [Descargar contenido de paquete](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent).  

#### <a name="time-out-minutes"></a>Tiempo de espera (minutos)

Especifique el número de minutos antes de que se produzca un error de Configuration Manager en este paso. Esta opción es útil si el programa de instalación de Windows detiene el procesamiento pero no finaliza.  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>Realizar examen de compatibilidad del programa de instalación de Windows sin iniciar la actualización

Realice el examen de compatibilidad del programa de instalación de Windows sin iniciar el proceso de actualización. Esta opción corresponde a la opción de línea de comandos de instalación de Windows `/Compat ScanOnly`. Implemente el paquete de actualización del sistema operativo completo con esta opción.

<!--SCCMDocs-pr issue 2812-->
A partir de la versión 1806, cuando se habilita esta opción, este paso no pone el cliente de Configuration Manager en modo de aprovisionamiento. El programa de instalación de Windows se ejecuta silenciosamente en segundo plano y el cliente continúa funcionando con normalidad. Para obtener más información, vea [Modo de aprovisionamiento](/sccm/osd/understand/provisioning-mode).

La instalación devuelve un código de salida como resultado de la exploración. En la tabla siguiente se proporcionan algunos de los códigos de salida más comunes:  

|Código de salida|Detalles|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|No hay problemas de compatibilidad ("correcto").|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Problemas de compatibilidad accionables.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|La opción de migración seleccionada no está disponible. Por ejemplo, una actualización de Enterprise a Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|No elegible para Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|No hay suficiente espacio en disco libre.|  

Para más información sobre este parámetro, vea [Opciones de la línea de comandos del programa de instalación de Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#6).  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>Omitir cualquier mensaje de compatibilidad descartable

Especifica que el programa de instalación completa la instalación, omitiendo los mensajes de compatibilidad descartables. Esta opción corresponde a la opción de línea de comandos de instalación de Windows `/Compat IgnoreWarning`.  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>Actualizar programa de instalación de Windows dinámicamente con Windows Update

Habilite el programa de instalación para realizar operaciones de actualización dinámica, como buscar, descargar e instalar actualizaciones. Esta opción corresponde a la opción de línea de comandos de instalación de Windows `/DynamicUpdate`. Esta opción no es compatible con las actualizaciones de software de Configuration Manager. Habilite esta opción cuando administre actualizaciones con Windows Server Update Services (WSUS) independiente o Windows Update para empresas.  

#### <a name="override-policy-and-use-default-microsoft-update"></a>Invalidar directiva y usar Microsoft Update predeterminado

Invalide temporalmente la directiva local en tiempo real para ejecutar operaciones de actualización dinámica. El equipo obtiene actualizaciones desde Windows Update.
