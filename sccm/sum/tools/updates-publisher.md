---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Usar System Center Updates Publisher para administrar actualizaciones personalizadas
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 25a1003fe6f2c61f089e1e2223d2b6f9fbd9b73f
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70888610"
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
> La versión anterior, [System Center Updates Publisher 2011](https://go.microsoft.com/fwlink/?LinkId=848111), sigue teniendo soporte técnico. Esta versión actualizada conserva la misma funcionalidad, pero admite sistemas operativos adicionales, ofrece nuevas características que simplifican algunas tareas y tiene una interfaz de usuario actualizada.

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

## <a name="whats-new-in-the-system-center-updates-publisher-preview"></a>Novedades de la vista previa de System Center Updates Publisher

>[!NOTE] 
>La información de esta sección solo se aplica a la versión preliminar de System Center updates Publisher. Para instalar la versión preliminar, descárguela desde el [centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=58390).

Hay un nuevo modo de creación en la versión preliminar de System Center Updates Publisher para ayudarle a crear las actualizaciones. Al habilitar el modo de creación, se agrega un **área de trabajo categorías** a la pantalla Inicio. También se agrega un nuevo botón **Detectoid** al **área de trabajo actualizaciones** cuando está habilitado el modo de creación. 

### <a name="to-enable-authoring-mode-in-the-preview"></a>Para habilitar el modo de creación en la vista previa

1. En la esquina superior izquierda de la consola, haga clic en la pestaña **propiedades** del **publicador de actualizaciones** y, a continuación, elija **Opciones**.
1. Vaya a las opciones de **creación** .
1. Active la casilla **Habilitar el modo de creación**.

![Habilitar el modo de creación para updates Publisher](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>Acerca del área de trabajo categorías

El área de trabajo categorías permite a los autores de actualizaciones organizar las actualizaciones que pertenecen a la vez. Por ejemplo, si es un OEM, puede que desee organizar las actualizaciones basadas en modelos o líneas de productos. Puede definir varias categorías y categorías secundarias, pero no categorías secundarias generales, ya que está limitado a dos niveles.

![Captura de pantalla del área de trabajo categorías](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>Asignación de una actualización a una categoría

Una vez que haya creado la actualización, puede asignarla a una categoría; para ello, seleccione la actualización y haga clic en el botón **clasificar** . También puede hacer clic con el botón secundario en la actualización y seleccionar **clasificar**.

![Captura de pantalla de la categorización de una actualización](media/scup-categorize-update.png)


### <a name="about-detectoids"></a>Acerca de detectoids

Una vez habilitado el modo de creación, puede crear detectoids para las actualizaciones. Detectoids son útiles cuando se tienen varias actualizaciones que usan la misma regla (o un conjunto de reglas) para determinar la aplicabilidad. En esos casos, crearía un detectoid y lo asignaría como requisito previo para una actualización. Puede asignar varios detectoids a una actualización creada.


### <a name="create-a-detectoid"></a>Creación de un detectoid

1. Abra **Updates Workspace** (Área de trabajo Actualizaciones).
1. En la cinta de opciones, haga clic en el botón **Detectoid** .
1. Siga las indicaciones del Asistente para crear el detectoid.



![Actualización de los requisitos previos mediante detectoid](media/scup-detectoid-as-prerequisite.png)


## <a name="next-steps"></a>Pasos siguientes
Para empezar, primero [instale](/sccm/sum/tools/install-updates-publisher) y luego [configure opciones](/sccm/sum/tools/updates-publisher-options) de Updates Publisher.
