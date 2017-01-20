---
title: Configurar el control remoto | System Center Configuration Manager
description: Configure el control remoto en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: aea35afe970e20bc2b22f9ae3f413a3c735caae1


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>Configuración del control remoto en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Para poder usar el control remoto en System Center Configuration Manager, debe realizar los siguientes pasos de configuración.  

## <a name="how-to-enable-remote-control-and-configure-client-settings"></a>Cómo habilitar el control remoto y configurar el cliente  
 En este procedimiento se describe cómo definir la configuración predeterminada de cliente para el control remoto y se aplica a todos los equipos de la jerarquía. Si quiere que esta configuración solo se aplique a algunos equipos, cree una configuración de cliente de dispositivo personalizada y asígnela a una recopilación que contenga los equipos en los que quiere usar una sesión de control remoto. Para más información sobre cómo crear configuraciones de dispositivo personalizadas, vea [Cómo establecer la configuración del cliente en Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Para habilitar el control remoto y configurar el cliente  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Configuración de cliente**.  

3.  Haga clic en **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5.  En el cuadro de diálogo **Predeterminado**  , haga clic en **Herramientas remotas**.  

6.  Defina la configuración de cliente del control remoto, la Asistencia remota y el Escritorio remoto que necesite. Para obtener una lista de las opciones de cliente de las herramientas remotas que puede configurar, vea la sección [Herramientas remotas](../../../../core/clients/deploy/about-client-settings.md#BKMK_RemoteToolsDeviceSettings) del tema [Acerca de la configuración de cliente en Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

    > [!NOTE]  
    >  Puede cambiar el nombre de la compañía que aparece en el cuadro de diálogo **Control remoto de ConfigMgr** mediante la configuración de un valor para **Nombre de organización mostrado en el Centro de software** en la configuración de cliente del **Agente de equipo** .  

    > [!IMPORTANT]  
    >  Para usar Asistencia remota o Escritorio remoto, debe estar instalado y configurado en el equipo que ejecuta la consola de Configuration Manager. Para obtener más información sobre cómo instalar y configurar la Asistencia remota o el Escritorio remoto, consulte la documentación de Windows.  

7.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configuración predeterminada** .  

 Los equipos cliente se configuran con estas opciones la próxima vez que descargan directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [How to manage clients in System Center Configuration Manager (Cómo administrar clientes en System Center Configuration Manager)](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Nov16_HO1-->


