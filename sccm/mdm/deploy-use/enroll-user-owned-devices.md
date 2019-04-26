---
title: Inscripción de dispositivos propiedad del usuario para implementaciones híbridas
titleSuffix: Configuration Manager
description: Obtenga información sobre los diferentes métodos para inscribir dispositivos propiedad del usuario para implementaciones híbridas con Configuration Manager.
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2bdaa8a7-6a64-4b0e-b617-309dcd912c45
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b6d56309238acc2889ac39ab39d5982fb8d535c
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62282416"
---
# <a name="enroll-user-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Inscripción de dispositivos propiedad del usuario para implementaciones híbridas con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los dispositivos de los usuarios pueden incorporarse al sistema de administración mediante su inscripción, un proceso que suele conocerse como  	"Bring Your Own Device" o simplemente "BYOD". Para ello, los usuarios deben instalar la aplicación Portal de empresa e iniciar sesión en su dispositivo (iOS, Mac OS o Android), o bien agregar una cuenta profesional o educativa al dispositivo y unirse a un dominio (Windows). Este proceso inscribe el dispositivo con Intune, lo que proporciona al usuario acceso a los recursos administrados por Intune, y permite que Intune administre ciertas configuraciones del dispositivo, como la usada para requerir un PIN.

Para incorporar dispositivos al sistema de administración, el administrador debe [configurar la administración de dispositivos móviles](setup-hybrid-mdm.md) y [habilitar la inscripción](enable-platform-enrollment.md). Una vez habilitada la inscripción, los usuarios pueden inscribir sus propios dispositivos. Consulte [Cómo presentar Microsoft Intune a los usuarios finales](https://docs.microsoft.com/intune/end-user-educate) para conocer las consideraciones y los pasos que deben compartir con los usuarios.

Las empresas o los centros escolares que adquieran dispositivos pueden aprovechar las ventajas de los programas que permiten [administrar dispositivos corporativos](enroll-company-owned-devices.md).
