---
title: "Probar la colección de preproducción de actualizaciones de cliente | Microsoft Docs"
description: "Pruebe las actualizaciones de cliente en una recopilación de preproducción en System Center Configuration Manager."
ms.custom: na
ms.date: 12/04/2016
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
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 17b36eae97272c408fce20e1f88812dafc984773
ms.openlocfilehash: bfc53760572e71814ebf0e38ea24c5c4684619ee


---
# <a name="how-to-test-client-upgrades-in-a-preproduction-collection-in-system-center-configuration-manager"></a>Cómo probar las actualizaciones de cliente en una recopilación de preproducción en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede probar una nueva versión de cliente de Configuration Manager en una colección de preproducción antes de actualizar el resto del sitio con ella.  Al hacerlo, solo se actualizan los dispositivos que forman parte de la recopilación de prueba. Una vez que haya tenido la oportunidad de probar el cliente, puede promover el cliente, lo que hace que la nueva versión del software cliente esté disponible para el resto del sitio.

> [!NOTE]
> Para promover un cliente de prueba a producción, debe iniciar sesión como un usuario con el rol de seguridad de **Administrador total** y un ámbito de seguridad de **Todo**. Para obtener más información, vea [Aspectos básicos de la administración basada en roles](/sccm/core/understand/fundamentals-of-role-based-administration). También debe iniciar sesión en un servidor conectado al sitio de administración central o en un sitio primario independiente de nivel superior.

 Existen 3 pasos básicos para probar los clientes en preproducción.  

1.  [Para configurar las actualizaciones automáticas de cliente para que usen una recopilación de preproducción](#BKMK_config) para usar una recopilación de preproducción.  

2.  [Para instalar una actualización de Configuration Manager que incluye una nueva versión del cliente](#BKMK_install) que incluye una nueva versión del cliente. Durante la instalación, especifique una colección de preproducción para el nuevo software cliente.  

3.  [Para promover el nuevo cliente a producción](#BKMK_promote) después de una prueba correcta.  

> [!TIP]  
>  Si va a actualizar su infraestructura desde una versión anterior de Configuration Manager \(como Configuration Manager 2007 o System Center 2012 Configuration Manager\), se recomienda que realice las actualizaciones de servidor, incluida la instalación de todas las actualizaciones de la rama actual. Esto garantiza que tendrá la versión más reciente del software cliente antes de actualizar a los clientes de Configuration Manager.  

##  <a name="a-namebkmkconfiga-to-configure-automatic-client-upgrades-to-use-a-preproduction-collection"></a><a name="BKMK_config"></a> Para configurar las actualizaciones automáticas de cliente para que usen una recopilación de preproducción  

1. Configure una recopilación que contenga los equipos en los que quiere implementar el cliente de preproducción. Para obtener más información sobre cómo realizar este paso, consulte [Cómo crear recopilaciones](..\collections\create-collections.md).

> [!NOTE]
> No incluya equipos de grupo de trabajo en las recopilaciones de preproducción. Los equipos de grupo de trabajo no pueden usar la autenticación requerida para que el punto de distribución obtenga acceso al paquete de cliente de preproducción.   

1.  En la consola de Configuration Manager, abra **Administración** > **Configuración del sitio** > **Sitios** y elija **Configuración de jerarquía**.  

     En la pestaña **Actualización de cliente** de las **Propiedades de configuración de la jerarquía**:  

    -   Seleccione **Actualizar todos los clientes de la colección de preproducción automáticamente mediante el cliente de preproducción**.  

    -   Escriba el nombre de una colección para usarla como colección de preproducción.  


##  <a name="a-namebkmkinstalla-to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a><a name="BKMK_install"></a> Para instalar una actualización de Configuration Manager que incluye una nueva versión del cliente  

1.  En la consola de Configuration Manager, abra **Administración** > **Servicios en la nube** > **Actualizaciones y servicios**, seleccione una actualización **Disponible** y después elija **Instalar el paquete de actualización**  

     Para obtener más información sobre cómo instalar actualizaciones, consulte [Actualizaciones para System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

2.  Durante la instalación de la actualización, en la página **Opciones de cliente** del asistente, seleccione **Probar en la colección de preproducción**.  

3.  Complete el resto del asistente e instale el paquete de actualización.  

     Una vez que se complete el Asistente, los clientes de la recopilación de preproducción empezarán a implementar el cliente actualizado. Puede supervisar la implementación de clientes actualizados yendo a **Supervisión** > **Estado de cliente** > **Implementación de cliente de preproducción**. Para obtener más información, consulte [Supervisar el estado de implementación de cliente en System Center Configuration Manager](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > El estado de implementación en equipos que hospedan los roles de sistema de sitio en una recopilación de preproducción puede aparecer registrado como **No compatible** incluso cuando el cliente se ha implementado correctamente. Cuando se promueve el cliente a la producción, el estado de implementación se registrará correctamente.

##  <a name="a-namebkmkpromotea-to-promote-the-new-client-to-production"></a><a name="BKMK_promote"></a> Para promover el nuevo cliente a producción  

1.  En la consola de Configuration Manager, abra **Administración** > **Servicios en la nube** > **Actualizaciones y mantenimiento** y elija **Promover el cliente de preproducción**.

    > [!TIP]
    > El botón **Promover el cliente de preproducción** también está disponible cuando se están supervisando las implementaciones de cliente en la consola en **Supervisión** > **Estado de cliente** > **Implementación del cliente de preproducción**.

2.  En el cuadro de diálogo, revise las versiones de cliente de preproducción y de producción, asegúrese de que está especificada la recopilación de preproducción correcta y luego haga clic en **Promover**. En el cuadro de diálogo Confirmación, haga clic en **Sí**.  

3.  Después de cerrar el cuadro de diálogo, la versión del cliente actualizado reemplazará a la versión del cliente actual que se usa en la jerarquía. A continuación, puede actualizar los clientes de todo el sitio. Para obtener más información, consulte [Actualizar clientes de equipos Windows con System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  



<!--HONumber=Dec16_HO1-->


