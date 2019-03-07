---
title: MDM local
titleSuffix: Configuration Manager
description: Obtenga información sobre la administración de dispositivos móviles local, una solución de administración de dispositivos en Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49e07a7ebe6ec53d61ea9e2ee3bc941dd8561094
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558225"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>MDM local en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Administrador de configuración en el entorno local la administración de dispositivos móviles (MDM) es una solución de administración de dispositivos que se basa en las capacidades integradas de administración de sistema operativo del dispositivo. Esta característica se basa en el estándar de administración de dispositivos de Open Mobile Alliance (OMA) (DM). Infraestructura de Configuration Manager de su organización usa para administrar y mantener los dispositivos. En el entorno local MDM requiere Microsoft Intune configurar la capacidad de administración, pero solo es necesario para la suscripción. Intune se utiliza a veces para notificar a los dispositivos que busquen cambios de directiva, pero no se utiliza para administrar los dispositivos o almacenar datos acerca de ellos.  

![Concepto local](media/On-premises-conceptual.png)  

MDM local difiere de Microsoft Intune, que también se basa en capacidades integradas de OMA DM. Todas las funciones de administración en Intune se entregan a través de servicios en la nube. MDM local también difiere de la solución de administración basada en cliente que tradicionalmente ofrecida Configuration Manager. Se basa en una infraestructura similar, pero no usa el software cliente instalado por separado en los dispositivos que administra.  

> [!Note]  
> A partir de la versión 1810, una conexión a Intune ya no es necesaria para nuevas implementaciones de MDM local.<!--3607730, fka 1359124--> La organización sigue necesitando licencias de Intune para usar esta característica. Actualmente no se puede quitar la conexión de Intune de las implementaciones de MDM locales existentes. Para más información, vea la [entrada del blog de soporte técnico de Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

En la tabla siguiente se enumera las ventajas y desventajas de MDM local en comparación con la administración basada en cliente tradicional:  

|Ventajas|Desventajas|  
|----------------|-------------------|  
|**Infraestructura simplificada** : se necesitan menos roles de sistema de sitio.<br /><br /> **Más fácil de mantener** : porque la funcionalidad de administración está integrada en el sistema operativo del dispositivo, las nuevas versiones del software cliente no son necesarios cuando se introducen nuevas características de administración en el sistema de Configuration Manager.<br /><br /> **Local** : todos los datos y la administración se conservan de forma local.|**Menos funciones de administración de clientes** : no se necesita orquestación, medición de software, integración de terceros, secuenciación de tareas ni soporte técnico de Centro de software.<br /><br /> **Compatibilidad de dispositivos limitada** : actualmente en el entorno local MDM solo admite dispositivos que ejecutan Windows 10 y Windows 10 Mobile.|  

Los siguientes artículos proporcionan información que puede usar para planear, preparar e inscribir dispositivos para MDM local:  

- [Planear la MDM local](/sccm/mdm/plan-design/plan-on-premises-mdm)  

    Conozca los aspectos a tener en cuenta al configurar la infraestructura de Configuration Manager y planear la inscripción de dispositivos en MDM local  

- [Pasos de preparación para MDM local](/sccm/mdm/get-started/preparation-steps-for-on-premises-mdm)  

    Preparar Configuration Manager para MDM local. Configurar la suscripción de Microsoft Intune, configurar los certificados, instalar roles de sistema de sitio y configurar la inscripción del dispositivo.  

- [Inscribir dispositivos en MDM local](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  

    Descubra cómo inscribir dispositivos, cómo los usuarios pueden inscribir sus dispositivos y cómo se realiza la inscripción masiva con un paquete de inscripción.  

