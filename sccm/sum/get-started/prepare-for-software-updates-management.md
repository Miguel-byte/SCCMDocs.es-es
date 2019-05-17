---
title: Preparar la administración de actualizaciones de software
titleSuffix: Configuration Manager
description: Para preparar la administración de actualizaciones, lleve a cabo estas tareas para mostrar los datos de la evaluación de compatibilidad en la consola de System Center Configuration Manager.
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
manager: dougeby
author: mestew
ms.author: mstewart
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8381a9a5195982a2defa347934c28286e9082ce7
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65493968"
---
# <a name="prepare-for-software-updates-management"></a>Preparar la administración de actualizaciones de software

*Se aplica a: System Center Configuration Manager (Rama actual)*

Antes de que se muestren los datos de la evaluación de compatibilidad de la actualización de software en la consola de System Center Configuration Manager, y antes de poder implementar actualizaciones de software en equipos cliente, debe llevar a cabo los pasos descritos en las siguientes secciones.

## <a name="step-1-install-a-software-update-point"></a>Paso 1: Instalar un punto de actualización de software  
El punto de actualización de software es necesario en el sitio de administración central (o sitio principal independiente) y en los sitios principales para habilitar la evaluación del compatibilidad de las actualizaciones de software e implementar las actualizaciones de software en los clientes. El punto de actualización de software es opcional en los sitios secundarios. Para obtener información detallada, consulte [Install a software update point](install-a-software-update-point.md) (Instalar un punto de actualización de software).  

## <a name="step-2-synchronize-software-updates"></a>Paso 2: Sincronizar actualizaciones de software
La sincronización de las actualizaciones de software es el proceso de recuperación de los metadatos de actualización de software que cumplen los criterios configurados. Las actualizaciones de software no se muestran en la consola de Configuration Manager hasta que se sincronizan. Para obtener información detallada, consulte [Synchronize software updates](synchronize-software-updates.md) (Sincronizar actualizaciones de software).   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>Paso 3: Configurar las clasificaciones y los productos que se van a sincronizar
Realice esta configuración en el sitio de administración central o el sitio primario independiente. Después de sincronizar las actualizaciones de software por primera vez, Configuration Manager recupera una lista actualizada de productos y clasificaciones. Ahora puede seleccionar entre las opciones nuevas de las propiedades del componente de punto de actualización de software. Después de configurar las clasificaciones y productos nuevos, repita el paso 2 para iniciar la sincronización de actualizaciones de software para recuperar los metadatos de las actualizaciones de software para los criterios nuevos. Para obtener información detallada, consulte [Configurar las clasificaciones y los productos que va a sincronizar](configure-classifications-and-products.md).

## <a name="step-4-manage-settings-for-software-updates"></a>Paso 4: Administrar la configuración de las actualizaciones de software
Después de sincronizar las actualizaciones de software, compruebe la configuración del cliente de Configuration Manager, la configuración de las directivas de grupo y la configuración de las actualizaciones de software antes de implementarlas. Para obtener información detallada, consulte [Manage settings for software updates](manage-settings-for-software-updates.md) (Administrar la configuración de las actualizaciones de software).
