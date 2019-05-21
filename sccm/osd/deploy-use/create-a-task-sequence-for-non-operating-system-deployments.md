---
title: Crear una secuencia de tareas para implementaciones que no son de sistema operativo
titleSuffix: Configuration Manager
description: Creación de secuencias de tareas que no son para implementar un sistema operativo, como la distribución de software o la automatización de tareas
ms.date: 05/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17ba0f146a80928b1eaae6334e6418a5e08b1114
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083064"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>Crear una secuencia de tareas para implementaciones que no son de sistema operativo

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las secuencias de tareas de Configuration Manager se usan para automatizar diferentes clases de tareas del entorno. Estas tareas están diseñadas principalmente y probadas para implementar sistemas operativos. Configuration Manager tiene muchas otras características que deben ser la tecnología principal que use en los siguientes escenarios:

- [Instalación de la aplicación](/sccm/apps/understand/introduction-to-application-management)
- [Instalación de actualizaciones de software](/sccm/sum/understand/software-updates-introduction)
- [Establecimiento de la configuración](/sccm/compliance/understand/ensure-device-compliance)

Considere también otras tecnologías de automatización de Microsoft System Center, como [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) y [Service Management Automation](https://docs.microsoft.com/system-center/sma/).  

La eficacia de las secuencias de tareas radica en su flexibilidad y en cómo se usan. Se pueden usar para configurar clientes, distribuir software, actualizar controladores, editar estados de usuario y realizar otras tareas independientes de la implementación del sistema operativo. Puede crear una secuencia de tareas personalizada para agregar cualquier número de tareas. En Configuration Manager se admite el uso de secuencias de tareas personalizadas para implementaciones que no son de sistema operativo. Pero si una secuencia de tareas produce resultados incoherentes o no deseados, debe buscar formas de simplificar la operación:

- Usar pasos más sencillos
- Dividir las acciones entre varias secuencias de tareas
- Adoptar un enfoque por fases para crear y probar la secuencia de tareas

Los siguientes pasos pueden usarse en una secuencia de tareas personalizada de una implementación que no es de sistema operativo:  

- [Comprobar preparación](/sccm/osd/understand/task-sequence-steps#BKMK_CheckReadiness)  

- [Conectar a carpeta de red](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder)  

- [Descargar contenido de paquete](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent)  

- [Instalar aplicación](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication)  

- [Instalar paquete](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage)  

- [Instalar actualizaciones de software](/sccm/osd/understand/task-sequence-steps#BKMK_InstallSoftwareUpdates)  

- [Reiniciar equipo](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer)  

- [Ejecutar línea de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)  

- [Ejecutar script de PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript)  

- [Ejecutar secuencia de tareas](/sccm/osd/understand/task-sequence-steps#child-task-sequence)  

- [Establecer variables dinámicas](/sccm/osd/understand/task-sequence-steps#BKMK_SetDynamicVariables)  

- [Establecer variable de secuencia de tareas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)  
