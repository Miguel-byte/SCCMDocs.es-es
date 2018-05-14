---
title: Panel de ciclo de vida del producto
titleSuffix: Configuration Manager
description: Obtenga información sobre el panel de ciclo de vida del producto en System Center Configuration Manager.
ms.date: 02/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 8f24fcd2d75d34e2d2d69c9c54f4f47991be7301
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="use-the-product-lifecycle-dashboard-to-manage-microsoft-lifecycle-policy-in-system-center-configuration-manager"></a>Uso del panel de ciclo de vida del producto para administrar la directiva de ciclo de vida de Microsoft en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Technical Preview)*

A partir de la [versión 1802 de Technical Preview](/sccm/core/get-started/capabilities-in-technical-preview-1802), puede usar el panel de ciclo de vida del producto de Configuration Manager. El panel muestra el estado de la directiva de ciclo de vida de los productos de Microsoft instalados en los dispositivos administrados con Configuration Manager. El panel proporciona información acerca de los productos de Microsoft de su entorno, el estado de compatibilidad y la fechas de finalización del soporte técnico. Puede utilizar el panel para tener constancia de la disponibilidad del soporte técnico para cada producto. Le ayuda a planear cuándo actualizar los productos de Microsoft que utiliza antes de que llegue el fin del soporte actual.  

Para obtener más información acerca de la directiva de ciclos de vida de productos de Microsoft, consulte [Directiva de ciclos de vida de Microsoft](https://support.microsoft.com/en-us/lifecycle).

## <a name="prerequisites"></a>Requisitos previos 

 Para ver los datos en el panel del ciclo de vida del producto, se requiere lo siguiente: 
- Internet Explorer 9 o una versión posterior debe estar instalado en el equipo que ejecuta la consola de Configuration Manager. 
- Se requiere un punto de servicios de informes para la funcionalidad de hipervínculo en el panel dado que se vinculan a un informe de SQL Server Reporting Services. Para obtener más información, consulte [Reporting in System Center Configuration Manager](/sccm/core/servers/manage/reporting) (Generación de informes en System Center Configuration Manager). 
- El punto de sincronización de Asset Intelligence debe estar configurado y sincronizado. Para obtener más información, consulte [Configurar Asset Intelligence en System Center Configuration Manager](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).

Los datos del panel dependen de si tiene instalado el punto de sincronización de Asset Intelligence. El panel usa el catálogo de Asset Intelligence como metadatos para los títulos de productos. Los metadatos se comparan con los datos de inventario en la jerarquía. 

>[!NOTE]
>Si está configurando el punto de servicio de Asset Intelligence por primera vez, no olvide [habilitar las clases de inventario de hardware de Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence#BKMK_EnableAssetIntelligence). El panel del ciclo de vida depende de esas clases de inventario de hardware de Asset Intelligence y no mostrará datos hasta que los clientes hayan analizado y devuelto el inventario de hardware.  

## <a name="use-the-microsoft-product-lifecycle-dashboard"></a>Uso del panel del ciclo de vida de productos de Microsoft

El panel mostrará información sobre todos los productos actuales en función de los datos de inventario que recopile de los dispositivos administrados. Sin embargo, la información mostrada para los sistemas operativos y SQL Server se limita a las siguientes versiones:

- Windows Server 2008 y versiones posteriores
- Windows XP y versiones posteriores
- SQL Server 2008 y versiones posteriores

Para tener acceso al panel de ciclo de vida, en la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Asset Intelligence** > **Ciclo de vida del producto**.

>[!NOTE]
>Los datos del panel se basan en el sitio al que se conecta la consola de Configuration Manager. Si la consola se conecta a su sitio de nivel superior, verá datos en toda la jerarquía. Cuando se conecta a un sitio primario secundario, se mostrarán solamente los datos de ese sitio.

### <a name="product-lifecycle-dashboard"></a>Panel de ciclo de vida del producto

![Panel de ciclo de vida del producto](/sccm/core/clients/manage/asset-intelligence/media/product-lifecycle-dashboard.png)

El panel presenta los iconos siguientes: 
- **Los cinco principales productos cuyo ciclo de vida ha expirado** este icono es una vista de datos consolidados de los productos cuyo ciclo de vida ha expirado que se encuentran en su entorno. El gráfico muestra el software instalado que ha expirado en comparación con el ciclo de vida de soporte técnico para sistemas operativos y productos de SQL server.  
- **Los cinco principales productos que se aproximan al final de su ciclo de vida** este icono es una vista de datos consolidados de los productos cuyo ciclo de vida finaliza en el plazo de seis meses que se encuentran en su entorno. El gráfico muestra el software instalado al que le quedan seis meses en relación con el ciclo de vida de soporte técnico para sistemas operativos y productos de SQL server.
- **Datos de ciclo de vida de los productos instalados:** este icono ofrece una idea general del momento en el que un producto pasa del estado con soporte técnico al estado expirado. El gráfico proporciona un desglose del número de clientes en los que está instalado el producto y el estado de disponibilidad del soporte técnico, junto con un vínculo para obtener más información acerca de los siguientes pasos que se deben realizar. En el gráfico se incluye la siguiente información:     
    - Tiempo de soporte técnico restante
    - Número en el entorno 
    - Fecha de finalización del soporte técnico estándar
    - Fecha de finalización del soporte técnico ampliado
    - Pasos siguientes 

>[!IMPORTANT]
>La información que se muestra en este panel se proporciona para su comodidad y únicamente para el uso interno en su empresa. No debe confiar exclusivamente en esta información para comprobar el cumplimiento. Asegúrese de comprobar la exactitud de la información proporcionada, junto con la disponibilidad de la información de soporte técnico, en https://support.microsoft.com/en-us/lifecycle.

## <a name="reporting"></a>Generación de informes
Se agregan los siguientes informes nuevos a la categoría **Ciclo de vida del producto**:
- **Información general del ciclo de vida de productos:** vea una lista de los ciclos de vida de los productos. La lista se puede filtrar por nombre de producto y los días para la expiración, que el usuario puede definir. 
- **Equipos con un producto de software específico:** vea una lista de equipos en los que se detecta un producto determinado.
- **Lista de productos expirados que se encuentran en la organización:** vea los detalles de productos de su entorno cuyo ciclo de vida ha expirado. 
- **Lista de equipos con productos expirados de la organización:** vea equipos que contienen productos expirados. Este informe se puede filtrar por nombre de producto.

## <a name="next-steps"></a>Pasos siguientes
Para información sobre cómo instalar o actualizar la rama de Technical Preview, vea [Technical Preview para System Center Configuration Manager](/sccm/core/get-started/technical-preview).  

