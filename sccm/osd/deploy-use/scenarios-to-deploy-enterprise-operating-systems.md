---
title: Escenarios para implementar sistemas operativos de empresa
titleSuffix: Configuration Manager
description: Obtenga información sobre distintos escenarios para implementar sistemas operativos de empresa con System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92b968a8dae63d15e087e098452b56b0397c7b78
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137582"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-system-center-configuration-manager"></a>Escenarios para implementar sistemas operativos de empresa con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los siguientes escenarios de implementación de sistema operativo están disponibles en System Center Configuration Manager:  

-   [Actualizar Windows a la versión más reciente](upgrade-windows-to-the-latest-version.md): este escenario actualiza el sistema operativo en equipos que ejecutan actualmente Windows 7, Windows 8, Windows 8.1 o Windows 10. El proceso de actualización conserva las aplicaciones, la configuración y los datos de usuario en el equipo. No hay dependencias externas, como Windows ADK, y este proceso es más rápido y más flexible que las implementaciones de sistema operativo tradicionales.  

-   [Actualizar un equipo existente con una versión nueva de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md): este escenario realiza la partición y formatea (borra) un equipo existente, e instala un sistema operativo nuevo en el equipo. Puede migrar la configuración y los datos de usuario después de instalar el sistema operativo.  

-   [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md): este escenario instala un sistema operativo en un equipo nuevo. Se trata de una instalación nueva del sistema operativo y no incluye los valores de configuración ni la migración de datos de usuario.  

-   [Reemplazar un equipo existente y transferir la configuración](replace-an-existing-computer-and-transfer-settings.md): este escenario instala un sistema operativo en un equipo nuevo. Opcionalmente, puede migrar la configuración y los datos de usuario del equipo antiguo al nuevo.  

## <a name="things-to-consider-before-you-deploy-operating-system-images"></a>Aspectos a tener en cuenta antes de implementar imágenes de sistema operativo  
 Es necesario considerar ciertos aspectos antes de implementar un sistema operativo.  

### <a name="operating-system-image-size"></a>Tamaño de la imagen del sistema operativo  
 El tamaño de una imagen de sistema operativo puede ser bastante grande. Por ejemplo, el tamaño de la imagen de Windows 7 es 3 gigabytes (GB) o más. El tamaño de la imagen y el número de equipos en que implementa al mismo tiempo el sistema operativo afecta al rendimiento de la red y al ancho de banda disponible. Asegúrese de probar el rendimiento de la red para evaluar mejor el efecto que podría tener la implementación de la imagen y el tiempo necesario para completarla. Las actividades de Configuration Manager que afectan al rendimiento de la red incluyen la distribución de la imagen a un punto de distribución, la distribución de la imagen de un sitio a otro y la descarga de la imagen al cliente de Configuration Manager.  

 Asegúrese también de que planea suficiente espacio de almacenamiento en disco en los puntos de distribución que hospedan las imágenes del sistema operativo.  

### <a name="client-cache-size"></a>Tamaño de la caché de cliente  
 Cuando los clientes de Configuration Manager descargan contenido, usan automáticamente el servicio de transferencia inteligente en segundo plano (BITS) si está disponible. Cuando implementa una secuencia de tareas que instala un sistema operativo, puede establecer una opción en la implementación de forma que los clientes de Configuration Manager descarguen la imagen completa en una memoria caché local antes de que se ejecute la secuencia de tareas.  

 En general, cuando un cliente de Configuration Manager debe descargar una imagen de sistema operativo (o cualquier otro paquete), pero no hay suficiente espacio en la memoria caché, el cliente comprueba los otros paquetes de la caché para determinar si la eliminación de alguno de los paquetes más antiguos (o todos) liberará espacio suficiente en el disco para la imagen. Si la eliminación paquetes no libera suficiente espacio en disco, el cliente no descarga la imagen y se produce un error en la implementación. Esto puede ocurrir si la memoria caché tiene un paquete grande que está configurado para conservarse en la memoria caché. Si la eliminación de paquetes libera suficiente espacio en disco en la memoria caché, el cliente los elimina y luego descarga la imagen en la caché.  

 El tamaño de caché predeterminado en clientes de Configuration Manager puede no ser lo suficientemente grande para la mayoría de las implementaciones de imagen de sistema operativo. Si planea descargar la imagen completa a la caché del cliente, debe ajustar el tamaño de la caché del cliente de Configuration Manager en los equipos de destino para acomodar el tamaño de la imagen que va a implementar.  

 Para obtener más información, vea [Configurar la caché del cliente para clientes de Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

## <a name="task-sequence-deployments"></a>Implementaciones de secuencia de tareas  
 La secuencia de tareas que cree puede implementar la imagen del sistema operativo en un equipo cliente de Configuration Manager de una de las formas siguientes:  

- Descargar primero la imagen y su contenido en la caché del cliente de Configuration Manager desde un punto de distribución y, a continuación, instalarla.  

- Instalar inmediatamente la imagen y su contenido desde el punto de distribución.  

- Instalar la imagen y su contenido a medida que sea necesario desde el punto de distribución.  

  De forma predeterminada, cuando crea la implementación para la secuencia de tareas, la imagen se descarga primero en la caché de cliente de Configuration Manager y luego se instala. Si elige descargar la imagen a la caché de cliente de Configuration Manager antes de ejecutar la imagen y la secuencia de tareas contiene una etapa para volver a particionar el disco duro, esta etapa produce un error porque, al particionar el disco duro, se borra el contenido de la caché de cliente de Configuration Manager. Si la secuencia de tareas debe volver a particionar el disco duro, debe ejecutar la instalación de la imagen desde el punto de distribución mediante la opción **Ejecutar programa desde el punto de distribución**  cuando implemente la secuencia de tareas.  

  Para obtener más información, vea [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  
