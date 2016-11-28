---
title: "Finalizar la migración | System Center Configuration Manager"
description: "Obtenga información sobre cómo finalizar la migración a una jerarquía de destino de System Center Configuration Manager cuando la jerarquía de origen ya no contiene datos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 862a039ada302c9432fc86d68f5ba9aad360f69b


---
# <a name="planning-to-complete-migration-in-system-center-configuration-manager"></a>Planear la finalización de la migración en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Con System Center Configuration Manager, el proceso de migración puede finalizarse cuando la jerarquía de origen ya no contiene datos que se deseen migrar a la jerarquía de destino. La finalización de la migración incluye los siguientes pasos generales:  

-   Asegurarse de que ha migrado los datos requeridos. Antes de completar la migración desde una jerarquía de origen, asegúrese de haber migrado correctamente todos los recursos requeridos desde la jerarquía de origen a la jerarquía de destino. Esto puede incluir datos y clientes.  

-   Detener la recopilación de datos de sitios de origen. Para completar la migración de una jerarquía de origen, primero debe detener la recopilación de datos de sitios de origen.  

-   Limpiar datos de migración. Después de detener la recopilación de datos de todos los sitios de origen en una jerarquía de origen, es posible quitar datos sobre el proceso de migración y la jerarquía de origen de la base de datos de la jerarquía de destino.  

-   Retirar la jerarquía de origen. Una vez se ha completado la migración de una jerarquía de origen y que la jerarquía deja de contener recursos administrados, es posible retirar los sitios de la jerarquía de origen y quitar la infraestructura relacionada de su entorno. Para obtener información sobre cómo retirar sitios y jerarquías de origen, consulte la documentación de esa versión de Configuration Manager.  

Utilice las secciones siguientes como ayuda para planear a completar la finalización de la migración de una jerarquía de origen deteniendo la recopilación de datos y, a continuación, limpiando los datos de migración:  

-   [Plan para detener la recopilación de datos](#Plan_to_Stop_Data_Gath)  

-   [Plan para limpiar los datos de migración](#Plan_to_clean_up)  

##  <a name="a-nameplantostopdatagatha-plan-to-stop-gathering-data"></a><a name="Plan_to_Stop_Data_Gath"></a> Plan para detener la recopilación de datos  
 Antes de completar la migración y limpiar los datos de migración, debe detener la recopilación de datos de cada sitio de origen de la jerarquía de origen. Para detener la recopilación de datos de cada sitio de origen, debe ejecutar el comando **Detener la recopilación de datos** en los sitios de origen del nivel inferior y, a continuación, repetir el proceso en cada sitio principal. El sitio de nivel superior de la jerarquía de origen debe ser el último sitio en el que se detenga la recopilación de datos. Debe detener la recopilación en cada sitio secundario antes de ejecutar este comando en un sitio principal. Normalmente, solo debe detener la recopilación de datos cuando esté listo para completar el proceso de migración.  

 Después de detener la recopilación de datos de un sitio de origen, los puntos de distribución compartidos de ese sitio ya no están disponibles como ubicaciones de contenido para los clientes en la jerarquía de destino. Por lo tanto, asegúrese de que cualquier contenido migrado al que los clientes de la jerarquía de destino deban tener acceso siga estando disponible mediante una de las siguientes opciones:  

-   En la jerarquía de destino, distribuya el contenido al menos a un punto de distribución.  

-   Antes de detener la recopilación de datos desde un sitio de origen, actualice o reasigne los puntos de distribución compartidos que tienen el contenido requerido. Para obtener más información sobre la actualización o la reasignación de los puntos de distribución compartidos, consulte las secciones correspondientes en el tema [Planear una estrategia de migración de implementación de contenido en System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

Después de detener la recopilación de datos de cada sitio de origen de la jerarquía de origen, puede limpiar los datos de migración. Hasta que limpie los datos de migración, todos los trabajos de migración que se hayan ejecutado o que estén programados para ejecutarse seguirán accesibles en la consola de Configuration Manager.  

Para obtener más información sobre los sitios de origen y la recopilación de datos, consulte [Planear una estrategia de jerarquía de origen en System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).  

##  <a name="a-nameplantocleanupa-plan-to-clean-up-migration-data"></a><a name="Plan_to_clean_up"></a> Plan para limpiar los datos de migración  
 El último paso para completar la migración es limpiar los datos de migración. Puede utilizar el comando **Limpiar datos de migración** después de haber detenido la recopilación de datos para cada sitio de origen en la jerarquía de origen. Esta acción opcional quita datos acerca de la jerarquía de origen actual de la base de datos de la jerarquía de destino.  

 Al limpiar los datos de migración, la mayoría de los datos relativos a la migración se quita de la base de datos de la jerarquía de destino. Sin embargo, se conservan los detalles acerca de los objetos migrados. Con estos detalles, puede usar el área de trabajo **Migración** para volver a configurar la jerarquía de origen que contiene los datos que se migraron con el objetivo de reanudar la migración desde esa jerarquía de origen, o de revisar los objetos y la propiedad del sitio de los objetos que se migraron previamente.  



<!--HONumber=Nov16_HO1-->


