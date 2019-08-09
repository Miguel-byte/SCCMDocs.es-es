---
title: Crear grupos de aplicaciones
titleSuffix: Configuration Manager
description: Cree un grupo de aplicaciones que puede enviar a una colección de usuarios o dispositivos como una sola implementación en Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2698105d125abbbf1354cb045753586899e003ba
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537663"
---
# <a name="create-application-groups"></a>Crear grupos de aplicaciones

<!--3555907-->

A partir de la versión 1906, cree un grupo de aplicaciones que puede enviar a una colección de usuarios o dispositivos como una sola implementación. Los metadatos que especifique sobre el grupo de aplicaciones se ven en el Centro de software como una sola entidad. Puede ordenar las aplicaciones en el grupo para que el cliente las instale en un orden específico.

> [!Note]  
> En esta versión de Configuration Manager, los grupos de aplicaciones son una característica de versión preliminar. Para habilitarla, vea [Características de versión preliminar](/sccm/core/servers/manage/pre-release-features).  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Administración de aplicaciones** y seleccione el nodo **Grupo de aplicaciones**.  

1. En el grupo crear de la cinta de opciones, seleccione **Crear grupo de aplicaciones**.

1. En la página **Información general**, especifique información sobre el grupo de aplicaciones.  

1. En la página **Centro de software**, incluya la información que se muestra en el Centro de software.  

1. En la página **Grupo de aplicaciones**, seleccione **Agregar**. Seleccione una o más aplicaciones para este grupo. Puede cambiarlas de orden con las acciones **Subir** y **Bajar**.  

1. Complete el asistente.  

Implemente el grupo de aplicaciones con el mismo proceso que para una aplicación. Para obtener más información, consulte [Deploy applications](/sccm/apps/deploy-use/deploy-applications) (Implementar aplicaciones).

Si agrega una nueva aplicación al grupo después de implementar el grupo, debe distribuir por separado el nuevo contenido de la aplicación en los puntos de distribución.

Para solucionar problemas de una implementación de grupo de aplicaciones, use los siguientes archivos de registro en el cliente:

- **AppGroupHandler. log**
- **AppEnforce.log**
- **SettingsAgent. log**

> [!Important]  
> No cree ni implemente un grupo de aplicaciones hasta que actualice la jerarquía completa y los clientes de destino a la versión 1906 como mínimo.

### <a name="known-issues"></a>Problemas conocidos

- Las aplicaciones del grupo solo pueden contener tipos de implementación de **Windows Installer** o **script** . Establezca el comportamiento de instalación del tipo **de implementación en instalar para el sistema**.
- Solo puede implementar el grupo de aplicaciones en una recopilación de dispositivos.
