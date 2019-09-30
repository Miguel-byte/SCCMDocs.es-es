---
title: Procedimientos recomendados para las colecciones
titleSuffix: Configuration Manager
description: Obtenga los procedimientos recomendados para las recopilaciones de Configuration Manager.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ee91fe8b8b5b1c8d737e5818f42fa08e689a7e5a
ms.sourcegitcommit: 670cfed1e47a7a4a73aa4ccb873c6312be3c21ff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71311535"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Procedimientos recomendados para recopilaciones en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use los procedimientos recomendados siguientes para las recopilaciones de Configuration Manager.  

## <a name="dont-use-incremental-updates-with-many-collections"></a>No use actualizaciones incrementales con muchas recopilaciones.

Cuando se habilita la opción **Usar actualizaciones incrementales para esta recopilación** , esta configuración puede provocar retrasos de evaluación cuando se habilita para muchas recopilaciones. El umbral es de aproximadamente 200 recopilaciones en la jerarquía. El número exacto depende de los siguientes factores:  

- El número total de recopilaciones  

- La frecuencia con la que se agregan y cambian recursos nuevos en la jerarquía  

- El número de clientes en la jerarquía  

- La complejidad de las reglas de pertenencia a la recopilación en la jerarquía  

## <a name="maintenance-window-size-for-software-updates"></a>Tamaño de la ventana de mantenimiento de las actualizaciones de software

Puede configurar ventanas de mantenimiento para que las colecciones de dispositivos restrinjan las horas a las que Configuration Manager puede instalar software en estos dispositivos. Si configura una ventana de mantenimiento demasiado pequeña, es posible que el cliente no pueda instalar las actualizaciones de software imprescindibles, lo que hace que el cliente sea vulnerable a los ataques que la actualización de software mitiga. 
 
 > [!Tip] 
 > Consideraciones importantes que se deben tener en cuenta al planear las ventanas de mantenimiento:
 > - El tiempo de ejecución máximo de actualización de software predeterminado es de 60 minutos.
 > - Cuando Configuration Manager calcula si una actualización puede instalarse, se agregan cinco minutos al tiempo de ejecución máximo para tener en cuenta el reinicio.
 > - La duración restante de una ventana de mantenimiento debe ser mayor que el tiempo de ejecución máximo de la actualización de software más cinco minutos.
 
