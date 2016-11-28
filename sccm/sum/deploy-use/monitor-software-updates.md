---

title: Supervisar actualizaciones de software | Configuration Manager
description: La consola de System Center Configuration Manager proporciona alertas y estados para supervisar la compatibilidad y las actualizaciones.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fe41807cebf87f4e6bab47e41db0ffe7cc83c5d1

---
# <a name="monitor-software-updates-in-system-center-configuration-manager"></a>Supervisar actualizaciones de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

System Center Configuration Manager ofrece muchas maneras de ayudarle a supervisar los objetos, procesos e información de compatibilidad de las actualizaciones de software. Use las secciones siguientes para supervisar las actualizaciones de software.

##  <a name="a-namebkmksualertsa-alerts-for-software-updates"></a><a name="BKMK_SUAlerts"></a> Alertas de actualizaciones de software  
 Puede configurar alertas de actualizaciones de software a fin de notificar a los usuarios administrativos cuándo los niveles de compatibilidad de las implementaciones de actualizaciones de software están por debajo del porcentaje configurado. Puede configurar alertas para las implementaciones de actualizaciones de software en las siguientes ubicaciones:  

-   Configuración de ADR: puede configurar las opciones de alertas en el Asistente para crear regla de implementación automática y en las propiedades de la regla de implementación automática.  

-   Configuración de implementación: puede configurar las opciones de alertas en el Asistente para implementar actualizaciones de software y en las propiedades de la implementación.  

Después de configurar las opciones de alertas, si se producen las condiciones especificadas, Configuration Manager genera una alerta. Puede revisar las alertas de actualizaciones de software en las siguientes ubicaciones:  

1.  Revise las alertas recientes en el nodo **Actualizaciones de software** en el área de trabajo **Biblioteca de software** .  

2.  Administre las alertas configuradas en el nodo **Alertas** en el área de trabajo **Supervisión** .  

##  <a name="a-namebkmksusyncstatusa-software-updates-synchronization-status"></a><a name="BKMK_SUSyncStatus"></a> Estado de sincronización de las actualizaciones de software  
 Después de iniciar el proceso de sincronización, puede usar la consola de Configuration Manager para supervisar el proceso de sincronización de todos los puntos de actualización de software de la jerarquía. Utilice el siguiente procedimiento para supervisar el proceso de sincronización de la actualización de software.  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Para supervisar el proceso de sincronización de las actualizaciones de software  

- En la consola de Configuration Manager, navegue hasta **Supervisión** > **Introducción** > **Estado de sincronización de punto de actualización de software**.  

    Los puntos de la actualización de software en su jerarquía de Configuration Manager se muestran en el panel de resultados. Desde esta vista, puede supervisar el estado de la sincronización de todos los puntos de actualización de software. Para consultar más información detallada sobre el proceso de sincronización, puede revisar el archivo wsyncmgr.log, que se encuentra en <*Ruta de instalación de Configuration Manager*>\Logs en cada servidor de sitio.  

##  <a name="a-namebkmksudeploystatusa-software-update-deployment-status"></a><a name="BKMK_SUDeployStatus"></a> Estado de implementación de actualizaciones de software  
 Después de implementar las actualizaciones de software en un grupo de actualizaciones de software, o después de implementar una actualización de software individual, puede supervisar el estado de implementación. Utilice el siguiente procedimiento para supervisar el estado de implementación de un grupo de actualizaciones de software o de una actualización de software.  

#### <a name="to-monitor-deployment-status"></a>Para supervisar el estado de implementación  

1.  En la consola de Configuration Manager, navegue hasta **Supervisión** > **Información general** > **Implementaciones**.  

2.  Haga clic en el grupo de actualizaciones de software o en una actualización de software cuyo estado de implementación desea supervisar.  

3.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Ver estado**.  

