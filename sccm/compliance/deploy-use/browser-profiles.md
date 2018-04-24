---
title: Configuración de las opciones de Microsoft Edge
titleSuffix: Configuration Manager
description: Configuración de las opciones para el explorador web Microsoft Edge en los clientes de Windows 10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/28/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: cb162e030249b02018af52ad3266b6b8df5ce355
ms.sourcegitcommit: aed99ba3c5e9482199cb3fc5c92f6f3a160cb181
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="configure-microsoft-edge-settings-in-system-center-configuration-manager"></a>Configuración de Microsoft Edge en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

<!-- 1357310 -->
A partir de la versión 1802, para los clientes que usan el explorador web [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) en los clientes de Windows 10, cree una directiva de configuración de cumplimiento de Configuration Manager para configurar varias opciones de Microsoft Edge. 

Esta directiva solo se aplica a clientes de Windows 10, versión 1703 o una versión posterior. <!--511552-->


## <a name="policy-settings"></a>Configuración de directiva
Actualmente, esta directiva incluye las siguientes opciones:
- **Set Microsoft Edge browser as default** (Establecer el explorador Microsoft Edge como predeterminado): configura los parámetros de la aplicación predeterminada de Windows 10 en cuanto a explorador web para que sea Microsoft Edge.
- **Allow address bar drop down** (Permitir desplegable en la barra de direcciones): requiere Windows 10, versión 1703, o una versión posterior. Para obtener más información, consulte [AllowAddressBarDropdown browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown) (Directiva de explorador AllowAddressBarDropdown).
- **Allow sync favorites between Microsoft browsers** (Permitir la sincronización de favoritos entre exploradores): requiere Windows 10, versión 1703, o una versión posterior. Para obtener más información, consulte [SyncFavoritesBetweenIEAndMicrosoftEdge browser policy](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge) (Directiva de explorador SyncFavoritesBetweenIEAndMicrosoftEdge).
- **Allow clear browsing data on exit** (Permitir el borrado de datos de exploración al salir): requiere Windows 10, versión 1703, o una versión posterior. Para obtener más información, consulte [ClearBrowsingDataOnExit browser policy](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit) (Directiva de explorador ClearBrowsingDataOnExit).
- **Allow Do Not Track headers** (Permitir encabezados No rastrear): para obtener más información, consulte [AllowDoNotTrack browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack) (Directiva de explorador AllowDoNotTrack).
- **Permitir el autorrelleno**: para obtener más información, consulte [AllowAutofill browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill) (Directiva de explorador AllowAutofill).
- **Permitir cookies**: para obtener más información, consulte [AllowCookies browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies). (Directiva de explorador AllowCookies).
- **Permitir bloqueador de elementos emergentes**: para obtener más información, consulte [AllowPopups browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups). (Directiva de explorador AllowPopups).
- **Permitir sugerencias de búsqueda en la barra de direcciones**: para obtener más información, consulte [AllowSearchSuggestionsinAddressBar browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar) (Directiva de explorador AllowSearchSuggestionsinAddressBar).
- **Allow send intranet traffic to Internet Explorer** (Permitir el envío de tráfico de la intranet a Internet Explorer): para obtener más información, consulte [SendIntranetTraffictoInternetExplorer browser policy](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer) (Directiva de explorador SendIntranetTraffictoInternetExplorer).
- **Permitir administrador de contraseñas**: para obtener más información, consulte [AllowPasswordManager browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager) (Directiva de explorador AllowPasswordManager).
- **Permitir herramientas de desarrollo**: para obtener más información, consulte [AllowDeveloperTools browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools) (Directiva de explorador AllowDeveloperTools).
- **Permitir extensiones**: para obtener más información, consulte [AllowExtensions browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions) (Directiva de explorador AllowExtensions).



## <a name="create-the-microsoft-edge-browser-profile"></a>Crear el perfil del explorador Microsoft Edge

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**. Expanda **Configuración de cumplimiento** y seleccione el nuevo nodo **Microsoft Edge Browser Profiles** (Perfiles de explorador de Microsoft Edge). Haga clic en la opción de cinta de opciones **Create Microsoft Edge Browser Policy** (Crear directiva de explorador de Microsoft Edge).
2. Especifique un **nombre** para la directiva, opcionalmente, escriba una **descripción** y haga clic en **Siguiente**.
3. En la página **configuración**, cambie el valor a **Configurado** para incluir en esta directiva y haga clic en **Siguiente**.
4. En la página **Plataformas admitidas**, seleccione las versiones y las arquitecturas de sistema operativo a las que se aplica esta directiva y haga clic en **Siguiente**. 
5. Complete el asistente.



## <a name="deploy-the-policy"></a>Implementar la directiva

1. Seleccione la directiva y haga clic en la opción de cinta de opciones **Implementar**.
2. Haga clic en **Examinar** para seleccionar la recopilación de usuarios o dispositivos en la que desea implementar la directiva. 
3. Seleccione opciones adicionales según sea necesario. 
    a. Genere alertas cuando la directiva no sea compatible. 
    b. Establezca la programación según la cual el cliente evalúa el cumplimiento del dispositivo con esta directiva.
4. Haga clic en **Aceptar** para crear la implementación.



## <a name="next-steps"></a>Pasos siguientes

Como ocurre con cualquier directiva de configuración de cumplimiento, el cliente corrige la configuración según la programación que especifique. [Supervise el cumplimiento del dispositivo y genere informes al respecto](/sccm/compliance/deploy-use/monitor-compliance-settings) en la consola de Configuration Manager.
