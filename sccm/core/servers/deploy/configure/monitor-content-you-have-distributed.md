---
title: "Implementación de contenido | System Center Configuration Manager"
description: Aprenda a supervisar contenido distribuido mediante la consola de Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 402c06ed92bbfe509206d3e7800e41e90c5d3a38

---
# <a name="monitor-content-you-have-distributed-with-system-center-configuration-manager"></a>Supervisión del contenido que se ha distribuido con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Utilice la consola de System Center Configuration Manager para supervisar el contenido distribuido, incluyendo:  

-   El estado de todos los tipos de paquetes en relación con los puntos de distribución asociados  

-   El estado de validación del contenido de un paquete  

-   El estado del contenido asignado a un grupo específico de puntos de distribución  

-   El estado del contenido asignado a un punto de distribución  

-   El estado de las características opcionales de cada punto de distribución (validación de contenido, PXE y multidifusión).  

> [!NOTE]  
>  Configuration Manager solo supervisa el contenido de un punto de distribución que se encuentre en la biblioteca de contenido. No se supervisa el contenido almacenado en el punto de distribución de recursos compartidos personalizados o de paquete.  

##  <a name="a-namebkmkcontentstatusa-content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Supervisión del estado del contenido  
 El nodo **Estado de contenido** en el área de trabajo **Supervisión** proporciona información acerca de los paquetes de contenido. En la consola de Configuration Manager, puede revisar información como la siguiente:  

-   El nombre del paquete  

-   Tipo  

-   El número de puntos de distribución a los que se envió un paquete  

-   La tasa de compatibilidad  

-   Cuándo se creó el paquete  

-   Identificador de paquete  

-   La versión de origen  

También encontrará información detallada del estado de cualquier paquete, así como el estado de distribución del paquete, incluido lo siguiente:  

-   El número de errores  

-   Las distribuciones pendientes  

-   El número de instalaciones  

También puede administrar las distribuciones que siguen en curso en un punto de distribución o que no pudieron distribuir correctamente el contenido a un punto de distribución:  

-   La opción aplicable para cancelar o redistribuir contenido está disponible cuando ve el mensaje de estado de implementación de un trabajo de distribución en un punto de distribución en el panel **Detalles de activos** de la ficha **En curso** o de la ficha **Error** el nodo **Estado de contenido** .  

-   Adicionalmente los detalles del trabajo muestran el porcentaje del trabajo que se ha completado cuando ve los detalles de un trabajo en la ficha **En curso** y el número de reintentos para un trabajo así como el tiempo que falta para el siguiente reintento cuando ve los detalles de un trabajo que está disponible en la ficha **Error** .  

Al cancelar una implementación que no está completa, se detiene el trabajo de distribución para transferir ese contenido:  

-   A continuación el estado de la implementación se actualiza para indicar el error de la distribución y la cancelación por una acción del usuario.  

-   Este nuevo estado aparece en la ficha **Error** .  

> [!TIP]  
>  Cuando una implementación está a punto de terminar, es posible que la acción para cancelar esa distribución no se procese antes de que se complete la distribución al punto de distribución. Cuando esto ocurre, se omite la acción para cancelar la implementación, y el estado de la implementación se muestra como correcto.  

> [!NOTE]  
>  Aunque puede seleccionar la opción de cancelar una distribución a un punto de distribución que se encuentra en un servidor del sitio, no tiene efecto. Esto se debe a que el servidor del sitio y el punto de distribución de un servidor de sitio comparten el mismo almacén de contenido de instancia único y no hay ningún trabajo de distribución real que cancelar.  

Cuando redistribuye contenido que previamente no se pudo transferir a un punto de distribución, Configuration Manager inicia inmediatamente la implementación de ese contenido al punto de distribución de nuevo y actualiza el estado de la implementación para reflejar el estado en curso de esa reimplementación.  

Utilice los procedimientos siguientes para ver el estado del contenido y administrar las distribuciones que siguen en curso o que han resultado erróneas.  

#### <a name="to-monitor-content-status"></a>Para supervisar el estado del contenido  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Estado de distribución**y, a continuación, haga clic en **Estado de contenido**. Se mostrarán los paquetes.  

