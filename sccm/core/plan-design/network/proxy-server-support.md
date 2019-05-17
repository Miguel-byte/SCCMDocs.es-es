---
title: Compatibilidad de servidor proxy
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo los servidores de sistema de sitio de Configuration Manager usan los servidores proxy.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e5c689ff3621477aa84d958e97c2dfebb81dcca1
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499169"
---
# <a name="proxy-server-support-in-configuration-manager"></a>Compatibilidad con servidores proxy en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Algunos servidores de sistema de sitio de Configuration Manager requieren conexiones a Internet. Si su entorno necesita tráfico de Internet para usar un servidor proxy, configure estos roles de sistema de sitio para que usen el proxy.  

-   Un equipo que hospede un servidor de sistema de sitio solo admite una configuración de servidor proxy. Todos los roles de sistema de sitio de ese equipo comparten esta misma configuración de proxy. Si necesita servidores proxy independientes para otros roles o instancias de un rol, coloque esos roles en servidores de sistema de sitio independientes.  

-   Al definir la nueva configuración de servidor proxy para un servidor de sistema de sitio que ya tiene una configuración de servidor proxy, se sobrescribe la configuración original.  

-   De forma predeterminada, las conexiones al proxy usan la cuenta de **sistema** del equipo que hospeda el rol de sistema de sitio.  

-   Si no se puede autenticar la cuenta de equipo, el servidor de sistema de sitio puede almacenar las credenciales de usuario para conectarse al servidor proxy. Estas credenciales son la **cuenta del servidor proxy de sistema de sitio**.  



## <a name="site-system-roles-that-use-a-proxy"></a>Roles de sistema de sitio que usan un proxy

Los roles de sistema de sitio siguientes se conectan a Internet y, si es necesario, pueden usar un servidor proxy:  


#### <a name="asset-intelligence-synchronization-point"></a>Punto de sincronización de Asset Intelligence
Este rol de sistema de sitio se conecta a Microsoft y usa una configuración de servidor proxy en el equipo que hospeda el punto de sincronización de Asset Intelligence.  


#### <a name="cloud-distribution-point"></a>Punto de distribución de nube
El rol de punto de distribución de nube se ejecuta en Microsoft Azure. No configure este rol de sistema de sitio para usar un proxy. Establezca la configuración de proxy en el servidor de sitio primario que administra el punto de distribución de nube.  

Para esta configuración, el servidor de sitio primario:  

-   Debe poder conectarse a Microsoft Azure para configurar, supervisar y distribuir contenido en el punto de distribución de nube.  

-   De forma predeterminada, usa la cuenta de **sistema** del equipo para realizar la conexión. También puede usar la cuenta de servidor proxy de sistema de sitio, si es necesario.  

-   Usa las API de explorador web de Windows.  


#### <a name="exchange-server-connector"></a>Conector de Exchange Server
Este rol de sistema de sitio se conecta a una instancia de Exchange Server. Usa una configuración de servidor proxy en el equipo que hospeda el conector de Exchange Server.  


#### <a name="service-connection-point"></a>Punto de conexión de servicio
Este rol de sistema de sitio se conecta al servicio en la nube de Configuration Manager para descargar las actualizaciones de versión de Configuration Manager, y se conecta a Microsoft Intune en una configuración híbrida. Usa un servidor proxy que se configura en el equipo que hospeda el punto de conexión de servicio.  


#### <a name="software-update-point"></a>Punto de actualización de software
Este rol de sistema de sitio usa el proxy al conectarse a Microsoft Update para descargar revisiones y sincronizar la información sobre las actualizaciones. Como en los demás roles de sistema de sitio, establezca primero la configuración de proxy del sistema de sitio. Después, configure las opciones siguientes específicas para el punto de actualización de software:  

-   **Utilizar un servidor proxy al sincronizar las actualizaciones de software**  

-   **Utilizar un servidor proxy al descargar contenido mediante reglas de implementación automática**  

    > [!Note]  
    > Si se encuentra disponible para su uso, esta configuración no se usa para los puntos de actualización de software en los sitios secundarios.  

Estas opciones se encuentran en la pestaña **Configuración de cuenta y proxy** de las propiedades de punto de actualización de software.  

> [!NOTE]  
>  De forma predeterminada, la cuenta **Sistema** en el servidor de sitio en el que se ha creado una regla de implementación automática se usa para conectarse a Internet y descargar actualizaciones de software cuando se ejecutan las reglas de implementación automática. Como alternativa, configure y use la cuenta de servidor proxy del sistema de sitio. 
>   
>  Cuando esta cuenta no puede acceder a Internet, no se pueden descargar las actualizaciones de software. La entrada siguiente se registra en **ruleengine.log**:  
> `Failed to download the update from internet. Error = 12007.`  



## <a name="configure-the-proxy-for-a-site-system-server"></a>Configurar el proxy para un servidor de sistema de sitio  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Configuración del sitio** y, después, haga clic en el nodo **Servidores y roles del sistema de sitios**.  

2.  Seleccione el servidor de sistema de sitio que quiera modificar. En el panel de detalles, haga clic con el botón derecho en el rol **Sistema de sitio** y seleccione **Propiedades**.  

3.  En las propiedades del sistema de sitio, cambie a la pestaña **Proxy**. Configure las opciones de proxy siguientes:  

    - **Usar un servidor proxy al sincronizar información desde Internet**: seleccione esta opción para permitir que el servidor de sistema de sitio use un servidor proxy.  

    - **Nombre del servidor proxy**: especifique el nombre de host o FQDN del servidor proxy en el entorno.  

    - **Puerto**: especifique el puerto de red en el que se realiza la comunicación con el servidor proxy. De forma predeterminada, se usa el puerto **80**.  

    - **Usar credenciales para conectarse al servidor proxy**: muchos servidores proxy necesitan que un usuario se autentique. De forma predeterminada, el servidor de sistema de sitio usa su cuenta de equipo para conectarse al servidor proxy. Si es necesario, habilite esta opción, haga clic en **Establecer** y, después, elija una **Cuenta existente** o especifique una **Nueva cuenta**. Estas credenciales son la **cuenta del servidor proxy de sistema de sitio**.  Para obtener más información, vea [Cuentas que se usan en Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).  

4.  Seleccione **Aceptar** para guardar la nueva configuración del servidor proxy.  
