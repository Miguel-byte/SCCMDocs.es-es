---
title: Creación de líneas base de configuración
titleSuffix: Configuration Manager
description: Cree líneas base de configuración en System Center Configuration Manager que pueda implementar en una recopilación.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 665f5720486164cc4c728d579f1a700c4fb16245
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384678"
---
# <a name="create-configuration-baselines-in-system-center-configuration-manager"></a>Crear líneas base de configuración en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


Las líneas base de configuración en System Center Configuration Manager contienen elementos de configuración predefinidos y, de manera opcional, otras líneas base de configuración. Después de crear una línea base de configuración, puede implementarla en una recopilación para que los dispositivos de esa recopilación descarguen la línea base de configuración y evalúen su cumplimiento con ella.  

 Las líneas base de configuración de Configuration Manager pueden contener revisiones específicas de elementos de configuración o pueden estar configuradas para usar siempre la última versión de un elemento de configuración. Para obtener más información sobre las revisiones de elementos de configuración, consulte [Management tasks for configuration data](../../compliance/deploy-use/management-tasks-for-configuration-data.md) (Tareas de administración para datos de configuración).  

 Puede usar dos métodos para crear líneas base de configuración:  

-   Importar datos de configuración de un archivo Para iniciar el **Asistente para importar datos de configuración**, en el nodo **Elementos de configuración** o **Líneas de base de configuración** en el área de trabajo **Activos y compatibilidad** , haga clic en **Importar datos de configuración**.  

-   Use el cuadro de diálogo **Crear línea de base de configuración** para crear una nueva línea base de configuración.  

Para crear una línea base de configuración mediante el cuadro de diálogo **Crear línea base de configuración**, use el procedimiento siguiente:  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Líneas base de configuración**.  

2.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear línea de base de configuración**.  

3.  En el cuadro de diálogo **Crear línea de base de configuración** , escriba un nombre único y una descripción para la línea de base de configuración. Puede usar un máximo de 255 caracteres para el nombre y 512 caracteres para la descripción.  

4.  En la lista **Datos de configuración** se muestran todos los elementos de configuración o líneas base de configuración que se incluyen en esta línea base de configuración. Haga clic en **Agregar** para agregar un nuevo elemento de configuración o línea base de configuración a la lista. Puede elegir entre los elementos siguientes:  

    -   **Elementos de configuración**  

    -   **Actualizaciones de software**  

    -   **Líneas de base de configuración**  
      > [!IMPORTANT]
      > Debe limitar cada línea base de configuración a un máximo de 1000 actualizaciones de software.
5.  Use la lista **Cambiar propósito** para especificar el comportamiento de un elemento de configuración que ha seleccionado en la lista **Datos de configuración**. Puede elegir entre los elementos siguientes:  

    -   **Requerido**: la línea base de configuración se evalúa como no conforme si el elemento de configuración no se detecta en un dispositivo cliente. Si se detecta, se evalúa para el cumplimiento.  

    -   **Opcional**: el elemento de configuración solo se evalúa para el cumplimiento si la aplicación a la que hace referencia se encuentra en los equipos cliente. Si no se encuentra la aplicación, la línea base de configuración no se marca como no conforme (solo es aplicable a los elementos de configuración de la aplicación).  

    -   **Prohibido**: la línea base de configuración se evalúa como no conforme si el elemento de configuración se detecta en los equipos cliente (solo es aplicable a los elementos de configuración de aplicación).  

    > [!NOTE]
    >  La lista **Cambio propósito** solo está disponible si se ha hecho clic en la opción **Este elemento de configuración contiene configuraciones de aplicación** en la página **General** del **Asistente para crear elemento de configuración**.  

6.  Use la lista **Cambiar revisión** para seleccionar una revisión determinada o la más reciente del elemento de configuración para evaluar el cumplimiento de dispositivos cliente o seleccione **Usar siempre el más reciente** para emplear siempre la revisión más reciente. Para obtener más información sobre las revisiones de elementos de configuración, consulte [Management tasks for configuration data](../../compliance/deploy-use/management-tasks-for-configuration-data.md) (Tareas de administración para datos de configuración).  

7.  Para eliminar un elemento de configuración de la línea base de configuración, seleccione un elemento de configuración y luego haga clic en **Quitar**.  

8. A partir de la versión 1806, seleccione si quiere **Aplicar siempre esta línea de base para los clientes administrados conjuntamente**. Cuando se activa, esta línea de base se aplicará incluso en los clientes que se administran mediante Intune.  Esta excepción podría utilizarse para definir la configuración que necesita su organización, pero aún no está disponible en Intune. 

9. Opcionalmente, haga clic en **Categorías** para asignar categorías a la línea de base de búsqueda y filtrado. 

10. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Crear línea de base de configuración** y crear la línea base de configuración.  

>[!NOTE]
> La modificación de una línea de base existente, como establecer **Aplicar siempre esta línea de base para los clientes administrados conjuntamente**, aumentará la versión de contenido de línea de base. Los clientes tendrán que evaluar la nueva versión para actualizar los informes de línea de base. 