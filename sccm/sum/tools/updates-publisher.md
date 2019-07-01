---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Usar System Center Updates Publisher para administrar actualizaciones personalizadas
ms.date: 6/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 26ad3be032a3dd8ea21d7eeb6a4755c32d546f38
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2019
ms.locfileid: "67158634"
---
# <a name="system-center-updates-publisher"></a>Editor de actualizaciones de System Center

*Se aplica a: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) es una herramienta independiente que permite a proveedores de software independientes o desarrolladores de aplicaciones de línea de negocio administrar actualizaciones personalizadas. Esta administración de actualizaciones personalizadas incluye actualizaciones que tienen dependencias, como controladores y agrupaciones de actualizaciones.

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


**Updates Workspace** (Área de trabajo Actualizaciones): use este área de trabajo para [crear](/sccm/sum/tools/create-updates-with-updates-publisher) y [administrar](/sccm/sum/tools/manage-updates-with-updates-publisher) actualizaciones de software y agrupaciones de actualizaciones. Esta área de trabajo incluye asignar actualizaciones y agrupaciones a una publicación, publicarlas y exportarlas a otro repositorio de Updates Publisher.

**Publications Workspace** (Área de trabajo Publicaciones): aquí se [administran las publicaciones](/sccm/sum/tools/updates-publisher-publications). Una publicación es un grupo de actualizaciones que se crea para simplificar la exportación y publicación de las actualizaciones.

La administración de publicaciones incluye publicar actualizaciones en un servidor para que sus clientes pueden encontrarlas e instalarlas, exportar actualizaciones y agrupaciones para su uso con otras instalaciones de Updates Publisher o modificar el contenido o los detalles de una publicación.

**Rules Workspace** (Área de trabajo Reglas): aquí puede [administrar reglas de aplicabilidad](/sccm/sum/tools/updates-publisher-applicability-rules) que puede guardar y luego usar con actualizaciones que implemente. Hay dos tipos de informes:

-   Reglas instalables: estas reglas ayudan a determinar si un cliente debe instalar una actualización.
-   Reglas instaladas: estas reglas comprueban si una actualización está ya instalada.

**Catalogs Workspace** (Área de trabajo Catálogos): use este espacio de trabajo para agregar y [administrar catálogos de actualizaciones de software](/sccm/sum/tools/updates-publisher-catalogs). Esta área de trabajo incluye la importación de actualizaciones de software desde esos catálogos al repositorio de Updates Publisher.

## <a name="whats-new-in-the-system-center-updates-publisher-preview"></a>Novedades de la versión preliminar de System Center Updates Publisher

>[!NOTE] 
>La información de esta sección se aplica solo a la versión preliminar de System Center Updates publisher. Para instalar la versión preliminar, descárguelo desde el [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=58390).

Hay un nuevo modo de edición en la versión preliminar de System Center Updates Publisher que le ayudarán a crear sus actualizaciones. Cuando se habilita el modo de creación, un **área de trabajo de las categorías** se agrega a la pantalla Inicio. Un nuevo **detección** botón también se agrega a la **área de trabajo actualizaciones** cuando está habilitado el modo de creación. 

### <a name="to-enable-authoring-mode-in-the-preview"></a>Para habilitar el modo de creación de la versión preliminar

1. En la esquina superior izquierda de la consola, haga clic en el **Updates Publisher** **propiedades** pestaña y, a continuación, elija **opciones**.
1. Vaya a la **Authoring** opciones.
1. Active la casilla de **habilitar modo de creación**.

![Habilitar modo de creación de Updates Publisher](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>El área de trabajo de categorías

El área de trabajo de categorías permite a los autores de actualización organizar las actualizaciones que forman un conjunto. Por ejemplo, si es un fabricante OEM, es posible que desea organizar las actualizaciones en función de los modelos o las líneas de productos. Puede definir varias categorías y categorías secundarias pero categorías no grand secundario que están limitadas a dos niveles.

![Captura de pantalla del área de trabajo de categorías](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>Asignar una actualización a una categoría

Una vez que haya creado la actualización, puede asignarla a una categoría mediante la selección de la actualización, a continuación, haga clic en el **clasificar** botón. También puede haga clic en la actualización y seleccione **clasificar**.

![Captura de pantalla de categorización de una actualización](media/scup-categorize-update.png)


### <a name="about-detectoids"></a>Acerca de los detectoids

Una vez habilitado el modo de creación, puede crear detectoids para las actualizaciones. Los Detectoids son útiles cuando tiene varias actualizaciones que utilizan la misma regla (o un conjunto de reglas) para determinar la aplicabilidad. En esos casos, podría crear un identificador y asígnela como requisito previo para una actualización. Puede asignar varios detectoids a una actualización creada.


### <a name="create-a-detectoid"></a>Crear un identificador

1. Abra **Updates Workspace** (Área de trabajo Actualizaciones).
1. En la cinta de opciones, haga clic en el **detección** botón.
1. Siga las indicaciones del Asistente para crear su identificador.



![Actualizar los requisitos previos mediante una detección](media/scup-detectoid-as-prerequisite.png)


## <a name="next-steps"></a>Pasos siguientes
Para empezar, primero [instale](/sccm/sum/tools/install-updates-publisher) y luego [configure opciones](/sccm/sum/tools/updates-publisher-options) de Updates Publisher.
