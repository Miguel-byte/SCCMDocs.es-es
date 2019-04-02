---
title: Migración desde MDM híbrido
titleSuffix: Configuration Manager
description: MDM híbrida está en desuso, se requiere Intune independiente para la administración conjunta.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 456f32d5-8590-499f-a54d-d00618bc61f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 84625c12c9cac643fe5a895c066632f44ffeacdc
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "56755572"
---
# <a name="migrate-from-hybrid-mdm-for-co-management"></a>Migración desde MDM híbrida para la administración conjunta

La administración de dispositivos móviles (MDM) es una característica en desuso. La compatibilidad con MDM híbrida finaliza el 1 de septiembre de 2019. Para más información, consulte [MDM híbrida con Configuration Manager y Microsoft Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

Intune independiente es la topología de implementación recomendada y se requiere para la administración conjunta. Si quiere habilitar la administración conjunta, migre desde una configuración híbrida de Intune a Intune independiente. 

En el siguiente vídeo, Andrew McMurry, Jefe Principal de Programas, y Mayunk Jain, Jefe de Marketing de Productos Senior, abordan y demuestran la migración desde MDM híbrida:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Moving-From-Hybrid-MDM-To-Microsoft-Intune/player]



## <a name="how-to-do-it"></a>Cómo hacerlo

La migración a Intune independiente tendrá más éxito cuando se use un enfoque en fases. Con una migración en fases, se mueve un pequeño subconjunto de usuarios y dispositivos, mientras la mayoría de los usuarios y dispositivos se siguen administrando con MDM híbrida. Una vez que compruebe que la migración se realizó correctamente, puede empezar a migrar más recursos a Intune.

Para empezar la migración, use la [herramienta Microsoft Intune Data Importer](/sccm/mdm/deploy-use/migrate-import-data) para recopilar y automatizar el proceso de volver a crear los objetos desde Configuration Manager en el inquilino de Intune independiente. A continuación, cambie la entidad de MDM de un conjunto específico de usuarios y pruebe la funcionalidad en Intune independiente. Cuando se realice esta comprobación, cambie la entidad de MDM a Intune independiente para todos los usuarios.

> [!Important]  
> Si usa el acceso condicional local en Configuration Manager, esta funcionalidad actualmente requiere Intune híbrido.  

Para más información sobre este proceso de migración, consulte [Migración de dispositivos y usuarios de MDM híbrida a Intune independiente](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).



## <a name="case-studies"></a>Casos prácticos

Microsoft IT recientemente movió a 130 000 usuarios de Intune híbrido a Intune independiente en tres meses. Para más información, consulte el vídeo donde se explica [cómo Microsoft usa el acceso condicional: Endpoint Zone 1812](https://youtu.be/offk-KH7eIA?t=651). Este vídeo es una conversación entre el Vicepresidente Corporativo de Microsoft, Brad Anderson, y Bret Arsenault, Director de Seguridad de Información Principal, que supervisó personalmente la migración. 

Una empresa farmacéutica de gran tamaño movió a 10 000 usuarios de Intune híbrido a Intune independiente en pocas semanas.

Una gran empresa de consultoría de TI de India migró a 40 000 usuarios de Intune híbrido a Intune independiente en menos de un mes.



## <a name="contact-fasttrack"></a>Póngase en contacto con FastTrack

Si necesita ayuda para migrar desde MDM híbrida en cualquier punto del proceso, vaya a [Microsoft FastTrack](https://Microsoft.com/FastTrack/), inicie sesión y solicite ayuda. 

Para más información, consulte [Ayuda de FastTrack](/sccm/comanage/quickstart-fasttrack). 

