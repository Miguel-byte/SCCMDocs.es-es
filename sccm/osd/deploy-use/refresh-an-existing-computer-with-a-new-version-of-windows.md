---
title: Actualizar un equipo existente con una nueva versión de Windows
titleSuffix: Configuration Manager
description: Puede usar varios métodos en Configuration Manager para la partición y el formato (borrado) de un equipo existente, así como para instalar un nuevo sistema operativo en el equipo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 622b49b9fb689db8238be8254a66b3a0264b4399
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350942"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows-using-system-center-configuration-manager"></a>Actualizar un equipo existente con una nueva versión de Windows mediante System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este tema se proporcionan las etapas generales de System Center Configuration Manager para la partición y el formato (borrado) de un equipo existente, así como para instalar un nuevo sistema operativo en el equipo. Para este escenario, puede elegir entre muchos métodos de implementación diferentes, como PXE, el medio de arranque o el Centro de software. También puede optar por instalar un punto de migración de estado para almacenar la configuración y, después, restaurarla en el nuevo sistema operativo después de instalarlo. Si no está seguro de si se trata del escenario de implementación de sistema operativo adecuado para usted, consulte [Escenarios para implementar sistemas operativos de empresa](scenarios-to-deploy-enterprise-operating-systems.md).  

 Use las secciones siguientes para actualizar un equipo existente con una nueva versión de Windows.  

##  <a name="BKMK_Plan"></a> Plan  

-   **Planear e implementar los requisitos de infraestructura**  

     Hay varios requisitos de infraestructura que deben cumplirse antes de implementar sistemas operativos, como Windows ADK, la Herramienta de migración de estado de usuario (USMT), los Servicios de implementación de Windows (WDS), las configuraciones compatibles de disco duro, etc. Para obtener más información, consulte [Infrastructure requirements for operating system deployment](../plan-design/infrastructure-requirements-for-operating-system-deployment.md) (Requisitos de infraestructura para la implementación de sistema operativo).  

-   **Instalar un punto de migración de estado (solo es necesario si se transfiere la configuración)**  

     Si se dispone a capturar la configuración del equipo existente para restaurarla posteriormente en el nuevo sistema operativo, debe instalar un punto de migración de estado. Para obtener más información, consulte [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints) (Punto de migración de estado).  

##  <a name="BKMK_Configure"></a> Configurar  

1.  **Preparar una imagen de arranque**  

     Las imágenes de arranque inician un equipo en un entorno de Windows PE (un sistema operativo mínimo con componentes y servicios limitados) que puede instalar un sistema operativo completo de Windows en el equipo.   Al implementar sistemas operativos, debe seleccionar una imagen de arranque para el uso y la distribución de la imagen en un punto de distribución. Para preparar la imagen de arranque, use lo siguiente:  

    -   Para obtener más información sobre las imágenes de arranque, consulte [Manage boot images (Administrar imágenes de arranque)](../get-started/manage-boot-images.md).  

    -   Para obtener más información sobre la personalización de una imagen de arranque, consulte [Customize boot images (Personalizar imágenes de arranque)](../get-started/customize-boot-images.md).  

    -   Distribuya la imagen de arranque a puntos de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Preparar una imagen de sistema operativo**  

     La imagen del sistema operativo contiene los archivos necesarios para instalar el sistema operativo en el equipo de destino. Use lo siguiente para preparar la imagen del sistema operativo:  

    -   Para obtener más información sobre cómo crear una imagen de sistema operativo, consulte [Manage operating system images (Administrar imágenes de sistema operativo)](../get-started/manage-operating-system-images.md).  

    -   Distribuya la imagen del sistema operativo a los puntos de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Crear una secuencia de tareas para implementar sistemas operativos a través de la red**  

     Use una secuencia de tareas para automatizar la instalación del sistema operativo a través de la red. Siga los pasos de [Crear una secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md). Según el método de implementación que elija, puede haber consideraciones adicionales para la secuencia de tareas.  

    > [!NOTE]  
    >  En este escenario, la secuencia de tareas da formato y realiza la partición de los discos duros en el equipo. Para capturar la configuración de usuario, debe usar el punto de migración de estado y seleccionar **Guardar archivos y configuración de usuario en un punto de migración de estado** en la página **Migración de estado** del Asistente para crear secuencia de tareas. Si guarda la configuración y los archivos de usuario localmente, se perderán al formatear el disco duro y Configuration Manager no podrá restaurar la configuración. Para obtener más información, consulte [Manage user state](../get-started/manage-user-state.md) (Administrar el estado de usuario).  

##  <a name="BKMK_Deploy"></a> Implementar  

-   Use uno de los siguientes métodos de implementación para implementar el sistema operativo:  

    -   [Usar PXE para implementar Windows a través de la red](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Usar multidifusión para implementar Windows a través de la red](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Crear una imagen para un OEM en fábrica o en un almacén local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Use stand-alone media to deploy Windows without using the network](use-stand-alone-media-to-deploy-windows-without-using-the-network.md) (Uso de medios independientes para implementar Windows sin usar la red)  

    -   [Usar medios de arranque para implementar Windows a través de la red](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Usar Centro de software para implementar Windows a través de la red](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Monitor  

-   **Supervisar la implementación de la secuencia de tareas**  

     Para supervisar la implementación de la secuencia de tareas para instalar el sistema operativo, consulte [Monitor operating system deployments (Supervisar implementaciones del sistema operativo)](monitor-operating-system-deployments.md).  
