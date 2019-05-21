---
title: Creación de elementos de configuración secundarios
titleSuffix: Configuration Manager
description: Cree elementos de configuración secundarios en System Center Configuration Manager.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0b88ee7eaac8df8ffce93937f3a3f2616b9e085b
ms.sourcegitcommit: 417e3834a42b415a8e129327dd3c15cc0c7ec5a2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2019
ms.locfileid: "65443160"
---
# <a name="how-to-create-child-configuration-items-in-system-center-configuration-manager"></a>Cómo crear elementos de configuración secundarios en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los elementos de configuración secundarios de System Center Configuration Manager son copias de los elementos de configuración que mantienen una relación con el elemento de configuración original; por tanto, heredan la configuración original del elemento de configuración primario.  

Al ver las propiedades de un elemento de configuración secundario en la consola de Configuration Manager, no puede editar la configuración y los objetos heredados con sus criterios de validación. No obstante, puede agregar y después editar los criterios de validación adicionales para el elemento de configuración secundario, y también puede agregar nuevos objetos y configuraciones en el elemento de configuración secundario.
Un ejemplo para crear y editar un elemento de configuración secundario es ajustar el elemento de configuración original para adaptarse a sus requisitos empresariales.  

> [!NOTE]  
>  Solo puede crear elementos de configuración secundarios a partir de elementos de configuración del tipo **Servidores y equipos de escritorio de Windows (personalizados)**.  

## <a name="to-create-a-child-configuration-item"></a>Cómo crear elementos de configuración secundarios  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Elementos de configuración**.  

3.  En la lista **Elementos de configuración** , seleccione el elemento de configuración para el que quiere crear un elemento de configuración secundario y después, en la pestaña **Inicio** , en el grupo **Elemento de configuración** , haga clic en **Crear elemento de configuración secundario**.  

4.  En la página **General** del **Asistente para crear elemento de configuración secundario**, puede elegir una revisión concreta del elemento de configuración primario que se usará para crear el elemento secundario. El resto de pasos de este asistente son idénticos a los que seguiría para crear un elemento de configuración estándar. Para obtener más información, consulte [How to create custom configuration items for Windows desktop and server computers](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md) (Cómo crear elementos de configuración personalizados para equipos de escritorio y servidores).  

5.  Complete el asistente. El nuevo elemento de configuración secundario se muestra en la lista **Elementos de configuración** .  
