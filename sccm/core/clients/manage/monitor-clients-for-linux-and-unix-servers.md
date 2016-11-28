---
title: "Supervisión de clientes | Linux UNIX |System Center Configuration Manager"
description: Superviser clientes en servidores de Linux y UNIX en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
caps.latest.revision: 6
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 707cb13bcb62848eb42ca824137a645dfd2f9d82


---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Cómo supervisar clientes para servidores Linux y UNIX en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La información de los servidores Linux y UNIX se puede ver en la consola de System Center Configuration Manager mediante los mismos métodos que se usan para ver la información de clientes basados en Windows.  

 La información que se puede ver incluye lo siguiente:  

-   Detalles de estado de los clientes, en los paneles de la consola de Configuration Manager  

-   Detalles sobre los clientes en los informes predeterminados de Configuration Manager  

-   Detalles de inventario en el Explorador de recursos  

 Las secciones siguientes proporcionan información sobre cómo usar los informes y el Explorador de recursos para ver los detalles de los servidores Linux y UNIX.  

##  <a name="a-namebkmkuseresourceexpforlnua-how-to-use-resource-explorer-to-view-inventory-for-linux-and-unix-servers"></a><a name="BKMK_UseResourceExpforLnU"></a> Uso del Explorador de recursos para ver el inventario de servidores de Linux y UNIX  
 El Explorador de recursos permite ver los detalles del hardware y el software instalados en los servidores Linux y UNIX.  

 Una vez que un cliente de Configuration Manager envía el inventario de hardware al sitio de Configuration Manager, se puede usar el Explorador de recursos para ver esta información. El cliente de Configuration Manager para Linux y UNIX no agrega nuevas clases ni vistas de inventario en el Explorador de recursos. Los datos del inventario de Linux y UNIX se asigna a las clases WMI existentes. Con el Explorador de recursos, es posible ver los detalles de inventario de los servidores Linux y UNIX en la clasificación basada en Windows.  

 Por ejemplo, puede recopilar la lista de todos los programas instalados de forma nativa que se encuentran en los servidores Linux y UNIX. Los ejemplos de programas instalados de forma nativa incluyen **.rpms** en Linux o **.pkgs** en Solaris. Después de que un cliente Linux o UNIX envía el inventario, se puede ver la lista de todos los programas de Linux o UNIX instalados de forma nativa mediante el Explorador de recursos en la consola de Configuration Manager.  

 Para obtener información sobre cómo utilizar el Explorador de recursos, consulte [How to use Resource Explorer to view hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) (Uso del Explorador de recursos para ver el inventario de hardware en System Center Configuration Manager).  

##  <a name="a-namebkmkusereportsforlnua-how-to-use-reports-to-view-information-for-linux-and-unix-servers"></a><a name="BKMK_UseReportsforLnU"></a> Uso de informes para ver la información de servidores de Linux y UNIX  
 Los informes de Configuration Manager incluyen información de servidores de Linux y UNIX, así como información de equipos basados en Windows. No se necesitan configuraciones adicionales para integrar los datos de Linux y UNIX en los informes.  

 Por ejemplo, si ejecuta el informe denominado Recuento de versiones de sistema operativo, se muestra la lista de los distintos sistemas operativos y el número de clientes que ejecutan cada sistema operativo. El informe se basa en la información de inventario de hardware enviada por los diferentes clientes de Configuration Manager que se ejecutan en los distintos sistemas operativos.  

 También se pueden crear informes personalizados específicos para datos de servidores Linux y UNIX. La propiedad **Título** de la clase de inventario de hardware **Sistema operativo** es un atributo útil que puede usarse para identificar sistemas operativos específicos en la consulta del informe.  

 Para obtener más información sobre informes en Configuration Manager, vea [Reporting in System Center Configuration Manager](../../../core/servers/manage/reporting.md) (Generación de informes en System Center Configuration Manager).  



<!--HONumber=Nov16_HO1-->


