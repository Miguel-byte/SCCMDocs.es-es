---
title: Crear medios de secuencia de tareas
titleSuffix: Configuration Manager
description: Cree medios de secuencia de tareas, como un CD, para implementar un sistema operativo en un equipo de destino en su entorno de Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 69c2f3620ed618711534366121aa1267efe6a8a5
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="create-task-sequence-media-with-system-center-configuration-manager"></a>Crear medios de secuencia de tareas con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede usar medios para capturar una imagen de sistema operativo de un equipo de referencia o implementar un sistema operativo en un equipo de destino en su entorno de System Center Configuration Manager. La creación de medios puede realizarse en un CD, un DVD o una unidad flash USB.  

 Los medios se usan mayoritariamente para implementar sistemas operativos en equipos de destino que no tienen una conexión de red o que tienen una conexión de bajo ancho de banda en el sitio de Configuration Manager. Sin embargo, los medios de implementación también se utilizan para iniciar una implementación de sistema operativo fuera de un sistema operativo Windows existente. Este segundo uso de los medios de implementación es importante, ya que a veces no hay ningún sistema operativo en el equipo de destino, el equipo de destino está en un estado no operativo o el usuario administrativo desea volver a particionar el disco duro del equipo de destino.  

 Los medios de implementación incluyen medios de arranque, medios independientes y medios preconfigurados. El contenido de los medios de implementación varía según el tipo de medios que utiliza. Por ejemplo, los medios independientes contienen la secuencia de tareas que implementa el sistema operativo, mientras que otros tipos de medios recuperan secuencias de tareas del punto de administración.  

> [!IMPORTANT]  
>  Para crear medios de secuencia de tareas, debe ser administrador en el equipo desde el que se ejecuta la consola de Configuration Manager. Si no es administrador, se le pedirán las credenciales de administrador al iniciar el Asistente para crear medio de secuencia de tareas.  

##  <a name="BKMK_PlanCaptureMedia"></a> Medios de captura de imágenes de sistema operativo  
 Los medios de captura le permiten capturar una imagen de sistema operativo desde un equipo de referencia. Los medios de captura contienen la imagen de arranque que inicia el equipo de referencia y la secuencia de tareas que captura la imagen de sistema operativo. Para obtener información sobre cómo crear medios de captura, consulte [Create capture media with System Center Configuration Manager](create-capture-media.md) (Crear medios de captura con System Center Configuration Manager).  

##  <a name="BKMK_PlanBootableMedia"></a> Implementaciones de sistema operativo de medios de arranque  
 El medio de arranque contiene solo la imagen de arranque, los [comandos de preinicio](../understand/prestart-commands-for-task-sequence-media.md) opcionales y los archivos necesarios, además de los archivos binarios de Configuration Manager. Cuando se inicia el equipo de destino, se conecta a la red y se recupera la secuencia de tareas, la imagen de sistema operativo y cualquier otro tipo de contenido necesario de la red. Dado que la secuencia de tareas no está en el medio, puede cambiar la secuencia de tareas o el contenido sin tener que volver a crear el medio.  

> [!IMPORTANT]  
>  Los paquetes en el medio de arranque no se cifran. El usuario administrativo debe adoptar las medidas de seguridad adecuadas, como agregar una contraseña a los medios, para asegurarse de que el contenido del paquete está protegido contra usuarios no autorizados.  

 Para obtener información sobre cómo crear un medio de arranque, consulte [Create bootable media](create-bootable-media.md) (Crear medios de arranque).  

##  <a name="BKMK_PlanPrestagedMedia"></a> Implementaciones de sistema operativo de medios preconfigurados  
 Los medios preconfigurados permiten preconfigurar medios de arranque y una imagen de sistema operativo en un disco duro antes del proceso de aprovisionamiento. Los medios preconfigurados son un archivo Windows Imaging Format (WIM) que puede ser instalado en un equipo sin sistema operativo por el fabricante o en un centro de configuración empresarial no relacionado con el entorno de Configuration Manager.  

 Los medios preconfigurados contienen la imagen de arranque que se utiliza para iniciar el equipo de destino y la imagen de sistema operativo que se aplica al equipo de destino. También puede especificar las aplicaciones, los paquetes y los paquetes de controladores que quiere incluir como parte de los medios preconfigurados. La secuencia de tareas que implementa el sistema operativo no se incluye en el medio. Al implementar una secuencia de tareas que usa un medio preconfigurado, el asistente comprueba en primer lugar la presencia de contenido válido en la memoria caché local de la secuencia de tareas y, si el contenido no se encuentra o se ha revisado, el asistente lo descarga del punto de distribución.  

 Los medios preconfigurados se aplican a la unidad de disco duro de un nuevo equipo antes de enviar el equipo al usuario final. Cuando el equipo se inicia por primera vez después de la aplicación del medio preconfigurado, el equipo inicia Windows PE y se conecta a un punto de administración para encontrar la secuencia de tareas que completa el proceso de implementación de sistema operativo.  

> [!IMPORTANT]  
>  Los paquetes en el medio de preconfigurado no se cifran. El usuario administrativo debe adoptar las medidas de seguridad adecuadas, como agregar una contraseña a los medios, para asegurarse de que el contenido del paquete está protegido contra usuarios no autorizados.  

 Para obtener información sobre cómo crear medios preconfigurados, consulte [Create prestaged media](create-prestaged-media.md) (Crear medios preconfigurados).  

##  <a name="BKMK_PlanStandaloneMedia"></a> Implementaciones de sistema operativo de medios independientes  
 Los medios independientes contienen todo lo necesario para implementar el sistema operativo. Esto incluye la secuencia de tareas y demás elementos necesarios. Ya que todo lo necesario para implementar el sistema operativo se guarda en el medio independiente, el espacio en disco necesario para el medio independiente es significativamente mayor que el espacio en disco necesario para otros tipos de medios.  

 Para obtener información sobre cómo crear medios independientes, consulte [Create stand-alone media](create-stand-alone-media.md) (Crear medios independientes).  

## <a name="media-considerations-when-using-site-systems-configured-for-https"></a>Consideraciones de medios al usar sistemas de sitio configurados para HTTPS  
 Cuando su punto de administración y sus puntos de distribución están configurados para usar la comunicación HTTPS, debe crear medios de arranque y medios preconfigurados en un sitio primario; no los cree en el sitio de administración central. Además, tenga en cuenta lo siguiente para determinar si se configura el medio como dinámico o de sitio:  

-   Para configurar el medio como dinámico, todos los sitios primarios deben tener la entidad de certificación raíz del sitio desde el que se creó el medio. Puede importar la entidad de certificación raíz en todos los sitios primarios en la jerarquía.  

-   Si los sitios primarios de su jerarquía de Configuration Manager usan otras entidades de certificación raíz, debe usar medios basados en sitio en cada sitio.  
