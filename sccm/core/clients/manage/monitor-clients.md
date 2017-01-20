---
title: "Supervisión de clientes | System Center Configuration Manager"
description: "Obtenga información detallada acerca de cómo supervisar clientes en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
caps.latest.revision: 23
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9961932a35a685626c021613d69f9b223f781d46


---
# <a name="how-to-monitor-clients-in-system-center-configuration-manager"></a>Supervisar clientes en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


 Una vez que la aplicación cliente de System Center Configuration Manager se ha instalado en los equipos y dispositivos Windows de su sitio, puede supervisar su estado y la actividad en la consola de Configuration Manager.  

##  <a name="a-namebkmkabouta-about-client-status"></a><a name="bkmk_about"></a> Acerca del estado de cliente  
 Configuration Manager proporciona los siguientes tipos de información como estado de cliente:  

-   **Estado de conexión de cliente**: a partir de la versión 1602 de Configuration Manager, este estado indica si el equipo está en línea o no. Un equipo se considera en línea si está conectado a su punto de administración asignado.  Para indicar que el cliente está en línea, envía mensajes de estilo ping al punto de administración. Si el punto de administración no recibe un mensaje en cinco minutos, se considera que el cliente está sin conexión.  

-   **Actividad del cliente**: este estado indica si el cliente ha interactuado con Configuration Manager durante los últimos siete días. Si el cliente no ha solicitado una actualización de directivas, no ha enviado un mensaje de latido o no ha enviado inventario de hardware en siete días, se considera inactivo.  

