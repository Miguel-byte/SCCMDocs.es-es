---
title: Supervisar contenido
titleSuffix: Configuration Manager
description: Aprenda a supervisar contenido distribuido mediante la consola de Configuration Manager.
ms.custom: na
ms.date: 4/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
caps.latest.revision: "5"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 5b1c0401c0b1ce2aa8765ccfb8898b90cf7a5c93
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2017
---
# <a name="monitor-content-you-have-distributed-with-system-center-configuration-manager"></a>Supervisión del contenido que se ha distribuido con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Utilice la consola de System Center Configuration Manager para supervisar el contenido distribuido, incluido lo siguiente:  

-   Estado de todos los tipos de paquetes en relación con los puntos de distribución asociados  
-   Estado de validación del contenido de un paquete  
-   Estado del contenido asignado a un grupo específico de puntos de distribución  
-   Estado del contenido asignado a un punto de distribución  
-   Estado de las características opcionales de cada punto de distribución (validación de contenido, PXE y multidifusión)  

> [!NOTE]  
>  Configuration Manager solo supervisa el contenido de un punto de distribución que se encuentre en la biblioteca de contenido. No se supervisa el contenido almacenado en el punto de distribución de recursos compartidos personalizados o de paquete.  

##  <a name="BKMK_ContentStatus"></a> Supervisión del estado del contenido  
 El nodo **Estado de contenido** en el área de trabajo **Supervisión** proporciona información acerca de los paquetes de contenido. En la consola de Configuration Manager, puede revisar información como la siguiente:  

-   Nombre del paquete  
-   Tipo  
-   Número de puntos de distribución a los que se envió un paquete  
-   Tasa de cumplimiento  
-   Fecha de creación del paquete  
-   Identificador del paquete  
-   Versión de origen  

También encontrará información detallada del estado de cualquier paquete, así como el estado de distribución del paquete, incluido lo siguiente:  

-   Número de errores  
-   Distribuciones pendientes  
-   Número de instalaciones

También puede administrar las distribuciones que siguen en curso en un punto de distribución o que no pudieron distribuir correctamente el contenido en un punto de distribución:  

-   La opción para cancelar o redistribuir contenido está disponible cuando ve el mensaje de estado de implementación de un trabajo de distribución en un punto de distribución en el panel **Detalles del activo**. Este panel se encuentra en la pestaña **En curso**, o bien en la pestaña **Error** del nodo **Estado de contenido**.  
-   Además, en los detalles del trabajo se muestra el porcentaje del trabajo que se ha completado al consultarlo en la pestaña **En curso**. En los detalles del trabajo también se muestra el número de reintentos restantes de un trabajo, así como el tiempo que queda hasta que se produzca el siguiente reintento al consultar los detalles de un trabajo que está disponible en la pestaña **Error**.  

Al cancelar una implementación que no está completa, se detiene el trabajo de distribución para transferir ese contenido:  

-   Luego, el estado de la implementación se actualiza para indicar que se produjo un error en la distribución y que esta se canceló por medio de una acción del usuario.  
-   Este nuevo estado aparece en la ficha **Error** .  

> [!TIP]  
>  Cuando una implementación está a punto de terminar, es posible que la acción para cancelar esa distribución no se procese antes de que se complete la distribución al punto de distribución. Cuando esto ocurre, se omite la acción para cancelar la implementación, y el estado de la implementación se muestra como correcto.  

> [!NOTE]  
>  Aunque puede seleccionar la opción de cancelar una distribución a un punto de distribución que se encuentra en un servidor del sitio, no tiene efecto. Esto se debe a que el servidor del sitio y el punto de distribución de un servidor de sitio comparten el mismo almacén de contenido de instancia único. No hay ningún trabajo de distribución real que cancelar.  

Cuando se redistribuye contenido que previamente no se pudo transferir a un punto de distribución, Configuration Manager comienza inmediatamente a volver a implementar ese contenido en el punto de distribución. Configuration Manager actualiza el estado de la implementación para reflejar el estado en curso de esa reimplementación.  

Utilice los procedimientos siguientes para ver el estado del contenido y administrar las distribuciones que siguen en curso o que han generado errores.  

### <a name="to-monitor-content-status"></a>Para supervisar el estado del contenido  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Estado de distribución**y, a continuación, haga clic en **Estado de contenido**. Se mostrarán los paquetes.  

3.  Seleccione el paquete para el que quiera información detallada de su estado.  

4.  En la pestaña **Inicio** , haga clic en **Ver estado**. Se mostrará información detallada del estado del paquete.  

### <a name="to-cancel-a-distribution-that-remains-in-progress"></a>Para cancelar una distribución que sigue en curso  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Estado de distribución**y, a continuación, haga clic en **Estado de contenido**. Se mostrarán los paquetes.  

3.  Seleccione el paquete que desea administrar y, a continuación, en el panel de detalles, haga clic en **Ver estado**.  

4.  En el panel **Detalles del activo** de la pestaña **En curso**, haga clic con el botón derecho en la entrada de la distribución que quiera cancelar y seleccione **Cancelar**.  

5.  Haga clic en **Sí** para confirmar la acción y cancelar el proceso de distribución a ese punto de distribución.  

### <a name="to-redistribute-content-that-failed-to-distribute"></a>Para redistribuir el contenido que no ha podido distribuir  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Estado de distribución**y, a continuación, haga clic en **Estado de contenido**. Se mostrarán los paquetes.  

