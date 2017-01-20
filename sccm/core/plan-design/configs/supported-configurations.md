---
title: Configuraciones admitidas | System Center Configuration Manager
description: "Identifique requisitos y configuraciones fundamentales para que pueda planear, implementar y mantener una implementación funcional de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 170bd941bd123b998dd5d6235359aee97adc06bd


---
# <a name="supported-configurations-for-system-center-configuration-manager"></a>Configuraciones admitidas para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Como una solución local, System Center Configuration Manager usa los servidores, clientes, configuraciones de red y otros productos como Microsoft Intune, SQL Server y Azure.

La información de este tema y los siguientes es esencial para identificar las configuraciones y requisitos o limitaciones fundamentales para que pueda planear, implementar y mantener una implementación funcional de Configuration Manager.  Esta información es específica de la infraestructura de jerarquías, dispositivos administrados y sitios de Configuration Manager. Cuando una característica o capacidad de Configuration Manager requiere configuraciones más específicas, esa información se incluirá con la documentación específica de la característica y complementa estos detalles de configuración compatible más generales.  

 Los productos y tecnologías que se detallan en los temas siguientes son compatibles con Configuration Manager. En cambio, su inclusión en este contenido no expresa una extensión de la compatibilidad con cualquier producto más allá del ciclo de vida de soporte individual de los productos. Los productos que están fuera de su ciclo de vida de soporte no se pueden usar con Configuration Manager. Para obtener más información sobre los ciclos de vida de soporte de Microsoft, visite el sitio web [Ciclo de vida de soporte de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270).  

> [!NOTE]  
>  Para obtener información sobre la directiva de ciclo de vida de soporte de Microsoft, visite el sitio web de preguntas más frecuentes sobre la directiva de ciclo de vida de soporte de Microsoft en [Directiva de ciclo de vida de soporte técnico: preguntas más frecuentes](http://go.microsoft.com/fwlink/p/?LinkId=31976).  

 Además, los productos y las versiones de los productos que no aparecen en los temas siguientes no son compatibles con System Center Configuration Manager a menos que se hayan anunciado en el [Blog de Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/).  En ocasiones, el contenido de este blog estará precedido de una actualización de este conjunto de documentación.


-  [Números de tamaño y escala](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Detalles sobre cuántos sitios, roles de sistema de sitio por sitio y clientes o dispositivos son compatibles en diferentes diseños de jerarquía de Configuration Manager.

-  [Requisitos previos de sitio y sistema de sitio](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Configuraciones necesarias en un servidor Windows para admitir diferentes tipos de sitio y roles de sistema de sitio.

-  [Sistemas operativos compatibles con los servidores de sistema de sitio](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Obtenga información sobre qué sistemas operativos puede usar como servidor de sitio o servidor de sistema de sitio.

-  [Supported operating systems for clients and devices](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) (Sistemas operativos compatibles con clientes y dispositivos)  
Obtenga información sobre qué sistemas operativos puede administrar con Configuration Manager, incluidos Windows, Linux y UNIX, Mac, sistemas operativos incrustados y dispositivos móviles.

-  [Sistemas operativos compatibles con la consola](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Obtenga información sobre qué sistemas operativos pueden hospedar la consola de Configuration Manager para proporcionar un punto de acceso para administrar la implementación.  

-  [Compatibilidad con versiones de SQL Server](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Enumera las versiones de SQL Server que pueden hospedar la base de datos del sitio y la base de datos de informes, así como las configuraciones necesarias y opcionales que puede usar.

-  [Opciones de alta disponibilidad](../../../protect/understand/high-availability-options.md)  
Obtenga información sobre las opciones que puede implementar al diseñar el entorno para ayudar a mantener un alto nivel de servicio disponible para la implementación de Configuration Manager.

-  [Hardware recomendado](../../../core/plan-design/configs/recommended-hardware.md)  
Instrucciones que le ayudarán a identificar el hardware y las configuraciones adecuadas para hospedar los servicios y sitios fundamentales de Configuration Manager.

-  [Compatibilidad con dominios de Active Directory](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Obtenga información sobre las configuraciones de dominio de Active Directory admitidas que requiere y admite Configuration Manager.

-  [Compatibilidad con las características de Windows y redes](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Configuration Manager admite varias tecnologías de Windows, como la desduplicación de datos y BranchCache. Obtenga información sobre las tecnologías compatibles y las limitaciones para su uso con Configuration Manager.

-  [Compatibilidad con entornos de virtualización](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Información para ayudarle a usar tecnologías de máquina virtual compatibles.



<!--HONumber=Nov16_HO1-->


