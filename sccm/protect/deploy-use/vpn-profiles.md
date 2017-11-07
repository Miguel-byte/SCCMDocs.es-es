---
title: Perfiles de VPN
titleSuffix: Configuration Manager
description: "Obtenga información sobre cómo usar perfiles de VPN en System Center Configuration Manager para implementar la configuración de VPN en los usuarios de la organización."
ms.custom: na
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
caps.latest.revision: "6"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 02d9178dbfe8cb00d38367d0dfcb2f521d4c26a0
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>Perfiles de VPN en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


Use perfiles de VPN en System Center Configuration Manager (también conocido como ConfigMgr o SCCM) para implementar la configuración de VPN en los usuarios de la organización. Mediante la implementación de esta configuración, se minimiza la intervención del usuario final necesaria para conectarse a los recursos de la red de la empresa.  

 Por ejemplo, quiere aprovisionar todos los dispositivos que ejecutan el sistema operativo Windows RT con la configuración necesaria para conectarse a un recurso compartido de archivos de la red corporativa. Puede crear un perfil de VPN que contiene la configuración necesaria para conectarse a la red corporativa y, después, implementar este perfil en todos los usuarios de la jerarquía que tienen dispositivos que ejecutan Windows RT. Los usuarios de dispositivos Windows RT verán la conexión VPN en la lista de redes disponibles y pueden conectarse a esta red con un esfuerzo mínimo.  

 Cuando cree un perfil de VPN, puede incluir una amplia gama de opciones de seguridad, incluidos certificados para la validación del servidor y la autenticación del cliente aprovisionados mediante perfiles de certificado de System Center Configuration Manager. Para obtener más información sobre los perfiles de certificado, consulte [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Perfiles de certificado en Configuration Manager).  

 En las secciones siguientes se explica qué dispositivos se pueden configurar con perfiles de VPN si se usa Configuration Manager.

 Consulte [VPN profiles on mobile devices](/sccm/mdm/deploy-use/create-vpn-profiles) (Perfiles de VPN en dispositivos móviles) para revisar los dispositivos que puede configurar mediante Configuration Manager con Microsoft Intune.  

## <a name="vpn-profiles-when-using-configuration-manager"></a>Perfiles de VPN en Configuration Manager  
 En la tabla siguiente se describen los perfiles de VPN que se pueden configurar para varias plataformas de dispositivo.  

|Tipo de conexión|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|No|No|No|No|  
|**Pulse Secure**|Sí|No|Sí|Sí|  
|**F5 Edge Client**|Sí|No|Sí|Sí|  
|**Dell SonicWALL Mobile Connect**|Sí|No|Sí|Sí|  
|**VPN móvil de punto de comprobación**|Sí|No|Sí|Sí|  
|**Microsoft SSL (SSTP)**|Sí|Sí|Sí|No|  
|**Microsoft Automatic**|Sí|Sí|Sí|No|  
|**IKEv2**|Sí|Sí|Sí|No|  
|**PPTP**|Sí|Sí|Sí|No|  
|**L2TP**|Sí|Sí|Sí|No|  

### <a name="next-steps"></a>Pasos siguientes  
 Use los temas siguientes para planear, configurar, operar y mantener perfiles de VPN en Configuration Manager.  

-   [Requisitos previos de los perfiles de VPN en System Center Configuration Manager](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Seguridad y privacidad de los perfiles de VPN en System Center Configuration Manager](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
