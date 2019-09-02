---
title: Actualizar el sistema operativo de un equipo existente
titleSuffix: Configuration Manager
description: Puede usar varios métodos en Configuration Manager para la partición y el formato de un equipo existente, así como para instalar un nuevo sistema operativo en el equipo.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e2443f8ddc280e880ffb43a8e82bbc47b49d4395
ms.sourcegitcommit: 2d38de4846ea47a03cc884cbd3df27db48f64a6a
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2019
ms.locfileid: "70110210"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Actualizar un equipo existente con una nueva versión de Windows

*Se aplica a: System Center Configuration Manager (Rama actual)*

Utilice Configuration Manager para particionar y formatear un equipo existente y, a continuación, instalar un nuevo sistema operativo. Este proceso se denomina a veces volver a *Imaging* o *borrar y cargar*. Para este escenario, puede elegir entre muchos métodos de implementación diferentes, como PXE, el medio de arranque o el Centro de software. También puede usar un punto de migración de estado para almacenar la configuración y, a continuación, restaurarla en el nuevo sistema operativo.

Para elegir el escenario de implementación de sistema operativo adecuado, consulte [escenarios para implementar sistemas operativos de empresa](/sccm/osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems).  

## <a name="BKMK_Plan"></a> Plan  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>Planeación e implementación de los requisitos de infraestructura

Hay varios requisitos de infraestructura que deben cumplirse para poder implementar un sistema operativo. Algunos de estos requisitos incluyen Windows ADK, el Herramienta de migración de estado de usuario (USMT) y servicios de implementación de Windows (WDS). Para más información, vea [Requisitos de infraestructura para la implementación de SO en Configuration Manager](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

### <a name="install-a-state-migration-point"></a>Instalar un punto de migración de estado

Si desea capturar la configuración de un equipo existente y, a continuación, restaurar la configuración en el nuevo sistema operativo, considere la posibilidad de usar un punto de migración de estado. Para obtener más información, consulte [State migration point](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_StateMigrationPoints) (Punto de migración de estado).  

## <a name="BKMK_Configure"></a> Configurar  

### <a name="prepare-a-boot-image"></a>Preparar una imagen de arranque

Las imágenes de arranque inician un equipo en un entorno de Windows PE. Windows PE es un sistema operativo mínimo con componentes y servicios limitados. En Windows PE, Configuration Manager puede instalar un sistema operativo Windows completo en el equipo.

Vea los siguientes artículos para más información:

- [Administrar imágenes de arranque](/sccm/osd/get-started/manage-boot-images)

- [Personalizar imágenes de arranque](/sccm/osd/get-started/customize-boot-images)

- [Distribución de contenido](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute)

### <a name="prepare-an-os-image"></a>Preparar una imagen de sistema operativo

La imagen del sistema operativo contiene los archivos necesarios para instalar el sistema operativo en el equipo de destino.

Vea los siguientes artículos para más información:

- [Administración de imágenes del sistema operativo](/sccm/osd/get-started/manage-operating-system-images)

- [Distribución de contenido](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Creación de una secuencia de tareas para implementar un sistema operativo

Use una secuencia de tareas para automatizar la instalación del sistema operativo. Según el método de implementación que elija, puede haber consideraciones adicionales para la secuencia de tareas.

Vea los siguientes artículos para más información:

- [Creación de una secuencia de tareas para instalar un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system)

- [Administrar el estado de usuario](/sccm/osd/get-started/manage-user-state)

## <a name="BKMK_Deploy"></a> Implementar

- Para implementar el sistema operativo, use uno de los métodos de implementación siguientes:  

  - [Usar PXE para implementar Windows a través de la red](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network)  

  - [Usar multidifusión para implementar Windows a través de la red](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network)  

  - [Crear una imagen para un OEM en fábrica o en un almacén local](/sccm/osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot)  

  - [Use stand-alone media to deploy Windows without using the network](/sccm/osd/deploy-use/use-stand-alone-media-to-deploy-windows-without-using-the-network) (Uso de medios independientes para implementar Windows sin usar la red)  

  - [Usar medios de arranque para implementar Windows a través de la red](/sccm/osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network)  

  - [Usar Centro de software para implementar Windows a través de la red](/sccm/osd/deploy-use/use-software-center-to-deploy-windows-over-the-network)  

## <a name="monitor"></a>Monitor  

Para más información, vea [Supervisar las implementaciones de sistema operativo en System Center Configuration Manager](/sccm/osd/deploy-use/monitor-operating-system-deployments).  

> [!Note]
> Al restablecer la imagen inicial de un dispositivo UEFI, el administrador de arranque de Windows crea una nueva entrada en el cargador de arranque. Este comportamiento es más evidente cuando se restablece la imagen inicial de un dispositivo de forma repetida, como en un entorno de prueba o un laboratorio de estudiantes. Por lo general, no afecta al rendimiento ni al uso del dispositivo. Si la lista es demasiado grande, algunos dispositivos de hardware específicos pueden encontrar problemas funcionales. Por ejemplo, no arrancar en una unidad USB externa o no puede seleccionar la entrada de arranque actual de la lista. Use el comando **bcdedit** de Windows para borrar las entradas de arranque sin usar. Para obtener más información, vea [bcdedit/deletevalue](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--deletevalue).<!-- 2841926 -->
