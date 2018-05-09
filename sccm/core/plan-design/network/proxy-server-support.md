---
title: Compatibilidad de servidor proxy
titleSuffix: Configuration Manager
description: Obtenga información sobre la compatibilidad de System Center Configuration Manager con los servidores proxy que usan los servidores y los clientes del sistema de sitio.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 480ab29bbd97f2cdc173019b1b3cccd90403d011
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="proxy-server-support-in-system-center-configuration-manager"></a>Compatibilidad de servidor proxy en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Tanto los servidores como los clientes del sistema de sitio de System Center Configuration Manager pueden usar un servidor proxy.  

## <a name="site-system-servers"></a>Servidores de sistema de sitio  
Si los roles de sistema de sitio necesitan conectarse a Internet, puede configurarlos para usar un servidor proxy.  

-   Un equipo que hospeda un servidor de sistema de sitio admite una única configuración de servidor proxy que comparten todos los roles de sistema de sitio en ese equipo. Si necesita servidores proxy independientes para distintos roles o instancias de un rol, necesita colocar esos roles en servidores de sistema de sitio independientes.  

-   Al definir la nueva configuración de servidor proxy para un servidor de sistema de sitio que ya tiene una configuración de servidor proxy, se sobrescribe la configuración original.  

-   Las conexiones al proxy usan la cuenta de **sistema** del equipo que hospeda el rol de sistema de sitio.  

Los siguientes roles de sistema de sitio se conectan a Internet y pueden necesitar un servidor proxy.  Con una excepción, los roles de sistema de sitio que pueden usar un proxy lo hacen sin ninguna configuración adicional. La excepción es el punto de actualización de software. La lista siguiente contiene información sobre las configuraciones adicionales que necesita un punto de actualización de software:  

**Punto de sincronización de Asset Intelligence**: este rol de sistema de sitio se conecta a Microsoft y usa una configuración de servidor proxy en el equipo que hospeda el punto de sincronización de Asset Intelligence.  

**Punto de distribución basado en la nube**: para configurar un servidor proxy para un punto de distribución basado en la nube necesita configurar el proxy en el sitio primario que administra el punto de distribución basado en la nube.  

Para esta configuración, el servidor de sitio primario:  

-   Necesita conectarse a Microsoft Azure para configurar, supervisar y distribuir contenido en el punto de distribución.  

-   Usa la cuenta del sistema de ese equipo para realizar la conexión.  

-   Usa el explorador web predeterminado de ese equipo.  

No se puede configurar un servidor proxy en el punto de distribución basado en la nube de Microsoft Azure.  

**Punto de conexión en la nube**: este rol de sistema de sitio se conecta al servicio en la nube de Configuration Manager para descargar actualizaciones de la versión de Configuration Manager y usa un servidor proxy configurado en el equipo que hospeda el punto de conexión de servicio.  

**Conector de Exchange Server**: este rol de sistema de sitio se conecta a un servidor de Exchange Server y usará una configuración de servidor proxy en el equipo que hospeda el conector de Exchange Server.  

**Punto de conexión de servicio**: este rol de sistema de sitio se conecta a Microsoft Intune y usará una configuración de servidor proxy en el equipo que hospeda el punto de conexión de servicio.  

**Punto de actualización de software**: este rol de sistema de sitio puede usar el proxy al conectarse a Microsoft Update para descargar revisiones y sincronizar la información acerca de las actualizaciones. Los puntos de actualización de software solo usan un proxy para las opciones siguientes después de habilitar esa opción al configurar el punto de actualización de software:  

-   **Utilizar un servidor proxy al sincronizar las actualizaciones de software**  

-   **Usar un servidor proxy cuando se descargue contenido mediante reglas de implementación automática** (si se encuentra disponible para su uso, esta configuración no se usa para los puntos de actualización de software en sitios secundarios).  

Configure el servidor proxy en la página Punto de actualización de software activo del Asistente para agregar roles de sistema de sitio o en la pestaña **General** de **Propiedades de componente de punto de actualización de software**.  

-   La configuración del servidor proxy está asociada únicamente al punto de actualización de software en el sitio.  

-   Las opciones del servidor proxy solo están disponibles cuando ya hay configurado un servidor proxy para el servidor de sistema de sitio que hospeda el punto de actualización de software.  

> [!NOTE]  
>  De forma predeterminada, la cuenta **Sistema** para el servidor en el que se creó una regla de implementación automática se utiliza para conectarse a Internet y descargar actualizaciones de software cuando se ejecutan las reglas de implementación automática.  
>   
>  Si esta cuenta no tiene acceso a Internet, las actualizaciones de software no se descargarán y se registrará la entrada siguiente en ruleengine.log: **Failed to download the update from internet (No se pudo descargar la actualización de Internet). Error = 12007.**  

#### <a name="to-set-up-the-proxy-server-for-a-site-system-server"></a>Para configurar el servidor proxy para un servidor de sistema de sitio  

1.  En la consola de Configuration Manager, seleccione **Administración**, expanda **Configuración de sitio** y, después, haga clic en **Servidores y roles del sistema de sitios**.  

2.  Seleccione el servidor de sistema de sitio que quiera editar y, en el panel de detalles, haga clic con el botón derecho en **Sistema de sitio** y, después, haga clic en **Propiedades**.  

3.  En Propiedades de sistema de sitio, seleccione la pestaña **Proxy** y, después, establezca la configuración de proxy para este servidor de sitio primario.  

4.  Seleccione **Aceptar** para guardar la nueva configuración del servidor proxy.  
