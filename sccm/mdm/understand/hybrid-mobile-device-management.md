---
title: "Administración de dispositivos móviles híbridos (MDM) con Microsoft Intune"
titleSuffix: Configuration Manager
description: "Obtenga información sobre la administración híbrida de dispositivos móviles (MDM) con System Center Configuration Manager y Microsoft Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: "34"
caps.handback.revision: "0"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: da817ac299115c1151851d302c1935ad3f956bdf
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Administración híbrida de dispositivos móviles (MDM) con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*


Puede administrar dispositivos iOS, Windows y Android con Configuration Manager y Microsoft Intune. Todas las tareas de administración se controlan desde la consola de Configuration Manager donde realiza el resto de las tareas de administración que se integran perfectamente al servicio en línea de Microsoft Intune mediante Internet.  Puede usar Configuration Manager para permitir a los usuarios un acceso seguro y administrado a los recursos de la compañía en sus dispositivos. Mediante el uso de la administración de dispositivos, se protegen los datos de la compañía a la vez que se permite a los usuarios inscribir sus dispositivos corporativos o personales para tener acceso a los datos de la compañía. Funcionalidades de administración en dispositivos:

-   Retirar y borrar dispositivos
-   Definir la configuración de cumplimiento, como contraseñas, seguridad, movilidad, cifrado y comunicación inalámbrica
-   Implementar aplicaciones de línea de negocio (LOB) en los dispositivos
-   Implementar aplicaciones en los dispositivos que se conectan a la Tienda Windows, la Tienda Windows Phone, App Store o Google Play
-   Recopilar información de inventario de hardware
-   Recopilar información de inventario de software mediante el uso de informes integrados

Para leer sobre las nuevas características que están disponibles para MDM híbrido, consulte [What's new in hybrid mobile device management (Novedades en la administración híbrida de dispositivos móviles)](../understand/whats-new-in-hybrid-mobile-device-management.md).

En este documento se supone que usa Configuration Manager para administrar equipos y que quiere extender la consola de Configuration Manager con Intune para administrar dispositivos móviles. Para comprender las diferencias entre Intune y la administración híbrida de dispositivos móviles, consulte [Choose between Microsoft Intune standalone and hybrid mobile device management with System Center Configuration Manager (Elección entre Microsoft Intune independiente y la administración híbrida de dispositivos móviles con System Center Configuration Manager)](choose-between-standalone-intune-and-hybrid-mobile-device-management.md).

Tras extender Configuration Manager con Intune, puede inscribir y administrar dispositivos de propiedad corporativa o proporcionar permiso a los usuarios para inscribir sus dispositivos personales. También puede administrar dispositivos corporativos con Intune mediante Configuration Manager.

## <a name="hybrid-mdm-enrollment"></a>Inscripción híbrida de MDM
Para integrar dispositivos en la administración híbrida, esos dispositivos deben inscribirse al servicio. La manera en que los dispositivos inscriben dispositivos depende del tipo de dispositivo, la propiedad y el nivel de administración necesario.
- La inscripción "Bring Your Own Device" (BYOD) permite a los usuarios inscribir sus teléfonos personales, tabletas o equipos PC.
- La inscripción de dispositivos de propiedad corporativa (COD) habilita la administración de escenarios como el borrado remoto, los dispositivos compartidos o la afinidad de usuario para un dispositivo.
- Si usa [Exchange ActiveSync](../plan-design/device-enrollment-methods.md#mobile-device-management-with-exchange-activesync-and-configuration-manager), de manera local u hospedado en la nube, puede habilitar la administración simple de Intune sin la inscripción. Los equipos con Windows también pueden administrarse mediante el [software cliente de Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).
