---
title: Requisitos previos de control remoto
titleSuffix: Configuration Manager
description: Cumpla los requisitos previos del control remoto en System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 117ad9a087151db51c4cf33112ab662f53b9134e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="prerequisites-for-remote-control-in-system-center-configuration-manager"></a>Requisitos previos del control remoto en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

El control remoto de System Center Configuration Manager tiene dependencias externas y dependencias dentro del producto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependencias externas a Configuration Manager  

|Dependencia|Más información|  
|----------------|----------------------|  
|Controlador de tarjeta de vídeo del equipo|Asegúrese de que el controlador de vídeo más reciente esté instalado en los equipos cliente para garantizar un rendimiento óptimo del control remoto.|  

 Los dispositivos que ejecutan Windows Embedded, Windows Embedded para punto de servicio (POS) y Windows Fundamentals for Legacy PCs no admiten el visor de control remoto, pero admiten el cliente de control remoto.  

 El control remoto de Configuration Manager no se puede usar para administrar de forma remota los equipos cliente que ejecuten Systems Management Server 2003 o Configuration Manager 2007.  

> [!NOTE]  
>  No hay servicios de Windows son necesarios como una dependencia externa para el control remoto.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Sistemas operativos compatibles con el visor de control remoto  
El Visor de control remoto se admite en todos los sistemas operativos compatibles con la consola de Configuration Manager. Para más información, vea [Configuraciones compatibles con las consolas de System Center Configuration Manager](../../../../core/plan-design/configs/supported-operating-systems-consoles.md).   

## <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  

|Dependencia|Más información|  
|----------------|----------------------|  
|El control remoto debe habilitarse para los clientes|De forma predeterminada, el control remoto no está habilitado cuando se instala Configuration Manager. Para obtener información sobre cómo habilitar y configurar el control remoto, consulte [Configuración del control remoto en System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Punto de servicios de informes|El rol de sistema de sitio de punto de servicios de informes debe instalarse antes de poder ejecutar informes para el control remoto. Para obtener más información, consulte [Reporting in System Center Configuration Manager](../../../../core/servers/manage/reporting.md) (Generación de informes en System Center Configuration Manager).|  
|Permisos de seguridad para administrar el control remoto|Para acceder a recursos de la colección e iniciar una sesión de control remoto desde la consola de Configuration Manager: permiso **Leer**, **Leer recurso** y **Control remoto** para el objeto **Recopilación**.<br /><br /> El rol de seguridad **Operador de herramientas remotas** incluye estos permisos, que son necesarios para administrar el control remoto en Configuration Manager.<br /><br /> Para obtener más información, consulte [Configurar la administración basada en roles de System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Además, es necesario conceder permisos a los visores permitidos para usar el control remoto mediante la adición de estos usuarios a la lista **Visores permitidos de control remoto y asistencia remota** de la configuración del cliente **Herramientas remotas**.
