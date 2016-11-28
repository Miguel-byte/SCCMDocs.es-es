---
title: "Clasificar automáticamente dispositivos en colecciones | System Center Configuration Manager"
description: "Clasifique los dispositivos en colecciones automáticamente con System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6e1e8c1da1209be03d4a1377dcc0c9ce9478a216

---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>Clasificar automáticamente dispositivos en colecciones con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede crear categorías de dispositivos, que se pueden usar para colocar automáticamente los dispositivos en colecciones de dispositivos cuando se usa Configuration Manager con Microsoft Intune. Después, cuando los usuarios inscriben un dispositivo en Intune, tienen que elegir una categoría de dispositivos. Además, puede cambiar la categoría de un dispositivo desde la consola de Configuration Manager.

> [!IMPORTANT]  
    >  Esta capacidad funciona con la versión de **junio de 2016** de Microsoft Intune. Asegúrese de haber actualizado a esta versión antes de probar estos procedimientos.

## <a name="create-device-categories"></a>Crear categorías de dispositivos

1.  En el área de trabajo **Activos y compatibilidad** de la consola de Configuration Manager, expanda **Información general** y haga clic en **Colecciones de dispositivos**.
2.  En el grupo **Colecciones de dispositivos** de la pestaña **Inicio**, haga clic en **Administrar categorías de dispositivos**.
3.  En el cuadro de diálogo **Administrar categorías de dispositivos**, puede crear, editar o quitar categorías.

## <a name="associate-a-collection-with-a-device-category"></a>Asociar una colección a una categoría de dispositivos

Cuando asocia una colección a una categoría de dispositivos, todos los dispositivos de la categoría que especifique se agregan a esa colección.

> [!IMPORTANT]  
    >  No se puede agregar una regla de categoría de dispositivos a una colección integrada como **Todos los sistemas**.

1.  En la pestaña **Reglas de pertenencia** del cuadro de diálogo **Propiedades** de una colección de dispositivos, haga clic en **Agregar regla** > **Regla de categoría de dispositivos**.
2.  En el cuadro de diálogo **Seleccionar categorías de dispositivos**, seleccione una o más categorías de dispositivos que se vayan a aplicar a todos los dispositivos de la colección.
3.  Cierre el cuadro de diálogo **Seleccionar categorías de dispositivos** y el cuadro de diálogo de propiedades de la colección.


## <a name="change-the-category-of-a-device"></a>Cambiar la categoría de un dispositivo

1.  En el área de trabajo **Activos y compatibilidad** de la consola de Configuration Manager, expanda **Información general** y haga clic en **Dispositivos**.
2.  Seleccione un dispositivo de la lista **Dispositivos** y, luego, en la pestaña **Inicio**, en el grupo **Dispositivo**, haga clic en **Cambiar categoría**.
3.  En el cuadro de diálogo **Editar categoría de dispositivos**, elija la categoría que se va a aplicar a este dispositivo y haga clic en **Aceptar**.

## <a name="view-which-category-a-device-belongs-to"></a>Ver a qué categoría pertenece un dispositivo

1.  En el área de trabajo **Activos y compatibilidad** de la consola de Configuration Manager, expanda **Información general** y haga clic en **Dispositivos**.
2.  En la lista **Dispositivos**, la categoría se muestra en la columna **Categoría de dispositivos**.
> [!TIP]  
    >  Si la columna **Categoría de dispositivos** no aparece, haga clic con el botón derecho en el encabezado de una de las columnas de la lista **Dispositivos** (como **Nombre**) y seleccione **Categoría de dispositivos**.

Si asigna un dispositivo a una categoría y posteriormente elimina la categoría, el informe **Lista de dispositivos inscritos en Microsoft Intune por usuario** mostrará un GUID en la columna **Categoría de dispositivos** en lugar de un nombre de categoría.



<!--HONumber=Nov16_HO1-->


