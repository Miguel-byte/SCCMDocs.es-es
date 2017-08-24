---
title: Mantenimiento de las actualizaciones de software | Microsoft Docs
description: Para mantener las actualizaciones en Configuration Manager, puede programar la tarea de limpieza de WSUS o ejecutarla de forma manual.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
ms.openlocfilehash: 1590c623f7bc2f42a8617f110de5321212732a03
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="software-updates-maintenance"></a>Mantenimiento de las actualizaciones de software

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede programar y ejecutar la tarea de limpieza de WSUS desde la consola de Configuration Manager o puede ejecutar la tarea de limpieza de WSUS de forma manual desde las propiedades del componente de punto de actualización de software. Cuando se seleccione ejecutar la tarea de limpieza de WSUS, se ejecutará en la siguiente sincronización de actualizaciones de software. Las actualizaciones de software expiradas se establecerán en un estado rechazado en el servidor de WSUS y el agente de Windows Update de los equipos ya no las examinará. De forma predeterminada, el trabajo de limpieza de WSUS se ejecuta cada 30 días.  

#### <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Para programar y ejecutar el trabajo de limpieza de WSUS  

1.  En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Configuración del sitio** > **Sitios**.  

2.  Haga clic en **Configurar componentes de sitio** en el grupo **Configuración** y, a continuación, haga clic en **Punto de actualización de software** para abrir las propiedades del componente de punto de actualización de software.  

3.  Haga clic en la pestaña **Reglas de sustitución** , seleccione **Ejecutar el Asistente para la limpieza de WSUS**y, a continuación, haga clic en **Aceptar**.
