---
title: Agregar roles de sistema de sitio
titleSuffix: Configuration Manager
description: Obtenga información sobre los roles del sistema de sitio de Configuration Manager y cómo agregarlos para ampliar las funciones y capacidades de un sitio.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2959d2b97088a2d92b861f0ca4a4d37d0df3e726
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334239"
---
# <a name="add-site-system-roles-for-system-center-configuration-manager"></a>Agregar roles de sistema de sitio para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Cada sitio de System Center Configuration Manager admite varios roles de sistema de sitio. Cada rol amplía la función y la capacidad del sitio para ofrecer servicios al sitio y para administrar dispositivos y usuarios. Todos los roles de sistema de sitio de un servidor de sistema de sitio deben pertenecer al mismo sitio.   

Configuration Manager no admite roles del sistema de sitio para varios sitios en un solo servidor de sistema de sitio.  

> [!TIP]  
>  Si no está familiarizado con los conceptos básicos de los roles del sistema de sitio o la diferencia entre servidores de sitio, servidores de sistema de sitio y roles del sistema de sitio, consulte [Aspectos básicos de System Center Configuration Manager](../../../../core/understand/fundamentals.md).  

 En los temas siguientes se explican los procedimientos y los detalles relacionados para la instalación de roles de sistema de sitio:  

-   [Install site system roles for System Center Configuration Manager (Instalar roles del sistema de sitio para System Center Configuration Manager)](../../../../core/servers/deploy/configure/install-site-system-roles.md)  

     Este tema contiene instrucciones básicas sobre cómo usar los dos asistentes en la consola para instalar nuevos roles de sistema de sitio.  

-   [Install cloud-based distribution points in Microsoft Azure for System Center Configuration Manager (Instalar puntos de distribución basados en la nube en Microsoft Azure para System Center Configuration Manager)](../../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  

    Si quiere usar Microsoft Azure para hospedar contenido que implementará en clientes, la información de este tema le resultará útil para configurar los archivos de certificado necesarios para habilitar Configuration Manager para que se comunique con la suscripción de Microsoft Azure y la use. Además, necesita configurar la resolución de nombres para permitir que los clientes encuentren los puntos de distribución basados en la nube.  

-   [Install site system roles for On-premises Mobile Device Management in System Center Configuration Manager (Instalar roles del sistema de sitio para la administración de dispositivos móviles local en System Center Configuration Manager)](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     Este tema le resultará útil para configurar correctamente los roles del sistema de sitio para administrar los dispositivos modernos con MDM local de Configuration Manager.  

-   [Opciones de configuración de roles de sistema de sitio para System Center Configuration Manager](../../../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md)  

     Algunos roles de sistema de sitio admiten configuraciones que necesitan más información de la que se puede explicar en la interfaz de usuario. En este tema encontrará esa información.  