##  <a name="a-namebkmksureportsa-software-updates-reports"></a><a name="BKMK_SUReports"></a> Informes de actualizaciones de software  
 Los mensajes de estado para las actualizaciones de software proporcionan información acerca de la compatibilidad de las actualizaciones de software y el estado de la evaluación y aplicación de las implementaciones de actualizaciones de software. Puede ejecutar informes de actualizaciones de software para mostrar los mensajes de estado. Se encuentran disponibles más de 30 informes predefinidos de actualizaciones de software. Se organizan en diferentes categorías y se pueden utilizar para proporcionar información específica acerca de las implementaciones y actualizaciones de software. Además de utilizar los informes preconfigurados, también puede crear informes de actualizaciones de software personalizados según las necesidades de la empresa. Para obtener más información, vea [Operaciones y mantenimiento de informes](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

##  <a name="a-namebkmkmonitorcontenta-monitor-content"></a><a name="BKMK_MonitorContent"></a> Supervisar contenido  
 Puede supervisar el contenido en la consola de Configuration Manager para consultar el estado de todos los tipos de paquetes en relación con los puntos de distribución asociados. Esto puede incluir el estado de validación del contenido del paquete, el estado del contenido asignado a un grupo de puntos de distribución específico, el estado del contenido asignado a un punto de distribución y el estado de las características opcionales de cada punto de distribución (validación de contenido, PXE y multidifusión).  

###  <a name="a-namebkmkcontentstatusa-content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Supervisión del estado del contenido  
 El nodo **Estado de contenido** en el área de trabajo **Supervisión** proporciona información acerca de los paquetes de contenido. Puede consultar información general acerca del paquete, el estado de distribución del paquete e información de estado detallada acerca del paquete. Utilice el procedimiento siguiente para ver el estado del contenido.  

#### <a name="to-monitor-content-status"></a>Para supervisar el estado del contenido  

1.  En la consola de Configuration Manager, navegue hasta **Supervisión** > **Información general** > **Estado de distribución** > **Estado del contenido**. Se mostrarán los paquetes.  

2.  Seleccione el paquete del que desea ver información de estado detallada.  

3.  En la pestaña **Inicio** , haga clic en **Ver estado**. Se mostrará información detallada del estado del paquete.  

###  <a name="a-namebkmkdpgroupstatusa-distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a> Estado del grupo de puntos de distribución  
 El nodo **Estado de grupo de puntos de distribución** en el área de trabajo **Supervisión** proporciona información acerca de los grupos de puntos de distribución. Puede consultar información general acerca del grupo de puntos de distribución, como el estado y la tasa de compatibilidad del grupo de puntos de distribución, así como información de estado detallada acerca del grupo de puntos de distribución. Utilice el procedimiento siguiente para ver el estado del grupo de puntos de distribución.  

#### <a name="to-monitor-distribution-point-group-status"></a>Para supervisar el estado del grupo de puntos de distribución  

1.  En la consola de Configuration Manager, navegue hasta **Supervisión** > **Información general** > **Estado de distribución** > **Estado del grupo de puntos de distribución**. Se mostrarán los grupos de puntos de distribución.  

2.  Seleccione el grupo de puntos de distribución del que desea ver información de estado detallada.  

3.  En la pestaña **Inicio** , haga clic en **Ver estado**. Se mostrará información detallada del estado del grupo de puntos de distribución.  

###  <a name="a-namebkmkdpconfigstatusa-distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a> Estado de configuración de punto de distribución  
 El nodo **Estado de configuración de punto de distribución** en el área de trabajo **Supervisión** proporciona información acerca del punto de distribución. Puede revisar los atributos que están habilitados para el punto de distribución, como PXE, multidifusión y validación de contenido. También puede ver información detallada del estado del punto de distribución. Utilice el procedimiento siguiente para ver el estado de configuración del punto de distribución.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Para supervisar el estado de configuración de punto de distribución  

1.  En la consola de Configuration Manager, navegue hasta **Supervisión** > **Información general** > **Estado de distribución** > **Estado de configuración de punto de distribución**. Se mostrarán los puntos de distribución.  

2.  Seleccione el punto de distribución del que desea ver información de estado de punto de distribución.  

3.  En el panel de resultados, haga clic en la pestaña **Detalles** . Se mostrará información de estado del punto de distribución.  



<!--HONumber=Nov16_HO1-->


