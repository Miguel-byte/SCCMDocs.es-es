---
title: Asociar usuarios a un equipo
titleSuffix: Configuration Manager
description: Configure Configuration Manager para asociar usuarios a equipos de destino al implementar sistemas operativos.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: de06556d6fbf785e08e5c14f7e0ee1b09458feaf
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68340401"
---
# <a name="associate-users-with-a-destination-computer-in-configuration-manager"></a>Asocie usuarios a un equipo de destino en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Si utiliza Configuration Manager para implementar sistemas operativos, puede asociar los usuarios con el equipo de destino. Esta opción funciona con independencia de que sea un solo usuarios o sean varios usuarios los usuarios primarios del equipo de destino.  

La afinidad de dispositivo de usuario admite la administración centrada en el usuario para el proceso de implementación de aplicaciones. Si asocia un usuario con el equipo de destino en el que va a instalar un sistema operativo, puede implementar posteriormente aplicaciones para ese usuario. Las aplicaciones se instalarán automáticamente en el equipo de destino. Aunque puede configurar la compatibilidad para la afinidad de dispositivo de usuario durante la implementación del sistema operativo, no puede usar la afinidad de dispositivo de usuario para implementar el sistema operativo.  

Para más información sobre la afinidad entre usuario y dispositivo, vea [Link users and devices with user device affinity (Vincular usuarios y dispositivos con afinidad entre usuario y dispositivo)](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  

Existen varios métodos por los que puede integrar la afinidad de dispositivo de usuario en las implementaciones de sistema operativo. Puede integrar la afinidad de dispositivo de usuario en implementaciones de PXE, implementaciones de medios de arranque e implementaciones de medios preconfigurados.  


### <a name="create-a-task-sequence-that-includes-the-smstsassignusersmode-variable"></a>Crear una secuencia de tareas que incluye la variable **SMSTSAssignUsersMode**

Agregue la variable **SMSTSAssignUsersMode** al principio de la secuencia de tareas mediante el paso [Configurar variable de secuencia de tareas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable). Esta variable especifica cómo administra la secuencia de tareas la información del usuario.

Para más información, vea [Task sequence variables](/sccm/osd/understand/task-sequence-variables#SMSTSAssignUsersMode) (Variables de secuencia de tareas).


### <a name="create-a-prestart-command-that-gathers-the-user-information"></a>Crear un comando de preinicio que recopila la información de usuario

El comando de preinicio puede ser un VBScript con un cuadro de entrada. También puede ser una aplicación HTML (HTA) que valida los datos de usuario que escriban. 

Este comando de preinicio debe establecer la variable **SMSTSUDAUsers** que se utiliza cuando se ejecuta la secuencia de tareas. Esta variable se puede establecer en un equipo, en una recopilación o en una variable de secuencia de tareas.

Para más información, vea [Task sequence variables](/sccm/osd/understand/task-sequence-variables#SMSTSUDAUsers) (Variables de secuencia de tareas).


### <a name="configure-how-distribution-points-and-media-associate-the-user-with-the-destination-computer"></a>Configurar cómo asocian el usuario con el equipo de destino los puntos de distribución y los medios

El punto de distribución o el medio admite la asociación de los usuarios con el equipo de destino donde se implementa el sistema operativo. Use uno de los métodos siguientes: 

- [Configurar un punto de distribución para aceptar solicitudes de arranque PXE](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_PXEDistributionPoint)  
- [Crear medios de arranque](/sccm/osd/deploy-use/create-bootable-media)  
- [Crear medios preconfigurados](/sccm/osd/deploy-use/create-prestaged-media)  


La configuración de la compatibilidad de la afinidad de dispositivo de usuario no tiene ningún método integrado que valide la identidad de usuario. Este comportamiento es importante si un técnico que lleva a cabo el aprovisionamiento del equipo introduce información en nombre del usuario. Además de configurar cómo administra la información de usuario la secuencia de tareas, la configuración de estas opciones en el punto de distribución y en el medio permite restringir las implementaciones que se inician desde un arranque PXE o un tipo de medio determinado.
