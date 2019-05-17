---
title: Eliminación de un punto de actualización de software
titleSuffix: Configuration Manager
description: Siga este procedimiento para quitar el rol de sistema de sitio del punto de actualización de software en un sitio desde la consola de Configuration Manager.
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 2486375c-d4a2-4cf2-9124-9bee02bbf173
manager: dougeby
author: mestew
ms.author: mstewart
ms.collection: M365-identity-device-management
ms.openlocfilehash: 999ace880812c6baa3fd359433e4e929699c8612
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499762"
---
#  <a name="BKMK_RemoveSUP"></a> Quitar el rol de sistema de sitio de punto de actualización de software  

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede quitar el rol de sistema de sitio del punto de actualización de software en un sitio desde la consola de Configuration Manager. La directiva de cliente se actualiza para quitar el punto de actualización de software de la lista. Cuando quite el último punto de actualización de software del sitio, la lista de puntos de actualización de software no contendrá ningún punto de actualización de software y las actualizaciones de software quedarán, esencialmente, deshabilitadas en el sitio. Si tiene más de un punto de actualización de software en un sitio primario y quita el punto de actualización de software que está configurado como el origen de sincronización, debe elegir otro punto de actualización de software en el sitio para que sea el nuevo origen de sincronización.  

> [!NOTE]  
>  Si quita el rol de sitio de punto de actualización de software de un sistema de sitio, espere al menos 15 minutos antes de reinstalar el rol de sitio de punto de actualización de software.  

 Utilice el siguiente procedimiento para quitar un punto de actualización de software.  

#### <a name="to-remove-the-software-update-point"></a>Para quitar el punto de actualización de software  

1.  En la consola de **Configuration Manager** , haga clic en **Administración**.  

2.  En el área de trabajo Administración, expanda **Configuración del sitio**y, a continuación, haga clic en **Servidores y roles del sistema de sitios**.  

3.  Seleccione el servidor de sistema de sitio que tiene el punto de actualización de software que desea quitar y, a continuación, en **Roles del sistema de sitio**, seleccione **Punto de actualización de software**.  

4.  En la pestaña **Rol del sitio** , en el grupo **Rol del sitio** , haga clic en **Rol remoto**. Confirme que quiere quitar el punto de actualización de software o seleccione un nuevo origen de sincronización para los demás puntos de actualización de software en el sitio.  
