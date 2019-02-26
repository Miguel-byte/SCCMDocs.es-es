---
title: Migración desde MDM híbrido
titleSuffix: Configuration Manager
description: MDM híbrida está en desuso, Intune independiente es necesaria para la administración conjunta.
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755572"
---
# <a name="migrate-from-hybrid-mdm-for-co-management"></a>Migración desde MDM híbrida para la administración conjunta

Administración híbrida de dispositivos móviles (MDM) es una característica en desuso. Soporte técnico para MDM híbrida finaliza en 1 de septiembre de 2019. Para obtener más información, consulte [MDM híbrida con Configuration Manager y Microsoft Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

Intune independiente es la topología de implementación recomendada y es necesario para la administración conjunta. Si desea habilitar la administración conjunta, migrar desde una configuración híbrida de Intune a Intune independiente. 

En el siguiente vídeo, Andrew McMurray del director de programas principal y director de marketing de productos senior Mayunk Jain discutan y demostración de migración de MDM híbrida:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Moving-From-Hybrid-MDM-To-Microsoft-Intune/player]



## <a name="how-to-do-it"></a>Para saber cómo hacerlo

La migración a Intune independiente será más éxito cuando use un enfoque por fases. Con una migración por fases, mover un pequeño subconjunto de usuarios y dispositivos mientras la mayoría de los usuarios y dispositivos se siguen administrando con MDM híbrida. Cuando haya comprobado que la migración es correcta, puede empezar a migrar más recursos a Intune.

Para comenzar la migración, use el [herramienta Microsoft Intune Data Importer](/sccm/mdm/deploy-use/migrate-import-data) para recopilar y automatizar el proceso de volver a crear los objetos de Configuration Manager en el inquilino de Intune independiente. A continuación, cambie la entidad de MDM para un conjunto específico de usuarios y probar la funcionalidad en Intune independiente. Cuando se realiza esta comprobación, cambiar la entidad MDM a Intune independiente para todos los usuarios.

> [!Important]  
> Si usa acceso condicional local en Configuration Manager, esta funcionalidad requiere actualmente Intune híbrido.  

Para obtener más información sobre este proceso de migración, consulte [migrar dispositivos y usuarios de MDM híbrida a Intune independiente](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).



## <a name="case-studies"></a>Casos prácticos

Microsoft IT se movió recientemente 130.000 usuarios de Intune híbrido a Intune independiente durante tres meses. Para obtener más información, consulte [cómo Microsoft usa acceso condicional: punto de conexión de zona 1812](https://youtu.be/offk-KH7eIA?t=651). Este vídeo es una conversación entre Microsoft vicepresidente corporativo de Brad Anderson y responsable de seguridad de director de información de Microsoft Bret Arsenault, que supervisaba personalmente la migración. 

Una gran empresa farmacéutica había movido 10.000 usuarios de Intune híbrido a Intune independiente en unas semanas.

Una gran empresa de consultoría de TI en India migra 40.000 usuarios de Intune híbrido a Intune independiente en menos de un mes.



## <a name="contact-fasttrack"></a>Póngase en contacto FastTrack

Si necesita asistencia de migración de MDM híbrida en cualquier momento en el proceso, vaya a [Microsoft FastTrack](https://Microsoft.com/FastTrack/), inicie sesión y solicitar asistencia. 

Para obtener más información, consulte [obtener ayuda de FastTrack](/sccm/comanage/quickstart-fasttrack). 

