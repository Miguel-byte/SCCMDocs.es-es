---
title: Exclusión de actualizaciones de cliente en Windows
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo excluir clientes Windows de su actualización en Configuration Manager.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7a16bc859006b0253459259d354a68e2ff1dec83
ms.sourcegitcommit: 2d38de4846ea47a03cc884cbd3df27db48f64a6a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2019
ms.locfileid: "70110151"
---
# <a name="how-to-exclude-clients-from-upgrade-in-configuration-manager"></a>Cómo excluir clientes Windows de su actualización en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede excluir una colección de clientes de la instalación automática de versiones de cliente actualizadas. Use esta exclusión para una colección de equipos a la que haya que prestar una mayor atención a la hora de actualizar el cliente. Un cliente que esté en una colección excluida omite las solicitudes para instalar el software de cliente actualizado.

Esta exclusión se aplica a los métodos siguientes:

- Actualización automática
- Actualización basada en actualización de software
- Scripts de inicio de sesión
- Directiva de grupo.

> [!NOTE]
> Aunque la interfaz de usuario indica que no se actualizarán los clientes mediante ningún método, hay dos que se pueden usar para invalidar esta configuración. Use la instalación de inserción de cliente y la instalación de cliente manual para invalidar esta configuración. Para obtener más información, consulte [Cómo actualizar un cliente que está en una colección excluida](#bkmk_override).

## <a name="bkmk_exclude"></a> Configuración de la exclusión

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Configuración del sitio**, seleccione el nodo **Sitios** y luego seleccione **Configuración de jerarquía** en la cinta.

2. Cambie a la pestaña **Actualización de cliente**.

3. Seleccione la opción **Excluir los clientes especificados de la actualización**. A continuación, seleccione la **colección de exclusión** que desea excluir. Solo puede seleccionar una colección para la exclusión.

4. Seleccione **Aceptar** para cerrar y guardar la configuración.

![Configuración de exclusión de actualización automática](media/automatic_upgrade_exclusion.png)

Una vez que los clientes de la colección excluida actualicen la directiva, no instalan automáticamente actualizaciones de cliente. Para obtener más información, consulte [How to upgrade clients for Windows computers (Cómo actualizar clientes para equipos Windows)](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers).

> [!NOTE]
> Los clientes excluidos continuarán descargando y ejecutando Ccmsetup, pero no se actualizarán.

Cuando se quita un cliente de la colección de exclusión, no se actualiza automáticamente hasta el siguiente ciclo de actualización automática.

## <a name="bkmk_override"></a> Actualización de un cliente excluido

Si un dispositivo es miembro de una colección que se ha excluido de la actualización, aún es posible actualizarlo mediante uno de los métodos siguientes:

- **Instalación de inserción de cliente**: Ccmsetup permite la instalación de inserción de cliente porque es su intención directa. Este método le permite actualizar un cliente sin quitarlo de la colección o quitar toda la colección de la exclusión.

- **Instalación de cliente manual**: Actualice manualmente un cliente excluido usando el siguiente parámetro de la línea de comandos de Ccmsetup: **/IgnoreSkipUpgrade**.

    Si intenta actualizar manualmente un cliente que es miembro de la colección excluida y no usa este parámetro, el cliente no se actualiza. Para obtener más información, vea [How to install Configuration Manager Clients Manually (Instalación manual de clientes de Configuration Manager)](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).

## <a name="see-also"></a>Consulte también

- [Actualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients)

- [Implementar clientes en equipos Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)

- [Cliente de interoperabilidad extendida](/sccm/core/understand/interoperability-client)
