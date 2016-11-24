---
title: Excluir carpetas del inventario de software | System Center Configuration Manager
description: Excluya carpetas del inventario de software en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 07328e086a09e924a4807b05759937929152bda9


---
# <a name="how-to-exclude-folders-from-software-inventory-in-system-center-configuration-manager"></a>Cómo excluir carpetas del inventario de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use los pasos siguientes para configurar el inventario de software de System Center Configuration Manager para su sitio.  

 Este procedimiento configura las opciones de cliente predeterminadas para el inventario de software y se aplicará a todos los equipos de la jerarquía. Si quiere que esta configuración solo se aplique a algunos equipos, cree una configuración de cliente de dispositivo personalizada y asígnela a una recopilación que contenga los equipos en los que quiere usar el inventario de software. Para obtener más información sobre cómo crear configuraciones de dispositivo personalizadas, consulte [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md) (Cómo configurar el cliente en System Center Configuration Manager).  

### <a name="to-configure-software-inventory"></a>Cómo configurar el inventario de software  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Configuración de cliente**.  

3.  Haga clic en **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5.  En el cuadro de diálogo **Configuración predeterminada** , haga clic en **Inventario de software**.  

6.  En la lista **Configuración de dispositivo** , configure los valores siguientes:  

    -   **Habilitar inventario de software en clientes**: en la lista desplegable, seleccione **Verdadero**.  

    -   **Programar inventario de software y recopilación de archivos**: configura el intervalo en el que los clientes recopilan archivos e inventario de software. Use el valor predeterminado de **7 días** o haga clic en **Programar** para configurar un intervalo personalizado.  

7.  Configure las opciones de cliente que necesite. Para obtener una lista de la configuración de cliente del inventario de software que puede configurar, consulte la sección [Software Inventory](../../../../core/clients/deploy/about-client-settings.md#BKMK_SoftInventoryDeviceSettings) (Inventario de software) del tema [About client settings in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) (Acerca de la configuración de cliente en System Center Configuration Manager).  

8.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configurar valor de cliente** .  

 Los equipos cliente se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, consulte [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md) (Cómo administrar clientes en System Center Configuration Manager).  



<!--HONumber=Nov16_HO1-->


