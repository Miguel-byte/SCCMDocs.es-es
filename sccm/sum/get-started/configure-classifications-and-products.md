---
title: Configurar las clasificaciones y los productos que va a sincronizar
titleSuffix: Configuration Manager
description: Siga estos pasos para configurar las clasificaciones y los productos que se van a sincronizar en la consola de Configuration Manager.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: f36ff74b794e57b51742c40d10bd25a9cb4a13a5
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
#  <a name="configure-classifications-and-products-to-synchronize"></a>Configurar las clasificaciones y los productos que va a sincronizar  

*Se aplica a: System Center Configuration Manager (rama actual)*


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
    > A partir de la versión 1706 de Configuration Manager, puede activar la casilla **Incluir actualizaciones de controladores y firmware de Microsoft Surface** para sincronizar los controladores de Microsoft Surface. Todos los puntos de actualización de software deben ejecutar Windows Server 2016 para sincronizar correctamente los controladores de Surface. Si habilita un punto de actualización de software en un equipo que ejecuta Windows Server 2012 después de habilitar a los controladores de Surface, los resultados del examen de las actualizaciones de controladores no serán precisos. Esto genera datos de cumplimiento incorrectos que se muestran en la consola y en los informes de Configuration Manager.  
    > 
    > La casilla **Incluir actualizaciones de controladores y firmware de Microsoft Surface** siempre está disponible en la versión 1710 de Configuration Manager. Sin embargo, se trata de característica en versión preliminar disponible en la versión 1706 de Configuration Manager que debe activar. Las características de versión preliminar son características que se encuentran en la Rama actual para realizar las primeras pruebas en un entorno de producción. Estas características son totalmente compatibles pero aún se encuentran en proceso de desarrollo y podrían recibir cambios hasta que se saquen de la categoría de versión preliminar. Para más información, consulte [Use pre-release features from updates](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease) (Uso de características de la versión preliminar a partir de las actualizaciones).

5.  En la pestaña **Productos** , especifique los productos para los que desea sincronizar las actualizaciones de software y, a continuación, haga clic en **Cerrar**.  

    > [!NOTE]  
    >  Los metadatos para cada actualización de software definen los productos para los que la actualización es aplicable. Un producto es una edición específica de un sistema operativo o una aplicación, por ejemplo, Windows Server 2012. Una familia de productos es el sistema operativo o la aplicación de base de los cuales se derivan los productos individuales. Un ejemplo de una familia de productos es Windows, de la cual Windows Server 2012 forma parte. Puede especificar una familia de productos o productos individuales dentro de una familia de productos. Cuantos más productos seleccione, más tiempo tomará sincronizar las actualizaciones de software.  
    >   
    >  Cuando las actualizaciones de software son aplicables a varios productos y al menos se ha seleccionado uno de ellos para sincronización, todos los productos aparecerán en la consola de Configuration Manager, aunque algunos no se hayan seleccionado. Por ejemplo, si Windows Server 2012 es el único sistema operativo que ha seleccionado y si una actualización de software se aplica a Windows 8 y Windows Server 2012, la consola de Configuration Manager mostrará ambos productos.  

    > [!IMPORTANT]  
    >  Configuration Manager almacena una lista de productos y familias de productos entre los que puede elegir cuando instala por primera vez el punto de actualización de software. Es posible que los productos y las familias de productos lanzados después del lanzamiento de Configuration Manager no estén disponibles para seleccionar hasta que se complete la sincronización de las actualizaciones de software, lo cual actualiza la lista de productos y familias de productos disponibles para seleccionar.  

## <a name="next-steps"></a>Pasos siguientes
Inicie la sincronización de las actualizaciones de software para recuperar actualizaciones de software en función de los nuevos criterios. Para obtener detalles, vea [Synchronize software updates (Sincronizar actualizaciones de software)](synchronize-software-updates.md).
