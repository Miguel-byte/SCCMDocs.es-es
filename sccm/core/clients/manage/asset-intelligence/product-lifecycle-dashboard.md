---
title: Panel de ciclo de vida del producto
titleSuffix: Configuration Manager
description: Vea la Directiva del ciclo de vida de Microsoft con el panel de ciclo de vida del producto en Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f99aeba109ed4de3ef1b88b721b59eebb4653cb6
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384638"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>Administrar la directiva de ciclo de vida de Microsoft con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

A partir de la versión 1806, puede usar el panel de ciclo de vida del producto de Configuration Manager para ver la Directiva de ciclo de vida de Microsoft. El panel muestra el estado de la Directiva de ciclo de vida de Microsoft de los productos instalados en los dispositivos administrados con Configuration Manager. Además proporciona información sobre los productos de Microsoft del entorno, el estado de compatibilidad y la fechas de finalización del soporte técnico. Use el panel para conocer la disponibilidad del soporte técnico para cada producto. Esta información le ayuda a planear cuándo actualizar los productos de Microsoft que usa antes de que llegue el fin del soporte actual.  

Para más información, vea la [Directiva de ciclo de vida de Microsoft](https://support.microsoft.com/lifecycle).



## <a name="prerequisites"></a>Requisitos previos 

 Para ver los datos en el panel del ciclo de vida del producto, se requieren los siguientes componentes:  

- Internet Explorer 9 o una versión posterior debe estar instalado en el equipo que ejecuta la consola de Configuration Manager.  

- Un punto de servicios de informes es necesario para la funcionalidad de hipervínculo en el panel. Los informes de vínculos del panel para SQL Server Reporting Services (SSRS). Para obtener más información, vea [Generación de informes en Configuration Manager](/sccm/core/servers/manage/reporting).  

- El punto de sincronización de Asset Intelligence debe estar configurado y sincronizado. El panel usa el catálogo de Asset Intelligence como metadatos para los títulos de productos. Los metadatos se comparan con los datos de inventario en la jerarquía. Para obtener más información, consulte [Configurar Asset Intelligence en Configuration Manager](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  

     > [!NOTE]  
     > Si está configurando el punto de servicio de Asset Intelligence por primera vez, no olvide [habilitar las clases de inventario de hardware de Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence#BKMK_EnableAssetIntelligence). El panel de ciclo de vida depende de esas clases de inventario de hardware de Asset Intelligence. El panel no mostrará datos hasta que los clientes hayan analizado y devuelto el inventario de hardware.  



## <a name="use-the-product-lifecycle-dashboard"></a>Uso del panel de ciclo de vida del producto

El panel mostrará información sobre todos los productos actuales en función de los datos de inventario que recopile el sitio de los dispositivos administrados. Sin embargo, la información mostrada para los sistemas operativos y SQL Server se limita a las siguientes versiones:

- Windows Server 2008 y versiones posteriores
- Windows XP y versiones posteriores
- SQL Server 2008 y versiones posteriores

Para tener acceso al panel de ciclo de vida, en la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**, expanda **Asset Intelligence** y seleccione el nodo **Ciclo de vida del producto**.

> [!NOTE]  
> Los datos del panel se basan en el sitio al que se conecta la consola de Configuration Manager. Si la consola se conecta a su sitio de nivel superior, verá datos en toda la jerarquía. Cuando se conecta a un sitio primario secundario, se mostrarán solamente los datos de ese sitio.

### <a name="product-lifecycle-dashboard"></a>Panel de ciclo de vida del producto

![Captura de pantalla del panel de ciclo de vida del producto en la consola](media/product-lifecycle-dashboard.png)

El panel presenta los iconos siguientes:  

- **Los cinco principales productos cuyo ciclo de vida ha expirado**: este icono es una vista de datos consolidados de los productos que se encuentran en su entorno cuyo ciclo de vida ha expirado. El gráfico muestra el software instalado que ha expirado en comparación con el ciclo de vida de soporte técnico para sistemas operativos y productos de SQL server.  

- **Los cinco principales productos que se aproximan al final de su ciclo de vida**: este icono es una vista de datos consolidados de los productos que se encuentran en su entorno cuyo ciclo de vida finaliza en un plazo de seis meses. El gráfico muestra el software instalado al que le quedan seis meses en relación con el ciclo de vida de soporte técnico para sistemas operativos y productos de SQL server.  

- **Datos de ciclo de vida de los productos instalados**: este icono ofrece una idea general del momento en el que un producto pasa del estado con soporte técnico al estado expirado. El gráfico proporciona un desglose del número de clientes en los que está instalado el producto y el estado de disponibilidad del soporte técnico, junto con un vínculo para obtener más información acerca de los siguientes pasos que se deben realizar. En el gráfico se incluye la siguiente información:     
    - Tiempo de soporte técnico restante
    - Número en el entorno 
    - Fecha de finalización del soporte técnico estándar
    - Fecha de finalización del soporte técnico ampliado
    - Pasos siguientes  

> [!IMPORTANT]  
> La información que se muestra en este panel se proporciona para su comodidad y únicamente para el uso interno en su empresa. No debe confiar exclusivamente en esta información para comprobar el cumplimiento. Asegúrese de comprobar la exactitud de la información proporcionada, junto con la disponibilidad de la información de soporte técnico, en [Directiva de ciclo de vida de Microsoft](https://support.microsoft.com/lifecycle).  



## <a name="reporting"></a>Generación de informes

También existen informes adicionales. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Informes** y expanda **Informes**. Se agregan los siguientes informes nuevos a la categoría **Ciclo de vida del producto**:  

- **Información general del ciclo de vida de productos**: vea una lista de los ciclos de vida de los productos. Filtre la lista por nombre de producto y los días para que expire.  

- **Equipos con un producto de software específico**: vea una lista de equipos en los que se detecta un producto determinado.  

- **Lista de productos expirados que se encuentran en la organización**: vea los detalles de productos de su entorno cuyo ciclo de vida ha expirado.  

- **Lista de equipos con productos expirados de la organización**: vea equipos que contienen productos expirados. Este informe se puede filtrar por nombre de producto.

