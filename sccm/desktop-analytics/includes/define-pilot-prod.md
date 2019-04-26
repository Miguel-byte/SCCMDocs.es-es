---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8305102657a5973c19ca161f65204587954b0232
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62231923"
---
Para diferenciar entre piloto y de producción, use las siguientes definiciones:  

- **Piloto**: Un subconjunto de los dispositivos que desea validar antes de implementar en un conjunto más amplio. Usar análisis de escritorio para marcar los dispositivos como único para el conjunto de piloto. Los dispositivos en el proyecto piloto están preparados para actualizarse cuando no se bloquea ningún recurso. Un recurso de bloqueo está marcado como *críticos* y *no se puede* para actualizar.  

- **Production**: Todos los demás dispositivos inscriben en análisis de escritorio que no están en la prueba piloto. Dispositivos de producción están preparados para actualizarse cuando todos los recursos están aprobada. Análisis de escritorio apruebe automáticamente los recursos que no son críticos.  

