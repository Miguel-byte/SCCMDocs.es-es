---
title: Depurar una secuencia de tareas
titleSuffix: Configuration Manager
description: Use la herramienta de depuración de secuencias de tareas para solucionar problemas de una secuencia de tareas.
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 4b60b0e1-ffa4-4fd5-864e-70a0546c8b3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 00c05b7023f90783fbdd741a354cfd6382f632ad
ms.sourcegitcommit: f7e4ff38d4b4afb49e3bccafa28514be406a9d7b
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2019
ms.locfileid: "69549564"
---
# <a name="debug-a-task-sequence"></a>Depurar una secuencia de tareas

<!--3612274-->

A partir de la versión 1906, el depurador de la secuencia de tareas es una nueva herramienta de solución de problemas. La secuencia de tareas se implementa en modo de depuración en una colección pequeña. Le permite recorrer la secuencia de tareas de una manera controlada para facilitar la investigación y la resolución de problemas. El depurador se ejecuta actualmente en el mismo dispositivo que el motor de secuencia de tareas, no es un depurador remoto.

> [!Note]  
> En esta versión de Configuration Manager, el depurador de la secuencia de tareas es una característica de versión preliminar. Para habilitarla, vea [Características de versión preliminar](/sccm/core/servers/manage/pre-release-features).  


## <a name="prerequisites"></a>Requisitos previos

- Actualice al cliente de Configuration Manager en el dispositivo de destino.

- Inicie sesión en el dispositivo de destino como usuario en el grupo de **administradores** local. El depurador solo se ejecuta para administradores.

- Actualice la imagen de arranque asociada a la secuencia de tareas para asegurarse de que tiene la versión más reciente del cliente.


## <a name="start-the-tool"></a>Iniciar la herramienta

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.

1. Seleccione una secuencia de tareas. En el grupo Implementación de la cinta, seleccione **Depurar**.

    > [!Tip]  
    > Como alternativa, establezca la variable **TSDebugMode** en `TRUE` en una colección en la que se haya implementado la secuencia de tareas, o bien en un objeto de equipo en el que también se hayan implementado. Cualquier dispositivo que tenga este conjunto de variables colocará cualquier secuencia de tareas implementada en el modo de depuración.

1. Cree una implementación de depuración. La configuración de implementación es la misma que la de una implementación de secuencia de tareas normal. Para obtener más información, vea [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence#process).

    > [!Note]  
    > Solo puede seleccionar una colección pequeña para una implementación de depuración. Solo se muestran las recopilaciones de dispositivos con 10 miembros o menos.


## <a name="use-the-tool"></a>Usar la herramienta

Cuando la secuencia de tareas se ejecuta en el dispositivo, se abre la ventana del depurador de secuencia de tareas, como en la captura de pantalla siguiente:

![Captura de pantalla del depurador de secuencia de tareas](media/3612274-tsdebug.png)

El depurador incluye los controles siguientes:

- **Paso**: desde la posición *actual*, ejecute solo el paso siguiente de la secuencia de tareas.  

    > [!Note]  
    > Cuando la secuencia de tareas está en modo de depuración, si un paso devuelve un error irrecuperable, la secuencia de tareas no produce un error normal. Este comportamiento ofrece la opción de volver a intentar un paso después de realizar un cambio externo.

- **Ejecutar**:desde la posición *actual*, ejecute la secuencia de tareas con normalidad hasta el final o el próximo punto de *interrupción*, o si hay error en un paso. Antes de usar esta acción, asegúrese de establecer los puntos de interrupción con la acción **establecer interrupción** .

- **Establecer actual**: seleccione un paso en el depurador y, después, seleccione **Establecer actual**. Esta acción mueve el puntero *actual* a ese paso. Esta acción permite omitir pasos o retroceder.  

    > [!Warning]  
    > El depurador no considera el tipo de paso cuando se cambia la posición actual en la secuencia. Algunos pasos pueden establecer variables de secuencia de tareas que se necesitan para la evaluación de condiciones en pasos posteriores. Si se ejecutan de forma desordenada, algunos pasos pueden producir un error o causar daños importantes en un dispositivo. Use esta opción bajo su responsabilidad.  

- **Establecer interrupción**: seleccione un paso en el depurador y, después, seleccione **Establecer interrupción**. Esta acción agrega un punto de *interrupción* al depurador. Cuando se **ejecuta** la secuencia de tareas, se detiene en un *punto de interrupción*.  

    - Antes de usar la acción **Ejecutar** , establezca puntos de interrupción.

    - Los puntos de interrupción no se guardan después de que se reinicie el equipo, como sucede con el paso [reiniciar el equipo](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer) . Por ejemplo, si inicia el depurador desde el centro de software para una secuencia de tareas de creación de imágenes, no establezca interrupciones en la fase de Windows PE. Cuando el equipo se reinicia en Windows PE, el depurador pausa la secuencia de tareas para que pueda establecer interrupciones.

- **Borrar todas las interrupciones**: quitar todos los puntos de interrupción.

- **Archivo de registro**: abre el archivo de registro de la secuencia de tareas actual, **archivo smsts. log**, con [CMTrace](/sccm/core/support/cmtrace). Puede ver las entradas del registro cuando el motor de secuencia de tareas está en espera del depurador.

- **Símbolo del sistema**: en Windows PE, abre un símbolo del sistema.

- **Cancelar**: cierra el depurador y produce un error en la secuencia de tareas.

- **Quit**: desasocie y cierre el depurador, pero la secuencia de tareas continúa ejecutándose con normalidad.

La ventana **variables de secuencia de tareas** muestra los valores actuales de todas las variables en el entorno de la secuencia de tareas. Para más información, vea [Task sequence variables](/sccm/osd/understand/task-sequence-variables) (Variables de secuencia de tareas). Si usa el paso [configurar variable de secuencia de tareas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) con la opción de **no mostrar este valor**, el depurador no muestra el valor de la variable. No se pueden editar los valores de las variables en el depurador.

> [!Note]
> Algunas variables de secuencia de tareas son solo para uso interno y no se incluyen en la documentación de referencia.

El depurador de la secuencia de tareas continúa ejecutándose después de un paso [reiniciar el equipo](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer) , pero debe volver a crear los puntos de interrupción. Aunque es posible que la secuencia de tareas no la necesite, dado que el depurador requiere la interacción del usuario, debe iniciar sesión en Windows para continuar. Si no inicia sesión después de una hora para continuar con la depuración, se produce un error en la secuencia de tareas.

También se detallan en una secuencia de tareas secundaria con el paso [Ejecutar secuencia de tareas](/sccm/osd/understand/task-sequence-steps#child-task-sequence) . La ventana del depurador muestra los pasos de la secuencia de tareas secundaria junto con la secuencia de tareas principal.


## <a name="known-issues"></a>Problemas conocidos

Si el destino es una implementación normal y una implementación de depuración en el mismo dispositivo a través de varias implementaciones, es posible que el depurador de la secuencia de tareas no se inicie.


## <a name="see-also"></a>Consulte también

- [Acerca de los pasos de la secuencia de tareas](/sccm/osd/understand/task-sequence-steps)
- [Variables de secuencias de tareas](/sccm/osd/understand/task-sequence-variables)
- [Uso de variables de secuencias de tareas](/sccm/osd/understand/using-task-sequence-variables)
- [Implementación de una secuencia de tareas](/sccm/osd/deploy-use/deploy-a-task-sequence)
