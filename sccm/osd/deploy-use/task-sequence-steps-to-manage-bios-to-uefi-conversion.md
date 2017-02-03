---
title: "Pasos de la secuencia de tareas para administrar la conversión de BIOS a UEFI | Configuration Manager"
description: "Obtenga información sobre cómo personalizar una secuencia de tareas de implementación de sistema operativo para preparar una partición FAT32 para la transición a UEFI."
ms.custom: na
ms.date: 11/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c92d88517b4e1d54add489a53cd34b0f23be0c4c
ms.openlocfilehash: 04951b3ed50206941850ddcc893fcf9c9596f89f


---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Pasos de la secuencia de tareas para administrar la conversión de BIOS a UEFI
A partir de la versión 1610 de Configuration Manager, ahora puede personalizar una secuencia de tareas de implementación de sistema operativo con una nueva variable, TSUEFIDrive, para que el paso **Reiniciar el equipo** prepare una partición FAT32 en la unidad de disco duro para la transición a UEFI. En el procedimiento siguiente se proporciona un ejemplo de cómo crear pasos de secuencia de tareas para preparar la unidad de disco duro para la conversión de BIOS en UEFI.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Para preparar la partición FAT32 para la conversión a UEFI:
En una secuencia de tareas existente para instalar un sistema operativo, agregue un nuevo grupo con pasos para realizar la conversión de BIOS a UEFI.

1. Cree un nuevo grupo de secuencia de tareas después de los pasos para capturar archivos y configuraciones y antes de los pasos para instalar el sistema operativo. Por ejemplo, cree un grupo después del grupo **Capturar archivos y configuraciones** denominado **BIOS a UEFI**.
2. En la pestaña **Opciones** del nuevo grupo, agregue una nueva variable de secuencia de tareas como una condición donde **_SMSTSBootUEFI** **No es igual** a **true**. Esto evita que los pasos del grupo se ejecuten cuando un equipo ya está en modo UEFI.

   ![Grupo BIOS a UEFI](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. Debajo del nuevo grupo, agregue el paso de secuencia de tareas **Reiniciar el equipo**. En **Especifique qué desea ejecutar después del reinicio**, seleccione **La imagen de arranque asignada a esta secuencia de tareas** para iniciar el equipo en Windows PE.  
4. En la pestaña **Opciones**, agregue una variable de secuencia de tareas como una condición donde **_SMSTSInWinPE es igual a false**. Esto evita que este paso se ejecute si el equipo ya está en Windows PE.

    ![Paso Reiniciar el equipo](../../core/get-started/media/restart-in-windows-pe.png)
5. Agregue un paso para iniciar la herramienta de OEM que va a convertir el firmware de BIOS a UEFI. Normalmente será un paso de secuencia de tareas **Ejecutar línea de comandos** con una línea de comandos para iniciar la herramienta de OEM.
6.  Agregue el paso de secuencia de tareas Formatear y crear particiones en el disco que va a crear particiones en la unidad de disco duro y a aplicarle formato. En el paso, haga lo siguiente:
    1.  Cree la partición FAT32 que se convertirá en UEFI antes de instalar el sistema operativo. Elija **GPT** para **Tipo de disco**.

       ![Paso Formatear y crear particiones en el disco](../media/format-and-partition-disk.png)
    2.  Vaya a las propiedades de la partición FAT32. Escriba **TSUEFIDrive** en el campo **Variable**. Cuando la secuencia de tareas detecte esta variable, se preparará para la transición a UEFI antes de reiniciar el equipo.

       ![Propiedades de la partición](../../core/get-started/media/partition-properties.png)
    3. Cree una partición NTFS que el motor de secuencia de tareas use para guardar su estado y para almacenar archivos de registro.
7.  Agregue el paso de secuencia de tareas **Reiniciar el equipo**. En **Especifique qué desea ejecutar después del reinicio**, seleccione **La imagen de arranque asignada a esta secuencia de tareas** para iniciar el equipo en Windows PE.  



<!--HONumber=Jan17_HO1-->


