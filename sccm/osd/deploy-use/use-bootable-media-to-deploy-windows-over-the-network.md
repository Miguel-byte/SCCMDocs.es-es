---
title: Usar medios de arranque para implementar Windows a través de la red
titleSuffix: Configuration Manager
description: Use implementaciones de medios de arranque en System Center Configuration Manager para implementar el sistema operativo al iniciar el equipo de destino.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 98aa69cc0a80b12ca5caabb2c5b7167310ea2c83
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70892536"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Use medios de arranque para implementar Windows a través de la red con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede implementar el sistema operativo cuando el equipo de destino se inicia con una implementación de medios de arranque. Los medios contienen un puntero a la secuencia de tareas, la imagen del sistema operativo y otro contenido requerido de la red. Cuando se inicia el equipo de destino, el equipo recupera los elementos a los que hace referencia el puntero. Una vez que los medios de arranque liberan contenido, puede actualizar el destino sin tener que reemplazarlo en los medios.

Puede implementar sistemas operativos a través de la red mediante multidifusión en los siguientes escenarios de implementación de sistema operativo:

-   [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Reemplazar un equipo existente y transferir la configuración](replace-an-existing-computer-and-transfer-settings.md)  

Complete los pasos de uno de los escenarios de implementación de sistema operativo y luego use las secciones siguientes para usar medios de arranque para implementar el sistema operativo.  

## <a name="configure-deployment-settings"></a>Configurar la implementación  
Cuando use medios de arranque para iniciar el proceso de implementación del sistema operativo, configure la implementación para que el sistema operativo esté disponible para los medios. Puede configurar esta opción en la página **Configuración de implementación** del Asistente para implementar software o en la pestaña **Configuración de implementación** en las propiedades de la implementación. Para la opción de configuración **Estar disponible para** , configure uno de los siguientes:

-   Clientes de Configuration Manager, medios y PXE

-   Solo medios y PXE

-   Sólo medios y PXE (ocultos)

## <a name="create-the-bootable-media"></a>Crear medios de arranque
Puede especificar si el medio de arranque es una unidad flash USB o un conjunto de CD/DVD. El equipo que inicia el medio debe admitir la opción que elija como unidad de arranque. Para obtener más información, consulte [Crear medios de arranque](create-bootable-media.md).  

##  <a name="BKMK_Deploy"></a> Instalar el sistema operativo desde un medio de arranque  
Inserte el medio de arranque en una unidad de arranque en el equipo y luego vuelva a encenderlo para instalar el sistema operativo.
