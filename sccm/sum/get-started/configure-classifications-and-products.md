---
title: Configurar las clasificaciones y los productos
titleSuffix: Configuration Manager
description: Haga lo siguiente para configurar los productos y clasificaciones de actualización de software que se van a sincronizar en la consola de Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/25/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2edf117f27eda3ee3c9e587edb9f69c8d84bf5dc
ms.sourcegitcommit: 670cfed1e47a7a4a73aa4ccb873c6312be3c21ff
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71311585"
---
# <a name="configure-classifications-and-products-to-synchronize"></a>Configurar las clasificaciones y los productos que va a sincronizar  

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los metadatos de las actualizaciones de software se recuperan durante el proceso de sincronización en Configuration Manager según la configuración que especifique en las propiedades de componente de punto de actualización de software. Después de sincronizar las actualizaciones de software por primera vez o cuando se publiquen nuevos productos y clasificaciones, debe ir a las propiedades para seleccionar los nuevos elementos. Utilice el siguiente procedimiento para configurar las clasificaciones y los productos para sincronizar.  

> [!NOTE]  
> Utilice el procedimiento de esta sección solo en el sitio de nivel superior.  

## <a name="to-configure-classifications-and-products-to-synchronize"></a>Para configurar las clasificaciones y los productos para sincronizar  

1. En la consola de **Configuration Manager**, vaya a **Administración** > **Configuración del sitio** > **Sitios**.

2. Seleccione el sitio de administración central o el sitio primario independiente.  

3. En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Configurar componentes de sitio**y, a continuación, haga clic en **Punto de actualización de software**.

4. En la pestaña **Clasificaciones** , especifique las clasificaciones de actualización de software para las que desea sincronizar las actualizaciones de software.  

    Cada actualización de software se define con una clasificación de actualización que facilita la organización de los distintos tipos de actualizaciones. Durante el proceso de sincronización, se sincronizan los metadatos de las actualizaciones de software para las clasificaciones especificadas. Configuration Manager ofrece la posibilidad de sincronizar actualizaciones de software con las siguientes clasificaciones de actualización:  

     - **Actualizaciones críticas**: especifica una corrección de amplia distribución para un problema específico que permite solucionar un error crítico no relacionado con la seguridad.  
     - **Actualizaciones de definición**: especifica una actualización de software frecuente y de amplia distribución que contiene adiciones a la base de datos de definiciones de un producto.  
     - **Paquetes de características**: especifica la nueva función del producto que se distribuye fuera de una versión del producto y que normalmente se incluye en la siguiente versión del producto completo.  
     - **Actualizaciones de seguridad**: especifica una corrección de amplia distribución de una vulnerabilidad relacionada con la seguridad de un producto específico.  
     - **Service Packs**: especifica un conjunto acumulativo y probado de todas las revisiones, actualizaciones de seguridad, actualizaciones críticas y actualizaciones que se aplican a un producto. Además, los Service Pack pueden contener correcciones adicionales para problemas que se han identificado internamente desde la publicación del producto.  
     - **Herramientas**: especifica una utilidad o característica que ayuda a realizar una o más tareas.  
     - **Actualizaciones acumulativas**: especifica un conjunto acumulativo y probado de revisiones, actualizaciones de seguridad, actualizaciones críticas y actualizaciones que se incluyen en un producto de forma conjunta para facilitar su implementación. Un paquete acumulativo de actualizaciones suele relacionarse, por lo general, con un área específica (por ejemplo, un componente del producto o de la seguridad).  
     - **Actualizaciones**: especifica una corrección de amplia distribución de un problema específico. Una actualización proporciona una solución para un error de código no crítico y no relacionado con la seguridad.  
     - **Actualizaciones**: especifica una actualización para las características y la funcionalidad de Windows 10. Los sitios y los puntos de actualización de software tienen que ejecutar como mínimo WSUS 6.2 con la [revisión 3095113](https://support.microsoft.com/kb/3095113) para obtener la clasificación **Actualización**. Para obtener más información sobre la instalación de esta actualización y otras actualizaciones para las **actualizaciones, consulte** [requisitos previos para las actualizaciones de software](/sccm/sum/plan-design/prerequisites-for-software-updates#BKMK_wsus2012).

    > [!NOTE] 
    > 
    > A partir de la versión 1706 de Configuration Manager, puede activar la casilla **Incluir actualizaciones de controladores y firmware de Microsoft Surface** para sincronizar los controladores de Microsoft Surface.<!--1098490--> Todos los puntos de actualización de software deben ejecutar Windows Server 2016 para sincronizar correctamente los controladores de Surface. Si habilita un punto de actualización de software en un equipo que ejecuta Windows Server 2012 después de habilitar a los controladores de Surface, los resultados del examen de las actualizaciones de controladores no serán precisos. Esto genera datos de cumplimiento incorrectos que se muestran en la consola y en los informes de Configuration Manager.  
    >  
    > - Esta característica se introdujo por primera vez en la versión 1706 como una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). A partir de la versión 1710, ya no es una característica de versión preliminar.  
    >  
    > - Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

