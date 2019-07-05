---
title: Consola de Configuration Manager
titleSuffix: Configuration Manager
description: Obtenga información sobre la navegación a través de la consola de Configuration Manager.
ms.date: 06/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3fc9e6fad0b7be3762b3d642c94c4cf17266e0b3
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285733"
---
# <a name="using-the-configuration-manager-console"></a>Uso de la consola de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los administradores usan la consola de Configuration Manager para administrar el entorno de Configuration Manager. Este artículo trata los aspectos básicos de navegación de la consola.  



## <a name="connect-to-a-site-server"></a>Conexión a un servidor de sitio

La consola se conecta al servidor de sitio de administración central o a los servidores de sitio primarios. No se puede conectar una consola de Configuration Manager a un sitio secundario. Puede [instalar la consola de Configuration Manager](/sccm/core/servers/deploy/install/install-consoles). Durante la instalación, especificó el nombre de dominio completo (FQDN) del servidor de sitio al que se conecta la consola. 

Para conectarse a otro servidor de sitio, siga estos pasos: 

1. Haga clic en la flecha situada en la parte superior de la [cinta](#ribbon) y elija **Conectar a un nuevo sitio**.  

    ![Conexión de la consola a un sitio nuevo](media/connect-to-a-new-site.png)  

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

 ![Ventana de Opciones del Panel de navegación para cambiar el orden de las áreas de trabajo](media/navigation-pane-options.png)  

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

## <a name="bkmk_viewconnected"></a> Consulta de las consolas conectadas recientemente
<!--3699367-->

A partir de la versión 1902, puede ver las conexiones más recientes de la consola de Configuration Manager. La vista incluye las conexiones activas y aquellas que se acaban de conectar. Siempre verá la conexión actual de la consola en la lista. Solo se muestran las conexiones desde la consola de Configuration Manager, no las conexiones de PowerShell ni otras conexiones basadas en el SDK al proveedor de SMS. El sitio quita las instancias de la lista que tienen más de 30 días.


### <a name="prerequisites-to-view-connected-consoles"></a>Requisitos previos para ver las consolas conectadas

- La cuenta debe tener el permiso **Lectura** en el objeto **SMS_Site**. 
- IIS debe estar instalado en el servidor de proveedor de SMS <!---SCCMDocs-pr issue 1326--> 
- Habilitar el proveedor de SMS para usar un certificado.<!--SCCMDocs-pr issue 3135--> Use una de las opciones siguientes:  

  - Habilitar [HTTP mejorado](/sccm/core/plan-design/hierarchy/enhanced-http) (recomendado)
  - Enlazar manualmente un certificado basado en PKI al puerto 443 en IIS en el servidor que hospeda el rol de proveedor de SMS  

### <a name="view-connected-consoles"></a>Consulta de las consolas conectadas

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**.  

2. Expanda **Seguridad** y seleccione el nodo **Conexiones de la consola**.  

3. Vea las conexiones recientes con estas propiedades:  

    - Nombre de usuario
    - Nombre de máquina
    - Código de sitio conectado
    - Versión de la consola
    - Hora de la última conexión: momento en el que el usuario *abrió* la consola por última vez

![Consulta de las conexiones de la consola de Configuration Manager](media/console-connections.png) 


## <a name="bkmk_notify"></a> Notificaciones de la consola de Configuration Manager
<!--3556016, fka 1318035-->
A partir de la versión 1902 de Configuration Manager, la consola lo notifica en caso de los siguientes eventos:

- Cuando hay una actualización disponible para el propio Configuration Manager
- Cuando se producen eventos de ciclo de vida y mantenimiento en el entorno

Esta notificación es una barra en la parte superior de la ventana de la consola, debajo de la cinta. Reemplaza a la experiencia anterior cuando había disponibles actualizaciones de Configuration Manager. Estas notificaciones en consola aún muestran información crítica, pero no interfieren con el trabajo en la consola. No se pueden descartar las notificaciones críticas. La consola muestra todas las notificaciones en una nueva área de notificación de la barra de título.

![Barra de notificación y marca en consola](./media/1318035-notify-eval-version-expired.png)

### <a name="configure-a-site-to-show-non-critical-notifications"></a>Configuración de un sitio para que muestre notificaciones no críticas

Puede configurar cada sitio para que muestre las notificaciones no críticas en las propiedades del sitio.

1.  En el área de trabajo **Administración**, expanda **Configuración del sitio** y, a continuación, haga clic en el nodo **Sitios**.
1. Seleccione el sitio que quiere configurar para las notificaciones no críticas.
1. En la cinta, haga clic en **Propiedades**.
1. En la pestaña **Alertas**, seleccione la opción de **habilitar las notificaciones de la consola para cambios de estado de sitio no críticos**.
   - Si habilita esta opción, todos los usuarios de la consola ven notificaciones críticas, de advertencia e informativas. Esta opción está habilitada de forma predeterminada.  
   - Si deshabilita esta opción, los usuarios de la consola solo ven las notificaciones críticas.  

La mayoría de las notificaciones de consola son por sesión. La consola evalúa las consultas cuando un usuario la inicia. Para ver los cambios en las notificaciones, reinicie la consola. Si un usuario descarta una notificación no crítica, vuelve a notificar cuando se reinicia la consola, si sigue siendo aplicable.

Las siguientes notificaciones se vuelven a evaluar cada cinco minutos:
- El sitio está en modo de mantenimiento  
- El sitio está en modo de recuperación  
- El sitio está en modo de actualización  

Las notificaciones siguen los permisos de la administración basada en roles. Por ejemplo, si un usuario no tiene permisos para ver las actualizaciones de Configuration Manager, no ve esas notificaciones.

Algunas notificaciones tienen una acción relacionada. Por ejemplo, si la versión de la consola no coincide con la versión del sitio, seleccione **Instalar la nueva versión de la consola**. Esta acción inicia el instalador de la consola. 

Las siguientes notificaciones son más aplicables a la rama de Technical Preview:  

- La versión de evaluación expira en 30 días (advertencia): faltan 30 días desde la fecha actual para la fecha de expiración de la versión de evaluación  
- La versión de evaluación ha expirado (crítico): la fecha actual es posterior a la fecha de expiración de la versión de evaluación  
- Discrepancia de versiones de consola (crítico): la versión de la consola no coincide con la versión del sitio  
- Actualización de sitio disponible (advertencia): hay un nuevo paquete de actualización disponible  

Para obtener más información y ayuda para la solución de problemas, vea el archivo **SmsAdminUI.log** en el equipo de la consola. De forma predeterminada, este archivo de registro está en la ruta de acceso siguiente: `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog\SmsAdminUI.log`.

## <a name="bkmk_doc-dashboard"></a> Panel de documentación en consola
<!--3556019 FKA 1357546-->

A partir de la versión 1902 de Configuration Manager, hay un nodo de **Documentación** en la nueva área de trabajo **Comunidad**. Este nodo incluye información actualizada acerca de los artículos de soporte técnico y la documentación de Configuration Manager. Se incluyen las secciones siguientes:  

### <a name="product-documentation-library"></a>Biblioteca de documentación del producto

- **Recomendado**: lista mantenida manualmente de artículos importantes.
- **Tendencias**: los artículos más populares del último mes.
- **Actualizado recientemente**: artículos revisados en el último mes.

### <a name="support-articles"></a>Artículos de soporte técnico

- **Artículos de solución de problemas**: tutoriales guiados que le ayudarán a solucionar problemas de características y componentes de Configuration Manager.
- **Artículos de soporte técnico nuevos y actualizados**: artículos que son nuevos o se han actualizado en los últimos dos meses.


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

### <a name="search-device-views-using-mac-address"></a>Vistas de búsqueda de dispositivos mediante dirección MAC
<!--3600878-->
*(Se introdujo en la versión 1902)*

Puede buscar una dirección MAC en la vista de un dispositivo de la consola de Configuration Manager. Esta propiedad es útil para los administradores de implementaciones de sistema operativo durante la solución de problemas de implementaciones de PXE. Cuando vea una lista de dispositivos, agregue la columna **Dirección MAC** a la vista. Use el campo de búsqueda para agregar los criterios de búsqueda de **Dirección MAC**.

### <a name="maximize-the-browse-registry-window"></a>Maximizar la ventana Examinar registro
<!--3594151 includes all MMS 1902 console changes-->
*(Se introdujo en la versión 1902)*
1. En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y haga clic en el nodo **Aplicaciones**. 
1. Seleccione una aplicación que tenga un tipo de implementación con un método de detección. Por ejemplo, un método de detección de Windows Installer. 
1. En el panel de detalles, cambie a la pestaña **Tipos de implementación**. 
1. Abra las propiedades de un tipo de implementación y cambie a la pestaña **Método de detección**. Haga clic en **Agregar cláusula**. 
1. Cambiar **Tipo de configuración** a **Registro** y haga clic en **Examinar** para abrir la ventana **Examinar registro**. Ahora puede maximizar esta ventana.  

### <a name="go-to-the-collection-from-an-application-deployment"></a>Ir a la colección desde una implementación de aplicación

*(Se introdujo en la versión 1902)*
1. En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y haga clic en el nodo **Aplicaciones**. 
1. Seleccione una aplicación. En el panel de detalles, cambie a la pestaña **Implementaciones**.
1. Seleccione una implementación y, después, haga clic en la nueva opción **Colección** en la cinta de la pestaña Implementación. Esta acción cambia la vista a la colección que es el destino de la implementación.
   - Esta acción también está disponible en el menú contextual de la implementación de esta vista.

### <a name="edit-a-task-sequence-by-default"></a>Editar una secuencia de tareas de forma predeterminada

*(Se introdujo en la versión 1902)*

En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en el nodo **Secuencias de tareas**. **Editar** es ahora la acción predeterminada cuando se abre una secuencia de tareas. Anteriormente, la acción predeterminada era **Propiedades**.  

### <a name="remove-content-from-monitoring-status"></a>Quitar contenido del estado de supervisión
*(Se introdujo en la versión 1902)*

1. En el área de trabajo **Supervisión**, expanda **Estado de distribución** y haga clic en **Estado de contenido**.
1. Seleccione un elemento en la lista y haga clic en la nueva opción **Ver estado** de la cinta. 
1. En el panel Detalles del activo, haga clic con el botón derecho en un punto de distribución y seleccione la nueva opción **Quitar**. Esta acción quita este contenido del punto de distribución seleccionado.

### <a name="views-sort-by-integer-values"></a>Ordenar las vistas por valores enteros
*(Se introdujo en la versión 1902)*

Realizamos mejoras en la forma en que varias vistas orden los datos. Por ejemplo, en el nodo **Implementaciones** del área de trabajo **Supervisión**, ahora las columnas siguientes se ordenan como números en lugar de como valores de cadena:  

- Enumerar errores
- Enumerar en progreso
- Enumerar otros
- Enumerar correctos
- Enumerar desconocidos  

### <a name="move-the-warning-for-a-large-number-of-results"></a>Mover la advertencia de un número de resultados elevado
*(Se introdujo en la versión 1902)*

Cuando en la consola hace clic en un nodo que devuelve más de 1.000 resultados, Configuration Manager muestra la advertencia siguiente:

> Configuration Manager devolvió un gran número de resultados. Puede restringir los resultados mediante las características de búsqueda. O hacer clic aquí para ver un número máximo de 100 000.
 
Ahora hay un espacio en blanco adicional entre esta advertencia y el campo de búsqueda. Este cambio ayuda a evitar que se seleccione accidentalmente la advertencia para mostrar más resultados. 



### <a name="send-feedback"></a>Enviar comentarios
<!--1357542-->

A partir de la versión 1806, los comentarios sobre el producto se envían desde la consola.  

- **Enviar una sonrisa**: envíe comentarios sobre lo que le ha gustado.  

- **Enviar una desaprobación**: envíe comentarios sobre lo que no le ha gustado.  

- **Enviar una sugerencia**: le lleva a UserVoice para compartir sus ideas.  
 
Para obtener más información, vea [Comentarios sobre el producto](/sccm/core/understand/find-help#BKMK_1806Feedback).


### <a name="assets-and-compliance-workspace"></a>Área de trabajo Activos y compatibilidad

#### <a name="view-users-for-a-device"></a>Ver los usuarios de un dispositivo
A partir de la versión 1806, las siguientes columnas están disponibles en el nodo **Dispositivos**:  

- **Usuarios primarios** <!--1357280-->  

- **Usuario que ha iniciado sesión actualmente** <!--1358202-->  
    > [!NOTE]  
    > Para poder ver el usuario que ha iniciado sesión actualmente, necesitará la [detección de usuarios](/sccm/core/servers/deploy/configure/configure-discovery-methods#bkmk_config-adud) y la [afinidad entre usuario y dispositivo](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  

Para obtener más información sobre cómo mostrar una columna no predeterminada, vea [Columnas](#columns).

#### <a name="improvement-to-device-search-performance"></a>Mejora de rendimiento de la búsqueda de dispositivos
<!-- 3614690 -->
A partir de la versión 1806, al realizar búsquedas en una recopilación de dispositivos, no se busca la palabra clave en todas las propiedades del objeto. Cuando no especifique lo que hay que buscar, busca a través de las cuatro propiedades siguientes:
- Nombre
- Usuarios primarios
- Usuario que ha iniciado sesión actualmente
- Nombre de usuario de último inicio de sesión

Este comportamiento mejora significativamente el tiempo necesario para buscar por nombre, especialmente en un entorno grande. Las búsquedas personalizadas según criterios específicos no se ven afectadas. 


### <a name="monitoring-workspace"></a>Área de trabajo de supervisión

#### <a name="copy-details-in-monitoring-views"></a>Copiar detalles en las vistas de supervisión
<!--1357856-->
A partir de la versión 1806, se puede copiar información desde el panel **Detalles del activo** a los siguientes nodos de supervisión:  

- **Estado de distribución de contenido**  

- **Estado de implementación**  

![Vista del estado de implementación, detalles del activo de copia](media/1810-deployment-status.PNG)



## <a name="next-steps"></a>Pasos siguientes

[Características de accesibilidad](/sccm/core/understand/accessibility-features)

