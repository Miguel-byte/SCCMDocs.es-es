---
title: Consola de Configuration Manager
titleSuffix: Configuration Manager
description: Obtenga información sobre la navegación a través de la consola de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d783211396f3cdc9f14798ed7dc97e921e45554
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385916"
---
# <a name="using-the-system-center-configuration-manager-console"></a>Usar la consola de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los administradores usan la consola de System Center Configuration Manager para administrar el entorno de Configuration Manager. Este artículo trata los aspectos básicos de navegación de la consola. Las mejoras en la consola se muestran por versión al final de este artículo. 

## <a name="connect-the-console-to-a-site-server"></a>Conecte la consola a un servidor de sitio
La consola se conecta al servidor de sitio de administración central o a los servidores de sitio primarios. En cambio, no puede conectar una consola de Configuration Manager a un sitio secundario. Si es necesario, [instale la consola de Configuration Manager](../deploy/install/install-consoles.md). Durante la instalación, especificó el nombre de dominio completo (FQDN) del servidor de sitio al que se conecta la consola de Configuration Manager. Para conectarse a otro servidor de sitio, use las siguientes instrucciones: 

1. Haga clic en la flecha situada en la parte superior de la cinta y seleccione **Conectar a un nuevo sitio**.
    ![Conecte la consola a un nuevo sitio](media/connect-to-a-new-site.png)
2. Escriba el FQDN del servidor del sitio. Si se ha conectado anteriormente al servidor de sitio, seleccione el servidor en la lista desplegable.  
    ![Escribir el FQDN del servidor del sitio](media/site-server-fqdn.png)
3. Haga clic en **Conectar**. 

## <a name="navigate-the-console"></a>Ir a la consola
Algunas opciones en la consola pueden no estar visibles en función del rol de seguridad asignado. Para obtener más información sobre roles, vea [Conceptos básicos de la administración basada en roles](../../understand/fundamentals-of-role-based-administration.md). 

### <a name="workspaces"></a>Áreas de trabajo
La consola de Configuration Manager tiene cuatro **áreas de trabajo**: 
   - **Activos y compatibilidad**
   - **Biblioteca de software**
   - **Supervisión**
   - **Administración**

 ![Áreas de trabajo de Configuration Manager](media/configuration-manager-workspaces.png)

Cambie el orden de los botones del área de trabajo; para ello, haga clic en la flecha hacia abajo y seleccione **Opciones de Panel de navegación**. Seleccione un elemento que quiera **Subir** o **Bajar**. Haga clic en **Restablecer** para restaurar el orden de botones predeterminado. 

 ![Cambiar el orden de las áreas de trabajo de Configuration Manager](media/navigation-pane-options.png)

Puede minimizar un botón del área de trabajo seleccionando **Mostrar menos botones**. La última área de trabajo en la lista del áreas de trabajo se minimiza en primer lugar. Si hace clic en un botón minimizado y selecciona **Mostrar más botones**, se restaura el botón a su tamaño original.  

![Áreas de trabajo de Configuration Manager](media/workspace-buttons.png)


### <a name="nodes"></a>Nodos
Las áreas de trabajo son una colección de **nodos**. Un ejemplo de un nodo es el nodo **Grupos de actualizaciones de software**. Una vez que se encuentran en el nodo, puede hacer clic en la flecha para minimizar el panel de navegación. 

![Áreas de trabajo de Configuration Manager](media/software-update-groups-node.png)

Puede usar la **barra de navegación** para desplazarse por la consola cuando se minimiza el panel de navegación. 

![Configuration Manager minimizado en el panel de navegación](media/minimized-navigation-pane.png)

En la consola, los nodos a veces se organizan en carpetas. Si hace clic directamente en la carpeta, suele llevarle a un **índice de navegación** o a un **panel**.

![Índice de navegación de las actualizaciones de software de Configuration Manager](media/software-updates-navigation-index.png)

### <a name="ribbon"></a>Cinta de opciones 
La cinta está en la parte superior de la consola de Configuration Manager. La cinta puede tener más de una pestaña y se puede minimizar usando la flecha situada a la derecha. Los botones de la cinta de opciones cambian en función del nodo. La mayoría de los botones de la cinta también están disponibles en los menús que verá al hacer clic con el botón derecho. 
 
![Índice de navegación de las actualizaciones de software de Configuration Manager](media/ribbon.png)

### <a name="details-pane"></a>Panel de detalles
Puede obtener información adicional sobre los elementos revisando el panel de detalles. El panel de detalles puede tener una o más pestañas. Las pestañas variarán según el nodo. 
![Panel de detalles de Configuration Manager](media/details-pane.png)

### <a name="columns"></a>Columnas 
Puede agregar columnas, quitarlas, reordenarlas y cambiar su tamaño. Estas acciones le permiten mostrar los datos que prefiera. Las columnas disponibles variarán según el nodo. Haga clic con el botón derecho en un encabezado de columna existente y después haga clic en un elemento para agregarlo o quitarlo de la vista. Reordene las columnas arrastrando el encabezado de columna donde desee que esté ubicado. 
![Agregar columna en Configuration Manager](media/add-columns.png)

En la parte inferior del menú contextual de la columna puede ordenar o agrupar por una columna. Además, puede ordenar por una columna si hace clic en su encabezado. 

![Agrupar por columna en Configuration Manager](media/column-group-by.png)

## <a name="console-improvements-in-version-1806"></a>Mejoras en la consola en la versión 1806
En la versión 1806 de Configuration Manager, se agregan las siguientes mejoras de la consola:

- **Los usuarios primarios** están disponibles como una columna en el nodo dispositivo. <!--1357280-->
- **Los usuarios con sesión iniciada actualmente** están disponibles como una columna en el nodo del dispositivo.<!--1358202-->
- Se puede copiar información desde el panel **Detalles del activo** a las siguientes vistas de supervisión: <!--1357856-->
    - Estado de distribución de contenido
    - Estado de implementación 

    ![Detalles de activos de copia de Configuration Manager](media/1810-deployment-status.PNG)

 - Enviar comentarios desde la consola. Puede guardar una copia para enviarla más tarde si no tiene acceso a Internet. <!--1357542-->
   
    - **Enviar una sonrisa**: enviar comentarios sobre lo que le gustó.
    - **Enviar una desaprobación**: enviar comentarios sobre lo que no le gustó. 
    - **Enviar una sugerencia**: le lleva a UserVoice para compartir sus ideas. 
 
       ![Enviar comentarios de Configuration Manager](media/1810-send-a-smile.PNG)
![Formulario de comentarios de Configuration Manager](media/1810-feedback-form.PNG)

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Características de accesibilidad](/sccm/core/understand/accessibility-features.md)

