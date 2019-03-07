---
title: Preparar para MDM local
titleSuffix: Configuration Manager
description: Prepararse para administrar dispositivos con administración de dispositivos móviles local en Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fad5ce96b84b5a6edfafdead64cff0223009ebf8
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558055"
---
# <a name="preparation-steps-for-on-premises-mdm-in-configuration-manager"></a>Pasos de preparación para MDM local en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Para administrar dispositivos con administración de dispositivos móviles local de Configuration Manager (MDM), configure primero la infraestructura necesaria. Los roles de sistema de sitio requeridos necesitan comunicarse a través de un canal de confianza con los dispositivos móviles. Estas funciones incluyen el punto de proxy de inscripción, punto de inscripción, punto de administración de dispositivos y punto de distribución.

Las siguientes tareas de alto nivel son necesarios para preparar Configuration Manager para MDM local:  

- [Configurar una suscripción de Microsoft Intune para MDM local](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm)  

    Suscribirse a Microsoft Intune y, a continuación, agregar la suscripción a Configuration Manager a través de la consola de Configuration Manager. Este paso es necesario solo con fines de licencia. No se usa Intune para administrar los dispositivos o almacenar la información de administración. La coordinación y la administración de dispositivos se llevan a cabo con la empresa de su organización mediante la infraestructura local de Configuration Manager.  

    > [!Note]  
    > A partir de la versión 1810, una conexión a Intune ya no es necesaria para nuevas implementaciones de MDM local.<!--3607730, fka 1359124--> La organización sigue necesitando licencias de Intune para usar esta característica. Actualmente no se puede quitar la conexión de Intune de las implementaciones de MDM locales existentes. Para más información, vea la [entrada del blog de soporte técnico de Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

- [Instalar roles de sistema de sitio para MDM local](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm)  

    Instale y configure los sistemas de sitio necesarios para administrar dispositivos con la infraestructura de Configuration Manager en el entorno local. Como mínimo, esta característica requiere el punto de proxy de inscripción, punto de inscripción, punto de administración de dispositivos y roles de punto de distribución.  

- [Configurar los certificados de comunicaciones de confianza para MDM local](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  

    Configurar la infraestructura de Configuration Manager local para permitir a comunicaciones de confianza (HTTPS) entre los dispositivos administrados y los servidores que hospedan los roles de sistema de sitio requeridos.  

- [Configurar la inscripción de dispositivos para MDM local](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

    Conceder permiso a los usuarios para inscribir equipos y dispositivos. Instale el certificado raíz de confianza en dispositivos para permitir las conexiones HTTPS a los servidores de sistema de sitio. Normalmente, estos dispositivos no unidos al dominio.  

