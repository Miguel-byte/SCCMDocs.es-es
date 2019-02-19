---
title: Creación de entornos virtuales de App-V
titleSuffix: Configuration Manager
description: Cree entornos virtuales con Microsoft Application Virtualization para que las aplicaciones puedan compartir datos entre sí.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2becf31d807f0854bf6ab9d4eb58adf84d8ab7e6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135769"
---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>Crear entornos virtuales de App-V en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En un entorno virtual de Microsoft Application Virtualization (App-V) en System Center Configuration Manager (Configuration Manager), las aplicaciones virtuales implementadas pueden compartir el mismo sistema de archivos y el Registro en equipos cliente de Windows. A diferencia de las aplicaciones virtuales estándar, estas aplicaciones pueden compartir datos entre sí. Los entornos virtuales se crean o modifican en equipos cliente cuando se instala la aplicación o cuando los clientes vuelven a evaluar sus aplicaciones instaladas. Puede ordenar las aplicaciones para que cuando varias aplicaciones intenten modificar un valor del Registro o del sistema de archivos, la aplicación con el orden más alto tenga prioridad.  

> [!IMPORTANT]  
>  No se base en entornos virtuales de App-V para proporcionar protección de seguridad (por ejemplo, contra malware).  

 Use el procedimiento siguiente para crear un entorno virtual de App-V en Configuration Manager.  

## <a name="create-an-app-v-virtual-environment"></a>Crear un entorno virtual de App-V  

1.  En la consola de Configuration Manager, pulse **Biblioteca de software** > **Administración de aplicaciones** > **Entornos virtuales de App-V**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, pulse **Crear entorno virtual**.  

4.  En el cuadro de diálogo **Crear entorno virtual**, especifique la siguiente información:  

    -   **Nombre**.  Especifique un nombre único para el entorno virtual (máximo 128 caracteres).  

    -   **Descripción**. (Opcional) Especifique una descripción para el entorno virtual.  

5.  Pulse **Agregar** para agregar un nuevo tipo de implementación para el entorno virtual. Debe agregar al menos un tipo de implementación.  

6.  En el cuadro de diálogo **Agregar aplicaciones**, especifique un **Nombre de grupo** (máximo 128 caracteres). Usará este nombre para hacer referencia al grupo de aplicaciones que agregue al entorno virtual.  

7.  Pulse **Agregar**, seleccione los tipos de implementación y las aplicaciones de App-V 5 que quiera agregar al grupo y, después, pulse **Aceptar**.  

8.  En el cuadro de diálogo **Agregar aplicaciones**, puede seleccionar **Aumentar orden** o **Disminuir orden** para establecer la aplicación que tendrá prioridad si varias aplicaciones intentan modificar la configuración del Registro o del sistema de archivos en el mismo entorno virtual.  

9. Pulse **Aceptar** para volver al cuadro de diálogo **Crear entorno virtual**.  

10. Cuando haya terminado de agregar grupos, pulse **Aceptar** para crear el entorno virtual. El nuevo entorno virtual se muestra en el nodo **Entornos virtuales de App-V** de la consola de Configuration Manager. Puede supervisar el estado de los entornos virtuales mediante el informe Estado del entorno virtual de App-V.  

    > [!NOTE]  
    >  El entorno virtual se agrega o modifica en equipos cliente cuando la aplicación se instala o cuando el cliente vuelve a evaluar las aplicaciones instaladas.  
