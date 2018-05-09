---
title: Sincronización remota de directivas en dispositivos inscritos con Intune
titleSuffix: Configuration Manager
description: Obtener información sobre cómo sincronizar directivas en dispositivos inscritos con Intune desde la consola de Configuration Manager
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3ecd2c480ab67a82539edff6daa18ef0f93628c6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Sincronizar directivas en dispositivos inscritos con Intune de manera remota desde la consola de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


Puede solicitar una sincronización de directivas en un dispositivo inscrito con Intune desde la consola de Configuration Manager, en lugar de solicitar una sincronización desde la aplicación de portal de empresa en el propio dispositivo. 

Para realizar esta tarea:

1.  Seleccione un dispositivo en **Activos y compatibilidad** > **Información general** > **Dispositivos**.
2.  Haga clic en **Send Sync Request (Enviar solicitud de sincronización)** en el menú **Acciones de dispositivo remoto**.


Después de cinco a diez minutos, cualquier cambio en la directiva se sincronizará con el dispositivo. Puede ver la información del estado de la solicitud de sincronización en una nueva columna en las vistas del dispositivo denominada **Remote Sync State (Estado de la sincronización remota)**, así como en la sección de datos de detección del cuadro de diálogo **Propiedades** de cada dispositivo.
