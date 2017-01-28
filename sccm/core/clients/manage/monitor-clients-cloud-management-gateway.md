---
title: "Supervisar la puerta de enlace de administración en la nube en Configuration Manager | Microsoft Docs"
description: 
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: ef12c9b966a1b83b61243311b30e1a925c20d2e3
ms.openlocfilehash: 4475205c37c20631a189e0c315dc48e288c15ba6

---

# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Supervisar la puerta de enlace de administración en la nube en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

A partir de la versión 1610, después de que se ejecute el servicio de puerta de enlace de administración en la nube y los clientes se conecten a través de él, puede supervisar clientes y tráfico de red para asegurarse de que sabe cómo está funcionando el servicio.

## <a name="monitor-clients"></a>Supervisar clientes

Los clientes conectados mediante el servicio de puerta de enlace de administración en la nube aparecen en la consola de Configuration Manager de la misma manera que los clientes locales. Para obtener más información, consulte [Supervisar clientes en System Center Configuration Manager](monitor-clients.md).

## <a name="monitor-traffic-in-the-console"></a>Supervisar el tráfico en la consola

Puede supervisar el tráfico en la puerta de enlace de administración en la nube con la consola de Configuration Manager:

1. Vaya a **Administración > Cloud Services > Puerta de enlace de administración en la nube**.

2. Seleccione el servicio de puerta de enlace de administración en la nube en el panel de lista.

3. Vea la información de tráfico en el panel de detalles para el rol de conexión de la puerta de enlace de administración en la nube y los roles de sistema de sitio a los que se conecta.

## <a name="set-up-outbound-traffic-alerts"></a>Configurar alertas de tráfico de salida

Las alertas de tráfico de salida le ayudarán a saber el momento en el que el tráfico se acerca a un nivel de umbral de 14 días (2 semanas). Se le proporciona la opción de configurar alertas de tráfico cuando crea el servicio de puerta de enlace de administración en la nube. Si omite esa parte, todavía puede configurar las alertas después de que se ejecute el servicio. Y, además, puede ajustar la configuración de alertas en cualquier momento.

1. Vaya a **Administración > Cloud Services > Puerta de enlace de administración en la nube**.

2. Haga clic con el botón derecho en el servicio de puerta de enlace de administración en la nube en el panel de lista y pulse **Propiedades**.

3. Haga clic en la pestaña Alertas y pulse activar (o desactivar) el umbral y las alertas. Después, especifique el umbral de 14 días (en GB) y los porcentajes del umbral para generar los diferentes niveles de alerta.

4. Haga clic en **Aceptar** cuando haya terminado.

## <a name="monitor-logs"></a>Supervisar los registros

El servicio de puerta de enlace de administración en la nube genera entradas en los siguientes archivos de registro:

-   **Cloudmgr.log**: contiene entradas para la implementación del servicio de puerta de enlace de administración en la nube, el estado del servicio en curso y datos de uso asociados con el servicio.

-   **SMS\_Cloud\_ProxyConnector.log**: contiene entradas para la configuración de conexiones entre el servicio de puerta de enlace de administración en la nube y el punto de conexión de la puerta de enlace de administración en la nube.

Para obtener más información, consulte [Archivos de registro en System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files).



<!--HONumber=Jan17_HO4-->

