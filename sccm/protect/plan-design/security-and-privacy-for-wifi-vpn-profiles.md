---
title: Seguridad y privacidad de perfiles de VPN y Wi-Fi
titleSuffix: Configuration Manager
description: Obtenga información sobre los procedimientos recomendados de seguridad para administrar perfiles de Wi-Fi y VPN de dispositivos en System Center Configuration Manager.
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: be81ff80f0da01916e2ec21a8ba1c7fe48fb8062
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142330"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Seguridad y privacidad de los perfiles de Wi-Fi y VPN en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

##  <a name="security-best-practices-for-wi-fi--and-vpn-profiles"></a>Procedimientos recomendados de seguridad para perfiles de Wi-Fi y VPN  
 Use los siguientes procedimientos recomendados de seguridad al administrar perfiles de Wi-Fi y VPN para dispositivos.  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Siempre que sea posible, elija las opciones más seguras admitidas por sus sistemas operativos cliente y la infraestructura de Wi-Fi y VPN.|Los perfiles de Wi-Fi y VPN constituyen un método muy práctico para administrar y distribuir de forma centralizada la configuración de Wi-Fi y VPN que sus dispositivos ya admiten. Configuration Manager no agrega ninguna característica de Wi-Fi o VPN.<br /><br /> Identifique, implemente y siga las recomendaciones de seguridad indicadas para los dispositivos y la infraestructura.|  

## <a name="privacy-information-for-wi-fi-profiles"></a>Información de privacidad de los perfiles de Wi-Fi  
 Puede usar perfiles de Wi-Fi y VPN para configurar la conexión de dispositivos cliente a servidores de Wi-Fi y VPN y después evaluar la compatibilidad de los dispositivos después de aplicar los perfiles. El punto de administración envía información de compatibilidad al servidor de sitio. La información se almacena en la base de datos del sitio. La información se cifra cuando los dispositivos la envían al punto de administración, pero no se almacena en formato cifrado en la base de datos del sitio. La base de datos conserva la información hasta que la tarea de mantenimiento **Eliminar datos antiguos de administración de configuración** la elimina. El intervalo de eliminación predeterminado es de 90 días, pero puede cambiarlo. La información de compatibilidad no se envía a Microsoft.  

 De manera predeterminada, los dispositivos no evalúan perfiles de Wi-Fi y VPN. Además, debe configurar los perfiles y luego implementarlos en usuarios.  

 Antes de configurar los perfiles de Wi-Fi o VPN, tenga en cuenta sus requisitos de privacidad.  
