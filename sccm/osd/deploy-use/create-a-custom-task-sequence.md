---
title: Crear una secuencia de tareas personalizada
titleSuffix: Configuration Manager
description: Edite una secuencia de tareas personalizada en System Center Configuration Manager para agregar pasos a la secuencia de tareas.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: add5ad2ed82e394b62613951fcaad6c38fee2465
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-custom-task-sequence-with-system-center-configuration-manager"></a>Crear una secuencia de tareas personalizada con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Cuando se crea una secuencia de tareas personalizada en System Center Configuration Manager, no contiene ningún paso de secuencia de tareas. Después de crear la secuencia de tareas, debe modificarla y agregar las etapas de secuencia de tareas que necesite.  

##  <a name="BKMK_CustomTS"></a> Crear una secuencia de tareas personalizada  
 Use el procedimiento siguiente para crear una secuencia de tareas personalizada.  

#### <a name="to-create-a-custom-task-sequence"></a>Para crear una secuencia de tareas personalizada  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear secuencia de tareas** para iniciar el Asistente para crear secuencia de tareas.  

4.  En la página **Crear una nueva secuencia de tareas** , seleccione **Crear una nueva secuencia de tareas personalizada**.  

5.  En la página **Información de secuencia de tareas** , especifique un nombre para la secuencia de tareas, una descripción de la secuencia de tareas y una imagen de arranque opcional para que use la secuencia de tareas. A continuación, complete el asistente.  

 Después de completar el Asistente para crear secuencia de tareas, Configuration Manager agrega la secuencia de tareas personalizada al nodo **Secuencias de tareas**. Ahora puede editar esta secuencia de tareas y agregar pasos.  

 Para obtener una lista de los pasos de secuencia de tareas disponibles, vea [Pasos de la secuencia de tareas](../understand/task-sequence-steps.md).  

 Para más información sobre cómo editar una secuencia de tareas, vea [Edit a task sequence (Editar una secuencia de tareas)](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

 Con mayor frecuencia, usará secuencias de tareas para automatizar tareas de implementación de sistema operativo, pero puede crear una secuencia de tareas personalizada para automatizar diversas tareas. Para más información, vea [Crear una secuencia de tareas para implementaciones que no son de sistema operativo](create-a-task-sequence-for-non-operating-system-deployments.md).  

 ## <a name="next-steps"></a>Pasos siguientes
 [Implementar la secuencia de tareas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
