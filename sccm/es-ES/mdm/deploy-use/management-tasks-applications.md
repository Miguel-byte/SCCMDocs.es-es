---
title: Administración de aplicaciones
titleSuffix: Configuration Manager
description: Administre aplicaciones en System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 26aff6a374da4c6822943083b24c1a7ac04ee91d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="manage-applications-in-system-center-configuration-manager"></a>Administración de aplicaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Al administrar dispositivos a través de la administración de dispositivos locales de Microsoft Intune o Configuration Manager, puede administrar estos tipos de aplicación adicionales:
- Paquete de aplicación de Windows Phone (archivo *.xap)
- Paquete de aplicación iOS (archivo *.ipa)
- Paquete de aplicación de Android (archivo *.apk)
- Paquete de aplicación para Android en Google Play
- Paquete de aplicación de Windows Phone (en la Tienda Windows Phone)
- Windows Installer a través de MDM
- Aplicación web

En esta sección se proporciona información detallada sobre la creación y administración de aplicaciones mediante MDM híbrida o MDM local.

[Tareas de administración de aplicaciones de System Center Configuration Manager](../../apps/deploy-use/management-tasks-applications.md) proporciona información más general sobre la administración de aplicaciones de System Center Configuration Manager y los tipos de implementación.

## <a name="deploying-and-monitoring-apps"></a>Implementación y supervisión de aplicaciones

La implementación y supervisión de aplicaciones en System Center Configuration Manager son los mismos procesos para dispositivos móviles que para dispositivos locales, como pueden ser equipos portátiles y equipos de escritorio. Puede leer los temas siguientes para obtener información general sobre la implementación y supervisión de aplicaciones:

- [Implementación de aplicaciones en System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md)
- [Supervisión de aplicaciones en System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md)

Estas son algunas consideraciones que se deben tener en cuenta durante la implementación y supervisión de aplicaciones y que son específicas de la administración de dispositivos móviles.

- Los dispositivos inscritos en MDM no admiten implementaciones simuladas, la experiencia del usuario o la configuración de programación.

- Puede asociar la implementación con una directiva de configuración de aplicación iOS si ya tiene una configurada. Consulte [Aplicar configuración a aplicaciones iOS con directivas de configuración de aplicaciones en System Center Configuration Manager](configure-ios-apps-with-app-configuration-policies.md).

### <a name="next-steps"></a>Pasos siguientes

Con el tiempo, le podría interesar realizar cambios en una aplicación, desinstalar una aplicación o reemplazar una aplicación implementada por una nueva. Lea [Actualizar y retirar aplicaciones mediante System Center Configuration Manager](../../apps/deploy-use/update-and-retire-applications.md) para comprender estas funcionalidades.
