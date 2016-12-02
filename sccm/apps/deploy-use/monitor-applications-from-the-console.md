---
title: "Supervisión de aplicaciones desde la consola de System Center Configuration Manager | System Center Configuration Manager"
description: "Supervise la implementación de software, incluidas actualizaciones, configuración de cumplimiento y aplicaciones, mediante el área de trabajo Configuración de Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ca82638267d6d9e1bb4eb6855785ac383a2191e9


---
# <a name="monitor-applications-from-the-system-center-configuration-manager-console"></a>Supervisar aplicaciones desde la consola de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


## <a name="introduction"></a>Introducción

En System Center Configuration Manager, puede supervisar la implementación de todo el software, incluidas las actualizaciones de software, las configuraciones de cumplimiento, las aplicaciones, las secuencias de tareas, los paquetes y los programas. Puede supervisar las implementaciones mediante el área de trabajo **Supervisión** en la consola de Configuration Manager o mediante el uso de informes.  

 Las aplicaciones de Configuration Manager admiten la supervisión basada en estado, lo cual permite hacer un seguimiento del último estado de implementación de aplicación para usuarios y dispositivos. Estos mensajes de estado muestran información acerca de dispositivos individuales. Por ejemplo, si una aplicación se implementa en una recopilación de usuarios, puede ver el estado de cumplimiento de la implementación y el propósito de la implementación en la consola de Configuration Manager.  

 El estado de implementación de una aplicación puede tener uno de los siguientes estados de cumplimiento:  

-   **Correcto** : la implementación de aplicación se realizó correctamente o se encontró que ya estaba instalada.  

-   **En curso** : la implementación de aplicación está en curso.  

-   **Desconocido** : no se pudo determinar el estado de la implementación de aplicación. Este estado no se aplica a las implementaciones cuyo propósito sea **Disponible**. Este estado suele mostrarse cuando todavía no se han recibido mensajes de estado del cliente.  

-   **Requisitos no cumplidos** : la aplicación no se implementó porque no cumplía con los requisitos de una dependencia o una regla de requisitos, o porque el sistema operativo en el que se iba a implementar no correspondía.  

-   **Error** : la aplicación no pudo implementarse debido a un error.  
  
Puede ver información adicional para cada estado de cumplimiento, que incluye subcategorías dentro del estado de cumplimiento y la cantidad de usuarios y dispositivos en esa categoría. Por ejemplo, el estado de cumplimiento **Error** incluye las subcategorías siguientes:  
  
-   Error al evaluar los requisitos  

-   Errores relacionados con el contenido  

-   Errores de instalación  

 Cuando se aplica más de un estado de cumplimiento para la implementación de una aplicación, puede ver el estado agregado que representa el cumplimiento más bajo. Por ejemplo:  

-   Si un usuario inicia sesión en dos dispositivos y la aplicación se instala correctamente en uno de los dispositivos, pero produce error en el segundo, el estado agregado de implementación de la aplicación para ese usuario indicará **Error**.  

-   Si se implementa una aplicación para todos los usuarios que inician sesión en un equipo, recibirá varios resultados de implementación para ese equipo. Si se produce un error en una de las implementaciones, el estado de implementación agregado para el equipo indicará **Error**.  
  
El estado de implementación para las implementaciones de paquete y de programa no se agrega.  
  
 Utilice estas subcategorías para que le ayuden a detectar rápidamente cualquier problema importante en la implementación de una aplicación. También puede ver información adicional acerca de los dispositivos que corresponden a una subcategoría particular de un estado de cumplimiento.  

 La administración de aplicaciones en Configuration Manager incluye una cantidad de informes integrados que permiten supervisar la información acerca de aplicaciones e implementaciones. Estos informes tienen la categoría de informe **Distribución de software - Supervisión de aplicaciones**.  

 Para obtener más información sobre cómo configurar la generación de informes en Configuration Manager, consulte [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md) (Generación de informes en System Center Configuration Manager).  
  
## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Supervisión del estado de una aplicación en la consola de Configuration Manager  
  
1.  En la consola de Configuration Manager, haga clic en **Supervisión** > **Implementaciones**.  
  
3.  Para ver los detalles de implementación de cada estado de cumplimiento y los dispositivos que tienen ese estado, seleccione una implementación y, a continuación, en la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Ver estado** para abrir el panel **Estado de implementación** . En este panel, puede ver los activos con cada estado de cumplimiento. Haga clic en cualquier activo para ver información más detallada sobre el estado de implementación para dicho activo.  

    > [!NOTE]  
    >  El panel **Estado de implementación** puede mostrar hasta 20.000 elementos. Si necesita ver más elementos, use los informes de Configuration Manager para ver datos de estado de aplicación.  
    >   
    >  El estado de los tipos de implementación se muestra agregado en el panel **Estado de implementación** . Para ver información más detallada sobre los tipos de implementación, use el informe **Errores de infraestructura de aplicación** en la categoría de informe **Distribución de software - Supervisión de aplicaciones**.  

4.  Para revisar información de estado general sobre una implementación de aplicación, seleccione una implementación y, a continuación, haga clic en la pestaña **Resumen** en la ventana **Implementación seleccionada** .  

5.  Para revisar información sobre el tipo de implementación de aplicaciones, seleccione una implementación y, a continuación, haga clic en la pestaña **Tipos de implementación** en la ventana **Implementación seleccionada** .  

La información que se muestra en el panel **Estado de implementación** después de hacer clic en **Ver estado** está conformada por datos en directo de la base de datos de Configuration Manager. La información que se muestra en la pestaña **Resumen** y la pestaña **Tipos de implementación** está conformada por datos resumidos. Si los datos que se muestran en la pestaña **Resumen** y en la pestaña **Tipos de implementación** no coinciden con los datos que se muestran en el panel **Estado de implementación** , haga clic en **Ejecutar resumen** para actualizar los datos de esas pestañas. Para configurar el intervalo de resumen predeterminado de implementación de aplicación, haga lo siguiente:  
1. En la consola de Configuration Manager, haga clic en **Administración** > **Configuración del sitio** > **Sitios**.
2. En la lista **Sitios** , seleccione el sitio para el que desea configurar el intervalo de resumen y, a continuación, en la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Generadores de resumen de estado**.
3. En el cuadro de diálogo **Generadores de resumen de estado** , haga clic en **Generador de resumen de implementación de aplicación**y, a continuación, haga clic en **Editar**.  
4. En el cuadro de diálogo **Propiedades del generador de resumen de implementación de aplicación** , configure los intervalos de resumen requeridos y, a continuación, haga clic en **Aceptar**.  



<!--HONumber=Nov16_HO1-->

