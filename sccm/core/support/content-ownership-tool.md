---
title: Content Ownership Tool
titleSuffix: Configuration Manager
description: Use Content Ownership Tool para cambiar la propiedad de los paquetes huérfanos en Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 500a59b4af9f1d25a1e0b5e82ba0a75bfa23df88
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500877"
---
# <a name="content-ownership-tool"></a>Content Ownership Tool

*Se aplica a: System Center Configuration Manager (Rama actual)*

Content Ownership Tool es una de las [herramientas de Configuration Manager](/sccm/core/support/tools). Cambia la propiedad de los paquetes huérfanos en Configuration Manager. Los paquetes huérfanos no tienen un servidor de sitio propietario. Los paquetes pueden quedar huérfanos quitando el servidor de sitio mientras todavía los poseía este servidor de sitio.

Ejecute Content Ownership Tool en cualquier servidor de sitio en la jerarquía de Configuration Manager. Inicie sesión como un usuario administrativo con suficientes permisos de paquete.  

> [!Tip]  
> Use **ContentLibraryCleanup.exe** en `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` para *quitar* contenido huérfano desde un punto de distribución. Para obtener más información, vea [Content Library Cleanup Tool](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool).  



## <a name="features"></a>Funciones

- Mostrar todos los paquetes huérfanos  

- Mostrar todos los paquetes, incluso si no están huérfanos  

- Ver el estado de la conexión a un sitio  

- Filtrar paquetes por nombre, código de sitio o tipo de paquete  

- Ordenar por cualquier columna mostrada  

- Cambiar la asignación de uno o varios paquetes con una sola acción  

- Ver el progreso de la actividad de transferencia de propiedad  



## <a name="usage"></a>Uso

Ejecute **ContentOwnershipTool.exe** para iniciar la herramienta. No se requieren permisos de administrador local en el equipo para ejecutar la herramienta.

No hay parámetros de línea de comandos.

> [!Important]   
> Esta herramienta cambia la propiedad de un paquete huérfano. El propio paquete no se mueve desde el punto de distribución en el que se almacena. Este cambio de propiedad no hace que el paquete actualice los puntos de distribución. Tampoco hace que los clientes vuelvan a evaluar la directiva para la implementación del paquete. Una vez que cambia la propiedad, asegúrese de que el nuevo servidor de sitio puede tener acceso a los archivos de origen. Debe tener al menos permisos de **lectura** a los archivos de origen de cada paquete. 



## <a name="see-also"></a>Consulte también

- [Conceptos básicos de la administración de contenido](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [La biblioteca de contenido](/sccm/core/plan-design/hierarchy/the-content-library)