5. En la pestaña **Productos** , especifique los productos para los que desea sincronizar las actualizaciones de software y, a continuación, haga clic en **Cerrar**.  

    - Configuration Manager almacena una lista de productos y familias de productos entre los que puede elegir cuando instala por primera vez el punto de actualización de software. Es posible que los productos y las familias de productos lanzados después del lanzamiento de Configuration Manager no estén disponibles para seleccionar hasta que se complete la sincronización de las actualizaciones de software, lo cual actualiza la lista de productos y familias de productos disponibles para seleccionar.  

    - Los metadatos para cada actualización de software definen los productos para los que la actualización es aplicable. Un producto es una edición específica de un sistema operativo o una aplicación, por ejemplo, Windows Server 2012. Una familia de productos es el sistema operativo o la aplicación de base de los cuales se derivan los productos individuales. Un ejemplo de una familia de productos es Windows, de la cual Windows Server 2012 forma parte. Puede especificar una familia de productos o productos individuales dentro de una familia de productos. Cuantos más productos seleccione, más tiempo tomará sincronizar las actualizaciones de software.  

    - Cuando las actualizaciones de software son aplicables a varios productos y se seleccionó al menos uno de ellos para sincronización, todos los productos aparecerán en la consola de Configuration Manager, aunque algunos no se hayan seleccionado. Por ejemplo, si Windows Server 2012 es el único sistema operativo que ha seleccionado y si una actualización de software se aplica a Windows 8 y Windows Server 2012, la consola de Configuration Manager mostrará ambos productos.  

    > [!NOTE]  
    > **Windows 10, versión 1903 y posteriores** se ha agregado a Microsoft Update como un producto propio en lugar de formar parte del producto **Windows 10** como en las versiones anteriores. Este cambio le obligaba a realizar una serie de pasos manuales para asegurarse de que los clientes veían estas actualizaciones. Hemos ayudado a reducir el número de pasos manuales que debe realizar para el nuevo producto en Configuration Manager versión 1906. <!--4682946-->
    >
    > Cuando actualice a la versión 1906 de Configuration Manager y tenga seleccionado el producto **Windows 10** para la sincronización, las siguientes acciones tendrán lugar de forma automática:
    > - El producto **Windows 10, versión 1903 y posteriores** se agrega para la sincronización.
    > - Las [reglas de implementación automática](/sccm/sum/deploy-use/automatically-deploy-software-updates#bkmk_adr-process) que contienen el producto **Windows 10** se actualizarán para incluir **Windows 10, versión 1903 y versiones posteriores**.
    > - Los [planes de mantenimiento](/sccm/osd/deploy-use/manage-windows-as-a-service#servicing-plan-workflow) se actualizan para incluir el producto **Windows 10, versión 1903 y posteriores**.

## <a name="bkmk_WIfB"></a>Programa de Windows Insider
<!--3556023-->
A partir de septiembre de 2019, puede atender y actualizar los dispositivos que ejecutan compilaciones de Windows Insider Preview con Configuration Manager. Este cambio significa que puede administrar estos dispositivos sin cambiar los procesos normales ni habilitar Windows Update para empresas. Puede descargar actualizaciones de características y actualizaciones acumulativas para las compilaciones de Windows Insider Preview en Configuration Manager igual que cualquier otra actualización de Windows 10 o actualización. Para obtener más información, consulte la entrada de blog [publicar actualizaciones de características de Windows 10 en la versión preliminar de WSUS](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Publishing-pre-release-Windows-10-feature-updates-to-WSUS/ba-p/845054) .

Para obtener más información sobre la compatibilidad de Windows Insider en Configuration Manager, consulte [compatibilidad con Windows 10](/sccm/core/plan-design/configs/support-for-windows-10bkmk_WIfB-support).

### <a name="prerequisites"></a>Requisitos previos

- Configuration Manager versión 1906 o posterior, configurada para la [Administración de actualizaciones de software](/sccm/sum/plan-design/plan-for-software-updates).
- Dispositivos Windows 10 que ejecutan la [compilación de Windows Insider Preview](https://insider.windows.com/en-us/how-to-pc/).<!--the direct page link doesn't work without a locale :(-->
- Colección que contiene los dispositivos de Windows Insider.


### <a name="enable-windows-insider-upgrades-and-updates"></a>Habilitar actualizaciones y actualizaciones de Windows Insider

Debe habilitar los productos y las clasificaciones para las actualizaciones y actualizaciones de Windows Insider. Las actualizaciones de características para Windows Insider están bajo el producto de **versión preliminar de Windows Insider** . Sin embargo, las actualizaciones acumulativas y otras actualizaciones para Windows Insider estarán en el producto **Windows 10, versión 1903 y versiones posteriores**.

1. En la consola de **Configuration Manager**, vaya a **Administración** > **Configuración del sitio** > **Sitios**.
2. Seleccione el sitio de administración central o el sitio primario independiente.  
3. En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Configurar componentes de sitio**y, a continuación, haga clic en **Punto de actualización de software**.
4. En la pestaña **productos** , asegúrese de que se seleccionan los siguientes productos para la sincronización:
    - Versión preliminar de Windows Insider
    - Windows 10, version 1903 and later
5. En la pestaña **clasificaciones** , asegúrese de que están seleccionadas las siguientes clasificaciones para la sincronización:
    - Actualizaciones
    - Actualizaciones de seguridad
    - Actualizaciones (opcional)
6. Haga clic en **Aceptar** para cerrar **Propiedades de componente de punto de actualización de software**.

### <a name="upgrading-windows-insider-devices"></a>Actualización de dispositivos de Windows Insider

Una vez que se sincronizan las actualizaciones de Windows Insider, puede verlas desde la **biblioteca** > de software**Windows 10 mantenimiento** > de**todas las actualizaciones de Windows 10**.

![Actualizaciones de características de Windows Insider para el mantenimiento de Windows 10](media/3556023-windows-insiders-pre-release-feature-update.png)

Implemente actualizaciones de características para Windows Insider en la recopilación de destino, al igual que cualquier otra actualización. Sin embargo, querrá tener en cuenta los siguientes elementos al implementar estas actualizaciones de características:

- Estas actualizaciones se aplicarán a todos los clientes de Windows 10 1903 o versiones anteriores, con arquitectura, edición e idioma coincidentes.
- Hay términos de licencia, la implementación debe aceptar los términos para poder instalarlos.
- Considere la posibilidad [de utilizar la prioridad del subproceso en la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#bkmk_thread-priority).
- La actualización dinámica instala automáticamente las actualizaciones críticas, incluida la actualización acumulativa más reciente, directamente desde Microsoft Update. Este comportamiento comenzó con las actualizaciones de características para la versión 1903 de Windows 10. 
  - Puede deshabilitar explícitamente la [actualización dinámica en la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#bkmk_du) o con un [archivo setupconfig. ini](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options). 
  - Para obtener más información, consulte la entrada de blog de [actualización dinámica de Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) .

Para obtener más información sobre cómo implementar actualizaciones, consulte [Administración de Windows como servicio](/sccm/osd/deploy-use/manage-windows-as-a-service).


### <a name="keeping-insider-devices-up-to-date"></a>Mantenimiento de los dispositivos internos actualizados

Las actualizaciones acumulativas para Windows Insider estarán disponibles para WSUS y por extensión para Configuration Manager. Estas actualizaciones acumulativas se lanzarán con una frecuencia similar a la de las actualizaciones acumulativas de Windows 10, versión 1903. Las actualizaciones acumulativas de Windows Insider se encuentran en la categoría de producto **Windows 10, versión 1903 y versiones posteriores** , y se clasifican como actualizaciones de **seguridad** o **actualizaciones**. Puede implementar las actualizaciones acumulativas para Windows Insider mediante el proceso de actualización de software normal como el uso de [reglas de implementación automática](/sccm/sum/deploy-use/automatically-deploy-software-updates) o [implementaciones por fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).


## <a name="next-steps"></a>Pasos siguientes

Inicie la sincronización de las actualizaciones de software para recuperar actualizaciones de software en función de los nuevos criterios. Para más información, vea [Sincronizar actualizaciones de software](synchronize-software-updates.md).
