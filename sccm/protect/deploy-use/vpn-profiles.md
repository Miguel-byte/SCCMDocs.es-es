---
title: Perfiles de VPN
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo usar perfiles de VPN en System Center Configuration Manager para implementar la configuración de VPN en los usuarios de la organización.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 505a4f3c00bc69e115b4130d422e11d8dec3fe30
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500398"
---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>Perfiles de VPN en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

<!--1283610-->
Use perfiles de VPN en Configuration Manager para implementar la configuración de VPN en los usuarios de la organización. Mediante la implementación de esta configuración, se minimiza la intervención del usuario final necesaria para conectarse a los recursos de la red de la empresa.  

 Por ejemplo, quiere configurar todos los dispositivos iOS Windows 10 con las opciones de configuración necesarias para conectarse a un recurso compartido de archivos de la red corporativa. Puede crear un perfil de VPN con la configuración necesaria para conectarse a la red corporativa. Luego, implemente el perfil para todos los usuarios que tengan dispositivos Windows 10. Los usuarios ven la conexión VPN en la lista de redes disponibles y pueden conectarse sin apenas esfuerzo.  

 Cuando se crea un perfil de VPN, puede incluir una amplia gama de opciones de seguridad. Estas opciones incluyen certificados para la validación de servidor y la autenticación de cliente que se aprovisionan por medio de perfiles de certificado de Configuration Manager. Para obtener más información, consulte [Introduction to certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Introducción a perfiles de certificado en Configuration Manager).  

> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


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
