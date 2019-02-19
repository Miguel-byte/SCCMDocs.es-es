---
title: Procedimientos recomendados para las colecciones
titleSuffix: Configuration Manager
description: Conozca procedimientos recomendados para las colecciones en System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1c685cf4efd5eca5f93694edd4a01715120df9a8
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140582"
---
# <a name="best-practices-for-collections-in-system-center-configuration-manager"></a>Procedimientos recomendados para recopilaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use los procedimientos recomendados siguientes para las colecciones en System Center Configuration Manager.  

## <a name="do-not-use-incremental-updates-for-a-large-number-of-collections"></a>No realice actualizaciones incrementales en un gran número de recopilaciones.  
 Cuando se habilita la opción **Usar actualizaciones incrementales para esta recopilación** , esta configuración puede provocar retrasos de evaluación cuando se habilita para muchas recopilaciones. El umbral es de aproximadamente 200 recopilaciones en la jerarquía. El número exacto depende de los siguientes factores:  

-   El número total de recopilaciones  

-   La frecuencia con la que se agregan y cambian recursos nuevos en la jerarquía  

-   El número de clientes en la jerarquía  

-   La complejidad de las reglas de pertenencia a la recopilación en la jerarquía  

## <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Asegúrese de que las ventanas de mantenimiento son lo suficientemente grandes como para implementar las actualizaciones de software imprescindibles  
 Puede configurar ventanas de mantenimiento para que las colecciones de dispositivos restrinjan las horas a las que Configuration Manager puede instalar software en estos dispositivos. Si configura una ventana de mantenimiento demasiado pequeña, es posible que el cliente no pueda instalar las actualizaciones de software imprescindibles, lo que hace que el cliente sea vulnerable a los ataques que la actualización de software mitiga.  
