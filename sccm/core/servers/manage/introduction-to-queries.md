---
title: "Introducción a las consultas | System Center Configuration Manager"
description: "Cree y ejecute consultas para buscar objetos en una jerarquía de System Center Configuration Manager que coincidan con los criterios de consulta."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 054f3cc5ba7963231df93ed0ceb973d20b2e8f8e


---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>Introducción a las consultas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede crear y ejecutar consultas para buscar objetos en una jerarquía de System Center Configuration Manager que coincidan con los criterios de consulta. Estos objetos incluyen elementos, como tipos específicos de equipos o grupos de usuarios. Las consultas pueden devolver la mayoría de los tipos de objetos de Configuration Manager, que incluyen sitios, recopilaciones, aplicaciones y datos de inventario.  

 Al crear una consulta, debe especificar un mínimo de dos parámetros: donde quiere buscar y lo que quiere buscar. Por ejemplo, para averiguar la cantidad de espacio en disco duro que está disponible en todos los equipos de un sitio de Configuration Manager, puede crear una consulta para buscar la clase de atributos **Disco lógico** y el atributo **Espacio libre (MB)** para el espacio disponible en disco.  

 Después de crear una consulta inicial, puede especificar criterios adicionales de consulta. Por ejemplo, puede especificar que los resultados de la consulta solo incluyan los equipos que estén asignados a un sitio especificado. También puede modificar cómo se muestran los resultados para que pueda verlos en el orden que prefiera. Por ejemplo, puede especificar que los resultados se ordenen según la cantidad de espacio libre en disco en orden ascendente o descendente.  

 Cuando se crea una consulta, Configuration Manager la almacena y se muestra en el nodo **Consultas** del área de trabajo **Supervisión**. Desde esta ubicación, puede crear una nueva consulta y luego ejecutar, actualizar o administrar una consulta existente.  

 También puede importar una consulta en una regla de consulta de una recopilación de Configuration Manager. Para obtener más información, consulte [Cómo crear recopilaciones en System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

## <a name="see-also"></a>Véase también  
 [Referencia técnica de consultas para System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)



<!--HONumber=Nov16_HO1-->


