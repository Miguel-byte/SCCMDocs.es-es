---
title: "Probar las actualizaciones de cliente en una recopilación de preproducción | System Center Configuration Manager"
description: "Pruebe las actualizaciones de cliente en una recopilación de preproducción en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
caps.latest.revision: 10
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1e648b94a475bda2b35d69ff0a8863d2e0d248fb


---
# <a name="how-to-test-client-upgrades-in-a-preproduction-collection-in-system-center-configuration-manager"></a>Cómo probar las actualizaciones de cliente en una recopilación de preproducción en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Para actualizar el cliente de Configuration Manager en equipos y dispositivos Windows, puede probar una nueva versión de cliente en una recopilación de preproducción antes de actualizar el resto del sitio.  Al hacerlo, solo los dispositivos que forman parte de la recopilación de preproducción se actualizan al nuevo cliente. Una vez que haya tenido la oportunidad de probar el cliente en esta recopilación de preproducción, puede promover el cliente, lo que hace que la nueva versión del software cliente esté disponible para el resto del sitio.  

 Hay 3 pasos básicos para probar los clientes en preproducción  

1.  [Para configurar las actualizaciones automáticas de cliente para que usen una recopilación de preproducción](#BKMK_config) para usar una recopilación de preproducción.  

2.  [Para instalar una actualización de Configuration Manager que incluye una nueva versión del cliente](#BKMK_install) que incluye una nueva versión del cliente. Durante la instalación, especifique que se debe usar una recopilación de preproducción para el nuevo software cliente.  

3.  [Para promover el nuevo cliente a producción](#BKMK_promote) después de haberlo probado suficientemente en preproducción.  

> [!TIP]  
>  Si va a actualizar su infraestructura desde una versión anterior de Configuration Manager \(como Configuration Manager 2007 o System Center 2012 Configuration Manager\), se recomienda que realice las actualizaciones de servidor, incluida la instalación de todas las actualizaciones de la rama actual, antes de actualizar los clientes Configuration Manager.   La última actualización de la rama actual contiene la versión más reciente del cliente, por lo que es mejor realizar las actualizaciones de cliente después de instalar todas las actualizaciones de Configuration Manager que desea utilizar.  

##  <a name="a-namebkmkconfiga-to-configure-automatic-client-upgrades-to-use-a-preproduction-collection"></a><a name="BKMK_config"></a> Para configurar las actualizaciones automáticas de cliente para que usen una recopilación de preproducción  

1. Configure una recopilación que contenga los equipos en los que quiere implementar el cliente de preproducción. Para obtener más información sobre cómo realizar este paso, consulte [Cómo crear recopilaciones](..\collections\create-collections.md).

> [!NOTE]
> No incluya equipos de grupo de trabajo en las recopilaciones de preproducción. Los equipos de grupo de trabajo no pueden usar la autenticación requerida para que el punto de distribución obtenga acceso al paquete de cliente de preproducción.   

1.  En la consola de Configuration Manager, abra **Administración** > **Configuración del sitio** > **Sitios** y haga clic en **Configuración de jerarquía**.  

     En la pestaña **Actualización de cliente** de las **Propiedades de configuración de la jerarquía**:  

    -   Seleccione **Actualizar todos los clientes de la colección de preproducción automáticamente mediante el cliente de preproducción**.  

    -   Escriba el nombre de una colección para usarla como colección de preproducción.  

2.  Haga clic en **Aceptar** para guardar la configuración de la actualización de cliente.  

##  <a name="a-namebkmkinstalla-to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a><a name="BKMK_install"></a> Para instalar una actualización de Configuration Manager que incluye una nueva versión del cliente  

1.  En la consola de Configuration Manager, abra **Administración** > **Servicios en la nube** > **Actualizaciones y servicios**, seleccione una actualización **Disponible** y después haga clic en **Instalar el paquete de actualización**  

     Para obtener más información sobre cómo instalar actualizaciones, consulte [Actualizaciones para System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

2.  Durante la instalación de la actualización, en la página **Client Options** del asistente, seleccione **Test in pre-production collection**y haga clic en **Siguiente**.  

3.  Complete el resto del asistente e instale el paquete de actualización.  

     Una vez que se complete el Asistente, los clientes de la recopilación de preproducción empezarán a implementar el cliente actualizado. Puede supervisar la implementación de clientes actualizados yendo a **Supervisión** > **Estado de cliente** > **Implementación de cliente de preproducción**. Para obtener más información, consulte [Supervisar el estado de implementación de cliente en System Center Configuration Manager](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > El estado de implementación en equipos que hospedan los roles de sistema de sitio en una recopilación de preproducción puede aparecer registrado como **No iniciado** incluso cuando el cliente se ha implementado correctamente. Cuando se promueve el cliente a la producción, el estado de implementación se registrará correctamente.

##  <a name="a-namebkmkpromotea-to-promote-the-new-client-to-production"></a><a name="BKMK_promote"></a> Para promover el nuevo cliente a producción  

1.  En la consola de Configuration Manager, abra **Administración** > **Servicios en la nube** > **Actualizaciones y mantenimiento** y haga clic en **Promover el cliente de preproducción**.

    > [!TIP]
    > El botón **Promover el cliente de preproducción** también está disponible cuando se están supervisando las implementaciones de cliente en la consola en **Supervisión** > **Estado de cliente** > **Implementación del cliente de preproducción**.

2.  En el cuadro de diálogo, revise las versiones de cliente de preproducción y de producción, asegúrese de que está especificada la recopilación de preproducción correcta y luego haga clic en **Promover**. En el cuadro de diálogo Confirmación, haga clic en **Sí**.  

3.  Después de cerrar el cuadro de diálogo, la versión del cliente actualizado reemplazará a la versión del cliente actual que se usa en la jerarquía. A continuación, puede actualizar los clientes de todo el sitio. Para obtener más información, consulte [Actualizar clientes de equipos Windows con System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  



<!--HONumber=Nov16_HO1-->


