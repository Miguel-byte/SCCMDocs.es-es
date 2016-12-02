---
title: "Configurar clientes para buscar la publicación en DNS de puntos de administración | System Center Configuration Manager"
description: "Configure los equipos cliente para buscar puntos de administración mediante la publicación en DNS en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
caps.latest.revision: 6
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: c6470a39519bc25357ba5d9721afe9c39a28c348


---
# <a name="how-to-configure-client-computers-to-find-management-points-by-using-dns-publishing-in-system-center-configuration-manager"></a>Configurar los equipos cliente para buscar los puntos de administración mediante el uso de la publicación en DNS en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los clientes de System Center Configuration Manager deben encontrar un punto de administración para completar la asignación de sitios y como proceso continuo para seguir siendo administrados. Los Servicios de dominio de Active Directory proporcionan el método más seguro para que los clientes en la intranet encuentren puntos de administración. Sin embargo, si los clientes no pueden usar este método de ubicación de servicio (por ejemplo, no han extendido el esquema de Active Directory o son parte de un grupo de trabajo) use la publicación en DNS con método de ubicación de servicio alternativo.  

> [!NOTE]  
>  Al instalar el cliente para Linux y UNIX, debe especificar un punto de administración como punto inicial de contacto. Para más información sobre cómo instalar el cliente para Linux y UNIX, vea [How to deploy clients to UNIX and Linux servers in System Center Configuration Manager (Cómo implementar clientes en servidores UNIX y Linux en System Center Configuration Manager)](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

 Antes de utilizar la publicación en DNS para puntos de administración, asegúrese de que los servidores DNS en la intranet tienen registros de recurso de ubicación de servicio (SRV RR) y los correspondientes registros de recurso de host (A o AAA) para los puntos de administración del sitio. Los registros de recurso de ubicación de servicio pueden ser creados automáticamente por Configuration Manager o, de manera manual, por el administrador de DNS que crea los registros en DNS.  

 Para más información sobre la publicación en DNS como método de ubicación de servicio para clientes de Configuration Manager, vea [Understand how clients find site resources and services for System Center Configuration Manager (Comprender cómo los clientes buscan servicios y recursos de sitio para System Center Configuration Manager)](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

 De forma predeterminada, los clientes buscan DNS para puntos de administración en su dominio DNS. Pero si no se publican puntos de administración en el dominio de los clientes, debe configurar manualmente los clientes con un sufijo DNS del punto de administración. Puede configurar este sufijo DNS en clientes durante o después de la instalación del cliente:  

-   Para configurar clientes para un sufijo de punto de administración durante la instalación del cliente, configure las propiedades de Client.msi de CCMSetup.  

-   Para configurar clientes para un sufijo de punto de administración tras la instalación del cliente, en el Panel de control, configure las **Propiedades de Configuration Manager**.  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>Para configurar clientes para un sufijo de punto de administración durante la instalación del cliente  

-   Instale el cliente con la siguiente propiedad de Client.msi de CCMSetup:  

    -   **DNSSUFFIX=** *&lt;dominio del punto de administración\>*  

         Si el sitio tiene varios puntos de administración en más de un dominio, especifique un solo dominio. Cuando los clientes se conectan a un punto de administración en este dominio, descargarán una lista de puntos de administración disponibles que incluirá los puntos de administración de los otros dominios.  

     Para más información sobre las propiedades de línea de comandos de CCMSetup, vea [Acerca de las propiedades de instalación de cliente de Configuración Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>Para configurar clientes para un sufijo de punto de administración después de la instalación del cliente  

1.  En el Panel de Control del equipo cliente, vaya a **Configuration Manager**y, a continuación, haga doble clic en **Propiedades**.  

2.  En la pestaña **Sitio** , especifique el sufijo DNS de un punto de administración y, a continuación, haga clic en **Aceptar**.  

     Si el sitio tiene varios puntos de administración en más de un dominio, especifique un solo dominio. Cuando los clientes se conectan a un punto de administración en este dominio, descargarán una lista de puntos de administración disponibles que incluirá los puntos de administración de los otros dominios.



<!--HONumber=Nov16_HO1-->

