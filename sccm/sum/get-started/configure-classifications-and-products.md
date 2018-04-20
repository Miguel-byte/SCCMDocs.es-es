---
title: Configurar las clasificaciones y los productos
titleSuffix: Configuration Manager
description: Haga lo siguiente para configurar los productos y clasificaciones de actualización de software que se van a sincronizar en la consola de Configuration Manager.
keywords: ''
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/10/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: 9ba0872b1d2e4ef5dd027df3f7c16a6b3a94e9ac
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
#  <a name="configure-classifications-and-products-to-synchronize"></a>Configurar las clasificaciones y los productos que va a sincronizar  

*Se aplica a: System Center Configuration Manager (Rama actual)*


> [!NOTE]  
>  Utilice el procedimiento de esta sección solo en el sitio de nivel superior.  

 Los metadatos de las actualizaciones de software se recuperan durante el proceso de sincronización en Configuration Manager según la configuración que especifique en las propiedades de componente de punto de actualización de software. Después de sincronizar las actualizaciones de software por primera vez o cuando se publiquen nuevos productos y clasificaciones, debe ir a las propiedades para seleccionar los nuevos elementos. Utilice el siguiente procedimiento para configurar las clasificaciones y los productos para sincronizar.  

#### <a name="to-configure-classifications-and-products-to-synchronize"></a>Para configurar las clasificaciones y los productos para sincronizar  

1.  En la consola de **Configuration Manager**, vaya a **Administración** > **Configuración del sitio** > **Sitios**.

2. Seleccione el sitio de administración central o el sitio primario independiente.  

3.  En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Configurar componentes de sitio**y, a continuación, haga clic en **Punto de actualización de software**.

4.  En la pestaña **Clasificaciones** , especifique las clasificaciones de actualización de software para las que desea sincronizar las actualizaciones de software.  

    > [!NOTE]  
    >  Cada actualización de software se define con una clasificación de actualización que facilita la organización de los distintos tipos de actualizaciones. Durante el proceso de sincronización, se sincronizan los metadatos de las actualizaciones de software para las clasificaciones especificadas. Configuration Manager ofrece la posibilidad de sincronizar actualizaciones de software con las siguientes clasificaciones de actualización:  
    >   
    > - **Actualizaciones críticas**: especifica una actualización de amplia distribución para un problema específico que resuelve un error crítico no relacionado con la seguridad.  
    > - **Actualizaciones de definiciones**: especifica una actualización para un archivo de definición de virus u otros.  
    > - **Paquetes de características**: especifica las nuevas características de producto que se distribuyen fuera de una versión del producto y que normalmente se incluyen en la siguiente versión del producto completo.  
    > - **Actualizaciones de seguridad**: especifica una actualización de amplia distribución para un problema específico del producto relacionado con la seguridad.  
    > - **Service Packs**: especifica un conjunto acumulativo de revisiones correspondientes a una aplicación. Estas revisiones pueden incluir actualizaciones de seguridad, actualizaciones críticas, actualizaciones de software, etc.  
    > - **Herramientas**: especifica una utilidad o característica que ayuda a realizar una o más tareas.  
    > - **Paquetes acumulativos de revisiones**: especifica un conjunto acumulativo de revisiones que se recopilan para facilitar la implementación. Estas revisiones pueden incluir actualizaciones de seguridad, actualizaciones críticas, actualizaciones, etc. Un paquete acumulativo de revisiones suele relacionarse, por lo general, con un área específica; por ejemplo, un componente del producto o de la seguridad.  
    > - **Actualizaciones**: especifica una actualización para una aplicación o un archivo actualmente instalados.  
    > - **Actualizaciones**: especifica una actualización para las características y la funcionalidad de Windows 10. Los sitios y los puntos de actualización de software tienen que ejecutar como mínimo WSUS 4.0 con la [revisión 3095113](https://support.microsoft.com/kb/3095113) para obtener la clasificación **Actualización**.    
    >       

    > [!NOTE]    
    > A partir de la versión 1706 de Configuration Manager, puede activar la casilla **Incluir actualizaciones de controladores y firmware de Microsoft Surface** para sincronizar los controladores de Microsoft Surface.<!--1098490--> Todos los puntos de actualización de software deben ejecutar Windows Server 2016 para sincronizar correctamente los controladores de Surface. Si habilita un punto de actualización de software en un equipo que ejecuta Windows Server 2012 después de habilitar a los controladores de Surface, los resultados del examen de las actualizaciones de controladores no serán precisos. Esto genera datos de cumplimiento incorrectos que se muestran en la consola y en los informes de Configuration Manager.  
    >  
    > Esta característica se introdujo por primera vez en la versión 1706 como una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). A partir de la versión 1710, ya no es una característica de versión preliminar.  
    >  
    > Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para más información, vea [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

5.  En la pestaña **Productos** , especifique los productos para los que desea sincronizar las actualizaciones de software y, a continuación, haga clic en **Cerrar**.  

    > [!NOTE]  
    >  Los metadatos para cada actualización de software definen los productos para los que la actualización es aplicable. Un producto es una edición específica de un sistema operativo o una aplicación, por ejemplo, Windows Server 2012. Una familia de productos es el sistema operativo o la aplicación de base de los cuales se derivan los productos individuales. Un ejemplo de una familia de productos es Windows, de la cual Windows Server 2012 forma parte. Puede especificar una familia de productos o productos individuales dentro de una familia de productos. Cuantos más productos seleccione, más tiempo tomará sincronizar las actualizaciones de software.  
    >   
    >  Cuando las actualizaciones de software son aplicables a varios productos y al menos se ha seleccionado uno de ellos para sincronización, todos los productos aparecerán en la consola de Configuration Manager, aunque algunos no se hayan seleccionado. Por ejemplo, si Windows Server 2012 es el único sistema operativo que ha seleccionado y si una actualización de software se aplica a Windows 8 y Windows Server 2012, la consola de Configuration Manager mostrará ambos productos.  

    > [!IMPORTANT]  
    >  Configuration Manager almacena una lista de productos y familias de productos entre los que puede elegir cuando instala por primera vez el punto de actualización de software. Es posible que los productos y las familias de productos lanzados después del lanzamiento de Configuration Manager no estén disponibles para seleccionar hasta que se complete la sincronización de las actualizaciones de software, lo cual actualiza la lista de productos y familias de productos disponibles para seleccionar.  

## <a name="next-steps"></a>Pasos siguientes
Inicie la sincronización de las actualizaciones de software para recuperar actualizaciones de software en función de los nuevos criterios. Para obtener detalles, vea [Synchronize software updates (Sincronizar actualizaciones de software)](synchronize-software-updates.md).
