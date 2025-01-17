---
title: Planear y configurar la configuración de cumplimiento
titleSuffix: Configuration Manager
description: Obtenga información sobre los requisitos previos y las tareas de configuración necesarios para trabajar con la configuración de cumplimiento de System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2d728dae6dc67a4c66403bdb2299e50dcd6e3557
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67677941"
---
# <a name="plan-for-and-configure-compliance-settings-in-system-center-configuration-manager"></a>Planear y configurar la configuración de cumplimiento en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Antes de empezar a trabajar con la configuración de cumplimiento de System Center Configuration Manager, hay algunos requisitos previos que debe conocer y algunas tareas de configuración que debe realizar.  

## <a name="prerequisites-for-compliance-settings"></a>Requisitos previos para la configuración de cumplimiento  

|Requisito previo|Más información|  
|------------------|----------------------|  
|Los clientes de Windows Configuration Manager deben estar habilitados y configurados para la evaluación de cumplimiento.|Vea a continuación|  
|Si quiere ejecutar informes, debe configurarlos para el sitio.|[Generación de informes en System Center Configuration Manager](../../core/servers/manage/reporting.md)|  
|Permisos de seguridad requeridos.|El rol de seguridad **Administrador de configuración de cumplimiento** incluye estos permisos necesarios para administrar la configuración de cumplimiento, los elementos de configuración de perfiles y datos de usuario, y los perfiles de conexión remota.<br /><br /> [Configurar la administración basada en roles](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>Habilitar y establecer la configuración de cumplimiento (solo para equipos Windows)  

En este procedimiento se define la configuración de cliente predeterminada para la configuración de cumplimiento y se aplica a todos los equipos de la jerarquía. Si quiere que esta configuración solo se aplique a algunos equipos, cree una configuración de cliente de dispositivo personalizada y asígnela a una recopilación que contenga los equipos en los que quiere usar la configuración de cumplimiento. Para obtener más información sobre cómo crear configuraciones de dispositivo personalizadas, vea [Cómo establecer la configuración de cliente](../../core/clients/deploy/configure-client-settings.md).  

> [!TIP]  
>  Otros tipos de dispositivos no requieren ninguna configuración específica para evaluar la configuración de cumplimiento.  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de cliente** > **Configuración predeterminada**.  
2.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  
3.  En el cuadro de diálogo **Configuración predeterminada** , haga clic en **Configuración de cumplimiento**.  
4.  Configure las siguientes opciones de cliente para la configuración de cumplimiento:
    - **Habilitar la evaluación de cumplimiento en los clientes**: establézcala en **True** si quiere evaluar el cumplimiento en dispositivos cliente.
    - **Programar evaluación de compatibilidad**: haga clic en **Programar** si quiere modificar la programación de evaluación de cumplimiento predeterminada en los dispositivos cliente.
    - **Habilitar perfiles y datos de usuario**: habilite esta opción si quiere crear e implementar los elementos de configuración de perfiles y datos de usuario en los equipos Windows. Para obtener más información, vea [Crear elementos de configuración de perfiles y datos de usuario](/sccm/compliance/deploy-use/create-remote-connection-profiles).
5. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configuración predeterminada** .  

Los equipos cliente se configuran con estas opciones la próxima vez que descargan directivas de cliente.  
