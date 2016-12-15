---
title: Configurar el control remoto | Documentos de Microsoft
description: Configure el control remoto en System Center Configuration Manager.
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 88828e68bc4aff216e83807ea8288c7d42c60cbd
ms.openlocfilehash: cbfa9dc6cb37518c0a561700272cc882b0041350


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>Configuración del control remoto en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

 En este procedimiento se describe cómo definir la configuración predeterminada de cliente para el control remoto y se aplica a todos los equipos de la jerarquía. Si quiere que esta configuración solo se aplique a algunos equipos, cree una configuración de cliente de dispositivo personalizada y asígnela a una recopilación que contenga los equipos en los que quiere usar una sesión de control remoto. Para más información, vea [Cómo establecer la configuración del cliente en Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md). 

Para usar Asistencia remota o Escritorio remoto, debe estar instalado y configurado en el equipo que ejecuta la consola de Configuration Manager. Para obtener más información sobre cómo instalar y configurar la Asistencia remota o el Escritorio remoto, consulte la documentación de Windows.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Para habilitar el control remoto y configurar el cliente  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

5.  En el cuadro de diálogo **Predeterminado**, elija **Herramientas remotas**.  

6.  Defina la configuración de cliente del control remoto, la Asistencia remota y el Escritorio remoto. Para obtener una lista de la configuración de cliente de las herramientas remotas que puede configurar, vea [Herramientas remotas](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

    Puede cambiar el nombre de la compañía que aparece en el cuadro de diálogo **Control remoto de ConfigMgr** mediante la configuración de un valor para **Nombre de organización mostrado en el Centro de software** en la configuración de cliente del **Agente de equipo** .  

 Los equipos cliente se configuran con estas opciones la próxima vez que descargan directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [How to manage clients in System Center Configuration Manager (Cómo administrar clientes en System Center Configuration Manager)](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Dec16_HO1-->


