---
title: Supervisar clientes
titleSuffix: Configuration Manager
description: Obtenga información detallada acerca de cómo supervisar clientes en Configuration Manager
ms.date: 05/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55fd698ac5213a3b11b207d0625d953f687e319f
ms.sourcegitcommit: 65753c51fbf596f233fc75a5462ea4a44005c70b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/03/2019
ms.locfileid: "66463033"
---
# <a name="how-to-monitor-clients-in-configuration-manager"></a>Supervisión de clientes en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Una vez que instale el cliente de Configuration Manager en los dispositivos Windows de su sitio, supervise su estado y la actividad en la consola de Configuration Manager.  


## <a name="bkmk_about"></a> Acerca del estado de cliente

Configuration Manager proporciona los siguientes tipos de información como estado de cliente:  

- **Estado de conexión de clientes**: El sitio considera que un dispositivo está **en línea** si está conectado a su punto de administración asignado. Para indicar que el cliente está en línea, envía mensajes de estilo ping al punto de administración. Si el punto de administración no recibe un mensaje después de cinco minutos, el sitio considera al cliente **sin conexión**.  

- **Actividad de cliente**: El sitio considera que el cliente está **activo** si se ha comunicado con Configuration Manager en los últimos siete días. El sitio considera que el cliente está **inactivo** si no se ha solicitado ni realizado las siguientes acciones en siete días:  

    - Solicitud de actualización de directiva  
    - Envío de mensaje de latido  
    - Envío de inventario de hardware  

