---
title: "Planeamiento de la interoperabilidad de la implementación de sistema operativo | Microsoft Docs"
description: "Comprenda los problemas de interoperabilidad cuando diferentes sitios de System Center Configuration Manager en una sola jerarquía usan versiones diferentes."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
caps.latest.revision: "10"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 50a4b75b8c8c1cb6f7a8e696abad285f99080fcd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-operating-system-deployment-interoperability-in-system-center-configuration-manager"></a>Planeamiento de la interoperabilidad de la implementación de sistema operativo en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Si en una misma jerarquía hay varios sitios de System Center Configuration Manager que usan versiones diferentes, no estarán disponibles algunas funciones de Configuration Manager. Normalmente, la funcionalidad de la versión más actual de Service Pack de Configuration Manager no es accesible en sitios o por clientes que ejecutan una versión anterior. Para obtener más información, consulte [Interoperabilidad entre diferentes versiones de System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

 Considere los siguientes puntos cuando actualice el sitio de nivel superior de la jerarquía y otros sitios de la jerarquía ejecuten Configuration Manager con una versión anterior:  

-   Paquete de instalación de cliente  

    -   El origen del paquete de instalación de cliente predeterminado se actualiza automáticamente y todos los puntos de distribución de la jerarquía se actualizan con el paquete de instalación de cliente nuevo, incluso en aquellos puntos de distribución de sitios de la jerarquía que tienen una versión inferior.  

    -   Los clientes que ejecutan la nueva versión no se pueden asignar a sitios que aún no se actualizaron a dicha versión. Asignación se bloquea en el punto de administración.  

-   Imágenes de arranque  

    -   Si actualiza el sitio de primer nivel a la última versión de Configuration Manager, las imágenes de arranque predeterminadas (x86 y x64) se actualizan automáticamente a imágenes de arranque basadas en Windows ADK para Windows 10, que usan Windows PE 10. Los archivos asociados a las imágenes de arranque predeterminadas se actualizan con la versión de Configuration Manager más reciente de los archivos. Las imágenes de arranque personalizadas no se actualizan automáticamente. Deberá actualizar las imágenes de arranque personalizadas manualmente, incluidas las versiones anteriores de Windows PE.  

    -   No use medios dinámicos si la jerarquía de sitio contiene sitios con versiones diferentes de Configuration Manager. En su lugar, use medios basados en el sitio para establecer contacto con un punto de administración concreto hasta que todos los sitios se actualicen a la misma versión de Configuration Manager.  

    -   Compruebe que las imágenes de arranque de Configuration Manager más recientes contienen las personalizaciones pertinentes y, después, actualice todos los puntos de distribución en los sitios con la versión más reciente de Configuration Manager con las imágenes de arranque nuevas.  

-   Herramienta de migración de estado de usuario (USMT)  

    -   Si actualiza el sitio de primer nivel a la última versión de Configuration Manager, el paquete de USMT predeterminado también se actualizará automáticamente a esta versión. Los paquetes USMT personalizados no se actualizan automáticamente. Por tanto, tendrá que actualizarlos manualmente.  

-   Nuevas etapas de la secuencia de tareas  

    -   Periódicamente, se introducen nuevas etapas en la secuencia de tareas con las nuevas versiones de Configuration Manager. Al implementar una secuencia de tareas con una nueva etapa en clientes más antiguos, se producirá un error en la etapa de la secuencia de tareas. Antes de implementar una secuencia de tareas con una nueva etapa, asegúrese de que los clientes de la recopilación de destino están actualizados a la nueva versión.  

-   Medios de implementación del sistema operativo  

    -   Siempre que el sitio se actualice a una nueva versión, todos los medios (de arranque, de captura, preconfigurados e independientes) deben actualizarse con el nuevo paquete de cliente de Configuration Manager.  

-   Extensiones de terceros para la implementación del sistema operativo  

    -   Si dispone de extensiones de terceros para la implementación del sistema operativo y tiene diferentes versiones de los sitios o clientes de Configuration Manager (es decir, una jerarquía mixta), puede haber problemas con las extensiones.  

 Durante la actualización activa de sitios de la jerarquía, use las siguientes secciones para las implementaciones de sistema operativo.  

## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Versión más reciente de los sitios de Configuration Manager en una jerarquía mixta  
 Cuando actualiza un sitio a la versión más reciente de Configuration Manager, las secuencias de tareas que hacen referencia al paquete de instalación de cliente predeterminado se iniciarán automáticamente para implementar la versión de cliente de Configuration Manager más reciente. Las secuencias de tareas que hagan referencia a un paquete de instalación de cliente personalizado seguirán implementando la versión del cliente incluida en dicho paquete personalizado (probablemente una versión anterior del cliente de Configuration Manager). Estas secuencias de tareas deben actualizarse para evitar errores en su implementación. Si tiene una secuencia de tareas configurada para usar un paquete de instalación de cliente personalizado, debe actualizar la etapa de la secuencia de tareas para que use la versión de Configuration Manager más reciente del paquete de instalación de cliente o actualizar el paquete personalizado para que use el origen de instalación de cliente de Configuration Manager más reciente.  

> [!IMPORTANT]  
>  No implemente secuencias de tareas que hagan referencia al paquete de instalación del cliente de Configuration Manager más reciente en clientes que se encuentren en un sitio de Configuration Manager más antiguo. Cuando se actualizan los clientes asignados a un sitio de Configuration Manager anterior a la última versión de cliente de Configuration Manager, Configuration Manager bloquea la asignación del anterior sitio de Configuration Manager. Por tanto, el cliente ya no estará asignado a ningún sitio y permanecerá sin administrar hasta que lo asigne manualmente al sitio de Configuration Manager más reciente o reinstale la versión anterior del cliente de Configuration Manager en el equipo.  

## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Versiones anteriores de Configuration Manager en una jerarquía mixta  
 Una vez que el sitio de administración central se actualiza a la última versión de Configuration Manager, debe pasar a la etapa siguiente para asegurarse de que las secuencias de tareas de implementación del sistema operativo que se implementen en clientes asignados a un sitio de Configuration Manager (y que aún no se hayan actualizado a la versión más reciente del mismo) no dejen dichos clientes en un estado no administrado.  

-   Cree una secuencia de tareas y úsela para implementarla exclusivamente en clientes que se encuentren en un sitio de Configuration Manager. Lo más probable es que cree una copia de una secuencia de tareas, que usará para implementarla en clientes que se encuentren en un sitio de Configuration Manager con la última versión, y que la modifique posteriormente para poder implementarla en clientes de un sitio de Configuration Manager más antiguo. Después, tendrá que configurar la secuencia de tareas para que haga referencia al paquete de instalación de cliente personalizado que usa el origen de instalación del cliente de Configuration Manager más reciente. Si aún no tiene un paquete de instalación de cliente personalizado que haga referencia al origen de instalación del cliente de Configuration Manager más antiguo, deberá crear uno manualmente.  
