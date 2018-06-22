---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Usar System Center Updates Publisher para administrar actualizaciones personalizadas
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 3a9c7758e394118041700192a393aff98f0d9087
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347338"
---
# <a name="system-center-updates-publisher"></a>Editor de actualizaciones de System Center

*Se aplica a: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) es una herramienta independiente que permite a proveedores de software independientes o desarrolladores de aplicaciones de línea de negocio administrar actualizaciones personalizadas. Esto incluye actualizaciones que tienen dependencias, como controladores y agrupaciones de actualizaciones.

Con Updates Publisher, puede:

-   Importar actualizaciones de catálogos externos (catálogos de actualizaciones que no sean de Microsoft).
-   Modificar definiciones de actualización, incluidos metadatos de implementación y aplicabilidad.
-   Exportar actualizaciones a catálogos externos.
-   Publicar actualizaciones en un servidor de actualización.

Después de publicar actualizaciones en un servidor de actualización, puede usar System Center Configuration Manager para detectar esas actualizaciones e implementarlas en los dispositivos administrados.

> [!TIP]  
> La versión anterior, [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/?LinkId=848111), sigue teniendo soporte técnico. Esta versión actualizada conserva la misma funcionalidad, pero admite sistemas operativos adicionales, ofrece nuevas características que simplifican algunas tareas y tiene una interfaz de usuario actualizada.

## <a name="workspaces"></a>Áreas de trabajo
Al abrir Updates Publisher, se abre de manera predeterminada en el nodo Introducción del *área de trabajo Actualizaciones*.

![Updates Publisher](media/console1.png)   


Updates Publisher tiene cuatro áreas de trabajo que ayudan a organizarlo.


**Updates Workspace** (Área de trabajo Actualizaciones): use este área de trabajo para [crear](/sccm/sum/tools/create-updates-with-updates-publisher) y [administrar](/sccm/sum/tools/manage-updates-with-updates-publisher) actualizaciones de software y agrupaciones de actualizaciones. Esto incluye asignar actualizaciones y agrupaciones a una publicación, publicarlas y exportarlas a otro repositorio de Updates Publisher.

**Publications Workspace** (Área de trabajo Publicaciones): aquí se [administran las publicaciones](/sccm/sum/tools/updates-publisher-publications). Una publicación es un grupo de actualizaciones que se crea para simplificar la exportación y publicación de las actualizaciones.

La administración de publicaciones incluye publicar actualizaciones en un servidor para que sus clientes pueden encontrarlas e instalarlas, exportar actualizaciones y agrupaciones para su uso con otras instalaciones de Updates Publisher o modificar el contenido o los detalles de una publicación.



**Rules Workspace** (Área de trabajo Reglas): aquí puede [administrar reglas de aplicabilidad](/sccm/sum/tools/updates-publisher-applicability-rules) que puede guardar y luego usar con actualizaciones que implemente. Hay dos tipos de informes:

-   Reglas instalables: estas reglas ayudan a determinar si un cliente debe instalar una actualización.
-   Reglas instaladas: estas reglas comprueban si una actualización está ya instalada.

**Catalogs Workspace** (Área de trabajo Catálogos): use este espacio de trabajo para agregar y [administrar catálogos de actualizaciones de software](/sccm/sum/tools/updates-publisher-catalogs). Esto incluye la importación de actualizaciones de software desde esos catálogos al repositorio de Updates Publisher.
## <a name="first-steps"></a>Primeros pasos
Para empezar, primero [instale](/sccm/sum/tools/install-updates-publisher) y luego [configure opciones](/sccm/sum/tools/updates-publisher-options) de Updates Publisher.
