---
title: Herramienta Content Library Transfer
titleSuffix: Configuration Manager
description: Use la herramienta Content Library Transfer para transferir contenido de una unidad de disco a otra en un punto de distribución de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ee63a4eb7b3f0d575586b2e672f9440060c7f6f6
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65495808"
---
# <a name="content-library-transfer-tool"></a>Herramienta Content Library Transfer

*Se aplica a: System Center Configuration Manager (Rama actual)*

La herramienta Content Library Transfer es una de las [herramientas de Configuration Manager](/sccm/core/support/tools). Transfiere contenido de una unidad de disco a otra. La herramienta está diseñada para ejecutarse en sistemas de sitio de punto de distribución. Admite puntos de distribución ubicados en un sitio o en sistemas de sitio remoto.  

La herramienta es útil para el escenario en que la unidad de disco que hospeda la biblioteca de contenido se llena. En primer lugar, agregue o identifique otro disco duro con espacio suficiente para hospedar la biblioteca de contenido. Luego use **ContentLibraryTransfer.exe** para transferir el contenido del disco duro antiguo lleno a la unidad nueva vacía.
 
Una vez completada la transferencia, el contenido es accesible a los equipos cliente desde la nueva ubicación.



## <a name="usage"></a>Uso 

Ejecute **ContentLibraryTransfer.exe** como usuario con permisos administrativos en el punto de distribución. 

#### <a name="syntax"></a>Sintaxis 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>Ejemplo
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>Limitaciones

- Ejecute la herramienta localmente en el punto de distribución. No se puede ejecutar desde un equipo remoto.  

- Úsela únicamente cuando los clientes no estén accediendo de forma activa al punto de distribución. Si ejecuta la herramienta mientras los clientes están accediendo al contenido, la biblioteca de contenido de la unidad de destino puede tener datos incompletos. Se puede producir un error en la transferencia de datos que dé lugar a una biblioteca de contenido completamente inutilizable.  

- No distribuya contenido al punto de distribución mientras se ejecuta la herramienta. Si ejecuta la herramienta mientras se está escribiendo contenido en el punto de distribución, la biblioteca de contenido de la unidad de destino puede tener datos incompletos. Se puede producir un error en la transferencia de datos que dé lugar a una biblioteca de contenido completamente inutilizable.



## <a name="see-also"></a>Consulte también

- [Conceptos básicos de la administración de contenido](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [La biblioteca de contenido](/sccm/core/plan-design/hierarchy/the-content-library)
