---
title: Herramientas de Configuration Manager
titleSuffix: Configuration Manager
description: Obtenga información sobre las herramientas que ayudan a administrar la infraestructura de Configuration Manager y a solucionar problemas de ella.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fd23bd523eb64f7d00f71c38c79a180c4e2e569a
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386546"
---
# <a name="configuration-manager-tools"></a>Herramientas de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las herramientas de Configuration Manager incluyen [herramientas basadas en cliente](#client-tools) y [basadas en servidor](#server-tools). Use estas herramientas para prestar soporte y solucionar problemas en la infraestructura de Configuration Manager. 

A partir de Configuration Manager versión 1806, estas herramientas están incluidas en la carpeta `CD.Latest\SMSSETUP\Tools` del servidor de sitio. No se necesita ninguna otra instalación.<!--1357145--> Use estas versiones de las herramientas con Configuration Manager versión 1806 y versiones posteriores.

Todos los sistemas operativos Windows que se indican como clientes compatibles en [Sistemas operativos compatibles con clientes y dispositivos](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) se pueden usar con estas herramientas.

> [!Note]  
> El [kit de herramientas de System Center 2012 R2 Configuration Manager](https://www.microsoft.com/en-us/download/details.aspx?id=50012) sigue estando disponible en el Centro de descarga de Microsoft. En Configuration Manager versión 1806 y versiones posteriores, use las versiones de las herramientas de la carpeta CD.Latest del servidor de sitio. Antes, algunas herramientas se encontraban en el kit de herramientas, pero no se incluían en la versión 1806. Estas herramientas heredadas ya no se admiten.


## <a name="client-tools"></a>Herramientas cliente

- [CMTrace](/sccm/core/support/cmtrace): sirve para ver, supervisar y analizar archivos de registro de Configuration Manager  

- [Cliente Spy](/sccm/core/support/clispy): soluciona problemas relacionados con la distribución de software, el inventario y la medición

- [Deployment Monitoring Tool](/sccm/core/support/deployment-monitoring-tool): permite solucionar los problemas de aplicaciones, actualizaciones e implementaciones de línea de base.  

- [Policy Spy](/sccm/core/support/policy-spy): permite ver las asignaciones de directiva.  

- [Power Viewer Tool](/sccm/core/support/power-viewer-tool): permite ver el estado de la característica de administración de energía.  

- [Send Schedule Tool](/sccm/core/support/send-schedule-tool): desencadena programaciones y evaluaciones de líneas de base de configuración  

> [!Note]  
> La carpeta ClientTools también incluye el archivo Microsoft.Diagnostics.Tracing.EventSource.dll. Varias herramientas de cliente necesitan esta biblioteca. No se puede usar directamente.  


## <a name="server-tools"></a>Herramientas de servidor

- [DP Job Queue Manager](/sccm/core/support/dp-job-manager): soluciona los problemas de los trabajos de distribución de contenido a los puntos de distribución  

- [Collection Evaluation Viewer](/sccm/core/support/ceviewer): permite ver los detalles de evaluación de la recopilación.  

- [Content Library Explorer](/sccm/core/support/content-library-explorer): permite ver el contenido del almacén de instancia única de la biblioteca de contenido.  

- [Content Library Transfer](/sccm/core/support/content-library-transfer): transfiere la biblioteca de contenido entre unidades.  

- [Content Ownership Tool](/sccm/core/support/content-ownership-tool): cambia la propiedad de los paquetes huérfanos. Estos paquetes existen en el sitio sin un servidor de sitio propietario.  

- [Role-based Administration and Auditing Tool](/sccm/core/support/rbaviewer): ayuda a los administradores a auditar la configuración de los roles.  

- [Run Meter Summarization Tool](/sccm/core/support/run-meter-summ): Ejecuta la tarea de resumen de medición y analiza los datos de medición

> [!Note]  
> La carpeta ServerTools también incluye los siguientes archivos 
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll. 
>
> Varias herramientas de servidor necesitan estas bibliotecas. No se pueden usar directamente.  



## <a name="other-tools"></a>Otras herramientas

- [Content library cleanup tool](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool): use **ContentLibraryCleanup.exe** en `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` para quitar contenido huérfano de un punto de distribución.  

- [Hierarchy Maintenance Tool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe): use **Preinst.exe** en la carpeta compartida `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` del servidor de sitio para pasar comandos al componente Administrador de jerarquía.  

- [Update reset tool](/sccm/core/servers/manage/update-reset-tool): use **CMUpdateReset.exe** en `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` para solucionar los problemas de descarga o replicación de las actualizaciones en la consola.  

- [Service Connection Tool](/sccm/core/servers/manage/use-the-service-connection-tool): use **ServiceConnectionTool.exe** en `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` para mantener actualizado el sitio cuando el punto de conexión de servicio está sin conexión.  
