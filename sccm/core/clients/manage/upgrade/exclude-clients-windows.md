---
title: Excluir actualizaciones de cliente | Windows | System Center Configuration Manager
description: "Obtenga información sobre cómo excluir clientes Windows de su actualización en System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: de5602179f3ac55b51133b8280a0143f1b0ff30e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-exclude-upgrading-clients-for-windows-computers-in-system-center-configuration-manager"></a>Cómo excluir la actualización de clientes para equipos Windows con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

A partir de la versión 1610, puede excluir una colección de clientes de la instalación automática de versiones de cliente actualizadas. Esto se aplica a la actualización automática y a otros métodos como la actualización basada en actualizaciones de software, los scripts de inicio de sesión y la directiva de grupo. Puede usar esto para una colección de equipos a la que haya que prestar una mayor atención a la hora de actualizar el cliente. Un cliente que esté en una colección excluida omite las solicitudes para instalar el software de cliente actualizado.

## <a name="configure-exclusion-for-automatic-upgrades"></a>Configurar la exclusión de las actualizaciones automáticas

1. En la consola de Configuration Manager, vaya a **Administración** > **Configuración del sitio** > **Sitios** y, después, haga clic en **Configuración de jerarquía**.

2. Haga clic en la pestaña **Actualización de cliente**.

3. Haga clic en la casilla **Excluir los clientes especificados de la actualización** y, en la colección de exclusión, seleccione la colección que quiere excluir. Solo puede seleccionar una colección para la exclusión.

4.  Haga clic en **Aceptar** para cerrar y guardar la configuración. Luego, después de que los clientes actualicen la directiva, los de la colección excluida ya no instalarán automáticamente las actualizaciones del software de cliente. Para obtener más información, consulte [How to upgrade clients for Windows computers (Cómo actualizar clientes para equipos Windows)](upgrade-clients-for-windows-computers.md).

![Configuración de exclusión de actualización automática](media/automatic_upgrade_exclusion.png)



>[!NOTE]
>Aunque la interfaz de usuario indica que no se actualizarán los clientes mediante ningún método, hay dos que se pueden usar para invalidar esta configuración. Se pueden usar la instalación de inserción de cliente y la instalación de cliente manual para invalidar esta configuración. Para obtener más detalles, vea la siguiente sección.

## <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Cómo actualizar un cliente que está en una colección excluida

Siempre que una colección está configurada para ser excluida, sus miembros solo pueden actualizar el software de cliente mediante uno de dos métodos que invalidan la exclusión:
 - **Instalación de inserción de cliente**: se puede usar la instalación de inserción de cliente para actualizar un cliente que está en una colección excluida. Se permite porque se considera la intención del administrador y permite actualizar los clientes sin quitar toda la colección de la exclusión.       

 - **Instalación de cliente manual**: puede actualizar manualmente los clientes que están en una colección excluida con el siguiente modificador de la línea de comandos con ccmsetup: ***/ignoreskipupgrade***

  Si intenta actualizar manualmente un cliente que es miembro de la colección excluida y no usa este modificador, el cliente no instalará el nuevo software de cliente. Para más información, vea [How to install Configuration Manager Clients Manually (Instalación manual de clientes de Configuration Manager)](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).

Para más información sobre los métodos de instalación de clientes, vea [How to deploy clients to Windows computers in System Center Configuration Manager (Implementar clientes en equipos Windows con System Center Configuration Manager)](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).
