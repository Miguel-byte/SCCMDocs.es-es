---
title: Crear una secuencia de tareas para implementaciones que no son de sistema operativo | Microsoft Docs
description: "Cree secuencias de tareas que no estén relacionadas con la implementación de sistemas operativos, como la distribución de software, la actualización de controladores, la edición de estados de usuario, etc."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
caps.latest.revision: 6
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: ec146270ef39d48673ae6f3ca405b3f0bd7e8afa


---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>Crear una secuencia de tareas para implementaciones que no son de sistema operativo con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Las secuencias de tareas de System Center Configuration Manager se usan para automatizar distintas tareas del entorno. Estas tareas están diseñadas principalmente y probadas para implementar sistemas operativos.  Configuration Manager tiene muchas otras características que deben ser la tecnología principal para escenarios como la [instalación de aplicaciones](../../apps/understand/introduction-to-application-management.md), la [instalación de actualizaciones de software](../../sum/understand/software-updates-introduction.md), la [configuración](../../compliance/understand/ensure-device-compliance.md)o la automatización personalizada. Existen otras tecnologías de automatización de Microsoft System Center, como [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) y [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) que también debe tener en cuenta.  

 La eficacia de las secuencias de tareas radica en su flexibilidad y en cómo puede usarlas para configurar el cliente, distribuir software, actualizar los controladores, editar los estados de usuario y realizar otras tareas independientes de la implementación de sistema operativo. Puede crear una secuencia de tareas personalizada para agregar cualquier número de tareas. Aunque se admite el uso básico de secuencias de tareas personalizadas para una implementación que no es de sistema operativo, no hay ninguna manera de probar todas las configuraciones posibles y la posibilidad de tener problemas aumenta a medida que se desarrollan secuencias de tareas más complejas.  

 Las siguientes etapas pueden usarse en una secuencia de tareas personalizada de implementación que no es de sistema operativo:  

-   [Comprobar preparación](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [Conectar a carpeta de red](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [Descargar contenido de paquete](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [Instalar aplicación](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [Instalar paquete](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [Instalar actualizaciones de software](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [Reiniciar equipo](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)  

-   [Ejecutar línea de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [Ejecutar script de PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [Establecer variables dinámicas](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [Establecer variable de secuencia de tareas](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Pasos siguientes
[Implementar la secuencia de tareas](manage-task-sequences-to-automate-tasks.md#a-namebkmkdeploytsa-deploy-a-task-sequence)



<!--HONumber=Dec16_HO3-->


