---
title: Configuraciones admitidas
titleSuffix: Configuration Manager
description: Identifique requisitos y configuraciones fundamentales para que pueda planear, implementar y mantener una implementación funcional de System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de769a24b44c5ab5e28035e96fef341aecd78006
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="supported-configurations-for-system-center-configuration-manager"></a>Configuraciones admitidas para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Como una solución local, System Center Configuration Manager usa los servidores, clientes, configuraciones de red y otros productos como Microsoft Intune, SQL Server y Azure.

La información de este tema y de los siguientes es esencial para ayudarle a identificar las configuraciones, requisitos y limitaciones fundamentales para que pueda planear, implementar y mantener una implementación funcional de Configuration Manager.  Esta información es específica de la infraestructura de dispositivos administrados, jerarquías y sitios de Configuration Manager.

Cuando una característica o capacidad de Configuration Manager requiere configuraciones más específicas, esa información se incluye en la documentación específica de la característica y complementa los detalles de configuración más generales.  

 Los productos y tecnologías que se describen en los temas siguientes son compatibles con Configuration Manager. En cambio, su inclusión en este contenido no implica una extensión de la compatibilidad con cualquier producto más allá del ciclo de vida de soporte individual de los productos. Los productos que están fuera de su ciclo de vida de soporte no se pueden usar con Configuration Manager. Para obtener más información sobre los ciclos de vida de soporte de Microsoft, visite el sitio web [Ciclo de vida de soporte de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270).  

> [!NOTE]  
>  Para obtener información sobre la directiva de ciclo de vida de soporte de Microsoft, visite el sitio web de preguntas más frecuentes sobre la directiva de ciclo de vida de soporte de Microsoft en [Directiva de ciclo de vida de soporte técnico: preguntas más frecuentes](http://go.microsoft.com/fwlink/p/?LinkId=31976).  

 Además, los productos y las versiones de los productos que no aparecen en los temas siguientes no son compatibles con System Center Configuration Manager a menos que se hayan anunciado en el [Blog de Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/).  En ocasiones, el contenido de este blog precede una actualización de este conjunto de documentación.


-  [Números de tamaño y escala](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Obtenga información sobre cuántos sitios, roles de sistema de sitio por sitio y clientes o dispositivos son compatibles en diferentes diseños de jerarquía con Configuration Manager.

-  [Requisitos previos de sitio y sistema de sitio](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Obtenga información sobre las configuraciones necesarias en un servidor de Windows para admitir diferentes tipos de sitio y roles de sistema de sitio.

-  [Sistemas operativos compatibles con servidores de sistema de sitio](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Obtenga información sobre qué sistemas operativos puede usar como servidor de sitio o servidor de sistema de sitio.

-  [Supported operating systems for clients and devices](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) (Sistemas operativos compatibles con clientes y dispositivos)  
Obtenga información sobre qué sistemas operativos puede administrar con Configuration Manager, incluidos Windows, Windows Embedded, Linux y UNIX, Mac y dispositivos móviles.

-  [Sistemas operativos compatibles con la consola](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Obtenga información sobre qué sistemas operativos pueden hospedar la consola de Configuration Manager para proporcionar un punto de acceso para administrar la implementación.  

-  [Compatibilidad con versiones de SQL Server](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Obtenga información sobre qué versiones de SQL Server pueden hospedar la base de datos del sitio y la base de datos de informes, así como las configuraciones necesarias y opcionales que puede usar.

-  [Opciones de alta disponibilidad](../../../protect/understand/high-availability-options.md)  
Obtenga información sobre las opciones que puede implementar al diseñar el entorno para ayudar a mantener un alto nivel de servicio disponible para la implementación de Configuration Manager.

-  [Hardware recomendado](../../../core/plan-design/configs/recommended-hardware.md)  
Obtenga información sobre las instrucciones que le ayudarán a identificar el hardware y las configuraciones adecuadas para hospedar los servicios fundamentales y los sitios de Configuration Manager.

-  [Compatibilidad con dominios de Active Directory](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Obtenga información sobre las configuraciones de dominio de Active Directory admitidas que Configuration Manager necesita y admite.

-  [Compatibilidad con las características de Windows y redes](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Obtenga información sobre las tecnologías de Windows admitidas (como BranchCache y la desduplicación de datos) y las limitaciones de su uso con Configuration Manager.

-  [Compatibilidad con entornos de virtualización](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Obtenga más información sobre cómo usar tecnologías de máquina virtual compatibles.
