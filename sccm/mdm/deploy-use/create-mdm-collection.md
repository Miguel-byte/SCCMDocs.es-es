---
title: Creación de una recopilación de MDM
titleSuffix: Configuration Manager
description: Cree una colección de MDM mediante System Center Configuration Manager.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3ec7c4cd58fbb717ab586d355ba4f0bf5f91fd06
ms.sourcegitcommit: ec4411fe30770f90128cf6cbd181047db90040cb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/14/2019
ms.locfileid: "57881663"
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>Creación de una colección de MDM con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (Rama actual)*

Se necesita una recopilación de usuarios de Configuration Manager para especificar qué usuarios pueden inscribir dispositivos en la administración. Solo puede usar recopilaciones de usuarios (en lugar de recopilaciones de dispositivos) porque las licencias de Intune se asignan por usuario.

> [!NOTE]
> Para inscribir dispositivos con Intune, no es necesario asignar licencias a los usuarios en el centro de administración de Microsoft 365 o el portal de Azure Active Directory. Todo lo que necesita es incluir a los usuarios en una colección que se asocia a la suscripción de Intune (en un [paso posterior](configure-intune-subscription.md)).

Con fines de prueba, puede configurar una **regla directa** y agregar usuarios específicos que pueden inscribir dispositivos. En la consola de Configuration Manager, elija **Activos y compatibilidad** > **Recopilaciones de usuarios**, haga clic en la pestaña **Inicio** > grupo **Crear** y luego haga clic en **Crear recopilación de usuario**. Para una distribución más amplia, debe usar **reglas de consulta** para definir usuarios. Para obtener más información sobre las recopilaciones, consulte [Cómo crear recopilaciones](https://technet.microsoft.com/library/mt629371.aspx).

![Crear una recopilación de usuarios de MDM](../media/mdm-create-user-collection.png)

> [!div class="button"]
> [Paso siguiente >](confirm-dns.md)
