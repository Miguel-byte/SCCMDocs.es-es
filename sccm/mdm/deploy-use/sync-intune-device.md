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
ms.collection: M365-identity-device-management
ms.openlocfilehash: eab8f812b8772be0812437359275b80702f5760c
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62227650"
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Sincronizar directivas en dispositivos inscritos con Intune de manera remota desde la consola de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


Puede solicitar una sincronización de directivas en un dispositivo inscrito con Intune desde la consola de Configuration Manager, en lugar de solicitar una sincronización desde la aplicación de portal de empresa en el propio dispositivo. 

Para realizar esta tarea:

1.  Seleccione un dispositivo en **Activos y compatibilidad** > **Información general** > **Dispositivos**.
2.  Haga clic en **Send Sync Request (Enviar solicitud de sincronización)** en el menú **Acciones de dispositivo remoto**.


Después de cinco a diez minutos, cualquier cambio en la directiva se sincronizará con el dispositivo. Puede ver la información del estado de la solicitud de sincronización en una nueva columna en las vistas del dispositivo denominada **Remote Sync State (Estado de la sincronización remota)**, así como en la sección de datos de detección del cuadro de diálogo **Propiedades** de cada dispositivo.
