---
title: Excluir carpetas del inventario de software | Microsoft Docs
description: Excluya carpetas del inventario de software en System Center Configuration Manager.
ms.custom: na
ms.date: 12/04/2016
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
ms.sourcegitcommit: 6d1aabbde576f01de920468fd3ef372bd23be9df
ms.openlocfilehash: 7850b69cdccb0e897ee71b75255004bdc8d0ae97


---
# <a name="how-to-exclude-folders-from-software-inventory-in-system-center-configuration-manager"></a>Cómo excluir carpetas del inventario de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

 Este procedimiento configura las opciones de cliente predeterminadas para el inventario de software y se aplicará a todos los equipos de la jerarquía. Si quiere aplicar esta configuración solo a algunos equipos, cree una configuración de cliente de dispositivo personalizada y asígnela a una recopilación que contenga los equipos en los que quiere usar el inventario de software. Para más información sobre cómo crear configuraciones de dispositivo personalizadas, vea [Cómo establecer la configuración del cliente en Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

### <a name="to-configure-software-inventory"></a>Cómo configurar el inventario de software  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente**  **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

5.  En el cuadro de diálogo **Configuración predeterminada**, elija **Inventario de software**.  

6.  En la lista **Configuración de dispositivo** , configure los valores siguientes:  

    -   **Habilitar inventario de software en clientes**: en la lista desplegable, seleccione **Verdadero**.  

    -   **Programar inventario de software y recopilación de archivos**: configura el intervalo en el que los clientes recopilan archivos e inventario de software.   

7.  Configure las opciones de cliente que necesite. Para obtener una lista de la configuración de cliente del inventario de software que puede configurar, consulte la sección [Software Inventory](../../../../core/clients/deploy/about-client-settings.md#software-inventory) (Inventario de software) del tema [About client settings in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) (Acerca de la configuración de cliente en System Center Configuration Manager).  

 Los equipos cliente se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, consulte [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md) (Cómo administrar clientes en System Center Configuration Manager).  



<!--HONumber=Dec16_HO1-->