3.  Seleccione el paquete que desea administrar y, a continuación, en el panel de detalles, haga clic en **Ver estado**.  

4.  En el panel **Detalles del activo** de la pestaña **Error**, haga clic con el botón derecho en la entrada de la distribución que quiera redistribuir y seleccione **Redistribuir**.  

5.  Haga clic en **Sí** para confirmar la acción e iniciar el proceso de redistribución a ese punto de distribución.  

## <a name="distribution-point-group-status"></a>Estado del grupo de puntos de distribución  
El nodo **Estado de grupo de puntos de distribución** en el área de trabajo **Supervisión** proporciona información acerca de los grupos de puntos de distribución. Puede revisar información como la siguiente:  

-   Nombre del grupo de puntos de distribución  
-   Descripción  
-   Número de puntos de distribución que pertenecen al grupo de puntos de distribución  
-   Número de paquetes que se asignaron al grupo  
-   Estado del grupo de puntos de distribución  
-   Tasa de cumplimiento  

También puede ver información de estado detallada, incluido lo siguiente:  

-   Errores del grupo de puntos de distribución  
-   Número de distribuciones en curso
-   Número de distribuciones correctas  

### <a name="to-monitor-distribution-point-group-status"></a>Para supervisar el estado del grupo de puntos de distribución  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Estado de distribución**y, a continuación, haga clic en **Estado de grupo de puntos de distribución**. Se mostrarán los grupos de puntos de distribución.  

3.  Seleccione el grupo de puntos de distribución para el que quiera obtener información detallada de su estado.  

4.  En la pestaña **Inicio** , haga clic en **Ver estado**. Se mostrará información detallada del estado del grupo de puntos de distribución.  

## <a name="distribution-point-configuration-status"></a>Estado de configuración de punto de distribución  
 El nodo **Estado de configuración de punto de distribución** en el área de trabajo **Supervisión** proporciona información acerca del punto de distribución. Puede revisar los atributos que están habilitados para el punto de distribución, tales como PXE, multidifusión y validación de contenido, así como el estado de distribución del punto de distribución. También puede ver información detallada del estado del punto de distribución.  

> [!WARNING]  
>  El estado de la configuración del punto de distribución se refiere a las últimas 24 horas. Si el punto de distribución tiene un error y se recupera, el estado del error podría mostrarse hasta 24 horas después de que se recupere el punto de distribución.  

Utilice el procedimiento siguiente para ver el estado de configuración del punto de distribución.  

### <a name="to-monitor-distribution-point-configuration-status"></a>Para supervisar el estado de configuración de punto de distribución  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Estado de distribución**y, a continuación, haga clic en **Estado de configuración de punto de distribución**. Se mostrarán los puntos de distribución.  

3.  Seleccione el punto de distribución para el que quiera obtener información de su estado.  

4.  En el panel de resultados, haga clic en la pestaña **Detalles** . Se mostrará información de estado del punto de distribución.  

## <a name="client-data-sources-dashboard"></a>Panel de orígenes de datos de cliente
A partir de la versión 1610, puede usar el panel **Orígenes de datos de cliente** para entender el uso del [Almacenamiento en caché del mismo nivel](/sccm/core/plan-design/hierarchy/client-peer-cache) en su entorno. El panel mostrará los datos después de que los clientes descarguen contenido y notifiquen esa información al sitio. Esto puede tardar hasta 24 horas.

> [!TIP]  
> El panel **Orígenes de datos de cliente** y **Caché del mismo nivel de cliente**  son características de la versión preliminar introducidas en la versión 1610. Debe habilitar Caché del mismo nivel de cliente antes de que el panel Orígenes de datos de cliente se vuelva visible en la consola. Para habilitar Caché del mismo nivel de cliente, vea [Uso de las características de versión preliminar de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease). Una vez que lo haya habilitado, puede tardar hasta 24 horas en empezar a mostrar los datos.

En la consola, vaya a **Supervisión** > **Estado de distribución** > **Orígenes de datos de cliente**. Aquí puede seleccionar un período de tiempo que se aplicará al panel. A continuación, en la pantalla, puede seleccionar el grupo de límites o el paquete para el que desea ver información. Al ver la información, puede mantener el puntero sobre la superficie para ver más detalles sobre los distintos orígenes de contenido o directiva.

Entre los detalles se incluye lo siguiente:  
- **Orígenes de contenido de cliente**: muestra el origen desde el que los clientes obtuvieron el contenido.
- **Puntos de distribución**: muestra el número de puntos de distribución que forman parte del grupo de límites seleccionado.
- **Clientes que utilizan un punto de distribución**: del número de clientes que están en el grupo de límites seleccionado, muestra cuántos usaron un punto de distribución para obtener el contenido.
- **Orígenes de almacenamiento en caché del mismo nivel**: para el grupo de límites seleccionado, muestra cuántos orígenes de almacenamiento caché del mismo nivel han informado del historial de descargas.
- **Clientes que utilizan almacenamiento caché del mismo nivel**: del número de clientes que están en el grupo de límites seleccionado, muestra cuántos usaron un origen de almacenamiento caché del mismo nivel para obtener el contenido.



También puede usar un nuevo informe, **Orígenes de datos de cliente - Resumen**, para ver un resumen de los orígenes de datos de cliente de cada grupo de límites.
