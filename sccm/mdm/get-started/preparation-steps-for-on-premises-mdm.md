---
title: "Pasos de preparación | MDM local | System Center Configuration Manager"
description: "Prepare la administración de dispositivos mediante la administración local de dispositivos móviles (MDM) en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
caps.latest.revision: 4
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 21bac2eae1aaea5bbd5897fcd4eb2aa11538aac7


---
# <a name="preparation-steps-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Pasos de preparación para la administración local de dispositivos móviles en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

La administración de dispositivos mediante la administración local de dispositivos móviles de System Center Configuration Manager requiere que la infraestructura de Configuration Manager se configure para que los roles de sistema de sitio (punto de proxy de inscripción, punto de inscripción, punto de administración de dispositivos y punto de distribución) puedan comunicarse a través de un canal de confianza con los dispositivos móviles que administrará.  

 Se deben llevar a cabo las siguientes tareas de alto nivel para preparar el sistema de Configuration Manager para la administración local de dispositivos móviles:  

-   [Configurar una suscripción de Microsoft Intune para la administración local de dispositivos móviles en System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md)  

     En esta tarea debe suscribirse a Microsoft Intune y agregar la suscripción a Configuration Manager mediante la consola de Configuration Manager. Este paso es necesario solo con fines de licencia. Intune no se usa para administrar los dispositivos ni para almacenar información de administración. La coordinación y la administración de dispositivos se llevan a cabo con la empresa de su organización mediante la infraestructura local de Configuration Manager.  

-   [Instalar roles de sistema de sitio para la administración local de dispositivos móviles en System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     En esta tarea, instala y configura los roles de sistema de sitio necesarios para administrar dispositivos con la infraestructura local de Configuration Manager. La administración local de dispositivos móviles requiere como mínimo los roles de sistema de sitio de punto de punto de proxy de inscripción, punto de inscripción, punto de administración de dispositivos y punto de distribución.  

-   [Configurar certificados para las comunicaciones de confianza para la administración local de dispositivos móviles en System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

     En esta tarea, se configura la infraestructura local de Configuration Manager para permitir comunicaciones de confianza (HTTPS) entre los dispositivos administrados y los servidores que hospedan los roles de sistema de sitio requeridos.  

-   [Configurar la inscripción del dispositivo para Administración de dispositivos móviles local en System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

     En esta tarea, otorga permiso a los usuarios para inscribir los equipos y dispositivos, e instala el certificado raíz de confianza en los dispositivos (normalmente unos que no están unidos a un dominio) para permitir conexiones HTTPS con los servidores del sistema de sitio.  



<!--HONumber=Nov16_HO1-->


