---
title: Consola de Configuration Manager
titleSuffix: Configuration Manager
description: Obtenga información sobre la navegación a través de la consola de Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 073f908057d459d847cbec6b380e7a4a8683db2b
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456165"
---
# <a name="using-the-configuration-manager-console"></a>Uso de la consola de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los administradores usan la consola de Configuration Manager para administrar el entorno de Configuration Manager. Este artículo trata los aspectos básicos de navegación de la consola.  



## <a name="connect-to-a-site-server"></a>Conexión a un servidor de sitio

La consola se conecta al servidor de sitio de administración central o a los servidores de sitio primarios. No se puede conectar una consola de Configuration Manager a un sitio secundario. Puede [instalar la consola de Configuration Manager](/sccm/core/servers/deploy/install/install-consoles). Durante la instalación, especificó el nombre de dominio completo (FQDN) del servidor de sitio al que se conecta la consola. 

Para conectarse a otro servidor de sitio, siga estos pasos: 

1. Haga clic en la flecha situada en la parte superior de la [cinta](#ribbon) y elija **Conectar a un nuevo sitio**.  
    ![Conecte la consola a un nuevo sitio](media/connect-to-a-new-site.png)  

2. Escriba el FQDN del servidor del sitio. Si se ha conectado anteriormente al servidor de sitio, seleccione el servidor en la lista desplegable.  
    ![Ventana de conexión de sitio, especifique el FQDN del servidor de sitio](media/site-server-fqdn.png)  

3. Seleccione **Conectar**.  


A partir de la versión 1810, puede especificar el nivel mínimo de autenticación para que los administradores accedan a sitios de Configuration Manager. Esta característica exige que los administradores inicien sesión en Windows con el nivel requerido. Para más información, vea [Plan for the SMS Provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth) (Planear el proveedor de SMS). <!--1357013-->  



## <a name="navigation"></a>Navegación

Algunas áreas de la consola pueden no estar visibles en función del rol de seguridad asignado. Para obtener más información sobre roles, vea [Conceptos básicos de la administración basada en roles](/sccm/core/understand/fundamentals-of-role-based-administration). 


### <a name="workspaces"></a>Áreas de trabajo

La consola de Configuration Manager tiene cuatro **áreas de trabajo**: 
   - **Activos y compatibilidad**  
   - **Biblioteca de software**  
   - **Supervisión**  
   - **Administración**  

![Áreas de trabajo de Configuration Manager con el menú contextual](media/configuration-manager-workspaces.png)  

Cambie el orden de los botones del área de trabajo; para ello, haga clic en la flecha hacia abajo y elija **Opciones de Panel de navegación**. Seleccione un elemento que quiera **Subir** o **Bajar**. Haga clic en **Restablecer** para restaurar el orden de botones predeterminado.  
 ![Ventana de Opciones de Panel de navegación para cambiar el orden de las áreas de trabajo](media/navigation-pane-options.png)  

Minimice un botón del área de trabajo seleccionando **Mostrar menos botones**. La última área de trabajo de la lista se minimiza primero. Seleccione un botón minimizado y elija **Mostrar más botones** para restaurar el botón a su tamaño original.   
![Áreas de trabajo minimizadas en la consola de Configuration Manager](media/workspace-buttons.png)  


### <a name="nodes"></a>Nodos

Las áreas de trabajo son una colección de **nodos**. Un ejemplo de un nodo es el nodo **Grupos de actualizaciones de software** en el área de trabajo **Biblioteca de software**. 

Una vez que se encuentran en el nodo, puede hacer clic en la flecha para minimizar el panel de navegación.  
![Nodo de ejemplo y flecha de minimizar resaltado](media/software-update-groups-node.png)  

Use la **barra de navegación** para desplazarse por la consola al minimizar el panel de navegación.  
![Configuration Manager minimizado en el panel de navegación](media/minimized-navigation-pane.png)  

En la consola, los nodos a veces se organizan en carpetas. Si hace clic directamente en la carpeta, suele llevarle a un **índice de navegación** o a un **panel**.  
![Índice de navegación de las actualizaciones de software de Configuration Manager](media/software-updates-navigation-index.png)  


### <a name="ribbon"></a>Cinta de opciones 

La cinta está en la parte superior de la consola de Configuration Manager. La cinta puede tener más de una pestaña y se puede minimizar usando la flecha situada a la derecha. Los botones de la cinta de opciones cambian en función del nodo. La mayoría de los botones de la cinta también están disponibles en los menús que verá en los menús contextuales.  
![Cinta de opciones de ejemplo, flecha para resaltar varias pestañas y minimizar](media/ribbon.png)   


### <a name="details-pane"></a>Panel de detalles

Puede obtener información adicional sobre los elementos revisando el panel de detalles. El panel de detalles puede tener una o más pestañas. Las pestañas varían según el nodo. 
![Panel de detalles de ejemplo de Configuration Manager](media/details-pane.png)   


### <a name="columns"></a>Columnas 

Puede agregar columnas, quitarlas, reordenarlas y cambiar su tamaño. Estas acciones le permiten mostrar los datos que prefiera. Las columnas disponibles varían en función del nodo. Para agregar o quitar una columna de la vista, haga clic con el botón derecho en un encabezado de columna existente y seleccione un elemento. Reordene las columnas arrastrando el encabezado de columna donde desee que esté ubicado.  
![Columna para agregar en Configuration Manager](media/add-columns.png)  

En la parte inferior del menú contextual de la columna puede ordenar o agrupar por una columna. Además, también puede ordenar por columna seleccionando el encabezado.  
![Agrupar por columna en Configuration Manager](media/column-group-by.png)  



## <a name="command-line-options"></a>Opciones de línea de comandos

La consola de Configuration Manager tiene las opciones de línea de comandos siguientes:

|Opción|Descripción|  
|------------|-----------------|  
|`/sms:debugview=1`|Se incluye un elemento DebugView en todos los elementos ResultView que especifican una vista. DebugView muestra las propiedades sin procesar (nombres y valores).|  
|`/sms:NamespaceView=1`|Muestra la vista del espacio de nombres en la consola.|  
|`/sms:ResetSettings`|La consola pasa por alto los estados de vista y conexión seguidas por el usuario. No se restablece el tamaño de la ventana.|  
|`/sms:IgnoreExtensions`|Deshabilita las extensiones de Configuration Manager.|  
|`/sms:NoRestore`|La consola omite la anterior navegación por nodos persistente.|  



## <a name="tips"></a>Sugerencias

### <a name="send-feedback"></a>Enviar comentarios
<!--1357542-->

A partir de la versión 1806, los comentarios sobre el producto se envían desde la consola.  
   
- **Enviar una sonrisa**: enviar comentarios sobre lo que le gustó.
- **Enviar una desaprobación**: enviar comentarios sobre lo que no le gustó. 
- **Enviar una sugerencia**: le lleva a UserVoice para compartir sus ideas. 
 
Para obtener más información, vea [Comentarios sobre el producto](/sccm/core/understand/find-help#BKMK_1806Feedback).


### <a name="assets-and-compliance-workspace"></a>Área de trabajo Activos y compatibilidad

#### <a name="view-users-for-a-device"></a>Ver los usuarios de un dispositivo
A partir de la versión 1806, las siguientes columnas están disponibles en el nodo **Dispositivos**:
- **Usuarios primarios** <!--1357280-->  
- **Usuario que ha iniciado sesión actualmente** <!--1358202-->  

Para obtener más información sobre cómo mostrar una columna no predeterminada, vea [Columnas](#columns).


### <a name="monitoring-workspace"></a>Área de trabajo de supervisión

#### <a name="copy-details-in-monitoring-views"></a>Copiar detalles en las vistas de supervisión
<!--1357856-->A partir de la versión 1806, se puede copiar información desde el panel **Detalles del activo** a los siguientes nodos de supervisión: 
    - **Estado de distribución de contenido**  
    - **Estado de implementación**  

![Vista del estado de implementación, detalles del activo de copia](media/1810-deployment-status.PNG)



## <a name="next-steps"></a>Pasos siguientes

[Características de accesibilidad](/sccm/core/understand/accessibility-features)

