---
title: "Actualizar Windows a la versión más reciente | Microsoft Docs"
description: "Obtenga información sobre cómo usar medios independientes o el Centro de software de Configuration Manager para actualizar un sistema operativo de Windows 7 o una versión posterior a Windows 10."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
caps.latest.revision: 13
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 147841212dbb85dd9d4ee7c8a79ca7869584fd99


---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>Actualizar Windows a la versión más reciente con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

En este tema, se indican las etapas de System Center Configuration Manager para actualizar un sistema operativo en un equipo de Windows 7 o una versión posterior a Windows 10. Puede elegir entre distintos métodos de implementación, como medios independientes o el Centro de software. Escenario de actualización local de Windows 10:  

-   Actualiza el sistema operativo en equipos que ejecutan actualmente Windows 7, Windows 8 o Windows 8.1. También puede realizar actualizaciones de compilación a compilación de Windows 10. Por ejemplo, puede actualizar Windows 10 RTM a Windows 10, versión 1511.  

-   Conserva las aplicaciones, la configuración y los datos de usuario en el equipo.  

-   No tiene dependencias externas, como Windows ADK.  

-   Por lo general, es más rápido y resistente que las implementaciones de sistema operativo tradicionales.  

 Use las secciones siguientes para implementar sistemas operativos a través de la red mediante una secuencia de tareas.  

##  <a name="a-namebkmkplana-plan"></a><a name="BKMK_Plan"></a> Plan  

-   **Revisar las limitaciones de la secuencia de tareas para actualizar un sistema operativo**  

     Revise los siguientes requisitos y limitaciones de la secuencia de tareas actualizar un sistema operativo y asegurarse de que satisface sus necesidades:  

    -   Solo debe agregar las etapas de la secuencia de tareas que estén relacionadas con la tarea principal de la implementación de sistemas operativos y la configuración de equipos tras la instalación de la imagen. Esto incluye las etapas que instalan paquetes, aplicaciones o actualizaciones, y las etapas que ejecutan líneas de comandos, PowerShell o establecen variables dinámicas.  

    -   Revise los controladores y las aplicaciones que están instalados en los equipos para asegurarse de que sean compatibles con Windows 10 antes de implementar la secuencia de tareas de actualización.  

    -   Las tareas siguientes no son compatibles con la actualización local y requieren que use las implementaciones de sistema de operativo tradicionales:  

        -   Cambiar la pertenencia a dominios de los equipos o actualizar los administradores locales.  

        -   Implementar un cambio fundamental en el equipo, como la partición del disco, cambiar una arquitectura de x86 a x64, implementar UEFI o modificar el idioma del sistema operativo base.  

        -   Tiene requisitos personalizados, como el uso de una imagen base personalizada, el uso de cifrado de disco de terceros<sup></sup> o requerir operaciones de WinPE sin conexión.  

-   **Planear e implementar los requisitos de infraestructura**  

     Los únicos requisitos previos para el escenario de actualización es que tiene un punto de distribución disponible para el paquete de actualización de sistema operativo y otros paquetes que incluya en la secuencia de tareas. Para obtener más información, consulte [Instalar o modificar un punto de distribución](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).

##  <a name="a-namebkmkconfigurea-configure"></a><a name="BKMK_Configure"></a> Configurar  

1.  **Preparar el paquete de actualización del sistema operativo**  

     El paquete de actualización de Windows 10 contiene los archivos de origen necesarios para actualizar el sistema operativo en el equipo de destino. El paquete de actualización debe coincidir en la edición, la arquitectura y el idioma con los clientes que va a actualizar.  Para más información, consulte [Administrar paquetes de actualización de sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  

2.  **Crear una secuencia de tareas para actualizar el sistema operativo**  

     Siga los pasos que aparecen en [Crear una secuencia de tareas para actualizar un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) para automatizar la actualización del sistema operativo.  

    > [!NOTE]  
    >  Normalmente, usará los pasos de [Crear una secuencia de tareas para actualizar un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) para crear una secuencia de tareas para actualizar un sistema operativo a Windows 10. La secuencia de tareas incluye el paso Actualizar sistema operativo, así como pasos adicionales recomendados y grupos para controlar el proceso de actualización integral. En cambio, puede crear una secuencia de tareas personalizada y agregar el paso [Actualizar sistema operativo](../understand/task-sequence-steps.md#BKMK_UpgradeOS) de la secuencia de tareas para actualizar el sistema operativo. Esta es la única etapa necesaria para actualizar el sistema operativo a Windows 10. Si elige este método, agregue también el paso [Reiniciar equipo](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer) después del paso Actualizar sistema operativo para completar la actualización. Asegúrese de usar la opción **El sistema operativo predeterminado instalado actualmente** para reiniciar el equipo con el sistema operativo instalado y no con Windows PE.  

##  <a name="a-namebkmkdeploya-deploy"></a><a name="BKMK_Deploy"></a> Implementar  

-   Use uno de los siguientes métodos de implementación para implementar el sistema operativo:  

    -   [Usar Centro de software para implementar Windows a través de la red](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Usar medios independientes para implementar Windows sin usar la red](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

## <a name="monitor"></a>Monitor  

-   **Supervisar la implementación de la secuencia de tareas**  

     Para supervisar la implementación de la secuencia de tareas para actualizar el sistema operativo, consulte [Monitor operating system deployments (Supervisar implementaciones del sistema operativo)](monitor-operating-system-deployments.md).  



<!--HONumber=Dec16_HO3-->


