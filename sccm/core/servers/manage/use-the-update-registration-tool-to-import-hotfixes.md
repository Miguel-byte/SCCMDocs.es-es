---
title: Herramienta de registro de actualizaciones | Microsoft Docs
description: "Averigüe cuándo y cómo usar la herramienta de registro de actualizaciones para importar manualmente una actualización a la consola de Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: c729212d38168acfff3f11ea41f3d52b234c70c8
ms.lasthandoff: 12/16/2016


---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-system-center-configuration-manager"></a>Uso de la herramienta de registro de actualizaciones para importar revisiones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

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

    Una vez registrada la revisión, aparece como nueva actualización en la consola en el plazo de 24 horas.  Puede acelerar el proceso mediante uno de los métodos siguientes:  

    -   Con la versión 1511: en la consola de Configuration Manager, vaya a **Administración > Cloud Services > Actualizaciones y mantenimiento** y, después, seleccione **Start update discovery process immediately** (Iniciar proceso de detección de actualizaciones inmediatamente).  De este modo se inicia la importación de la revisión inmediatamente en cuanto finalice el proceso de registro, haciendo que esté disponible en la consola.  

    -   Con la versión 1602 y posteriores: en la consola de Configuration Manager, vaya a **Administración > Cloud Services > Actualizaciones y mantenimiento** y, después, haga clic en **Buscar actualizaciones**.  

    La herramienta de registro de actualizaciones registra sus acciones en un archivo .log en el equipo local. El archivo de registro tiene el mismo nombre que el archivo hotfix.exe y se escribe en la carpeta **%SystemRoot%/Temp**.  

     Una vez registrada la actualización, podrá cerrar la herramienta de registro de actualizaciones.  

3.  Abra la consola de Configuration Manager y vaya a AdministraciónServicios en la nubeActualizaciones y mantenimiento(Iniciar proceso de detección de actualizaciones inmediatamente). Ahora están disponibles para instalar las revisiones que se han importado. Para obtener más información sobre la instalación de actualizaciones, consulte [Install in-console updates for System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md) (Instalación de actualizaciones en la consola para System Center Configuration Manager).  

