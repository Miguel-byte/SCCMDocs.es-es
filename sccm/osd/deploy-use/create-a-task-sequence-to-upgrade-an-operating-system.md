---
title: Crear una secuencia de tareas para actualizar un sistema operativo | Configuration Manager
description: "Las secuencias de tareas de System Center Configuration Manager pueden actualizar automáticamente un sistema operativo de Windows 7 o posterior a Windows 10."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: 12
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fe70a3bfddcc0638a27eccb04324c4e6e2ace1d4


---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Cree una secuencia de tareas para actualizar un sistema operativo en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use las secuencias de tareas de System Center Configuration Manager para actualizar automáticamente un sistema operativo de Windows 7 o posterior a Windows 10 en un equipo de destino. Cree una secuencia de tareas que haga referencia a la imagen del sistema operativo que quiere instalar en el equipo de destino y a cualquier otro contenido adicional, como actualizaciones de aplicaciones o software que quiera instalar. La secuencia de tareas para actualizar un sistema operativo es parte del escenario de [Upgrade Windows to the latest version (Actualizar Windows a la versión más reciente)](upgrade-windows-to-the-latest-version.md).  

##  <a name="a-namebkmkupgradeosa-create-a-task-sequence-to-upgrade-an-operating-system"></a><a name="BKMK_UpgradeOS"></a> Crear una secuencia de tareas para actualizar un sistema operativo  
 Para actualizar el sistema operativo a Windows 10 en los equipos, puede crear una secuencia de tareas y seleccionar **Actualizar un sistema operativo desde el paquete de actualización** en el Asistente para crear secuencia de tareas. El asistente agregará los pasos para actualizar el sistema operativo, aplicar actualizaciones de software e instalar aplicaciones. Antes de crear la secuencia de tareas, lo siguiente debe estar en su lugar:  

-   **Requerido**  

     - El [paquete de actualización del sistema operativo](../get-started/manage-operating-system-upgrade-packages.md) de Windows 10 debe estar disponibles en la consola de Configuration Manager.  

-   **Necesario (si se usa)**  

    -   Las [actualizaciones de software](../../sum/get-started/synchronize-software-updates.md) deben estar sincronizadas en la consola de Configuration Manager.  

    -   Las [aplicaciones](../../apps/deploy-use/create-applications.md) deben agregarse a la consola de Configuration Manager.  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>Para crear una secuencia de tareas que actualice un sistema operativo  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear secuencia de tareas** para iniciar el Asistente para crear secuencia de tareas.  

4.  En la página **Crear nueva secuencia de tareas** , haga clic en **Actualizar un sistema operativo desde el paquete de actualización**y luego haga clic en **Siguiente**.  

5.  En la página **Información de secuencia de tareas** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

    -   **Nombre de secuencia de tareas**: especifique un nombre que identifique la secuencia de tareas.  

    -   **Descripción**: especifique una descripción de la tarea que se realiza mediante la secuencia de tareas.  

6.  En la página **Actualizar el sistema operativo de Windows** , especifique la siguiente configuración y luego haga clic en **Siguiente**.  

    -   **Paquete de actualización**: especifique el paquete de actualización que contiene los archivos de origen de actualización del sistema operativo. Puede comprobar que ha seleccionado el paquete de actualización correcto examinando la información del panel **Propiedades** . Para más información, vea [Manage operating system upgrade packages (Administrar paquetes de actualización de sistema operativo)](../get-started/manage-operating-system-upgrade-packages.md).  

    -   **Índice de edición**: si hay varios índices de edición del sistema operativo disponibles en el paquete, seleccione el índice de la edición deseada. De forma predeterminada, se selecciona el primer elemento.  

    -   **Clave de producto**: especifique la clave de producto para el sistema operativo Windows que quiere instalar. Puede especificar claves de licencia por volumen codificadas y claves de producto estándar. Si utiliza una clave de producto no codificada, cada grupo de 5 caracteres debe estar separado por un guión (-). Por ejemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Si se trata de una actualización de una edición de licencia por volumen, la clave de producto no es necesaria. La clave de producto solo se necesita cuando la actualización es para una edición comercial de Windows.  

