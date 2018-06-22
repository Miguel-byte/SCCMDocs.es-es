---
title: Administración de una suscripción a Intune
titleSuffix: Configuration Manager
description: Administre una suscripción a Intune asociada a System Center Configuration Manager.
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9b494767-68c1-47b1-9a86-591bff0ad491
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1b8390faa557f37b2ee148299079df81d3c13299
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346746"
---
# <a name="manage-an-intune-subscription-associated-with-system-center-configuration-manager"></a>Administración de una suscripción a Intune asociada a System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Si agrega una suscripción de Microsoft Intune (una suscripción de prueba o suscripción de pago) a Configuration Manager y luego necesita cambiar a otra suscripción de Intune, debe eliminar tanto la **suscripción a Microsoft Intune** como el **punto de conexión de servicio** desde la consola de Configuration Manager antes de poder agregar una nueva suscripción.

> [!NOTE]
> Solamente puede configurar una suscripción a Intune a la vez en la administración de dispositivos móviles híbrida.

## <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Cómo eliminar una suscripción a Intune en Configuration Manager

> [!IMPORTANT]
>  Al eliminar la suscripción se elimina todo el contenido, incluidas las inscripciones de usuario, las directivas y las implementaciones de aplicaciones configuradas para dispositivos administrados por la suscripción a Intune.

1.  En la consola de Configuration Manager, vaya a **Administración** > **General** > **Cloud Services** > **Suscripciones a Microsoft Intune**.

2.  Haga clic con el botón derecho en la **Suscripción a Microsoft Intune** que se muestra y, luego, haga clic en **Eliminar**.

3.   En el asistente, haga clic en **Remove Microsoft Intune Subscription from Configuration Manager** (Quitar suscripción a Microsoft Intune de Configuration Manager), en **Siguiente** y, después, otra vez en **Siguiente** para quitar la suscripción.


## <a name="how-to-remove-the-service-connection-point-role"></a>Cómo quitar el rol de punto de conexión de servicio

1.  Vaya a **Administración** > **General** > **Configuración de sitio** > **Servidores y roles de sistema de sitio**.

2.  Seleccione el servidor que hospeda el rol **Punto de conexión de servicio**.

3.  En la lista **Roles del sistema de sitio**, seleccione **Punto de conexión de servicio** y haga clic en **Quitar rol** en la cinta de opciones. Confirme que desea quitar el rol. Se elimina el punto de conexión de servicio.

Ahora puede crear un nuevo punto de conexión de servicio, agregar una nueva suscripción de Intune a Configuration Manager y establecer Configuration Manager como la entidad de MDM.

## <a name="how-to-change-mdm-authority-to-intune"></a>Cómo cambiar la entidad de MDM a Intune
A partir de la versión 1610 de Configuration Manager y la versión 1705 de Microsoft Intune, puede cambiar la entidad de MDM sin tener que ponerse en contacto con el soporte técnico de Microsoft y sin necesidad de anular y volver a crear la inscripción de sus dispositivos administrados existentes. Para obtener más información, consulte [Cambio de la entidad de MDM](/sccm/mdm/deploy-use/change-mdm-authority).
