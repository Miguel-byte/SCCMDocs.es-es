---
title: Crear una secuencia de tareas para implementaciones que no son de sistema operativo
titleSuffix: Configuration Manager
description: Cree secuencias de tareas que no estén relacionadas con la implementación de sistemas operativos, como la distribución de software, la actualización de controladores, la edición de estados de usuario, etc.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c8ef75ea9b0948a932c1b146d0f4fe7051017759
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140320"
---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>Crear una secuencia de tareas para implementaciones que no son de sistema operativo con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las secuencias de tareas de System Center Configuration Manager se usan para automatizar distintas tareas del entorno. Estas tareas están diseñadas principalmente y probadas para implementar sistemas operativos.  Configuration Manager tiene muchas otras características que deben ser la tecnología principal para escenarios como la [instalación de aplicaciones](../../apps/understand/introduction-to-application-management.md), la [instalación de actualizaciones de software](../../sum/understand/software-updates-introduction.md), la [configuración](../../compliance/understand/ensure-device-compliance.md)o la automatización personalizada. Existen otras tecnologías de automatización de Microsoft System Center, como [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) y [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) que también debe tener en cuenta.  

La eficacia de las secuencias de tareas radica en su flexibilidad y en cómo puede usarlas para configurar el cliente, distribuir software, actualizar los controladores, editar los estados de usuario y realizar otras tareas independientes de la implementación de sistema operativo. Puede crear una secuencia de tareas personalizada para agregar cualquier número de tareas. En Configuration Manager se admite el uso de secuencias de tareas personalizadas para las implementaciones que no son de sistema operativo. Pero si una secuencia de tareas produce resultados incoherentes o no deseados, debe buscar formas de simplificar la operación. Para ello, puede seguir pasos más sencillos, dividir las acciones en varias secuencias de tareas o usar un método por fases para crear y probar la secuencia de tareas.

 Los siguientes pasos pueden usarse en una secuencia de tareas personalizada de implementación que no es de sistema operativo:  

-   [Comprobar preparación](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [Conectar a carpeta de red](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [Descargar contenido de paquete](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [Instalar aplicación](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [Instalar paquete](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [Instalar actualizaciones de software](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [Reiniciar equipo](../understand/task-sequence-steps.md#BKMK_RestartComputer)   

-   [Ejecutar línea de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [Ejecutar script de PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [Establecer variables dinámicas](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [Establecer variable de secuencia de tareas](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Pasos siguientes 
[Implementar la secuencia de tareas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
