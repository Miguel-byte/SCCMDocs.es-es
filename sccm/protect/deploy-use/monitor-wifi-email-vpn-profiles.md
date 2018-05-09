---
title: Supervisión de perfiles de correo electrónico, Wi-Fi y VPN
titleSuffix: Configuration Manager
description: Aprenda a supervisar el estado de compatibilidad de los perfiles de correo electrónico, Wi-Fi y VPN en System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 47b5bb12a89143a0c7e6d16a3252948b955b8ff3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Supervisión de perfiles de correo electrónico, Wi-Fi y VPN en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Después de implementar los perfiles de correo electrónico, Wi-Fi y VPN de System Center Configuration Manager en los usuarios de la jerarquía, puede realizar estos procedimientos para supervisar el estado de compatibilidad del perfil:  

-   [Ver los resultados de compatibilidad en la consola de Configuration Manager](#BKMK_console)  

-   [Ver los resultados de compatibilidad mediante informes](#BKMK_Reports)  

##  <a name="BKMK_console"></a> Ver los resultados de compatibilidad en la consola de Configuration Manager  
 Use este procedimiento para ver los detalles sobre la compatibilidad de los perfiles implementados en la consola de System Center Configuration Manager.  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para ver los resultados de compatibilidad en la consola de Configuration Manager  

1.  En la consola de System Center Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , haga clic en **Implementaciones**.  

3.  En la lista **Implementaciones**, seleccione la implementación del perfil para el que quiere revisar la información de compatibilidad.  

4.  Puede revisar la información de resumen sobre la compatibilidad de la implementación del perfil en la página principal. Para ver información más detallada, seleccione la implementación del perfil y luego, en la pestaña **Inicio** del grupo **Implementación**, haga clic en **Ver estado** para abrir la página **Estado de implementación**.  

     La página **Estado de implementación** contiene las siguientes pestañas:  

    -   **Compatible:** muestra la compatibilidad del perfil en función del número de recursos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** , en el área de trabajo **Activos y compatibilidad** , que contiene todos los usuarios compatibles con este perfil. El panel **Detalles del activo** muestra los usuarios que son compatibles con el perfil. Haga doble clic en un usuario de la lista para mostrar información adicional.  

        > [!IMPORTANT]  
        >  Un perfil no se evalúa si no es aplicable en un determinado dispositivo cliente, pero se devuelve como compatible.  

    -   **Error:** muestra una lista de todos los errores de la implementación del perfil seleccionada en función del número de recursos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** , en el área de trabajo **Activos y compatibilidad** , que contiene todos los usuarios que generaron errores con este perfil. Cuando se selecciona un usuario, el panel **Detalles del activo** muestra los usuarios afectados por el problema seleccionado. Haga doble clic en un usuario de la lista para mostrar información adicional sobre el problema.  

    -   **No compatible:** muestra una lista de todas las reglas no compatibles en el perfil, en función del número de activos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** , en el área de trabajo **Activos y compatibilidad** , que contiene todos los usuarios no compatibles con este perfil. Cuando se selecciona un usuario, el panel **Detalles del activo** muestra los usuarios afectados por el problema seleccionado. Haga doble clic en un usuario de la lista para mostrar información adicional sobre el problema.  

    -   **Desconocido:** muestra una lista de todos los usuarios que no han notificado la compatibilidad de la implementación de perfil seleccionado y el estado de cliente actual de los dispositivos.  

5.  En la página **Estado de implementación**, puede revisar información detallada sobre la compatibilidad del perfil implementado. Se crea un nodo temporal en el nodo **Implementaciones** que le permite encontrar esta información rápidamente.  

##  <a name="BKMK_Reports"></a> Ver los resultados de compatibilidad mediante informes  
 La configuración de compatibilidad, que incluye los perfiles en System Center Configuration Manager, también incluye varios informes integrados que permiten supervisar la información sobre los perfiles. Estos informes tienen la categoría de informe de **Administración de compatibilidad y configuración**.  

> [!IMPORTANT]  
>  Debe usar un carácter comodín (%) para utilizar los parámetros **Filtro del dispositivo** y **Filtro de usuarios** en los informes de configuración de cumplimiento.  

 Para obtener más información sobre cómo configurar los informes en System Center Configuration Manager, vea [Generación de informes en System Center Configuration Manager](../../core/servers/manage/reporting.md).  
