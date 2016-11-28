---
title: Asociar usuarios a un equipo de destino | Configuration Manager
description: Configure System Center Configuration Manager para asociar usuarios a equipos de destino al implementar sistemas operativos.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
caps.latest.revision: 9
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5339b5aba31efc06b46d0ffcfe37b5e05dcb839d


---
# <a name="associate-users-with-a-destination-computer-in-system-center-configuration-manager"></a>Asociar usuarios a un equipo de destino en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Si usa System Center Configuration Manager para implementar un sistema operativo, puede asociar usuarios al equipo de destino donde se ha implementado el sistema operativo. Esta configuración incluye lo siguiente:  

-   Que un solo usuario es el usuario primario del equipo de destino.  

-   Que varios usuarios son los usuarios primarios del equipo de destino.  

 La afinidad de dispositivo de usuario admite la administración centrada en el usuario para el proceso de implementación de aplicaciones. Si asocia un usuario con el equipo de destino en el que va a instalar un sistema operativo, puede implementar posteriormente aplicaciones para ese usuario. Las aplicaciones se instalarán automáticamente en el equipo de destino. Sin embargo, aunque puede configurar la compatibilidad para la afinidad de dispositivo de usuario al implementar sistemas operativos, no puede utilizar la afinidad de dispositivo de usuario para implementar sistemas operativos.  

 Para más información sobre la afinidad entre usuario y dispositivo, vea [Link users and devices with user device affinity (Vincular usuarios y dispositivos con afinidad entre usuario y dispositivo)](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

## <a name="how-to-specify-a-user-when-you-deploy-operating-systems"></a>Cómo especificar un usuario al implementar sistemas operativos  
 La tabla siguiente incluye las acciones que puede realizar para integrar la afinidad de dispositivo de usuario en las implementaciones de sistemas operativos. Puede integrar la afinidad de dispositivo de usuario en implementaciones de PXE, implementaciones de medios de arranque e implementaciones de medios preconfigurados.  

|Acción|Más información|  
|------------|----------------------|  
|Crear una secuencia de tareas que incluye la variable **SMSTSAssignUsersMode**|Agregue la variable **SMSTSAssignUsersMode** al principio de la secuencia de tareas mediante el paso de secuencia de tareas [Configurar variable de secuencia de tareas](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable). Esta variable especifica cómo administra la secuencia de tareas la información del usuario.<br /><br /> Establezca la variable en uno de los siguientes valores:<br /><br /> <br /><br /> **Automático**: la secuencia de tareas crea automáticamente una relación entre el usuario y el equipo de destino, e implementa el sistema operativo.<br /><br /> **Pendiente**: la secuencia de tareas crea una relación entre el usuario y el equipo de destino, pero espera la aprobación del usuario administrativo antes de implementar el sistema operativo.<br /><br /> **Deshabilitado**: La secuencia de tareas no asocia ningún usuario con el equipo de destino y continúa con la implementación del sistema operativo.<br /><br /> <br /><br /> Esta variable también se puede configurar en un equipo o una recopilación. Para más información sobre las variables integradas, vea [Variables integradas de secuencia de tareas en Configuration Manager](../../osd/understand/task-sequence-built-in-variables.md).|  
|Crear un comando de preinicio que recopila la información de usuario|El comando de preinicio puede ser un script de Visual Basic (VB) que tiene un cuadro de entrada, o una aplicación HTML (HTA) que valida los datos de usuario que se especifican.<br /><br /> El comando de preinicio debe establecer la variable **SMSTSUdaUsers** que se utiliza cuando se ejecuta la secuencia de tareas. Esta variable se puede establecer en un equipo, en una recopilación o en una variable de secuencia de tareas. Use el siguiente formato al agregar varios usuarios: *dominio\usuario1, dominio\usuario2, dominio\usuario3*.|  
|Configurar cómo asocian el usuario con el equipo de destino los puntos de distribución y los medios|Si [configura un punto de distribución para que acepte solicitudes de arranque PXE](https://technet.microsoft.com/library/mt627944\(TechNet.10\).aspx#BKMK_PXEDistributionPoint) y si crea [medios de arranque](http://technet.microsoft.com/library/mt627921\(TechNet.10\).aspx) o [medios preconfigurados](https://technet.microsoft.com/library/mt627922\(TechNet.10\).aspx) mediante el Asistente para crear medio de secuencia de tareas, puede especificar cómo admite el punto de distribución o el medio la asociación de los usuarios con el equipo de destino en el que está implementado el sistema operativo.<br /><br /> La configuración de la compatibilidad de la afinidad de dispositivo de usuario no tiene ningún método integrado que valide la identidad de usuario. Este aspecto puede ser importante si un técnico que lleva a cabo el aprovisionamiento del equipo introduce información en nombre del usuario. Además de configurar cómo administra la información de usuario la secuencia de tareas, la configuración de estas opciones en el punto de distribución y en el medio permite restringir las implementaciones que se inician desde un arranque PXE o un tipo de medio determinado.|  



<!--HONumber=Nov16_HO1-->


