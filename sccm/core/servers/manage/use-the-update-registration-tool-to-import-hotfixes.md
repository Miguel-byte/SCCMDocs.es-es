---
title: Herramienta de registro de actualizaciones
titleSuffix: Configuration Manager
description: Averigüe cuándo y cómo usar la herramienta de registro de actualizaciones para importar manualmente una actualización a la consola de Configuration Manager.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 94f0da3fa9f4aa43ce4818b7b6edf752df53d66a
ms.sourcegitcommit: ee434c53b3695a039b56298082b6f61f1006d9dd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2018
ms.locfileid: "49943281"
---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-system-center-configuration-manager"></a>Uso de la herramienta de registro de actualizaciones para importar revisiones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Algunas actualizaciones para Configuration Manager no están disponibles desde el servicio en la nube de Microsoft y solo se obtienen de un origen externo. Un ejemplo es la versión limitada de una revisión para resolver un problema específico.   
Si instala una versión de un origen externo y el nombre de archivo de la actualización o la revisión termina con la extensión **update.exe**, use la **herramienta de registro de actualizaciones** para importar manualmente la actualización a la consola de Configuration Manager. La herramienta permite extraer y transferir el paquete de actualización al servidor del sitio y registrar la actualización en la consola de Configuration Manager.  

 Si el archivo de revisión tiene la extensión de archivo **.exe** (no **update.exe**), consulte [Use the Hotfix Installer to install updates for System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md) (Uso del instalador de revisiones para instalar actualizaciones para System Center Configuration Manager).  

> [!NOTE]  
>  En este tema se proporcionan instrucciones generales sobre cómo instalar las revisiones que actualizan System Center Configuration Manager. Para obtener información más detallada acerca de una revisión o actualización específica, consulte su correspondiente artículo de Knowledge Base (KB) en el soporte técnico de Microsoft.  

 **Requisitos previos para usar la herramienta de registro de actualizaciones:**  

-   Con esta herramienta solo se pueden instalar actualizaciones de orígenes externos que finalicen con la extensión **.update.exe**.  

-   La herramienta se incluye con las actualizaciones individuales que obtiene directamente de Microsoft.  

-   La herramienta no tiene una dependencia sobre el modo del punto de conexión de servicio.  

-   La herramienta debe ejecutarse en el equipo que hospeda el punto de conexión de servicio.  

-   El equipo donde se ejecuta la herramienta (el equipo del punto de conexión de servicio) debe tener instalado .NET Framework 4.52.  

-   La cuenta que usa para ejecutar la herramienta debe tener permisos de **administrador local** en el equipo que hospeda el punto de conexión de servicio (donde se ejecuta la herramienta).  

-   La cuenta que usa para ejecutar la herramienta debe tener permisos de **escritura** en la siguiente carpeta en el equipo que hospeda el punto de conexión de servicio: **&lt;directorio de instalación de Configuration Manager\>\EasySetupPayload\offline**.  

### <a name="to-use-the-update-registration-tool"></a>Para usar la herramienta de registro de actualizaciones  

1.  En el equipo que hospeda el punto de conexión de servicio:  

    -   Abra un símbolo del sistema con privilegios administrativos y, después, cambie los directorios a la ubicación que contiene **&lt;Producto\>-&lt;versión de producto\>-&lt;id. de artículo de KB\>-ConfigMgr.Update.exe**.  

2.  Ejecute el siguiente comando para iniciar la herramienta de registro de actualizaciones:  

    -   **&lt;Producto\>-&lt;versión de producto\>-&lt;id. de artículo de KB\>-ConfigMgr.Update.exe**  

    Una vez registrada la revisión, aparece como nueva actualización en la consola en el plazo de 24 horas.  Puede acelerar el proceso:

    - Abra la consola de Configuration Manager y vaya a **Administración** > **Updates and Servicing** (Actualizaciones y mantenimiento) y, luego, haga clic en **Check for Updates** (Buscar actualizaciones). (Antes de la versión 1702, la opción Actualizaciones y mantenimiento se encontraba en **Administración** > **Cloud Services**). 

    La herramienta de registro de actualizaciones registra sus acciones en un archivo .log en el equipo local. El archivo de registro tiene el mismo nombre que el archivo hotfix.exe y se escribe en la carpeta **%SystemRoot%/Temp**.  

     Una vez registrada la actualización, podrá cerrar la herramienta de registro de actualizaciones.  

3.  Abra la consola de Configuration Manager y vaya a **Administración** > **Actualizaciones y mantenimiento**. Ahora están disponibles para instalar las revisiones que se han importado. (Antes de la versión 1702, la opción Actualizaciones y mantenimiento se encontraba en **Administración** > **Cloud Services**).

 Para obtener más información sobre la instalación de actualizaciones, consulte [Install in-console updates for System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md) (Instalación de actualizaciones en la consola para System Center Configuration Manager).  