3.  Seleccione el paquete del que desee información detallada de su estado.  

4.  En la pestaña **Inicio** , haga clic en **Ver estado**. Se mostrará información detallada del estado del paquete.  

#### <a name="to-cancel-a-distribution-that-remains-in-progress"></a>Para cancelar una distribución que sigue en curso  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Estado de distribución**y, a continuación, haga clic en **Estado de contenido**. Se mostrarán los paquetes.  

3.  Seleccione el paquete que desea administrar y, a continuación, en el panel de detalles, haga clic en **Ver estado**.  

4.  En el panel **Detalles de activos** de la ficha **En curso** , haga clic con el botón secundario en la entrada para la distribución que desea cancelar y seleccione **Cancelar**.  

5.  Haga clic en **Sí** para confirmar la acción y cancelar el proceso de distribución a ese punto de distribución.  

#### <a name="to-redistribute-content-that-failed-to-distribute"></a>Para redistribuir el contenido que no ha podido distribuir  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Estado de distribución**y, a continuación, haga clic en **Estado de contenido**. Se mostrarán los paquetes.  

3.  Seleccione el paquete que desea administrar y, a continuación, en el panel de detalles, haga clic en **Ver estado**.  

4.  En el panel **Detalles de activos** de la ficha **Error** , haga clic con el botón secundario en la entrada para la distribución que desea redistribuir y seleccione **Redistribuir**.  

5.  Haga clic en **Sí** para confirmar la acción e iniciar el proceso de redistribución a ese punto de distribución.  

## <a name="distribution-point-group-status"></a>Estado del grupo de puntos de distribución  
El nodo **Estado de grupo de puntos de distribución** en el área de trabajo **Supervisión** proporciona información acerca de los grupos de puntos de distribución. Puede revisar información como la siguiente:  

-   El nombre del grupo de puntos de distribución  

-   Descripción  

-   El número de puntos de distribución que pertenecen al grupo de puntos de distribución  

-   El número de paquetes que se asignaron al grupo  

-   Estado del grupo de puntos de distribución  

-   La tasa de compatibilidad  

También puede ver información de estado detallada, incluido lo siguiente:  

-   Errores del grupo de puntos de distribución  

-   El número de distribuciones que están en curso  

-   El número de distribuciones que son correctas  

#### <a name="to-monitor-distribution-point-group-status"></a>Para supervisar el estado del grupo de puntos de distribución  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Estado de distribución**y, a continuación, haga clic en **Estado de grupo de puntos de distribución**. Se mostrarán los grupos de puntos de distribución.  

3.  Seleccione el grupo de puntos de distribución del que desee obtener información detallada de su estado.  

4.  En la pestaña **Inicio** , haga clic en **Ver estado**. Se mostrará información detallada del estado del grupo de puntos de distribución.  

## <a name="distribution-point-configuration-status"></a>Estado de configuración de punto de distribución  
 El nodo **Estado de configuración de punto de distribución** en el área de trabajo **Supervisión** proporciona información acerca del punto de distribución. Puede revisar los atributos que están habilitados para el punto de distribución, tales como PXE, multidifusión y validación de contenido, y el estado de la configuración del punto de distribución. También puede ver información detallada del estado del punto de distribución.  

> [!WARNING]  
>  El estado de la configuración del punto de distribución se refiere a las últimas 24 horas. Si el punto de distribución tiene un error y se recupera, el estado del error podría mostrarse hasta 24 horas después de que se recupere el punto de distribución.  

Utilice el procedimiento siguiente para ver el estado de configuración del punto de distribución.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Para supervisar el estado de configuración de punto de distribución  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Estado de distribución**y, a continuación, haga clic en **Estado de configuración de punto de distribución**. Se mostrarán los puntos de distribución.  

3.  Seleccione el punto de distribución del que desee obtener información de su estado.  

4.  En el panel de resultados, haga clic en la pestaña **Detalles** . Se mostrará información de estado del punto de distribución.  



<!--HONumber=Nov16_HO1-->


