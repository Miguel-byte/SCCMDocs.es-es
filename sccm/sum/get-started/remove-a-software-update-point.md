---

title: "Quitar un punto de actualización de software | Configuration Manager"
description: "Siga este procedimiento para quitar el rol de sistema de sitio del punto de actualización de software en un sitio desde la consola de Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 2486375c-d4a2-4cf2-9124-9bee02bbf173
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e95e3fc2aafde2d947f08d32e2b2130a313e7328


---
#  <a name="a-namebkmkremovesupa-remove-the-software-update-point-site-system-role"></a><a name="BKMK_RemoveSUP"></a> Quitar el rol de sistema de sitio de punto de actualización de software  

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede quitar el rol de sistema de sitio del punto de actualización de software en un sitio desde la consola de Configuration Manager. La directiva de cliente se actualiza para quitar el punto de actualización de software de la lista. Cuando quite el último punto de actualización de software del sitio, la lista de puntos de actualización de software no contendrá ningún punto de actualización de software y las actualizaciones de software quedarán, esencialmente, deshabilitadas en el sitio. Si tiene más de un punto de actualización de software en un sitio primario y quita el punto de actualización de software que está configurado como el origen de sincronización, debe elegir otro punto de actualización de software en el sitio para que sea el nuevo origen de sincronización.  

> [!NOTE]  
>  Si quita el rol de sitio de punto de actualización de software de un sistema de sitio, espere al menos 15 minutos antes de reinstalar el rol de sitio de punto de actualización de software.  

 Utilice el siguiente procedimiento para quitar un punto de actualización de software.  

#### <a name="to-remove-the-software-update-point"></a>Para quitar el punto de actualización de software  

1.  En la consola de **Configuration Manager** , haga clic en **Administración**.  

2.  En el área de trabajo Administración, expanda **Configuración del sitio**y, a continuación, haga clic en **Servidores y roles del sistema de sitios**.  

3.  Seleccione el servidor de sistema de sitio que tiene el punto de actualización de software que desea quitar y, a continuación, en **Roles del sistema de sitio**, seleccione **Punto de actualización de software**.  

4.  En la pestaña **Rol del sitio** , en el grupo **Rol del sitio** , haga clic en **Rol remoto**. Confirme que quiere quitar el punto de actualización de software o seleccione un nuevo origen de sincronización para los demás puntos de actualización de software en el sitio.  



<!--HONumber=Nov16_HO1-->


