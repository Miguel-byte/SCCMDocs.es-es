---
title: Seguridad y privacidad de perfiles de VPN y Wi-Fi | Microsoft Docs
description: "Obtenga información sobre los procedimientos recomendados de seguridad para administrar perfiles de Wi-Fi y VPN de dispositivos en System Center Configuration Manager."
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 6d1d0a393a2ce614ae5f819475bd47b05e699b45
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Seguridad y privacidad de los perfiles de Wi-Fi y VPN en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

##  <a name="security-best-practices-for-wi-fi--and-vpn-profiles"></a>Procedimientos recomendados de seguridad para perfiles de Wi-Fi y VPN  
 Use los siguientes procedimientos recomendados de seguridad al administrar perfiles de Wi-Fi y VPN para dispositivos.  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Siempre que sea posible, elija las opciones más seguras admitidas por sus sistemas operativos cliente y la infraestructura de Wi-Fi y VPN.|Los perfiles de Wi-Fi y VPN constituyen un método muy práctico para administrar y distribuir de forma centralizada la configuración de Wi-Fi y VPN que sus dispositivos ya admiten. Configuration Manager no agrega ninguna característica de Wi-Fi o VPN.<br /><br /> Identifique, implemente y siga las recomendaciones de seguridad indicadas para los dispositivos y la infraestructura.|  

## <a name="privacy-information-for-wi-fi-profiles"></a>Información de privacidad de los perfiles de Wi-Fi  
 Puede usar perfiles de Wi-Fi y VPN para configurar la conexión de dispositivos cliente a servidores de Wi-Fi y VPN y después evaluar la compatibilidad de los dispositivos después de aplicar los perfiles. El punto de administración envía información de compatibilidad al servidor de sitio. La información se almacena en la base de datos del sitio. La información se cifra cuando los dispositivos la envían al punto de administración, pero no se almacena en formato cifrado en la base de datos del sitio. La base de datos conserva la información hasta que la tarea de mantenimiento **Eliminar datos antiguos de administración de configuración** la elimina. El intervalo de eliminación predeterminado es de 90 días, pero puede cambiarlo. La información de compatibilidad no se envía a Microsoft.  

 De manera predeterminada, los dispositivos no evalúan perfiles de Wi-Fi y VPN. Además, debe configurar los perfiles y luego implementarlos en usuarios.  

 Antes de configurar los perfiles de Wi-Fi o VPN, tenga en cuenta sus requisitos de privacidad.  
