---
title: Instalar Windows en un equipo nuevo con Configuration Manager | Microsoft Docs
description: Use Configuration Manager para instalar un sistema operativo en un equipo nuevo (sin sistema operativo) mediante el entorno PXE, OEM o medios independientes.
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
caps.latest.revision: 8
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 89158debdf4c345a325feeb608db2215a88ed81b
ms.openlocfilehash: 584dad7d8b05a2da9f7a66b73028ae99ff1a594f


---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-system-center-configuration-manager"></a>Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo) con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

En este tema se indican los pasos generales de System Center Configuration Manager para instalar un sistema operativo en un equipo nuevo. Para este escenario, puede elegir entre muchos métodos de implementación diferentes, como PXE, OEM o medios independientes. Si no está seguro de si se trata del escenario de implementación de sistema operativo adecuado para usted, consulte [Escenarios para implementar sistemas operativos de empresa](scenarios-to-deploy-enterprise-operating-systems.md).  

Use las secciones siguientes para actualizar un equipo existente con una nueva versión de Windows.  

##  <a name="a-namebkmkplana-plan"></a><a name="BKMK_Plan"></a> Plan  

-   **Planear e implementar los requisitos de infraestructura**  

     Hay varios requisitos de infraestructura que deben cumplirse antes de implementar sistemas operativos, como Windows ADK, los Servicios de implementación de Windows (WDS), las configuraciones compatibles de disco duro, etc. Para obtener más información, consulte [Infrastructure requirements for operating system deployment](../plan-design/infrastructure-requirements-for-operating-system-deployment.md) (Requisitos de infraestructura para la implementación de sistema operativo).

##  <a name="a-namebkmkconfigurea-configure"></a><a name="BKMK_Configure"></a> Configurar  

1.  **Preparar una imagen de arranque**  

     Las imágenes de arranque inician un equipo en un entorno de Windows PE (un sistema operativo mínimo con componentes y servicios limitados) que puede instalar un sistema operativo completo de Windows en el equipo.   Al implementar sistemas operativos, debe seleccionar una imagen de arranque para el uso y la distribución de la imagen en un punto de distribución. Para preparar la imagen de arranque, use lo siguiente:  

    -   Para obtener más información sobre las imágenes de arranque, consulte [Manage boot images (Administrar imágenes de arranque)](../get-started/manage-boot-images.md).  

    -   Para obtener más información sobre la personalización de una imagen de arranque, consulte [Customize boot images (Personalizar imágenes de arranque)](../get-started/customize-boot-images.md).  

    -   Distribuya la imagen de arranque a puntos de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).  

2.  **Preparar una imagen de sistema operativo**  

     La imagen del sistema operativo contiene los archivos necesarios para instalar el sistema operativo en el equipo de destino. Use lo siguiente para preparar la imagen del sistema operativo:  

    -   Para obtener más información sobre cómo crear una imagen de sistema operativo, consulte [Manage operating system images (Administrar imágenes de sistema operativo)](../get-started/manage-operating-system-images.md).

    -   Distribuya la imagen del sistema operativo a los puntos de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).

3.  **Crear una secuencia de tareas para implementar sistemas operativos a través de la red**  

     Use una secuencia de tareas para automatizar la instalación del sistema operativo a través de la red. Siga los pasos de [Crear una secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md). Según el método de implementación que elija, puede haber consideraciones adicionales para la secuencia de tareas.  

##  <a name="a-namebkmkdeploya-deploy"></a><a name="BKMK_Deploy"></a> Implementar  

-   Use uno de los siguientes métodos de implementación para implementar el sistema operativo:  

    -   [Usar PXE para implementar Windows a través de la red](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Usar multidifusión para implementar Windows a través de la red](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Crear una imagen para un OEM en fábrica o en un almacén local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Usar medios independientes para implementar Windows sin usar la red](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Usar medios de arranque para implementar Windows a través de la red](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Monitor  

-   **Supervisar la implementación de la secuencia de tareas**  

     Para supervisar la implementación de la secuencia de tareas para instalar el sistema operativo, consulte [Monitor operating system deployments (Supervisar implementaciones del sistema operativo)](monitor-operating-system-deployments.md).  



<!--HONumber=Jan17_HO4-->


