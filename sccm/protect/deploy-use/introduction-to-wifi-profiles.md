---
title: "Introducción a los perfiles de Wi-Fi | System Center Configuration Manager"
description: "Obtenga información sobre cómo usar perfiles de Wi-Fi en System Center Configuration Manager para implementar la configuración de red inalámbrica para los usuarios de su organización."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 86725460-c2f3-49ed-90aa-6b2724d34d69
caps.latest.revision: 8
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 30fefb291a6fccb630d5e3272ce7266339c9139c


---
# <a name="introduction-to-wi-fi-profiles-in-system-center-configuration-manager"></a>Introducción a los perfiles de Wi-Fi en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use perfiles de Wi-Fi en System Center Configuration Manager para implementar la configuración de red inalámbrica para los usuarios de su organización. Mediante la implementación de estas opciones, se minimiza la intervención del usuario final necesaria para conectarse a la red inalámbrica.  

 Por ejemplo, ha instalado una nueva red Wi-Fi denominada **Contoso Wi-Fi**. Quiere aprovisionar todos los dispositivos que ejecutan el sistema operativo iOS con la configuración necesaria para conectarse a esta red. Puede crear un perfil de Wi-Fi que contiene la configuración necesaria para conectarse a la red inalámbrica **Contoso Wi-Fi** . Después, puede implementar este perfil para todos los usuarios que tienen dispositivos que ejecutan iOS. Los usuarios de dispositivos iOS ven la red de la compañía en la lista de redes inalámbricas y pueden conectarse fácilmente a esta red.  

 Puede configurar los siguientes tipos de dispositivos con perfiles de Wi-Fi:  

-   Dispositivos con Windows 8.1 de 32 bits  

-   Dispositivos con Windows 8.1 de 64 bits  

-   dispositivos con Windows RT 8.1  

-   Dispositivos con Windows Phone 8.1  

-   Dispositivos con Windows 10 Desktop o Mobile  

-   Dispositivos IPhone con iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos IPad con iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos Android con la versión 4  

> [!IMPORTANT]  
>  Para implementar perfiles en dispositivos Android, iOS, Windows Phone y Windows 8.1 o posterior inscritos, estos dispositivos deben inscribirse en Microsoft Intune. Para obtener información sobre cómo inscribir dispositivos, consulte [Administrar dispositivos móviles con Microsoft Intune](https://technet.microsoft.com/library/dn646962.aspx).  

 Cuando se crea un perfil de Wi-Fi, puede incluir una amplia gama de opciones de seguridad. Estas incluyen certificados para la validación de servidor y la autenticación de cliente que se han aprovisionado mediante perfiles de certificado de Configuration Manager. Para obtener más información sobre los perfiles de certificado, consulte [Perfiles de certificado en System Center Configuration Manager](introduction-to-certificate-profiles.md).  



<!--HONumber=Nov16_HO1-->


