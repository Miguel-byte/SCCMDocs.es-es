---
title: Administrar paquetes de actualización del sistema operativo
titleSuffix: Configuration Manager
description: Aprenda a administrar paquetes de actualización del sistema operativo en Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 46e948a215535bf57153e5a97dbdc9cad2e35e3b
ms.sourcegitcommit: 54e5786875c4e5f5c1b54e38ed59e96344faf9b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2019
ms.locfileid: "53817858"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>Administrar paquetes de actualización del sistema operativo con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Un paquete de actualización del sistema operativo en Configuration Manager contiene los archivos de origen de instalación de Windows necesarios para actualizar un sistema operativo existente en un equipo. En este artículo se describe cómo agregar, distribuir y reparar un paquete de actualización de sistema operativo.

>[!NOTE]
>Los paquetes de actualización del sistema operativo también pueden utilizarse para las nuevas instalaciones de Windows. Sin embargo, dependen de que los controladores sean compatibles con este método. Al realizar nuevas instalaciones de Windows desde un paquete de actualización del sistema operativo, los controladores se instalan en Windows PE en lugar de simplemente inyectarse en Windows PE. Algunos controladores no son compatibles con la instalación en Windows PE. Si los controladores no son compatibles con la instalación en Windows PE, en su lugar, use una [imagen del sistema operativo](/sccm/osd/get-started/manage-operating-system-images), como **install.wim**.


##  <a name="BKMK_AddOSUpgradePkgs"></a> Agregar un paquete de actualización del sistema operativo  

Para poder usar un paquete de actualización del sistema operativo, primero debe agregarlo a su sitio de Configuration Manager. 

1.  En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y después haga clic en el nodo **Paquetes de actualización del sistema operativo**.  

2.  En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Agregar paquete de actualización de sistema operativo**. Esta acción inicia el asistente para agregar una actualización del sistema operativo.  

3.  En la página **Origen de datos**, especifique la siguiente configuración: 

    - La **Ruta** de red a la instalación de los archivos de origen del paquete de actualización del sistema operativo. Por ejemplo, `\\server\share\path`.  

        > [!NOTE]  
        >  Los archivos de origen de instalación contienen setup.exe y otros archivos y carpetas para instalar el sistema operativo.  

        > [!IMPORTANT]  
        >  Limite el acceso a los archivos de origen de instalación para evitar la manipulación no deseada.  

    - Si quiere almacenar previamente en caché contenido en un cliente, especifique la **Arquitectura** y el **Lenguaje** de la imagen. Para obtener más información, vea [Configuración del contenido de la caché previa](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

4.  En la página **General**, especifique la siguiente información. Esta información es útil para identificar el paquete de actualización del sistema operativo cuando se tiene más de uno.  

    -   **Nombre**: nombre único del paquete de actualización del sistema operativo.  

    -   **Versión**: identificador de versión opcional. Esta propiedad no tiene que ser la versión del sistema operativo del paquete de actualización. A menudo es la versión de la organización para el paquete.  

    -   **Comentario**: breve descripción opcional.  

5.  Complete el asistente.  


A continuación, distribuya el paquete de actualización del sistema operativo a puntos de distribución.  



##  <a name="BKMK_Distribute"></a> Distribución de contenido a un punto de distribución  

Distribuya los paquetes de actualización del sistema operativo a puntos de distribución del mismo modo que otro tipo de contenido. Antes de implementar la secuencia de tareas, distribuya el paquete de actualización del sistema operativo al menos a un punto de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  



[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]



## <a name="next-steps"></a>Pasos siguientes

[Creación de una secuencia de tareas para actualizar un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)
