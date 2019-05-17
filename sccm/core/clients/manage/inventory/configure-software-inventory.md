---
title: Configuración del inventario de software
titleSuffix: Configuration Manager
description: Configure el inventario de software y excluya carpetas del inventario de software en Configuration Manager.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0ca174893aab04194b96969375e9d073a4fee7b9
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500106"
---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Cómo configurar el inventario de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Este procedimiento configura las opciones de cliente predeterminadas para el inventario de software y se aplica a todos los equipos de la jerarquía. Si solo quiere aplicar esta configuración a algunos clientes, cree una configuración de cliente de dispositivo personalizada y asígnela a una recopilación. Para más información sobre cómo crear configuraciones de dispositivo personalizadas, vea [Cómo establecer la configuración del cliente en Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).   

## <a name="to-configure-software-inventory"></a>Cómo configurar el inventario de software  

1. En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente**  **Configuración de cliente predeterminada**.  

2. En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

3. En el cuadro de diálogo **Configuración predeterminada**, elija **Inventario de software**.  

4. En la lista **Configuración de dispositivo** , configure los valores siguientes:  

   -   **Habilitar inventario de software en clientes**: en la lista desplegable, seleccione **Verdadero**.  

   -   **Programar inventario de software y recopilación de archivos**: configura el intervalo en el que los clientes recopilan archivos e inventario de software.   

5. Configure las opciones de cliente que necesite. En la sección [Inventario de software](../../../../core/clients/deploy/about-client-settings.md#software-inventory) del artículo [Acerca de la configuración de cliente en System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) se incluye una lista de la configuración de cliente.  

   Los equipos cliente se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [Cómo administrar clientes en System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

   > [!TIP]
   >   El código de error 80041006 en inventoryprovider.log significa que el proveedor de WMI no tiene memoria suficiente. Es decir, se ha alcanzado el límite de cuota de memoria para un proveedor y el proveedor de inventario no puede continuar.
   > En este caso, el agente de inventario crea un informe con 0 entradas, por lo que no se informa de ningún elemento de inventario. <br/>
   > Una posible solución para este error sería reducir el ámbito de la recopilación de inventario de software. En los casos en los que el error se produce después de limitar el ámbito de inventario, aumentar la propiedad [MemoryPerHost](https://blogs.technet.microsoft.com/askperf/2008/09/16/memory-and-handle-quotas-in-the-wmi-provider-service/) definida en la clase [_ProviderHostQuotaConfiguration](https://msdn.microsoft.com/library/aa394671) puede proporcionar una solución.

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>Cómo excluir carpetas del inventario de software  

1.  Con Notepad.exe, cree un archivo vacío llamado **Skpswi.dat**.  

2.  Haga clic con el botón derecho en el archivo **Skpswi.dat** y después haga clic en **Propiedades**. En las propiedades de archivo del archivo Skpswi.dat, seleccione el atributo **Oculto** .  

3.  Coloque el archivo **Skpswi.dat** en la raíz de cada estructura de carpeta o unidad de disco duro de cliente que quiera excluir del inventario de software.  

> [!NOTE]  
>  El inventario de software no inventariará la unidad de cliente de nuevo a menos que este archivo se elimine de la unidad del equipo cliente.