- **Comprobación de cliente**: El estado de la evaluación periódica que el cliente de Configuration Manager ejecuta en el dispositivo. La evaluación comprueba el dispositivo y puede corregir algunos de los problemas que encuentre. Para obtener más información, vea [Comprobaciones del estado del cliente](#BKMK_ClientHealth).  

     En los dispositivos que ejecutan Windows 7, la comprobación de cliente se ejecuta como una tarea programada. En las versiones de sistemas operativos posteriores, la comprobación de cliente se ejecuta automáticamente en la ventana de mantenimiento de Windows.  

     Puede configurar la corrección para que no se ejecute en dispositivos específicos, por ejemplo, un servidor crítico del negocio. Si hay elementos adicionales que desee a evaluar, utilice la configuración de cumplimiento de Configuration Manager para supervisar las configuraciones adicionales. Para obtener más información sobre la configuración de cumplimiento, consulte [Planear y configurar la configuración de cumplimiento](/sccm/compliance/plan-design/plan-for-and-configure-compliance-settings).  

- **Dado de baja**: El sitio ha marcado el registro del dispositivo para su eliminación. Este comportamiento puede ocurrir cuando se asigna un nuevo registro para el mismo dispositivo al mismo sitio primario o a uno diferente en una jerarquía. El sitio elimina estos dispositivos la próxima vez que ejecute la tarea de mantenimiento **Eliminar datos de detección antiguos**.<!-- SCCMDocs issue #1418 -->  

- **Obsoleto**: El sitio ha detectado un nuevo registro de dispositivo con el mismo identificador de hardware, por lo que marca el registro anterior como obsoleto. Los informes no cuentan los registros obsoletos del mismo dispositivo varias veces. Puede seguir destinando directivas a dispositivos obsoletos. Si el sitio no recibe un latido para un registro obsoleto después de 90 días de inactividad, quita el dispositivo obsoleto cuando se ejecuta la tarea de mantenimiento **Eliminar datos obsoletos de detección de cliente**.


## <a name="bkmk_indStatus"></a> Supervisión de clientes individuales

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**. Seleccione el nodo **Dispositivos** o elija una recopilación en **Recopilaciones de dispositivos**.  

    Los iconos al principio de cada fila indican el estado de conexión del dispositivo:  

    |||  
    |-|-|  
    |![icono de estado conectado para los clientes](../../../core/clients/manage/media/online-status-icon.png)|El dispositivo está conectado|  
    |![icono de estado desconectado para los clientes](../../../core/clients/manage/media/offline-status-icon.png)|El dispositivo está desconectado|  
    |![icono de estado desconocido para los clientes](../../../core/clients/manage/media/unknown-status-icon.png)|Se desconoce el estado de conexión|  
    |![cliente no instalado](../../../core/clients/manage/media/client-not-installed.png)|El cliente no está instalado en el dispositivo|  

2. Para obtener el estado en línea más detallado, agregue la información del estado de conexión del cliente a la vista del dispositivo. Haga clic derecho en el encabezado de columna y seleccione los campos del estado de conexión que desea agregar:

    - **Estado de conexión del dispositivo**: Indica si el cliente está actualmente conectado o no. (Esta es la misma información proporcionada por los iconos).  

    - **Última hora en línea**: Indica cuándo cambió el estado de conexión del cliente a conectado.  

    - **Última hora sin conexión** indica cuándo cambió el estado a sin conexión  

3. Seleccione un cliente individual en el panel de lista para ver más estado en el panel de detalles. Esta información incluye la actividad y el estado de comprobación del cliente.  


## <a name="bkmk_allStatus"></a> Supervisión del estado de todos los clientes

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y seleccione el nodo **Estado del cliente**. Revise las estadísticas generales de actividad del cliente y comprobaciones de cliente en todo el sitio. Cambie el ámbito de la información eligiendo una recopilación diferente.  

2. Para profundizar en los detalles sobre las estadísticas notificadas, elija el nombre de la información notificada. Por ejemplo, **clientes activos que han pasado la comprobación de cliente o que no han obtenido resultados**. A continuación, revise la información acerca de los clientes individuales.  

3. Seleccione **Actividad de cliente** para ver gráficos que representan la actividad del cliente en su sitio de Configuration Manager.  

4. Seleccione **Comprobación de cliente** para ver gráficos que representan el estado de las comprobaciones de cliente en el sitio de Configuration Manager.  

    Configure alertas que le avisen cuando la actividad del cliente o los resultados de la comprobación del cliente caigan por debajo de un porcentaje especificado. El sitio también le alerta cuando se produce un error de corrección en un porcentaje específico de clientes. Para obtener más información, vea [Cómo configurar el estado de cliente](/sccm/core/clients/deploy/configure-client-status).  


## <a name="BKMK_ClientHealth"></a> Comprobaciones del estado del cliente

La comprobación del cliente ejecuta las siguientes comprobaciones y correcciones:  

|Comprobación de cliente|Acción correctiva|Más información|  
|------------------|------------------------|----------------------|  
|Comprobar que la comprobación de cliente se ha ejecutado recientemente|Ejecutar la comprobación de cliente|Comprueba que la comprobación del cliente ha ejecutado al menos una vez en los últimos tres días.|  
|Comprobar que están instalados los requisitos previos de cliente|Instalar los requisitos previos de cliente|Comprueba que están instalados los requisitos previos de cliente. Lee el archivo ccmsetup.xml en la carpeta de instalación de cliente para detectar los requisitos previos.|  
|Prueba de integridad del repositorio WMI.|Reinstalar el cliente de Configuration Manager|Comprueba que las entradas de cliente de Configuration Manager están presentes en WMI.|  
|Comprobar que el servicio de cliente se está ejecutando|Iniciar el servicio de cliente (Host de agente de SMS)|No hay información adicional|  
|Prueba de receptor de eventos WMI.|Reiniciar el servicio de cliente|Comprobar si se ha perdido el receptor de eventos WMI de Configuration Manager|  
|Comprobar que existe el servicio Instrumental de administración de Windows (WMI)|No hay corrección|No hay información adicional|  
|Comprobar que el cliente se instaló correctamente|Volver a instalar el cliente|No hay información adicional|  
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
|Comprobar si el tipo de inicio del servicio de Windows Update en dispositivos Windows 8 es automático o manual|Restablecer el tipo de inicio de servicio a manual|No hay información adicional|  
|Compruebe que el servicio de cliente (host de agente de SMS) existe.|No hay corrección|No hay información adicional|  
|Comprobar si el tipo de inicio del servicio de control remoto de Configuration Manager es automático o manual|Restablecer el tipo de inicio de servicio a automático|No hay información adicional|  
|Comprobar que el servicio de control remoto de Configuration Manager se está ejecutando|Iniciar el servicio de control remoto|No hay información adicional|  
|Comprobar que el servicio de proxy de reactivación (proxy de reactivación de Configuration Manager) se está ejecutando|Iniciar el servicio de proxy de reactivación de Configuration Manager|Esta comprobación de cliente se realiza solo si la opción de cliente **Administración de energía**: **Habilitar proxy de reactivación** se ha configurado como **Sí** en los sistemas operativos de cliente admitidos.|  
|Comprobar que el tipo de inicio del servicio de proxy de reactivación (proxy de reactivación de Configuration Manager) es automático|Restablecer el tipo de inicio del servicio de proxy de reactivación de Configuration Manager como automático|Esta comprobación de cliente se realiza solo si la opción de cliente **Administración de energía**: **Habilitar proxy de reactivación** se ha configurado como **Sí** en los sistemas operativos de cliente admitidos.|  


<!-- 
5/31/2019 ACz: need to confirm if these checks are still applicable
|WMI repository read and write test|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->


## <a name="client-deployment-log-files"></a>Archivos de registro de implementación de cliente

Para obtener información acerca de los archivos de registro utilizados por la implementación del cliente y las operaciones de administración, consulte los [archivos de registro](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs).
