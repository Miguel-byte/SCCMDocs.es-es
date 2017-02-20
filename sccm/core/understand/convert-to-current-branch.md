---
title: Actualizar la rama de mantenimiento a largo plazo a la rama actual | Microsoft Docs
description: Aprenda a convertir un sitio de rama de mantenimiento a largo plazo en un sitio de rama actual.
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 60631bc0346bd78d704e7129bb755af504c59b1b
ms.openlocfilehash: 6e7edc85630d22c5bbba1ff66bd1199903db76db

---


# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Actualizar la rama de mantenimiento a largo plazo a la rama actual

*Se aplica a: System Center Configuration Manager (rama de mantenimiento a largo plazo)*

Use este tema para aprender a actualizar (convertir) un sitio y la jerarquía que ejecuta la rama mantenimiento a largo plazo (LTSB) de Configuration Manager a la rama actual.

Si cuenta con un acuerdo Software Assurance actual (o derechos de licencia similares) que le concede derechos de uso de la rama actual, puede convertir la instalación de la LTSB a la rama actual.  Esta es una conversión unidireccional, ya que no se puede convertir un sitio de Rama actual a la LTSB.

Si tiene varios sitios, basta con convertir el sitio de nivel superior de la jerarquía. Una vez convertido el sitio de nivel superior:
- Se convierten automáticamente los sitios primarios secundarios.
-    Debe actualizar manualmente los sitios secundarios desde la consola de Configuration Manager.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Ejecutar el programa de instalación para convertir la Rama de mantenimiento a largo plazo
En el sitio de nivel superior de la jerarquía puede ejecutar el programa de instalación de Configuration Manager desde el medio de línea base correspondiente y seleccionar **Mantenimiento del sitio**.  Después, cuando aparezca la página de licencias, seleccione la opción de la Rama actual y complete el asistente.

Después de convertir el sitio a la Rama actual, podrán usarse las funciones y características que antes no estaban disponibles.

> [!NOTE]  
> El medio de línea base aplicable es un medio que tiene una versión igual o posterior a la instalación de LTSB.

Por ejemplo, dado que la LTSB se basa en la versión 1606, no puede usar el medio 1511 de línea base para convertir a la rama actual. En su lugar, ejecute el programa de instalación desde el mismo medio de línea base de la versión 1606 usado para instalar el sitio de LTSB y seleccione la opción de licencia de la Rama actual.  Como alternativa, si se ha publicado una línea base posterior de la Rama actual, puede ejecutar el programa de instalación desde ese medio de línea base.

Para obtener una lista de las versiones de línea base, vea **Baseline and update versions** (Versiones de línea base y actualización) en [Updates for System Center Configuration Manager](/sccm/core/servers/manage/updates) (Actualizaciones para System Center Configuration Manager).

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Usar la consola de Configuration Manager para convertir la rama de mantenimiento a largo plazo
Si el sitio ejecuta la LTSB, puede usar la siguiente opción de la consola de Configuration Manager para convertir a la rama actual:

 1. En la consola, vaya a **Administración** > **Configuración del sitio** > **Sitios** y, después, abra **Configuración de jerarquía**.  

 2. Seleccione la opción para convertir a la Rama actual y, después, haga clic en **Aplicar**.  

Después de convertir el sitio a la Rama actual, podrán usarse las funciones y características que antes no estaban disponibles.



<!--HONumber=Feb17_HO2-->


