---
title: Introducción a las consultas
titleSuffix: Configuration Manager
description: Cree y ejecute consultas para buscar objetos en una jerarquía de System Center Configuration Manager que coincidan con los criterios de consulta.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a976b7beab3650ccad58ea41bca644dc24425ef0
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65497398"
---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>Introducción a las consultas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede crear y ejecutar consultas para buscar objetos en una jerarquía de System Center Configuration Manager que coincidan con los criterios de consulta. Estos objetos incluyen elementos, como tipos específicos de equipos o grupos de usuarios. Las consultas pueden devolver la mayoría de los tipos de objetos de Configuration Manager, que incluyen sitios, recopilaciones, aplicaciones y datos de inventario.  

## <a name="query-creation-overview"></a>Información general sobre la creación de consultas

 Al crear una consulta, debe especificar un mínimo de dos parámetros: donde quiere buscar y lo que quiere buscar. Por ejemplo, para averiguar la cantidad de espacio en disco duro que está disponible en todos los equipos de un sitio de Configuration Manager, puede crear una consulta para buscar la clase de atributos **Disco lógico** y el atributo **Espacio libre (MB)** para el espacio disponible en disco.  

 Después de crear una consulta inicial, puede especificar criterios adicionales de consulta. Por ejemplo, puede especificar que los resultados de la consulta solo incluyan los equipos que estén asignados a un sitio especificado. También puede modificar cómo se muestran los resultados para que pueda verlos en el orden que prefiera. Por ejemplo, puede especificar que los resultados se ordenen según la cantidad de espacio libre en disco en orden ascendente o descendente.  

 Cuando se crea una consulta, Configuration Manager la almacena y se muestra en el nodo **Consultas** del área de trabajo **Supervisión**. Desde esta ubicación, puede crear una nueva consulta y luego ejecutar, actualizar o administrar una consulta existente.  

 También puede importar una consulta en una regla de consulta de una recopilación de Configuration Manager. Para obtener más información, consulte [Cómo crear recopilaciones en System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

## <a name="next-steps"></a>Pasos siguientes

 [Cómo crear consultas en System Center Configuration Manager](../../../core/servers/manage/create-queries.md)
