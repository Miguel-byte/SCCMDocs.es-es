---
title: Configuración del contenido de la caché previa
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo los clientes pueden descargar el contenido de la implementación del sistema operativo antes de que un usuario instale la secuencia de tareas.
ms.date: 09/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9d1e8252-99e3-48aa-bfa5-0cf4cd6637b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fc212104dc69e4ba4cc7d82e0b8c4813094bea2d
ms.sourcegitcommit: 2dbe49e3ef1133d49e58d82cefdeba69f9ba3ce2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 09/19/2019
ms.locfileid: "71127292"
---
# <a name="configure-pre-cache-content-for-task-sequences"></a>Configurar el contenido de la caché previa para las secuencias de tareas

*Se aplica a: System Center Configuration Manager (Rama actual)*

<!--1021244-->
La característica de caché previa para las implementaciones disponibles de secuencias de tareas permite que los clientes descarguen el contenido pertinente antes de que un usuario instale la secuencia de tareas. El cliente puede almacenar en caché previamente el contenido de las secuencias de tareas que [actualizan un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system) o [instalan una imagen de sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system).

> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

Por ejemplo, solo quiere una secuencia de tareas de actualización en contexto para todos los usuarios y tiene muchas arquitecturas y lenguajes. En versiones anteriores, el contenido se comienza a descargar cuando el usuario instala una implementación de secuencia de tareas disponible desde el Centro de software. Este retraso agrega tiempo adicional antes de que la instalación esté lista para iniciarse. Se descarga todo el contenido al que se hace referencia en la secuencia de tareas. Este contenido incluye el paquete de actualización de sistema operativo para todos los lenguajes y arquitecturas. Si cada paquete de actualización tiene aproximadamente 3 GB de tamaño, el contenido total es muy grande.

El contenido de caché previa proporciona la opción al cliente de descargar solo el contenido aplicable y otro contenido al que se haga referencia, tan pronto como reciba la implementación. Cuando el usuario hace clic en **Instalar** en el Centro de software, el contenido está listo. La instalación se inicia rápidamente porque el contenido está en el disco duro local.

En Configuration Manager versión 1902 y versiones anteriores, este comportamiento solo se aplica al *paquete de actualización del sistema operativo*. Ese paquete es el único contenido en el que se especifica la arquitectura o el idioma correspondiente. Por ejemplo, si la secuencia de tareas también hace referencia a varios paquetes de controladores, el cliente los descarga todos. El motor de secuencia de tareas evalúa las condiciones en los pasos cuando se ejecuta la secuencia de tareas, no con antelación. El cliente usa las etiquetas de las propiedades del paquete para determinar qué contenido se almacena en la caché previa.

A partir de la versión 1906,<!--4224642--> puede usar el almacenamiento en caché previa para reducir el consumo de ancho de banda de los siguientes tipos de contenido:

- Paquetes de actualización del sistema operativo
- Imágenes de SO
- Paquetes de controladores
- Paquetes


## <a name="configure-pre-caching"></a>Configurar el almacenamiento en caché previa

Hay tres pasos para configurar la característica de caché previa:

