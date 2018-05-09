---
title: Supervisión de la puerta de enlace de administración de nube
titleSuffix: Configuration Manager
description: Supervise los clientes y el tráfico de red a través de Cloud Management Gateway (CMG).
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a4ecbeb2484297160797b7b5632c86cee4ff1122
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Supervisar la puerta de enlace de administración en la nube en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Después de que se ejecute la instancia de Cloud Management Gateway y los clientes se conecten a través de ella, se pueden supervisar los clientes y el tráfico de red para asegurarse de que se sabe cómo está funcionando el servicio.



## <a name="monitor-clients"></a>Supervisar clientes

Los clientes conectados mediante la instancia de Cloud Management Gateway aparecen en la consola de Configuration Manager de la misma manera que los clientes locales. Para obtener más información, consulte [Supervisar clientes en System Center Configuration Manager](/sccm/core/clients/manage/monitor-clients).



## <a name="monitor-traffic-in-the-console"></a>Supervisar el tráfico en la consola

Puede supervisar el tráfico en la instancia de Cloud Management Gateway con la consola de Configuration Manager:

1. Vaya a **Administración > Cloud Services > Puerta de enlace de administración en la nube**.

2. Seleccione la instancia de Cloud Management Gateway en el panel de lista.

3. Vea la información de tráfico en el panel de detalles para el punto de conexión de la instancia de Cloud Management Gateway y los roles de sistema de sitio a los que se conecta.



## <a name="set-up-outbound-traffic-alerts"></a>Configurar alertas de tráfico de salida

Las alertas de tráfico de salida ayudan a saber el momento en el que el tráfico se acerca a un nivel de umbral de 14 días. Al crear la instancia de Cloud Management Gateway, se pueden configurar alertas de tráfico. Si omite esa parte, todavía puede configurar las alertas después de que se ejecute el servicio. Ajuste la configuración de alertas en cualquier momento.

1. Vaya a **Administración > Cloud Services > Puerta de enlace de administración en la nube**.

2. Haga clic con el botón derecho en la instancia de Cloud Management Gateway en el panel de lista y seleccione **Propiedades**.

3. Haga clic en la pestaña **Alertas**. Habilite el umbral y las alertas. Especifique el umbral de datos de 14 días en gigabytes (GB). Especifique también el porcentaje de umbral para elevar los distintos niveles de alerta.

4. Haga clic en **Aceptar** cuando haya terminado.



## <a name="monitor-logs"></a>Supervisar los registros

La instancia de Cloud Management Gateway genera entradas en una serie de archivos de registro. Para obtener más información, consulte [Archivos de registro en System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).
