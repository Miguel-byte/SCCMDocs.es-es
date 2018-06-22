---
title: Eliminación de un punto de actualización de software
titleSuffix: Configuration Manager
description: Siga este procedimiento para quitar el rol de sistema de sitio del punto de actualización de software en un sitio desde la consola de Configuration Manager.
author: aczechowski
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 2486375c-d4a2-4cf2-9124-9bee02bbf173
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 585077c44b13d79da55e8ab140fd93998b8371c1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353576"
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
