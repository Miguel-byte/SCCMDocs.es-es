---
title: Configurar el inventario de hardware | Microsoft Docs
description: "Configure el inventario de hardware de todos los clientes o de una colección en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: f39714e53e1b38c162e2c0418356d223432fdd87


---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>Cómo configurar el inventario de hardware en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use los pasos siguientes para configurar el inventario de hardware de System Center Configuration Manager de su sitio.  

 Este procedimiento configura las opciones de cliente predeterminadas del inventario de hardware y se aplicará a todos los clientes de la jerarquía. Si quiere que esta configuración solo se aplique a algunos clientes, cree una configuración de cliente de dispositivo personalizada y asígnela a una recopilación que contenga los dispositivos que quiera usar para el inventario de hardware. Para más información sobre cómo crear configuraciones de dispositivo personalizadas, vea [Cómo establecer la configuración del cliente en Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Si un dispositivo cliente recibe la configuración de inventario de hardware de varios conjuntos de configuraciones de cliente, las clases de inventario de hardware de cada conjunto de configuraciones se combinarán cuando el cliente informe del inventario de hardware.  

### <a name="to-configure-hardware-inventory"></a>Cómo configurar el inventario de hardware  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Configuración de cliente**.  

3.  Haga clic en **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5.  En el cuadro de diálogo **Configuración predeterminada** , haga clic en **Inventario de hardware**.  

6.  En la lista **Configuración de dispositivo** , configure lo siguiente:  

    -   **Habilitar inventario de hardware en clientes** : en la lista desplegable, seleccione **Verdadero**.  

    -   **Programación de inventario de hardware**: especifique el intervalo en el que los clientes recopilan el inventario de hardware. Use el valor predeterminado de **7 días** o haga clic en **Programar** para configurar un intervalo personalizado.  

7.  Configure el resto de opciones de cliente que necesite. Para obtener una lista de las opciones de cliente del inventario de hardware que puede configurar, vea la sección [Inventario de software](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) del tema [Acerca de la configuración de cliente en Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

8.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configuración predeterminada** .  

 Los dispositivos cliente se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [How to manage clients in System Center Configuration Manager (Cómo administrar clientes en System Center Configuration Manager)](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Dec16_HO3-->


