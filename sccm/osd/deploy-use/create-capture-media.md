---
title: Crear medios de captura
titleSuffix: Configuration Manager
description: Use el Asistente para crear medio de secuencia de tareas para crear medios de captura en Configuration Manager para capturar una imagen de sistema operativo desde un equipo de referencia.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d733f4eb70b9e95bb00a918cb82f47c85cb3059
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417547"
---
# <a name="create-capture-media-with-system-center-configuration-manager"></a>Crear medios de captura con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los medios de captura de Configuration Manager permiten capturar una imagen de sistema operativo desde un equipo de referencia. Use los medios de captura para el escenario siguiente:  

-   [Crear una secuencia de tareas para capturar un sistema operativo](create-a-task-sequence-to-capture-an-operating-system.md)  

##  <a name="BKMK_CreateCaptureMedia"></a> Creación de medios de captura  
 Use medios de captura para capturar una imagen de sistema operativo de un equipo de referencia. Los medios de captura contienen la imagen de arranque que inicia el equipo de referencia y la secuencia de tareas que captura la imagen de sistema operativo.

Los medios de captura se crean mediante el Asistente para crear medio de secuencia de tareas. Antes de ejecutar el asistente, asegúrese de que se cumplen todas las condiciones siguientes:  

|Tarea|Descripción|  
|----------|-----------------|  
|Imagen de arranque|Tenga en cuenta los siguientes datos sobre la imagen de arranque que usará en la secuencia de tareas para capturar el sistema operativo:<br /><br /> - La arquitectura de la imagen de arranque debe ser adecuada para la arquitectura del equipo de destino. Por ejemplo, un equipo de destino x64 puede arrancar y ejecutar una imagen de arranque x86 o x64. Sin embargo, un equipo de destino x86 solo puede arrancar y ejecutar una imagen de arranque x86.<br />- Asegúrese de que la imagen de arranque contiene los controladores de almacenamiento masivo y de red necesarios para aprovisionar el equipo de destino.|  
|Distribuir todo el contenido asociado con la secuencia de tareas|Debe distribuir todo el contenido requerido por la secuencia de tareas a un punto de distribución como mínimo. Esto incluye la imagen de arranque, la imagen de sistema operativo y otros archivos asociados. El asistente recopila la información desde el punto de distribución al crear los medios independientes. Debe tener derechos de acceso de **lectura** para la biblioteca de contenido de dicho punto de distribución.  Para obtener más información, vea [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).|  
|Preparar la unidad USB extraíble|Para una unidad USB extraíble:<br /><br /> Si va a usar una unidad USB extraíble, dicha unidad debe estar conectada al equipo donde se ejecuta el asistente y debe ser detectada por Windows como un dispositivo de eliminación. El asistente escribe directamente en la unidad extraíble cuando crea los medios.|  
|Crear una carpeta de salida|Para un conjunto de CD o DVD:<br /><br /> Antes de ejecutar el Asistente para crear medio de secuencia de tareas para crear medios para un conjunto de CD o DVD, debe crear una carpeta para los archivos de salida creados por el asistente. El medio creado para un conjunto de CD o DVD se escribe como archivo .iso directamente en esa carpeta.|  

 Use el procedimiento siguiente para crear medios de captura.  

#### <a name="to-create-capture-media"></a>Para crear medios de captura  

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2. En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear medio de secuencia de tareas** para iniciar el Asistente para crear medio de secuencia de tareas.  

4. En la página **Seleccionar tipo de medio** , seleccione **Medio de captura**y, a continuación, haga clic en **Siguiente**.  

5. En la página **Tipo de medios** , especifique si se trata de una unidad flash o un conjunto de CD o DVD y luego haga clic para configurar los siguientes elementos:  

   - Si selecciona **Unidad flash USB**, especifique la unidad en la que quiere almacenar el contenido.  

   - Si selecciona **Conjunto de CD/DVD**, especifique la capacidad del medio y el nombre y la ruta de acceso de los archivos de salida. El asistente escribe los archivos de salida en esta ubicación. Por ejemplo: **\\\nombre de servidor\carpeta\archivo de salida.iso**  

      Si la capacidad de los medios es demasiado pequeña para almacenar todo el contenido, se crean varios archivos y debe almacenar el contenido en varios CD o DVD. Si se requieren varios medios, Configuration Manager agrega un número de secuencia al nombre de cada archivo de salida que crea. Además, si implementa una aplicación junto con el sistema operativo y la aplicación no cabe en un solo medio, Configuration Manager almacena la aplicación en varios medios. Cuando se ejecuta el medio independiente, Configuration Manager pide al usuario el siguiente medio en el que se almacena la aplicación.  

     > [!IMPORTANT]  
     >  Si selecciona una imagen .iso existente, el Asistente para crear medio de secuencia de tareas elimina la imagen de la unidad o el recurso compartido cuando pasa a la siguiente página del asistente. Se elimina la imagen existente incluso si, a continuación, se cancela al asistente.  

     Haga clic en **Siguiente**.  

6. En la página **Imagen de arranque** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

   > [!IMPORTANT]  
   >  La arquitectura de la imagen de arranque que especifique debe ser adecuada para la arquitectura del equipo de referencia. Por ejemplo, un equipo de referencia x64 puede arrancar y ejecutar una imagen de arranque x86 o x64. Sin embargo, un equipo de referencia x86 puede arrancar y ejecutar únicamente una imagen de arranque x86.  

   -   En el cuadro **Imagen de arranque** , especifique la imagen de arranque para iniciar el equipo de referencia.  

   -   En el cuadro **Punto de distribución** , especifique el punto de distribución donde reside la imagen de arranque. El asistente recupera la imagen de arranque desde el punto de distribución y la escribe en el medio.  

       > [!NOTE]  
       >  Debe tener derechos de acceso de lectura en la biblioteca de contenido del punto de distribución.  

7. Complete el asistente.  
