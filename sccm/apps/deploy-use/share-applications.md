---
title: Uso compartido de aplicaciones en el Centro de software
titleSuffix: Configuration Manager
description: Comparta un vínculo a una aplicación en el Centro de software de System Center Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 309a369358789e1948ab7b17ddb0e3619ae1b129
ms.sourcegitcommit: 2504617dc4db90e205327d06cab32f050e88dbf2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2018
ms.locfileid: "51505166"
---
# <a name="share-an-application-from-software-center"></a>Uso compartido de una aplicación del Centro de software

*Se aplica a: System Center Configuration Manager (rama actual)* <!-- 1706 -->

Puede copiar un hipervínculo en una aplicación del Centro de software con el botón ![Compartir](media/share15.png)**Share** en la vista Detalles de la aplicación. Solo se pueden compartir hipervínculos de aplicaciones. Si la aplicación deja de estar disponible, el hipervínculo abrirá una ventana con un mensaje que indica que la aplicación no está disponible.

1. Elija **Aplicaciones**y, luego, seleccione la aplicación.
2. Haga clic en el botón ![Compartir](media/share15.png) **Share**.
3. Haga clic en **Copiar** en la ventana.
4. Pegue la URL en un correo electrónico para compartir la aplicación.  

> [!TIP]  
>  Para crear un vínculo en un correo electrónico de Outlook, pulse **Ctrl** + **K** y pegue la dirección URL.  
>  
> De forma predeterminada, Outlook muestra una alerta de seguridad del protocolo del Centro de software cuando el destinatario hace clic en el vínculo. Si quiere evitar este comportamiento en su entorno, agregue una clave de protocolo de confianza al registro. Por ejemplo, `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:`.  