-   **Comprobación de cliente**: este estado indica el éxito de la evaluación periódica que el cliente de Configuration Manager ejecuta en el equipo.  La evaluación comprueba el equipo y puede corregir algunos de los problemas que encuentre. Para más información, consulte las [comprobaciones y correcciones realizadas mediante comprobación de cliente](#BKMK_ClientHealth).  

     En los equipos que ejecutan Windows 7, la comprobación de cliente se ejecuta como una tarea programada. En los sistemas operativos posteriores, la comprobación de cliente se ejecuta automáticamente en la ventana de mantenimiento de Windows.  

     Puede configurar la corrección para que no se ejecute en equipos específicos, por ejemplo, un servidor crítico del negocio. Además, si hay elementos adicionales que desea evaluar, puede usar la configuración de cumplimiento de Configuration Manager para obtener una solución completa para la supervisión del estado general, la actividad y el cumplimiento de los equipos de su organización. Para obtener más información sobre la configuración de cumplimiento, consulte [Plan for and configure compliance settings in System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) (Planeación y configuración de las opciones de cumplimiento en System Center Configuration Manager).  

##  <a name="a-namebkmkindstatusa-monitor-the-status-of-individual-clients"></a><a name="bkmk_indStatus"></a> Supervisión del estado de clientes individuales  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Dispositivos**, o elija una recopilación en **Recopilaciones de dispositivos**.  

     A partir de la versión 1602 de Configuration Manager, los iconos al principio de cada fila indican el estado de conexión del dispositivo:  

    |||  
    |-|-|  
    |![icono de estado conectado para los clientes](../../../core/clients/manage/media/online-status-icon.png)|El dispositivo está conectado.|  
    |![icono de estado desconectado para los clientes](../../../core/clients/manage/media/offline-status-icon.png)|El dispositivo está desconectado.|  
    |![icono de estado desconocido para los clientes](../../../core/clients/manage/media/unknown-status-icon.png)|Se desconoce el estado de conexión.|  
    |![cliente no instalado](../../../core/clients/manage/media/client-not-installed.png)|El cliente no está instalado en el dispositivo.|  

2.  Para tener información más detallada sobre el estado de conexión, agregue la información del estado de conexión del cliente a la vista de dispositivos; para ello, haga clic con el botón derecho en el encabezado de columna y haga clic en los campos de estado de conexión que quiera agregar. Las columnas que puede agregar son:  

    -   **Estado de conexión del dispositivo** indica si el cliente está actualmente conectado o no. (Esta es la misma información proporcionada por los iconos).  

    -   **Última hora en línea** indica cuándo cambió el estado de conexión del cliente a conectado.  

    -   **Última hora sin conexión** indica cuándo cambió el estado a sin conexión.  

3.  Haga clic en un cliente individual en el panel de lista para ver más información de estado en el panel de detalles, como actividad del cliente y comprobaciones del cliente.  

##  <a name="a-namebkmkallstatusa-monitor-the-status-of-all-clients"></a><a name="bkmk_allStatus"></a> Supervisión del estado de todos los clientes  

1.  En la consola de Configuration Manager, haga clic en **Supervisión** > **Estado de cliente**. En esta página de la consola, puede revisar las estadísticas generales de actividad del cliente y comprobaciones de cliente en todo el sitio.  También puede cambiar el ámbito de la información eligiendo una recopilación diferente.  

2.  Para profundizar en los detalles sobre las estadísticas notificadas, haga clic en el nombre de la información notificada (por ejemplo, **clientes activos que han pasado la comprobación de cliente o que no han obtenido resultados**) y revise la información acerca de los clientes individuales.  

3.  Haga clic en **Actividad de cliente** para ver gráficos que representan la actividad del cliente en su sitio de Configuration Manager.  

4.  Haga clic en **Comprobación de cliente** para ver gráficos que representan el estado de las comprobaciones de cliente en el sitio de Configuration Manager.  

 Puede configurar alertas para que le notifiquen cuándo los clientes comprueban los resultados o cuándo la actividad de los clientes cae por debajo de un porcentaje específico de clientes en una recopilación, o cuándo no se produce la corrección en un porcentaje específico de clientes. Para obtener más información acerca de cómo configurar el estado de cliente, consulte [How to configure client status in System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md) (Configuración del estado de cliente en System Center Configuration Manager).  

##  <a name="a-namebkmkclienthealtha-checks-and-remediations-made-by-client-check"></a><a name="BKMK_ClientHealth"></a> Comprobaciones y correcciones realizadas mediante comprobación de cliente  
 Las siguientes comprobaciones y correcciones pueden realizarse mediante la comprobación de cliente.  

|Comprobación de cliente|Acción correctiva|Más información|  
|------------------|------------------------|----------------------|  
|Comprobar que la comprobación de cliente se ha ejecutado recientemente|Ejecutar la comprobación de cliente|Comprueba que la comprobación del cliente ha ejecutado al menos una vez en los últimos tres días.|  
|Comprobar que están instalados los requisitos previos de cliente|Instalar los requisitos previos de cliente|Comprueba que están instalados los requisitos previos de cliente. Lee el archivo ccmsetup.xml en la carpeta de instalación de cliente para detectar los requisitos previos.|  
|Prueba de integridad del repositorio WMI.|Reinstalar el cliente de Configuration Manager|Comprueba que las entradas de cliente de Configuration Manager están presentes en WMI.|  
|Comprobar que el servicio de cliente se está ejecutando|Iniciar el servicio de cliente (Host de agente de SMS)|No hay información adicional|  
|Prueba de receptor de eventos WMI.|Reiniciar el servicio de cliente|Comprobar si se ha perdido el receptor de eventos WMI de Configuration Manager|  
|Comprobar que existe el servicio Instrumental de administración de Windows (WMI)|No hay corrección|No hay información adicional|  
|Comprobar que el cliente se instaló correctamente|Volver a instalar el cliente|No hay información adicional|  
|Prueba de lectura y escritura de repositorio WMI|Restablecer el repositorio WMI y volver a instalar el cliente de Configuration Manager|La corrección de esta comprobación de cliente sólo se lleva a cabo en equipos que ejecutan Windows Server 2003, Windows XP (64 bits) o versiones anteriores.|  
|Comprobar que el tipo de inicio del servicio antimalware sea automático|Restablecer el tipo de inicio de servicio a automático|No hay información adicional|  
|Comprobar que el servicio antimalware se está ejecutando|Iniciar el servicio antimalware|No hay información adicional|  
|Comprobar que el tipo de inicio del servicio Windows Update sea automático o manual|Restablecer el tipo de inicio de servicio a automático|No hay información adicional|  
|Comprobar que el tipo de inicio del servicio de cliente (Host de agente de SMS) sea automático|Restablecer el tipo de inicio de servicio a automático|No hay información adicional|  
|Comprobar que se está ejecutando el servicio Instrumental de administración de Windows (WMI).|Iniciar el servicio Instrumental de administración de Windows|No hay información adicional|  
|Comprobar que el estado de la base de datos de Microsoft SQL CE sea correcto|Reinstalar el cliente de Configuration Manager|No hay información adicional|  
|Prueba de integridad WMI de Microsoft Policy Platform|Reparar Microsoft Policy Platform|No hay información adicional|  
|Comprobar que existe el servicio Microsoft Policy Platform|Reparar Microsoft Policy Platform|No hay información adicional|  
|Verificar que el tipo de inicio del servicio Microsoft Policy Platform es manual|Restablecer el tipo de inicio de servicio a manual|No hay información adicional|  
|Comprobar que existe el Servicio de transferencia inteligente en segundo plano|No hay corrección|No hay información adicional|  
|Comprobar que el tipo de inicio del Servicio de transferencia inteligente en segundo plano sea automático o manual|Restablecer el tipo de inicio de servicio a automático|No hay información adicional|  
|Comprobar que el tipo de inicio del servicio Inspección de red sea manual|Restablecer el tipo de inicio de servicio a manual si está instalado|No hay información adicional|  
|Compruebe que el tipo de inicio del servicio Instrumental de administración de Windows (WMI) sea automático|Restablecer el tipo de inicio de servicio a automático|No hay información adicional|  
|Comprobar si el tipo de inicio del servicio de Windows Update en equipos Windows 8 es automático o manual|Restablecer el tipo de inicio de servicio a manual|No hay información adicional|  
|Compruebe que el servicio de cliente (host de agente de SMS) existe.|No hay corrección|No hay información adicional|  
|Comprobar si el tipo de inicio del servicio de control remoto de Configuration Manager es automático o manual|Restablecer el tipo de inicio de servicio a automático|No hay información adicional|  
|Comprobar que el servicio de control remoto de Configuration Manager se está ejecutando|Iniciar el servicio de control remoto|No hay información adicional|  
|Comprobar que el estado del proveedor WMI de cliente es correcto|Reiniciar el servicio Instrumental de administración de Windows|La corrección de esta comprobación de cliente solo se lleva a cabo en equipos que ejecutan Windows Server 2003, Windows XP (64 bits) o versiones anteriores.|  
|Comprobar que el servicio de proxy de reactivación (proxy de reactivación de Configuration Manager) se está ejecutando|Iniciar el servicio de proxy de reactivación de Configuration Manager|Esta comprobación de cliente solo se realiza si la opción **Administración de energía**: **Habilitar proxy de reactivación** está establecida en **Sí** en los sistemas operativos de cliente admitidos.|  
|Comprobar que el tipo de inicio del servicio de proxy de reactivación (proxy de reactivación de Configuration Manager) es automático|Restablecer el tipo de inicio del servicio de proxy de reactivación de Configuration Manager como automático|Esta comprobación de cliente solo se realiza si la opción **Administración de energía**: **Habilitar proxy de reactivación** está establecida en **Sí** en los sistemas operativos de cliente admitidos.|  



<!--HONumber=Nov16_HO1-->


