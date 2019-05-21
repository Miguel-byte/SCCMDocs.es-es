---
title: 'Adición de actualizaciones a un grupo de actualizaciones '
titleSuffix: Configuration Manager
description: Agregue actualizaciones de software de forma manual o automática a un grupo de actualizaciones de software del entorno.
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a0767664-fd60-46a8-9da5-86cc431ce53c
manager: dougeby
author: mestew
ms.author: mstewart
ms.collection: M365-identity-device-management
ms.openlocfilehash: b207d0c210aa25489d67a5a551bf795e86c1582b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500244"
---
# <a name="add-software-updates-to-an-update-group"></a>Agregar actualizaciones de software a un grupo de actualizaciones  

*Se aplica a: System Center Configuration Manager (Rama actual)*

 Los grupos de actualizaciones de software suponen un método eficaz para organizar las actualizaciones de software del entorno. Puede agregar manualmente actualizaciones de software a un grupo de actualizaciones de software o puede hacerlo automáticamente mediante una regla de implementación automática (ADR). También puede implementar un grupo de actualizaciones de software manualmente o implementarlo de forma automática mediante una ADR. Después de implementar un grupo de actualizaciones de software, puede agregar nuevas actualizaciones de software al grupo para que Configuration Manager las implemente automáticamente. Utilice los procedimientos siguientes para agregar actualizaciones de software a un grupo de actualizaciones de software nuevo o existente.  

#### <a name="to-add-software-updates-to-a-new-software-update-group"></a>Para agregar actualizaciones de software a un grupo de actualizaciones de software nuevo  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo de la biblioteca de software, expanda **Actualizaciones de software**y haga clic en **Todas las actualizaciones de software**.  

3.  Seleccione las actualizaciones de software que se van a agregar al grupo de actualizaciones de software nuevo.  

4.  En la pestaña **Inicio** , en el grupo **Actualizar** , haga clic en **Crear grupo de actualizaciones de software**.  

5.  Especifique el nombre para el grupo de actualizaciones de software y, opcionalmente, incluya una descripción. Utilice un nombre y una descripción que proporcione información suficiente para determinar qué tipo de actualizaciones de software incluye el grupo de actualizaciones de software. Para proceder, haga clic en **Crear**.  

6.  Haga clic en **Grupos de actualizaciones de software** para mostrar el grupo de actualizaciones de software nuevo.  

7.  Seleccione el grupo de actualizaciones de software y, en la pestaña **Inicio** , en el grupo **Actualizar** , haga clic en **Mostrar miembros** para mostrar una lista de las actualizaciones de software incluidas en el grupo.  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>Para agregar actualizaciones de software a un grupo de actualizaciones de software existente  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo de la biblioteca de software, expanda **Actualizaciones de software**y haga clic en **Todas las actualizaciones de software**.  

3.  Seleccione las actualizaciones de software que se van a agregar al nuevo grupo de actualizaciones de software nuevo.  

    > [!NOTE]  
    >  En el nodo **Todas las actualizaciones de software**, Configuration Manager muestra todas las actualizaciones, salvo las de la clasificación **Actualizaciones** y las de la clasificación de producto de **cliente de Office 365**.  

4.  En la pestaña **Inicio** , en el grupo **Actualizar** , haga clic en **Editar pertenencia**.  

5.  Seleccione el grupo de actualizaciones de software en el que va a agregar las actualizaciones de software.  

6.  Haga clic en el nodo **Grupos de actualizaciones de software** para mostrar el grupo de actualizaciones de software.  

7.  Seleccione el grupo de actualizaciones de software y, en la pestaña **Inicio** , en el grupo **Actualizar** , haga clic en **Mostrar miembros** para mostrar una lista de las actualizaciones de software incluidas en el grupo de actualizaciones de software.  
