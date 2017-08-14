---
title: Supervisar clientes Linux y UNIX en Configuration Manager | Microsoft Docs
description: Superviser clientes en servidores de Linux y UNIX en System Center Configuration Manager.
ms.custom: na
ms.date: 08/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: afe0ecc4230733fa76e41bf08df5ccfb221da7c8
ms.openlocfilehash: 62843bd544217734c4566d656a7c3a35bd5613cb
ms.contentlocale: es-es
ms.lasthandoff: 08/04/2017

---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Cómo supervisar clientes para servidores Linux y UNIX en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La información de los servidores Linux y UNIX se puede ver en la consola de System Center Configuration Manager mediante los mismos métodos que se usan para ver la información de clientes basados en Windows.  

 La información que se puede ver incluye lo siguiente:  

-   Detalles de estado de los clientes, en los paneles de la consola de Configuration Manager  

-   Detalles sobre los clientes en los informes predeterminados de Configuration Manager  

-   Detalles de inventario en el Explorador de recursos  

 En las siguientes secciones se describe cómo obtener estos detalles del Explorador de recursos y de los informes.  

##  <a name="BKMK_UseResourceExpforLnU"></a> Usar el Explorador de recursos para ver el inventario de servidores Linux y UNIX  

 Una vez que un cliente de Configuration Manager envía el inventario de hardware al sitio de Configuration Manager, se puede usar el Explorador de recursos para ver esta información. El cliente de Configuration Manager para Linux y UNIX no agrega nuevas clases ni vistas de inventario en el Explorador de recursos. Los datos del inventario de Linux y UNIX se asigna a las clases WMI existentes. Con el Explorador de recursos, es posible ver los detalles de inventario de los servidores Linux y UNIX en la clasificación basada en Windows.  

 Por ejemplo, puede recopilar la lista de todos los programas instalados de forma nativa que se encuentran en los servidores Linux y UNIX. Los ejemplos de programas instalados de forma nativa incluyen **.rpms** en Linux o **.pkgs** en Solaris. Después de que un cliente Linux o UNIX envía el inventario, se puede ver la lista de todos los programas de Linux o UNIX instalados de forma nativa mediante el Explorador de recursos en la consola de Configuration Manager.  

 Para obtener información sobre cómo utilizar el Explorador de recursos, consulte [How to use Resource Explorer to view hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) (Uso del Explorador de recursos para ver el inventario de hardware en System Center Configuration Manager).  

##  <a name="BKMK_UseReportsforLnU"></a> Usar informes para ver la información de servidores Linux y UNIX  
 Los informes de Configuration Manager incluyen información de servidores de Linux y UNIX, así como información de equipos basados en Windows. No se necesitan configuraciones adicionales para integrar los datos de Linux y UNIX en los informes.  

 Por ejemplo, si ejecuta el informe denominado Recuento de versiones de sistema operativo, se muestra la lista de los distintos sistemas operativos y el número de clientes que ejecutan cada sistema operativo. El informe se basa en la información de inventario de hardware enviada por los diferentes clientes de Configuration Manager que se ejecutan en los distintos sistemas operativos.  

 También se pueden crear informes personalizados específicos para datos de servidores Linux y UNIX. La propiedad **Título** de la clase de inventario de hardware **Sistema operativo** es un atributo útil que puede usarse para identificar sistemas operativos específicos en la consulta del informe.  

 Para obtener más información sobre informes en Configuration Manager, vea [Reporting in System Center Configuration Manager](../../../core/servers/manage/reporting.md) (Generación de informes en System Center Configuration Manager).  

