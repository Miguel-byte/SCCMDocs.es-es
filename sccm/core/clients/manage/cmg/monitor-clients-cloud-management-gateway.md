---
title: Supervisión de la puerta de enlace de administración de nube
titleSuffix: Configuration Manager
description: Supervise los clientes y el tráfico de red a través de Cloud Management Gateway (CMG).
ms.date: 09/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ef27c67b9b17f41fbe71d57fdea9552b7dff9f7
ms.sourcegitcommit: 2badee2b63ae63687795250e298f463474063100
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/14/2018
ms.locfileid: "45601048"
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Supervisar la puerta de enlace de administración en la nube en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Después de que se ejecute la instancia de Cloud Management Gateway (CMG) y los clientes se conecten a través de ella, se pueden supervisar los clientes y el tráfico de red para asegurarse de que se sabe cómo está funcionando el servicio.



## <a name="monitor-clients"></a>Supervisar clientes

Los clientes conectados mediante la instancia de CMG aparecen en la consola de Configuration Manager de la misma manera que los clientes locales. Para obtener más información, consulte [Supervisar clientes en System Center Configuration Manager](/sccm/core/clients/manage/monitor-clients).



## <a name="monitor-traffic-in-the-console"></a>Supervisar el tráfico en la consola

Puede supervisar el tráfico en la instancia de CMG con la consola de Configuration Manager:

1. Vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo **Cloud Management Gateway**.  

2. Seleccione CMG en el panel de lista.  

3. Vea la información de tráfico en el panel de detalles para el punto de conexión de la instancia de CMG y los roles de sistema de sitio a los que se conecta.  



## <a name="set-up-outbound-traffic-alerts"></a>Configurar alertas de tráfico de salida

Las alertas de tráfico de salida ayudan a saber el momento en el que el tráfico se acerca a un nivel de umbral de 14 días. Al crear la instancia de CMG, se pueden configurar alertas de tráfico. Si omite esa parte, todavía puede configurar las alertas después de que se ejecute el servicio. Ajuste la configuración de alertas en cualquier momento.

1. Vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo **Cloud Management Gateway**.  

2. Seleccione la instancia de CMG en el panel de lista y después seleccione **Propiedades** en la cinta de opciones.  

3. Vaya a la pestaña **Alertas** para habilitar el umbral y las alertas. Especifique el umbral de datos de 14 días en gigabytes (GB). Especifique también el porcentaje de umbral para elevar los distintos niveles de alerta.  

4. Cuando haya terminado, seleccione **Aceptar**.  



## <a name="monitor-logs"></a>Supervisar los registros

La instancia de CMG genera entradas en una serie de archivos de registro. Para obtener más información, consulte [Archivos de registro en System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="cloud-management-dashboard"></a>Panel de administración en la nube
<!--1358461--> A partir de la versión 1806, el panel de administración en la nube proporciona una vista centralizada para el uso de CMG. Cuando el sitio está incorporado a [servicios de Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para la administración en la nube, también muestra los datos sobre los usuarios en la nube y los dispositivos.  

La captura de pantalla siguiente es una parte del panel de administración en la nube que muestra dos de los iconos disponibles:  
![Iconos del panel de administración: Tráfico de CMG y Clientes en línea actuales](media/1358461-cmg-dashboard.png)

En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**. Seleccione el nodo **Administración en la nube** y vea los iconos del panel.  



## <a name="connection-analyzer"></a>Analizador de conexión

A partir de la versión 1806, use el analizador de conexión de CMG para la comprobación en tiempo real que ayuda a solucionar problemas. La utilidad en la consola comprueba el estado actual del servicio y el canal de comunicación a través del punto de conexión de CMG a todos los puntos de administración que permiten el tráfico CMG.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Cloud Services** y seleccione el nodo **Cloud Management Gateway**.  

2. Seleccione la instancia de CMG de destino y luego seleccione **Analizador de conexión** en la cinta.  

3. En la ventana del analizador de conexión de CMG, seleccione una de las siguientes opciones para autenticarse con el servicio:  

     1. **Usuario de Azure AD**: use esta opción para simular la comunicación de la misma manera que una identidad de usuario basado en la nube que ha iniciado sesión en un dispositivo con Windows 10 unido a Azure AD. Haga clic en **Iniciar sesión** para escribir las credenciales de forma segura para esta cuenta de usuario de Azure AD.  

     2. **Certificado de cliente**: utilice esta opción para simular la comunicación de la misma manera que un cliente de Configuration Manager con un [certificado de autenticación del cliente](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate).  

4. Seleccione **Iniciar** para iniciar el análisis. Los resultados se muestran en la ventana del analizador. Seleccione una entrada para ver más detalles en el campo Descripción.  

