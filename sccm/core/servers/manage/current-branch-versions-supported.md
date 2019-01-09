---
title: Versiones de la rama actual
titleSuffix: Configuration Manager
description: Revise el historial de versiones de Configuration Manager y obtenga información sobre las fases del servicio ofrecido.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 35b5baec-d313-46aa-9d14-c443aa0d6c09
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c5d3635ee6d1ed4e9c3819e2cffc3ee5028953f5
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422205"
---
# <a name="support-for-configuration-manager-current-branch-versions"></a>Compatibilidad con versiones de la rama actual de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Microsoft tiene previsto publicar actualizaciones de la rama actual de Configuration Manager varias veces al año. Para las versiones de Configuration Manager anteriores a la 1710, se ofrece soporte técnico durante 12 meses. A partir de la versión 1710, cada versión de actualización sigue siendo compatible durante 18 meses a partir de la fecha de lanzamiento de disponibilidad general. Microsoft proporciona soporte técnico durante todo el período de soporte técnico. Hay dos fases de servicio distintas que dependen de la disponibilidad de la versión más reciente de la rama actual.  

- Fase de servicio de **actualizaciones críticas y de seguridad**: cuando se ejecuta la versión más reciente de la rama actual de Configuration Manager, se reciben actualizaciones críticas y seguridad.  

- Fase de servicio de **actualizaciones de seguridad (solo)**: después del lanzamiento de una versión nueva de la rama actual, Microsoft solo admite actualizaciones de seguridad a las versiones anteriores durante el resto del ciclo de vida de soporte técnico de esa versión (como se muestra en la Ilustración 1).  

  ![Gráfico de escala de tiempo de servicio y soporte técnico de Configuration Manager](media/CM_Servicing_support_timeline1.png)  
  Ilustración 1. Ejemplo de la superposición del ciclo de versiones del soporte técnico de mantenimiento de la rama actual. Este ejemplo sirve para ilustrar el ciclo y no representa una fecha de lanzamiento real o prevista.

> [!NOTE]  
>  La versión más reciente de la rama actual siempre se encuentra en la fase de servicio de **actualizaciones críticas y de seguridad**. Esta instrucción de compatibilidad significa que, si encuentra un defecto en el código que garantice una actualización crítica, debe tener instalada la versión más reciente de la rama actual para recibir una corrección. Las demás versiones compatibles de la rama actual solo podrán optar a recibir actualizaciones de seguridad.
> - Para las versiones 1710 y posterior, el soporte técnico finaliza después de que haya expirado el ciclo de vida de 18 meses de una versión de la rama actual.
> - Para la versión 1706 y posteriores, el soporte técnico finaliza después de expirar el ciclo de vida de 12 meses.
> 
> Actualice el entorno de Configuration Manager a la versión más reciente antes de que expire el soporte técnico de la versión actual.

Para obtener una lista de las versiones de la rama actual, vea [Detalles de la versión](/sccm/core/servers/manage/updates#version-details).

Para obtener más información sobre los números de versión y la disponibilidad como una actualización en la consola o una línea de base, vea [Versiones de línea de base y versiones de actualización](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions).