7.  En la página **Incluir actualizaciones** , especifique si desea instalar las actualizaciones de software necesarias, todas las actualizaciones de software o ninguna y, a continuación, haga clic en **Siguiente**. Si especifica que se instalen las actualizaciones de software, Configuration Manager instala solo las que se destinan a las colecciones a las que pertenece el equipo de destino.  

8.  En la página **Instalar aplicaciones** , especifique las aplicaciones que desee instalar en el equipo de destino y, a continuación, haga clic en **Siguiente**. Si especifica varias aplicaciones, también puede especificar que la secuencia de tareas continúe si se produce un error en la instalación de una aplicación específica.  

9. Complete el asistente.  

## <a name="download-package-content-task-sequence-step"></a>Paso de la secuencia de tareas Descargar contenido de paquete  
 El paso [Descargar contenido de paquete](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) se puede usar antes del paso **Actualizar sistema de operativo** en los siguientes escenarios:  

-   Use una secuencia de tareas de actualización única que funciona con las plataformas x86 y x64. Para hacerlo, incluya dos pasos **Descargar contenido de paquete** en el grupo **Preparación para actualización** con condiciones para detectar la arquitectura del cliente y descargar únicamente el paquete de actualización del sistema operativo adecuado. Configure todos los pasos **Descargar contenido de paquete** para que usen la misma variable, y use la variable para la ruta de los medios en el paso **Actualizar sistema operativo** .  

-   Para descargar dinámicamente un paquete de controladores aplicables, use dos pasos **Descargar contenido de paquete** con condiciones para detectar el tipo de hardware adecuado para cada paquete de controlador. Configure todos los pasos **Descargar contenido de paquete** para que usen la misma variable, y use la variable para el valor **Staged content** en la sección de controladores en el paso **Actualizar sistema operativo** .  

   > [!NOTE]
   > Cuando hay más de un paquete, Configuration Manager agrega un sufijo numérico al nombre de variable. Por ejemplo, si especifica una variable de %mycontent% como variable personalizada, es la raíz de donde se almacena todo el contenido al que se hace referencia (que puede ser varios paquetes). Cuando se hace referencia a la variable en un paso de subsecuencia, como Actualizar el sistema operativo, se usa con un sufijo numérico. En este ejemplo, %mycontent01% o %mycontent02%, donde el número corresponde al orden en el que el paquete aparece en este paso.

## <a name="optional-post-processing-task-sequence-steps"></a>Pasos de la secuencia de tareas de procesamiento posterior opcional  
 Después de crear la secuencia de tareas, puede agregar pasos adicionales para desinstalar las aplicaciones con problemas de compatibilidad conocidos, o bien agregar acciones posteriores al procesamiento para que se ejecuten después de reiniciar el equipo y tras la correcta actualización a Windows 10. Agregue estos pasos adicionales al grupo de procesamiento posterior de la secuencia de tareas.  

> [!NOTE]  
>  Dado que esta secuencia de tareas no es lineal, hay condiciones en los pasos que pueden afectar a sus resultados, en función de si actualiza correctamente el equipo cliente o si tiene que revertir el equipo cliente a la versión del sistema operativo inicial.  

## <a name="optional-rollback-task-sequence-steps"></a>Pasos de secuencia de tareas de reversión opcional  
 Cuando se produce algún problema con el proceso de actualización después de reiniciar el equipo, el programa de instalación revertirá la actualización al sistema operativo anterior y continuará la secuencia de tareas con cualquier paso en el grupo de reversión. Después de crear la secuencia de tareas, puede agregar pasos adicionales al grupo de reversión.  

## <a name="folder-and-files-removed-after-computer-restart"></a>Carpeta y archivos eliminados después del reinicio del equipo  
 Cuando se completan la secuencia de tareas para actualizar un sistema operativo a Windows 10 y todos los demás pasos de la secuencia de tareas, los scripts posteriores al procesamiento y la reversión no se quitan hasta que no se reinicia el equipo.  Estos archivos de script no contienen información confidencial.  



<!--HONumber=Nov16_HO1-->


