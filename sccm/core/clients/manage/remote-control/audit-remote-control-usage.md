---
title: Auditar el uso del control remoto | Microsoft Docs
description: Audite el uso del control remoto en System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c975e69-0cc0-4afd-b7fb-b7182162a933
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 4259ecfca48ccdffa83247e9ab5a65b3f006c5d9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-audit-remote-control-usage-in-system-center-configuration-manager"></a>Cómo auditar el uso del control remoto en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede usar los informes de System Center Configuration Manager para ver información de auditoría del control remoto.  

 Para más información sobre cómo configurar la generación de informes en Configuration Manager, vea [Reporting in System Center Configuration Manager (Generación de informes en System Center Configuration Manager)](../../../../core/servers/manage/reporting.md).  

 Los dos informes siguientes están disponibles con la categoría **Mensajes de estado - Auditoría**:  

-   **Control remoto - Todos los equipos controlados remotamente por un usuario específico**: muestra un resumen de la actividad de control remoto iniciada por un usuario concreto.  

-   **Control remoto - Toda la información de control remoto**: muestra un resumen de los mensajes de estado sobre el control remoto de los equipos cliente.  

### <a name="to-run-the-report-remote-control---all-computers-remote-controlled-by-a-specific-user"></a>Para ejecutar el informe Control remoto - Todos los equipos controlados remotamente por un usuario específico  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Generación de informes**y, a continuación, haga clic en **Informes**.  

3.  En el nodo **Informes** , haga clic en la columna **Categoría** para ordenar los informes a fin de poder encontrar más fácilmente los informes de la categoría **Mensajes de estado - Auditoría**.  

4.  Seleccione el informe **Control remoto - Todos los equipos controlados remotamente por un usuario específico**y, a continuación, en la pestaña **Inicio** , en el **Grupo de informes**, haga clic en **Ejecutar**.  

5.  En la lista **Nombre de usuario** de **Control remoto - Todos los equipos controlados remotamente por un usuario específico**, especifique el usuario para el que quiere notificar la información de auditoría y, a continuación, haga clic en **Ver informe**.  

6.  Cuando haya terminado de consultar los datos en el informe, cierre la ventana del informe.  

### <a name="to-run-the-report-remote-control---all-remote-control-information"></a>Para ejecutar el informe Control remoto - Toda la información de control remoto  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Generación de informes**y, a continuación, haga clic en **Informes**.  

3.  En el nodo **Informes** , haga clic en la columna **Categoría** para ordenar los informes a fin de poder encontrar más fácilmente los informes de la categoría **Mensajes de estado - Auditoría**.  

4.  Seleccione el informe **Control remoto - Toda la información de control remoto**y, a continuación, en la pestaña **Inicio** , en el **Grupo de informes**, haga clic en **Ejecutar** para abrir la ventana **Control remoto - Toda la información de control remoto** .  

5.  Cuando haya terminado de consultar datos en el informe, cierre la ventana del informe.  
