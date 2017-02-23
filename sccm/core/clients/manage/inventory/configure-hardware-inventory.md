---
title: Configurar el inventario de hardware | Microsoft Docs
description: "Configure el inventario de hardware de todos los clientes o de una colección en System Center Configuration Manager."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: 5
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 05c27c7aa36e0b4236867766dab36125c31467b3
ms.openlocfilehash: deed112cca011b3b410c1197b7abf0f36a864f3c


---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>Cómo configurar el inventario de hardware en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Este procedimiento configura las opciones de cliente predeterminadas del inventario de hardware y se aplicará a todos los clientes de la jerarquía. Si quiere que esta configuración solo se aplique a algunos clientes, cree una configuración de cliente de dispositivo personalizada y asígnela a una recopilación que contenga los dispositivos que quiera usar para el inventario de hardware. Vea [Cómo configurar el cliente en System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Si un dispositivo cliente recibe la configuración de inventario de hardware de varios conjuntos de configuraciones de cliente, las clases de inventario de hardware de cada conjunto de configuraciones se combinarán cuando el cliente informe del inventario de hardware.  

### <a name="to-configure-hardware-inventory"></a>Cómo configurar el inventario de hardware  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

5.  En el cuadro de diálogo **Configuración predeterminada**, pulse **Inventario de hardware**.  

6.  En la lista **Configuración de dispositivo** , configure lo siguiente:  

    -   **Habilitar inventario de hardware en clientes**; seleccione **True**.  

    -   **Programación de inventario de hardware**; haga clic en **Programar** para especificar el intervalo en el que los clientes recopilan el inventario de hardware.  

7.  Configure otras opciones de [configuración del cliente de inventario de hardware](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) que necesite.  

Los dispositivos cliente se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [How to manage clients in System Center Configuration Manager (Cómo administrar clientes en System Center Configuration Manager)](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Jan17_HO1-->


