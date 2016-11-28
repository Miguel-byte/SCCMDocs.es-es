---
title: Agregar roles del sistema de sitio | System Center Configuration Manager
description: "Entienda los roles del sistema de sitio de Configuration Manager y cómo agregarlos para ampliar la funcionalidad y la capacidad de un sitio."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
caps.latest.revision: 12
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f9437760936cdc4f9daad67205e635ab916207bd


---
# <a name="add-site-system-roles-for-system-center-configuration-manager"></a>Agregar roles de sistema de sitio para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Cada sitio de System Center Configuration Manager admite varios roles del sistema de sitio que amplían la funcionalidad y la capacidad del sitio para proporcionar servicios a usuarios y dispositivos y para administrar estos. Todos los roles de sistema de sitio de un servidor de sistema de sitio deben pertenecer al mismo sitio.   

Configuration Manager no admite roles del sistema de sitio para varios sitios en un solo servidor de sistema de sitio.  

> [!TIP]  
>  Si no está familiarizado con los conceptos básicos de los roles del sistema de sitio o la diferencia entre servidores de sitio, servidores de sistema de sitio y roles del sistema de sitio, vea [Fundamentals of System Center Configuration Manager (Conceptos básicos de System Center Configuration Manager)](../../../../core/understand/fundamentals.md).  

 En los temas siguientes se explican los procedimientos y los detalles relacionados para la instalación de roles de sistema de sitio:  

-   [Install site system roles for System Center Configuration Manager (Instalar roles del sistema de sitio para System Center Configuration Manager)](../../../../core/servers/deploy/configure/install-site-system-roles.md)  

     Este tema proporciona instrucciones básicas sobre el uso de los dos asistentes en la consola que puede usar para instalar nuevos roles de sistema de sitio.  

-   [Install cloud-based distribution points in Microsoft Azure for System Center Configuration Manager (Instalar puntos de distribución basados en la nube en Microsoft Azure para System Center Configuration Manager)](../../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  

    Si quiere usar Microsoft Azure para hospedar contenido implementado en los clientes, la información de este tema le ayudará a configurar los archivos de certificado necesarios para habilitar Configuration Manager a fin de que se comunique con la suscripción de Microsoft Azure y la use. Además, debe configurar la resolución de nombres para permitir que los clientes busquen los puntos de distribución basados en la nube.  

-   [Install site system roles for On-premises Mobile Device Management in System Center Configuration Manager (Instalar roles del sistema de sitio para la administración de dispositivos móviles local en System Center Configuration Manager)](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     Este tema le ayudará a configurar correctamente los roles del sistema de sitio para poder administrar los dispositivos modernos con MDM local de Configuration Manager.  

-   [Opciones de configuración de roles de sistema de sitio para System Center Configuration Manager](../../../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md)  

     Algunos roles de sistema de sitio admiten configuraciones que requieren más detalles que pueden explicarse dentro de la interfaz de usuario. En este tema se proporcionan los detalles.  



<!--HONumber=Nov16_HO1-->