1. [Crear y configurar los paquetes](#bkmk_createpkg)
2. [Crear una secuencia de tareas con pasos condicionales](#bkmk_createts)
3. [Implementar la secuencia de tareas y habilitar el almacenamiento en caché previa](#bkmk_deploy)


### <a name="bkmk_createpkg"></a> 1. Crear y configurar los paquetes

El cliente evalúa los atributos de los paquetes para determinar qué contenido se descarga durante el almacenamiento en caché previa.  

#### <a name="os-upgrade-package"></a>Paquete de actualización del sistema operativo

Cree [paquetes de actualización del sistema operativo](/sccm/osd/get-started/manage-operating-system-upgrade-packages) para arquitecturas e idiomas específicos. Especifique la **Arquitectura** y el **Idioma** en la pestaña **Origen de datos** de sus propiedades.

#### <a name="os-image"></a>Imagen del sistema operativo

Cree [imágenes del sistema operativo](/sccm/osd/get-started/manage-operating-system-images) para idiomas y arquitecturas específicos. Especifique la **Arquitectura** y el **Idioma** en la pestaña **Origen de datos** de sus propiedades.

#### <a name="driver-package"></a>Paquete de controladores

Cree [paquetes de controladores](/sccm/osd/get-started/manage-drivers#BKMK_ManagingDriverPackages) para los modelos de hardware específicos. Especifique el **modelo** en la pestaña **General** de sus propiedades.

Para determinar qué paquete de controladores descarga durante el almacenamiento en la caché previa, el cliente evalúa el modelo en comparación con la propiedad **Nombre** de la clase de WMI **Win32_ComputerSystemProduct**.  

#### <a name="package"></a>Paquete

Cree [paquetes](/sccm/apps/deploy-use/packages-and-programs) para idiomas y arquitecturas específicos. Especifique la **Arquitectura** y el **Idioma** en la pestaña **General** de sus propiedades.


### <a name="bkmk_createts"></a> 2. Creación de una secuencia de tareas

Cree una secuencia de tareas con pasos condicionales para los distintos idiomas y arquitecturas, o modelos de hardware diferentes para los paquetes de controladores.

|Content|Paso|
|---------|---------|
|Paquete de actualización del sistema operativo|[Actualizar sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS)|
|Imagen del sistema operativo|[Aplicar imagen de sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyOperatingSystemImage)|
|Paquete de controladores|[Aplicar paquete de controladores](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage)|
|Paquete|[Instalar paquete](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage)|

Por ejemplo, en el siguiente paso de **actualización del sistema operativo** se usa la versión en inglés:  

![Editor de secuencia de tareas en el que se muestran varios pasos de actualización del sistema operativo para ENU, DEU y JPN](../media/precacheproperties2.png)

![Pestaña Opciones del editor de secuencia de tareas, en la que se muestra la consulta WQL de WMI para la Configuración regional y OSArchitecture](../media/precacheoptions2.png)  

> [!Tip]
> Se recomienda la siguiente consulta WMI para el sistema operativo de inglés (Estados Unidos) y la arquitectura de 64 bits:
>
> ```WMI
> SELECT * FROM Win32_OperatingSystem WHERE OSArchitecture LIKE '%64%' AND OSLanguage=1033`
> ```
>
> En primer lugar, agregue el idioma seleccionando la condición de **idioma del sistema operativo** . Después, edite la consulta WMI para incluir la cláusula Architecture.


### <a name="bkmk_deploy"></a> 3. Implementar la secuencia de tareas

[Implemente la secuencia de tareas](/sccm/osd/deploy-use/deploy-a-task-sequence). Para la característica de caché previa, configure las opciones siguientes:  

- En la pestaña **General**, seleccione **Descargar contenido previamente para esta secuencia de tareas**.  

- En la pestaña **Configuración de implementación**, configure la secuencia de tareas como **Disponible**.  

- En la pestaña **Programación**, elija la hora seleccionada actualmente para la opción **Programar cuándo estará disponible esta implementación**. El cliente inicia el almacenamiento del contenido en la caché previa a la hora de disponibilidad de la implementación. Cuando un cliente de destino recibe esta directiva, la hora disponible se encuentra en el pasado, por lo que la descarga en la caché previa se inicia inmediatamente. Si el cliente recibe esta directiva pero la hora disponible está en el futuro, el cliente no inicia el almacenamiento del contenido en la caché previa hasta la hora disponible.  

- En la pestaña **Puntos de distribución**, configure los valores **Opciones de implementación**. Si el contenido no se ha almacenado previamente en la caché antes de que un usuario inicie la instalación, el cliente usa esta configuración.  

    > [!Important]  
    > En el caso de una secuencia de tareas que instala una imagen de sistema operativo, no use la opción de implementación para **descargar el contenido localmente cuando sea necesario para la secuencia de tareas en ejecución**. Cuando la secuencia de tareas borra el disco antes de aplicar la imagen de sistema operativo, quita la memoria caché del cliente. Dado que el contenido ha desaparecido, se produce un error en la secuencia de tareas.<!-- SCCMDocs-PR #1338 -->


## <a name="user-experience"></a>Experiencia del usuario

- Cuando el cliente recibe la directiva de implementación, inicia el almacenamiento del contenido en la caché previa después de la hora disponible de la implementación. Este contenido incluye todos los paquetes a los que se hace referencia, pero solo el paquete de actualización del sistema operativo que coincide con los atributos de idioma y arquitectura del paquete.  

- Cuando el cliente pone la implementación a disposición de los usuarios, se muestra una notificación para informarles sobre la nueva implementación. Ahora la secuencia de tareas es visible en el Centro de software. El usuario puede ir al Centro de software y hacer clic en **Instalar** para iniciar la instalación.  

- Si el cliente no ha almacenado previamente en la caché el contenido cuando el usuario instala la secuencia de tareas, el cliente usa la configuración que se especifique en la pestaña **Opción de implementación** de la implementación.  


## <a name="see-also"></a>Consulte también

- [Creación de una secuencia de tareas para actualizar un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)
- [Escenario para actualizar Windows a la versión más reciente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)
