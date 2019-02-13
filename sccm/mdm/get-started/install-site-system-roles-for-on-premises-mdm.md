---
title: 'Instalación de roles para la MDM local '
titleSuffix: Configuration Manager
description: Instalar roles de sistema de sitio para la administración de dispositivos móviles local en System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e5d81d385c48d9653e1596e6a5d9d1163e84f314
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141762"
---
# <a name="install-site-system-roles-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Instalar roles de sistema de sitio para Administración de dispositivos móviles local en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La Administración de dispositivos móviles local en System Center Configuration Manager requiere los siguientes roles de sistema de sitio en su infraestructura de sitio de Configuration Manager:  

- Punto de inscripción  

- Punto de proxy de inscripción  

- Punto de distribución  

- Punto de administración de dispositivos  

- Punto de conexión de servicio  

  Si va a agregar la administración de dispositivos móviles local a su organización que tiene la mayoría de los equipos y dispositivos administrados con el software del cliente de Configuration Manager, es posible que tenga la mayoría de los roles de sistema de sitio ya instalados como parte de su infraestructura existente. Si no, consulte [Add site system roles for System Center Configuration Manager (Agregar roles de sistema de sitio para System Center Configuration Manager)](../../core/servers/deploy/configure/add-site-system-roles.md) para completar la información sobre cómo agregarlos al sitio.  

> [!NOTE]  
>  Si usa réplicas de base de datos con el rol de sistema de sitio del punto de administración de dispositivos, los dispositivos recién inscritos presentarán inicialmente un error al conectarse al punto de administración de dispositivos hasta que la réplica de base de datos se sincroniza con él. Este error de conexión se produce porque la réplica de base de datos no tiene la información sobre el dispositivo recién inscrito que se necesita para establecer una conexión correctamente. Las réplicas se sincronizan cada 5 minutos, por lo que no se podrán conectar durante los primeros 5 minutos tras la inscripción (normalmente 2 intentos de conexión). Una vez transcurrido este tiempo, el dispositivo se conectará correctamente.  

 Ya esté usando los roles de sistema de sitio existentes o agregando nuevos, debe configurarlos para usarlos en la administración de dispositivos modernos. Siga los pasos siguientes para configurar el punto de distribución y el punto de administración de dispositivos a fin de que funcionen correctamente para la administración de dispositivos móviles local:  

> [!NOTE]  
>  La rama actual de Configuration Manager solo admite conexiones de intranet desde dispositivos a los puntos de distribución y puntos de administración de dispositivos para la Administración de dispositivos móviles local. Sin embargo, si también está administrando equipos con Mac OS X, esos clientes requieren conexiones de Internet a esos roles de sistema de sitio. En ese caso, al configurar las propiedades del punto de distribución y el punto de administración de dispositivos, debe usar la configuración **Permitir conexiones de intranet e Internet** en su lugar.  

### <a name="to-configure-site-system-roles-to-manage-modern-devices"></a>Para configurar roles de sistema de sitio para administrar dispositivos modernos:  

1. En la consola de Configuration Manager, haga clic en **Administración** > **Información general** > **Configuración de sitio** > **Servidores y roles del sistema de sitios**.  

2. Seleccione el servidor de sistema de sitio con el punto de distribución o el punto de administración de dispositivos que quiere configurar, abra las propiedades del **Sistema de sitio** y asegúrese de que tiene un FQDN especificado. Haga clic en **Aceptar**.  

3. Abra las propiedad del rol de sistema de sitio de punto de distribución. En la pestaña General, asegúrese de que **HTTPS** está seleccionado y seleccione **Permitir solo conexiones de intranet**.  

    Si también administra equipos Mac por separado con el cliente de Configuration Manager, use **Permitir conexiones de intranet e Internet** en su lugar.  

   > [!NOTE]  
   >  Los puntos de distribución configurados para conexiones de intranet requieren que se configuren límites de sitio para ellos. La rama actual de Configuration Manager solo admite límites de intervalo IPv4 para la Administración de dispositivos móviles local. Para obtener más información sobre la configuración de límites de sitio, consulte [Definir los límites del sitio y los grupos de límites para System Center Configuration Manager](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

4. Haga clic en la casilla junto a **Permitir que los dispositivos móviles se conecten a este punto de distribución** y luego haga clic en **Aceptar**.  

5. Abra las propiedad del rol de sistema de sitio de punto de administración. En la pestaña General, asegúrese de que **HTTPS** está seleccionado y seleccione **Permitir solo conexiones de intranet**.  

    Si también administra equipos Mac por separado con el cliente de Configuration Manager, use **Permitir conexiones de intranet e Internet** en su lugar.  

6. Haga clic en la casilla que se encuentra junto a **Permitir a los dispositivos móviles y equipos Mac usar este punto de administración**. Haga clic en **Aceptar**.  

    Esto convierte de manera efectiva el punto de administración en un punto de administración de dispositivos.  

   Una vez que se han agregado y configurado los roles de sistema de sitio para administrar dispositivos modernos, debe configurar los servidores que hospedan los roles como puntos de conexión de confianza para inscribirse y comunicarse con los dispositivos administrados. Consulte [Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager (Configurar certificados de comunicaciones de confianza para la administración de dispositivos móviles local en System Center Configuration Manager)](../../mdm/get-started/set-up-certificates-on-premises-mdm.md) para obtener más información.  
